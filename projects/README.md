# Development Projects
## 2026 EPICS Codeathon - Phoebus Track

This directory contains the list of development projects for the Phoebus tools and services during the codeathon week.

---

## How to Use This Guide

1. Browse through the project list
2. Check the **Difficulty** level (Beginner, Intermediate, Advanced)
3. Review **Prerequisites** and **Skills Required**
4. Sign up by adding your name to the project
5. Create a GitHub issue in the respective repository
6. Fork the repository and create a feature branch
7. Submit a pull request when ready

---

## Projects

### ALARM-KAFKA-001: Enhanced Kafka Streams Error Handling

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Advanced  
**Estimated Time:** 3-4 days  
**Skills Required:** Java, Kafka Streams API, Error Handling Patterns  

**Description:**  
Implement robust error handling for Kafka Streams in alarm logger and alarm config logger services using the latest Kafka Streams API patterns. Currently, services can fail silently or terminate when encountering deserialization errors, malformed messages, transient Kafka issues, or missing/deleted topics.

- Add `StreamsUncaughtExceptionHandler` to all KafkaStreams instances in `AlarmMessageLogger`, `AlarmCmdLogger`, and `AlarmConfigLogger` to handle fatal errors and decide on stream continuation vs. shutdown
- Implement custom `DeserializationExceptionHandler` for handling corrupted messages without stopping the entire stream
- Add `ProductionExceptionHandler` for producer-side error handling
- Handle `MissingSourceTopicException` by logging the error, preventing service crash, and allowing retry logic to eventually reconnect when topics are created
- Log structured error information (message offset, partition, topic, error type) for debugging
- Implement graceful degradation: continue processing valid messages despite errors in other messages
- Add metrics/counters for error rates per error type (deserialization failures, missing topics, transient errors)
- Create unit tests with intentionally malformed Kafka messages and missing topic scenarios

**Resources:**
- `services/alarm-logger/src/main/java/org/phoebus/alarm/logging/AlarmMessageLogger.java`
- `services/alarm-logger/src/main/java/org/phoebus/alarm/logging/AlarmCmdLogger.java`
- `services/alarm-config-logger/src/main/java/org/phoebus/alarm/logging/AlarmConfigLogger.java`
- Kafka Streams error handling: https://kafka.apache.org/41/documentation/streams/developer-guide/config-streams.html#default-deserialization-exception-handler

**Assigned To:** _Available_

---

### ALARM-KAFKA-002: Resilient Topic Handling with Retry Logic

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Intermediate  
**Estimated Time:** 3 days  
**Skills Required:** Java, Kafka Admin API, Retry Patterns  

**Description:**  
Enhance alarm logger and alarm configuration logger services to gracefully handle missing or deleted Kafka topics with automatic retry logic. Currently, services fail on startup if topics don't exist.

- Modify `AlarmMessageLogger`, `AlarmCmdLogger`, and `AlarmConfigLogger` to catch topic-not-found exceptions on startup and during runtime
- Implement exponential backoff retry strategy (initial: 5s, max: 5min, backoff: 2x)
- Add periodic topic existence checks using Kafka `AdminClient` to verify topic availability
- Log messages about missing topics and retry attempts with countdown timers
- When topics appear, automatically initialize streams and resume processing without requiring service restart
- Ensure service remains running in degraded state during topic unavailability, providing health check endpoints that reflect the degraded status
- Add configuration properties for retry intervals and max retry attempts
- Services should recover automatically without restart when topics are recreated, reconnecting to Kafka and resuming message processing

**Resources:**
- `services/alarm-logger/src/main/java/org/phoebus/alarm/logging/AlarmLoggingService.java`
- `services/alarm-config-logger/src/main/java/org/phoebus/alarm/logging/AlarmConfigLoggingService.java`
- `app/alarm/model/src/main/java/org/phoebus/applications/alarm/client/KafkaHelper.java`
- Example: `services/alarm-server/src/main/java/org/phoebus/applications/alarm/server/CreateTopics.java`

