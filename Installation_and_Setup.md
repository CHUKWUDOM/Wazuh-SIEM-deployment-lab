
# WAZUH SIEM DEPLOYMENT – FULL INSTALLATION WALKTHROUGH
________________________________________
## BEFORE YOU START

### Confirm VM Specs <br>

### Inside Ubuntu Terminal, Run:

*free -h* <br>
*nproc* <br>
*lsb_release -a* <br>

#### You should see:
•	4GB RAM<br>
•	2 CPUs<br>
•	Ubuntu 24.04.4 or your specic VM name (it could be Kali, Fedora, etc. But for this setup, Ubuntu 24.04.4 is used)<br>
________________________________________
<img width="1920" height="309" alt="System specs 1" src="https://github.com/user-attachments/assets/b835d81d-f729-4005-9086-6aa55e796476" /> <br>

<img width="1920" height="1080" alt="Screenshot (34)" src="https://github.com/user-attachments/assets/fa492d62-1f0f-4048-9a02-31e2a0bdca05" />
<br>

________________________________________
## STEP 1 — Update System <br>

*sudo apt update && sudo apt upgrade -y* <br>

#### What this does: <br> 
•	Updates package index <br>
•	Upgrades installed packages <br>
•	Ensures compatibility before installing Wazuh <br>
________________________________________
<img width="1325" height="397" alt="Update and Upgrade VM" src="https://github.com/user-attachments/assets/32f8f112-96ac-4d66-9983-6fec0e85d529" /> <br>

<br>

________________________________________
## STEP 2 — Install curl <br>

*sudo apt install curl -y* <br>

### Why: <br>

•	Required to download Wazuh installation script securely.
________________________________________
<img width="1292" height="613" alt="Installing Curl" src="https://github.com/user-attachments/assets/bd15787d-9044-4e3c-9a4f-52fff7274871" />

<br>
________________________________________

## STEP 3 — Download Wazuh Installer <br>

### Run the command<br>

*curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh* <br>

________________________________________

## STEP 4 — Run Single-Node Installation <br>

Run the command <br>

*sudo bash wazuh-install.sh -a* <br>

### The -a flag installs: <br>

•	Wazuh Manager <br>
•	Wazuh Indexer<br>
•	Wazuh Dashboard<br><br>

#### ⚠️ This may take 10–20 minutes. <br>

CPU will spike.<br>
RAM usage will increase.<br><br>
#### This is normal. <br>

### Verify file downloaded: <br>

*ls* <br>

#### You should see: <br>

*wazuh-install.sh* 
<br>

________________________________________

<img width="1920" height="1080" alt="Installing Wazuh 1" src="https://github.com/user-attachments/assets/f08a3737-0245-4bd7-9d49-8c30c6764958" /><br><br>
<img width="1920" height="1080" alt="Installing Wazuh 2" src="https://github.com/user-attachments/assets/dc0ef4e0-c2f9-4521-97e4-677ca59a200e" /><br><br>
<img width="1920" height="274" alt="Installation Confirmation" src="https://github.com/user-attachments/assets/631cc4a4-0ee7-4b83-998d-36ef3af0658d" /><br><br>

________________________________________

## STEP 5 — Capture Generated Credentials<br>

At the end of installation, you will see:<br>

•	Username (usually admin)<br>
•	Generated password<br>

### ⚠️ Save it securely.<br>
________________________________________

<img width="1920" height="1080" alt="Login Credentials" src="https://github.com/user-attachments/assets/f9bd0bd5-7aeb-4e53-b7f9-016ee12b5cfe" /><br>

________________________________________

## STEP 6 — Verify Services<br
### Run:<br>

*sudo systemctl status wazuh-manager*<br>
*sudo systemctl status wazuh-indexer*<br>
*sudo systemctl status wazuh-dashboard*<br>

###  Each must show:<br>

#### *active (running)*

### If not:<br>

*sudo systemctl restart wazuh-manager*<br>
*sudo systemctl restart wazuh-indexer*<br>
*sudo systemctl restart wazuh-dashboard*<br>
________________________________________
<img width="1920" height="1080" alt="Dashboard Status" src="https://github.com/user-attachments/assets/b7875f46-1e97-4f15-ba9e-ad5c7ce481db" /><br>
<img width="1920" height="1080" alt="Indexer Status" src="https://github.com/user-attachments/assets/20cd48a2-221f-427c-bd2d-ca3e4aa67aab" /><br>
<img width="1920" height="1080" alt="Manager Status" src="https://github.com/user-attachments/assets/9dee57f9-3ee8-4771-b50a-3005a2bc6fa6" /><br>

