# nginx-2420
Set A assignment 3-1

## Step 1: Install necessary software

```bash
# Update package repositories
sudo pacman -Syu

# Install Vim and Nginx
sudo pacman -S vim nginx
```

## Step 2: Configure Nginx

```bash
# Create a new repository
mkdir -p /web/html/nginx-2420

# Create a new file in the directory to store the website document
vim mkdir -p /web/html/nginx-2420/website_document

# Create a new server block configuration file
vim /etc/nginx/nginx-2420.conf
```
