# Daily Usage Guide: AI-Enhanced Development Workflows

Complete reference for using the AI-powered development system in your daily work.

## 🔄 Daily Workflow Commands

Once the system is set up, your team uses these AI-powered workflows:

### **Smart Development**
```bash
@shipit         # Full workflow: stage, commit, push with AI assistance*
@commit         # Smart commit messages based on changes and context
@branch         # Create contextual branches with proper naming
@pr             # Generate pull requests with context-aware descriptions*
```
*_GitHub only: `@pr` and `@shipit` (with PR creation) require GitHub repos and GitHub CLI (`gh`) authentication. Other platforms support `@commit`, `@branch`, and `@push` only._

### **Context Management**
```bash
@update-context        # Refresh all context when project evolves
@update-workflow-rules # Update configuration for team/tech changes
@update-ai-guidance    # Refine AI decision-making based on learnings
```

## 🎯 For Team Members Using This System

### **For New Team Members**
1. **Read** `workflow-rules.yml` to understand project standards
2. **Explore** `llms/project-overview.llms` for learning roadmap  
3. **Test the system** with `@commit --dry-run` or ask AI to explain your workflow-rules.yml
4. **Reference** the README files when curious about how the system works

### **For Contributing to the System**
1. **Propose changes** to `workflow-rules.yml` for new standards
2. **Use** `@update-ai-guidance` to capture new team learnings
3. **Create custom prompts** for team-specific workflows - see [Customization Guide](#customization--extension)
4. **Add custom rules** for quality standards and team practices - see [Creating Custom Rules](#creating-custom-rules)
5. **Test workflows** in feature branches before merging
6. **Document insights** in team retrospectives for system improvement

## 📋 Troubleshooting Daily Usage

### **Common Workflow Issues**

#### **Git Workflow Problems**
```bash
# If @shipit fails:
- Ensure you're in git repository root
- Check that changes are staged or use @shipit --auto-stage
- Verify remote repository is configured

# If commits are poorly formatted:
- Check workflow-rules.yml for commit format standards
- Run @update-ai-guidance to refresh AI understanding
- Ensure context files are up to date
```

#### **Context Issues**
```bash
# If AI suggestions seem off-target:
@update-context  # Refresh project understanding

# If AI doesn't understand recent changes:
@update-workflow-rules  # Update project configuration

# If team processes have changed:
@update-ai-guidance  # Capture new team wisdom
```

#### **Command Not Working**
```bash
# If commands don't exist:
- Check .cursor/prompts.json for available commands
- Verify .cursor folder was copied completely
- Restart Cursor to refresh prompt catalog

# If prompts give errors:
- Check context files exist in .cursor/llms/
- Verify workflow-rules.yml was generated properly
- Try running setup steps again
```

### **Performance Issues**
```bash
# If commands are slow:
- Large repositories may take longer for context analysis
- Consider running @update-context periodically vs. every command
- Check if context files are extremely large (>50KB each)

# If context generation fails:
- Ensure sufficient disk space in .cursor/llms/ folder
- Check file permissions on .cursor directory
- Verify all required dependencies are available
```

## 🔧 System Maintenance

### **When to Update Context**
- **After major feature additions** - New capabilities change project scope
- **When team composition changes** - Different expertise and processes
- **During architecture evolution** - New tools, patterns, or standards
- **Quarterly reviews** - Keep context fresh and accurate

### **When to Update Configuration**
- **New team processes** - Updated git workflows, review standards
- **Technology changes** - New tools, languages, or frameworks
- **Business priority shifts** - Different stakeholder focus or success metrics
- **Quality standard evolution** - Updated coding standards or practices

### **Context File Management**
```bash
# Check context file sizes:
ls -la .cursor/llms/

# Files getting too large (>100KB)? Regenerate them:
@update-context

# Missing context files? Regenerate specific ones:
@generate-project-overview
@generate-business-context
@generate-tech-stack
@generate-team-context
```

## 💡 Pro Tips for Daily Usage

### **Efficient Workflows**
1. **Use @shipit for most commits** - It handles staging, committing, and pushing intelligently
2. **Branch early and often** - Use @branch for descriptive, contextual branch names
3. **Let AI write PR descriptions** - Use @pr for comprehensive pull request content
4. **Update context regularly** - Fresh context = better AI assistance

### **Team Collaboration**
1. **Share workflow learnings** - Update @update-ai-guidance with team insights
2. **Standardize on commands** - Consistent usage across team members
3. **Document customizations** - Note any project-specific adjustments
4. **Review context together** - Team reviews of generated context improve quality

### **Quality Assurance**
1. **Review AI suggestions** - Always validate commit messages and branch names
2. **Test workflows in feature branches** - Don't experiment directly on main
3. **Keep documentation current** - Update this guide based on team experience
4. **Monitor context accuracy** - Ensure AI understanding matches reality

## 🛠️ **Customization & Extension**

The cursor development tools are designed to be extended and customized for your specific needs.

### **Adding Custom Prompts**

**1. Create a New Prompt File:**
```bash
# Example: Add a custom deployment prompt
touch .cursor/prompts/deploy.mdc
```

**2. Prompt Structure:**
```markdown
---
name: "deploy"
description: "Smart deployment with environment validation"
author: "@your-username"
tags: ["deployment", "production", "validation"]
context_files: ["../workflow-rules.yml", "../ai-guidance.llms"]
---

# Smart Deployment Executor

Deploy applications with intelligent pre-flight checks and rollback capabilities.

## Command Format
- `@deploy staging` - Deploy to staging environment
- `@deploy production --validate` - Deploy to prod with extra validation
- `@deploy rollback` - Rollback last deployment

## Execution Protocol
1. **Environment Validation**: Check target environment health
2. **Pre-deployment Tests**: Run automated test suite
3. **Backup Creation**: Create rollback point
4. **Deployment Execution**: Deploy with monitoring
5. **Post-deployment Validation**: Verify deployment success
```

**3. Register the Prompt:**
Add to `.cursor/prompts.json`:
```json
{
  "prompts": [
    {
      "name": "deploy",
      "path": "prompts/deploy.mdc",
      "description": "Smart deployment with validation"
    }
  ]
}
```

### **Creating Custom Rules**

**1. Add a New Rule File:**
```bash
# Example: Add API documentation standards
touch .cursor/rules/api-documentation.mdc
```

**2. Rule Structure:**
```markdown
---
name: "api-documentation"
description: "Standards for API documentation and OpenAPI specs"
scope: "api_content"
author: "@your-username"
---

# API Documentation Standards

## Context
This rule applies when creating or editing API documentation, OpenAPI specifications, and endpoint descriptions.

## Standards
- Use OpenAPI 3.0+ specification format
- Include example requests and responses for all endpoints
- Document all error codes and response formats
- Provide clear parameter descriptions with validation rules

## Quality Checklist
- [ ] All endpoints have summary and description
- [ ] Request/response schemas are complete
- [ ] Authentication requirements documented
- [ ] Rate limiting information included
- [ ] Example usage provided
```

### **Updating Project Configuration**

**Edit Workflow Rules:**
```bash
# Use the built-in prompt to update configuration
@update-workflow-rules
```

Or edit directly:
```yaml
# .cursor/workflow-rules.yml
project:
  name: "Your Project Name"
  type: "web-application"  # or api, library, mobile-app, etc.
  
team:
  size: 5
  roles: ["frontend", "backend", "devops", "qa", "design"]
  
git:
  branch_protection: true
  require_pr_reviews: 2
  conventional_commits: true
  
quality:
  linting: true
  testing_required: true
  code_coverage_minimum: 80
  
deployment:
  environments: ["development", "staging", "production"]
  auto_deploy_staging: true
  manual_deploy_production: true
```

### **Generating Custom Context**

**Update AI Context Files:**
```bash
# Regenerate all context files from updated rules
@update-context

# Or generate specific context types
@generate-business-context
@generate-tech-stack  
@generate-team-context
@generate-project-overview
```

**Manual Context Editing:**
```markdown
# .cursor/ai-guidance.llms

# Custom AI Guidance for [Your Project]

## Project-Specific Considerations
- Our codebase uses microservices architecture
- We prioritize performance over rapid prototyping
- Security compliance is critical (SOC2, HIPAA)
- Team prefers TypeScript over JavaScript

## Decision Frameworks
When suggesting technical solutions:
1. Consider impact on existing microservices
2. Evaluate security implications first  
3. Prefer strongly-typed solutions
4. Factor in deployment complexity

## Communication Style
- Be direct and technical with senior developers
- Provide more context and examples for junior developers
- Always explain security implications
- Include performance considerations
```

### **Advanced Customization**

**1. Environment-Specific Prompts:**
```bash
# Create environment-specific variations
.cursor/prompts/git/commit-staging.mdc
.cursor/prompts/git/commit-production.mdc
```

**2. Team Role-Specific Rules:**
```bash
# Different rules for different team roles
.cursor/rules/frontend-standards.mdc
.cursor/rules/backend-standards.mdc  
.cursor/rules/qa-testing-standards.mdc
```

**3. Integration-Specific Context:**
```markdown
# .cursor/llms/integrations-context.llms

# Third-Party Integrations

## Payment Processing
- Stripe for recurring subscriptions
- PayPal for one-time payments
- Handle PCI compliance requirements

## Authentication
- Auth0 for user management
- SAML SSO for enterprise customers
- MFA required for admin accounts
```

### **Maintenance & Updates**

**Regular Maintenance Tasks:**
```bash
# Keep context current (run monthly)
@update-context

# Review and update rules (run quarterly)  
@update-workflow-rules

# Update AI guidance (as team/project evolves)
@update-ai-guidance
```

**Version Control Best Practices:**
- Commit `.cursor/workflow-rules.yml` - shared team configuration
- Commit `.cursor/prompts/` and `.cursor/rules/` - shared team workflows  
- Consider gitignoring `.cursor/llms/` - context files can be regenerated
- Document custom prompts in your project README

### **Testing Custom Prompts**

**1. Start Simple:**
```markdown
# Test basic prompt execution
@your-custom-prompt --dry-run
```

**2. Validate with Team:**
- Have team members test new prompts
- Gather feedback on prompt clarity and usefulness
- Iterate based on real usage patterns

**3. Monitor Usage:**
- Track which custom prompts get used most
- Identify prompts that need refinement
- Remove unused prompts to keep system clean

## 🔄 Advanced Usage Patterns

### **Hotfix Workflows**
```bash
@hotfix         # Emergency branch creation and workflow
# Follow with standard @commit and @pr for urgent fixes
```

### **Context-Aware Development**
```bash
# Before major changes, refresh understanding:
@update-context

# After major changes, update configuration:
@update-workflow-rules
@update-ai-guidance
```

### **Cross-Project Consistency**
- **Use same commands** across all projects with this system
- **Share workflow-rules.yml patterns** for similar project types
- **Document team-specific customizations** for reuse

---

**Related Guides:** 
- [SETUP.md](./SETUP.md) - Initial system setup
- [PROJECT-TYPES.md](./PROJECT-TYPES.md) - Understanding auto-detection
- [README.md](./README.md) - System overview and architecture
