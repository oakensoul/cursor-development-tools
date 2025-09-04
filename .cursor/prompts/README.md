# Cursor AI Prompts for Documentation Project

**Context-driven, declarative workflow automation for documentation development**

## 🎯 Purpose

These prompts provide **declarative command interfaces** for common documentation tasks, enabling AI tools to execute workflows intelligently based on project context and team standards.

## 📁 Prompt Categories

All prompts are discoverable through Cursor's @ command interface. Type `@` and start typing the command name to see available options.

### [Git Workflows](./git/) - **Primary Workflow System**
Declarative git commands that read project context and execute intelligently:

- **[@shipit](./git/shipit.mdc)** - 🚀 Complete end-to-end workflow automation (recommended)
- **[@commit](./git/commit.mdc)** - Smart commit execution with auto-generated conventional messages
- **[@push](./git/push.mdc)** - Intelligent push strategy (direct-to-main vs feature-branch-PR)
- **[@pr](./git/pr.mdc)** - Auto-generated pull requests with descriptions and reviewers
- **[@branch](./git/branch.mdc)** - Branch creation with naming convention auto-application
- **[@hotfix](./git/hotfix.mdc)** - 🚨 Emergency hotfix branch creation for urgent fixes
- **[@git-workflow](./git/git-workflow.mdc)** - Comprehensive workflow orchestration

### [Context Generation](./context/) - **LLM Context Management**
Automated generation of LLM context files from project configuration:

- **[@update-context](./context/update-context.mdc)** - 🔄 Regenerate all LLM context files from workflow-rules.yml
- **[@generate-project-overview](./context/generate-project-overview.mdc)** - Generate project overview context
- **[@generate-business-context](./context/generate-business-context.mdc)** - Generate business and stakeholder context
- **[@generate-tech-stack](./context/generate-tech-stack.mdc)** - Generate technology stack context
- **[@generate-team-context](./context/generate-team-context.mdc)** - Generate team collaboration context

### [Configuration Management](./config/) - **Foundation File Management**
Create and maintain the core configuration files that drive the entire AI system:

- **[@init-workflow-rules](./config/init-workflow-rules.mdc)** - 🆕 Initialize workflow-rules.yml for new projects
- **[@update-workflow-rules](./config/update-workflow-rules.mdc)** - 🔄 Update workflow-rules.yml for team/tech/process changes
- **[@init-ai-guidance](./config/init-ai-guidance.mdc)** - 🆕 Initialize ai-guidance.llms for new projects
- **[@update-ai-guidance](./config/update-ai-guidance.mdc)** - 🔄 Update ai-guidance.llms with team insights and learnings

### Future Prompt Categories *(Planned)*
- **Documentation Generation** - Content creation and improvement workflows
- **Review Automation** - Systematic documentation review and feedback
- **Maintenance Tasks** - Keeping documentation current and organized

## 🧠 **Intelligence Layer**

All prompts are powered by context files that define team standards and project-specific guidance:

### **[project-context.yml](../project-context.yml)** - Structured Rules
```yaml
# Example: Auto-commit message generation
git:
  commit_convention:
    format: "{type}({scope}): {description}"
    scopes: ["onboarding", "team", "architecture", "stakeholders"]
  
  branching:
    substantial_changes: "docs/{section-name}"
    collaborative_work: "feature/{project-name}"
```

### **[context.llms](../context.llms)** - AI Guidance
```markdown
# Example: Workflow intelligence
This is a documentation repository for data engineering team onboarding.
Focus on clarity and usability over perfection.
Use real project examples when possible.
```

## 🔄 **Declarative Usage Patterns**

### **Individual Documentation Work**
```bash
# The easy way - complete automation
@shipit  # → Auto-handles everything: stage, commit, branch, push, PR

# Quick fixes  
@shipit "fix broken links"  # → Direct to main for simple changes

# Custom workflow when you need control
@commit "add new troubleshooting guide"
@push  # → Analyzes: new content, suggests feature branch + PR
@pr    # → Auto-generates comprehensive PR
```

### **Collaborative Documentation**
```bash
# Start collaborative project
@branch "team-onboarding-restructure" feature
@commit "initial restructuring plan"
@push --sync  # → Coordinates with team collaboration
```

### **Context-Driven Decisions**
```bash
# System reads context and decides:
@push  # → "This is substantial content, creating PR for review"
@pr    # → "Onboarding content detected, assigning manager + new_hire reviewers"
```

