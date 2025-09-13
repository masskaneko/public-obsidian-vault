# 日本語入力
WSLのObsidianから日本語入力したかった。

```
sudo apt install -y fcitx-bin fcitx-mozc dbus-x11
sudo apt -y install fonts-noto-cjk fonts-ipafont fonts-takao
```

.profile
```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
export DefaultIMModule=fcitx
fcitx-autostart &> /dev/null
```

/etc/fonts/local.conf
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
<dir>/mnt/c/Windows/Fonts</dir>
</fontconfig>
```



https://www.aise.ics.saitama-u.ac.jp/~gotoh/GeditInUbuntuonWSL2InWin11.html

https://wp.beken.miyakonojo-nct.ac.jp/2024/08/12/wsl%E3%81%AEubuntu-22-04-lts%E3%81%AEgui%E3%81%AE%E6%97%A5%E6%9C%AC%E8%AA%9E%E5%85%A5%E5%8A%9B/