**Assigned To:** _Available_

---

### ALARM-REST-001: Alarm Configuration REST API

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Intermediate  
**Estimated Time:** 2-3 days  
**Skills Required:** Java, Spring Boot, REST API Design, Kafka  

**Description:**  
Create a REST API for the alarm configuration service that exposes read-only access to the current alarm tree configuration.

- Add REST controller to alarm-config-logger or create new alarm-config-service module
- Implement GET endpoints:
  - `/api/config/{root}` - Get entire alarm tree for configuration root
- Return the complete alarm config as xml (or json)
- Add OpenAPI/Swagger documentation
- Implement proper HTTP status codes (404 for missing nodes)

**Resources:**
- `services/alarm-config-logger/src/main/java/org/phoebus/alarm/logging/AlarmConfigLogger.java`
- `app/alarm/model/src/main/java/org/phoebus/applications/alarm/client/AlarmClient.java`
- `services/alarm-logger/src/main/java/org/phoebus/alarm/logging/rest/SearchController.java` (existing REST example)
- `app/alarm/model/src/main/java/org/phoebus/applications/alarm/model/json/JsonModelWriter.java`

**Assigned To:** _Available_

---

### ALARM-TOPICS-001: Centralized Kafka Topic Management Service

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Intermediate  
**Estimated Time:** 2-3 days  
**Skills Required:** Java, Kafka Admin API, Refactoring  

**Description:**  
Refactor the alarm server's Kafka topic creation and configuration logic into a centralized utility class or service. Currently, topic management code is scattered across multiple locations (AlarmServerMain, AggregateTopics) with inconsistent patterns and configuration.

- Create a dedicated `KafkaTopicManager` service class in the alarm-server module
- Consolidate all topic creation logic from `AlarmServerMain` and `AggregateTopics` into the new service
- Implement consistent topic configuration (partitions, replication factor, retention, cleanup policy)
- Make topic attributes configurable via Phoebus preferences (replication factor, partitions, retention policy, backup settings)
- Implement topic validation and health checks (verify topic exists, check configuration matches expectations)
- Add logging for all topic operations with structured information
- Add unit tests with embedded Kafka or mock AdminClient
- Update `AlarmServerMain` and `AggregateTopics` to use the new service

**Resources:**
- `services/alarm-server/src/main/java/org/phoebus/applications/alarm/server/AlarmServerMain.java`
- `services/alarm-server/src/main/java/org/phoebus/applications/alarm/server/AggregateTopics.java`
- Kafka AdminClient API: https://kafka.apache.org/41/javadoc/org/apache/kafka/clients/admin/AdminClient.html
- Topic configuration: https://kafka.apache.org/41/documentation.html#topicconfigs

**Assigned To:** _Available_

---

### PHOEBUS-VT-001: Virtual Threads Integration Assessment

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Advanced  
**Estimated Time:** 3-4 days  
**Skills Required:** Java 21, Concurrency, Performance Analysis, Virtual Threads  

**Description:**  
Identify and prototype Virtual Threads (Project Loom) integration opportunities across Phoebus services and tools. Analyze current threading model, identify blocking operations, and create proof-of-concept implementations showing performance improvements with virtual threads.

- Document current threading model in alarm-server, alarm-logger, alarm-config-logger, save-and-restore, scan-server
- Identify blocking operations: Kafka I/O, Elasticsearch writes, Git operations, PV connections, database queries
- Create branch with Virtual Thread executors for:
  - Elasticsearch bulk write operations in `AlarmMessageLogger`
  - Git commit operations in `AlarmConfigLogger`
  - PV connection handling in `AlarmServer` (ServerModel)
  - Database operations in save-and-restore service
  - Scan engine PV processing
- Test with realistic load: 10k+ PVs, 100+ alarms/second, concurrent save-and-restore operations
- Document migration strategy: code changes, JVM requirements, configuration

