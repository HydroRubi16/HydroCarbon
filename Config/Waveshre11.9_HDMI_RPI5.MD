1. Attach HDMI screen, attach USB power, USB Touch, and HDMI to the first HDMI port (closest to USB-C)  
2. SSH into the PI (might not be needed)  
	```sudo nano /boot/firmware/cmdline.txt```
          
	add the following at the very end:  
	```video=HDMI-A-1:1480x320@60,rotate=90```
	
3. Install Klipperscreen. When prompted for x11 or Wayland, choose W for Waland  
4. Klipperscreen installs Cage, and I could only get Weston to work:  
	Uninstall Cage:  
	```sudo systemctl stop KlipperScreen```
	```sudo apt remove cage```
	Install Weston:  
	```sudo apt install Weston seatd```
5. Verify HDMI port and connection status  
	```grep -H . /sys/class/drm/card*-*/status | grep :connected```
	Should look like: ```/sys/class/drm/card1-HDMI-A-1/status:connected```
		
6. Update INI file  
	```sudo nano ~/.config/weston.ini```
	Add the follow:  
	```[output]  
	name=HDMI-A-1  
	transform=rotate-90```
7. Reboot. Klipperscreen should be oriented correctly. Changing the rotating in the Weston.ini file also appears to change the touch overlay, as well.  
