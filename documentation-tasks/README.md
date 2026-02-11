# Documentathon Tasks
## 2026 EPICS Codeathon - Phoebus Documentation Track

Documentation is a critical part of making Phoebus tools and services accessible to users and developers. This track focuses on improving, creating, and organizing documentation.

---

## Documentation Categories

1. [User Documentation](#user-documentation)
2. [Developer Documentation](#developer-documentation)
3. [Installation & Deployment Guides](#installation--deployment-guides)
4. [API Documentation](#api-documentation)
5. [Tutorials & Examples](#tutorials--examples)

---

## Documentation Workflow

1. Choose a task from the list below
2. Review existing documentation in the respective repository
3. Create a GitHub issue for tracking (label: "documentation")
4. Fork the repository and create a branch
5. Write/update documentation
6. Submit a pull request
7. Coordinate with reviewers for technical accuracy

---

## User Documentation

### DOC-USER-001: Phoebus Application User Guides

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Beginner  
**Estimated Time:** 2-3 days  
**Skills Required:** Technical Writing, Basic Phoebus Usage  

**Tasks:**
- [ ] Update Display Builder user guide with latest features
- [ ] Create PV Table user guide with examples
- [ ] Document Databrowser features and usage patterns
- [ ] Write Alarm UI user guide
- [ ] Create Save & Restore user guide
- [ ] Document Logbook integration features

**Deliverables:**
- Markdown files in `docs/source/` directory
- Screenshots and diagrams
- Example files where applicable

**Assigned To:** _Available_

---

### DOC-USER-002: Olog User Documentation

**Repository:** https://github.com/Olog/phoebus-olog  
**Difficulty:** Beginner  
**Estimated Time:** 1-2 days  
**Skills Required:** Technical Writing  

**Tasks:**
- [ ] Document attachment handling
- [ ] Explain tag and property usage
- [ ] Create search and filter guide
- [ ] Document template usage

**Deliverables:**
- User guide in repository docs
- Workflow diagrams
- Screenshot examples

**Assigned To:** _Available_

---

### DOC-USER-003: ChannelFinder User Guide

**Repository:** https://github.com/ChannelFinder/ChannelFinderService  
**Difficulty:** Beginner  
**Estimated Time:** 1-2 days  
**Skills Required:** Technical Writing  

**Tasks:**
- [ ] Document channel search capabilities
- [ ] Explain property and tag system
- [ ] Create user guide for channel browsing
- [ ] Document integration with Phoebus applications

**Deliverables:**
- User documentation
- Search query examples
- Use case scenarios

**Assigned To:** _Available_

---

### DOC-USER-004: Archive Appliance User Guide

**Repository:** https://github.com/shroffk/epicsarchiverap  
**Difficulty:** Intermediate  
**Estimated Time:** 2 days  
**Skills Required:** Technical Writing, Archiver Knowledge  

**Tasks:**
- [ ] Document PV archiving configuration
- [ ] Explain data retrieval methods
- [ ] Create guide for using web interface
- [ ] Document integration with Databrowser

**Deliverables:**
- Comprehensive user guide
- Configuration examples
- Troubleshooting section

**Assigned To:** _Available_

---

## Developer Documentation

### DOC-DEV-001: Phoebus Plugin Development Guide

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Intermediate  
**Estimated Time:** 3-4 days  
**Skills Required:** Java, JavaFX, Technical Writing  

**Tasks:**
- [ ] Write step-by-step plugin development tutorial
- [ ] Document plugin architecture and lifecycle
- [ ] Explain service provider interfaces
- [ ] Create example plugin with complete code
- [ ] Document dependency injection patterns
- [ ] Explain preferences and settings management

**Deliverables:**
- Developer guide in `docs/source/`
- Working example plugin repository
- Architecture diagrams

**Assigned To:** _Available_

---

### DOC-DEV-002: Custom Widget Development

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Advanced  
**Estimated Time:** 3-4 days  
**Skills Required:** Java, JavaFX, Display Builder Knowledge  

**Tasks:**
- [ ] Document widget development API
- [ ] Explain widget properties and behaviors
- [ ] Create custom widget tutorial with complete example
- [ ] Document widget testing approaches
- [ ] Explain widget packaging and distribution

**Deliverables:**
- Widget development guide
- Example custom widget project
- Widget API reference

**Assigned To:** _Available_

---

### DOC-DEV-003: Middle Layer Services Development Guide

**Repository:** Multiple (Olog, ChannelFinder, Archive Appliance)  
**Difficulty:** Intermediate  
**Estimated Time:** 3 days  
**Skills Required:** Java, Spring Boot, REST APIs  

**Tasks:**
- [ ] Document service architecture patterns
- [ ] Explain REST API development conventions
- [ ] Create guide for adding new endpoints
- [ ] Document database migration procedures
- [ ] Explain testing strategies

**Deliverables:**
- Service development guide for each service
- API development template
- Testing examples

**Assigned To:** _Available_

---

### DOC-DEV-004: Contributing Guide

**Repository:** All repositories  
**Difficulty:** Beginner  
**Estimated Time:** 2 days  
**Skills Required:** Git, Technical Writing  

**Tasks:**
- [ ] Update CONTRIBUTING.md for each repository
- [ ] Document Git workflow and branching strategy
- [ ] Create pull request checklist
- [ ] Explain code review process
- [ ] Document coding standards

**Deliverables:**
- CONTRIBUTING.md files
- Workflow diagrams
- PR template updates

**Assigned To:** _Available_

---

### DOC-DEV-005: EPICS Core Java Documentation

**Repository:** https://github.com/shroffk/epicsCoreJava  
**Difficulty:** Advanced  
**Estimated Time:** 4 days  
**Skills Required:** Java, EPICS Protocol, Technical Writing  

**Tasks:**
- [ ] Document PVA Java client usage
- [ ] Explain PV Access patterns
- [ ] Create connection management guide
- [ ] Document data type handling
- [ ] Write performance tuning guide

**Deliverables:**
- Developer documentation
- Code examples
- Best practices guide

**Assigned To:** _Available_

---

## Installation & Deployment Guides

### DOC-INSTALL-001: Phoebus Installation Guide

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Beginner  
**Estimated Time:** 2 days  
**Skills Required:** Technical Writing, Multi-platform Knowledge  

**Tasks:**
- [ ] Update installation guide for Windows
- [ ] Update installation guide for Linux
- [ ] Update installation guide for macOS
- [ ] Document JDK requirements and recommendations
- [ ] Explain configuration file setup
- [ ] Create troubleshooting section

**Deliverables:**
- Platform-specific installation guides
- Configuration examples
- Troubleshooting FAQ

**Assigned To:** _Available_

---

### DOC-INSTALL-002: Service Deployment with Docker

**Repository:** Multiple  
**Difficulty:** Intermediate  
**Estimated Time:** 3 days  
**Skills Required:** Docker, Kubernetes, Technical Writing  

**Tasks:**
- [ ] Create Docker deployment guide for each service
- [ ] Document docker-compose setup for full stack
- [ ] Write Kubernetes deployment guide
- [ ] Document environment configuration
- [ ] Create production deployment checklist

**Deliverables:**
- Docker deployment guides
- docker-compose.yml examples
- Kubernetes manifests
- Deployment best practices

**Assigned To:** _Available_

---

### DOC-INSTALL-003: Service Configuration Guide

**Repository:** Multiple  
**Difficulty:** Intermediate  
**Estimated Time:** 2-3 days  
**Skills Required:** System Administration, Technical Writing  

**Tasks:**
- [ ] Document Olog configuration options
- [ ] Document ChannelFinder configuration
- [ ] Document Archive Appliance setup
- [ ] Explain authentication configuration
- [ ] Document database setup for each service

**Deliverables:**
- Configuration reference for each service
- Example configuration files
- Best practices guide

**Assigned To:** _Available_

---

## API Documentation

### DOC-API-001: REST API Documentation

**Repository:** Olog, ChannelFinder, Archive Appliance  
**Difficulty:** Intermediate  
**Estimated Time:** 3-4 days  
**Skills Required:** REST APIs, OpenAPI/Swagger  

**Tasks:**
- [ ] Generate/update OpenAPI specifications
- [ ] Document all REST endpoints with examples
- [ ] Create API usage guide
- [ ] Document authentication requirements
- [ ] Add example requests and responses
- [ ] Set up Swagger UI or similar for interactive docs

**Deliverables:**
- OpenAPI/Swagger specifications
- API documentation website
- Postman/curl example collections

**Assigned To:** _Available_

---

### DOC-API-002: Java API Documentation (JavaDoc)

**Repository:** All Java repositories  
**Difficulty:** Intermediate  
**Estimated Time:** Ongoing  
**Skills Required:** Java, JavaDoc  

**Tasks:**
- [ ] Review and improve JavaDoc comments
- [ ] Add missing package documentation
- [ ] Document public APIs thoroughly
- [ ] Create overview documentation
- [ ] Generate and publish JavaDoc HTML

**Deliverables:**
- Enhanced JavaDoc comments
- Published JavaDoc sites
- API overview guides

**Assigned To:** _Available_

---

## Tutorials & Examples

### DOC-TUT-001: Getting Started Tutorial

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Beginner  
**Estimated Time:** 2 days  
**Skills Required:** Phoebus Usage, Technical Writing  

**Tasks:**
- [ ] Create "Quick Start" guide for new users
- [ ] Write "First Display" tutorial
- [ ] Create "PV Connection" tutorial
- [ ] Write "Using Databrowser" tutorial
- [ ] Create video walkthroughs (optional)

**Deliverables:**
- Step-by-step tutorials
- Example files
- Screenshots/videos

**Assigned To:** _Available_

---

### DOC-TUT-002: Display Builder Cookbook

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Intermediate  
**Estimated Time:** 3 days  
**Skills Required:** Display Builder, Design, Technical Writing  

**Tasks:**
- [ ] Create widget showcase with examples
- [ ] Document common design patterns
- [ ] Write scripting tutorials
- [ ] Create embedded display examples
- [ ] Document navigation techniques
- [ ] Create responsive design guide

**Deliverables:**
- Display Builder cookbook
- Example display files (.bob)
- Design pattern library

**Assigned To:** _Available_

---

### DOC-TUT-003: Integration Examples

**Repository:** Multiple  
**Difficulty:** Intermediate  
**Estimated Time:** 3 days  
**Skills Required:** Multiple Phoebus Services, Technical Writing  

**Tasks:**
- [ ] Create end-to-end workflow examples
- [ ] Document alarm-to-olog workflow
- [ ] Create save/restore with ChannelFinder example
- [ ] Document archive data visualization workflow
- [ ] Write multi-service integration guide

**Deliverables:**
- Integration tutorials
- Complete example scenarios
- Configuration examples

**Assigned To:** _Available_

---

### DOC-TUT-004: Python Client Examples

**Repository:** New examples repository or within service repos  
**Difficulty:** Intermediate  
**Estimated Time:** 2-3 days  
**Skills Required:** Python, REST APIs  

**Tasks:**
- [ ] Create Python client examples for Olog
- [ ] Create Python client examples for ChannelFinder
- [ ] Create Python client examples for Archive Appliance
- [ ] Document authentication from Python
- [ ] Create Jupyter notebook examples

**Deliverables:**
- Python example scripts
- Jupyter notebooks
- Requirements.txt and setup guide

**Assigned To:** _Available_

---

## Documentation Infrastructure

### DOC-INFRA-001: Documentation Site Setup

**Repository:** New documentation site repository  
**Difficulty:** Intermediate  
**Estimated Time:** 3-4 days  
**Skills Required:** Static Site Generators (Sphinx, MkDocs), HTML/CSS  

**Tasks:**
- [ ] Set up centralized documentation site
- [ ] Configure build system (ReadTheDocs, GitHub Pages)
- [ ] Create documentation structure and navigation
- [ ] Implement search functionality
- [ ] Set up automated builds from repositories
- [ ] Configure versioning

**Deliverables:**
- Documentation website
- Build configuration
- Contribution guide for documentation

**Assigned To:** _Available_

---

### DOC-INFRA-002: Documentation Standards

**Repository:** Documentation repository  
**Difficulty:** Beginner  
**Estimated Time:** 1-2 days  
**Skills Required:** Technical Writing  

**Tasks:**
- [ ] Create documentation style guide
- [ ] Define templates for different doc types
- [ ] Document screenshot standards
- [ ] Create diagram guidelines
- [ ] Set up documentation review process

**Deliverables:**
- Style guide document
- Templates
- Review checklist

**Assigned To:** _Available_

---

## Migration and Updates

### DOC-MIG-001: Legacy Documentation Migration

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Intermediate  
**Estimated Time:** 3 days  
**Skills Required:** Technical Writing, Version Comparison  

**Tasks:**
- [ ] Review CS-Studio legacy documentation
- [ ] Identify relevant content for Phoebus
- [ ] Update and migrate applicable documentation
- [ ] Create migration guide from CS-Studio to Phoebus
- [ ] Document feature differences

**Deliverables:**
- Migrated documentation
- Migration guide
- Feature comparison matrix

**Assigned To:** _Available_

---

### DOC-MIG-002: Documentation Audit

**Repository:** All repositories  
**Difficulty:** Beginner  
**Estimated Time:** 2 days  
**Skills Required:** Attention to Detail  

**Tasks:**
- [ ] Review all existing documentation
- [ ] Identify outdated content
- [ ] Check broken links
- [ ] Verify screenshot currency
- [ ] Create update priority list

**Deliverables:**
- Documentation audit report
- Priority update list
- Dead link report

**Assigned To:** _Available_

---

## Video Documentation

### DOC-VID-001: Tutorial Videos

**Repository:** YouTube channel or documentation site  
**Difficulty:** Intermediate  
**Estimated Time:** 4 days  
**Skills Required:** Screen Recording, Video Editing  

**Tasks:**
- [ ] Create "Introduction to Phoebus" video
- [ ] Create "Building Your First Display" video
- [ ] Create "Using the Databrowser" video
- [ ] Create "Alarm System Overview" video
- [ ] Create "Service Configuration" videos

**Deliverables:**
- Video tutorials (5-10 minutes each)
- Video transcripts
- YouTube channel setup

**Assigned To:** _Available_

---

## Documentation Task Sign-up Sheet

| Task ID | Title | Assigned To | Status | Priority |
|---------|-------|-------------|--------|----------|
| DOC-USER-001 | Application User Guides | | Not Started | High |
| DOC-USER-002 | Olog User Docs | | Not Started | High |
| DOC-USER-003 | ChannelFinder User Guide | | Not Started | Medium |
| DOC-USER-004 | Archive User Guide | | Not Started | Medium |
| DOC-DEV-001 | Plugin Development | | Not Started | High |
| DOC-DEV-002 | Custom Widget Dev | | Not Started | High |
| DOC-DEV-003 | Service Dev Guide | | Not Started | Medium |
| DOC-DEV-004 | Contributing Guide | | Not Started | High |
| DOC-DEV-005 | Core Java Docs | | Not Started | Medium |
| DOC-INSTALL-001 | Phoebus Installation | | Not Started | High |
| DOC-INSTALL-002 | Docker Deployment | | Not Started | High |
| DOC-INSTALL-003 | Service Configuration | | Not Started | High |
| DOC-API-001 | REST API Docs | | Not Started | High |
| DOC-API-002 | JavaDoc | | Not Started | Medium |
| DOC-TUT-001 | Getting Started | | Not Started | High |
| DOC-TUT-002 | Display Builder Cookbook | | Not Started | High |
| DOC-TUT-003 | Integration Examples | | Not Started | Medium |
| DOC-TUT-004 | Python Client Examples | | Not Started | Medium |
| DOC-INFRA-001 | Documentation Site | | Not Started | High |
| DOC-INFRA-002 | Doc Standards | | Not Started | Medium |
| DOC-MIG-001 | Legacy Migration | | Not Started | Low |
| DOC-MIG-002 | Documentation Audit | | Not Started | Medium |
| DOC-VID-001 | Tutorial Videos | | Not Started | Low |

---

## Documentation Tools and Resources

### Recommended Tools
- **Markdown Editors:** VS Code, Typora, MacDown
- **Diagram Tools:** draw.io, PlantUML, Mermaid
- **Screenshot Tools:** Snagit, ShareX, macOS Screenshot
- **Screen Recording:** OBS Studio, Camtasia
- **API Documentation:** Swagger/OpenAPI, Postman
- **Static Site Generators:** Sphinx, MkDocs, Jekyll

### Documentation Guidelines
- Use clear, concise language
- Include code examples where applicable
- Add screenshots for UI-related documentation
- Keep step-by-step instructions numbered
- Use consistent formatting
- Test all examples before publishing
- Include version information

### Review Process
1. Self-review for clarity and accuracy
2. Peer review by another documentathon participant
3. Technical review by subject matter expert
4. Final approval by repository maintainer

---

## Daily Documentation Stand-up

**Time:** 9:45 AM (after main stand-up)  
**Format:**
- What documentation did you work on?
- What will you document today?
- Do you need technical input from developers?
- Any questions about features or functionality?

---

## Getting Technical Help

When documenting features:
1. Ask developers during their break times
2. Post questions in Matrix chat
3. Schedule short pairing sessions for complex features
4. Review existing code and tests for clarification