**Resources:**
- `services/alarm-server/src/main/java/org/phoebus/applications/alarm/server/ServerModel.java`
- `services/alarm-logger/src/main/java/org/phoebus/alarm/logging/AlarmMessageLogger.java`
- `services/alarm-config-logger/src/main/java/org/phoebus/alarm/logging/AlarmConfigLogger.java`
- `services/save-and-restore/src/main/java/org/phoebus/service/saveandrestore/`
- JEP 444: Virtual Threads - https://openjdk.org/jeps/444

**Assigned To:** _Available_

---

### SERVICES-HEALTH-001: Standardize Health Endpoint Implementation

**Repository:** Multiple (Olog, ChannelFinder, Save & Restore, Alarm Services)  
**Difficulty:** Intermediate  
**Estimated Time:** 2-3 days  
**Skills Required:** Java, Spring Boot Actuator, Health Indicators  

**Description:**  
Standardize Spring Boot Actuator health endpoints across all Phoebus middle layer services to provide consistent health monitoring and enable reliable Kubernetes probes, load balancer health checks, and service mesh integration.

- Implement custom `HealthIndicator` beans for service-specific health checks:
  - Database connectivity (Elasticsearch, PostgreSQL, MongoDB)
  - Kafka connectivity and topic availability
  - Disk space and memory thresholds
- Create health groups for Kubernetes liveness/readiness probes (`/actuator/health/liveness`, `/actuator/health/readiness`)
- Add custom health status mappings (map service-specific error states to HTTP status codes)
- Document health endpoint structure and expected response formats
- Configure health endpoint exposure in `application.properties` consistently across all services

**Resources:**
- `services/alarm-logger/src/main/java/org/phoebus/alarm/logging/`
- `services/save-and-restore/src/main/java/org/phoebus/service/saveandrestore/`
- Phoebus-Olog: https://github.com/Olog/phoebus-olog
- ChannelFinder: https://github.com/ChannelFinder/ChannelFinderService
- Spring Boot Actuator Health: https://docs.spring.io/spring-boot/reference/actuator/endpoints.html#actuator.endpoints.health

**Assigned To:** _Available_

---

### SERVICES-SB4-001: Spring Boot 4 Migration Planning

**Repository:** Multiple (Olog, ChannelFinder, Save & Restore)  
**Difficulty:** Advanced  
**Estimated Time:** 4-5 days  
**Skills Required:** Java, Spring Boot 3/4, Migration Planning  

**Description:**  
Create comprehensive migration plan and proof-of-concept for upgrading Phoebus middle layer services from Spring Boot 3.x to Spring Boot 4.x, leveraging new features while ensuring backward compatibility.

- Audit current Spring Boot 3.x usage across all services (dependencies, configurations, custom code)
- Document breaking changes and deprecations in Spring Boot 4:
  - Spring Security 7 authorization architecture changes
  - RestTemplate deprecation (migrate to HTTP Interface clients)
  - Configuration property changes
  - Minimum Java version requirements (JDK 21+)
- Create migration checklist with service-specific considerations:
  - Update `pom.xml`/`build.gradle` dependencies
  - Migrate security configurations to Spring Security 7 patterns
  - Replace RestTemplate with declarative HTTP Interface clients
  - Update actuator endpoint configurations
- Implement pilot migration for one service (Save & Restore or Alarm Logger) as proof-of-concept
- Test virtual threads integration with `spring.threads.virtual.enabled=true`
- Leverage Problem Details (RFC 7807) for standardized error responses
- Enable OpenTelemetry observability with `management.tracing.enabled=true`
- Document rollback strategy and deployment considerations

**Resources:**
- Spring Boot 4 roadmap: https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-4.0-Release-Notes
- Spring Boot 3.4 features: https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.4-Release-Notes
- Spring Security 7: https://docs.spring.io/spring-security/reference/7.0/migration/index.html
- HTTP Interface clients: https://docs.spring.io/spring-framework/reference/integration/rest-clients.html#rest-http-interface

**Assigned To:** _Available_

---

