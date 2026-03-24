all:
	dd if=boot.img of=Image bs=1 skip=2048 count=19804160
	dd if=boot.img of=dtb-kernel.dtb bs=1 skip=17850368 count=96816
	dtc -I dtb -O dts dtb-kernel.dtb -o dtb-kernel.dts
	ls -alh Image dtb-kernel.dtb dtb-kernel.dts


