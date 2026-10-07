# Migration Rules: Spring Boot 2.x to Spring Boot 3.x

## Migration Type
framework

## Source
- Spring Boot 2.1.6 (Red Hat BOM `me.snowdrop:spring-boot-bom:2.1.6.SP3-redhat-00001`)
- Java 11
- Spring Cloud Kubernetes 1.0.3.RELEASE

## Target
- Spring Boot 3.2.x (community upstream)
- Java 17
- Spring Cloud Kubernetes 3.1.x

## Transformation Rules

### RULE-001: Java Version Upgrade
- **Source**: Java 11 (`<source>11</source>`, `<target>11</target>`)
- **Target**: Java 17 (`<source>17</source>`, `<target>17</target>`)
- **Scope**: pom.xml `maven-compiler-plugin` configuration
- **Priority**: Critical

### RULE-002: javax.persistence → jakarta.persistence
- **Source**: `import javax.persistence.*`
- **Target**: `import jakarta.persistence.*`
- **Scope**: All Java files using JPA annotations (`@Entity`, `@Id`, `@Table`, etc.)
- **Priority**: Critical
- **Rationale**: Jakarta EE 9+ namespace migration required by Spring Boot 3

### RULE-003: Spring Boot BOM/Parent Update
- **Source**: `me.snowdrop:spring-boot-bom:2.1.6.SP3-redhat-00001`
- **Target**: `org.springframework.boot:spring-boot-starter-parent:3.2.5` (as parent POM)
- **Scope**: pom.xml dependency management
- **Priority**: Critical
- **Notes**: Remove Red Hat BOM, add Spring Boot parent; remove Red Hat repositories if not needed for other deps

### RULE-004: Spring Boot Maven Plugin Update
- **Source**: `spring-boot-maven-plugin` version `2.1.4.RELEASE-redhat-00001`
- **Target**: Remove explicit version (inherited from parent), update configuration
- **Scope**: pom.xml build plugins
- **Priority**: Critical

### RULE-005: Spring Cloud Kubernetes Update
- **Source**: `spring-cloud-starter-kubernetes-config` with `spring-cloud-kubernetes-dependencies:1.0.3.RELEASE`
- **Target**: `spring-cloud-starter-kubernetes-fabric8-config` with Spring Cloud `2023.0.x` BOM
- **Scope**: pom.xml dependencies
- **Priority**: High
- **Notes**: Spring Cloud Kubernetes was restructured; use Spring Cloud BOM for version management

### RULE-006: H2 Database Compatibility
- **Source**: H2 with `jdbc:h2:mem:catalog;DB_CLOSE_ON_EXIT=FALSE`
- **Target**: H2 with `jdbc:h2:mem:catalog;DB_CLOSE_ON_EXIT=FALSE` (verify compatibility with newer H2 bundled in Boot 3)
- **Scope**: application.properties
- **Priority**: Medium
- **Notes**: Boot 3 bundles H2 2.x which has some SQL compatibility changes

### RULE-007: Maven Compiler Plugin Update
- **Source**: `maven-compiler-plugin:3.6.1`
- **Target**: `maven-compiler-plugin:3.11.0` or later
- **Scope**: pom.xml build plugins
- **Priority**: Medium

### RULE-008: JKube Plugin Update
- **Source**: `kubernetes-maven-plugin:1.1.1`
- **Target**: `kubernetes-maven-plugin:1.16.2` or latest stable
- **Scope**: pom.xml build plugins
- **Priority**: Medium

### RULE-009: Actuator Endpoint Configuration
- **Source**: Default Spring Boot 2 actuator configuration
- **Target**: Ensure actuator endpoints are properly exposed for Boot 3
- **Scope**: application.properties
- **Priority**: Low

### RULE-010: Remove @Autowired Field Injection Warning
- **Source**: `@Autowired` on field (field injection)
- **Target**: Constructor injection (recommended pattern in Boot 3)
- **Scope**: CatalogController.java
- **Priority**: Low (recommended, not required)

## Quality Thresholds
- Build must compile with `mvn compile`
- Application must start with `mvn spring-boot:run`
- All existing endpoints must return same data
- H2 in-memory database must load import.sql correctly

## Anti-Patterns to Detect
- Use of `javax.*` namespace (must be `jakarta.*`)
- Red Hat-specific BOM versions (migrate to community upstream)
- Field injection with `@Autowired` (prefer constructor injection)
- Outdated plugin versions incompatible with Java 17

## Security Requirements
- No credentials in committed code
- H2 console disabled in production profile
- Actuator endpoints secured appropriately
