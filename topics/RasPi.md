
## Gifアニメーションをディスプレイに表示する

チャット用Gifアニメーションを https://www.animatedemojis.com/ で入手。

gifファイルパスを指定して表示させる。

```python
from PIL import Image
import sys
import time

WIDTH = 480
HEIGHT = 320
FB = "/dev/fb1"


def image_to_rgb565(image):
    image = image.convert("RGB")
    pixels = image.load()

    data = bytearray(WIDTH * HEIGHT * 2)

    i = 0
    for y in range(HEIGHT):
        for x in range(WIDTH):
            r, g, b = pixels[x, y]

            value = ((r >> 3) << 11) | \
                    ((g >> 2) << 5) | \
                    (b >> 3)

            data[i] = value & 0xff
            data[i + 1] = value >> 8
            i += 2

    return data


def play_gif(filename):
    gif = Image.open(filename)

    print(f"GIF: {filename}")
    print(f"size: {gif.size}")
    print(f"frames: {getattr(gif, 'n_frames', 1)}")

    with open(FB, "wb") as fb:
        frame = 0

        while True:
            try:
                gif.seek(frame)
            except EOFError:
                frame = 0
                continue

            image = gif.convert("RGB")

            # LCDいっぱいに表示
            image = image.resize(
                (WIDTH, HEIGHT),
                Image.Resampling.LANCZOS
            )

            data = image_to_rgb565(image)

            start = time.monotonic()

            fb.seek(0)
            fb.write(data)
            fb.flush()

            elapsed = time.monotonic() - start

            delay_ms = gif.info.get("duration", 100)
            if delay_ms < 10:
                delay_ms = 10

            # 転送にかかった時間を考慮
            remaining = delay_ms / 1000 - elapsed
            if remaining > 0:
                time.sleep(remaining)

            frame += 1

            if frame >= getattr(gif, "n_frames", 1):
                frame = 0


if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(f"Usage: sudo python3 {sys.argv[0]} GIF")
        sys.exit(1)

    play_gif(sys.argv[1])
```


```bash
sudo python3 ~/lcd_gif.py gifs/question.gif
```

なかなか遅い。本来の1/10程度ではないか。

RGB565変換が遅いのを疑い確かめる。
```python
from PIL import Image
import time

WIDTH = 480
HEIGHT = 320

image = Image.new("RGB", (WIDTH, HEIGHT), "red")


def image_to_rgb565(image):
    image = image.convert("RGB")
    pixels = image.load()

    data = bytearray(WIDTH * HEIGHT * 2)

    i = 0
    for y in range(HEIGHT):
        for x in range(WIDTH):
            r, g, b = pixels[x, y]

            value = ((r >> 3) << 11) | \
                    ((g >> 2) << 5) | \
                    (b >> 3)

            data[i] = value & 0xff
            data[i + 1] = value >> 8
            i += 2

    return data


start = time.monotonic()

for _ in range(100):
    image_to_rgb565(image)

elapsed = time.monotonic() - start

print(f"100 conversions: {elapsed:.3f} sec")
print(f"conversion FPS: {100 / elapsed:.2f}")
PY
```

```bash
$ python3 ~/bench_convert.py
100 conversions: 49.325 sec
conversion FPS: 2.03
```

## 文字をディスプレイに表示する
```bash
$ sudo apt install fonts-noto-core fonts-noto-cjk
```

```python
from PIL import Image, ImageDraw, ImageFont

WIDTH = 480
HEIGHT = 320
FB = "/dev/fb1"

FONT = "/usr/share/fonts/truetype/noto/NotoSans-Regular.ttf"

def rgb888_to_rgb565(image):
    pixels = image.load()
    data = bytearray(WIDTH * HEIGHT * 2)

    i = 0
    for y in range(HEIGHT):
        for x in range(WIDTH):
            r, g, b = pixels[x, y]

            value = ((r >> 3) << 11) | \
                    ((g >> 2) << 5) | \
                    (b >> 3)

            data[i] = value & 0xff
            data[i + 1] = value >> 8
            i += 2

    return data


image = Image.new("RGB", (WIDTH, HEIGHT), "black")
draw = ImageDraw.Draw(image)

font = ImageFont.truetype(FONT, 100)

text = "HELLO!"

bbox = draw.textbbox((0, 0), text, font=font)
text_width = bbox[2] - bbox[0]
text_height = bbox[3] - bbox[1]

x = (WIDTH - text_width) // 2
y = (HEIGHT - text_height) // 2 - bbox[1]

draw.text(
    (x, y),
    text,
    font=font,
    fill="white"
)

with open(FB, "wb") as f:
    f.write(rgb888_to_rgb565(image))

print("done")
```


