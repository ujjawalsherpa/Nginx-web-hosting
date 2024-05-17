Here is a corrected and professional version of your README file for the GitHub repository, including necessary changes and formatting:

---

# Hosting a Static Website with Nginx

This guide provides basic configuration steps for using Nginx to host your static website. The website used in this example is a dummy project from [Free CSS](https://www.free-css.com/), built using HTML and CSS.

## Step 1: Install Nginx on Linux

The following instructions are for RHEL. Adjust the commands according to your Linux distribution.

1. Update all packages:
   ```sh
   sudo yum update
   ```

2. Install Nginx:
   ```sh
   sudo yum install nginx
   ```

3. Start and enable Nginx:
   ```sh
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

## Step 2: Configure Nginx to Host Your Website

1. Navigate to the Nginx configuration directory:
   ```sh
   cd /etc/nginx
   ```

2. Locate the `nginx.conf` file (this is the main configuration file).

### Important: Backup the Existing Configuration File

Before making changes, create a backup of the existing `nginx.conf` file:
```sh
sudo cp nginx.conf nginx.conf.backup
```

### Create and Modify the New `nginx.conf` File

Open the `nginx.conf` file in your preferred text editor and replace its content with the following configuration:

```nginx
events {
}

http {
    include /etc/nginx/mime.types;

    server {
        listen 80;
        server_name _;

        root /location/to/your/website/files;
        index index.html index.htm;  # Ensure the index file is specified

        location / {
            try_files $uri $uri/ =404;
        }
    }
}
```

### Explanation of Configuration Lines

- **events { }**: Defines settings related to event-driven mechanisms in Nginx. It can remain empty for basic configurations.
  
- **http { }**: Contains configurations for handling HTTP traffic.
  
  - **include /etc/nginx/mime.types;**: Includes the MIME types file, which helps Nginx determine the correct `Content-Type` for files based on their extensions.
  
  - **server { }**: Defines a virtual server.
    
    - **listen 80;**: Tells Nginx to listen for incoming connections on port 80 (default for HTTP).
    
    - **server_name _;**: Uses an underscore as a wildcard to match any hostname.
    
    - **root /location/to/your/website/files;**: Sets the root directory for the server. Nginx will look for the requested files in this directory.
    
    - **index index.html index.htm;**: Specifies the index files to serve when a directory is requested.

    - **location / { try_files $uri $uri/ =404; }**: Tries to serve the requested URI as a file. If it doesn't exist, returns a 404 error.

### Ensure the Root Directive Points to Your Website Content

Make sure the `root` directive specifies the absolute path to your website's content.

Example:
```nginx
root /var/www/my-website;
```

After making these changes, reload Nginx to apply the new configuration:
```sh
sudo nginx -s reload
```

---

# HAVE A GOOD DAY.
