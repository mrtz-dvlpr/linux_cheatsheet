export  
locate  
ls -ltrha  
type cd  
uname -a   
touch   
$USER  
$HISTFILE  
$PATH  
$PS1  
unset PS1 -> for delete environment variable  
history  
~/.bash_history  
Ctrl+R  
$HISTSIZE  
less : G, nG, n, ?, /, PgUp, PgDn   
cat test.txt test1.txt  
bzcat, xzcat, zcat, gzcat  
od -c test.txt , -a test.txt -> for binary files or spell all file.  
head -n10 test.txt   
tail -n10 test.txt , -f test.txt -> -f get online latest chagne  
split -d -n 10 test.txt book -> split test file to 10 sub file with name book00 book01 ,... book09 (set number because use -d) and break to 10 file because use of -n 10.  
Need to join these files? cat them with cat book0* > originalfile.  
cut -f 1,2,4,7-9 -d ',' test.txt : split test.txt by column with , and get columns 1,2,4,7to9  
nl   
sort -n -r -c test.txt ->  warning :  work on sorted data     
past test1.txt test2.txt  
cat test.txt > tr 'JS' 'js'  
sed 's/a/b/g' test.txt  
wc  
wc -l mydata | cat mydata - mydata   
sha256sum test.txt  
md5sum  
sha512sum  
echo  
rm -rm test  
mkdir -p one/two/tree  
  
touch  
Or you can specify times. It is possible to use -d and give dates or use -t and give a timestamp in the form of [[CC]YY]MMDDhhmm[.ss]  
$ touch -t 200908121510.59 file1  
$ touch -d 11am file2  
$ touch -d "last fortnight" file3  
$ touch -d "yesterday 6am" file4  
$ touch -d "2 days ago 12:00" file5  
$ touch -d "tomorrow 02:00" file6  
$ touch -d "5 Nov" file3  
$ ls -ltrh file?  
-rw-rw-r-- 1 jadi jadi 0 Aug 12  2009 file1  
-rw-rw-r-- 1 jadi jadi 0 Aug 12 12:00 file5  
-rw-rw-r-- 1 jadi jadi 0 Aug 13 06:00 file4  
-rw-rw-r-- 1 jadi jadi 0 Aug 14  2022 file2  
-rw-rw-r-- 1 jadi jadi 0 Aug 15  2022 file6  
-rw-rw-r-- 1 jadi jadi 0 Nov  5  2022 file3  
  
$file /bin/bash  
/bin/bash: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=33a5554034feb2af38e8c75872058883b2988bc5, for GNU/Linux 3.2.0, stripped  
  
dd if=~/test.txt of=~/dir/test1.txt  
find . iname "*png" -type d -size +100k  
find . -size 0   
find . -empty  
find   
  
 gzip fileName.txt  
 gunzip fileName.txt.gz  
 bzip2 fileName.txt  
 bunzip2 fileName.txt.bz2  
 xz fileName.txt  
 unxz fileName.txt.xz  
   
tar cfz archive.tar.gz fileOne.txt fileTwo.txt  
tar xf archive.tar.gz  
  
echo "hello" | xargs -I E echo morhza E     
  
ls -1 | tee allfiles myfiles  
  
$ tr ' ' '.' << END_OF_DATA  
> this is a line  
> and then this  
>  
> we'll still type  
> and,  
> done!  
> END_OF_DATA  
this.is.a.line  
  
nohup xeyes &  
jobs   
fg %<number of jobs>  
bg %<number of jobs>  
^z  
^c  
  
kill -15  <PID>  
kill -9 <PID>  
  
killall <process name>  
pkill <anything of all of process name>  
  
dev/null   
   
ps -ef   
ps -aux  
  
ps -ef | grep <target name>  
  
pgreg <traget name> = ps -ef | grep <target name>  
  
pgrep <target name> | xargs kill   
  
top  
  
free -h  
  
uptime   
  
watch uptime   
watch "df -h | grep sda1"  
  
nice (in -20_19 range)  
nice -n 14 ls  
  
renice -n 4 <target PID>  
  
df -h   
du -h    
du <directory> -h --max-depth 1 = search file size in directory with depth 1  
ex: du ./home -h --max-depth 1  
  

#################################################  
sys  
/proc  
/dev  
  
lsusb  
lspci  
lsmod   
lsblk  
lshw  
  
-- Loadable Kernel modules :  
lsmod  
rmmod  
modprobe  
insmod  
rmmod -f <modules name>  
/etc/modules  
/etc/modprobe.d  
  
