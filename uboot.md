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
