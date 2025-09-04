# Configuration Management Prompts

This directory contains prompts for creating and maintaining the **foundation configuration files** that drive the entire AI workflow system.

## 🎯 **Purpose**

These prompts manage the **core configuration files** that everything else depends on:
- **`workflow-rules.yml`** - Structured project rules, team info, git workflows, quality standards
- **`ai-guidance.llms`** - Natural language context that guides AI decision-making

Without these files, your AI commands won't have the context they need to make good decisions.

## 📁 **Available Commands**

### **🆕 Initialization Commands**

#### **[@init-workflow-rules](./init-workflow-rules.mdc)**
Create comprehensive `workflow-rules.yml` for new projects.

**Use when:**
- Starting a new repository
- Converting to the AI workflow system
- Completely refreshing project configuration

**What it does:**
- Analyzes repository to detect project type (documentation/data-pipeline/api/etc.)
- Discovers technology stack and team structure
- Generates complete workflow-rules.yml with appropriate templates
- Sets up git conventions, quality checks, team processes

**Example usage:**
```bash
@init-workflow-rules
# → Interactive setup process
# → Generates complete workflow-rules.yml
# → Suggests running @update-context next
```

#### **[@init-ai-guidance](./init-ai-guidance.mdc)**
Create comprehensive `ai-guidance.llms` with natural language context.

**Use when:**
- Setting up AI guidance for new projects
- Creating nuanced decision-making context
- Adding team culture and business context

**What it does:**
- Reads workflow-rules.yml for structured context
- Generates natural language guidance for AI decision-making
- Includes business context, team culture, technical wisdom
- Provides examples and edge case handling

**Example usage:**
```bash
@init-ai-guidance
# → Reads existing workflow-rules.yml
# → Generates comprehensive ai-guidance.llms
# → Optimized for AI consumption and decision-making
```

### **🔄 Update Commands**

#### **[@update-workflow-rules](./update-workflow-rules.mdc)**
Intelligently update existing `workflow-rules.yml` with changes.

**Use when:**
- Adding new team members or changing team structure
- Integrating new technologies or tools
- Refining processes based on team learnings
- Evolving project scope or requirements

**What it does:**
- Analyzes current workflow-rules.yml
- Identifies what needs updating (team/tech/process/scope)
- Applies updates systematically with dependency checking
- Suggests follow-up actions (context updates, team communication)

**Example usage:**
```bash
@update-workflow-rules
# → Detects: "New engineer joined, Redis added to stack"
# → Updates: team size, tech stack, commit scopes, reviewers
# → Suggests: @update-context, team communication
```

#### **[@update-ai-guidance](./update-ai-guidance.mdc)**
Update `ai-guidance.llms` with new insights and evolved understanding.

**Use when:**
- Team culture or collaboration patterns evolve
- Learning what works/doesn't work in practice
- Stakeholder needs or business context changes
- Accumulating wisdom about technical decisions

**What it does:**
- Reviews current ai-guidance.llms for gaps and outdated content
- Incorporates team learnings and process evolution
- Updates business context and stakeholder understanding
- Refines decision-making guidance based on experience

**Example usage:**
```bash
@update-ai-guidance
# → Identifies: "PR process too slow for simple fixes"
# → Updates: guidance on when to use direct-to-main vs PR
# → Improves: AI suggestions for workflow decisions
```

## 🔄 **Configuration Lifecycle**

### **New Project Setup**
```bash
# 1. Initialize foundation
@init-workflow-rules    # → Creates workflow-rules.yml
@init-ai-guidance      # → Creates ai-guidance.llms

# 2. Generate context from foundation
@update-context        # → Creates all .cursor/llms/ files

# 3. Ready to use AI workflows
@shipit               # → AI now has full project context
```

### **Project Evolution**
```bash
# When team/tech/process changes:
@update-workflow-rules  # → Update structured rules
@update-ai-guidance    # → Update decision context
# → Context files automatically updated by git workflows
```

### **Cross-Project Replication**
```bash
# For new similar projects:
# 1. Copy workflow-rules.yml as template
# 2. Run @update-workflow-rules to customize
# 3. Run @init-ai-guidance for project-specific context
# 4. Run @update-context to generate LLM context files
```

## 🧠 **System Architecture**

### **Configuration Flow**
```
workflow-rules.yml     → Structured project rules and standards
       ↓
ai-guidance.llms      → Natural language decision context
       ↓
@update-context       → Generates specific LLM context files
       ↓
Git workflow commands → Use context for intelligent decisions
```

### **File Relationships**
```yaml
workflow-rules.yml:   # Source of truth for formal rules
  - Project identity and team structure
  - Git conventions and quality standards
  - Tool configurations and process definitions

ai-guidance.llms:     # Complements with nuanced guidance
  - Business context and stakeholder insights
  - Team culture and collaboration patterns
  - Decision-making frameworks and trade-offs
  
Generated context:    # AI-optimized derivatives
  - project-overview.llms (what/who/why)
  - business-context.llms (stakeholders/success)
  - tech-stack.llms (tools/architecture)
  - team-context.llms (collaboration/culture)
```

## 🎯 **Best Practices**

### **When to Update Configuration**
```yaml
team_changes:
  - New team members join or leave
  - Role responsibilities change
  - Team culture or collaboration evolves

technology_evolution:
  - New tools adopted or old tools deprecated  
  - Architecture or platform changes
  - Integration patterns change

process_improvements:
  - Workflow pain points identified and resolved
  - Quality standards refined through experience
  - Stakeholder feedback drives process changes

business_context_shifts:
  - New stakeholders or changed priorities
  - Market changes affecting technical decisions
  - Success metrics or goals evolve
```

### **Configuration Quality**
```yaml
accuracy:
  - Reflects actual current practices, not aspirational goals
  - Team structure and processes match reality
  - Technology stack represents what's actually used

completeness:
  - All major decision contexts covered
  - Edge cases and exceptions documented
  - Cross-team collaboration patterns included

consistency:
  - workflow-rules.yml and ai-guidance.llms complement each other
  - Generated context aligns with foundation files
  - Examples match stated principles and practices
```

### **Maintenance Schedule**
```yaml
regular_review:
  - Quarterly: Review configuration accuracy and completeness
  - After major changes: Update immediately (new tools, team changes)
  - Annual: Comprehensive refresh of business context and team culture

trigger_based_updates:
  - New team member onboarding: Update team context
  - Technology adoption: Update tech stack and processes  
  - Process pain points: Refine workflow guidance
  - Stakeholder feedback: Adjust business context
```

## 🚀 **Getting Started**

### **For New Projects**
1. **Run `@init-workflow-rules`** - Set up comprehensive project configuration
2. **Run `@init-ai-guidance`** - Add natural language decision context
3. **Run `@update-context`** - Generate all LLM context files
4. **Test with `@shipit`** - Verify AI workflows work correctly

### **For Existing Projects**
1. **Run `@init-workflow-rules`** - Convert existing project to system
2. **Customize generated rules** - Adjust for actual team practices
3. **Run `@init-ai-guidance`** - Add team culture and decision context
4. **Run `@update-context`** - Generate context files
5. **Gradually adopt AI workflows** - Start with simple commands, expand usage

### **For Team Adoption**
1. **Start with one project** - Prove value before expanding
2. **Document team learnings** - Capture what works in ai-guidance.llms
3. **Regular configuration updates** - Keep foundation files current
4. **Cross-project expansion** - Replicate successful patterns

This configuration management system ensures your AI workflows have the context they need to make intelligent, team-aligned decisions across all your projects! 🎉
