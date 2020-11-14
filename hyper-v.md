# Create a Private vSwitch named OKD


$VMName = 'P-OKD-SVC-001'
$InstallMedia = 'C:\Temp\CentOS-8.2.2004-x86_64-boot.iso'
$Switch = 'Default Switch'
New-VM -Name $VMName -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 120GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 4
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("CD","Floppy", "LegacyNetworkAdapter",  "IDE")

$VMName = 'P-OKD-MAST-001'
$InstallMedia = 'fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 4
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("CD","Floppy", "LegacyNetworkAdapter",  "IDE")
