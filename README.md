## Panduan Instalasi WSL dan Docker di Windows

### **Langkah 1: Aktifkan WSL dan Virtual Machine Platform**
1. **Buka PowerShell sebagai Administrator**.
2. Jalankan perintah berikut untuk mengaktifkan WSL dan Virtual Machine Platform:
   ```powershell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```

3. **Update Kernel WSL (Jika Diperlukan)**:
   - Unduh [WSL kernel update package](https://aka.ms/wsl2kernel).
   - Instal paket tersebut di komputer Anda.

4. **Setel WSL ke Versi 2**:
   - Jadikan WSL versi 2 sebagai default:
     ```powershell
     wsl --set-default-version 2
     ```

5. **Instal Distro Linux (Ubuntu)**:
   - Buka **Microsoft Store**, cari, dan instal **Ubuntu** (misalnya, Ubuntu 20.04, 22.04, atau 24.04).
   - Setelah instalasi selesai, buka aplikasi Ubuntu dan ikuti proses setup.
   - Buat **username** dan **password** Linux saat diminta.

---

### **Langkah 2: Instalasi dan Konfigurasi Docker di WSL**
1. **Update Sistem di Distro Linux**:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. **Tambahkan Repository Docker**:
   ```bash
   sudo apt install -y ca-certificates curl gnupg
   sudo install -m 0755 -d /etc/apt/keyrings
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   sudo chmod a+r /etc/apt/keyrings/docker.gpg
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
   https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

3. **Instal Docker Engine**:
   ```bash
   sudo apt update
   sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   ```

4. **Jalankan Docker tanpa Sudo (Opsional)**:
   - Tambahkan user Anda ke grup `docker`:
     ```bash
     sudo usermod -aG docker $USER
     ```
   - Logout dan login kembali ke terminal WSL agar perubahan grup diterapkan.

5. **Start Docker di WSL**:
   ```bash
   sudo service docker start
   ```

6. **Uji Docker**:
   - Jalankan container uji:
     ```bash
     docker run hello-world
     ```

---

### **Langkah 3: Integrasi Docker Desktop dengan WSL (Opsional)**
1. **Instal Docker Desktop**:
   - Unduh dan instal [Docker Desktop](https://www.docker.com/products/docker-desktop).

2. **Aktifkan Integrasi WSL**:
   - Buka **Docker Desktop**.
   - Pergi ke **Settings > Resources > WSL Integration**.
   - Aktifkan **Enable integration with my default WSL distro**.
   - Pilih distro WSL Anda (misalnya, Ubuntu).

3. **Restart Docker Desktop**:
   - Klik **Apply & Restart**.

---

### **Tips**
- **Cek Status WSL**:
  ```powershell
  wsl --list --verbose
  ```
- **Stop Docker Engine**:
  ```bash
  sudo service docker stop
  ```
