# Reference

## Vertical, Horizontal and Clock Frequencies.

### Decode your display's edid

1. Find the edid file of the display you want.
From the command line, run as root.
`find /sys -name edid`
In my case it displays.
```
/sys/devices/pci0000:00/0000:00:02.0/drm/card0/card0-HDMI-A-1/edid
/sys/devices/pci0000:00/0000:00:02.0/drm/card0/card0-VGA-1/edid
/sys/devices/pci0000:00/0000:00:02.0/drm/card0/card0-DP-1/edid
```
2. Use *edid-decode* to decode the edid and get what we need.
`edid-decode /sys/devices/pci0000:00/0000:00:02.0/drm/card0/card0-VGA-1/edid`
And in my  case, the result for this HP L1506 is.
```
EDID version: 1.3
Manufacturer: HWP Model 265b Serial Number 16843009
Made in week 33 of 2006
Analog display, Input voltage level: 0.7/0.7 V
Sync: Separate 
Maximum image size: 30 cm x 22 cm
Gamma: 2.40
DPMS levels: Standby Suspend Off
RGB color display
Default (sRGB) color space is primary color space
First detailed timing is preferred timing
Display x,y Chromaticity:
  Red:   0.6455, 0.3320
  Green: 0.3007, 0.5849
  Blue:  0.1435, 0.0781
  White: 0.3125, 0.3281
Established timings supported:
  720x400@70Hz 9:5 HorFreq: 31469 Hz Clock: 28.320 MHz
  640x480@60Hz 4:3 HorFreq: 31469 Hz Clock: 25.175 MHz
  640x480@72Hz 4:3 HorFreq: 37900 Hz Clock: 31.500 MHz
  640x480@75Hz 4:3 HorFreq: 37500 Hz Clock: 31.500 MHz
  800x600@60Hz 4:3 HorFreq: 37900 Hz Clock: 40.000 MHz
  800x600@72Hz 4:3 HorFreq: 48100 Hz Clock: 50.000 MHz
  800x600@75Hz 4:3 HorFreq: 46900 Hz Clock: 49.500 MHz
  832x624@75Hz 4:3 HorFreq: 49726 Hz Clock: 57.284 MHz
  1024x768@60Hz 4:3 HorFreq: 48400 Hz Clock: 65.000 MHz
  1024x768@70Hz 4:3 HorFreq: 56500 Hz Clock: 75.000 MHz
  1024x768@75Hz 4:3 HorFreq: 60000 Hz Clock: 78.750 MHz
Standard timings supported:
Detailed mode: Clock 65.000 MHz, 300 mm x 220 mm
               1024 1048 1184 1344 hborder 0
                768  771  777  806 vborder 0
               -hsync -vsync 
               VertFreq: 60 Hz, HorFreq: 48363 Hz
Monitor ranges (GTF): 50-76Hz V, 30-63kHz H, max dotclock 80MHz
Monitor name: HP L1506
Serial number: CNC633RBRF
Checksum: 0x7f (valid)
```

## Generate the Modelines

### videogen
I recommend *videogen* to generate modlines.

#### videogen syntaxe
videogen -m=DesiredxResolution -mdc=HighestPixel/DotClock -mhf=HorintalSync -mvf=VerticalRate -dvf=DesiredFrequency

`videogen -nfb -nnv -m=1152x900 -mdc=105.561 -mhf=71.71 -mvf=76.05 -dvf=60`

Will give the modeline:
`Modeline "1152x900" 83.64 1152 1192 1240 1472 900 902 904 947  # 84 MHz, 56.8 kHz, 60.0 Hz`

## xrandr

1. Create new mode. `xrandr --newmode "1152x900" 83.64 1152 1192 1240 1472 900 902 904 947  # 84 MHz, 56.8 kHz, 60.0 Hz`
2. Add new mode to list of resolutions. `xrandr --addmode VGA-1 "1152x900"`