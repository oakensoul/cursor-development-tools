# Context Generation Prompts

This directory contains prompts for **automatically generating LLM context files** from the project's `workflow-rules.yml` configuration.

## 🎯 **Purpose**

These prompts solve the **LLM context management problem** by:
- **Generating AI-optimized context** from structured configuration
- **Keeping context current** with project evolution
- **Providing instant project understanding** for all AI interactions
- **Eliminating manual context file maintenance**

## 📁 **Available Commands**

### **🔄 Master Generation Command**

#### **[@update-context](./update-context.mdc)**
Regenerate ALL LLM context files from current `workflow-rules.yml`.

**Use when:**
- workflow-rules.yml has been updated
- Starting fresh context generation
- Context files are stale or missing
- Setting up AI context for first time

**What it generates:**
- `project-overview.llms` - Project identity, structure, purpose
- `business-context.llms` - Company, stakeholders, success metrics  
- `tech-stack.llms` - Tools, architecture, technical standards
- `team-context.llms` - Team structure, collaboration, culture

**Example usage:**
```bash
@update-context
# → Reads workflow-rules.yml
# → Generates all 4 context files optimized for AI consumption
# → Reports what was updated and why
```

### **🎯 Individual Generation Commands**

#### **[@generate-project-overview](./generate-project-overview.mdc)**
Generate comprehensive project overview context.

**Focus areas:**
- Project identity (type, team, company, purpose)
- Target audience and user personas
- Repository structure and organization
- Content philosophy and standards
- Business impact and success metrics

#### **[@generate-business-context](./generate-business-context.mdc)**
Generate business and stakeholder context.

**Focus areas:**
- Company overview and industry position
- Stakeholder ecosystem and communication patterns
- Data landscape and business value
- Success metrics and collaboration patterns
- Decision frameworks for business alignment

#### **[@generate-tech-stack](./generate-tech-stack.mdc)**
Generate comprehensive technology context.

**Focus areas:**
- Core data platforms (Snowflake, dbt, Metabase)
- Development ecosystem (GitHub, Cursor AI, Python)
- Operational infrastructure (monitoring, security, deployment)
- Integration patterns and architecture principles
- Technical standards and best practices

#### **[@generate-team-context](./generate-team-context.mdc)**
Generate team collaboration and culture context.

**Focus areas:**
- Team composition and expertise distribution
- Collaboration processes and communication patterns
- Development culture and work-life balance
- Knowledge sharing and support systems
- Team growth and capacity planning

## 🧠 **Context System Architecture**

### **Source → Generation → Consumption**
```
workflow-rules.yml    → Structured project configuration
       ↓
Context Prompts       → LLM-powered content generation  
       ↓
.cursor/llms/*.llms   → AI-optimized context files
       ↓
Git Workflow Commands → Use context for intelligent decisions
```

### **Generated Context Files**
```
.cursor/llms/
├── project-overview.llms   ← What/who/why of the project
├── business-context.llms   ← Stakeholders/success/priorities  
├── tech-stack.llms        ← Tools/architecture/standards
└── team-context.llms      ← Collaboration/culture/growth
```

## 🔄 **When Context Gets Updated**

### **Automatic Updates**
The git workflow commands automatically detect when context needs updating:

```bash
# These commands check for workflow-rules.yml changes:
@shipit                # → Step 2: Offers context update if rules changed
@commit                # → Pre-commit: Prompts for context update
@pr                    # → Pre-PR: Checks context and adds reviewers
```

### **Manual Updates**
```bash
# Force context updates anytime:
@update-context                # → Regenerate all context files
@generate-project-overview     # → Update just project context
@generate-business-context     # → Update just business context
@generate-tech-stack          # → Update just technical context
@generate-team-context        # → Update just team context
```

### **Update Triggers**
```yaml
when_to_update:
  workflow_rules_changes:
    - "Team size or structure changes"
    - "New technologies added to stack"
    - "Process improvements implemented"
    - "Business context evolution"
  
  project_evolution:
    - "New stakeholders or requirements"
    - "Architecture or platform changes"  
    - "Team culture or collaboration changes"
    - "Success metrics or goals shift"
  
  regular_maintenance:
    - "Quarterly context accuracy review"
    - "After major project milestones"
    - "When onboarding new team members"
    - "Before important stakeholder presentations"
```

## 📊 **Generated Content Quality**

### **AI-Optimized Writing**
The context files are specifically written for AI consumption:
- **Natural language** - Easy for LLMs to parse and understand
- **Structured sections** - Consistent organization for reliable parsing
- **Concrete examples** - Specific scenarios over abstract principles
- **Business context** - Connects technical decisions to business value
- **Decision guidance** - Helps AI make better suggestions

### **Content Standards**
```yaml
accuracy:
  - Reflects actual current state, not aspirational goals
  - Team structure and processes match reality
  - Technology stack represents what's actively used

completeness:
  - All major decision contexts covered
  - Edge cases and exceptions documented  
  - Cross-functional collaboration patterns included

consistency:
  - Aligns with workflow-rules.yml structured data
  - Internal cross-references work correctly
  - Examples match stated principles and practices

freshness:
  - Contact information current and accurate
  - Process descriptions reflect actual workflows
  - Success metrics represent current priorities
```

## 🎯 **Benefits for AI Interactions**

### **⚡ Instant Context Loading**
Instead of expensive project scanning, AI gets immediate understanding:
- **Project purpose and audience** - Who this serves and why
- **Business priorities and stakeholders** - What matters to whom
- **Technical architecture and tools** - How systems work together
- **Team culture and collaboration** - How decisions get made

### **🧠 Better AI Decisions**
With rich context, AI provides:
- **Business-aligned suggestions** - Recommendations that serve stakeholder needs
- **Technically appropriate solutions** - Approaches that fit existing architecture
- **Team-culture compatible advice** - Suggestions that match collaboration style
- **Context-aware prioritization** - Understanding of what's urgent vs important

### **🔄 Consistent Behavior**
All AI interactions use the same context:
- **Same understanding** across different AI tools and commands
- **Consistent suggestions** regardless of when or how AI is invoked
- **Aligned recommendations** that build on each other over time
- **Predictable behavior** that teams can rely on

## 🚀 **Getting Started**

### **First Time Setup**
```bash
# After creating/updating workflow-rules.yml:
@update-context
# → Generates all context files from current configuration
# → Ready for intelligent AI workflows
```

### **Regular Maintenance**
```bash
# When workflow-rules.yml changes:
@shipit                  # → Auto-detects and offers context update
# OR manually:
@update-context         # → Force regeneration of all context files
```

### **Targeted Updates**
```bash
# When specific aspects change:
@generate-business-context  # → New stakeholders or priorities
@generate-tech-stack       # → New tools or architecture  
@generate-team-context     # → Team changes or culture evolution
@generate-project-overview # → Scope or purpose changes
```

## 🔧 **Integration with Git Workflows**

### **Context-Aware Commands**
All git commands now reference the generated context files:
```yaml
# In git prompt headers:
context_files: ["../workflow-rules.yml", "../ai-guidance.llms", "../llms/project-overview.llms"]
```

### **Context Update Integration**
```bash
# Workflow integration:
workflow_rules_change → git_command_detection → context_update_offer → regeneration → inclusion_in_commit
```

### **Review Process Enhancement**
When context files are updated:
- **Special reviewers added** - Senior engineer + manager for context validation
- **Enhanced PR descriptions** - Clear explanation of context changes
- **Review focus guidance** - Specific areas to validate for accuracy

This context generation system ensures your AI workflows always have **current, comprehensive, business-aligned context** for making intelligent decisions! 🎉
