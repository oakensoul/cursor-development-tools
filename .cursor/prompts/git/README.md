# Declarative Git Workflows for Documentation

**Context-driven, declarative git workflow automation for documentation projects**

## 🎯 **Philosophy**

This system uses **declarative commands** rather than conversational help. Developers specify **what they want** (`@commit`, `@push`, `@pr`) and the system intelligently executes using project context and team standards.

## 🔐 **Authentication Requirements**

### **GitHub CLI Setup**
Some commands require GitHub CLI authentication:
```bash
# Check authentication status
gh auth status

# Login if needed
gh auth login
```

**Commands requiring authentication:**
- `@pr` - Pull request creation
- `@branch-protection` - Repository security setup

**Admin access required for:**
- `@branch-protection` - Setting up branch protection rules

## 📁 **Available Commands**

### **Complete Workflow Command**

#### **@shipit** - End-to-End Workflow Automation 🚀
```bash
@shipit                   # Auto-analyze changes and execute full workflow
@shipit "Custom description"  # Use custom commit/PR description
@shipit --direct         # Force direct push to main (skip PR)
@shipit --draft          # Create draft PR for work in progress
```
**Intelligence**: Complete automation from unstaged changes to PR creation. Auto-creates branches when needed, stages changes, commits with conventional messages, pushes, and creates PRs with appropriate reviewers.

### **Individual Workflow Commands**

#### **@commit** - Smart Commit Execution with Documentation Checking
```bash
@commit                    # Auto-analyze and commit current changes
@commit "fix broken links" # Commit with custom description  
@commit --amend           # Amend last commit with current changes
@commit --staged          # Commit only staged changes, ignore unstaged
@commit --all             # Include all unstaged changes without asking
@commit --split           # Force split into multiple atomic commits
@commit --no-doc-check    # Skip documentation impact analysis
```
**Intelligence**: Auto-detects scope, generates conventional commit messages, checks for documentation impact, handles staged/unstaged changes intelligently, suggests commit splitting when appropriate

#### **@push** - Intelligent Push Strategy
```bash
@push                     # Smart push based on context analysis
@push main               # Force push to main (with safety checks)
@push --pr              # Push branch and create PR
@push --sync            # Sync with remote first, then push
```
**Intelligence**: Decides direct-to-main vs feature-branch-PR based on change analysis

#### **@pr** - Auto-Generated Pull Requests
```bash
@pr                      # Auto-generate PR from branch commits
@pr "Custom Title"       # PR with custom title
@pr --draft             # Create draft PR for work in progress
@pr --reviewers @user1,@user2  # Specify custom reviewers
```
**Intelligence**: Generates descriptions, assigns reviewers, sets labels based on content type
**Requirements**: GitHub CLI authentication (`gh auth login`)

#### **@branch-protection** - Repository Security Setup
```bash
@branch-protection           # Set up standard protection for main branch
@branch-protection --branch develop  # Protect specific branch
@branch-protection --strict  # Maximum security settings
@branch-protection --minimal # Basic protection only
@branch-protection --check   # Verify current protection status
```
**Intelligence**: Applies workflow-rules.yml protection requirements, verifies admin access, provides status feedback
**Requirements**: GitHub CLI authentication + admin repository access

#### **@branch** - Branch Creation with Naming Conventions
```bash
@branch "section-name"        # Create docs branch with auto-naming
@branch "project-name" feature  # Create feature branch
@branch "fix-description" fix   # Create fix branch
@branch "name" --from main      # Create from specific base branch
```
**Intelligence**: Applies naming conventions and sets up tracking automatically

#### **@hotfix** - Emergency Hotfix Branch Creation 🚨
```bash
@hotfix "JIRA-123"           # Create hotfix from main for ticket
@hotfix "GH-456" abc1234     # Create hotfix from specific commit
@hotfix "broken-links"       # Create hotfix with descriptive name
@hotfix "urgent-fix" --base production  # Create from specific base branch
```
**Intelligence**: Creates emergency hotfix branches with proper naming and setup guidance for urgent documentation fixes

### **Advanced Workflow Command**

#### **@git-workflow** - Comprehensive Orchestration
```bash
@git-workflow commit     # Smart commit with full context analysis
@git-workflow push       # Push with comprehensive workflow routing
@git-workflow pr         # PR creation with advanced context integration
@git-workflow branch "name"  # Create branch with naming conventions
@git-workflow resolve   # Intelligent merge conflict resolution
@git-workflow sync      # Sync current branch with latest main
@git-workflow hotfix "JIRA-123" [commit]  # Create hotfix branch for urgent fixes
```
**Intelligence**: Full workflow orchestration with comprehensive reporting, including emergency hotfix support