## 3a+ に Osoyoo 3.5 インチ SPI ディスプレイをつなげる
服や帽子にディスプレイをつけることを思いつき久々のRasPi。
本体は3a+、ディスプレイはSPI接続のOsoyoo3.5インチを選択。
この用途からしてスペックは過剰だろうけど、試作段階では融通が効きそうなので。
ImagerでOS、ssh、WiFi設定をしてmicroSDカードへ書き込み。
RasPiとPCをUSBケーブルでつなぎ電源を入れると、WiFiルーター上で接続デバイス数が1つ増えたので繋がったらしい。
PCからssh接続できるようになった。
デスクトップUIは使わないので64bit lite を選択。trixieというらしい。

```
$ cat /etc/os-release
PRETTY_NAME="Debian GNU/Linux 13 (trixie)"
NAME="Debian GNU/Linux"
VERSION_ID="13"
VERSION="13 (trixie)"
VERSION_CODENAME=trixie
DEBIAN_VERSION_FULL=13.7
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
```

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

sudo reboot の後にどうなったか確認。

```
$ ls -l /dev/fb* crw-rw---- 1 root video 29, 0 Sep 21 13:14 /dev/fb0 crw-rw---- 1 root video 29, 1 Sep 21 13:14 /dev/fb1

$ dmesg | grep -Ei 'spi|fb|ili9488|osoyoo' [ 0.000000] Kernel command line: coherent_pool=1M 8250.nr_uarts=0 snd_bcm2835.enable_headphones=0 cgroup_disable=memory snd_bcm2835.enable_headphones=1 snd_bcm2835.enable_hdmi=1 bcm2708_fb.fbwidth=480 bcm2708_fb.fbheight=320 bcm2708_fb.fbswap=1 vc_mem.mem_base=0x1ec00000 vc_mem.mem_size=0x20000000 console=ttyS0,115200 console=tty1 root=PARTUUID=4b89bdb3-02 rootfstype=ext4 fsck.repair=yes rootwait ds=nocloud;i=rpi-imager-1789958362299 cfg80211.ieee80211_regdom=JP [ 1.344683] bcm2708_fb soc:fb: FB found 1 display(s) [ 1.353935] bcm2708_fb soc:fb: Registered framebuffer for display 0, size 480x320 [ 4.440432] systemd[1]: Hostname set to <raspi3a>. [ 10.447465] ads7846 spi0.1: supply vcc not found, using dummy regulator [ 10.450524] ads7846 spi0.1: touchscreen, irq 184 [ 10.451415] input: ADS7846 Touchscreen as /devices/platform/soc/3f204000.spi/spi_master/spi0/spi0.1/input/input0 [ 10.463455] fbtft: module is from the staging directory, the quality is unknown, you have been warned. [ 10.622552] fb_ili9486: module is from the staging directory, the quality is unknown, you have been warned. [ 10.623171] SPI driver fb_ili9486 has no spi_device_id for ilitek,ili9486 [ 10.626035] fb_ili9486 spi0.0: fbtft_property_value: regwidth = 16 [ 10.626057] fb_ili9486 spi0.0: fbtft_property_value: buswidth = 8 [ 10.626066] fb_ili9486 spi0.0: fbtft_property_value: debug = 0 [ 10.626074] fb_ili9486 spi0.0: fbtft_property_value: rotate = 270 [ 10.626083] OF: /soc/spi@7e204000/osoyoo35b@0: Read of boolean property 'bgr' with a value. [ 10.626110] fb_ili9486 spi0.0: fbtft_property_value: fps = 30 [ 10.626119] fb_ili9486 spi0.0: fbtft_property_value: txbuflen = 32768 [ 11.132405] graphics fb1: fb_ili9486 frame buffer, 480x320, 300 KiB video memory, 32 KiB buffer memory, fps=31, spi0.0 at 20 MHz 

$ cat /proc/fb
0 BCM2708 FB
1 fb_ili9486
```


```
$ fbset -fb /dev/fb1

mode "480x320"
geometry 480 320 480 320 16
timings 0 0 0 0 0 0 0
nonstd 1
rgba 5/11,6/5,5/0,0/0
endmode

$ cat /sys/class/graphics/fb1/bits_per_pixel
16

$ cat /sys/class/graphics/fb1/virtual_size
480,320
```


- 解像度: **480 × 320**
- 色深度: **16bit**
- フォーマット: **RGB565**
- framebuffer: `/dev/fb1`

Python からフレームバッファーに書き込み画面全体を赤くする。
```python
import struct

WIDTH = 480
HEIGHT = 320
FB = "/dev/fb1"

def rgb565(r, g, b):
    return ((r >> 3) << 11) | ((g >> 2) << 5) | (b >> 3)

pixel = struct.pack("<H", rgb565(255, 0, 0))
frame = pixel * (WIDTH * HEIGHT)

with open(FB, "wb") as f:
    f.write(frame)

print("done")
```

画面全体が赤くなった。