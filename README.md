# how-to-connect-OVX
how to connect OVX in Reinstalled Ubuntu

# 如何連接 OVX
在重新安裝的 Ubuntu 中如何連接 OVX

重新安裝系統  
首先，請用 Ventoy 製作一個 USB 啟動盤  
我的 Ubuntu 版本是 22.04.5  
開機進入桌面時，請持續按 "Delete"、"F2"“f12" 或 "Esc"  
接著我們會進入開機選單  please select boot device:
選擇 UEFI（你的 USB 名稱）  
這樣我們就會進入安裝流程  
請依照這部影片的步驟進行
【两分半钟完成VMware安装及Linux-Ubuntu安装（全程无废话）】 https://www.bilibili.com/video/BV1W34y1k7ge/?share_source=copy_web&vd_source=7aae493e7da36f090c4c02123b0dd11b
如果在虛擬機裏安裝也依照這個影片流程

in side we first install chrome
[
](https://www.google.com.tw/chrome/browser/desktop/index.html )
download chrome for linux
open terminal
cd ~/Downloads
sudo apt install ./google-chrome-stable_current_amd64.deb

google omniverse launcher
we would find this website:
[
](https://blog.csdn.net/AmbitiousTyj/article/details/139855388)
參考他
https://docs.omniverse.nvidia.com/install-guide/latest/workstation-install.html
the above is website 

sign up 
log in 
back to mail and press nv mail
keep press start developing botton we find 
![image](https://github.com/user-attachments/assets/fbd0e154-f986-409c-8664-c856e79f2ae9)
press omniverse launcher
![image](https://github.com/user-attachments/assets/54ba3355-38df-4093-9357-c0c4866e862d)
download omniverse launcher (not kit sdk)

after that open terminal
sudo apt update
sudo apt install libfuse2
cd ~/Downloads
chmod +x omniverse-launcher-linux.AppImage
./omniverse-launcher-linux.AppImage