## 🧠 **Context Intelligence**

All commands read from:
- **`../workflow-rules.yml`** - Structured workflow rules and team standards
- **`../ai-guidance.llms`** - Additional guidance and project wisdom
- **`../llms/`** - Generated LLM context files for instant project understanding

## 📚 **Documentation Impact Checking**

The `@commit` command now includes intelligent documentation impact analysis:

### **Automatic Documentation Analysis**
```yaml
High Priority (Always Check):
- New team members → Check team rosters, org charts
- Process changes → Check workflow documentation
- Architecture updates → Check technical documentation
- Tool/stack changes → Check setup instructions
- Onboarding changes → Check roadmaps, checklists

Medium Priority (Conditional Check):  
- Business context updates → Check stakeholder docs
- Analytics standards → Check related documentation
- Structure changes → Check navigation, README files

Low Priority (Optional):
- Minor content updates → Usually self-contained
- Typo fixes → No cross-references needed
```

### **Interactive Documentation Flow**
When documentation impact is detected:
```bash
📚 DOCUMENTATION CHECK
Your changes may impact documentation:

✅ Changes detected:
- New team member added (team/members/john-doe.md)
- Onboarding process updated (onboarding/first-day-setup.md)

🔍 Suggested documentation updates:
- team/README.md (team roster may need updating)
- onboarding/README.md (process flow references)
- README.md (main onboarding links)

📝 Actions:
[u] Update suggested docs now
[r] Review suggestions and decide
[s] Skip - commit anyway  
[c] Cancel commit to update manually
```

### **Auto-Detection Examples**

#### **Commit Message Generation**
```yaml
Files changed: onboarding/README.md → docs(onboarding): [description]
Files changed: team/structure.md → docs(team): [description]  
Change type: bug fix → fix(scope): [description]
Change type: new content → feat(scope): [description]
```

#### **Push Strategy Selection**
```yaml
Small changes + single file → Direct to main
New major content + multi-file → Feature branch + PR
Business context changes → Requires stakeholder review
Collaborative branch → Sync first, coordinate push
```

#### **Reviewer Assignment**
```yaml
onboarding changes → manager + recent_new_hire
business context → stakeholder_contact  
technical architecture → senior_engineer
team processes → team_lead
cross-functional → multiple reviewers
```

## 🔄 **Context Update Integration**

### **Automatic Context Detection**
All git commands automatically detect changes to `workflow-rules.yml` and offer to regenerate LLM context files:

```bash
# When workflow-rules.yml is modified:
@commit                     # → Offers to update context before committing
@shipit                     # → Auto-detects and includes context updates
@pr                         # → Checks context and adds context reviewers
```

### **Force Context Updates**
```bash
@commit --update-context    # Force context regeneration before commit
@shipit --update-context    # Force context update in full workflow
@pr --update-context        # Force context update before PR creation
```

### **Context Update Benefits**
- **Consistent AI behavior** - Context files keep all LLMs aligned with current project state
- **Automatic maintenance** - No manual updating of context when project evolves
- **Review integration** - PRs with context changes get appropriate expert reviewers
- **Cross-project portability** - Same system works for all repositories

## 🔄 **Workflow Patterns**

### **Complete Workflow (Recommended)**
```bash
# Edit files, then ship it!
@shipit  # → Auto-analyzes, creates branch if needed, commits, pushes, creates PR

# Quick fixes
@shipit "fix broken links"  # → Direct to main for simple changes

# Work in progress
@shipit --draft  # → Creates draft PR for ongoing collaboration
```

### **Step-by-Step Workflow (When you need control)**
```bash
# Traditional approach with individual commands
@commit "add dashboard creation guide"  
@push  # → Analyzes: substantial new content, suggests PR
@pr    # → Creates comprehensive PR with auto-generated description
```

### **Collaborative Project**
```bash
# Start collaborative work...
@git-workflow branch "team-documentation-update"
# Work with team...
@shipit --draft   # → Keeps everything in sync with draft PR
```

### **Emergency Hotfix**
```bash
# Critical issue reported
@git-workflow hotfix "JIRA-456"  # → Creates hotfix/JIRA-456-urgent-fix from main
# OR from specific commit
@git-workflow hotfix "GH-789" abc1234  # → Creates hotfix from specific commit

# Fix the issue, then fast-track
@shipit --direct "fix critical stakeholder blocking issue"
```

