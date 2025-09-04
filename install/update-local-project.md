---
name: "update-cursor-tools"
description: "Update local .cursor system with latest templates from cursor-development-tools"
author: "@oakensoul"
version: "1.0.0"
tags: ["update", "maintenance", "cursor-system", "templates"]
---

# 🔄 Cursor Development Tools Updater

Updates your local `.cursor` system with the latest templates and workflows from the cursor-development-tools repository while preserving your project-specific context files.

## 🎯 What This Does

### **Updates (Overwrites):**
- Core prompt templates (`.cursor/prompts/**/*.mdc`)
- System rules (`.cursor/rules/*.mdc`) 
- Configuration templates (`.cursor/prompts.json`)
- Documentation (`.cursor/README.md`, `.cursor/SETUP.md`, `.cursor/USAGE.md`)

### **Preserves (Never Touches):**
- Your context files (`.cursor/llms/*.llms`)
- Your project configuration (`.cursor/workflow-rules.yml`, `.cursor/ai-guidance.llms`)
- Any custom prompts you've added
- Your project-specific customizations

## 🚀 Usage

```bash
# Run this prompt directly from the GitHub URL
# Replace the path with your actual project directory
@cursor-update
```

## 📋 Pre-Execution Checklist

1. **Backup your customizations** (optional but recommended)
2. **Commit any pending changes** to your repository
3. **Verify internet connection** for GitHub access

## 🔧 Execution Protocol

### Step 1: Environment Setup
```bash
# Set up temporary directory for download
TEMP_DIR=$(mktemp -d)
CURSOR_DIR=".cursor"
REPO_URL="https://github.com/oakensoul/cursor-development-tools"

echo "🔄 UPDATING: Cursor Development Tools"
echo "📁 Target: $(pwd)/$CURSOR_DIR"
echo "🌐 Source: $REPO_URL"
echo ""
```

### Step 2: Fetch Available Releases
```bash
# Get list of available releases from GitHub API
echo "🔍 FETCHING: Available releases..."
RELEASES_JSON=$(curl -s "https://api.github.com/repos/oakensoul/cursor-development-tools/releases" 2>/dev/null)

if [ $? -ne 0 ] || [ -z "$RELEASES_JSON" ]; then
    echo "❌ FAILED: Could not fetch releases from GitHub API"
    echo "🔧 Check: Internet connection and GitHub API access"
    exit 1
fi

# Parse releases and create selection menu
RELEASE_TAGS=$(echo "$RELEASES_JSON" | grep '"tag_name"' | cut -d'"' -f4 | head -10)
RELEASE_NAMES=$(echo "$RELEASES_JSON" | grep '"name"' | cut -d'"' -f4 | head -10)

if [ -z "$RELEASE_TAGS" ]; then
    echo "❌ FAILED: No releases found in repository"
    echo "🔧 Check: Repository has published releases"
    exit 1
fi

# Display available releases
echo "📋 AVAILABLE RELEASES:"
echo ""
counter=1
while IFS= read -r tag && IFS= read -r name <&3; do
    echo "$counter) $tag - $name"
    counter=$((counter + 1))
done <<< "$RELEASE_TAGS" 3<<< "$RELEASE_NAMES"

echo ""
echo "0) Latest release ($(echo "$RELEASE_TAGS" | head -1))"
echo ""

# Get user selection
read -p "🎯 SELECT: Which version to install? (0-$((counter-1)), or Enter for latest): " selection

# Determine selected release
if [ -z "$selection" ] || [ "$selection" = "0" ]; then
    SELECTED_TAG=$(echo "$RELEASE_TAGS" | head -1)
    echo "✅ SELECTED: Latest release ($SELECTED_TAG)"
else
    if [ "$selection" -ge 1 ] && [ "$selection" -lt "$counter" ]; then
        SELECTED_TAG=$(echo "$RELEASE_TAGS" | sed -n "${selection}p")
        echo "✅ SELECTED: Release $SELECTED_TAG"
    else
        echo "❌ INVALID: Selection out of range"
        exit 1
    fi
fi
```

