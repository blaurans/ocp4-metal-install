# Create a Private vSwitch named OKD  

``` Powershell
$VMName = 'P-OKD-SVC-001'
$InstallMedia = 'C:\Temp\CentOS-8.2.2004-x86_64-boot.iso'
$Switch = 'Default Switch'
$Switch2 = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 120GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 4
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:02
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("CD","Floppy", "LegacyNetworkAdapter",  "IDE")
Add-VMNetworkAdapter -VMName $VMName -SwitchName $Switch2 -StaticMacAddress 00:00:00:3E:3E:01

$VMName = 'P-OKD-MAST-001'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 4
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("CD","Floppy", "LegacyNetworkAdapter",  "IDE")
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:03

$VMName = 'P-OKD-MAST-002'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 4
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("CD","Floppy", "LegacyNetworkAdapter",  "IDE")
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:04

$VMName = 'P-OKD-MAST-003'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 4
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("CD","Floppy", "LegacyNetworkAdapter",  "IDE")
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:05

$VMName = 'P-OKD-WRK-001'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 4
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("CD","Floppy", "LegacyNetworkAdapter",  "IDE")
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:06

$VMName = 'P-OKD-WRK-002'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 4
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("CD","Floppy", "LegacyNetworkAdapter",  "IDE")
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:07

$VMName = 'P-OKD-BOOT-001'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 4
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("CD","Floppy", "LegacyNetworkAdapter",  "IDE")
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:08
```
