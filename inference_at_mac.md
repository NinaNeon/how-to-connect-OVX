

🍎 在 MacBook (M1) 上做 Inference 完整流程

⸻

第一步：安裝 Python 環境

打開 Terminal：

### 建議用 Homebrew 安裝 python 3.10+

```bash
brew install python@3.10
```
### 建一個新的虛擬環境（避免污染系統環境）

```bash
python3 -m venv myenv
source myenv/bin/activate
```

✅ 之後所有指令都在這個虛擬環境 myenv 裡操作。

⸻

第二步：安裝適合 M1 的 Torch 和 Diffusers
### 確認還在 myenv
### 強制用 myenv 的 pip 安裝 torch


```bash
source ~/myenv/bin/activate

/Users/nina/myenv/bin/pip install diffusers transformers
/Users/nina/myenv/bin/pip install torch torchvision torchaudio

cd ~/Documents/cat
python inference.py

```
✅ 注意這裡不用特別裝 cuda，因為 M1 不支援 cuda，用 MPS 就可以！

⸻

第三步：把你的模型搬過來
	•	把你剛剛訓練好的模型資料夾（裡面有 model_index.json、unet/、vae/ 等）
	•	放到一個乾淨的路徑，例如：

~/Documents/my-trained-sd-model/
⸻

第四步：寫一個推理腳本（inference.py）

建立一個 inference.py，內容如下：
```bash
from diffusers import StableDiffusionPipeline
import torch

pipe = StableDiffusionPipeline.from_pretrained(
    "/Users/nina/Documents/cat",   # 🔥 這裡改成你的模型根目錄！
    torch_dtype=torch.float16,
    safety_checker=None,  # 如果沒有安全檢查器可以關掉
)

device = "mps" if torch.backends.mps.is_available() else "cpu"
pipe = pipe.to(device)
prompt = "a photo of crack on the wall"
with torch.autocast(device):
    image = pipe(prompt).images[0]
image.save("output.png")
```

✅ 注意這邊：
	•	device = "mps" ➔ 讓推理在 Apple GPU 上跑！
	•	torch.autocast(device) ➔ 自動使用 float16加速！

⸻

第五步：執行推理！
```bash
cd ~/Documents/cat
python inference.py
```
成功的話，會在你當前資料夾下產生一張 output.png 圖片！

—

✨ 小提醒（M1特有的狀況）

狀況	說明
第一次推理會比較慢	因為 MPS 會 compile kernel
記憶體吃得還行（8G~12G）	你的 16G RAM夠用，安心
不要期待跟 A100 一樣快	但比單純CPU要快很多（3～5倍速度提升）


下次開
```bash
cd ~/Documents/cat500
source ~/myenv/bin/activate
python inference_cat500.py
```
