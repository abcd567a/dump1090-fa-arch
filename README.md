# dump1090-fa-arch

### dump1090-fa for Arch Linux & Arch Linux Arm

```
git clone https://github.com/abcd567a/dump1090-fa-arch.git

cd dump1090-fa-arch

makepkg -si

```

The cloned directory contains following three files

- PKGBUILD
- foo.install
- README.md

Give command `makepkg -si `

Above command will run the PKGBUILD script which will: 

1. Check for conflicts with existing other versions of dump1090
2. Check Build tools needed (git, make, gcc, pkgconf, binutils, and fakeroot), and will offer to install missing tools [Yes/no]. 
3. Offer to install dependencies rtl-sdr, lighttpd, and bladerf [Yes/no]
4. Build package `dump1090-fa-*.pkg.tar.xz` or `dump1090-fa-*.pkg.tar.zst`
5. Offer to install the above package [Yes/no]

The above package can be install later also by following command:
```
cd dump1090-fa-arch 
sudo pacman -U dump1090-fa-*.pkg.tar.*
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

*** ***

##  T H I N G S - TO -  DO (AFTER INSTALLATION IS COMPLETED)
  
*** ***

### IMPORTANT: REBOOT COMPUTER/RPi
**OTHERWISE DUMP1090-FA WILL FAIL TO START** </br>
**AND A ROTATING WHEEL WILL APPEARS ON THE MAP, OR MAP WILL NOT SHOW** </br></br>



To make SkyView Map show receiver location & range rings, do following: </br>

1. Open file "dump1090-fa" for editing  </br>
    `sudo nano  /etc/default/dump1090-fa`  </br>

2. In the opened file, go to following line:
    RECEIVER_OPTIONS="--device-index 0 --gain -10 --ppm 0"  </br>
    In above line, add your latitude and longitude, so the line becomes like below:  </br>
    RECEIVER_OPTIONS="--device-index 0 --gain -10 --lat xx.xxxx --lon yy.yyyy --ppm 0"  </br>
    NOTE: Repalce xx.xxxx and yy.yyyy by your actual latitude and Longitude  </br>

3. Restart dump1090-fa </br>

    `sudo systemctl restart dump1090-fa `  </br>

4. Clear browser cache and reload browser </br></br>
