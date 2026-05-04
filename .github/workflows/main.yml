nane: RDP

workflow dispatch:

jobs:

secure-rdp:

runs-on: windows-latest

timeout-minutes: 3600

steps:

name: Configure Core RDP Settings

run:

#Enable Remote Desktop and disable Network Level Authentication (if needed)

Set -ItemProperty -Path "HKLM\System\CurrentControlSet\Control\Terminal Server

Set-ItemProperty Path "HKLM\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp -Name "UserAuthentication" Value 0 -Force

-Name "fDenyTSConnections Value 0 Farce

Set-ItemProperty Path "HKLM\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp

Name "SecurityLayer" Value -Force

#Renove any existing rule with the same name to avoid duplication netsh advfirewall firewall delete rule name "RDP-Taliscale"

# For testing, allow any incoming connection on port 3389 netsh advfirewall firewall add rule name "RDP-Tailscale" dir=in action=allow protocol=TCP localport=3389

#(Optional) Restart the Remote Desktop service to ensure changes take effect

Restart-Service Nane TermService Force

name: Create RDP User with Secure Password

run:

Add-Type-AssenblyName System.Security

ScharSet (

Upper

[char[]] (65.90)

Lower [char[]] (97..122) Na-z

Number [char[]] (48..57) N0-9 Special ([char[]](33..47) [char[]](58.64)+

[char[]](91..96) [char[]] (123..126)) # Special characters

$rawPassword()

Get-Randon -Count 4 Get-Randon-Count 4 SrawPassword = $charSet.Upper SrawPassword $charSet. Lower

Get-Random Count 4 SrawPassword $charset.Number

$rawPassword $charSet.Special | Get-Random Count 4 $password-join (SrasPassword Sort-Object ( Gel-Random })

$securePass ConvertTo-SecureString $password -AsPlainText -Force

New-LocalUser Name "Skyro" -Password $securePass -AccountNeverExpires. Add-LocalGroupMenber -Group "Administrators" -Member "Skyro"

Add-LocalGroupMember Group "Renote Desktop Users Member "skyro"

echo "ROP CREDS-User: Skyra | Password: $password" >> $env: GITHUB ENV

if ( not (Get-Localuser -Nane

exit 1

name: Install Tailscale

run:

$tsUrl = "https://pkgs.tailscale.com/stable/tailscale-setup-1.82.0-amd64.msi

SinstallerPath "Senv: TEMP\tailscale.msi"

Start-Process nsiexec.exe -ArgunentList "/1", """SinstallerPath""", "/quiet", "/norestart" -Wait Remove Iten $installerPath Force

Invoke-WebRequest Uri StsUrl OutFile $installerPath

name: Establish Tailscale Connection

Bring up Tailscale with the provided auth key and set a unique hostname. "Senv: ProgramFiles\Tailscale\tailscale.exe" up-authkey=$((secrets. TAILSCALE AUTH KEY }} --hostname-gh-

iner-Senv: GITHUB RUN ID

#Wait for Taliscale to assign an IP

$tsIP = Snull Sretries 0

shile (-not $LSIP-and $retries -It 10) (

StsIP & "Senv: ProgramFiles\Tailscale\tailscale.exe" ip 4

Start-Sleep -Seconds 5

$retries++

Write-Error "Tailscale IP not assigned. Exiting." exit 1

echo "TAILSCALE 1P-StsIP" Senv: GITHUB_ENV

name: Verify ROP Accessibility run:

Write-Host "Tailscale IP: Seny: TAILSCALE_IP"

#Test connectivity using Test-NetConnection against the Tailscale IP on port 3389 StestResult Test-NetConnection -Computer Name Senv: TAILSCALE IP-Port 3389

if (not StestResult.TcpTestSucceeded) { Write-Error "TCP connection to RDP port 3389 failed" exit 1

Write-Host "TCP connectivity successful!"

name: Maintain Connection run

write-Host "RDP ACCESS

write-Host "Address: $env: TAILSCALE IP" Write-Host "Username: Skyro

write-Host "Password: $(echo $env: ROP CREDS)"

write-Host "Π"

#Keep runner active indefinitely (or until manually cancelled) while ($true) {

Write-Host "[ "[$(Get-Date)] RDP Active Use Ctrl+C in workflow to terminate" Start-Sleep -Seconds 300