-- Boot system :   
dmesg  
journalctl -k : kernul logs  
journalctl -b : boot logs  
/var/log/boot or /var/log/boot.log  
the bootloader file exist in : /boot/efi/EFI/.....  
systemctl list-units --type=target  
systemctl get-default  
systemctl cat list-unit-files  
systemctl stop sshd  
systemctl start sshd  
systemctl status sshd  
systemctl is-active sshd  
systemctl is-failed sshd  
systemctl restart sshd  
systemctl reload sshd # re-reads the configuration of the service configs  
systemctl daemon-reload sshd # re-reads the configuration of the systemd configs of this service  
systemctl enable sshd  
systemctl disable sshd  
/etc/systemd/system  
/run/systemd/system  
/usr/lib/systemd/system  
  
-- Runlevels / boot targets  
systemctl get-default  
systemctl status multi-user.target   
systemctl isolate emergency  
runlevel   
telinit  
/etc/init.d  
/etc/rc[0-6].d  
  
-- Unix directory  
bin	Essential command binaries  
boot	Static files of the boot loader  
dev	Device files  
etc	Host-specific system configuration  
home	Home directory of the users  
lib	Essential shared libraries and kernel modules  
media	Mount point for removable media  
mnt	Mount point for mounting a filesystem temporarily  
opt	Add-on application software packages  
root	Home directory of the root user  
sbin	Essential system binaries  
srv	Data for services provided by this system  
tmp	Temporary files, sometimes purged on each boot  
usr	Secondary hierarchy  
var	Variable data (logs, ...)  
  
-- Partition :   
mount | grep /dev/sda  
fdisk /dev/sda -> command p  
parted /dev/sda p  
gparted  
  
lsblk  
fdisk /dev/sda  
  
  
BIOS -> fdisk   
UEFI -> gdisk   
  
fdisk /dev/sda -l  
ls /sbin/mk*  
mkfs.exe4 /dev/sda6  
  
mkswap /dev/sda6  
  
fsck <partition> = fsck  /dev/sda1 -> find partition file system and with one of the /sbin/fsck.* check is partition file system ok .  
  
fsck -A  
fsck -y  
fsck -N  
fsck -i  
  
tune2fs  -l <partition>  
  
-- Swap :   
swapon  
  
swapon /dev/sda6  
  
-- Install a boot manager  
grub config at : /boot/grub/grub.cfg  
global config for grub.cfg file:   
#	Comment  
color	Foreground and background colors for normal and active items  
default	Which boot menu item is the default  
fallback	Which boot menu should be used if the default fails  
hiddenmenu	Hide the menu options  
splashimage	Show this image in the background!  
timeout	Wait this much and then start the default  
password	Security is important! Will ask this password  
savedefault	Remember the last booted item  
root	Disk and partition where /boot directory is. In the form of (hddrive, partition), say (hd0, 0) or (hd0, msdos0)  
kernel	Kernel image file name in /boot  
initrd	Initramfs file in /boot  
rootnoverify	Defines a non-Linux root partition  
chainloader	Another file will act as stage 1 loader. Used for booting Windows systems  
menuentry	Defines a new menuentry  
set root	Defines the root where /boot located  
linux, linux16	Defines the location of the Linux kernel on BIOS systems  
linuxefi	Defines the Linux kernel on UEFI systems  
initrd	Defines the initramfs image for BIOS systems  
initrdefi	Defines the initramfs image for UEFI systems  
  
***As you can see, GRUB uses Linux-style numbering for partitions, so the first partition on the first hard disk is (hd0,1) or (hd0,msdos1) for DOS partitions or (hd0,gpt1) for GPT drives.  
  
***The installation is done with grub-install /dev/sda and after changing the config files, you need to issue grub2-mkconfig or grub-mkconfig. It reads the configuration files from /etc/grub.d/ and /etc/default/grub/ and create the grub.cfg file based on them.   
  
file : /etc/grub.d  
file : /etc/default/grub  
then enter : grub2-mkconfig -o /boot/grub/grub.cfg  
or enter : grub2-mkconfig > /boot/grub/grub.cfg  
or enter : update-grub  
  
--  Manage shared libraries:   
ldd  
ldconfig  
/etc/ld.so.conf  
LD_LIBRARY_PATH  
  
/etc/ld.so.conf (Which might load more files from /etc/ld.so.conf.d/ in its beginning or its end)  
  
-- Mount   
mount <partition>  <directory>   
ex : mount  /dev/sda1  /tmp/testMount  
umount -f /dev/sda1  
umount -l /dev/sda1


-- permision  
whoami  
groups  
id  
ls -ltrh script.sh  
chmod 777 testFile.txt  
chmod u+rwx,g+rwg,o+rwg testFile.txt  

chown mori:root testFile.txt  
chgrp root testFile.txt  
A common switch is -R to chown recursively.  
newgrp root  

whereis passwd  
which passwd  

umask <mask number>
umask u=rw,g= ,o=  
chmod +x myfile  
execute (x character) means that they can see the files inside it, have a look if dir has not x   
