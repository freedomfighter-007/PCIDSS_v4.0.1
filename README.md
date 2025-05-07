📜 PCI DSS v4.0.1 Script and Payment Page Integrity Monitoring
This tool continuously monitors browser-executed scripts on your payment pages and detects unauthorized changes, meeting the requirements of:

✅ Requirement 6.4.3: Manage, inventory, and validate scripts on payment pages.
✅ Requirement 11.6.1: Detect tampering with HTTP headers or page content delivered to consumers.

📦 Features
✅ Scans and inventories all <script> tags from a specified payment page
✅ Detects and logs unauthorized, missing, or tampered scripts
✅ Tracks and hashes critical HTTP response headers (e.g., CSP, HSTS)
✅ Hashes the DOM structure to detect unauthorized content injection
✅ Generates a weekly PDF report for audit compliance
✅ Supports continuous monitoring via cron or systemd

🛠️ Requirements
Python 3.8+
Python packages: pip install requests beautifulsoup4 fpdf

📁 File Structure
/opt/fim/
├── script_monitor.py              # Main monitoring script
├── script_inventory.csv           # Live inventory of scripts
├── header_integrity.json          # Stored header & DOM structure hashes
├── script_monitor_log.txt         # Log file of detections
├── pci_6.4.3_11.6.1_report.pdf    # Weekly audit report

⚙️ Configuration
Edit the script to configure:
TARGET_URL = "https://yourdomain.com/checkout"
INVENTORY_FILE = "/opt/fim/script_inventory.csv"
HEADER_HASH_FILE = "/opt/fim/header_integrity.json"
LOG_FILE = "/opt/fim/script_monitor_log.txt"
CHECK_INTERVAL_SECONDS = 300

🚀 Usage
Run Manually: python3 script_monitor.py

Run Continuously via Cron: */5 * * * * /usr/bin/python3 /opt/fim/script_monitor.py

🧾 Weekly Audit Report
Generate a PDF summary: python3 generate_report.py
This outputs pci_6.4.3_11.6.1_report.pdf with:
- Script scan summary
- Header & DOM integrity snapshot
- Flagged issues

🔐 Compliance Coverage
Requirement	Description	Covered
PCI DSS 6.4.3	Inventory, authorization, and integrity of scripts	✅
PCI DSS 11.6.1	Detect tampering with headers or DOM content	    ✅

📬 Optional Enhancements
Email PDF report to compliance team
Slack or SIEM integration
HTML dashboard (included in dashboard.html)

🛡️ Notes
Always run in a secure, access-controlled environment.
Protect output files (.csv, .json, .pdf) from unauthorized changes.
Review justifications and update inventory monthly or when scripts change.
