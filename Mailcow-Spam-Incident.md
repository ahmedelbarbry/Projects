## Case Study: Investigating and Mitigating a Spam Email Incident on a Mail Server (Mailcow)

### Background:
While working in a sales company, I was also actively training for a career transition into cybersecurity. As my knowledge deepened, my manager asked me to investigate a suspected spam incident on one of our mail servers. An opportunity that allowed me to apply SOC skills in a live environment.

The server in question hosted email services using Mailcow in a Dockerized environment. A suspicious account, xyovt@company.com, was identified sending spam emails. This address didn’t exist in our system, immediately suggesting spoofing or server compromise.

### Initial Response and Assessment:
I SSH’d into the server to assess active sessions and recent system commands. Both appeared clean, ruling out an active intrusion or obvious tampering.

I then attempted to access the mail logs, but found them missing, likely due to the Mailcow containers being offline. Upon restarting the stack, I encountered database startup failures, traced to a crashing MariaDB container.

### Docker Debugging and Log Recovery:
Digging into the container logs revealed a version mismatch: the MariaDB data expected an older version. I created a full server snapshot, rolled back to the previous compatible version, and brought the system back online. Once Mailcow was operational, I resumed log analysis, but found no indication of spam being sent from inside.

At this point, spoofing became the primary theory. To rule out a hidden backdoor, I conducted a manual file audit across all PHP-based web directories, reviewing both timestamps and code patterns. One file appeared suspicious but was ultimately benign. A reminder that caution is key, but so is avoiding false flags.

### Security Review and Hardening Recommendations:
With internal compromise ruled out, I audited the server’s broader security posture. Basic firewall and brute-force protections were in place, but it lacked centralized logging and monitoring. I verified that SPF, DKIM, and DMARC were configured correctly, supporting the spoofing theory.

I delivered a set of recommendations:

- Enable persistent log retention and container version consistency checks  
- Integrate basic SIEM-like alerting for Mailcow anomalies  
- Improve visibility with centralized syslog forwarding or monitoring stack

### Outcome & Reflection:
Although the incident was ultimately traced to external spoofing, this real-world event gave me a full cycle of SOC experience, from detection to investigation to system hardening. I applied my training under pressure, collaborated with colleagues outside my role, and contributed meaningfully to our security posture.

This experience proved that even without a formal SOC role, I can deliver practical value and approach incidents with a structured, analytical mindset. I’m confident this hands-on challenge reflects my readiness for entry-level SOC analyst roles. Not just in theory, but in practice.

> **Note**: This investigation occurred before I began documenting my work professionally, so screenshots and command logs were not captured. Future case studies will include more detailed evidence and visual references.