## 📊 **Output Examples**

### **Successful Commit**
```
✅ COMMITTED: docs(architecture): update Snowflake configuration details
📁 Files: architecture/data-stack.md
🎯 Type: Documentation update (direct to main appropriate)
📋 Next: Ready to push (@push)
```

### **Commit with Documentation Impact**
```
📚 DOCUMENTATION CHECK: Impact detected
🔍 Changes: New team member (team/members/jane-smith.md)
📝 Suggested updates: team/README.md, README.md (team size)
✅ User chose: Update suggested docs
📝 Updated: team/README.md (added to roster)
📝 Updated: README.md (team size 3→4)
✅ COMMITTED: feat(team): add Jane Smith as Senior Data Engineer
📁 Files: team/members/jane-smith.md, team/README.md, README.md
🎯 Type: New team member with documentation sync
📋 Next: Ready to push (@push)
```

### **Multiple Commits (Split)**
```
📊 ANALYSIS: Changes span 3 scopes, suggesting split
✅ User chose: Split into separate commits
✅ COMMITTED (1/3): docs(setup): add comprehensive project setup tasks
📁 Files: onboarding/first-day-setup.md
✅ COMMITTED (2/3): docs(team): update team structure documentation  
📁 Files: team/README.md
✅ COMMITTED (3/3): docs(tooling): enhance commit prompt with doc checking
📁 Files: .cursor/prompts/git/commit.mdc
🎯 Summary: 3 logical commits created for better history
📋 Next: Ready to push (@push)
```

### **Smart Push Decision**
```
✅ PUSHED: feature/onboarding-improvements to remote
📝 Commits: 3 commits with new troubleshooting guide
🎯 Strategy: Feature branch (substantial changes detected)
📋 Next: Use '@pr' to create pull request for team review
👥 Suggested Reviewers: manager, recent_new_hire
```

### **Auto-Generated PR**
```
✅ CREATED: Pull Request #42
📝 Title: docs(onboarding): add comprehensive setup troubleshooting guide
🔗 URL: https://github.com/oakensoul/cursor-development-tools/pull/42
👥 Reviewers: @manager, @recent-new-hire
🏷️ Labels: documentation, onboarding
📋 Status: Ready for review
```

## 🎯 **Advantages Over Previous System**

### **Developer Experience**
- **Declarative**: Say what you want, not how to do it
- **Context-aware**: Follows team-specific patterns automatically
- **Consistent**: Same quality output every time
- **Fast**: No decision fatigue or process lookup
- **Documentation-aware**: Automatically detects when docs need updating
- **Intelligent splitting**: Suggests atomic commits for better history

### **Maintainability**
- **Single source of truth**: Update context files, not multiple prompts
- **Easy customization**: Team standards centralized in YAML/LLMs files
- **Self-documenting**: Context files document current practices
- **Extensible**: Add new patterns without creating new prompts

### **Team Coordination**
- **Automatic decisions**: Right workflow for the situation
- **Consistent quality**: Standardized commit messages and PR descriptions
- **Appropriate collaboration**: PR vs direct push based on content analysis
- **Smart reviewer assignment**: Right people for the content type
- **Documentation consistency**: Prevents outdated cross-references and broken documentation
- **Change impact awareness**: Surfaces related documentation that needs updating

## 🔄 **Migration from Previous System**

### **Old → New Command Mapping**
```yaml
git-branch-create.mdc → @git-workflow branch "name"
git-code-prep.mdc → Built into @commit validation
git-code-commit.mdc → @commit
git-code-push.mdc → @push  
git-pr-create.mdc → @pr
git-conflicts-fix.mdc → @git-workflow resolve
```

### **Benefits of Migration**
- ✅ **Simplified interface**: 4 main commands vs 6 separate prompts
- ✅ **Enhanced intelligence**: Context-driven decisions vs manual choices
- ✅ **Better integration**: Seamless handoffs between workflow steps
- ✅ **Reduced maintenance**: Update context files, not individual prompts

## 🚀 **Getting Started**

1. **Use simple commands**: Start with `@commit` and `@push`
2. **Trust the intelligence**: Let the system make workflow decisions
3. **Customize context**: Update `project-context.yml` for team needs
4. **Provide feedback**: Help improve the context and decision logic

---

**This declarative system provides the speed of informal workflows with the consistency of formal process - the best of both worlds for documentation teams!**