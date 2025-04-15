
# Ubuntu 22.04.5 安裝 OVX 環境教學（含 Linux 安裝、Chrome、Nucleus Launcher、OpenVPN、Farm 操作、Docker 傳送與 Task 提交）

## 步驟零：安裝 Ubuntu Linux 22.04.5

1. 前往 Ubuntu 官方網站下載 ISO 映像檔：
   https://releases.ubuntu.com/22.04/
![image](https://github.com/user-attachments/assets/14c8c420-4af0-4504-aacf-2afa7ac30548)
2. 將 ISO 檔燒錄到 USB：【Windows 和 Ubuntu 双系统的安装和卸载:制作Ubuntu安装盘】 【Windows11 安装 Ubuntu 避坑指南】 https://www.bilibili.com/video/BV1Cc41127B9/?p=4&share_source=copy_web&vd_source=7aae493e7da36f090c4c02123b0dd11b
![image](https://github.com/user-attachments/assets/c2091bdb-652b-48f5-adc9-d638a2da60a8)
使用ventoy燒錄

4. 使用 USB 開機並依畫面指示安裝 Ubuntu。

5. 安裝流程建議參考以下影片教學：
【两分半钟完成VMware安装及Linux-Ubuntu安装（全程无废话）】 https://www.bilibili.com/video/BV1W34y1k7ge/?share_source=copy_web&vd_source=7aae493e7da36f090c4c02123b0dd11b

![image](https://github.com/user-attachments/assets/86da96fc-7baf-46d7-8619-dad22b691722)
---

## 步驟一：安裝 Google Chrome

1. 打開 Terminal，貼上以下指令安裝 Chrome：

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb
```
![image](https://github.com/user-attachments/assets/38f974cf-4dd7-4a26-a7a2-741d1c0b2a2a)
也可以去網站[ ](https://www.google.com.tw/chrome/browser/desktop/index.html )安裝
```bash
cd ~/Downloads
sudo apt install ./google-chrome-stable_current_amd64.deb
```

2. 安裝完成後，可從應用程式搜尋 `Google Chrome` 並打開。

---

## 步驟二：安裝並登入 Nucleus Launcher

1. 開啟 Chrome，前往：
   https://www.nvidia.com/en-us/omniverse/download/

2. 點選下載 Nucleus Launcher for Linux。

3. 下載後解壓縮並執行。

4. 詳細步驟參考官方教學文件：
   https://docs.omniverse.nvidia.com/launcher/latest/install-guide-linux.html

5. 第一次開啟時會要求登入（使用公司提供帳號密碼）。

6. 登入後使用方式：
   檔案總管中選檔案，滑鼠右鍵可選「上傳」至伺服器。

![nucleus-launcher-login](https://example.com/images/nucleus-launcher-login.png)

---

## 步驟三：開啟 Farm 操作頁面

1. 開啟 Chrome，輸入以下網址：
   https://farm.ovx.nvidia.com

> 提醒：建議將此網址加入書籤。

![farm-home](https://example.com/images/farm-home.png)

---

## 步驟四：安裝 OpenVPN 3 並連線

1. 在 Terminal 中貼上以下指令安裝 OpenVPN 3：

```bash
sudo apt update
sudo apt install openvpn3
```

2. 準備好你的 .ovpn 檔案，放在合適位置（例如 ~/Downloads/config.ovpn）

3. 匯入並啟用 VPN：

```bash
openvpn3 config-import --config ~/Downloads/config.ovpn --persistent
openvpn3 session-start --config config.ovpn
```

4. 中斷連線：

```bash
openvpn3 session-manage --config config.ovpn --disconnect
```

5. 開機後手動連線 VPN：

```bash
openvpn3 session-start --config config.ovpn
```

![vpn-connected](https://example.com/images/vpn-connected.png)

---

## 步驟五：啟動 Omniverse Launcher（Terminal）

```bash
~/omniverse-launcher/launch.sh
```

> 若安裝於其他位置，請依實際路徑修正。

![launcher-start](https://example.com/images/launcher-start.png)

---

## 步驟六：提交 Task 到 Farm

1. 登入 Farm 後選擇你的 Workspace。

2. 點選「Submit Task」或「Create Job」。

3. 選擇對應的 Docker 映像（內建或自定義）。

4. 設定參數後按下 Submit。

![submit-task](https://example.com/images/submit-task.png)

---

## 步驟七：傳送 Docker 映像

1. 登入 Registry：

```bash
docker login registry.ovx.nvidia.com
```

2. 標記與上傳你的映像：

```bash
docker tag my_image:latest registry.ovx.nvidia.com/your_project/my_image:latest
docker push registry.ovx.nvidia.com/your_project/my_image:latest
```

3. 在 Farm 建立任務時選你上傳的映像即可。

![upload-docker](https://example.com/images/upload-docker.png)

---

## 步驟八：查看任務結果與輸出

1. 提交後到 Tasks 頁面觀察狀態。

2. 成功會顯示綠色，點進去可看 log 與輸出檔案。

![task-result](https://example.com/images/task-result.png)

---

## 附註與錯誤排解

- 權限問題：加 `sudo`。
- 套件錯誤修正：

```bash
sudo apt --fix-broken install
```

- 錯誤訊息不懂可複製給助教或 ChatGPT 協助。