### SERVICES-VERSIONING-001: REST API Versioning Strategy

**Repository:** Multiple (Olog, ChannelFinder, Save & Restore, Alarm Services)  
**Difficulty:** Intermediate  
**Estimated Time:** 3-4 days  
**Skills Required:** Java, Spring Boot, REST API Design, Versioning Patterns  

**Description:**  
Implement consistent REST API versioning across all Phoebus middle layer services to support backward compatibility, gradual feature rollout, and deprecation policies without breaking existing clients.

- Evaluate versioning strategies and select one approach:
  - URL path versioning: `/api/v1/logs`, `/api/v2/logs` (recommended for clarity)
  - Header-based versioning: `Accept: application/vnd.phoebus.v1+json`
  - Query parameter versioning: `/api/logs?version=1`
- Implement chosen strategy using Spring Boot features:
  - `@RequestMapping` with version prefix
  - Custom `RequestCondition` for header-based versioning
  - Version-specific controller classes or methods
- Create versioning policy document:
  - When to introduce new version (breaking changes only)
  - How long to support deprecated versions (e.g., N-2 policy)
  - Version deprecation headers (`Deprecation`, `Sunset`)
  - Migration guides for each version bump
- Implement version negotiation with default version fallback
- Add OpenAPI/Swagger documentation showing all supported versions
- Update existing endpoints to v1, prepare v2 structure for future changes
- Add integration tests covering multiple API versions simultaneously
- Create client migration examples (Python, Java, curl)

**Resources:**
- REST API Versioning Best Practices: https://restfulapi.net/versioning/
- Spring Boot REST versioning: https://www.baeldung.com/rest-versioning
- OpenAPI versioning: https://swagger.io/docs/specification/api-general-info/
- Existing service REST endpoints:
  - Olog: https://github.com/Olog/phoebus-olog
  - ChannelFinder: https://github.com/ChannelFinder/ChannelFinderService
  - Alarm Logger: `services/alarm-logger/src/main/java/org/phoebus/alarm/logging/rest/`

**Assigned To:** _Available_

---

### AI-DISPLAY-001: LLM-Assisted Display Screen Generation

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Advanced  
**Estimated Time:** 4-5 days  
**Skills Required:** Python/Java, LLM APIs (OpenAI/Anthropic/local models), Display Builder, Prompt Engineering  

**Description:**  
Explore using Large Language Models (LLMs) to generate Phoebus Display Builder screens (.bob files) from natural language descriptions or existing OPI/EDL files, accelerating screen development and migration from legacy CS-Studio.

- Research Display Builder XML/BOB file format structure:
  - Widget types (Label, TextUpdate, ActionButton, LED, Rectangle, Group, etc.)
  - Widget properties (position, size, PV names, colors, fonts)
  - Layout patterns and parent-child relationships
  - Rules, scripts, and actions
- Create prompt templates for LLM-based screen generation:
  - "Create a motor control screen with position readback, setpoint, start/stop buttons"
  - "Convert this EDM/EDL screen to Display Builder format"
  - "Generate a vacuum system overview with 12 gauge indicators arranged in a grid"
- Implement generation pipeline:
  - LLM API integration (OpenAI GPT-4, Claude, or local Llama models)
  - Prompt engineering with few-shot examples of BOB XML
  - XML validation and widget property verification
  - Post-processing to fix common LLM errors (invalid colors, missing required properties)
- Test with various complexity levels:
  - Simple screens (5-10 widgets)
  - Complex screens (100+ widgets, embedded displays, macros)
- Document findings: success rates, limitations, best practices, cost analysis

**Resources:**
- Display Builder format: `app/display/model/src/main/resources/` (XSD schema)
- Example displays: `app/display/model/src/main/resources/examples/`
- Widget implementations: `app/display/representation-javafx/src/main/java/org/csstudio/display/builder/representation/javafx/widgets/`
- LLM APIs: OpenAI, Anthropic Claude, Ollama (local), Hugging Face
- Legacy conversion examples: EDM, MEDM, BOY formats for training data

