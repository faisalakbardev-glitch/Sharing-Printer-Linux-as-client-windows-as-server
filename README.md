# Sharing-Printer-Linux-as-client-windows-as-server
Cara sharing printer linux sebagai client dan windows sebagai server
1. PERSIAPAN DI WINDOWS
--------------------------------------------------
- Aktifkan Sharing:
   - Masuk ke Control Panel -> Devices and Printers.
   - Klik kanan Epson L3210 -> Printer Properties -> Tab Sharing.
   - Centang "Share this printer" dan catat Share Name-nya (contoh: EPSON L3210 Series on Asus).
- Izin Akses (Permissions):
   - Di Tab Security, pastikan user 'Everyone' diberi izin 'Print'.
- Advanced Sharing:
   - Masuk ke Network and Sharing Center > Change advanced sharing settings.
   - Matikan "Password protected sharing" (opsional, untuk mempermudah akses).

2. INSTALASI DRIVER DI UBUNTU (CLIENT)
-----------------------------
- Download Driver:
   - Buka browser, cari: "Epson L3210 Linux Driver" di situs resmi Epson.
   - Pilih paket berformat .deb (LST/ESC-P-R).
- Install Driver:
   - Buka terminal di folder download, ketik:
     sudo apt install ./nama_file_driver.deb (debian,ubuntu,mint)
     sudo dnf install ./nama_file_driver.rpm (redhat,fedora)

3. INSTALASI SAMBA (CLIENT)
-----------------------------
- sudo apt update
- sudo apt install smbclient -y
- sudo systemctl restart cups

4. CEK NAMA PRINTER DI TERMINAL
-------------------------------
- smbclient -L 192.168.200.21(ini ip client) -U print%print11232(ini contoh user dan password dari server)

5. KONFIGURASI KONEKSI VIA CUPS (LOCALHOST)
-------------------------------
- Buka Browser di Ubuntu, akses URL: http://localhost:631
- Menu Administration:
   - Klik 'Add Printer' (Masukkan user & pass Ubuntu jika diminta).
   - Pilih 'Windows Printer via SAMBA', klik 'Continue'.
- Input Connection (Kunci Utama):
   - Masukkan alamat dengan format:
     smb://[username_windows]:[password_windows]@192.168.200.21/[Share_Name]
   - Contoh dengan spasi (%20):
     smb://print:password123@192.168.200.21/EPSON%20L3210%20Series%20on%20Asus
   - Klik 'Continue'.

6. PEMILIHAN DRIVER & FINISHING
-------------------------------
- Isi Nama & Deskripsi printer (bebas), klik 'Continue'.
- Pilih Make: 'Epson', klik 'Continue'.
- Pilih Model: 'Epson L3210 Series', klik 'Add Printer'.
- Klik 'Set Default Options'.

7. TESTING
-------------------------------
- Klik tab 'Printers' di CUPS.
- Pilih printer tadi, pilih Maintenance > Print Test Page.
- Pastikan status 'Idle, Accepting Jobs'.

