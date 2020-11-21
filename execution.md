# Creation des VM
```powershell
$VMName = 'P-OKD-BOOT-001'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1 -MaximumBytes 8GB -MinimumBytes 1GB
Set-VMProcessor -VMName $VMName -count 2
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VM -VMName $VMName -CheckpointType disabled
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:08

$VMName = 'P-OKD-MAST-001'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VM -VMName $VMName -CheckpointType disabled
Set-VMProcessor -VMName $VMName -count 2
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1 -MaximumBytes 16GB -MinimumBytes 1GB
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:03
```
