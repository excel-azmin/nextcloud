# nextcloud


* Create Real Directories

```
sudo mkdir -p /home/azmin/nextcloud/config
sudo mkdir -p /home/azmin/nextcloud/data
```

* Adjust the Docker Compose File

```
version: '3.8'
services:
  nextcloud:
    image: lscr.io/linuxserver/nextcloud:latest
    container_name: nextcloud
    environment:
      PUID: "1000"  # UID of the user Nextcloud should run as
      PGID: "1000"  # GID of the user Nextcloud should run as
      TZ: "Etc/UTC"  # Set the timezone
    volumes:
      - /home/azmin/nextcloud/config:/config  # Configuration files and logs
      - /home/azmin/nextcloud/data:/data  # Data directory for Nextcloud files
    ports:
      - "2443:443"  # Expose port 443 on the host and map to port 443 in the container
    restart: unless-stopped  # Container restart policy
```
  
* Apply Correct Permissions

```
sudo chown -R 1000:1000 /home/azmin/nextcloud/config
sudo chown -R 1000:1000 /home/azmin/nextcloud/data
sudo chmod -R 755 /home/azmin/nextcloud/config
sudo chmod -R 755 /home/azmin/nextcloud/data

```
  
