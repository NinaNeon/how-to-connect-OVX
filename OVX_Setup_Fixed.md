
# Ubuntu 22.04.5 安裝 OVX 環境教學（含 Linux 安裝、Chrome、Nucleus Launcher、OpenVPN、Farm 操作、Docker 傳送與 Task 提交）

## 步驟零：安裝 Ubuntu Linux 22.04.5

1. 前往 Ubuntu 官方網站下載 ISO 映像檔：
   https://releases.ubuntu.com/22.04/
![image](https://github.com/user-attachments/assets/14c8c420-4af0-4504-aacf-2afa7ac30548)
2. 將 ISO 檔燒錄到 USB：【Windows 和 Ubuntu 双系统的安装和卸载:制作Ubuntu安装盘】 【Windows11 安装 Ubuntu 避坑指南】 https://www.bilibili.com/video/BV1Cc41127B9/?p=4&share_source=copy_web&vd_source=7aae493e7da36f090c4c02123b0dd11b
![image](https://github.com/user-attachments/assets/c2091bdb-652b-48f5-adc9-d638a2da60a8)
使用ventoy燒錄

3. 使用 USB 開機並依畫面指示安裝 Ubuntu。

4. 安裝流程建議參考以下影片教學：
【两分半钟完成VMware安装及Linux-Ubuntu安装（全程无废话）】 https://www.bilibili.com/video/BV1W34y1k7ge/?share_source=copy_web&vd_source=7aae493e7da36f090c4c02123b0dd11b

![image](https://github.com/user-attachments/assets/86da96fc-7baf-46d7-8619-dad22b691722)

如上圖這樣就是好了

---

## 步驟一：安裝 Google Chrome

1. 打開 Terminal，貼上以下指令安裝 Chrome：

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb
```
![image](https://github.com/user-attachments/assets/38f974cf-4dd7-4a26-a7a2-741d1c0b2a2a)
也可以去網站[安裝Chrome官網：自動偵測您的作業系統](https://www.google.com.tw/chrome/browser/desktop/index.html )下載，打開 Terminal，貼上以下指令安裝 Chrome
```bash
cd ~/Downloads
sudo apt install ./google-chrome-stable_current_amd64.deb
```

2. 安裝完成後，可從應用程式搜尋 `Google Chrome` 並打開。

---

## 步驟二：安裝Nucleus Launcher
建議參考以下網站教學：
![image](https://github.com/user-attachments/assets/58629c13-b0f4-4243-b8d9-da6a8e20ff85)
[ NVIDIA Omniverse launcher下载](https://blog.csdn.net/AmbitiousTyj/article/details/139855388)

1. 開啟 Chrome，前往：[  Nucleus Launcher官網](https://www.nvidia.com/en-us/omniverse/)
![image](https://github.com/user-attachments/assets/34389b54-9582-440e-a8b6-f0961cf002a0)

2.點Start Developing

3.輸入帳號密碼

![image](https://github.com/user-attachments/assets/7d5c63d6-166a-4167-8587-d28f34959ef7)

4.可以在這個地方找到 Nucleus Launcher 別下載Kit SDK那個不對

![image](https://github.com/user-attachments/assets/f91a6ce5-a9e6-42eb-b3e9-c63ae164f59f)
![image](https://github.com/user-attachments/assets/c89aafad-7442-4e3e-83c9-e80569018985)
5. 點選下載 Nucleus Launcher for Linux。

6. 下載後如果缺少fuse會無法執行。

![image](https://github.com/user-attachments/assets/c968095d-d595-474b-b62c-7e1b57408e04)

打開 Terminal，貼上以下指令安裝fuse並執行.AppImage

```bash
sudo apt update
sudo apt install libfuse2
cd ~/Downloads
chmod +x omniverse-launcher-linux.AppImage
```
7. 第一次開啟時會要求登入（使用自己前面登過的帳號密碼）。

![image](https://github.com/user-attachments/assets/89fc235d-dff8-4f31-aecf-c4ca3797e424)

![image](https://github.com/user-attachments/assets/50cb2e49-1beb-4836-97bf-0d2fd313902e)

![image](https://github.com/user-attachments/assets/81fee6a0-4c69-42eb-9d63-2a64e6c927a4)

![image](https://github.com/user-attachments/assets/d2004051-9dd2-4ce2-9505-cdb101f65151)

8.先做其他步驟：打開 Terminal，貼上以下指令Clone j3soon/omni-farm-isaac且Install jq for JSON parsing

```bash
git clone https://github.com/j3soon/omni-farm-isaac.git
cd omni-farm-isaac

sudo apt-get update
sudo apt-get install -y jq

```


9.在omni-farm-isaac新建secret資料夾

![image](https://github.com/user-attachments/assets/4b2b1c2a-4ff6-4c98-8999-41bcf684a8fe)

放入從
![image](https://github.com/user-attachments/assets/7da73242-5d58-4a4b-aae9-149aa0818db9)

下載的env.sh和client.ovpn

![image](https://github.com/user-attachments/assets/9cb86f5e-7f15-4924-83b6-52eca62c6fee)

secrets/env.sh, for example:

![image](https://github.com/user-attachments/assets/3e6d7bb7-b708-4486-96aa-26ff6447f9d6)

10.打開 Terminal，貼上以下指令 執行這個 secrets/env.sh

```bash
cd omni-farm-isaac
source secrets/env.sh
```
## 步驟三：安裝OpenVPN 3 並連線


11.參考[script
](https://github.com/j3soon/omni-farm-isaac) 中的[  guide](https://openvpn.net/cloud-docs/tutorials/configuration-tutorials/connectors/operating-systems/linux/tutorial--learn-to-install-and-control-the-openvpn-3-client.html)安裝openvpn3，打開 Terminal，貼上以下指令

```bash
sudo snap install curl
sudo mkdir -p /etc/apt/keyrings && curl -fsSL https://packages.openvpn.net/packages-repo.gpg | sudo tee /etc/apt/keyrings/openvpn.asc
DISTRO=$(lsb_release -c -s)
echo "deb [signed-by=/etc/apt/keyrings/openvpn.asc] https://packages.openvpn.net/openvpn3/debian $DISTRO main" | sudo tee /etc/apt/sources.list.d/openvpn-packages.list
sudo apt update
sudo apt install openvpn3
```

12. 準備好你的 .ovpn 檔案，放在合適位置（secret)，我有改名變成client.ovpn

13. 匯入並啟用 VPN：

```bash
cd ~/omni-farm-isaac
source secrets/env.sh
scripts/vpn/install_config.sh client.ovpn
scripts/vpn/connect.sh
```


### 步驟四：開啟 Farm 操作頁面

14. 開啟 Chrome，輸入以下網址：
[  farm](http://farm.tpe1.local/queue/management/dashboard/)


```bash
http://farm.tpe1.local/queue/management/dashboard/
```
![image](https://github.com/user-attachments/assets/085361e5-d47e-4250-a8ef-f0e271a6fff1)

## 步驟五：登入Nucleus Launcher

15.connect to server 中填入伺服器地址

![image](https://github.com/user-attachments/assets/34ed8e74-157f-4bdb-9f69-efd7394c0ee6)

```bash
nucleus.tpe1.loacl
```

16. connect to server時會要求登入（使用公司提供帳號密碼）。密碼nvidia


![image](https://github.com/user-attachments/assets/91cd1ce5-3c77-4bd0-a100-6b97ccbcff44)

![image](https://github.com/user-attachments/assets/ab58f87d-c725-47d7-8c19-36fa2e53d063)
   

17. 登入後使用方式：在project資料夾內建立個人資料夾
   滑鼠右鍵可選「上傳」至伺服器。

![image](https://github.com/user-attachments/assets/ee35cfbc-cc47-4051-a4cd-eb27e61c14fa)

---
```bash
docker tag nina/defect-diffusion:latest ninaneon/defect-diffusion:latest
docker login
docker push ninaneon/defect-diffusion:latest
```

```bash
scripts/submit_task.sh diffusion-job "/run.sh \
  --download-src 'omniverse://nucleus.tpe1.local/Projects/alex' \
  --download-dest '/src/alex' \
  --upload-src '/src/alex/result' \
  --upload-dest 'omniverse://nucleus.tpe1.local/Projects/alex/result/1gpu_ep50' \
  'python3 -u /src/alex/train.py --pretrained_model_name_or_path /src/alex/models--CompVis--stable-diffusion-v1-4/snapshots/133a221b8aa7292a167afc5127cb63fb5005638b --data_files /src/alex/data.json --resolution 512 --train_batch_size 16 --gradient_accumulation_steps 8 --learning_rate 1e-7 --mixed_precision fp16 --num_train_epochs 50 --use_ema --image_column file_name --caption_column text --output_dir /src/alex/result'" \
"epoch50_1gpu"
```
