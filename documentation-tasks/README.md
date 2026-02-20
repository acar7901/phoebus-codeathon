# Documentathon Tasks
## 2026 EPICS Codeathon - Phoebus Documentation Track

Documentation is a critical part of making Phoebus tools and services accessible to users and developers. This track focuses on improving, creating, and organizing documentation.

---

## Documentation Categories

1. [Documentation Structure Standardization](#documentation-structure-standardization)
2. [User Documentation](#user-documentation)
3. [Developer Documentation](#developer-documentation)
4. [Installation & Deployment Guides](#installation--deployment-guides)
5. [API Documentation](#api-documentation)
6. [Tutorials & Examples](#tutorials--examples)

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

## Documentation Structure Standardization

### DOC-STRUCT-001: Documentation Structure by User Profile

**Repositories:** Multiple (Phoebus, ChannelFinder, Olog, Save & Restore, Alarm Services)  
**Difficulty:** Intermediate  
**Estimated Time:** 1 week  
**Skills Required:** Technical Writing, Documentation Architecture, ReadTheDocs/Sphinx  

**Problem:**  
Phoebus ecosystem mix user, developer, and admin documentation together, making it difficult for each audience to find relevant information. Documentation needs to be reorganized by user profile/role.

**Current State:**
- ChannelFinder: https://channelfinder.readthedocs.io/en/latest/
- Olog: https://olog.readthedocs.io/en/latest/
- Save & Restore: https://control-system-studio.readthedocs.io/en/latest/services/save-and-restore/doc/index.html
- Alarm Server: https://control-system-studio.readthedocs.io/en/latest/services/alarm-server/doc/index.html

**Tasks:**
- [ ] Audit current documentation and categorize content by target audience
- [ ] Design documentation structure organized by user profile:
  - **Operator**: Using applications, viewing displays, interacting with services
  - **Display Designer**: Creating displays, widget properties, PV syntax, simulated PVs
  - **System Administrator**: Installation, deployment, configuration, maintenance, troubleshooting
  - **Developer/Contributor**: API reference, architecture, contributing guidelines, development setup
- [ ] Consider [Diátaxis](https://diataxis.fr/) framework within each profile:
  - Tutorials (learning-oriented)
  - How-To Guides (task-oriented)
  - Reference (information-oriented)
  - Explanation (understanding-oriented)
- [ ] Move CONTRIBUTING.md and ARCHITECTURE.md from docs to repository root (developer-focused, not user docs)
- [ ] Define what content belongs in README.md vs full documentation
- [ ] Implement reorganization for one service as proof-of-concept (Olog recommended)
- [ ] Create migration guide for applying structure to other services

**Deliverables:**
- User profile-based documentation structure template
- One fully restructured service (Olog)
- Migration guide for other services

**Reference:**
- Discussion topic: [4.4 Documentation Strategy](discussion-topics/README.md#44-documentation-strategy)
- GitHub Issue #3558: https://github.com/ControlSystemStudio/phoebus/issues/3558

**Assigned To:** _Available_

---

### DOC-STRUCT-002: Documentation Standardization Across Repositories

**Repositories:** Multiple (Phoebus, ChannelFinder, Olog, Save & Restore, Alarm Services, Archiver Appliance)  
**Difficulty:** Advanced  
**Estimated Time:** 1-2 weeks  
**Skills Required:** Sphinx, MkDocs, OpenAPI/Swagger, JavaDoc, Technical Writing  

**Problem:**  
Each Phoebus service uses different documentation tools, organization patterns, and quality levels. Need consistent structure, tooling, and auto-generated documentation across the entire ecosystem.

**Current Inconsistencies:**
- Mixed tooling (Sphinx vs MkDocs vs plain markdown)
- Different section organization patterns
- Inconsistent API documentation (some use Swagger, some JavaDoc only, some have none)
- Varying levels of completeness
- No cross-repository linking strategy
- Different hosting approaches

**Tasks:**
- [ ] Standardize on documentation generator (recommend Sphinx with ReadTheDocs)
- [ ] Create standard section organization template:
  - Getting Started (quick start, prerequisites)
  - Installation & Deployment
  - Configuration Reference
  - User Guide (operations)
  - API Reference (REST, Java)
  - Administration Guide
  - Development Guide
  - Troubleshooting
- [ ] Standardize auto-generated documentation:
  - REST APIs: OpenAPI/Swagger specs with consistent formatting
  - Java APIs: JavaDoc with standardized structure and cross-linking
  - Configuration: Auto-generate from code annotations where possible
- [ ] Create shared documentation templates:
  - Installation page template
  - Configuration page template  
  - API endpoint documentation template
  - Troubleshooting page template
- [ ] Establish cross-repository linking conventions (linking between Phoebus <-> Olog, ChannelFinder, etc)
- [ ] Define hosting strategy and URL structure consistency
- [ ] Create documentation style guide for writers
- [ ] Implement standardization for 2-3 services as examples

**Deliverables:**
- Documentation tooling recommendation and rationale
- Standard section hierarchy template
- Shared documentation templates (Sphinx/RST)
- Auto-generated documentation standards and tooling
- Documentation style guide
- Cross-repository linking guide
- 2-3 services fully migrated to standard structure

**Reference:**
- Discussion topic: [4.4 Documentation Strategy](discussion-topics/README.md#44-documentation-strategy)

**Assigned To:** _Available_

---

### DOC-STRUCT-003: Multi-version Documentation on ReadTheDocs

**Repositories:** Multiple (Phoebus, ChannelFinder, Olog, Save & Restore, Alarm Services)  
**Difficulty:** Beginner  
**Estimated Time:** 2-3 days  
**Skills Required:** ReadTheDocs, Git tags, Documentation versioning  

**Problem:**  
Phoebus services only publish documentation for the latest master branch. Users on older releases cannot access version-specific documentation, and there's no way to compare documentation between versions.

**Tasks:**
- [ ] Configure ReadTheDocs to build all tagged releases (SemVer pattern)
- [ ] Set default documentation version to `stable` (latest release) instead of `latest` (master branch)
- [ ] Enable version selector flyout menu in ReadTheDocs theme
- [ ] Add automation rules to trigger builds on new tag creation
- [ ] Test version switching functionality
- [ ] Document versioning workflow for maintainers (when to tag, how versions are built)
- [ ] Add version banner/notice to documentation indicating which version user is viewing
- [ ] Implement for all services with tagged releases

**Deliverables:**
- ReadTheDocs configuration for multi-version builds
- Version switcher enabled in documentation UI
- Documentation for maintainers on versioning workflow

**Reference:**
- Discussion topic: [4.4 Documentation Strategy](discussion-topics/README.md#44-documentation-strategy)
- GitHub Issue: https://github.com/ControlSystemStudio/phoebus/issues/3556
- Proof of concept: https://phoebus-test.readthedocs.io/

**Assigned To:** _Available_

---

### DOC-STRUCT-004: Improve Phoebus.org Website

**Repository:** https://github.com/ControlSystemStudio/phoebus.org  
**Difficulty:** Intermediate  
**Estimated Time:** 3-5 days  
**Skills Required:** Web Development, Technical Writing, Community Management  

**Problem:**  
Phoebus.org serves as the main landing page for the Phoebus ecosystem but has outdated links, missing information, and insufficient emphasis on community collaboration. The site needs updates to better serve as the entry point for users, developers, and contributors.

**Tasks:**
- [ ] **Update Links and References**:
  - Audit all external links (GitHub repos, documentation sites, downloads)
  - Update broken or outdated links
  - Ensure links point to correct ReadTheDocs documentation
  - Add links to all ecosystem services (ChannelFinder, Olog, Save & Restore, Alarm Services, Archiver Appliance)
  - Link to community resources (Matrix chat, mailing lists, GitHub Discussions)
- [ ] **Add Missing Information**:
  - Complete service descriptions for all middleware services
  - Add "Getting Started" quickstart guide
  - Include architecture overview diagram showing how services interact
  - Add deployment options overview (bare metal, containers, cloud)
  - List key features and capabilities
  - Add FAQ section for common questions
- [ ] **Expand Collaboration Section**:
  - Highlight community contribution opportunities
  - Add "How to Contribute" section with clear paths for different skill levels
  - Showcase community contributors and facilities using Phoebus
  - Add community calendar (codeathons, meetings, webinars)
  - Link to CONTRIBUTING.md in main repository
  - Add code of conduct
  - Include community communication channels (Matrix, GitHub, mailing lists)
  - Feature community success stories and case studies
- [ ] **Improve Site Organization**:
  - Clear navigation: About, Documentation, Services, Community, Download, Support
  - Separate pages for different audiences (users, developers, administrators)
  - Add search functionality
  - Responsive design for mobile/tablet
- [ ] **Technical Updates**:
  - Update site generator dependencies
  - Improve build process and deployment
  - Add analytics to understand user engagement

**Deliverables:**
- Updated Phoebus.org website with current links and information
- Enhanced community collaboration section
- Improved site structure and navigation
- Documentation for site maintainers

**Reference:**
- Current site: https://phoebus.org (or phoebus-doc.readthedocs.io)
- Discussion topic: [4.4 Documentation Strategy](discussion-topics/README.md#44-documentation-strategy)

**Assigned To:** _Available_

---

## User Documentation
