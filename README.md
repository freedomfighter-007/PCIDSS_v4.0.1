📜 PCI DSS v4.0.1 Script and Payment Page Integrity Monitoring<br>
This tool continuously monitors browser-executed scripts on your payment pages and detects unauthorized changes, meeting the requirements of:<br>
<br>
✅ Requirement 6.4.3: Manage, inventory, and validate scripts on payment pages.<br>
✅ Requirement 11.6.1: Detect tampering with HTTP headers or page content delivered to consumers.<br>
<br>
✅ Combined Requirements Covered<br>
Feature	                    6.4.3	    11.6.1	  Description<br>
Script hash validation	      ✅	      ✅	    Ensures integrity and authorization<br>
Script inventory CSV	        ✅		            Tracks URLs, hashes, justification<br>
DOM structure hash		                  ✅	    Detects unexpected changes to HTML layout<br>
HTTP header hashing		                  ✅	    Detects tampering with CSP, HSTS, etc.<br>
Alert logging	                ✅	      ✅	    Logs tampering, additions, or changes<br>
Continuous monitoring loop	  ✅	      ✅	    Runs every 5 minutes<br>
<br>
📦 Features<br>
✅ Scans and inventories all <script> tags from a specified payment page<br>
✅ Detects and logs unauthorized, missing, or tampered scripts<br>
✅ Tracks and hashes critical HTTP response headers (e.g., CSP, HSTS)<br>
✅ Hashes the DOM structure to detect unauthorized content injection<br>
✅ Generates a weekly PDF report for audit compliance<br>
✅ Supports continuous monitoring via cron or systemd<br>
<br>
🛠️ Requirements<br>
Python 3.8+<br>
Python packages: pip install requests beautifulsoup4 fpdf<br>
<br>
📁 File Structure<br>
/opt/fim/<br>
├── script_monitor.py              # Main monitoring script<br>
├── script_inventory.csv           # Live inventory of scripts<br>
├── header_integrity.json          # Stored header & DOM structure hashes<br>
├── script_monitor_log.txt         # Log file of detections<br>
├── pci_6.4.3_11.6.1_report.pdf    # Weekly audit report<br>
<br>
⚙️ Configuration<br>
Edit the script to configure:<br>
TARGET_URL = "https://yourdomain.com/checkout"<br>
INVENTORY_FILE = "/opt/fim/script_inventory.csv"<br>
HEADER_HASH_FILE = "/opt/fim/header_integrity.json"<br>
LOG_FILE = "/opt/fim/script_monitor_log.txt"<br>
CHECK_INTERVAL_SECONDS = 300<br>
<br>
🚀 Usage<br>
Run Manually: python3 script_monitor.py<br>
Run Continuously via Cron: */5 * * * * /usr/bin/python3 /opt/fim/script_monitor.py<br>
<br>
🧾 Weekly Audit Report<br>
Generate a PDF summary: python3 generate_report.py<br>
This outputs pci_6.4.3_11.6.1_report.pdf with:<br>
✅ Script scan summary<br>
✅ Header & DOM integrity snapshot<br>
✅ Flagged issues<br>
<br>
🔐 Compliance Coverage<br>
Requirement	Description	Covered<br>
✅ PCI DSS 6.4.3	Inventory, authorization, and integrity of scripts<br>
✅ PCI DSS 11.6.1	Detect tampering with headers or DOM content<br>
<br>
📬 Optional Enhancements<br>
Email PDF report to compliance team<br>
Slack or SIEM integration<br>
HTML dashboard (included in dashboard.html)<br>
<br>
🛡️ Notes<br>
Always run in a secure, access-controlled environment.<br>
Protect output files (.csv, .json, .pdf) from unauthorized changes.<br>
Review justifications and update inventory monthly or when scripts change.<br>
