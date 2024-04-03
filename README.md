# nginx-2420

## Step 1: Install necessary software

```bash
# Update package repositories
sudo pacman -Syu

# Install Vim and Nginx
sudo pacman -S vim nginx
```

## Step 2: Create a file that stores the website document

```bash
# Create a new directory named "/web/html/nginx-2420"
mkdir -p /web/html/nginx-2420

# Create a new file named "index.html" in the directory to store the website document
vim /web/html/nginx-2420/index.html
```

#### Paste the following website document into the file

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2420</title>
    <style>
        * {
            color: #db4b4b;
            background: #16161e;
        }
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        h1 {
            text-align: center;
            font-family: sans-serif;
        }
    </style>
</head>
<body>
    <h1>All your base are belong to us</h1>
</body>
</html>
```

## Step 3: Create a new server block

```bash
# Create a new directory named "/etc/nginx/sites_available"
mkdir -p /etc/nginx/sites_available

# Create a new server block file named "/etc/nginx/sites_available/nginx-2420.conf" in the directory
vim /etc/nginx/sites_available/nginx-2420.conf
```

#### Paste the following server block configuration into the file

```
server {
    listen 80;
    server_name 146.190.40.206;
    
    root /web/html/nginx-2420;
    index index.html;
    
    location / {
        try_files $uri $uri/ =404;
    }
}
```

## Step 4: Create a symbolic link to enable the server block

```bash
# Create a new directory named "/etc/nginx/sites_enabled"
mkdir -p /etc/nginx/sites_enabled

# Create the symbolic link
sudo ln -s /etc/nginx/sites_available/nginx-2420.conf /etc/nginx/sites_enabled
```

## Step 5: Reload Daemon and start the server

```bash
# Reload Daemon
sudo systemctl daemon-reload

# Start the server
sudo systemctl start nginx.service
```

#### After you type the url [http://146.190.40.206:80](http://146.190.40.206:80), you can see the webpage successfully loaded.
