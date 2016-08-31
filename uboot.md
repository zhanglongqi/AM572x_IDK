uEnv.txt:
```
autoload=no
ipaddr=192.168.1.100
serverip=192.168.1.13
gatewayip=192.168.1.1
staticip=${ipaddr}:${serverip}:${gatewayip}:255.255.255.0:::off
bootpath=/tftpboot
rootfspath=/opt/ti-processor-sdk-linux-rt-am57xx-evm-03.00.00.04/targetNFS

#setting for kernel loading
kernel_addr=0x82000000
fdt_addr=0x88000000

nfs_args=setenv bootargs console=ttyO0,115200n8 root=/dev/nfs rw nfsroot=${serverip}:${rootfspath} ip=${staticip}
load_zimage=tftp ${kernel_addr} ${bootpath}/zImage
loadfdt=tftp ${fdt_addr} ${bootpath}/am572x-idk.dtb
boot_zimage=bootz ${kernel_addr} - ${fdt_addr}
uenvcmd=run load_zimage; run loadfdt; run nfs_args; run boot_zimage

```

This is the terminal output.
```
U-Boot SPL 2016.05-00230-ge9ef52a-dirty (Aug 30 2016 - 18:40:04)
DRA752-GP ES2.0
Trying to boot from MMC1
reading args
spl_load_image_fat_os: error reading image args, err - -1
reading u-boot.img
reading u-boot.img
reading u-boot.img
reading u-boot.img


U-Boot 2016.05-00230-ge9ef52a-dirty (Aug 30 2016 - 18:40:04 +0800)

CPU  : DRA752-GP ES2.0
Model: TI AM5728 IDK
Board: AM572x IDK REV 1.3B
I2C:   ready
DRAM:  2 GiB
MMC:   OMAP SD/MMC: 0, OMAP SD/MMC: 1
reading uboot.env

** Unable to read "uboot.env" from mmc0:1 **
Using default environment

SCSI:  SATA link 0 timeout.
AHCI 0001.0300 32 slots 1 ports 3 Gbps 0x1 impl SATA mode
flags: 64bit ncq stag pm led clo only pmp pio slum part ccc apst 
scanning bus for devices...
Found 0 device(s).
Net:   
Warning: ethernet@48484000 using MAC address from ROM
eth0: ethernet@48484000
Hit any key to stop autoboot:  0 
switch to partitions #0, OK
mmc0 is current device
SD/MMC found on device 0
reading boot.scr
** Unable to read file boot.scr **
reading uEnv.txt
1214 bytes read in 4 ms (295.9 KiB/s)
Loaded env from uEnv.txt
Importing environment from mmc0 ...
Running uenvcmd ...
ethernet@48484000 Waiting for PHY auto negotiation to complete. done
link up on port 0, speed 100, full duplex
Using ethernet@48484000 device
TFTP from server 192.168.1.13; our IP address is 192.168.1.100
Filename '/tftpboot/zImage'.
Load address: 0x82000000
Loading: #################################################################
	 #################################################################
	 #################################################################
	 #################################################################
	 #################################################################
	 #################################################################
	 #################################################################
	 #################################################################
	 #################################################################
	 #################################################################
	 #################################################################
	 ##################
	 420.9 KiB/s
done
Bytes transferred = 3750160 (393910 hex)
link up on port 0, speed 100, full duplex
Using ethernet@48484000 device
TFTP from server 192.168.1.13; our IP address is 192.168.1.100
Filename '/tftpboot/am572x-idk.dtb'.
Load address: 0x88000000
Loading: ####################
	 991.2 KiB/s
done
Bytes transferred = 99552 (184e0 hex)
Kernel image @ 0x82000000 [ 0x000000 - 0x393910 ]
## Flattened Device Tree blob at 88000000
   Booting using the fdt blob at 0x88000000
   Loading Device Tree to 8ffe4000, end 8ffff4df ... OK

Starting kernel ...


```
This is the output of printenv.
```
arch=arm
args_mmc=run finduuid;setenv bootargs console=${console} ${optargs} root=PARTUUID=${uuid} rw rootfstype=${mmcrootfstype}
baudrate=115200
board=am57xx
board_name=am572x_idk
board_rev=1.3B
board_serial=04164P470035
bootcmd=if test ${dofastboot} -eq 1; then echo Boot fastboot requested, resetting dofastboot ...;setenv dofastboot 0; saveenv;echo Booting into fastboot ...; fastboot 0;fi;run findfdt; run envboot; run mmcboot;setenv mmcdev 1; setenv bootpart 1:2; setenv mmcroot /dev/mmcblk0p2 rw; run mmcboot;
bootdelay=2
bootdir=/boot
bootenvfile=uEnv.txt
bootfile=zImage
bootm_size=0x10000000
bootpart=0:2
bootscript=echo Running bootscript from mmc${mmcdev} ...; source ${loadaddr}
console=ttyO2,115200n8
cpu=armv7
dofastboot=0
envboot=mmc dev ${mmcdev}; if mmc rescan; then echo SD/MMC found on device ${mmcdev};if run loadbootscript; then run bootscript;else if run loadbootenv; then echo Loaded env from ${bootenvfile};run importbootenv;fi;if test -n $uenvcmd; then echo Running uenvcmd ...;run uenvcmd;fi;fi;fi;
ethaddr=a0:f6:fd:b2:3f:ee
fdt_addr_r=0x88000000
fdtaddr=0x88000000
fdtcontroladdr=fef33ef0
fdtfile=undefined
findfdt=if test $board_name = omap5_uevm; then setenv fdtfile omap5-uevm.dtb; fi; if test $board_name = dra7xx; then setenv fdtfile dra7-evm.dtb; fi;if test $board_name = dra72x-revc; then setenv fdtfile dra72-evm-revc.dtb; fi;if test $board_name = dra72x; then setenv fdtfile dra72-evm.dtb; fi;if test $board_name = beagle_x15; then setenv fdtfile am57xx-beagle-x15.dtb; fi;if test $board_name = beagle_x15_revb1; then setenv fdtfile am57xx-beagle-x15-revb1.dtb; fi;if test $board_name = am57xx_evm; then setenv fdtfile am57xx-evm.dtb; fi;if test $board_name = am57xx_evm_reva3; then setenv fdtfile am57xx-evm-reva3.dtb; fi;if test $board_name = am572x_idk; then setenv fdtfile am572x-idk.dtb; fi;if test $board_name = am571x_idk; then setenv fdtfile am571x-idk.dtb; fi;if test $fdtfile = undefined; then echo WARNING: Could not determine device tree to use; fi; 
finduuid=part uuid mmc 0:2 uuid
importbootenv=echo Importing environment from mmc${mmcdev} ...; env import -t ${loadaddr} ${filesize}
kernel_addr_r=0x82000000
loadaddr=0x82000000
loadbootenv=fatload mmc ${mmcdev} ${loadaddr} ${bootenvfile}
loadbootscript=fatload mmc ${mmcdev} ${loadaddr} boot.scr
loadfdt=load mmc ${bootpart} ${fdtaddr} ${bootdir}/${fdtfile};
loadimage=load mmc ${bootpart} ${loadaddr} ${bootdir}/${bootfile}
mmcboot=mmc dev ${mmcdev}; if mmc rescan; then echo SD/MMC found on device ${mmcdev};if run loadimage; then run loadfdt; echo Booting from mmc${mmcdev} ...; run args_mmc; bootz ${loadaddr} - ${fdtaddr}; fi;fi;
mmcdev=0
mmcrootfstype=ext4 rootwait
netargs=setenv bootargs console=${console} ${optargs} root=/dev/nfs nfsroot=${serverip}:${rootpath},${nfsopts} rw ip=dhcp
netboot=echo Booting from network ...; setenv autoload no; dhcp; run netloadimage; run netloadfdt; run netargs; bootz ${loadaddr} - ${fdtaddr}
netloadfdt=tftp ${fdtaddr} ${fdtfile}
netloadimage=tftp ${loadaddr} ${bootfile}
nfsopts=nolock
partitions=uuid_disk=${uuid_gpt_disk};name=rootfs,start=2MiB,size=-,uuid=${uuid_gpt_rootfs}
pxefile_addr_r=0x80100000
ramdisk_addr_r=0x88080000
rdaddr=0x88080000
rootpath=/export/rootfs
scriptaddr=0x80000000
scsidevs=0
soc=omap5
static_ip=${ipaddr}:${serverip}:${gatewayip}:${netmask}:${hostname}::off
stderr=serial@48020000
stdin=serial@48020000
stdout=serial@48020000
usbtty=cdc_acm
vendor=ti
ver=U-Boot 2016.05-00230-ge9ef52a-dirty (Aug 30 2016 - 18:40:04 +0800)
vram=16M

Environment size: 3624/65532 bytes
```
