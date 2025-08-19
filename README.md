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
Open your browser and go to [https://nextcloud.local](https://nextcloud.local)

   
   > 💡 Tip: If your browser shows a warning about the certificate, you can safely proceed for local development. Caddy generates a self-signed certificate for `nextcloud.local`.
  
  
