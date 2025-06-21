# -File-Integrity-Monitoring-with-Linux-Audit-Daemon-HIDS-Implementation-
Utilize a Host-based Intrusion Detection System (HIDS) using the Linux Audit daemon to monitor and protect a sensitive directory from unauthorized changes.
## Project: File Integrity Monitoring with Linux Audit Daemon (HIDS Implementation)

### Objective
The purpose of this project is to simulate the deployment of a Host-based Intrusion Detection System (HIDS) in a Linux environment using the Audit daemon. By configuring audit rules, simulating file tampering through attack scripts, and analyzing audit logs, this project demonstrates how to detect unauthorized changes to critical files and respond with appropriate remediation. It reinforces best practices in file integrity monitoring, system hardening, and proactive incident detection.

### Skills 
- Linux system administration
- Host-based intrusion detection systems (HIDS)
- Writing and managing custom `audit.rules`
- Log filtering and analysis using `ausearch`
- Threat simulation and forensic documentation
- File integrity monitoring and reporting
- System hardening and proactive auditing

---

### Action Plan and Steps

### Step 1: Download and Prepare Starter Files
- Cloned and extracted the starter project repository into the working directory.
- Navigated into the project directory to begin configuration:
  cd project2-main

### Step 2: Set File Permissions for Attack Scripts

To prepare the attack simulation scripts for execution, I updated their permissions:

bash
chmod u+x attack-a attack-b attack-c

### Step 3: Create Audit Rules for File Monitoring

To monitor sensitive files for unauthorized changes, I configured custom audit rules using the Linux Audit daemon.

- Targeted 10 files located in `/protected_files` for write-watch monitoring.
- For each file, I added a rule to track write (`-p w`) operations.
- Each rule was tagged with a unique filter key (`-k file_watch`) to simplify log analysis later.

**Example audit rule:**
bash
-w /protected_files/cloudia.txt -p w -k file_watch

### Step 4: Run Simulated Attacks

With the audit rules in place and the attack scripts made executable, I executed each script to simulate unauthorized file modifications.

Each attack script (`attack-a`, `attack-b`, and `attack-c`) targeted a different file within the `/protected_files` directory:

- `attack-a` modified `cloudia.txt`
- `attack-b` modified `oakley.txt`
- `attack-c` modified `precipitation.csv`

These scripts could be executed one by one or simultaneously. For this project, I chose to run them sequentially to maintain clear correlation between each attack and the file it altered.

bash
./attack-a
./attack-b
./attack-c


### Step 5: Analyze Audit Logs

Once the simulated attacks were executed, I used the `ausearch` tool to analyze the audit logs and identify which files had been modified.

- I filtered the logs using the custom key assigned during rule creation:
  bash
  ausearch -k file_watch

### Step 6: Document and Report Findings

After analyzing the audit logs, I created a structured summary detailing the impact of the simulated attacks and the recommended remediation steps.

#### Impact Summary
- Three protected files in the `/protected_files` directory were modified without authorization.
- The files affected were:
  - `cloudia.txt`
  - `oakley.txt`
  - `precipitation.csv`
- Each file was changed by a separate simulated attack script (`attack-a`, `attack-b`, `attack-c`).
- These modifications confirmed that unauthorized file changes were effectively detected by the audit daemon.

#### Recommended Fixes
- **Restore** altered files from a known-good backup to preserve system integrity.
- **Harden Permissions** on sensitive directories to restrict unauthorized write access.
- **Schedule Regular Audits** using automated tools (e.g., `auditd` with filtering and alerting).
- **Train Administrators** on maintaining active monitoring rules and responding to integrity violations.

> **Purpose:** This documentation step ensures that each detected incident is recorded and that actionable security controls are put in place to mitigate similar risks in a production environment.

## Project Conclusion

This project successfully demonstrated how host-based intrusion detection can be implemented using the Linux Audit daemon. From configuring custom audit rules and simulating attacks to identifying modified files through ausearch and documenting the outcomes, each phase of the project reinforced core cybersecurity practices. The result is a functioning monitoring and alerting system that captures unauthorized file changes, improves visibility, and strengthens endpoint security. This experience enhanced my understanding of HIDS concepts, log analysis, and the importance of proactive monitoring in securing Linux systems.

## References

All configurations, commands, and security practices followed in these projects are based on real-world frameworks, documentation, and tool usage from the following sources:

- [Auditd Linux Manual](https://man7.org/linux/man-pages/man8/auditd.8.html)
- [Nessus Documentation](https://docs.tenable.com/nessus/)
- [ausearch Command Reference](https://linux.die.net/man/8/ausearch)
- [Microsoft Defender & Sentinel Documentation](https://learn.microsoft.com)
- [OWASP Security Best Practices](https://owasp.org)
