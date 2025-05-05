Last login: Mon May  5 14:29:44 on ttys015
nina@ninadeMacBook-Air ~ % cd /Users/nina/Documents/cat500/cat500_classifier
nina@ninadeMacBook-Air cat500_classifier % python3 train_cat500_fixed6.py
按下 Ctrl+C 將觸發信號處理器並保存當前模型狀態
使用設備: cpu
加載 VAE 模型...
Cannot initialize model with low cpu memory usage because `accelerate` was not found in the environment. Defaulting to `low_cpu_mem_usage=False`. It is strongly recommended to install `accelerate` for faster and less memory-intense model loading. You can do so with: 
```
pip install accelerate
```
.
加載 UNet 模型...
Cannot initialize model with low cpu memory usage because `accelerate` was not found in the environment. Defaulting to `low_cpu_mem_usage=False`. It is strongly recommended to install `accelerate` for faster and less memory-intense model loading. You can do so with: 
```
pip install accelerate
```
.
類別數量: 26
類別映射: {'blowhole': 0, 'break': 1, 'bump': 2, 'concavity': 3, 'crack': 4, 'crazing': 5, 'dent': 6, 'dirty spot': 7, 'edge defect': 8, 'fissure': 9, 'fray': 10, 'good': 11, 'horizontal defect': 12, 'inclusion': 13, 'missing head': 14, 'paint off': 15, 'particle': 16, 'patches': 17, 'pitted surface': 18, 'rolled': 19, 'scratch': 20, 'small defect': 21, 'stain': 22, 'uneven': 23, 'vertical': 24, 'void': 25}
未找到中斷模型，從頭開始訓練
開始訓練...
Epoch 1/10 | Batch 5/1376 | Loss: 3.1858 | Acc: 0.00%
Epoch 1/10 | Batch 10/1376 | Loss: 3.0640 | Acc: 5.00%
Epoch 1/10 | Batch 15/1376 | Loss: 2.7518 | Acc: 10.00%
Epoch 1/10 | Batch 20/1376 | Loss: 2.4466 | Acc: 17.50%
Epoch 1/10 | Batch 25/1376 | Loss: 2.3656 | Acc: 19.50%
Epoch 1/10 | Batch 30/1376 | Loss: 2.4844 | Acc: 20.00%
Epoch 1/10 | Batch 35/1376 | Loss: 2.4547 | Acc: 21.79%
Epoch 1/10 | Batch 40/1376 | Loss: 2.7371 | Acc: 22.81%

收到中斷信號，保存當前模型狀態...
模型已保存至 interrupted_defect_classifier.pth
正在退出...
nina@ninadeMacBook-Air cat500_classifier % 


nina@ninadeMacBook-Air cat500_classifier % python3 save_model_immediately.py
找到以下可能的進程 ID: [24058]
請輸入要發送 SIGINT 的進程 ID: 24058
已發送中斷信號到進程 24058
nina@ninadeMacBook-Air cat500_classifier % python3 inference_cat500.py --model_path interrupted_defect_classifier.pth --image_path "/Users/nina/Documents/0319/cat"
使用設備: cpu
加載模型: interrupted_defect_classifier.pth
Traceback (most recent call last):
  File "/Users/nina/Documents/cat500/cat500_classifier/inference_cat500.py", line 179, in <module>
    main()
  File "/Users/nina/Documents/cat500/cat500_classifier/inference_cat500.py", line 84, in main
    checkpoint = torch.load(args.model_path, map_location=device)
  File "/opt/homebrew/lib/python3.10/site-packages/torch/serialization.py", line 1524, in load
    raise pickle.UnpicklingError(_get_wo_message(str(e))) from None
_pickle.UnpicklingError: Weights only load failed. This file can still be loaded, to do so you have two options, do those steps only if you trust the source of the checkpoint. 
	(1) In PyTorch 2.6, we changed the default value of the `weights_only` argument in `torch.load` from `False` to `True`. Re-running `torch.load` with `weights_only` set to `False` will likely succeed, but it can result in arbitrary code execution. Do it only if you got the file from a trusted source.
	(2) Alternatively, to load with `weights_only=True` please check the recommended steps in the following error message.
	WeightsUnpickler error: Unsupported global: GLOBAL numpy.core.multiarray.scalar was not an allowed global by default. Please use `torch.serialization.add_safe_globals([numpy.core.multiarray.scalar])` or the `torch.serialization.safe_globals([numpy.core.multiarray.scalar])` context manager to allowlist this global if you trust this class/function.

