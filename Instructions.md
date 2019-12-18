# Building

## Goal

The main goal of the build is to be able to run the electron app in kiosk mode on the target raspberry pi that has Ubuntu installed on it.

## Prerequisits 

1. A Raspberry 3 device with Ubuntu Core
2. A windows machine with WSL enabled and Ubuntu installed. Note: You can also use any linux build, which should be very similar but I was working in Windows and thus the documentation being in Windows.

It also helps to have 3 command windows open at the same time.

## Steps

1. Switch to WSL from a command prompt by typing `bash` and install Snapcraft (the build tool for building snaps). While you won't be able to run your snaps on Windows, you should be able to do builds from here.
2. From the root of this repository, run `snapcraft`.
3. Wait for the build to finish. It can take a significant amount of time to build.
4. Once that is done, execute the following commands in normal windows terminal

```
scp electron-hello-world-kiosk_0.1_armhf.snap betsegaw-ta@192.168.86.26:~
```

5. From within the remoted in Raspberry PI, execute the following commands

```
snap install --dangerous ./electron-hello-world-kiosk_0.1_armhf.snap 
snap connect electron-hello-world-kiosk:browser-sandbox :browser-support
snap connect electron-hello-world-kiosk:x11-plug electron-hello-world-kiosk:x11
snap restart electron-hello-world-kiosk
```