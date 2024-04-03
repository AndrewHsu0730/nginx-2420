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
# Create a new directory
mkdir -p /web/html/nginx-2420

# Create a new file in the directory to store the website document
vim mkdir -p /web/html/nginx-2420/index.html
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
