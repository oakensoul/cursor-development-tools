# Project Types: Auto-Detection & Optimization

Understanding how the AI system automatically detects your project type and optimizes workflows accordingly.

## 🔍 How Auto-Detection Works

When you run `@init-workflow-rules`, the system analyzes your repository structure, files, and dependencies to automatically configure itself for your specific project type. This ensures optimal AI behavior from day one.

## 📊 Supported Project Types

### **📚 Documentation Repositories**
**Detected by:**
- `README.md`, `docs/`, `onboarding/`, `team/` folders
- Markdown files (`.md`) as primary content
- Absence of major code frameworks

**Optimized for:**
- **Content quality** - Writing style, clarity, completeness
- **Stakeholder communication** - Audience-appropriate language
- **Team knowledge** - Onboarding and reference materials

**Git workflow:**
- Documentation review processes
- Content validation and consistency
- Stakeholder feedback integration

**Generated workflow-rules.yml includes:**
```yaml
project_type: documentation
content_focus: team_knowledge
review_process: content_validation
commit_format: "docs: brief description of content changes"
```

---

### **🔄 Data Pipelines**
**Detected by:**
- `dbt_project.yml`, `models/`, `analysis/`, `macros/` directories
- Python data files (`*.py` with pandas, numpy imports)
- SQL files and data transformation scripts

**Optimized for:**
- **Data quality** - Validation, testing, monitoring
- **Model documentation** - Clear business logic explanation
- **Stakeholder impact** - Business value of data changes

**Git workflow:**
- Model review and validation
- Data quality checks
- Business stakeholder alignment

**Generated workflow-rules.yml includes:**
```yaml
project_type: data_pipeline
data_quality_focus: true
stakeholder_impact: business_metrics
commit_format: "feat(model): add/update model description"
```

---

### **🚀 API Services**
**Detected by:**
- `main.py`, `app.py`, `requirements.txt`, `Dockerfile`
- FastAPI, Flask, Django framework indicators
- API route definitions and service architecture

**Optimized for:**
- **Code quality** - Testing, documentation, maintainability
- **API documentation** - Clear endpoint and usage docs
- **Deployment safety** - Staging, rollback, monitoring

**Git workflow:**
- Code review and testing validation
- API documentation updates
- Deployment automation and safety

**Generated workflow-rules.yml includes:**
```yaml
project_type: api_service
code_quality_focus: testing_required
deployment_safety: staging_first
commit_format: "feat(api): endpoint or service description"
```

---

### **🌐 Web Applications**
**Detected by:**
- `package.json`, `src/`, `components/`, `pages/` directories
- React, Vue, Angular framework indicators
- Frontend build tools and configurations

**Optimized for:**
- **User experience** - Performance, accessibility, usability
- **Component reusability** - Modular, maintainable code
- **Performance** - Bundle size, loading, responsiveness

**Git workflow:**
- Feature development and testing
- UI/UX validation and review
- Performance monitoring and deployment

**Generated workflow-rules.yml includes:**
```yaml
project_type: web_application
ux_focus: performance_accessibility
component_architecture: modular_reusable
commit_format: "feat(ui): component or feature description"
```

---

### **🏗️ Infrastructure**
**Detected by:**
- `terraform/`, `*.tf` files, `kubernetes/`, `helm/` directories
- Infrastructure as Code patterns
- DevOps and deployment configurations

**Optimized for:**
- **Security** - Access controls, secrets, compliance
- **Reliability** - High availability, disaster recovery
- **Cost optimization** - Resource efficiency, monitoring
- **Compliance** - Audit trails, policy enforcement

**Git workflow:**
- Infrastructure review and validation
- Security and compliance checks
- Change management and rollback procedures

**Generated workflow-rules.yml includes:**
```yaml
project_type: infrastructure
security_focus: compliance_required
change_management: approval_required
commit_format: "infra: resource or configuration description"
```

## 🔧 Mixed Project Types

### **Full-Stack Applications**
If multiple indicators are found (e.g., both `package.json` and `main.py`), the system creates a hybrid configuration:

```yaml
project_type: full_stack
primary_focus: web_application
secondary_focus: api_service
commit_formats:
  frontend: "feat(ui): component or feature description"
  backend: "feat(api): endpoint or service description"
```

### **Data Science Projects**
Jupyter notebooks + Python data libraries + documentation:

```yaml
project_type: data_science
primary_focus: research_development
analysis_sharing: stakeholder_friendly
commit_format: "analysis: research question or finding"
```

## 🎯 Customizing Auto-Detection Results

### **Override Detection**
If auto-detection doesn't match your needs, edit `workflow-rules.yml` manually:

```yaml
# Change the detected project type
project_type: custom_type
# Add your specific configurations
custom_workflow_patterns: true
```

### **Hybrid Configurations**
For complex projects, combine multiple project type patterns:

```yaml
project_type: hybrid
primary_type: web_application
secondary_types: [api_service, documentation]
workflow_patterns:
  - web_ui_development
  - api_service_deployment
  - documentation_maintenance
```

### **Team-Specific Overrides**
Adjust generated rules for your team's specific needs:

```yaml
# Override default git workflow
git_workflow: github_flow  # vs. gitflow
branch_naming: ticket_based  # vs. feature_based
review_process: pair_programming  # vs. pr_review
```

## 📋 Detection Troubleshooting

### **Incorrect Project Type Detected**
```bash
# Re-run detection with manual hints:
@init-workflow-rules --project-type=web_application

# Or manually edit workflow-rules.yml and refresh:
@update-ai-guidance
@update-context
```

### **Missing Project Indicators**
If your project structure doesn't match standard patterns:

1. **Add standard files** - Create typical project structure files
2. **Manual configuration** - Edit workflow-rules.yml directly
3. **Custom detection** - Add your patterns to the base template

### **Multiple Valid Types**
For projects that could be multiple types:

1. **Choose primary focus** - What's the main development activity?
2. **Configure hybrid** - Use multiple project type patterns
3. **Team decision** - Align with team's primary workflow needs

## 🔄 Evolution & Updates

### **Project Type Changes**
As projects evolve, you may need to update the project type:

```bash
# When project focus shifts significantly:
@update-workflow-rules  # Re-analyze current project state
@update-ai-guidance     # Refresh AI understanding
@update-context         # Regenerate all context files
```

### **Adding New Project Types**
To extend the base template with new project types:

1. **Study existing patterns** - Look at current project type configurations
2. **Define detection criteria** - What files/patterns indicate this type?
3. **Create optimization rules** - What should be prioritized for this type?
4. **Test and refine** - Use in real projects and improve based on experience

---

**Related Guides:**
- [SETUP.md](./SETUP.md) - Setting up the system with auto-detection
- [USAGE.md](./USAGE.md) - Daily workflow commands
- [README.md](./README.md) - System overview and architecture