### Step 3: Download Selected Release
```bash
# Download the selected release
echo "📥 DOWNLOADING: Release $SELECTED_TAG..."

# Try to download release tarball first (more reliable)
RELEASE_URL="https://github.com/oakensoul/cursor-development-tools/archive/refs/tags/$SELECTED_TAG.tar.gz"
curl -L -s "$RELEASE_URL" | tar -xz -C "$TEMP_DIR" 2>/dev/null

if [ $? -eq 0 ]; then
    # Find the extracted directory (should be cursor-development-tools-{tag})
    EXTRACTED_DIR=$(find "$TEMP_DIR" -name "cursor-development-tools-*" -type d | head -1)
    if [ -n "$EXTRACTED_DIR" ]; then
        mv "$EXTRACTED_DIR" "$TEMP_DIR/cursor-tools"
        echo "✅ DOWNLOADED: Release $SELECTED_TAG (tarball)"
    else
        echo "⚠️  TARBALL: Extraction failed, trying git clone..."
        # Fallback to git clone with specific tag
        git clone --depth 1 --branch "$SELECTED_TAG" "$REPO_URL" "$TEMP_DIR/cursor-tools" 2>/dev/null || {
            echo "❌ FAILED: Could not download release $SELECTED_TAG"
            echo "🔧 Check: Internet connection and release availability"
            exit 1
        }
        echo "✅ DOWNLOADED: Release $SELECTED_TAG (git)"
    fi
else
    echo "⚠️  TARBALL: Download failed, trying git clone..."
    # Fallback to git clone with specific tag
    git clone --depth 1 --branch "$SELECTED_TAG" "$REPO_URL" "$TEMP_DIR/cursor-tools" 2>/dev/null || {
        echo "❌ FAILED: Could not download release $SELECTED_TAG"
        echo "🔧 Check: Internet connection and release availability"
        exit 1
    }
    echo "✅ DOWNLOADED: Release $SELECTED_TAG (git)"
fi
```

### Step 4: Backup Current System (Optional)
```bash
# Create backup of current .cursor directory
if [ -d "$CURSOR_DIR" ]; then
    BACKUP_DIR=".cursor-backup-$(date +%Y%m%d-%H%M%S)"
    echo "💾 BACKUP: Creating backup at $BACKUP_DIR"
    cp -r "$CURSOR_DIR" "$BACKUP_DIR"
    echo "✅ BACKUP: Created at $BACKUP_DIR"
fi
```

### Step 5: Selective File Updates
```bash
# Define core files to update (preserve user context)
CORE_FILES=(
    "prompts/git/"
    "prompts/config/"
    "prompts/context/"
    "prompts/README.md"
    "prompts.json"
    "rules/"
    "README.md"
    "SETUP.md" 
    "USAGE.md"
    "PROJECT-TYPES.md"
)

# Create .cursor directory if it doesn't exist
mkdir -p "$CURSOR_DIR"

# Update each core component
for file_path in "${CORE_FILES[@]}"; do
    source_path="$TEMP_DIR/cursor-tools/.cursor/$file_path"
    target_path="$CURSOR_DIR/$file_path"
    
    if [ -e "$source_path" ]; then
        echo "🔄 UPDATING: .cursor/$file_path"
        
        # Create target directory if needed
        mkdir -p "$(dirname "$target_path")"
        
        # Copy file or directory
        if [ -d "$source_path" ]; then
            # Directory: remove old, copy new
            [ -d "$target_path" ] && rm -rf "$target_path"
            cp -r "$source_path" "$target_path"
        else
            # File: direct copy
            cp "$source_path" "$target_path"
        fi
        
        echo "✅ UPDATED: .cursor/$file_path"
    else
        echo "⚠️  SKIPPED: .cursor/$file_path (not found in source)"
    fi
done
```

### Step 6: Preserve User Context
```bash
# Ensure user context directories exist but don't overwrite content
USER_DIRS=(
    "llms"
)

for dir_name in "${USER_DIRS[@]}"; do
    user_dir="$CURSOR_DIR/$dir_name"
    
    if [ ! -d "$user_dir" ]; then
        echo "📁 CREATING: .cursor/$dir_name directory"
        mkdir -p "$user_dir"
        
        # Copy README if it exists, but not context files
        if [ -f "$TEMP_DIR/cursor-tools/.cursor/$dir_name/README.md" ]; then
            cp "$TEMP_DIR/cursor-tools/.cursor/$dir_name/README.md" "$user_dir/"
            echo "✅ ADDED: .cursor/$dir_name/README.md"
        fi
    else
        echo "🔒 PRESERVED: .cursor/$dir_name (existing content kept)"
    fi
done
```

