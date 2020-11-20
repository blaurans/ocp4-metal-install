# To add to command line after a TAB according to doc
```
coreos.inst.install_dev=sda coreos.inst.image_url=http://192.168.22.1:8080/ocp4/fcos coreos.inst.ignition_url=http://192.168.22.1:8080/ocp4/bootstrap.ign
coreos:inst:instqll°dev=sdq coreos:inst:i,qge°url=httpM!!&çé:&-_:éé:&M_à_à!ocp'!fcos coreos:inst:ignition°url=httpM!!&çé:&-_:éé:&M_à_à!ocp'!bootstrqp:ign
coreos:inst:instqll°dev=sdq coreos:inst:i,qge°url=httpM!!&çé:&-_:éé:&M_à_à!ocp'!fcos coreos:inst:ignition°url=httpM!!&çé:&-_:éé:&M_à_à!ocp'!,qster:ign
coreos:inst:instqll°dev=sdq coreos:inst:i,qge°url=httpM!!&çé:&-_:éé:&M_à_à!ocp'!fcos coreos:inst:ignition°url=httpM!!&çé:&-_:éé:&M_à_à!ocp'!zorker:ign
```

# Alternate - To type after boot


```
mv ./fedora-coreos-32.20201018.3.0-metal.x86_64.raw.xz.sig /var/www/html/ocp4/fcos.sig

http://172.25.127.158:9000/stats
```



# Latest version of hyper-v VM creation
```
$VMName = 'P-OKD-SVC-001'
$InstallMedia = 'C:\Temp\CentOS-8.2.2004-x86_64-minimal.iso'
$Switch = 'Default Switch'
$Switch2 = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 120GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 2
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:02
Set-VM -VMName $VMName -CheckpointType disabled
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Add-VMNetworkAdapter -VMName $VMName -SwitchName $Switch2 -StaticMacAddress 00:00:00:3E:3E:01

$VMName = 'P-OKD-MAST-001'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VM -VMName $VMName -CheckpointType disabled
Set-VMProcessor -VMName $VMName -count 2
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:03

$VMName = 'P-OKD-MAST-002'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 2
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1 -MaximumBytes 16GB -MinimumBytes 1GB
Set-VM -VMName $VMName -CheckpointType disabled
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:04

$VMName = 'P-OKD-MAST-003'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 2
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1 -MaximumBytes 16GB -MinimumBytes 1GB
Set-VM -VMName $VMName -CheckpointType disabled
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:05

$VMName = 'P-OKD-WRK-001'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 2
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1
Set-VM -VMName $VMName -CheckpointType disabled
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:06

$VMName = 'P-OKD-WRK-002'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 2
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VM -VMName $VMName -CheckpointType disabled
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:07

$VMName = 'P-OKD-BOOT-001'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1
Set-VMProcessor -VMName $VMName -count 2
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VM -VMName $VMName -CheckpointType disabled
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:08


https://api-int.lab.okd.lan:22623/config/worker
```
