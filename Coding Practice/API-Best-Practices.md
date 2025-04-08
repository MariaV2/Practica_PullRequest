# API Best Practices Guidelines [Coding Practice] 
<font size="-1">_Author: Frank Arana - Dec. 2018_</font>

## Overview

This document covers general security guidelines for API endpoints within Unity. These guidelines will cover general points like:
- [Access control best practices](#access-controls)
- [Input validation](#input-validation)
- [Request verification](#request-integrity)
- [Replay attacks](#replay-attacks)
- [General security practices relevant to, but not specific to APIs](#general)

### Recommendations
#### Access Controls
###### Description

API endpoints should follow the principle of least privilege. Services with protected information should serve to the smallest group possible.
###### Why We Care

APIs with misconfigured access controls can lead to unintentional information leaks, or unauthorized and malicious state-changing actions on sensitive data.
###### Example of Issue (Optional)

A POST that allows the user to modify information on an account without checking if the user owns the account being modified.

A GET request that returns sensitive informative information without authentication.

###### How to Fix?

Determine which API actions should be considered sensitive or public.

For Internal (to Unity) APIs: Limit network access as much as possible. Ideally, these endpoints should be restricted to a closed network, and require authentication stronger than a singular API key. For example, multi-factor authentication.

For Public APIs with sensitive information: Require authentication before performing any action being requested. API keys should be both revocable and renewable.

For Public APIs providing public information: Ensure no state changing actions are being performed through a public API without authentication. Consider rate limiting to prevent a single host making too many requests in a small amount of time.
###### Risk Rating

Incorrect access controls can range from High to Low Severity.
###### References (Optional)

- https://www.owasp.org/index.php/REST_Security_Cheat_Sheet

---

#### Input Validation
###### Description

Incoming data can be malformed or crafted to cause unintended behavior when it is parsed.
###### Why We Care

Depending on how input is parsed, it is possible for unvalidated input to contain command injections, or other harmful actions.
###### Example of Issue (Optional)
*TBD*

###### How to Fix?

Type checking - Ensure input is of the expected data type, rejec