#dump1090-fa-arch

dump1090-fa for Arch Linux & Arch Linux Arm

Enter cloned directory. It contains following three files
- PKGBUILD
- foo.install
- README.md

Give command `makepkg -si `

Above command will run the PKGBUILD script which will: 

1. Check for conflicts with existing other versions of dump1090
2. Check Build tools needed (git, make, gcc, pkgconf, binutils, and fakeroot), and will offer to install missing tools [Yes/no]. 
3. Will offer to install dependencies rtl-sdr, lighttpd, and bladerf [Yes/no]
4. Will build package `dump1090-fa-latest-*-*.pkg.tar.xz`
5. Offer to install the above package[Yes/no]

The above package can be install later also by following command:
```
cd dump1090-fa-arch 
sudo pacman -U dump1090-fa-latest-*-*.pkg.tar.xz
```
### IMPORTANT: AFTER INSTALLATION, REBOOT COMPUTER / RPI.

**To check status:**
```
sudo systemctl status dump1090-fa
```

**To restart:**
```
sudo systemctl restart dump1090-fa
```

############################################################

##  T H I N G S - TO -  DO (AFTER INSTALLATION IS COMPLETED)
  
############################################################

### IMPORTANT: REBOOT COMPUTER/RPi
### OTHERWISE DUMP1090-FA WILL FAIL TO START
### AND A ROTATING WHEEL WILL APPEARS ON THE MAP, OR MAP WILL NOT SHOW



To make SkyView Map show range rings, do following:

1. Open file "dump1090-fa" for editing
    sudo nano  /etc/default/dump1090-fa

2. In the opened file, go to following line:
    RECEIVER_OPTIONS="--device-index 0 --gain -10 --ppm 0 --net-bo-port 30005"
    In above line, add your latitude and longitude, so the line becomes like below:
    RECEIVER_OPTIONS="--device-index 0 --gain -10 --lat xx.xxxx --lon yy.yyyy --ppm 0 --net-bo-port 30005"
    NOTE: Repalce xx.xxxx and yy.yyyy by your actual latitude and Longitude

3. Restart dump1090-fa

    `sudo systemctl restart dump1090-fa `

4. Clear browser cache and reload browser
