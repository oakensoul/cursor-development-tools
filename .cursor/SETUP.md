# Setup Guide: AI-Enhanced Development System

Complete step-by-step instructions for setting up the AI-powered development workflow system in your project.

## 📋 Pre-Setup: Optimize Your Documentation

**💡 Pro Tip: Better documentation = better AI configuration**

Before running setup, ensure your project has comprehensive documentation. The AI uses this to understand your project and generate accurate configurations.

## ⚙️ Prerequisites

### **Required for Full Functionality:**
- ✅ **Git** - Repository management and version control
- ✅ **GitHub CLI (`gh`)** - Required for PR creation and management (`@pr`, `@shipit`)
  ```bash
  # Install GitHub CLI:
  # macOS: brew install gh
  # Windows: winget install GitHub.cli
  # Linux: See https://cli.github.com/manual/installation
  
  # Authenticate with GitHub:
  gh auth login
  ```

### **Optional but Recommended:**
- 📝 **Cursor IDE** - Optimized for this AI-assisted workflow system
- 🔧 **Project dependencies** - Language-specific tools (npm, pip, etc.) for better project analysis

### **Essential Documentation for Best Results:**
- ✅ **Detailed README.md** - Project purpose, architecture, setup instructions
- ✅ **Technology documentation** - Stack details, dependencies, frameworks used
- ✅ **Team information** - Roles, processes, communication patterns
- ✅ **Business context** - Goals, stakeholders, success metrics
- ✅ **Development processes** - Git workflows, testing standards, deployment procedures

### **Optional But Helpful:**
- 📋 **PRDs/Requirements** - Product requirements, feature specifications
- 🏗️ **Architecture docs** - System design, data flows, API specifications
- 📊 **Project roadmap** - Timeline, milestones, feature priorities
- 👥 **Onboarding guides** - How new team members get started
- 🔧 **Runbooks** - Operational procedures, troubleshooting guides

**Why this matters:** The AI analyzes your existing documentation to:
- Detect project type and technology stack
- Understand team structure and workflows
- Generate appropriate git conventions and quality standards
- Create contextual AI guidance for your specific domain

**Don't worry if documentation is incomplete** - you can always re-run setup commands as your documentation improves!

## 🚀 Quick Setup Process

### **1. Copy to Your Project**
```bash
# From your new project root:
cp -r /path/to/data-engineering-cursor-base/.cursor ./
```

### **2. Initialize Configuration** 
```bash
@init-workflow-rules
```
**What it does:**
- Analyzes your repository to detect project type (docs/data-pipeline/api/web-app)
- Discovers technology stack from files and dependencies
- Creates `workflow-rules.yml` with project-specific configuration
- Sets up git conventions, quality standards, team processes

**Takes ~2-3 minutes** - Will ask clarifying questions about team size, processes, etc.

### **3. Create AI Decision Context**
```bash
@init-ai-guidance
```
**What it does:**
- Reads your `workflow-rules.yml` for structured context
- Generates `ai-guidance.llms` with natural language decision guidance
- Includes business context, team culture, technical wisdom
- Provides examples and edge case handling for AI

**Takes ~1-2 minutes** - Automatically pulls from workflow rules

### **4. Generate Context Files**
```bash
@update-context
```
**What it does:**
- Creates `project-overview.llms` (project identity, purpose, structure)
- Creates `business-context.llms` (stakeholders, success metrics, priorities)
- Creates `tech-stack.llms` (tools, architecture, standards, integration)
- Creates `team-context.llms` (collaboration, culture, processes)

**Takes ~3-5 minutes** - Generates all AI-optimized context files

### **5. Test the System**
```bash
# Safe testing options (won't commit anything):
@commit --dry-run    # See what commit message AI would generate
# OR ask AI: "Please explain my workflow-rules.yml file"
# OR ask AI: "What type of project did you detect?"
```
**What these tests do:**
- Validates AI understands your project context
- Shows intelligent commit message generation (without committing)
- Confirms configuration files are working properly
- Tests AI knowledge of your project setup

**Takes ~30 seconds** - Safe validation without making any git changes

**⚠️ Note:** Avoid using `@shipit` or `@commit` until you're ready to actually commit changes, as these commands will stage and commit files!

## 🔄 Improving Over Time

### **Re-running Setup as Documentation Improves**
As your project documentation gets better, you can re-run setup commands to get more accurate configurations:

```bash
# After adding more documentation, re-analyze your project
@init-workflow-rules

# Update AI guidance with new insights
@update-ai-guidance  

# Regenerate context with better understanding
@update-context
```

### **Iterative Improvement Process**
1. **Start with basic setup** - Even minimal documentation produces useful results
2. **Use the system** - Begin using AI-assisted workflows immediately  
3. **Improve documentation** - Add more detail as you develop
4. **Re-run configuration** - Update AI understanding periodically
5. **Capture learnings** - Use `@update-ai-guidance` to record team insights

**The system gets smarter as your project documentation becomes more comprehensive!**

