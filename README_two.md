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

# 
sudo ufw allow ssh

# 
sudo ufw allow http

# 
sudo ufw allow https

# 
sudo ufw status verbose
```
