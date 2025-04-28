

🍎 在 MacBook (M1) 上做 Inference 完整流程

⸻

第一步：安裝 Python 環境

打開 Terminal：

# 建議用 Homebrew 安裝 python 3.10+
brew install python@3.10

# 建一個新的虛擬環境（避免污染系統環境）
python3 -m venv myenv
source myenv/bin/activate

✅ 之後所有指令都在這個虛擬環境 myenv 裡操作。

⸻

第二步：安裝適合 M1 的 Torch 和 Diffusers

# 先升級 pip
pip install --upgrade pip

# 安裝 MPS 版 PyTorch（官方支持 M1 的版本）
pip install torch torchvision torchaudio

# 安裝 diffusers 和其他推理需要的包
pip install diffusers transformers

✅ 注意這裡不用特別裝 cuda，因為 M1 不支援 cuda，用 MPS 就可以！

⸻

第三步：把你的模型搬過來
	•	把你剛剛訓練好的模型資料夾（裡面有 model_index.json、unet/、vae/ 等）
	•	放到一個乾淨的路徑，例如：

~/Documents/my-trained-sd-model/



⸻

第四步：寫一個推理腳本（inference.py）

建立一個 inference.py，內容如下：

from diffusers import StableDiffusionPipeline
import torch

# 載入模型
pipe = StableDiffusionPipeline.from_pretrained(
    "./Documents/my-trained-sd-model",   # 路徑換成你的實際路徑
    torch_dtype=torch.float16,
    safety_checker=None,  # 如果沒有安全檢查器可以關掉
)

# 移到 MPS （Apple GPU）
device = "mps" if torch.backends.mps.is_available() else "cpu"
pipe = pipe.to(device)

# 給一個 prompt
prompt = "一隻可愛的貓咪在月亮上，唯美風格"

# 生成圖片
with torch.autocast(device):
    image = pipe(prompt).images[0]

# 儲存圖片
image.save("output.png")

✅ 注意這邊：
	•	device = "mps" ➔ 讓推理在 Apple GPU 上跑！
	•	torch.autocast(device) ➔ 自動使用 float16加速！

⸻

第五步：執行推理！

python inference.py

成功的話，會在你當前資料夾下產生一張 output.png 圖片！

—

✨ 小提醒（M1特有的狀況）

狀況	說明
第一次推理會比較慢	因為 MPS 會 compile kernel
記憶體吃得還行（8G~12G）	你的 16G RAM夠用，安心
不要期待跟 A100 一樣快	但比單純CPU要快很多（3～5倍速度提升）

—

📋 最小版小結

「在 Apple M1 上，安裝MPS版torch和diffusers，使用mps設備推理，第一次會慢一點，之後會加速！」

—

✅ 這樣就能直接在你的 MacBook 上，把自己訓練的模型跑起來！
✅ 而且用到 Apple GPU，不用慢慢用 CPU！

—

要不要我直接幫你順便整理成一個【一鍵版 shell script】，
你只要複製貼上，就可以自動建環境＋安裝＋下載＋推理？🚀
要的話跟我說「要一鍵版」，我可以直接生給你！
