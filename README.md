# MATRIX Hardware Abstraction Layer (HAL)

> [!NOTE]  
> 1) This fork doesn't seem to compile correctly anymore and I don't have access to MATRIX or RasPi hardware to debug this problem
> 2) The motivation for this fork was swapping out the WiringPi library for another RasPi GPIO library which was deprecated on newer versions of Raspbian. However, WiringPi has new maintainers now so maybe this fork is no longer useful...

[MATRIX Hardware Abstraction Layer (HAL)](https://matrix-io.github.io/matrix-documentation/matrix-hal/overview/) is an open source library for directly interfacing with the MATRIX Creator and MATRIX Voice. MATRIX HAL consists of driver files written in C++ which enable the user to write low level programs in C++.

This version of the library is patched to work with Ubuntu 22.04 and Raspbian Bullseye on the RasPi with the MATRIX Voice. 

WARNING: Not all features from the original library are available: the humidity sensor, IMU, pressure sensor and UV sensor have all been removed from the library. There is only the microphone array and everloop LED interface. The MATRIX Creator is not supported currently. 

## Install from Source

NOTE: This version of the library does NOT use the MATRIX kernel modules. If you install them, they will hide the spidev0.0 interface and prevent the library working. Please uninstall the MATRIX kernel modules before continuing.

# Configuring system

If you are on Ubuntu:
```
# increase SPI buffer size by
# appending boot parameter to cmdline.txt
sudo sed -i '$s/$/ spidev.bufsiz=12288/' /boot/firmware/cmdline.txt
```

If you are on Raspbian:
```
# enable SPI in the menu
sudo raspi-config

# increase SPI buffer size by
# appending boot parameter to cmdline.txt
sudo sed -i '$s/$/ spidev.bufsiz=12288/' /boot/cmdline.txt
```

...then for both, reboot.


# Install build prerequisites

```
sudo apt install cmake g++ git libfftw3-dev libgflags-dev 
```

Also requires [lgpio](http://abyz.me.uk/lg/lgpio.html). 
Please download and install from source.


# Build instructions

```
cd ~/
git clone https://github.com/gfwozniak/matrix-creator-hal.git
cd matrix-creator-hal
mkdir build
cd build
cmake ..
make -j4 && sudo make install
```

### Install locations

MATRIX HAL header files are installed in /usr/local/include/matrix_hal.

The compiled MATRIX HAL library file is installed in /usr/local/lib/libmatrix_creator_hal.so.


## Demos

Demos are included in the /demos directory. You can use the 
mic_energy_direct demo to test functionality of microphones.

```
# Should already be in ~/matrix-creator-hal/build
cd demos

# run the mic demo, gets brighter when picks up noise
./mic_energy_direct

# see the rest of the examples
ls -l
```

## References and Examples from MATRIX Website

[Function References](https://matrix-io.github.io/matrix-documentation/matrix-hal/reference/)
[Examples](https://matrix-io.github.io/matrix-documentation/matrix-hal/examples/)

## ChangeLog

There is a detailed changelog to describe why I made certain decisions.
