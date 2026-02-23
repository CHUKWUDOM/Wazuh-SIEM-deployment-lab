
WAZUH SIEM DEPLOYMENT – FULL INSTALLATION WALKTHROUGH
________________________________________
✅ BEFORE YOU START
Confirm VM Specs
Inside Ubuntu:
free -h
nproc
lsb_release -a
You should see:
•	~4GB RAM
•	2 CPUs
•	Ubuntu 22.04
________________________________________
📸 Screenshot →
screenshots/01-system-specs.png
________________________________________
✅ STEP 1 — Update System
sudo apt update && sudo apt upgrade -y
What this does:
•	Updates package index
•	Upgrades installed packages
•	Ensures compatibility before installing Wazuh
________________________________________
📸 Screenshot →
screenshots/02-system-update.png
Capture:
•	Terminal output showing packages updating
________________________________________
✅ STEP 2 — Install curl
sudo apt install curl -y
Why:
•	Required to download Wazuh installation script securely.
________________________________________
📸 Screenshot →
screenshots/03-install-curl.png
________________________________________
✅ STEP 3 — Download Wazuh Installer
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh

________________________________________
✅ STEP 4 — Run Single-Node Installation
sudo bash wazuh-install.sh -a
The -a flag installs:
•	Wazuh Manager
•	Wazuh Indexer
•	Wazuh Dashboard
⚠️ This may take 10–20 minutes.
CPU will spike.
RAM usage will increase.
This is normal.
Verify file downloaded:
ls
You should see:
wazuh-install.sh
________________________________________
📸 Screenshot →
screenshots/05-installation-progress.png
Capture:
•	Installation running
•	Services being configured
________________________________________
✅ STEP 5 — Capture Generated Credentials
At the end of installation, you will see:
•	Username (usually admin)
•	Generated password
⚠️ Save it securely.
________________________________________
📸 Screenshot →
screenshots/06-generated-credentials.png
(Blur password if uploading publicly)
________________________________________
✅ STEP 6 — Verify Services
Run:
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard
Each must show:
active (running)
If not:
sudo systemctl restart wazuh-manager
sudo systemctl restart wazuh-indexer
sudo systemctl restart wazuh-dashboard
________________________________________
📸 Screenshot →
screenshots/07-service-status.png
Capture:
•	All three services showing active
________________________________________
✅ STEP 7 — Get Ubuntu VM IP
ip a
Look for:
inet 10.0.2.x (NAT address)
________________________________________
📸 Screenshot →
screenshots/08-ip-address.png
________________________________________
✅ STEP 8 — Access Dashboard from Host
Because you configured port forwarding:
Host Port: 8443
Guest Port: 443
Open browser on host:
https://localhost:8443
You’ll see:
•	Certificate warning → Click Advanced → Proceed
Login with credentials generated earlier.
________________________________________
📸 Screenshot →
screenshots/09-dashboard-login.png
________________________________________
✅ STEP 9 — Confirm Dashboard Loads
After login, you should see:
•	Wazuh Dashboard Overview
•	Security Events section
•	System summary
________________________________________
📸 Screenshot →
screenshots/10-dashboard-overview.png
________________________________________
✅ STEP 10 — Monitor Resource Usage
Inside Ubuntu:
sudo apt install htop -y
htop
Observe:
•	RAM usage (~2–3GB typical)
•	CPU usage
•	Wazuh Indexer processes
________________________________________
📸 Screenshot →
screenshots/11-resource-usage.png
________________________________________
✅ STEP 11 — Test Service Restart (Operational Validation)
Simulate restart:
sudo systemctl restart wazuh-manager
Check status again:
sudo systemctl status wazuh-manager
Ensures services recover properly.
________________________________________
📸 Screenshot →
screenshots/12-service-restart-test.png

gh repo clone CHUKWUDOM/Wazuh-SIEM-deployment-lab
