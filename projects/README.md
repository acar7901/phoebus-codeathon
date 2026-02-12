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
- Log clear messages about missing topics and retry attempts with countdown timers
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
Create a REST API for the alarm configuration service that exposes read-only access to the current alarm tree configuration. This allows external tools, dashboards, and scripts to query alarm hierarchy and PV configurations without connecting directly to Kafka.

- Add REST controller to alarm-config-logger or create new alarm-config-service module
- Implement GET endpoints:
  - `/api/config/{root}` - Get entire alarm tree for configuration root
  - `/api/config/{root}/node/{path}` - Get specific node configuration
  - `/api/config/{root}/pv/{path}` - Get PV alarm configuration with guidance, displays, commands
  - `/api/config/{root}/search?query={term}` - Search for PVs or nodes
- Return JSON representation of `AlarmClientNode` and `AlarmTreeLeaf` objects
- Support path traversal (e.g., `/Accelerator/Vacuum/Sector01`)
- Include alarm state severity in responses (read from state topic)
- Add OpenAPI/Swagger documentation
- Implement proper HTTP status codes (404 for missing nodes)
- Add simple authentication/authorization checks

**Resources:**
- `services/alarm-config-logger/src/main/java/org/phoebus/alarm/logging/AlarmConfigLogger.java`
- `app/alarm/model/src/main/java/org/phoebus/applications/alarm/client/AlarmClient.java`
- `services/alarm-logger/src/main/java/org/phoebus/alarm/logging/rest/SearchController.java` (existing REST example)
- `app/alarm/model/src/main/java/org/phoebus/applications/alarm/model/json/JsonModelWriter.java`

**Assigned To:** _Available_

---

### ALARM-VT-001: Virtual Threads Integration Assessment

**Repository:** https://github.com/ControlSystemStudio/phoebus  
**Difficulty:** Advanced  
**Estimated Time:** 3-4 days  
**Skills Required:** Java 21, Concurrency, Performance Analysis, Virtual Threads  

**Description:**  
Identify and prototype Virtual Threads (Project Loom) integration opportunities in alarm services. Analyze current threading model, identify blocking operations, and create proof-of-concept implementations showing performance improvements with virtual threads.

- Document current threading model in alarm-server, alarm-logger, alarm-config-logger
- Identify blocking operations: Kafka I/O, Elasticsearch writes, Git operations, PV connections
- Create branch with Virtual Thread executors for:
  - Elasticsearch bulk write operations in `AlarmMessageLogger`
  - Git commit operations in `AlarmConfigLogger`
  - PV connection handling in `AlarmServer` (ServerModel)
- Benchmark throughput: messages/second with platform threads vs virtual threads
- Test with realistic load: 10k+ PVs, 100+ alarms/second
- Document migration strategy: code changes, JVM requirements, configuration
- Identify potential issues: pinned threads, synchronized blocks, native calls
- Measure memory footprint changes
- Create technical report with recommendations

**Resources:**
- `services/alarm-server/src/main/java/org/phoebus/applications/alarm/server/ServerModel.java`
- `services/alarm-logger/src/main/java/org/phoebus/alarm/logging/AlarmMessageLogger.java`
- `services/alarm-config-logger/src/main/java/org/phoebus/alarm/logging/AlarmConfigLogger.java`
- JEP 444: Virtual Threads - https://openjdk.org/jeps/444

**Assigned To:** _Available_

---

## Project Sign-up Sheet

| Project ID | Title | Assigned To | Status | Notes |
|------------|-------|-------------|--------|-------|
| ALARM-KAFKA-001 | Enhanced Kafka Streams Error Handling | | Not Started | |
| ALARM-KAFKA-002 | Resilient Topic Handling with Retry Logic | | Not Started | |
| ALARM-REST-001 | Alarm Configuration REST API | | Not Started | |
| ALARM-VT-001 | Virtual Threads Integration Assessment | | Not Started | |

---

## Getting Help

- Ask in the main room during work hours
- Use the Matrix chat: [#codeathon26:epics-controls.org](https://matrix.to/#/#codeathon26:epics-controls.org)
- Tag mentors: @Kunal Shroff, @Georg Weiss, @Sky Brewer
