# d007_tools

Development/research repo for SZDiier D007 Plus handheld


### Technical specs

- **CPU**: Rockchip RK3326
- **RAM**: 1024MB DDR3
- **Flash**: 8GB Samsung NAND
- **Screen**: 3.5 inches 640x480
- **Ports**: USB-C power, USB-C data, headphone jack 3.5mm, microSD slot
- **Buttons**: volume +/-, power, reset, ESC, gamepad buttons
- **Speaker**: 1 speaker


### Default system structure

Factory system (Android 8.1) is installed on flash within this partition scheme:

	NO  LBA       Name                
	00  16384     uboot
	01  24576     trust
	02  32768     misc
	03  40960     resource
	04  73728     kernel
	05  139264    boot
	06  204800    recovery
	07  335872    backup
	08  565248    security
	09  573440    cache
	10  1359872   system
	11  4505600   metadata
	12  4538368   vendor
	13  5324800   oem
	14  6635520   frp
	15  6636544   private
	16  7685120   logo
	17  7701504   userdata

SD card contains mainly game ROMs and some (not relevant) emulator configurations.


### Recovery mode

Keep volume up pressed, power on the device.


### Loader mode

Enter recovery mode and select "Reboot to bootloader".


### Safe mode

Power on device while keeping pressed volume down button until an Android stock launcher appears.


### Root access

ROM includes su binary by default, simply execute "su" command over ADB command line.


### Firmware backup

Using rkdeveloptool, rkloader or any other Rockchip-focused tool will only properly backup the first 32MB of flash, due to a bug? in device uboot. Anything beyond this point will be invalid data.
But as long as we have ADB shell and root permissions...

	dd if=/dev/block/mmcblk0 of=/storage/*external_SD_ID*/mmcblk0_backup.img


### Running other systems on D007

Device uboot is compatible with booting from SD, so any RK3326 distribution could boot with minor modifications (mainly DTB related).


### UART interface

[Three points indicated](docs/UART_location.jpg)


### Debugging with UART

On stock Android 8.1 logging stops as soon as Android itself starts booting (cmdline config probably). It's a config thing, so UART seems to be perfectly usable.
[UART log](docs/uart_log)


### Kernel config and DTBs

Located under this repo kernel and dtb folders.


### PCB

[Front](docs/PCB_front.jpg)
[Back](docs/PCB_back.jpg)

