# Connect OP-1

This is a fork of https://github.com/xmacex/connect-opz. Replacing the functionality to connect to OPZ to OP1, instead. There are no major contribution to the original code except just replacing the device reference to OP1 (2367:0004).



# Connect OP-Z

Connect OP-Z as an audio device on norns.

This norns program has a single purpose, namely to connect monone
norns to teenage engineering OP-Z audio over USB for both input and
output.

I hope to improve my setup in the following regards:

1. Audio signal from OP-Z headphones to norns input is weak and loses in quality when driving OP-Z at full volume. USB audio has more *umph*
1. OP-Z reserves the audio in jack of norns shield.
1. Less is more.

WARNING: Do not disconnect or turn off the OP-Z when it has been
connected as an audio device with this program. This will leave
processes running wild on the norns, and will produce loud digital
noise.

https://llllllll.co/t/using-usb-audio-with-norns-case-op-z/

# Requirements

* norns
* teenage engineering OP-Z

# Purpose

The following storyline illustrates the ambition, and success of this
program.

Original setup in which I have monome norns shield running on a
Raspberry Pi 3+ powered by a battery pack. Etymōtic ER2XR headphones
are connected to norns output, and OP-Z is connected both with a USB
cable for MIDI and with an audio cable for audio from OP-Z to norns.

![](doc/original-setup-greyscale.jpg)

In a simplified setup the USB cable which I'll use anyway also
transport audio both ways, removing the audio cable from the setup and
also adding sound from norns to OP-Z.

![](doc/simplified-setup-greyscale.jpg)

An extended setup, now that the norns audio input is free for using
with a PO-28 Robot, PO-16 Factory or smartphone running YouTube,
SoundCloud, browser, Spotify, software synths like nanoloop and
Caustic, messaging apps etc. fun sound sources.

![](doc/extended-setup-greyscale.jpg)

# Function

The way this program works is that is runs `alsa_in` and `alsa_out`
for the connected OP-Z, and routes them *softcut* and *crone* in
jack. This manipulates the audio stack under norns, which remains
ignorant of these changes.

Enabling input from OP-Z to norns and output from norns to OP-Z are
controlled separately.

# Further ideas

It would make sense to do this at system level rather than a norns
program. This would be done by adding *udev* rule in
`/etc/udev/rules.d` plus writing a program which starts `alsa_in` and
`alsa_out` when the OP-Z is plugged in and adds the jack routes, and
tears this setup down when the OP-Z is disconnected from USB.

Another idea would be to amend the norns *systemd* service norns-jackd
which is defined in file `/etc/systemd/system/norns-jack.service`.

It might be worth looking at alternatives to `alsa_in` and `alsa_out`,
Jack 2 might have something for this.

Last idea would be to get a hardware mixer, rather then user norns as
my mixer.
