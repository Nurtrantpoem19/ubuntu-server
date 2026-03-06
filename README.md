# Secure Ubuntu Server Deployment


**Production-ready Ubuntu server automation with UFW firewall, Fail2Ban brute-force protection, and Nextcloud private cloud deployment.**

## 🎯 Features
- **UFW Firewall**: Deny-all incoming, SSH/HTTP/HTTPS only
- **Fail2Ban**: SSH + web login protection (custom whitelist)
- **Nextcloud**: Snap deployment with HTTPS ready
- **Automated**: Single playbook deploys everything in ~2 minutes
- **Secure**: No passwords in repo, interactive configuration

## Run these commands in your terminal to set up ansible
```bash
# 1. Install Ansible (laptop/local machine)
sudo apt install ansible

# 2. Clone this repo
git clone https://github.com/Nurtrantpoem19/ubuntu-server.git
cd secure-ubuntu-server

# 3. Edit inventory
# Edit inventory.ini: set server_ip & ansible_user
# replace with your local server_ip and your server's username, respectively

# 4. Dry run (safe)
ansible-playbook -i inventory.ini playbook.yml --check -K
#the -K flag is for when it prompts you for sudo password

# 5. Deploy!
ansible-playbook -i inventory.ini playbook.yml
```

## 📁 Repository Structure
```
.
├── playbook.yml           # Main automation playbook
├── inventory.ini # To be edited
├── README.md            
└── screenshots/          # UFW/Fail2Ban/Nextcloud visuals
```

## 🛡️ What It Does
1. **Hardens firewall** (UFW: deny incoming, allow SSH 22/HTTP 80/HTTPS 443)
2. **Deploys Fail2Ban** with your IP whitelisted (`ignoreip = 127.0.0.1/8 YOUR_IP`)
3. **Installs Nextcloud snap** (ready for `sudo nextcloud.enable-https lets-encrypt`)
4. **Restarts services** safely

## 📊 Results (My Production Server)
```
UFW Status: Status: active (blocked 3158 connections)
Fail2Ban: active, will ban any IP who attempts connection without passphrase
Nextcloud: 2.5GB data, HTTPS via Let's Encrypt
Uptime: 30 days
```

## 💼 Why This Matters (CAR Method)
**Context**: Needed private cloud replacing Google Drive, but public exposure risky.  
**Action**: Built automated deployment with layered security (firewall + intrusion detection).  
**Result**: Production server running 47 days, blocked 100+ attacks, 2.5GB data synced securely.

## 📸 Screenshots
![UFW Status] (screenshots/ufw.png)




## 🔧 Customization
Edit `playbook.yml` `vars_prompt` section:
```yaml
vars_prompt:
  - name: whitelist_ip
    prompt: "Whitelist IP"
    default: "YOUR_HOME_IP"
  - name: ssh_port
    prompt: "SSH Port"
    default: "22"
```
