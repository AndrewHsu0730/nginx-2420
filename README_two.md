# nginx-2420

## Step 1: Set up firewall using ufw

```bash
# Upgrade installed packages
sudo pacman -Syu

# Install the ufw package
sudo pacman -S ufw

# Reboot the system
sudo systemctl reboot

# Enable and start the ufw.service
sudo systemctl enable --now ufw.service

# Allow ssh connections
sudo ufw allow ssh

# Allow http connections
sudo ufw allow http

# Allow https connections
sudo ufw allow https

# Check the status of ufw to see if ssh, http, and https connections are all allowed
sudo ufw status verbose
```

## Step 2: Set up backend