**Assigned To:** _Available_

---

### AI-DISPLAY-002: LLM-Based Display Screen CI/CD Validator

**Repository:** New GitHub Actions / CI tools repository  
**Difficulty:** Intermediate  
**Estimated Time:** 3-4 days  
**Skills Required:** Python, GitHub Actions, LLM APIs, Display Builder, XML parsing  

**Description:**  
Develop an LLM-powered automated validator for Display Builder screens (.bob files) that integrates into CI/CD pipelines to enforce design conventions, detect errors, and ensure quality standards before merging to production.

- Implement validation engine with multiple checks:
  - Static analysis: Schema validation, property ranges, XML correctness
  - Convention enforcement: Naming patterns, layout standards, color palette, fonts
  - LLM semantic analysis: "Does layout make sense?", "Are PV names consistent?", "Are labels clear?"
  - Security: No hardcoded credentials, valid PV patterns
  - Performance: Widget count limits, embedding depth
  - Accessibility: Contrast ratios, text sizes
- Create GitHub Actions workflow:
  - Trigger on PRs with `.bob` file changes
  - Post detailed reports and auto-fix suggestions as PR comments
  - Configurable severity levels (error/warning/info)
- Build configuration system:
  - YAML-based facility-specific rules
  - Custom validation patterns and LLM prompts
  - Exemption mechanisms with justification
- Generate reports:
  - Markdown PR summaries with line numbers
  - JSON output for programmatic use
  - Metrics dashboard showing violation trends
- Support multiple platforms: GitHub Actions, GitLab CI/CD, Jenkins, pre-commit hooks

**Resources:**
- GitHub Actions: https://docs.github.com/en/actions
- GitHub API for PR comments: https://docs.github.com/en/rest/pulls/comments
- Display Builder XSD: `app/display/model/src/main/resources/`
- Python XML parsing: `lxml`, `xmlschema`
- LLM APIs: OpenAI (with structured outputs), Claude (with tool use), local models
- CI/CD examples: Super-Linter, actionlint, vale for similar validation patterns

**Assigned To:** _Available_

---

### AI-ASSIST-001: LLM-Powered Phoebus Development Assistant

**Repository:** New AI tools repository  
**Difficulty:** Intermediate  
**Estimated Time:** 3-4 days  
**Skills Required:** Python, LLM APIs, RAG (Retrieval Augmented Generation), Vector Databases  

**Description:**  
Build an AI assistant that helps Phoebus developers by answering questions about the codebase, suggesting code patterns, and providing context-aware documentation using Retrieval Augmented Generation (RAG).

- Create knowledge base from Phoebus ecosystem:
  - Index Phoebus source code, JavaDoc, markdown documentation
  - Index Display Builder widget API documentation
  - Index common code patterns (service implementations, widget examples)
  - Index GitHub issues, discussions, and wiki pages
- Explore RAG pipeline:
  - Document chunking and embedding (OpenAI embeddings or open-source alternatives)
  - Semantic search for relevant context retrieval
  - LLM integration (GPT-4, Claude, or local models like CodeLlama)
  - Prompt construction with retrieved context
- Support use cases:
  - "How do I create a custom widget in Display Builder?"
  - "What's the difference between AlarmTree and AlarmTable?"
- Implement features:
  - Citation links back to source code/docs
  - Context window management for long conversations
- Evaluate usefullness:
  - Test on 20-30 common developer questions
  - Measure answer accuracy and relevance
  - Compare to manual documentation search time
  - Collect user feedback on usefulness

**Resources:**
- RAG frameworks: LangChain, LlamaIndex, Haystack
- Vector databases: ChromaDB, FAISS, Weaviate
- Phoebus documentation: https://github.com/ControlSystemStudio/phoebus/tree/master/docs
- Code embedding models: OpenAI `text-embedding-3`, `code-bison`, CodeBERT

**Assigned To:** _Available_

---

