# Brightwave Security SQL Investigations

# Insider Risk, Data Access & Phishing Response Investigation

## Project Overview
A SQL security analytics project investigating one month of security records for Brightwave Logistics, a fictional logistics company. The analysis examines employee access to sensitive systems, potential privilege mismatches, phishing and malware email responses, and incident handling.

| Project Detail | Description |
|---|---|
| Project type | SQL security analytics investigation |
| Database | MySQL 8.0+ |
| Data period | August 2026 |
| Tables | `employees`, `systems`, `access_logs`, `email_security_events`, `incidents` |
| Focus areas | Data access, privilege review, phishing response, incident management |

## Project Objectives
- Assess data quality and document cleaning decisions.
- Review access to sensitive systems, including activity outside business hours and data downloads or exports.
- Compare employee clearance levels and employment status with recorded access.
- Measure employee responses to phishing and malware emails.
- Evaluate incident status and response times against defined SLA targets.
- Develop reusable SQL reporting to support management review.

## Database Tables

| Table | Description |
|---|---|
| `employees` | Employee roles, departments, clearance levels, and employment status |
| `systems` | System names, data classifications, and owning departments |
| `access_logs` | System access attempts, actions, timestamps, results, and records accessed |
| `email_security_events` | Email categories and recorded employee responses |
| `incidents` | Incident types, severity, status, and reporting/closure timestamps |

## Key Business Questions
- How many access attempts were granted or denied, and which systems and actions were most common?
- Which employees or systems had the highest download and export volumes?
- Were there above-clearance or post-termination access events?
- How did employees respond to phishing and malware emails?
- Which incidents remained open or in progress, and which required SLA review?
- Which activity or processes should be prioritised for further investigation?

## SQL Techniques & Concepts
The project applies:
- Data profiling and quality checks
- `JOIN` operations across related tables
- Filtering, grouping, and aggregate functions
- Conditional logic and calculated indicators
- Subqueries and Common Table Expressions (CTEs)
- Date and time analysis
- Window functions, ranking, and running totals
- Reusable views for management reporting

## Aggregate Results

### 1. Data Overview

| Table | Records |
|---|---:|
| Employees | 20 |
| Systems | 10 |
| Access logs | 254 |
| Email security events | 119 |
| Incidents | 20 |

The access logs cover **3–29 August 2026**.

### 2. Access Activity

| Access Result | Events | Share |
|---|---:|---:|
| Granted | 236 | 92.9% |
| Denied | 18 | 7.1% |
| **Total** | **254** | **100%** |

*Capitalisation differences in `access_result` were standardised for this summary.*

| Action Type | Events | Records Accessed |
|---|---:|---:|
| View | 153 | 2,845 |
| Edit | 59 | 1,150 |
| Download | 29 | 8,621 |
| Export | 13 | 18,711 |
| **Total** | **254** | **31,327** |

Download and export events account for **27,332 records accessed** in the supplied logs.

| Access Timing | Events | Share |
|---|---:|---:|
| Within defined business hours | 227 | 89.4% |
| Outside defined business hours | 27 | 10.6% |
| **Total** | **254** | **100%** |

Business hours are defined in the project brief as Monday–Friday, 08:00–17:59.

### 3. Privilege Review

| Indicator | Events |
|---|---:|
| Attempts to access systems above recorded clearance | 23 |
| Above-clearance attempts denied | 15 |
| Above-clearance attempts granted | 8 |
| Access events after recorded termination date | 6 |

The six post-termination events relate to one employee and were all recorded as granted. These events and the granted above-clearance attempts warrant validation of account status and permission settings; they do not, by themselves, establish misconduct.

### 4. Phishing & Email Security

| Email Category | Events |
|---|---:|
| Phishing | 57 |
| Malware | 6 |
| Legitimate | 45 |
| Spam | 11 |
| **Total** | **119** |

| Response to Phishing/Malware Emails | Events |
|---|---:|
| Clicked link | 22 |
| Opened attachment | 3 |
| Reported | 18 |
| Deleted | 11 |
| Ignored | 9 |
| **Total** | **63** |

Of the 63 phishing or malware events, **25 (39.7%)** involved a clicked link or opened attachment, while **18 (28.6%)** were reported.

### 5. Incident Status

| Incident Status | Incidents |
|---|---:|
| Closed | 13 |
| In Progress | 4 |
| Open | 3 |
| **Total** | **20** |

| Severity | Incidents |
|---|---:|
| Critical | 3 |
| High | 6 |
| Medium | 6 |
| Low | 5 |
| **Total** | **20** |

Three Critical incidents were not marked Closed: one was In Progress and two were Open. These should be reviewed against the project’s severity-based SLA targets.

## Major Findings & Insights
- Most recorded access attempts were granted (**92.9%**); 18 were denied.
- Download and export activity represented **27,332 records accessed**, with exports accounting for the larger share.
- The logs contain **8 granted above-clearance attempts** and **6 granted access events after a recorded termination date**. These are priority items for access-control review.
- **25 of 63 phishing or malware events** involved a click or opened attachment, while 18 were reported.
- **Seven incidents** remained Open or In Progress, including three Critical incidents not marked Closed.

These observations identify areas for follow-up. They do not prove data leakage, malicious intent, or confirmed compromise.

## Recommended Review Priorities
1. Validate permissions for granted above-clearance access and confirm whether each event had an approved business reason.
2. Review the terminated employee’s account lifecycle and the six post-termination access events.
3. Examine download and export activity against employee responsibilities and expected business use.
4. Review phishing reporting and interaction patterns to identify where additional awareness or response controls may be needed.
5. Confirm the status and SLA position of unresolved Critical and High incidents.

Recommendations should be finalised against validated query results and documented assumptions.

## Data Limitations
- Some fields are missing, including email action timestamps, records-accessed values, employee clearance levels, incident system IDs, and incident closure timestamps.
- Text labels contain inconsistent capitalisation or spacing; standardisation may affect grouping and filtering.
- The project defines incident SLA targets, but missing closure timestamps and open statuses require careful handling when calculating elapsed time.
- Unusual access is an indicator for review, not proof of misconduct. Business context may not be captured in the available data.

## Tools & Technologies
- MySQL 8.0+
- SQL
- Data quality analysis
- Security analytics

## Repository Contents
- SQL scripts for data quality, access activity, privilege review, phishing analysis, incident response, and advanced SQL analysis
- Source CSV files for the five project tables
- Project documentation and findings, where included


