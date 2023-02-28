@echo off
chcp 65001


rem Nainstalujte FreeCommander kopírováním souborů

rem prejdeme do slozky kde je instalacni balicek
cd C:\Instalace\FreeCommander
rem prikaz pro spusteni instalacniho programu
start /wait FreeCommander_setup.exe /S /NCRC


rem Zástupce na ploše

rem Promenna musí odkazovat na správnou cestu k programu
set FCPath="C:\Program Files\FreeCommander\FreeCommander.exe"
rem Zde pojmenujeme zástupce
set FCName="FreeCommander"
rem Vytvoření zástupce
echo [InternetShortcut] > "%userprofile%\Desktop\%FCName%.url"
echo URL=file://%FCPath% >> "%userprofile%\Desktop\%FCName%.url"
echo IconIndex=0 >> "%userprofile%\Desktop\%FCName%.url"
echo IconFile=%FCPath% >> "%userprofile%\Desktop\%FCName%.url"


rem Nainstalujte Firefox a Thunderbird pomocí Ninite

rem Funguje pouze s připojením k internetu
Invoke-WebRequest -Uri https://ninite.com/firefox-thunderbird/ninite.exe -OutFile C:\Instalace\ninite.exe
rem Tento příkaz spouští instalační soubor Ninite, který byl stažen v předchozím kroku. Spouští se s argumenty "firefox,thunderbird"
Start-Process -FilePath "C:\Instalace\ninite.exe" -ArgumentList 'firefox,thunderbird' -Wait


rem Nainstalujte Adobe Reader a CCleaner pomocí Chocolatey

rem stazeni a instalace Chocolatey
powershell.exe -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))"
rem instalace Adobe Reader
choco install adobereader -y
ram instalace CCleaner
choco install ccleaner -y


rem Nainstalujte a odinstalujte 2 své oblíbené programy pomocí MSI balíku (bez klikání, tj. tiše)

rem /i je instalace
msiexec /i "cesta\k\souboru.msi" /qn
rem /x je odinstalace
msiexec /x "cesta\k\souboru.msi" /qn


rem Ze support.microsoft.com ručně stáhněte instalační soubor pro C++Redistributable

rem kontrola, zda systém má 64-bitovou architekturu
if "%PROCESSOR_ARCHITECTURE%"=="AMD64" (
rem spuštění 64bitové verze instalačního programu
   start /wait C:\Instalace\vc_redist.x64.exe /quiet
) else (
rem spuštění 32bitové verze instalačního programu - /quiet je pro tichou instalaci
   start /wait C:\Instalace\vc_redist.x86.exe /quiet
)
pause
