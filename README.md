# PROJECT-6---SIMULASI-DATA-RECOVERY-SAAT-BLUESCREEN
# TUGAS 1 - BASIC RECOVERY
# Membuat Script setup.bat :
[Deskripsi gambar] 
(https://drive.google.com/file/d/1TeokDEm0kJxUakNAya1g3D_BuirF6QY1/view?usp=sharing)
(https://drive.google.com/file/d/1YZNjwh9QRz584xCsm87dC5oD29SHkRnM/view?usp=sharing)

~~~
@echo off
title SETUP SIMULASI DATA RECOVERY
echo ===========================================
echo         MEMBUAT SIMULASI DRIVE D
echo ===========================================
echo.

:: Lokasi di Desktop
set base=C:\Users\acer\Desktop\SimulasiDrive_D

:: Membuat folder utama SimulasiDrive_D
echo Membuat folder utama SimulasiDrive_D...
mkdir "%base%" >nul 2>&1

echo Membuat struktur folder dan file...
echo.

for /l %%i in (1,1,10) do (

    echo Membuat Folder_%%i ...
    mkdir "%base%\Folder_%%i\SubFolder_A"
    mkdir "%base%\Folder_%%i\SubFolder_B"
    mkdir "%base%\Folder_%%i\SubFolder_C"

    :: ========== SUBFOLDER A ==========
    echo PDF dummy file > "%base%\Folder_%%i\SubFolder_A\dokumen_%%i_A.pdf"
    echo CSV dummy file > "%base%\Folder_%%i\SubFolder_A\data_%%i_A.csv"
    echo TXT dummy file > "%base%\Folder_%%i\SubFolder_A\catatan_%%i_A.txt"
    echo DOCX dummy file > "%base%\Folder_%%i\SubFolder_A\laporan_%%i_A.docx"
    echo BAT dummy file > "%base%\Folder_%%i\SubFolder_A\aplikasi_%%i_A.bat"

    :: ========== SUBFOLDER B ==========
    echo file B1 > "%base%\Folder_%%i\SubFolder_B\file_b1_%%i.txt"
    echo file B2 > "%base%\Folder_%%i\SubFolder_B\file_b2_%%i.csv"
    echo file B3 > "%base%\Folder_%%i\SubFolder_B\file_b3_%%i.docx"
    echo file B4 > "%base%\Folder_%%i\SubFolder_B\file_b4_%%i.py"
    echo file B5 > "%base%\Folder_%%i\SubFolder_B\file_b5_%%i.jpg"

    :: ========== SUBFOLDER C ==========
    echo file C1 > "%base%\Folder_%%i\SubFolder_C\file_c1_%%i.txt"
    echo file C2 > "%base%\Folder_%%i\SubFolder_C\file_c2_%%i.ini"
    echo file C3 > "%base%\Folder_%%i\SubFolder_C\file_c3_%%i.pdf"
    echo file C4 > "%base%\Folder_%%i\SubFolder_C\file_c4_%%i.xml"
    echo file C5 > "%base%\Folder_%%i\SubFolder_C\file_c5_%%i.csv"
    echo file C6 > "%base%\Folder_%%i\SubFolder_C\file_c6_%%i.py"

    :: ========== FILE LUAR SUBFOLDER ==========
    echo database dummy file > "%base%\Folder_%%i\database_%%i.db"
    echo config dummy file > "%base%\Folder_%%i\config_%%i.ini"
)

echo.
echo ===========================================
echo       SETUP SELESAI ! DATA DIBUAT
echo ===========================================
echo Lihat di C:\Users\acer\Desktop\SimulasiDrive_D
echo.
pause
~~~

Penjelasan :
- @echo off → Menyembunyikan perintah agar tampilan lebih rapi.
- set base=... → Menentukan lokasi folder simulasi.
- mkdir → Membuat folder otomatis.
- for /l %%i in (1,1,10) → Perulangan dari Folder_1 sampai Folder_10.
- echo dummy file > nama_file → Membuat file dummy di setiap subfolder.
- pause → Menunggu input sebelum CMD ditutup.


# Menjalankan Script di Run as administrator CMD :
[Deskripsi gambar] 
(https://drive.google.com/file/d/1UpMQXXck7f6ZQHdfDP5BIKGyla0wbrMD/view?usp=sharing)
(https://drive.google.com/file/d/1teJ_UdRkjkQ3As7tbNIifnNgItYPapW3/view?usp=sharing)

~~~
C:\Users\LILI\Desktop\setup.bat
~~~

# Membuat Script recovery.bat :
[Deskripsi gambar] 
(https://drive.google.com/file/d/1jfNstHwmiP0PDK7SiQEHdw4fO2zbtIOE/view?usp=sharing)
(https://drive.google.com/file/d/1jfOOpq4NJMKLwy06aW8pLxlYl0UVjt68/view?usp=sharing)

~~~
@echo off
echo ===============================================
echo               PROCESS RECOVERY DATA
echo ===============================================
echo.

:: Lokasi sumber (folder simulasi drive D)
set sumber=C:\Users\acer\Desktop\SimulasiDrive_D

:: Lokasi tujuan (folder simulasi drive C)
set root=C:\Users\acer\Desktop\SimulasiDrive_C

:: Membuat folder utama SimulasiDrive_C jika belum ada
if not exist "%root%" mkdir "%root%"

:: Format tanggal dan waktu
set yr=%date:~10,4%
set mo=%date:~4,2%
set dy=%date:~7,2%
set hr=%time:~0,2%
set mn=%time:~3,2%

:: Hilangkan spasi pada jam
set hr=%hr: =0%

set tujuan=%root%\DataRecovery_%yr%%mo%%dy%_%hr%%mn%

:: Lokasi file log
set logfile=%root%\recovery_log.txt

:: Buat folder tujuan recovery
mkdir "%tujuan%" >nul 2>&1

echo Menyalin file dari:
echo %sumber%
echo ke:
echo %tujuan%
echo.

echo Membuat file log...
echo RECOVERY LOG > "%logfile%"
echo Tanggal: %date%  Waktu: %time% >> "%logfile%"
echo Sumber: %sumber% >> "%logfile%"
echo Tujuan: %tujuan% >> "%logfile%"
echo ---------------------------------------- >> "%logfile%"

:: SALIN ISI FOLDER (PERBAIKAN UTAMA)
xcopy "%sumber%\*" "%tujuan%\" /E /H /C /I /Y >> "%logfile%"

echo ---------------------------------------- >> "%logfile%"
echo Recovery selesai >> "%logfile%"

echo.
echo ===============================================
echo            RECOVERY SELESAI !!!
echo ===============================================
echo Log File: %logfile%
echo.

pause
~~~


Penjelasan (script ini) :
- Membuat folder tujuan dengan format tanggal & waktu.
- Membuat file log bernama recovery_log.txt.
- Menyalin semua file menggunakan xcopy dengan opsi /E /H /C /I /Y agar semua file ikut tersalin.
- Menulis riwayat ke log file.

# Menjalankan Script di Run as administrator CMD :
[Deskripsi gambar] (https://drive.google.com/file/d/1xVDylLeJ5GUgtkqnFYVwNHcEMrFQIhwr/view?usp=sharing)

~~~
C:\Users\LILI\Desktop\recovery.bat
~~~

# Menampilkan file recovery_log :
https://drive.google.com/file/d/1G121AbSw-QCKzSxY53sR_Djk4nl78yLM/view?usp=sharing

# TUGAS 2 - MODIFIKASI SCRIPT
# Membuat Script recoverydata.bat :
[Deskripsi gambar] 
(https://drive.google.com/file/d/1scW0jGmX4JBd-NxVCisg4P1uDPNNemOa/view?usp=sharing)
(https://drive.google.com/file/d/1aWGm4PnUsJQIRz7xC40L35e4sR5vDzw7/view?usp=sharing)
(https://drive.google.com/file/d/1Gj3CB7dVvanzP0iTCgclEvUK9nu_erkp/view?usp=sharing)

~~~
@echo off

setlocal enabledelayedexpansion
echo ===============================================
echo               PROCESS RECOVERY DATA
echo ===============================================
echo.

:: Lokasi sumber (folder simulasi drive D)
set sumber=C:\Users\acer\Desktop\SimulasiDrive_D

:: Lokasi tujuan (folder simulasi drive C)
set root=C:\Users\acer\Desktop

:: Membuat folder utama SimulasiDrive_C jika belum ada
if not exist "%root%" mkdir "%root%"

:: Format tanggal dan waktu
set yr=%date:~10,4%
set mo=%date:~4,2%
set dy=%date:~7,2%
set hr=%time:~0,2%
set mn=%time:~3,2%

:: Hilangkan spasi pada jam
set hr=%hr: =0%

set tujuan=%root%\DataRecovery_%yr%%mo%%dy%_%hr%%mn%
mkdir "%tujuan%"

echo Folder Recovery: %tujuan%
echo. 

:: Hitung Jumlah File PDF dan DOCX
set count=0
for /r "%sumber%" %%f in (*.pdf *.docx) do (
set /a count+=1
)

echo total file ditemukan: %count%
echo.

:: Proses Recovery
set num=0
for /r "%sumber%" %%f in (*.pdf *.docx) do (
set /a num+=1
echo [!num!/%count%] Menyalin: %%~nxf

:: Buat folder tujuan sama persis dengan sumber
set "rel=%%~dpf"
set "rel=!rel:%sumber%=!"
if not exist "%tujuan%!rel!" mkdir "%tujuan%!rel!"

:: Salin file
xcopy "%%f" "%tujuan%!rel!" >nul 2>&1

:: Verifikasi ukuran file
for %%A in ("%%f") do set size1=%%~zA
for %%B in ("%tujuan%!rel!%%~nxf") do set size2=%%~zB

if "!size1!"=="!size2!" (
	echo Verifikasi: OK
  ) else (
	echo Verifikasi: Gagal
  )
)

echo.
echo Membuat File ZIP...
set zipfile=%root%\DataRecovery_%yr%%mo%%dy%_%hr%%mn%.zip
echo Membuat zip: %zipfile%

:: ZIP PAKAI POWERSHELL (built-in Windows)
powershell -command "Compress-Archive -Path '%tujuan%\*' -DestinationPath '%zipfile%'"

echo.
echo ===============================================
echo            TUGAS 2 SELESAI !!!
echo ===============================================
echo hasil ZIP: %zipfile%.zip
echo.
pause
~~~

Penjelasan :
- for /r "%sumber%" %%f in (*.pdf *.docx) = hanya file PDF dan DOCX yang akan di-backup.
- set count=0  DAN  set num=0  = menambahkan counter, counter ini digunakan untuk menampilkan progress seperti: [5/40] Menyalin file.pdf
- for %%A in ("%%f") do set size1=%%~zA  DAN  for %%B in (tujuan) do set size2=%%~zB  =  untuk memverifikasi ukuran file (file size check), jika ukuran file sama → OK, kalau beda → Verifikasi gagal.
- Compress-Archive -Path 'folder' -DestinationPath 'file.zip'  =  untuk mengompres hasil backup ke .zip


# Menjalankan Script di Run as administrator CMD :
[Deskripsi gambar] 
(https://drive.google.com/file/d/13AiVBKIiEFHtCCFZIExsnTv2LZbB1TT6/view?usp=sharing)
(https://drive.google.com/file/d/1QGEdbJm4N284U_QYbrHlun_-_lCN4hqi/view?usp=sharing)
(https://drive.google.com/file/d/1E4YyUFXChkhsezWixvkNHRFHoH0UYxb1/view?usp=sharing)

~~~
C:\Users\LILI\Desktop\recoverydata.bat
~~~


# TUGAS 3 - ADVANCED RECOVERY SYSTEM
# Membuat Script advanced.bat :
[Deskripsi gambar] 
(https://drive.google.com/file/d/1xDYTHSHDm9AMl7Ar11Khuzwnj7MmbKkW/view?usp=sharing)
(https://drive.google.com/file/d/1ehWG0DhJWmLW3SyZ9M12_bWj8WvAHij3/view?usp=sharing)
(https://drive.google.com/file/d/18MC-RJwWD0ilCMWRuD57BSRRsAIXw-UN/view?usp=sharing)


~~~
@echo off
title ADVANCED DATA RECOVERY SYSTEM
color 0B

set BASE=%USERPROFILE%\Desktop
set SOURCE=%BASE%\SimulasiDrive_D
set DEST_BASE=%BASE%\SimulasiDrive_C

:MENU
cls
echo ==========================================================
echo                ADVANCED DATA RECOVERY SYSTEM
echo ==========================================================
echo Source Folder: %SOURCE%
echo Destination:   %DEST_BASE%
echo ==========================================================
echo  1. Selective Backup (Pilih Folder)
echo  2. Incremental Backup (Hanya file baru/berubah)
echo  3. Scheduled Backup (Backup tiap X menit)
echo  4. Email Notification (Notifikasi Gmail)
echo  5. Exit
echo ==========================================================
set /p opc=Masukkan pilihan (1-5): 

if %opc%==1 goto SELECTIVE
if %opc%==2 goto INCREMENTAL
if %opc%==3 goto SCHEDULE
if %opc%==4 goto EMAIL
if %opc%==5 exit
goto MENU

:SELECTIVE
cls
echo ---- SELECTIVE BACKUP ----
echo Folder tersedia:
dir "%SOURCE%" /b
echo.
set /p FOLDER=Ketik nama folder yang ingin di-backup: 

set DEST=%DEST_BASE%\Selective_%FOLDER%%date:~-4%%date:~4,2%%date:~7,2%%time:~0,2%%time:~3,2%
mkdir "%DEST%"

xcopy "%SOURCE%\%FOLDER%" "%DEST%" /E /H /C /I /Y

echo SELESAI! Backup selective tersimpan di:
echo %DEST%
pause
goto MENU

:INCREMENTAL
cls
echo ---- INCREMENTAL BACKUP ----
set DEST=%DEST_BASE%\IncrementalBackup
mkdir "%DEST%"

robocopy "%SOURCE%" "%DEST%" /E /XO /LOG:%DEST%\incremental_log.txt

echo SELESAI! Incremental backup berjalan.
pause
goto MENU

:SCHEDULE
cls
echo ---- SCHEDULED BACKUP ----
set /p interval=Backup berulang setiap berapa menit?: 
echo Jalankan CTRL + C untuk menghentikan proses.
timeout 3 > nul

:LOOP
set TS=%date:~-4%%date:~4,2%%date:~7,2%_%time:~0,2%%time:~3,2%
set DEST=%DEST_BASE%\Schedule_%TS%
mkdir "%DEST%"
xcopy "%SOURCE%" "%DEST%" /E /H /C /I /Y

echo ----- Backup dilakukan pada %TS% -----
timeout %interval% * 60 > nul
goto LOOP

:EMAIL
cls
echo ---- EMAIL NOTIFICATION ----
set /p email=Masukkan email Gmail tujuan: 
set /p pesan=Tulis pesan singkat notifikasi: 

C:\Program Files\PowerShell\7\pwsh.exe-Command "Send-MailMessage -To '%email%' -From '%email%' -Subject 'Backup Selesai' -Body '%pesan%' -SmtpServer 'smtp.gmail.com' -Port 587 -UseSsl -Credential (New-Object System.Management.Automation.PSCredential('%email%', (Read-Host 'Password email Gmail' -AsSecureString)))"

echo Email notifikasi dikirim sukses!
pause
goto MENU
~~~


Penjelasan :
- set /p FOLDER=xcopy "%SOURCE%\%FOLDER%" …  =  Selective Backup (Pilih folder yang ingin di-backup)
- robocopy "%SOURCE%" "%DEST%" /E /XO  =  Incremental backup (hanya file yang berubah atau baru yang akan di-backup), /XO artinya skip old files.
- :LOOP timeout %interval% * 60 goto LOOP  =  Scheduled Backup (Backup otomatis tiap X menit / Script akan melakukan backup berulang dengan loop)
- Send-MailMessage  =  untuk mendapatkan Email Notification.


# Menjalankan Script di CMD :
[Deskripsi gambar] (https://drive.google.com/file/d/1yMbgj2nqoHQOf3Q0CYG2OC4-o4FRiJQ-/view?usp=sharing)

~~~
cd Desktop
~~~

~~~
advanced.bat
~~~

Penjelasan :
- cd Desktop  =  untuk masuk ke dalam drive Desktop.
- advanced.bat  =  untuk menjalankan script anvanced.bat


# HASIL / TAMPILAN DARI SCRIPT :
(https://drive.google.com/file/d/1kIlxFQZmLHiWt3rpRLKeF--Gc70H76x5/view?usp=sharing)
(https://drive.google.com/file/d/1Ag1Wi8arRDsxGJXDTOXGUbxS2KHWtMti/view?usp=sharing)
(https://drive.google.com/file/d/17wCJ6aAgchF95DfSN38I6Dlgu4dpn3IF/view?usp=sharing)
(https://drive.google.com/file/d/1kaXHhss_hG-vPOuFHD1LX_q6bdcNcADD/view?usp=sharing)
(https://drive.google.com/file/d/1TIxrVz7Ki2E0LxlHT_839lKivjIYuG5Z/view?usp=sharing)
(https://drive.google.com/file/d/1Nt0fVFH4FkXv485EFh2VZqaC3cqDmQoq/view?usp=sharing)
(https://drive.google.com/file/d/1p6Zk6VoHoNJYznI4ok2vYLwCvZZPl4xf/view?usp=sharing)
(https://drive.google.com/file/d/11TaaOE9O3zGM8kuFmdtdJVYYHcOOgOFx/view?usp=sharing)
(https://drive.google.com/file/d/1lj8HlZ1a5RmJaSrORi7BDftW6mitNr6k/view?usp=sharing)
(https://drive.google.com/file/d/1eh-0txEeIZ8DsT4eWH7uwNpB4FiKMuEV/view?usp=sharing)
(https://drive.google.com/file/d/13Ip5qM03ZeFseJOy2QsBmwMaaf_SSyQN/view?usp=sharing)
(https://drive.google.com/file/d/1B_1eJdY-r96yYxBRSbLh9h64TT841dKM/view?usp=sharing)
