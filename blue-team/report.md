# Blue Team Report – DC-3

## Overview

After completing the exploitation phase, system logs were analyzed to identify traces of the attack and understand how the intrusion could be detected from a defensive perspective.

---

## SQL Injection Detection

The Apache access logs showed multiple suspicious requests targeting the Joomla component:

- Repeated requests to:
  /index.php?option=com_fields&view=fields&layout=modal&list[fullordering]

- Presence of unusual payloads in the `list[fullordering]` parameter
- HTTP 500 responses, indicating backend errors triggered by injection attempts
- User-Agent clearly identified as sqlmap

These indicators strongly suggest automated SQL Injection activity.

---

## Web Shell Activity

After gaining admin access, a template file was modified to execute system commands.

This activity can be identified in logs by:

- Requests containing the `cmd` parameter:
  /templates/protostar/index.php?cmd=...

- Execution of system commands through HTTP GET requests

This behavior is abnormal for a web application and indicates Remote Command Execution.

---

## Reverse Shell Detection

The logs also revealed suspicious outbound activity:

- Requests triggering reverse shell payloads via the `cmd` parameter
- Encoded shell commands executed through the web application

Example indicators:

- Usage of `nc` (netcat)
- Pipes and redirections (`|`, `>`)
- Creation of temporary files in `/tmp`

These are common patterns associated with reverse shells.

---

## Key Indicators of Compromise (IOCs)

- SQL Injection patterns in URL parameters
- Repeated HTTP 500 responses
- sqlmap user-agent in logs
- Requests containing `cmd=`
- Commands executed via web requests
- Reverse shell payloads

---

## Conclusion

The attack could have been detected early by monitoring:

- Unusual query parameters
- Automated tool signatures (sqlmap)
- Web server errors (500 responses)
- Suspicious command execution via HTTP requests

Proper logging, monitoring, and input validation would significantly reduce the risk of such attacks.