### Step 7: Update Check & Validation
```bash
# Verify core files were updated
echo ""
echo "🔍 VALIDATION: Checking updated files..."

validation_files=(
    ".cursor/prompts/git/commit.mdc"
    ".cursor/prompts.json"
    ".cursor/README.md"
)

all_valid=true
for file in "${validation_files[@]}"; do
    if [ -f "$file" ]; then
        echo "✅ VERIFIED: $file"
    else
        echo "❌ MISSING: $file"
        all_valid=false
    fi
done

if [ "$all_valid" = true ]; then
    echo "✅ VALIDATION: All core files successfully updated"
else
    echo "⚠️  VALIDATION: Some files may not have updated correctly"
fi
```

### Step 7: Cleanup & Summary
```bash
# Remove temporary directory
rm -rf "$TEMP_DIR"

echo ""
echo "🎉 UPDATE COMPLETE!"
echo ""
echo "📊 SUMMARY:"
echo "✅ Updated: Core prompt templates and rules"
echo "✅ Updated: System documentation"
echo "🔒 Preserved: Your context files and configurations"
echo ""

# Show backup info if created
if [ -n "$BACKUP_DIR" ] && [ -d "$BACKUP_DIR" ]; then
    echo "💾 Backup: $BACKUP_DIR"
    echo "   (can be removed if everything works correctly)"
    echo ""
fi

echo "🚀 NEXT STEPS:"

# Check if this is a new installation or update
if [ ! -f ".cursor/workflow-rules.yml" ]; then
    echo ""
    echo "🆕 NEW INSTALLATION DETECTED"
    echo "The system templates are installed, but you need to configure for your project:"
    echo ""
    echo "1. Read the setup guide: .cursor/SETUP.md"
    echo "2. Run: @init-workflow-rules (analyze your project)"
echo "3. Run: @init-ai-guidance (create AI decision context)"
echo "4. Run: @update-context (generate project context files)"
echo "5. Test: Try '@commit --dry-run' or ask AI to explain your workflow-rules.yml"
    echo ""
    echo "📖 Complete setup instructions: .cursor/SETUP.md"
else
    echo ""
    echo "🔄 EXISTING INSTALLATION UPDATED"
    echo "Your project configuration is preserved. Optional steps:"
    echo ""
    echo "1. Test your cursor prompts to ensure they work correctly"
    echo "2. Review any new features in .cursor/README.md"
    echo "3. Update your workflow-rules.yml if new fields were added"
    echo "4. Run @update-context to refresh LLM context files if needed"
    echo ""
fi

echo "📖 Documentation: .cursor/README.md"
echo "🔧 Setup Guide: .cursor/SETUP.md"
echo "💡 Daily Usage: .cursor/USAGE.md"
```

## 🔒 Safety Features

### **Selective Updates Only**
- Never overwrites user-generated context files
- Preserves project-specific configurations
- Only updates template and system files

### **Backup Creation**
- Automatically creates timestamped backup
- Easy rollback if issues occur
- Backup can be safely deleted after validation

### **Validation Checks**
- Verifies files were copied correctly
- Reports any missing critical files
- Provides clear success/failure feedback

## 🚨 Troubleshooting

### **Download Fails**
```bash
❌ FAILED: Could not download from GitHub
🔧 Solutions:
- Check internet connection
- Verify repository URL is accessible
- Try again in a few minutes
```

### **Permission Errors**
```bash
❌ FAILED: Permission denied
🔧 Solutions:
- Check file permissions in .cursor directory
- Ensure you have write access to project directory
- Try running with appropriate permissions
```

### **Missing Files After Update**
```bash
⚠️  VALIDATION: Some files may not have updated correctly
🔧 Solutions:
- Check backup directory for original files
- Re-run the update command
- Manually copy missing files from backup
```

## 🔄 Rollback Procedure

If you need to rollback the update:

```bash
# Find your backup directory
ls -la | grep cursor-backup

# Restore from backup (replace TIMESTAMP with actual timestamp)
rm -rf .cursor
mv .cursor-backup-TIMESTAMP .cursor

echo "✅ ROLLBACK: Restored from backup"
```

## 📝 Version Compatibility

This updater is designed to be forward-compatible:
- **Preserves** existing user content
- **Adds** new template features
- **Updates** existing templates to latest versions
- **Maintains** backward compatibility with older configurations

## 🎯 Regular Maintenance

**Recommended Update Frequency:**
- **Monthly**: For active development projects
- **Quarterly**: For stable projects
- **As needed**: When new features are announced

**Before Major Updates:**
- Review release notes at the repository
- Backup your entire project (not just .cursor)
- Test in a non-production environment first

---

*This updater maintains the separation between the reusable cursor-development-tools template and your project-specific AI context, ensuring you get the latest workflow improvements without losing your customizations.*
