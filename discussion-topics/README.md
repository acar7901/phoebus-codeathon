# Core Developers Discussion Topics
## Monday, February 23rd, 2026

This document outlines the technical discussion topics for the Phoebus Tools and Services core developers session.

---

## Discussion Format

- **Duration:** 
- **Participants:** Developers and maintainers
- **Goal:** Strategic planning, architecture discussions, and technical decisions

---

## Technical Discussion Topics

### 1. Architecture & Framework

#### 1.1 Phoebus Framework Evolution
- [ ] Future of the RCP (Rich Client Platform) architecture
- [ ] Plugin system improvements and standardization
- [ ] Resource management and memory optimization
- [ ] Cross-platform compatibility challenges (Windows, Linux, macOS)

#### 1.2 UI/UX Framework Modernization
- [ ] JavaFX version strategy and roadmap
- [ ] CSS styling and theming improvements
- [ ] Responsive design patterns for different screen sizes
- [ ] Dark mode and accessibility enhancements
- [ ] Custom controls and widget library expansion

#### 1.3 Build System & Dependencies
- [ ] Dependency management and version conflicts
- [ ] Modularization strategy (Java modules/JPMS)
- [ ] CI/CD pipeline improvements

---

### 2. Middle Layer Services

#### 2.1 Service Architecture
- [ ] REST API standardization across services
- [ ] Authentication and authorization strategy (OAuth2, JWT, LDAP)
- [ ] Service discovery and registration
- [ ] Load balancing and high availability

#### 2.2 Archiver Service
- [ ] Archive Appliance performance tuning
- [ ] Data retrieval optimization strategies
- [ ] Storage backend options

#### 2.3 Olog Integration
- [ ] Search and indexing improvements (Elasticsearch integration)
- [ ] Template system enhancements
- [ ] Integration with other services (ChannelFinder, Alarm)
- [ ] Notification mechanisms

#### 2.4 ChannelFinder Service
- [ ] Property and tag management
- [ ] Scalability for large installations (10M+ channels)
- [ ] Integration with PVAccess and ChannelAccess Nameserver

#### 2.5 Alarm Services
- [ ] Alarm configuration management
- [ ] Notification systems (email, SMS, messaging platforms)
- [ ] Alarm history and analytics

---

### 3. Data Access & Performance

#### 3.1 EPICS Core Java (PVA)
- [ ] Connection management and reconnection strategies
- [ ] Compatibility with EPICS 7 features

#### 3.2 PV Access Layer
- [ ] ???

---

### 4. Development Practices & Community

#### 4.1 Code Quality & Standards
- [ ] Coding standards and style guides
- [ ] Static analysis tools integration
- [ ] Unit testing and test coverage goals
- [ ] Documentation standards

#### 4.2 Release Management
- [ ] Versioning strategy (semantic versioning)
- [ ] Release cycle and timing
- [ ] LTS (Long Term Support) versions
- [ ] Backwards compatibility policies
- [ ] Migration guides and upgrade paths

#### 4.3 Community Engagement
- [ ] ???

---

### 5. Security & Deployment

#### 5.1 Security Considerations
- [ ] Secure communication channels (TLS/SSL)
- [ ] Credential management (avoiding hardcoded passwords)
- [ ] Access control and permissions model

#### 5.2 Deployment Strategies
- [ ] Containerization (Docker, Kubernetes)
- [ ] Configuration management
- [ ] Monitoring and alerting
- [ ] Disaster recovery and backup strategies

---

### 6. Roadmap & Future Features

#### 6.1 Roadmap 
- [ ] Timeline for major releases


#### 6.2 Future Features 
- [ ] Web-based interfaces vs native applications
- [ ] Mobile support considerations
- [ ] AI/ML integration opportunities
- [ ] Next-generation control system requirements

---

### 7. Technical Debt & Refactoring
- [ ] Identification of major technical debt areas
- [ ] Deprecated API removal strategy
- [ ] Legacy code migration plans

---

## Meeting Notes

_To be filled during the session on Monday, February 23rd_

---

## References

- [Phoebus Documentation](https://github.com/ControlSystemStudio/phoebus/tree/master/docs)
- [EPICS Website](https://epics-controls.org/)
- [Previous Codeathon Reports](https://epics.anl.gov/meetings/)
