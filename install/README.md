# 📦 Installation & Update Scripts

This directory contains scripts for installing and updating the Cursor Development Tools system.

## 🔄 Available Scripts

### **update-local-project.md**
**Purpose**: Update your local `.cursor` system with the latest templates from this repository

**Features**:
- ✅ **Smart updates** - Only overwrites core template files
- 🔒 **Preserves your work** - Never touches your context files or configurations  
- 📋 **Release selection** - Choose which version to install
- 💾 **Automatic backups** - Creates timestamped backups before updating
- ✅ **Validation** - Checks that files updated correctly

**Usage via Cursor (Recommended)**:
```
Paste this into your Cursor chat:

Please read and explain the following installation script, highlighting any security considerations, and then (if I approve) execute it to add the cursor-development-tools system to my current repository: https://raw.githubusercontent.com/oakensoul/cursor-development-tools/main/install/update-local-project.md
```

**Usage via command line**:
```bash
# If you prefer running directly in terminal
bash <(curl -s https://raw.githubusercontent.com/oakensoul/cursor-development-tools/main/install/update-local-project.md)
```

**Usage from local copy**:
```bash
# If you have this repo cloned locally
bash ./install/update-local-project.md
```

## 🎯 What Gets Updated vs Preserved

### **Updated (Overwritten)**:
- `.cursor/prompts/git/` - Git workflow prompts
- `.cursor/prompts/config/` - Configuration prompts  
- `.cursor/prompts/context/` - Context generation prompts
- `.cursor/rules/` - AI behavior rules
- `.cursor/README.md`, `.cursor/SETUP.md`, `.cursor/USAGE.md` - Documentation
- `.cursor/prompts.json` - Prompt registry

### **Preserved (Never Touched)**:
- `.cursor/llms/*.llms` - Your generated context files
- `.cursor/workflow-rules.yml` - Your project configuration
- `.cursor/ai-guidance.llms` - Your project-specific AI guidance
- Any custom prompts you've added outside the core directories

## 🚀 Recommended Workflow

1. **Initial Setup**: Copy `.cursor/` folder to your project manually
2. **Configure**: Set up your `workflow-rules.yml` and generate context
3. **Stay Updated**: Use `update-local-project.md` periodically to get latest improvements
4. **Customize**: Add your own prompts and rules as needed

## 🔒 Safety Features

- **Automatic backups** before any changes
- **Validation checks** to ensure update success
- **Easy rollback** if something goes wrong
- **Selective updates** to protect your customizations

## 🆘 Support

If you encounter issues with the update scripts:

1. **Check the backup** - Every update creates a timestamped backup
2. **Review the validation** - Script reports what succeeded/failed
3. **Manual rollback** - Restore from backup if needed
4. **Report issues** - Create an issue in the repository

## 📝 Version Notes

The update script automatically:
- Fetches available releases from GitHub
- Lets you choose which version to install
- Downloads only the specific release (not development code)
- Validates that the selected release contains expected files

This ensures you're always getting stable, tested versions of the cursor tools.

---

*For detailed usage instructions, see the individual script files or the main repository README.*