### AI-LOG-001: Intelligent Log Analysis for Alarm Logs

**Repository:** New AI/ML analysis tools  
**Difficulty:** Intermediate  
**Estimated Time:** 3 days  
**Skills Required:** Java/Python, Log Parsing, Pattern Recognition  

**Description:**  
Apply natural language processing and pattern recognition to alarm service logs to automatically identify recurring issues, extract failure patterns, and provide actionable insights for control system behavior.

**Resources:**
- ???

**Assigned To:** _Available_

---

### DEVOPS-ANSIBLE-001: Phoebus Infrastructure Deployment

**Repository:** New ansible-phoebus-collection  
**Difficulty:** Intermediate  
**Estimated Time:** 4-5 days  
**Skills Required:** Ansible, Linux System Administration, Docker/Podman  

**Description:**  
Create a comprehensive Ansible collection with roles and playbooks for deploying the complete Phoebus tools and services technology stack. The collection should be generic and configurable enough for different facilities to adopt with minimal modifications.

- Design modular Ansible roles for each service: Phoebus client, Olog, ChannelFinder, Save & Restore, Alarm Server, Alarm Logger, Archiver Appliance
- Create roles for infrastructure dependencies: Elasticsearch, PostgreSQL, MongoDB, Kafka (KRaft mode)
- Implement role variables with sensible defaults and facility-specific overrides (ports, paths, credentials, heap sizes)
- Support multiple deployment targets: bare metal, containers (Docker/Podman), systemd services
- Include SSL/TLS certificate configuration and secure credential management (Ansible Vault)
- Add playbooks for common operations: deployment, updates, backups, health checks, scaling
- Implement idempotent tasks with proper error handling and rollback capabilities
- Create comprehensive documentation with example inventory files and variable configurations
- Package as Ansible Galaxy collection for easy distribution and installation
- Include molecule tests for role validation

**Resources:**
- Ansible best practices: https://docs.ansible.com/ansible/latest/tips_tricks/ansible_tips_tricks.html
- Ansible Galaxy collections: https://docs.ansible.com/ansible/latest/collections_guide/index.html
- Service repositories: https://github.com/ControlSystemStudio/
- Molecule testing: https://ansible.readthedocs.io/projects/molecule/

**Assigned To:** _Available_

---

## Project Sign-up Sheet

| Project ID | Title | Assigned To | Status | Notes |
|------------|-------|-------------|--------|-------|
| ALARM-KAFKA-001 | Enhanced Kafka Streams Error Handling | | Not Started | |
| ALARM-KAFKA-002 | Resilient Topic Handling with Retry Logic | | Not Started | |
| ALARM-REST-001 | Alarm Configuration REST API | | Not Started | |
| ALARM-TOPICS-001 | Centralized Kafka Topic Management Service | | Not Started | |
| PHOEBUS-VT-001 | Virtual Threads Integration Assessment | | Not Started | |
| SERVICES-HEALTH-001 | Standardize Health Endpoint Implementation | | Not Started | |
| SERVICES-SB4-001 | Spring Boot 4 Migration Planning | | Not Started | |
| SERVICES-VERSIONING-001 | REST API Versioning Strategy | | Not Started | |
| AI-DISPLAY-001 | LLM-Assisted Display Screen Generation | | Not Started | |
| AI-DISPLAY-002 | LLM-Based Display Screen CI/CD Validator | | Not Started | |
| AI-ASSIST-001 | LLM-Powered Phoebus Development Assistant | | Not Started | |
| AI-LOG-001 | Intelligent Log Analysis for Alarm Services | | Not Started | |
| DEVOPS-ANSIBLE-001 | Phoebus Infrastructure Deployment | | Not Started | |

---

## Getting Help

- Ask in the main room during work hours
- Use the Matrix chat: [#codeathon26:epics-controls.org](https://matrix.to/#/#codeathon26:epics-controls.org)
- Tag mentors: @Kunal Shroff, @Georg Weiss, @Sky Brewer
