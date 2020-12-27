A executer quand la machine p-okd-svc-001 est déjà crée
# Se connecter à un hôte hyper-v à distance
```powershell
Enter-PSSession hyperv.lauransad.local
Enter-PSSession t30.lauransad.local
```

# Preparation des hotes Hyper-V
```batch
md c:\temp
md c:\vm-machine
net share temp=c:\temp /grant:everyone,change
net share vm-machine=c:\vm-machine /grant:everyone,change
```
# Nettoyage des VM precedentes (optionnel)
```powershell
$VMName = 'P-OKD-BOOT-001'
Remove-VM -Name "$VMName" -Force
Remove-Item -Path "C:\vm-machine\$VMName" -Recurse

$VMName = 'P-OKD-MAST-001'
Remove-VM -Name "$VMName" -Force
Remove-Item -Path "C:\vm-machine\$VMName" -Recurse

$VMName = 'P-OKD-WRK-001'
Remove-VM -Name "$VMName" -Force
Remove-Item -Path "C:\vm-machine\$VMName" -Recurse

$VMName = 'P-OKD-WRK-002'
Remove-VM -Name "$VMName" -Force
Remove-Item -Path "C:\vm-machine\$VMName" -Recurse

$VMName = 'P-OKD-MAST-002'
Remove-VM -Name "$VMName" -Force
Remove-Item -Path "C:\vm-machine\$VMName" -Recurse

$VMName = 'P-OKD-MAST-003'
Remove-VM -Name "$VMName" -Force
Remove-Item -Path "C:\vm-machine\$VMName" -Recurse

```
# Nettoyage de l'install precedente (optionnel)
```bash
rm -rf /tmp/version46GA
rm -rf /var/www/html/version46GA
```
# Creation des VM
## Sur T30.  
```powershell
$VMName = 'P-OKD-BOOT-001'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 8GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1 -MaximumBytes 16GB -MinimumBytes 1GB
#Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 0
Set-VMProcessor -VMName $VMName -count 2
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VM -VMName $VMName -CheckpointType disabled
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:08

$VMName = 'P-OKD-MAST-001'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 16GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VM -VMName $VMName -CheckpointType disabled
Set-VMProcessor -VMName $VMName -count 2
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1 -MaximumBytes 18GB -MinimumBytes 1GB
#Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 0
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:03

$VMName = 'P-OKD-WRK-001'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 2
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1 -MaximumBytes 4GB -MinimumBytes 1GB
Set-VM -VMName $VMName -CheckpointType disabled
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:06

$VMName = 'P-OKD-WRK-002'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 2
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1 -MaximumBytes 4GB -MinimumBytes 1GB
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VM -VMName $VMName -CheckpointType disabled
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:07


```
## Sur Core i5.
```powershell

$VMName = 'P-OKD-MAST-002'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 16GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 2
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1 -MaximumBytes 18GB -MinimumBytes 1GB
# Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 0
Set-VM -VMName $VMName -CheckpointType disabled
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:04

$VMName = 'P-OKD-MAST-003'
$InstallMedia = 'C:\Temp\fedora-coreos-32.20201018.3.0-live.x86_64.iso'
$Switch = 'OKD'
New-VM -Name $VMName -MemoryStartupBytes 16GB -BootDevice VHD -NewVHDPath "C:\vm-machine\$VMName\$VMName.vhdx" -NewVHDSizeBytes 50GB -Path "C:\vm-machine\$VMName" -SwitchName $Switch
Set-VMProcessor -VMName $VMName -count 2
Set-VMMemory -VMName $VMName -DynamicMemoryEnabled 1 -MaximumBytes 18GB -MinimumBytes 1GB
Set-VM -VMName $VMName -CheckpointType disabled
Add-VMDvdDrive -VMName $VMName -Path $InstallMedia
Set-VMBios $VMName -StartupOrder @("IDE","CD","Floppy", "LegacyNetworkAdapter" )
Set-VMNetworkAdapter -VMName $VMName -StaticMacAddress 00:00:00:3E:3E:05

```
# Changement de l'image fcos
lien https://getfedora.org/coreos/download?tab=metal_virtualized&stream=stable  
Ne pas oublier de charger la signature aussi  
``` bash
scp fcos4 root@192.168.38.138:/var/www/html/ocp4/fcos4
scp fcos4.sig root@192.168.38.138:/var/www/html/ocp4/fcos4.sig
```
/var/www/html

# Generation des fichiers de configuration
Depuis la machine p-okd-svc-001. 
```bash
mkdir /tmp/version46GA
cd /tmp/version46GA
wget https://github.com/openshift/okd/releases/download/4.5.0-0.okd-2020-07-14-153706-ga/openshift-install-linux-4.5.0-0.okd-2020-07-14-153706-ga.tar.gz
tar zxvf openshift-install-linux-4.5.0-0.okd-2020-07-14-153706-ga.tar.gz
rm -f op*.gz
git clone https://github.com/blaurans/ocp4-metal-install
cp ../install-config.yaml .
./openshift-install create manifests --dir .
./openshift-install create ignition-configs --dir .
mkdir /var/www/html/version46GA
cp -R ./* /var/www/html/version46GA
chcon -R -t httpd_sys_content_t /var/www/html/version46GA/
chown -R apache: /var/www/html/version46GA/
chmod 755 /var/www/html/version46GA/
```
# Parametres de configuration des instances (tab au boot, ajouter a la suite de la ligne de boot
```
coreos.inst.install_dev=sda coreos.inst.image_url=http://192.168.22.1:8080/ocp4/fcos coreos.inst.ignition_url=http://192.168.22.1:8080/version45GA/bootstrap.ign
coreos:inst:instqll°dev=sdq coreos:inst:i,qge°url=httpM!!&çé:&-_:éé:&M_à_à!ocp'!fcos' coreos:inst:ignition°url=httpM!!&çé:&-_:éé:&M_à_à!version'-GQ!bootstrqp:ign
coreos:inst:instqll°dev=sdq coreos:inst:i,qge°url=httpM!!&çé:&-_:éé:&M_à_à!ocp'!fcos' coreos:inst:ignition°url=httpM!!&çé:&-_:éé:&M_à_à!version'-GQ!,qster:ign
coreos:inst:instqll°dev=sdq coreos:inst:i,qge°url=httpM!!&çé:&-_:éé:&M_à_à!ocp'!fcos' coreos:inst:ignition°url=httpM!!&çé:&-_:éé:&M_à_à!version'-GQ!zorker:ign

```
# Check config
``` bash
ssh -i /tmp/okd.key core@192.168.22.200 # Bootstrap 
ssh -i /tmp/okd.key core@192.168.22.201 # Master 001 
ssh -i /tmp/okd.key core@192.168.22.202 # Master 002
ssh -i /tmp/okd.key core@192.168.22.203 # Master 003 
ssh -i /tmp/okd.key core@192.168.22.204 # Worker 001
sudo crictl ps | wc -l
```
