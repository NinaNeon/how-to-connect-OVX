Ubuntu 22.04.5 安裝 OVX 環境教學（含 Linux 安裝、Chrome、Nucleus Launcher、OpenVPN、Farm 操作、Docker 傳送與 Task 提交）

步驟零：安裝 Ubuntu Linux 22.04.5

1. 前往 Ubuntu 官方網站下載 ISO 映像檔：

https://releases.ubuntu.com/22.04/



2. 將 ISO 檔燒錄到 USB：

可使用 Rufus（Windows）或 balenaEtcher（Linux/macOS）進行燒錄。



3. 使用 USB 開機並依畫面指示安裝 Ubuntu。


4. 安裝流程建議參考以下影片教學：



https://www.youtube.com/watch?v=F5U6zLrP_bw




---

步驟一：安裝 Google Chrome

1. 打開 Terminal，貼上以下指令安裝 Chrome：



wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb

2. 安裝完成後，可從應用程式搜尋 Google Chrome 並打開。






---

步驟二：安裝並登入 Nucleus Launcher

1. 開啟 Chrome，前往 https://www.nvidia.com/en-us/omniverse/download/。


2. 點選下載 Nucleus Launcher for Linux。


3. 下載後解壓縮並執行。


4. 安裝過程與使用方式建議參考以下教學文章：



https://docs.omniverse.nvidia.com/launcher/latest/install-guide-linux.html

5. 第一次開啟時會要求登入。

使用公司提供的帳號密碼登入。



6. 登入後，使用方式：

在檔案總管中選取檔案，滑鼠右鍵可選擇「上傳」至伺服器。







---

步驟三：開啟 Farm 操作頁面

1. 開啟 Chrome，輸入以下網址即可打開 Farm 頁面：



https://farm.ovx.nvidia.com

> 提醒：建議將此網址加入書籤，方便以後快速開啟。






---

步驟四：安裝 OpenVPN 3 並連線

1. 在 Terminal 中貼上以下指令安裝 OpenVPN 3：



sudo apt update
sudo apt install openvpn3

2. 將 .ovpn 檔案準備好，放在你知道的位置，例如 ~/Downloads/config.ovpn


3. 匯入並啟用 VPN：



openvpn3 config-import --config ~/Downloads/config.ovpn --persistent
openvpn3 session-start --config config.ovpn

4. 若要中斷 VPN：



openvpn3 session-manage --config config.ovpn --disconnect

5. 每次開機後要連線 VPN：

開啟 Terminal 貼上：




openvpn3 session-start --config config.ovpn




---

步驟五：啟動 Omniverse Launcher（從 Terminal 執行）

若你已安裝 Omniverse Launcher，可用 Terminal 啟動：

~/omniverse-launcher/launch.sh

（請依實際安裝路徑調整）




---

步驟六：提交 Task 到 Farm

1. 登入 Farm 網頁後，選擇你的專案 Workspace。


2. 點選「Submit Task」或「Create Job」。


3. 選擇預設的 Docker 映像（例如 Isaac Sim Container 或你自己上傳的 Docker）。


4. 設定輸入參數，例如任務類型、路徑、檔案名稱等。


5. 點選「Submit」，等待任務被排程處理。






---

步驟七：如何上傳或使用自訂 Docker 映像

1. 若需自訂 Docker，可以先使用 Docker CLI login 登入內部 registry：



docker login registry.ovx.nvidia.com

2. 上傳自製 image（假設已建立）：



docker tag my_image:latest registry.ovx.nvidia.com/your_project/my_image:latest
docker push registry.ovx.nvidia.com/your_project/my_image:latest

3. 在 Farm 頁面建立 Job 時，選擇你推上去的 Docker image 使用即可。






---

任務結果與下載輸出

1. 提交成功後，你可以在「Task」頁面查看狀態。


2. 執行成功的任務會顯示綠色的狀態。


3. 點選任務後可看到 log、output 檔案等資訊，並下載。






---

附註與錯誤排解

有些作業需要特權才能執行，若遇到權限問題可在指令前加上 sudo。

若遇到缺少套件，可使用以下指令補裝：


sudo apt --fix-broken install

若 Terminal 有錯誤訊息但你不確定意思，可以將錯誤內容複製給助教或貼給 ChatGPT 協助判讀。



---

如需進一步協助，請聯絡你的助教或管理員。