________________________________________
## STEP 7 — Get Ubuntu VM IP <br>

### This will be needed to access the wazuh dashboard on the web browser

*ip a*<br>

### Look for:<br>

#### *inet 10.0.2.x (NAT address)*<br>
________________________________________

<img width="1920" height="1080" alt="IP addreess" src="https://github.com/user-attachments/assets/e7f6f9af-c843-48c4-92d1-ccacf5caace3" />
<br>

________________________________________

## STEP 8 — Access Dashboard from Host<br>

### Because you configured port forwarding:<br>
#### To setup, go to VM Settings -> Network -> Port Forwarding -> click the "+" sign

* Name: Wazuh
* Protocol: TCP
* Host Port: 8443<br>
* Guest Port: 443<br>

<img width="1920" height="1080" alt="Screenshot (41)" src="https://github.com/user-attachments/assets/ef585b2b-b097-4eae-a02a-6323961b22a6" />
<br>

#### Open browser on host:<br>

*https://localhost:8443*<br>

### You’ll see:<br>

•	Certificate warning → Click Advanced → Proceed<br>

#### Login with credentials generated earlier.<br>

________________________________________

<img width="1920" height="1080" alt="Login Page" src="https://github.com/user-attachments/assets/4600d17c-cb4d-42df-8cef-3193ab6e6a2a" /><br>

________________________________________

## STEP 9 — Confirm Dashboard Loads:<br>

### After login, you should see:<br>

•	Wazuh Dashboard Overview<br>
•	Security Events section<br>
•	System summary<br>
________________________________________

<img width="1920" height="1080" alt="Dashboard 1" src="https://github.com/user-attachments/assets/b1942bc1-ba16-4786-ac42-6e5c23978b48" /><br>
<img width="1920" height="1080" alt="Dashboard 2" src="https://github.com/user-attachments/assets/20be9de7-0eb0-47a6-878d-e9a03d7f920c" /><br>
<img width="1920" height="1080" alt="Dashboard 3" src="https://github.com/user-attachments/assets/0cd78e67-a562-4dd0-ba23-6b5b836d6021" /><br>

________________________________________

## STEP 10 — Monitor Resource Usage (Optional tool but helpful) <br>

### Inside Ubuntu:<br>

*sudo apt install htop -y*<br><br>

<img width="1920" height="1080" alt="HTOP install" src="https://github.com/user-attachments/assets/47a89c90-9463-4309-83ef-51b2e70bf587" />
<br>
<br>

### Run<br>

*htop*<br>

### Observe:
•	RAM usage (~2–3GB typical)<br>
•	CPU usage<br>
•	Wazuh Indexer processes<br>

________________________________________

<img width="1920" height="1080" alt="HTOP running" src="https://github.com/user-attachments/assets/3dc9c0cd-9876-45f4-80ff-d41547847ac2" />
<br>
________________________________________

## STEP 11 — Test Service Restart (Operational Validation)<br>

### Simulate restart:<br>

*sudo systemctl restart wazuh-manager*<br>

### Check status again:<br>

*sudo systemctl status wazuh-manager*<br>

### Ensures services recover properly.<br>

________________________________________
<br><br>


## Wazuh Login Credentials Location<br><br>

#### During installation, Wazuh automatically generates dashboard credentials.<br>
If you did not save them, they can be retrieved.<br><br>


### 📂 Credential Storage Location<br>

Wazuh stores the auto-generated passwords in:<br>

*sudo cat /usr/share/wazuh-indexer/opensearch-security/internal_users.yml*<br>

This file contains hashed credentials for internal users including:<br>

*admin*<br>
*kibanaserver*<br>
*logstash*<br>

#### ⚠️ Passwords in this file are hashed and cannot be read directly in plain text.<br><br>

### Recommended Way to Retrieve Admin Password<br>
#### Wazuh installation script generates a password file in:<br>

*sudo cat wazuh-passwords.txt*<br>

If still in the directory where installation was run.<br>

If not, check:<br>

*sudo find / -name "wazuh-passwords.txt" 2>/dev/null*<br>

#### This will locate the generated password file.<br><br>


### Resetting Admin Password (If Lost)<br>

#### If credentials are completely lost, reset the dashboard password:<br>

##### Run:<br>

*sudo /usr/share/wazuh-indexer/plugins/opensearch-security/tools/hash.sh*<br>

##### Then follow Wazuh password reset procedure via securityadmin tool.<br><br>

## Extra Clarification About Credentials

### Important distinction:

*internal_users.yml* → contains hashed credentials

*wazuh-passwords.txt* → contains generated plain credentials (if preserved)


