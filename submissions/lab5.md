\# Lab 5 - Submission



\## Task 1: DAST with OWASP ZAP



\### Baseline (unauthenticated) scan



\- Duration: approximately 1–3 minutes

\- Total alert instances: 41

\- Total alert types: 10



| Severity | Count |

|----------|------:|

| High | 0 |

| Medium | 9 |

| Low | 21 |

| Informational | 11 |

| \*\*Total\*\* | \*\*41\*\* |



\### Authenticated full scan



\- Duration: approximately 5–10 minutes

\- Total alert instances: 37

\- Total alert types: 12



| Severity | Count |

|----------|------:|

| High | 2 |

| Medium | 16 |

| Low | 9 |

| Informational | 10 |

| \*\*Total\*\* | \*\*37\*\* |



\### The "10–20x more" claim



\- Baseline instances: 41

\- Authenticated instances: 37

\- Ratio: 37 / 41 = 0.90x



My run did not match the lecture's expected 10–20x increase for authenticated DAST. The authenticated scan found several additional categories that were not present in the baseline scan, including SQL Injection and session-management findings, but the total number of alert instances was slightly lower. This likely happened because the authenticated scan configuration, crawling coverage, and report filtering differed from the baseline scan.



\### Two alerts found only by the authenticated scan



\#### 1. SQL Injection



\- Alert title: SQL Injection

\- Severity: High

\- Count: 2



This alert was unreachable to the unauthenticated baseline scan because the vulnerable functionality was discovered during the authenticated scan after ZAP logged in as the admin user. The baseline scan did not authenticate, so it had less access to protected application routes and user-specific behavior.



\#### 2. Session ID in URL Rewrite



\- Alert title: Session ID in URL Rewrite

\- Severity: Medium

\- Count: 5



This alert was unreachable to the unauthenticated baseline scan because a real authenticated session had to be created before ZAP could observe session identifiers being handled in URLs. The baseline scan did not establish an authenticated user session.



\### Auth-only findings observed



| Alert | Severity | Count |

|-------|----------|------:|

| SQL Injection | High | 2 |

| Missing Anti-clickjacking Header | Medium | 1 |

| Session ID in URL Rewrite | Medium | 5 |

| Private IP Disclosure | Low | 1 |

| X-Content-Type-Options Header Missing | Low | 3 |

| Authentication Request Identified | Informational | 1 |

| Session Management Response Identified | Informational | 1 |

| User Agent Fuzzer | Informational | 3 |

