## High Level Overview
*User Input (Domain) → Input Validation → DNS Enumeration → Port Visibility Check
→ HTTP Header Inspection → Metadata Checks → Risk Interpretation → Markdown Report*

## Flow Description
1. **User Input (Domain):**
The user provides a target domain. Input is captured in a simple, secure interface.

2. **Input Validation:**
Validates that the domain is well-formed and reachable. Prevents invalid or malformed inputs from propagating further.

3. **DNS Enumeration:**
Uses DNS queries to discover subdomains, record types, and other DNS-related information. Critical for identifying the scope of exposure.

4. **Port Visibility Check:**
Scans common service ports to identify which are open and potentially exposed to external access.

5. **HTTP Header Inspection:**
Requests web-facing endpoints to inspect HTTP headers. Helps detect security misconfigurations, server versions, and potential information leakage.

6. **Metadata Checks:**
Collects additional metadata such as SSL/TLS configuration, certificate information, and other auxiliary data to refine the security context.

7. **Risk Interpretation:**
Aggregates all findings and interprets them against defined risk criteria, providing context for potential vulnerabilities.

8. **Markdown Report:**
Outputs a structured report in Markdown format, summarizing findings, severity, and actionable insights for stakeholders.

## Module Design Principles
Each step in the workflow is implemented as a single, isolated module with the following properties:
- One Responsibility: Each module performs exactly one task in the workflow.
- No Side Effects: Modules do not modify external state or depend on hidden behaviors.
- No Shared Global State: Data is passed explicitly between modules, ensuring testability, reliability, and maintainability.

## 4.3 Module Responsibilities
| Module                  | Responsibility                                               |
|-------------------------|-------------------------------------------------------------|
| input_validation        | Validate user-supplied domain input.                        |
| dns_enumeration         | Query DNS records and enumerate subdomains.                |
| port_check              | Scan specified ports and identify open services.           |
| http_header_inspection  | Request endpoints and parse HTTP headers for security info.|
| metadata_checks         | Collect auxiliary metadata such as SSL/TLS details and certificates. |
| risk_interpreter        | Analyze findings and assign risk levels.                   |
| report_generator        | Generate a human-readable Markdown report summarizing the assessment. |

## Data Flow
- Each module receives explicit input from the previous module and returns structured output.
- Output from one module becomes the input for the next, maintaining clear separation of concerns.
- No module directly accesses or modifies the internal state of other modules, promoting modularity and testability.

## Excluded Checks
Certain checks are intentionally excluded to keep the tool lightweight and focused:
- **Active exploitation:** The tool does not perform intrusive attacks or exploitation attempts.
- **Full vulnerability scanning:** Deep scanning is delegated to specialized tools.
- **OS or network fingerprinting:** Avoided to prevent potential legal or ethical issues during assessment.

This design ensures a fast, safe, and repeatable reconnaissance process that highlights actionable security risks without introducing unnecessary complexity or exposure.

## Summary
This architecture emphasizes:
- **Modularity:** Each module is independent, testable, and easy to maintain.
- **Safety:** Non-intrusive, low-risk operations.
- **Clarity:** Data flows explicitly from input to final report.

Adhering to these principles makes this tool professional-grade and career-relevant, suitable for both internal assessments and demonstration in security projects.
