
步驟六：提交 Task 到 Farm


步驟七：如何上傳或使用自訂 Docker 映像

1. 若需自訂 Docker，可以先使用 Docker CLI login 登入內部 registry：



docker login registry.ovx.nvidia.com

2. 上傳自製 image（假設已建立）：



docker tag my_image:latest registry.ovx.nvidia.com/your_project/my_image:latest
docker push registry.ovx.nvidia.com/your_project/my_image:latest

3. 在 Farm 頁面建立 Job 時，選擇你推上去的 Docker image 使用即可。






---

## 步驟七：傳送 Docker 映像

1. 登入 Registry：

```bash
docker login registry.ovx.nvidia.com
```




4. 中斷連線：

```bash
openvpn3 session-manage --config config.ovpn --disconnect
```

5. 開機後手動連線 VPN：

```bash
openvpn3 session-start --config config.ovpn
```
