
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