## 📋 Troubleshooting Setup Issues

### **Common Setup Problems**
```bash
# If initialization fails:
- Check project has at least README.md or core files
- Ensure you have write permissions in project directory
- Verify Cursor has access to project folder

# If context generation is incomplete:
@update-context  # Re-run full context generation
# Check .cursor/llms/ for missing files

# If git workflows don't work:
- Ensure you're in git repository root
- Check workflow-rules.yml was created properly
- Verify context files exist in .cursor/llms/
```

### **Validation Checklist**
After setup, verify these files exist:
- [ ] `.cursor/workflow-rules.yml` (project configuration)
- [ ] `.cursor/ai-guidance.llms` (AI decision guidance)
- [ ] `.cursor/llms/project-overview.llms`
- [ ] `.cursor/llms/business-context.llms`
- [ ] `.cursor/llms/tech-stack.llms`
- [ ] `.cursor/llms/team-context.llms`

### **Getting Help with Setup**
1. **Check prompts documentation** - Each `.cursor/prompts/` folder has detailed docs
2. **Review working examples** - Look at other projects using this system
3. **Ask your team** - Share learnings about what works
4. **Update this guide** - Improve based on your setup experience

## 🔒 Security & Privacy Considerations

**⚠️ Critical Warning for Corporate Use:**
When using AI/LLM tools in professional or corporate settings, **assume all input may be stored and potentially used for training** unless explicitly stated otherwise.

### **Data Exposure Risks:**
- 💾 **Training data inclusion** - Your code, comments, and prompts may become part of future model training
- 🔍 **Inadvertent disclosure** - Proprietary algorithms, business logic, and trade secrets could be exposed
- 📊 **Data aggregation** - Multiple interactions can reveal patterns about your organization
- 🌐 **Cross-contamination** - Your data might influence responses to other users

### **What NOT to share with AI:**
- 🚫 **API keys, passwords, tokens** - Any authentication credentials
- 🚫 **Proprietary source code** - Company-specific algorithms and implementations  
- 🚫 **Customer data** - PII, financial information, personal details
- 🚫 **Business secrets** - Strategic plans, unreleased features, competitive advantages
- 🚫 **Internal configurations** - Database schemas, server configurations, network details

### **Enterprise-Safe Alternatives:**
When corporate data protection is critical, consider:

**LLMs with No-Training Policies (as of 2025):**
- ✅ **Anthropic Claude API** - Enterprise plans explicitly don't train on user data
- ✅ **OpenAI API (Enterprise)** - Business/Enterprise tiers don't use data for training
- ✅ **Microsoft Azure OpenAI Service** - Strict data privacy, no training on user data
- ✅ **Google Gemini Enterprise** - Configurable privacy settings, no-training options
- ⚠️ **Consumer versions** - Free/basic tiers often DO train on data (check settings)

**Self-Hosted Options:**
- **Meta LLaMA 3** - Run locally, complete data control
- **Code Llama** - Specialized for code, can be deployed on-premises
- **Mistral AI** - Open source models with commercial licensing
- **Local deployment tools** - privateGPT, h2oGPT, Ollama

**Important Note:** Always verify current privacy policies as they change frequently. When in doubt, use self-hosted solutions for maximum data protection.

### **⚠️ Prompt Injection Awareness:**
When using LLMs to analyze external content, be aware of **prompt injection attacks**:

- **What they are**: Malicious instructions hidden in content that try to manipulate the AI's behavior
- **Common vectors**: Comments in code, README files, documentation, script outputs
- **Attack goals**: Make AI ignore safety instructions, execute unintended commands, or leak information

**Best Practices:**
- 🔍 **Manually review** any external scripts before having AI analyze them
- 🏗️ **Sandbox testing** - Run unknown code in isolated environments first
- 🤔 **Stay skeptical** - If AI behavior seems unusual after reading external content, stop and investigate
- 📝 **Verify outputs** - Double-check any commands or code the AI suggests after reviewing external sources

## 🔧 Advanced Setup Options

### **Custom Configuration**
If the auto-detection doesn't match your project perfectly:

1. **Edit workflow-rules.yml** manually after generation
2. **Run** `@update-ai-guidance` to refresh AI context
3. **Run** `@update-context` to regenerate all context files

### **Team Onboarding**
For new team members joining an existing project:

1. **Skip steps 2-4** (configuration already exists)
2. **Just run** `@shipit` to test the system
3. **Read** `workflow-rules.yml` to understand project standards
4. **Explore** `llms/project-overview.llms` for learning roadmap

### **Multi-Project Setup**
To replicate across similar projects:

1. **Copy this entire .cursor folder** to new project
2. **Run full setup process** (steps 2-5) for project-specific config
3. **Customize for differences** - adjust workflow-rules.yml as needed
4. **Share learnings** - update the base template with improvements

---

**Next Steps:** Once setup is complete, see [USAGE.md](./USAGE.md) for daily workflow commands and [PROJECT-TYPES.md](./PROJECT-TYPES.md) to understand how auto-detection works.
