
久々のRasPiとして本体3a+, Osoyooの3.5インチディスプレイを買った。
デスクトップUIは使わないので64bit lite trixie をインストール。
と、ここでOsoyooのドライバーはX11前提らしい。
https://osoyoo.com/ja/2026/01/29/rpi3-osoyoo-3-5-spi-screen-trixie-bookworm-system-complete-configuration-guide/

でもなんとか動かそうとしてみる。

SPI 有効化：
$ sudo raspi-config
Interface Options > SPI

$ sudo apt update

$ sudo apt install unzip -y

$ wget https://osoyoo.com/driver/osoyoo35b.zip

$ unzip osoyoo35b.zip

$ sudo cp osoyoo35b.dtbo /boot/firmware/overlays/

$ sudo cp /boot/firmware/config.txt /boot/firmware/config.txt.bak

$ sudo nano /boot/firmware/config.txt
コメントアウト
```
#dtoverlay=vc4-kms-v3d
#max_framebuffers=2
```

追加
```
# ========== Osoyoo 3.5 SPI Screen ==========
dtoverlay=osoyoo35b:speed=20000000
hdmi_force_hotplug=1
max_usb_current=1
hdmi_group=2
hdmi_mode=1
hdmi_mode=87
hdmi_cvt 480 320 60 6 0 0 0
hdmi_drive=2
display_rotate=2
```

SPI                 ON
VC4 KMS             OFF
Osoyoo overlay      ON
LCD解像度            480x320
LCD rotation        2
SPI speed           20MHz