Check the documentation of torch.load to learn more about types accepted by default with weights_only https://pytorch.org/docs/stable/generated/torch.load.html.

nina@ninadeMacBook-Air cat500_classifier % python inference_cat500_fixed.py --model_path interrupted_defect_classifier.pth --image_path "/Users/nina/Documents/0319/cat"
zsh: command not found: python
nina@ninadeMacBook-Air cat500_classifier % python3 inference_cat500_fixed.py --model_path interrupted_defect_classifier.pth --image_path "/Users/nina/Documents/0319/cat"
使用設備: cpu
嘗試加載模型: interrupted_defect_classifier.pth (方法1)
方法1失敗，嘗試方法2: Weights only load failed. This file can still be loaded, to do so you have two options, do those steps only if you trust the source of the checkpoint. 
	(1) In PyTorch 2.6, we changed the default value of the `weights_only` argument in `torch.load` from `False` to `True`. Re-running `torch.load` with `weights_only` set to `False` will likely succeed, but it can result in arbitrary code execution. Do it only if you got the file from a trusted source.
	(2) Alternatively, to load with `weights_only=True` please check the recommended steps in the following error message.
	WeightsUnpickler error: Unsupported global: GLOBAL numpy.dtype was not an allowed global by default. Please use `torch.serialization.add_safe_globals([numpy.dtype])` or the `torch.serialization.safe_globals([numpy.dtype])` context manager to allowlist this global if you trust this class/function.

Check the documentation of torch.load to learn more about types accepted by default with weights_only https://pytorch.org/docs/stable/generated/torch.load.html.
類別數量: 26
類別映射: {'blowhole': 0, 'break': 1, 'bump': 2, 'concavity': 3, 'crack': 4, 'crazing': 5, 'dent': 6, 'dirty spot': 7, 'edge defect': 8, 'fissure': 9, 'fray': 10, 'good': 11, 'horizontal defect': 12, 'inclusion': 13, 'missing head': 14, 'paint off': 15, 'particle': 16, 'patches': 17, 'pitted surface': 18, 'rolled': 19, 'scratch': 20, 'small defect': 21, 'stain': 22, 'uneven': 23, 'vertical': 24, 'void': 25}
加載 UNet 模型: /Users/nina/Documents/cat500/unet
Cannot initialize model with low cpu memory usage because `accelerate` was not found in the environment. Defaulting to `low_cpu_mem_usage=False`. It is strongly recommended to install `accelerate` for faster and less memory-intense model loading. You can do so with: 
```
pip install accelerate
```
.
加載 VAE 模型: /Users/nina/Documents/cat500/vae
Cannot initialize model with low cpu memory usage because `accelerate` was not found in the environment. Defaulting to `low_cpu_mem_usage=False`. It is strongly recommended to install `accelerate` for faster and less memory-intense model loading. You can do so with: 
```
pip install accelerate
```
.
找到 3 張圖像，開始處理...
處理圖像: /Users/nina/Documents/0319/cat/neudet4_oil_003拷貝.jpg
進度: 1/3 (33.3%)
處理圖像: /Users/nina/Documents/0319/cat/aircraft1_crack_122拷貝.jpg
進度: 2/3 (66.7%)
處理圖像: /Users/nina/Documents/0319/cat/aircraft1_missing_head_003拷貝.jpg
進度: 3/3 (100.0%)

所有圖像的預測結果:

檔案: neudet4_oil_003拷貝.jpg
預測類別: crack
置信度: 0.1972
前三可能類別:
  crack: 0.1972
  dent: 0.1463
  good: 0.1533

檔案: aircraft1_crack_122拷貝.jpg
預測類別: crack
置信度: 0.2985
前三可能類別:
  crack: 0.2985
  dent: 0.2169
  paint off: 0.0654

檔案: aircraft1_missing_head_003拷貝.jpg
預測類別: dent
置信度: 0.1829
前三可能類別:
  crack: 0.1648
  dent: 0.1829
  missing head: 0.0772
nina@ninadeMacBook-Air cat500_classifier % 