## 🎯 **Key Advantages**

### **Declarative Interface**
- **Say what you want**: `@commit`, `@push`, `@pr`
- **Not how to do it**: No need to remember process details
- **Context-aware execution**: Smart decisions based on project standards

### **Intelligent Automation**
- **Auto-generated content**: Commit messages, PR descriptions, reviewer assignments
- **Workflow routing**: Direct-to-main vs feature-branch-PR based on change analysis
- **Quality integration**: Built-in validation and team standard compliance

### **Maintainable Standards**
- **Single source of truth**: Update context files, not individual prompts
- **Team customization**: Project-specific rules and conventions
- **Evolution friendly**: Easy to adapt as team practices change

## 📊 **Migration from Previous System**

### **Old Conversational → New Declarative**
```yaml
Before: "How do I commit these changes? Should I create a PR? How do I write a good description?"
Now:    "@shipit" (handles everything automatically)

Before: "How do I commit these changes?"
Now:    "@commit"

Before: "Should I create a PR or push directly?"  
Now:    "@push" (it decides automatically)

Before: "How do I write a good PR description?"
Now:    "@pr" (auto-generates from commits)
```

### **Coverage Verification**
All original use cases from the previous git prompt system are covered:
- ✅ **Branch creation** → `@branch` with naming conventions
- ✅ **Change preparation** → Built into `@commit` validation
- ✅ **Commit creation** → `@commit` with auto-generation
- ✅ **Push strategy** → `@push` with intelligent routing
- ✅ **PR creation** → `@pr` with comprehensive auto-generation
- ✅ **Conflict resolution** → `@git-workflow resolve`

## 🔍 **Prompt Discovery**

### **Finding Available Commands**
- **Type `@` in Cursor** - See all available prompts in the current project
- **Start typing command name** - Auto-complete will show matching commands
- **Browse directory READMEs** - Each prompt folder documents its commands
- **Check .mdc file headers** - Usage, tags, and context files listed

### **Command Categories Quick Reference**
```bash
# Git Workflows (most common daily use)
@shipit @commit @push @pr @branch @hotfix @git-workflow

# Context Management (keep AI understanding current)
@update-context @generate-project-overview @generate-business-context 
@generate-tech-stack @generate-team-context

# Configuration Management (setup and maintenance)
@init-workflow-rules @update-workflow-rules @init-ai-guidance @update-ai-guidance
```

## 🚀 **Getting Started**

### **For New Users**
1. **Start simple**: Use `@commit` and `@push` for basic workflow
2. **Trust the intelligence**: Let the system make appropriate decisions
3. **Review context files**: Understand your team's standards and conventions
4. **Provide feedback**: Help improve the decision logic and context

### **For Advanced Users**
1. **Customize context**: Update `project-context.yml` for team-specific needs
2. **Extend workflows**: Add new patterns to context without creating new prompts
3. **Integrate with tools**: Use context files with other development tools
4. **Share patterns**: Adapt successful patterns for other projects

## 🔧 **Development & Maintenance**

### **Context File Updates**
- **project-context.yml**: Structured rules for workflows, naming, and standards
- **context.llms**: Natural language guidance and project-specific wisdom
- **Prompt files**: Generally stable, read context for current standards

### **Adding New Workflows**
1. **Identify pattern**: New repetitive workflow or decision point
2. **Update context**: Add rules to project-context.yml or guidance to context.llms
3. **Test with existing prompts**: Often no new prompt file needed
4. **Create specialized prompt**: Only if context-driven approach insufficient

### **Quality Assurance**
- **Test workflows**: Validate that declarative commands work as expected
- **Monitor effectiveness**: Track usage patterns and team satisfaction
- **Iterate context**: Improve decision logic based on real usage
- **Document learnings**: Capture new patterns and edge cases

## 🔗 Integration with Project

### **Documentation Standards**
These prompts work together with:
- [Documentation Style Rules](../rules/documentation-style.mdc)
- [Onboarding Content Standards](../rules/onboarding-content.mdc)
- [Business Context Guidelines](../rules/business-context.mdc)
- [Technical Documentation Standards](../rules/technical-documentation.mdc)

### **Team Workflows**
Prompts support:
- Individual contributor documentation work
- Collaborative team documentation projects  
- Onboarding new team members to documentation practices
- Maintaining quality and consistency across all documentation

---

*This declarative prompt system provides the speed of informal workflows with the consistency of formal processes - optimized for documentation team productivity and collaboration.*