Configuring Linux 4.x or higher
----------

While the drivers for the HiFiBerry boards are already included in the Raspberry Pi Linux kernel. However, to activate them, additional configurations called device tree overlays are needed. You might also need to disable the onboard sound and add an ALSA configuration as some applications will require it.

### Remove the driver for the onboard sound ###

Remove the line

`dtparam=audio=on`

from /boot/config.txt if it exists.

If your system uses the vc4-fkms-v3d overlay, make sure, audio is also disabled on this:

`dtoverlay=vc4-fkms-v3d,audio=off`

Newer system will probably use the vc4-kms-v3d (without the “f”), the syntax is a bit different:

`dtoverlay=vc4-kms-v3d,noaudio`

### Configure device tree overlay file ###

With the Pi5, some overlays had to be adapted. If you’re using a DAC+ Standard, DAC+ Pro, DAC2 Pro, DAC+ ADC please see the changes here: [Changes in HifiBerry drivers](https://www.hifiberry.com/blog/changes-in-hifiberry-drivers/)

You don’t have to edit /etc/modules anymore, but need to load the correct device tree file. To do this, you must edit /boot/config.txt and add the following line

#### DAC for Raspberry Pi 1/DAC+ Light/DAC Zero/MiniAmp/Beocreate/DAC+ DSP/DAC+ RTC ####

`dtoverlay=hifiberry-dac`

#### DAC+ Standard/Amp2/Amp4 ####

Kernel \< 6.1.77

`dtoverlay=hifiberry-dacplus`

Kernel \>= 6.1.77

`dtoverlay=hifiberry-dacplus-std`

#### DAC+ Pro/DAC2 Pro: ####

Kernel \< 6.1.77

`dtoverlay=hifiberry-dacplus`

Kernel \>= 6.1.77

`dtoverlay=hifiberry-dacplus-pro`

#### DAC2 HD ####

`dtoverlay=hifiberry-dacplushd`

#### DAC+ ADC ####

`dtoverlay=hifiberry-dacplusadc`

#### DAC+ ADC Pro ####

`dtoverlay=hifiberry-dacplusadcpro`

#### Digi+ ####

`dtoverlay=hifiberry-digi`

#### Digi+ Pro ####

`dtoverlay=hifiberry-digi-pro`

#### Amp+ (not Amp2!) ####

`dtoverlay=hifiberry-amp`

#### Amp3 ####

`dtoverlay=hifiberry-amp3`

#### Amp4 Pro ####

`dtoverlay=hifiberry-amp4pro`

###  ###

### Linux 5.4 and higher ###

Linux 5.4 has changed some internal structures that make it incompatible with device-tree overlays of previous versions. Therefore, the hardware configuration that
is stored in the onboard EEPROM of some HiFiBerry cards (e.g. DAC+ Pro) might not load correctly. You can read more about this on [our blog](https://www.hifiberry.com/blog/configuration-changes-in-linux-5-4/).

If you have configured the correct overlay, but the system still doesn’t load the driver, this might be caused by these changes.

In this case, you need to disable the onboard EEPROM by adding

```
force_eeprom_read=0
```

to your config.txt file.

### Configure ALSA (optional) ###

Create /etc/asound.conf with the following content:

```
pcm.!default {
  type hw card 0
}
ctl.!default {
  type hw card 0
}
```

Make sure you have no .asound.conf file with different settings in your home directory (you might simply delete it if there is one). Reboot again now.

### Test it ###

Check, if the sound card is enabled with “aplay”:

`pi@raspberrypi ~ $ aplay -l
**** List of PLAYBACK Hardware Devices **** card 0: sndrpihifiberry [snd_rpi_hifiberry_dac], device 0: HifiBerry DAC HiFi pcm5102a-hifi-0 []
Subdevices: 1/1
Subdevice #0: subdevice #0 `

This should work as root but also with the default “pi” user of Raspbian. If you created another user, make sure it is part of the “audio” group, otherwise it won’t be able to access the sound card and aplay won’t list it.

You can use aplay, to playback a WAV file. Note that aplayer won’t convert files that are in a format that is not natively supported from our drivers. (e.g. mono files or different sample rates). For other file formats (MP3, FLAC, …) We recommend to use mplayer.

`sudo apt-get install mplayer`

Some users have reported problems with MP3 playback of mplayer. It seems, that the MP3 codec is not installed by default on all systems. We found the FLAC format to be best supported by mplayer.

Depending of the board you’re using it will show another HiFiBerry sound card (DAC,DAC+, Digi or Amp)

### Device not recognised? ###

This could be caused by typos in config.txt or blacklisted drivers. Add

`dtdebug=1`

to your config.txt. Have a look at the output of

`dmesg`

and the output of

`sudo vcdbg log msg`

##### Last updated: March 14, 2024 #####
