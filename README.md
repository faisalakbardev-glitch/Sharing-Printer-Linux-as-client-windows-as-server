# Sharing-Printer-Linux-as-client-windows-as-server
Cara sharing printer linux sebagai client dan windows sebagai server
1. PERSIAPAN DI WINDOWS
--------------------------------------------------
a. Aktifkan Sharing:
   - Masuk ke Control Panel > Devices and Printers.
   - Klik kanan Epson L3210 > Printer Properties > Tab Sharing.
   - Centang "Share this printer" dan catat Share Name-nya (contoh: EPSON L3210 Series on Asus).
b. Izin Akses (Permissions):
   - Di Tab Security, pastikan user 'Everyone' diberi izin 'Print'.
c. Advanced Sharing:
   - Masuk ke Network and Sharing Center > Change advanced sharing settings.
   - Matikan "Password protected sharing" (opsional, untuk mempermudah akses).

2. INSTALASI DRIVER DI UBUNTU (CLIENT)
--------------------------------------
a. Download Driver:
   - Buka browser, cari: "Epson L3210 Linux Driver" di situs resmi Epson.
   - Pilih paket berformat .deb (LST/ESC-P-R).
b. Install Driver:
   - Buka terminal di folder download, ketik:
     sudo apt install ./nama_file_driver.deb

3. INSTALASI SAMBA (CLIENT)
---------------------------
a. sudo apt update
b. sudo apt install smbclient -y
c. sudo systemctl restart cups

4. CEK NAMA PRINTER DI TERMINAL
-------------------------------
a. smbclient -L 192.168.200.21(ini ip client) -U print%print11232(ini contoh user dan password dari server)

5. KONFIGURASI KONEKSI VIA CUPS (LOCALHOST)
-------------------------------------------
a. Buka Browser di Ubuntu, akses URL: http://localhost:631
b. Menu Administration:
   - Klik 'Add Printer' (Masukkan user & pass Ubuntu jika diminta).
   - Pilih 'Windows Printer via SAMBA', klik 'Continue'.
c. Input Connection (Kunci Utama):
   - Masukkan alamat dengan format:
     smb://[username_windows]:[password_windows]@192.168.200.21/[Share_Name]
   - Contoh dengan spasi (%20):
     smb://print:password123@192.168.200.21/EPSON%20L3210%20Series%20on%20Asus
   - Klik 'Continue'.

6. PEMILIHAN DRIVER & FINISHING
-------------------------------
a. Isi Nama & Deskripsi printer (bebas), klik 'Continue'.
b. Pilih Make: 'Epson', klik 'Continue'.
c. Pilih Model: 'Epson L3210 Series', klik 'Add Printer'.
d. Klik 'Set Default Options'.

7. TESTING
----------
a. Klik tab 'Printers' di CUPS.
b. Pilih printer tadi, pilih Maintenance > Print Test Page.
c. Pastikan status 'Idle, Accepting Jobs'.

