# nextcloud-s3
Run Nextcloud with S3 as your primary storage — effortlessly, reliably, and fully Dockerized.

## ⏳ Built to Save You Time
Setting up Nextcloud AIO with S3 as the primary storage can be challenging.
This project simplifies everything.
* 🧰 Based on the **[Nextcloud All-in-One manual installation](https://github.com/nextcloud/all-in-one/tree/main/manual-install#manual-installation)**
* ✅ Preconfigured with **[MinIO](https://www.min.io/)** as your S3-compatible backend.
* 🔄 Easily swappable with AWS S3, Wasabi, or any other provider when you're ready for production.

Just **clone**, **run**, and **enjoy** Nextcloud with S3 in minutes.


## ⚡ Quick Start

### **1. Clone the repository**  
   ```bash
   git clone https://github.com/carmine-ambrosino/nextcloud-s3.git
   cd nextcloud-s3/compose
   cp .env.example .env
   ```

### **2. Setup `nextcloud.local`** 
By default, this stack uses `https://nextcloud.local` as the access point. To make it work, you need to tell your operating system to resolve `nextcloud.local` to your local machine `127.0.0.1`.

#### 🐧Linux - 🍎 macOS
* Open a `terminal`
* Edit the `hosts file` with elevated privileges:
   ```bash
   sudo nano /etc/hosts
   ```
* Add the following line at the bottom:
   ```bash
   127.0.0.1 nextcloud.local
   ```
* `Save` and `exit` (`CTRL+O`, `ENTER`, `CTRL+X`)

#### 🪟 Windows
* Open `Notepad` as Administrator
* Open the file:
   ```bash
   C:\Windows\System32\drivers\etc\hosts
   ```
* Add the following line at the bottom:
   ```bash
   127.0.0.1 nextcloud.local
   ```
* `Save` the file

### **3. Launch the stack**
   ```bash
   docker compose up -d
   ```
   
### **4. Access Nextcloud**
Wait 30 seconds and then open your browser and go to [https://nextcloud.local](https://nextcloud.local)
   
   > 💡 Tip: If your browser shows a warning about the certificate, you can safely proceed for local development. Caddy generates a self-signed certificate for `nextcloud.local`.


**Default login**
* Username: `admin`
* Password: `changeme`
 
## ⚙️ How it works 
This stack leverages the modular architecture of **Nextcloud All-in-One (AIO)** to deliver a robust, scalable, and secure self-hosted cloud platform. Each container plays a specific role in the ecosystem.

### 🧩 Core Components 
- **Nextcloud:** Hosts the main Nextcloud application. It provides the web interface and core functionalities like file sharing, calendar, contacts, and more.
- **Apache:** Acts as the internal web server for Nextcloud, handling HTTP requests and serving static assets. It communicates with the Nextcloud container and is reverse-proxied by Caddy.
- **PostgreSQL:** Stores all structured data — user accounts, app configurations, sharing metadata, etc.
- **Redis:** Provides caching and locking mechanisms to optimize performance and prevent race conditions during concurrent operations.
- **Notify-push:** Enables real-time push notifications for mobile and desktop clients, improving responsiveness and user experience.

### 🌐 Reverse Proxy 
- **Caddy:** Serves as the public-facing reverse proxy. It handles HTTPS termination, automatic certificate management and routes traffic to the Apache container. Caddy simplifies secure deployments with minimal configuration.

### 🗄️ Storage Layer 
- **Minio:** Acts as an S3-compatible object storage backend. Nextcloud uses it to store user files, previews, and app data. You can replace it with AWS S3 or other providers if needed.


## 🗣️ FAQ
### Why do I need to edit the hosts file?  
Because `nextcloud.local` is not a public domain — your operating system needs to know it should point to your local machine (`127.0.0.1`). This allows your browser to correctly resolve the address.

### Can I use a different domain?  
Absolutely. You can replace `nextcloud.local` with any custom domain. Edit `NC_DOMAIN`.

### Can I use this setup on a remote server?  
Yes. This stack works on VPS or cloud servers. You’ll need to configure DNS properly, expose the necessary ports, and replace `nextcloud.local` with your actual domain.

### Is MinIO required?  
MinIO is included by default for convenience, especially for local development. You can replace it with AWS S3, Wasabi, or any other S3-compatible provider by updating the storage configuration.
