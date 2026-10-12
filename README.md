# Web Investigation — Network Forensics with Wireshark

> **Status:** In progress  
> **Focus:** Network traffic analysis, HTTP investigation, and web-attack evidence review.

## Overview

This repository documents a hands-on network-forensics investigation using Wireshark and a PCAP provided for the CyberDefenders **Web Investigation** training challenge.

The goal is to examine captured HTTP traffic, identify suspicious web requests, and document conclusions that can be supported by packet-level evidence. This is a learning lab, not a claim of professional incident-response experience.

## Objectives

- Filter and inspect HTTP requests in a PCAP.
- Examine suspicious query parameters and identify possible SQL injection attempts.
- Review HTTP POST requests and multipart form data for evidence relevant to a web investigation.
- Correlate observations with packet numbers and request details.
- Produce a clear investigation report with defensive recommendations.

## Tools

- **Wireshark** — packet inspection and display filters
- **PCAP** — packet-capture evidence supplied for the training challenge
- **Markdown** — investigation notes and reporting

## Investigation workflow

1. Open the PCAP in Wireshark and confirm that HTTP traffic is present.
2. Use display filters to narrow the traffic to relevant requests (for example, `http.request`).
3. Inspect suspicious requests and their URI/query parameters.
4. Review relevant POST requests and multipart form fields.
5. Record each finding with its packet number, supporting evidence, interpretation, and confidence.
6. Derive recommendations from the evidence rather than assumptions.

## Preliminary observations

The investigation is **not yet complete**. During initial triage:

- HTTP requests were identified in the capture.
- A challenge hint directs attention to packet **357** for an initial SQL-injection attempt involving a `search` parameter.
- Additional investigation is required to validate the relevant requests, identify any uploaded file name, and determine whether the available evidence supports further conclusions.

These are preliminary notes, not final incident findings. Exact values and conclusions will be added only after they have been verified against the capture.

## Evidence log

| Item | Evidence to record | Status |
|---|---|---|
| Suspicious HTTP request | Packet number, request URI, and decoded parameter value | In progress |
| SQL injection investigation | Exact request and supporting packet evidence | In progress |
| HTTP POST / upload investigation | Request details and any filename supported by the capture | Pending |
| Potentially exposed form data | Document the type of exposure without publishing credentials or personal data | Handle carefully |
| Final assessment | Evidence-backed conclusion and confidence level | Pending |

## Defensive recommendations

Recommendations will be finalized after the evidence review. Depending on what the capture confirms, relevant controls may include:

- Use parameterized queries or prepared statements rather than building SQL from user input.
- Validate input on the server side and handle unexpected input safely.
- Restrict upload types and verify file content server-side; store uploads outside executable web directories.
- Protect administrative interfaces with strong authentication and least-privilege access.
- Avoid transmitting credentials over unencrypted HTTP; use HTTPS and rotate any credentials confirmed to have been exposed.
- Monitor web-server logs for repeated suspicious parameters, unexpected upload attempts, and anomalous administrative requests.

These are general defensive measures; they should not be interpreted as proof that every listed weakness was present in this case.

## Scope and responsible handling

- This repository is for authorized training and educational analysis.
- No live target was tested as part of this write-up.
- Do not publish raw credentials, session tokens, personal information, or other sensitive values found in packet captures.
- The original PCAP is not included in this repository at this stage. Before redistributing challenge data, check the source platform's rules and licensing.
- Screenshots should be reviewed and redacted before publication.

## Next steps

- Complete the packet-by-packet investigation.
- Add sanitized screenshots and exact packet references.
- Replace preliminary notes with verified findings.
- Record limitations and distinguish observed facts from interpretations.

---

*This write-up is a work in progress. Findings will be reported only when supported by the captured evidence.*
