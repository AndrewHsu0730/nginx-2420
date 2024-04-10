# nginx-2420

## Step 1: Set up firewall using ufw

Before we start setting up firewall, we should log into our droplet.

```
ssh -i .ssh/do-key <user_name>@<your_droplet_ip_address>
```

Then, we can run the following commands to set up firewall.

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

# Update connection rules for our firewall
sudo ufw enable

# Check the status of ufw to see if ssh, http, and https connections are all allowed
sudo ufw status verbose
```

## Step 2: Place backend binary on the droplet

Before we start setting up backend, we should log out of our droplet and connect to our remote server using the sftp utility. 

```bash
sftp -i .ssh/do-key <user_name>@<your_droplet_ip_address>
```

Then, we can upload the backend binary file to our droplet.

```
put <path/to/backend/binary/file>
```

After the file transfer is done, we can type exit and press the enter key to disconnect from our remote server and log into our droplet again. We can see that the backend binary file is now in our home directory. Then, we can move the backend binary file to the directory of our choice.

```bash
sudo mv ~/hello-server <directory/of/your/choice>
```

After we locate the backend binary file to our desired location, it is important that we make the file executable.

```bash
sudo chmod u+x <directory/of/your/choice>/hello-server
```

## Step 3: Write a new service file to run the backend

Before we start writing a new service file, we have to create it first.

```bash
sudo vim /etc/systemd/system/backend.service
```

Then, copy the following and paste it to the new service file.

```
[Unit]
Description=Backend Service
After=network.target

[Service]
ExecStart=<path/to/hello/server>
Restart=always

[Install]
WantedBy=multi-user.target
```

After exiting the file, make sure to enable and start the backend service.

```bash
sudo systemctl enable --now backend.service
```

## Step 4: Edit nginx server block by adding reverse proxy to backend

Before we start editting nginx server block, we have to open it.

```bash
sudo vim /etc/nginx/sites-available/nginx-2420
```

Then, append the following reverse proxy to the server block.

```
location /hey {
    # Define the reverse proxy settings
    proxy_pass http://127.0.0.1:8080;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
location /echo {
    # Define the reverse proxy settings
    proxy_pass http://127.0.0.1:8080;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

## Step 5: Test connecting to backend

Before we perform the connection test, we have to restart the nginx service first.

```bash
sudo systemctl restart nginx.service
```

Then, we can test if the connections work by running the following commands.

```bash
curl http://<your_droplet_ip_address>

curl http://<your_droplet_ip_address>/hey

curl -X POST -H "Content-Type: application/json" \
  -d '{"message": "Hello from your server"}' \
  http://<your_droplet_ip_address>/echo
```
