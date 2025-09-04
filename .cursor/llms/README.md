# LLM Context Files

This directory contains automatically generated context files that provide LLMs with instant understanding of the project.

## 🎯 **Purpose**

Instead of requiring LLMs to scan the entire project to understand context, these files provide:
- **Instant project understanding** - what this repo is and who it serves
- **Business context** - company, industry, stakeholders, and data focus
- **Technical stack** - tools, platforms, and integration patterns
- **Team context** - structure, processes, and collaboration patterns

## 📁 **File Structure**

```
.cursor/llms/
├── README.md                 # ← This file (explains the system)
├── project-overview.llms     # ← Project purpose, structure, audience
├── business-context.llms     # ← Company info, stakeholders, industry context
├── tech-stack.llms          # ← Data tools, platforms, workflows
└── team-context.llms        # ← Team structure, processes, collaboration
```

## 🔄 **How These Files Are Generated**

### **Source of Truth**
All context files are **automatically generated** from:
- **`../workflow-rules.yml`** - Primary configuration and project rules
- **Project documentation** - README files and key content
- **Business context rules** - Stakeholder and industry information

### **Generation Commands**
```bash
@update-context                    # Regenerate all context files
@generate-project-overview         # Update just project overview
@generate-business-context         # Update just business context  
@generate-tech-stack              # Update just technical context
@generate-team-context            # Update just team information
```

### **Automatic Updates**
Context files are automatically updated when:
- **workflow-rules.yml changes** - Core project configuration modified
- **Major documentation updates** - Significant structural changes
- **Team structure changes** - New team members, role changes, process updates
- **Technology stack changes** - New tools, platform migrations, workflow updates

## 🧠 **How LLMs Use These Files**

### **Context Loading**
LLM prompts reference these files via `context_files` arrays:
```yaml
context_files: ["../llms/project-overview.llms", "../llms/business-context.llms"]
```

### **Instant Understanding**
Instead of expensive project scanning, LLMs get immediate context about:
- **What type of project this is** and its primary purpose
- **Who the stakeholders are** and how to communicate with them
- **What tools and platforms** are used in the tech stack
- **How the team operates** and collaborates

### **Better Decision Making**
With rich context, LLMs can:
- **Make business-aligned suggestions** that serve stakeholder needs
- **Use appropriate technical approaches** that fit the existing stack
- **Follow team conventions** and communication patterns
- **Understand urgency levels** and escalation procedures

## ⚙️ **Context File Format**

### **Optimized for LLM Consumption**
All `.llms` files use natural language optimized for AI understanding:
- **Clear section headers** for easy parsing
- **Concrete examples** over abstract descriptions
- **Business impact context** connecting technical decisions to outcomes
- **Practical guidance** for common scenarios and decisions

### **Structured but Natural**
```markdown
# Business Context: [Project Name]

## Company Overview
[Natural language description of company, industry, data focus]

## Stakeholder Ecosystem  
[Who depends on our work and how they use it]

## Data Landscape
[What data matters and how it flows through the organization]

## Success Metrics
[How we measure impact and business value]
```

## 🔧 **Maintenance**

### **When to Regenerate**
- **Before major releases** - Ensure context reflects current state
- **After team changes** - New members, role changes, process updates
- **Technology migrations** - Stack changes, new tools, platform updates
- **Process improvements** - Workflow changes, new standards, tool adoption

### **Validation Checks**
Regular validation ensures context files remain accurate:
- **Links and references work** - All internal and external references valid
- **Team information current** - Contact info, roles, responsibilities up-to-date
- **Technical details accurate** - Stack info, tools, versions, configurations current
- **Business context relevant** - Stakeholder info, processes, success metrics current

### **Quality Standards**
- **Business-aligned** - Content serves actual stakeholder needs
- **Technically accurate** - Reflects real tools, processes, constraints
- **Team-validated** - Regular review by team members for accuracy
- **Example-rich** - Concrete scenarios better than abstract explanations

## 🚀 **Benefits**

### **For AI Interactions**
- **Faster responses** - No project scanning required
- **Better suggestions** - Context-aware recommendations
- **Consistent behavior** - Same understanding across all interactions
- **Business alignment** - Suggestions that serve real stakeholder needs

### **For Team Productivity**
- **Instant AI onboarding** - New tools understand project immediately
- **Consistent standards** - AI follows established team conventions
- **Reduced context gathering** - Less explaining project basics
- **Cross-project portability** - Same system works for all repositories

### **For Project Quality**
- **Living documentation** - Context stays current with project evolution
- **Knowledge preservation** - Team wisdom captured in accessible format
- **Onboarding acceleration** - New team members and tools get instant context
- **Decision consistency** - AI suggestions align with team standards and business goals

---

**Last Updated**: Auto-generated from workflow-rules.yml
**Maintainer**: Data Engineering Team
**Update Frequency**: On workflow-rules.yml changes or major project updates
