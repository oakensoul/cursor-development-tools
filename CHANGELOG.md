# Changelog

All notable changes to the Cursor Development Tools project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial release of cursor development tools template system
- Complete `.cursor` system with prompts, rules, and context generation
- Smart git workflow automation (commit, branch, PR, shipit)
- Automated context management and LLM guidance system
- Auto-update script with release selection and safe updating
- Comprehensive documentation and setup guides
- Business-aligned development workflows
- Team collaboration patterns and standards
- Quality automation and validation systems

### Changed
- Migrated from Splash Sports-specific context to generic template system
- Updated all examples and documentation to be organization-agnostic
- Reorganized file structure with dedicated install directory

### Removed
- All business-specific references and examples
- Hardcoded organization names and contexts

## [1.0.0] - YYYY-MM-DD (To be released)

### Added
- **Core System Architecture**
  - `.cursor/prompts/` - Complete prompt template system
  - `.cursor/rules/` - AI behavior and content guidelines  
  - `.cursor/llms/` - Context file management system
  - `prompts.json` - Cursor prompt registry configuration

- **Git Workflow Automation**
  - `@commit` - Smart commit execution with context analysis
  - `@branch` - Intelligent branch creation with naming conventions
  - `@pr` - Auto-generated pull requests with descriptions and reviewers
  - `@push` - Workflow-aware push execution
  - `@shipit` - Complete end-to-end workflow automation
  - `@hotfix` - Emergency fix workflow

- **Context Management**
  - `@update-context` - Regenerate all LLM context files
  - `@generate-project-overview` - Project identity and purpose
  - `@generate-business-context` - Stakeholder and business alignment
  - `@generate-tech-stack` - Technical architecture context
  - `@generate-team-context` - Collaboration and culture

- **Configuration System**
  - `@init-workflow-rules` - Initialize project configuration
  - `@init-ai-guidance` - Setup AI decision context
  - `@update-workflow-rules` - Modify project settings
  - `@update-ai-guidance` - Enhance AI context

- **Installation & Updates**
  - One-command install/update script
  - Release-based version management
  - Selective file updates preserving user customizations
  - Automatic backup and rollback capabilities
  - GitHub API integration for release selection

- **Documentation**
  - Comprehensive setup and usage guides
  - Troubleshooting and maintenance instructions
  - Cross-project replication guidelines
  - Team onboarding documentation

### Features
- **Business Alignment** - All technical decisions connected to stakeholder value
- **Context Awareness** - AI understands project constraints and culture
- **Quality Automation** - Standards enforced automatically
- **Team Consistency** - Same AI behavior across all team members
- **Knowledge Preservation** - Team wisdom captured and reusable
- **Cross-Project Portability** - Template works across different project types

### Technical Specifications
- Compatible with Cursor IDE and GitHub CLI
- Supports conventional commit standards
- Integrates with GitHub pull request workflows
- Uses YAML configuration with LLM context files
- Bash-based automation scripts with error handling
- Markdown-based documentation with contextual examples

---

## Version History Guidelines

### Semantic Versioning
- **MAJOR** (X.0.0) - Breaking changes that require user action
- **MINOR** (1.X.0) - New features that are backward compatible  
- **PATCH** (1.0.X) - Bug fixes and minor improvements

### Changelog Sections
- **Added** - New features and capabilities
- **Changed** - Modifications to existing functionality
- **Deprecated** - Features that will be removed in future versions
- **Removed** - Features that have been removed
- **Fixed** - Bug fixes and error corrections
- **Security** - Security-related changes and fixes

### Release Process
1. Update CHANGELOG.md with new version section
2. Update version references in documentation
3. Create git tag with version number
4. Publish GitHub release with changelog notes
5. Update auto-update script compatibility

---

*For upgrade instructions and migration guides, see the [Installation Guide](install/README.md).*
