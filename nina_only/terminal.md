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


# segmentation
＃segmentation

nina@ninadeMacBook-Air seg % python3 train_segmentation_fixed.py
按下 Ctrl+C 將觸發信號處理器並保存當前模型狀態
加載數據集: /Users/nina/Downloads/VisA_20220922/This_final_coco_all_absolute_paths_fixed.json
loading annotations into memory...
Done (t=0.01s)
creating index...
index created!
載入了 10821 張圖像
類別數量（含背景）: 87
類別映射: {1: 1, 2: 2, 3: 3, 4: 4, 5: 5, 6: 6, 7: 7, 8: 8, 9: 9, 10: 10, 11: 11, 12: 12, 13: 13, 14: 14, 15: 15, 16: 16, 17: 17, 18: 18, 19: 19, 20: 20, 21: 21, 22: 22, 23: 23, 24: 24, 25: 25, 26: 26, 27: 27, 28: 28, 29: 29, 30: 30, 31: 31, 32: 32, 33: 33, 34: 34, 35: 35, 36: 36, 37: 37, 38: 38, 39: 39, 40: 40, 41: 41, 42: 42, 43: 43, 44: 44, 45: 45, 46: 46, 47: 47, 48: 48, 49: 49, 50: 50, 51: 51, 52: 52, 53: 53, 54: 54, 55: 55, 56: 56, 57: 57, 58: 58, 59: 59, 60: 60, 61: 61, 62: 62, 63: 63, 64: 64, 65: 65, 66: 66, 67: 67, 68: 68, 69: 69, 70: 70, 71: 71, 72: 72, 73: 73, 74: 74, 75: 75, 76: 76, 77: 77, 78: 78, 79: 79, 80: 80, 81: 81, 82: 82, 83: 83, 84: 84, 85: 85, 86: 86}
驗證圖像路徑...
原始圖像數量: 10821
有效圖像數量: 10716
無效路徑數量: 105
前5個無效路徑示例: ['/Users/nina/Downloads/VisA_20220922/pcb3/Data/Images/Normal/500.JPG', '/Users/nina/Downloads/VisA_20220922/pcb3/Data/Images/Normal/501.JPG', '/Users/nina/Downloads/VisA_20220922/pcb3/Data/Images/Normal/502.JPG', '/Users/nina/Downloads/VisA_20220922/pcb3/Data/Images/Normal/503.JPG', '/Users/nina/Downloads/VisA_20220922/pcb3/Data/Images/Normal/504.JPG']
類別數量: 87
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
從錯誤恢復模型繼續訓練，從 epoch 0 開始，最佳損失: inf
開始訓練...
Epoch 1/20 | Batch 5/2679 | Loss: 4.7569
Epoch 1/20 | Batch 10/2679 | Loss: 4.6977
Epoch 1/20 | Batch 15/2679 | Loss: 4.6472
Epoch 1/20 | Batch 20/2679 | Loss: 4.6009
Epoch 1/20 | Batch 25/2679 | Loss: 4.5588
Epoch 1/20 | Batch 30/2679 | Loss: 4.5201
Epoch 1/20 | Batch 35/2679 | Loss: 4.4840
Epoch 1/20 | Batch 40/2679 | Loss: 4.4497
Epoch 1/20 | Batch 45/2679 | Loss: 4.4161
Epoch 1/20 | Batch 50/2679 | Loss: 4.3843
Epoch 1/20 | Batch 55/2679 | Loss: 4.3537
Epoch 1/20 | Batch 60/2679 | Loss: 4.3239
Epoch 1/20 | Batch 65/2679 | Loss: 4.2942
Epoch 1/20 | Batch 70/2679 | Loss: 4.2678
Epoch 1/20 | Batch 75/2679 | Loss: 4.2848
Epoch 1/20 | Batch 80/2679 | Loss: 4.2105
Epoch 1/20 | Batch 85/2679 | Loss: 4.1833
Epoch 1/20 | Batch 90/2679 | Loss: 4.1563
Epoch 1/20 | Batch 95/2679 | Loss: 4.1315
Epoch 1/20 | Batch 100/2679 | Loss: 4.1033
Epoch 1/20 | Batch 105/2679 | Loss: 4.0769
Epoch 1/20 | Batch 110/2679 | Loss: 4.0504
Epoch 1/20 | Batch 115/2679 | Loss: 4.0246
Epoch 1/20 | Batch 120/2679 | Loss: 3.9986
Epoch 1/20 | Batch 125/2679 | Loss: 3.9728
Epoch 1/20 | Batch 130/2679 | Loss: 3.9472
Epoch 1/20 | Batch 135/2679 | Loss: 3.9212
Epoch 1/20 | Batch 140/2679 | Loss: 3.8968
Epoch 1/20 | Batch 145/2679 | Loss: 3.8700
Epoch 1/20 | Batch 150/2679 | Loss: 3.8457
Epoch 1/20 | Batch 155/2679 | Loss: 3.8189
Epoch 1/20 | Batch 160/2679 | Loss: 3.7952
Epoch 1/20 | Batch 165/2679 | Loss: 3.7675
Epoch 1/20 | Batch 170/2679 | Loss: 3.7416
Epoch 1/20 | Batch 175/2679 | Loss: 3.7161
Epoch 1/20 | Batch 180/2679 | Loss: 3.6906
Epoch 1/20 | Batch 185/2679 | Loss: 3.6649
Epoch 1/20 | Batch 190/2679 | Loss: 3.6390

收到中斷信號，保存當前模型狀態...
模型已保存至 interrupted_segmentation_model.pth
正在退出...
nina@ninadeMacBook-Air seg % 

nina@ninadeMacBook-Air seg % python3 inference_segmentation.py --image_path "/Users/nina/Documents/cat500/image.jpg" --overlay --model_path "/Users/nina/Documents/cat500/cat500_classifier/seg/segmentation_output/interrupted_segmentation_model.pth"
使用設備: cpu
加載COCO數據: /Users/nina/Downloads/VisA_20220922/This_final_coco_all_absolute_paths_fixed.json
loading annotations into memory...
Done (t=0.01s)
creating index...
index created!
加載了 87 個類別（包括背景）
類別映射: {1: '406', 2: '407', 3: '408', 4: '409', 5: '410', 6: '411', 7: '412', 8: '413', 9: '414', 10: '415', 11: '416', 12: '417', 13: '418', 14: '419', 15: '420', 16: '421', 17: '422', 18: '423', 19: '424', 20: '425', 21: '426', 22: '427', 23: '428', 24: '429', 25: '430', 26: '431', 27: '432', 28: '433', 29: '434', 30: '435', 31: '436', 32: '437', 33: '438', 34: '439', 35: '440', 36: '441', 37: '442', 38: '443', 39: '444', 40: '445', 41: '446', 42: '447', 43: '448', 44: '449', 45: '450', 46: '451', 47: '452', 48: '453', 49: '454', 50: '455', 51: '456', 52: '457', 53: '458', 54: '459', 55: '460', 56: '461', 57: '462', 58: '463', 59: '464', 60: '465', 61: '466', 62: '467', 63: '468', 64: '469', 65: '470', 66: '471', 67: '472', 68: '473', 69: '502', 70: '526', 71: '527', 72: '528', 73: '529', 74: '530', 75: '531', 76: '532', 77: '533', 78: '534', 79: '535', 80: '536', 81: '537', 82: '538', 83: '539', 84: '540', 85: '541', 86: '542'}
加載模型: /Users/nina/Documents/cat500/cat500_classifier/seg/segmentation_output/interrupted_segmentation_model.pth
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
成功加載模型權重
處理圖像: /Users/nina/Documents/cat500/image.jpg
/Users/nina/Documents/cat500/cat500_classifier/seg/inference_segmentation.py:370: UserWarning: Glyph 21407 (\N{CJK UNIFIED IDEOGRAPH-539F}) missing from font(s) DejaVu Sans.
  plt.savefig(os.path.join(args.output_dir, f"{base_name}_result.png"))
/Users/nina/Documents/cat500/cat500_classifier/seg/inference_segmentation.py:370: UserWarning: Glyph 22987 (\N{CJK UNIFIED IDEOGRAPH-59CB}) missing from font(s) DejaVu Sans.
  plt.savefig(os.path.join(args.output_dir, f"{base_name}_result.png"))
/Users/nina/Documents/cat500/cat500_classifier/seg/inference_segmentation.py:370: UserWarning: Glyph 22294 (\N{CJK UNIFIED IDEOGRAPH-5716}) missing from font(s) DejaVu Sans.
  plt.savefig(os.path.join(args.output_dir, f"{base_name}_result.png"))
/Users/nina/Documents/cat500/cat500_classifier/seg/inference_segmentation.py:370: UserWarning: Glyph 20687 (\N{CJK UNIFIED IDEOGRAPH-50CF}) missing from font(s) DejaVu Sans.
  plt.savefig(os.path.join(args.output_dir, f"{base_name}_result.png"))
/Users/nina/Documents/cat500/cat500_classifier/seg/inference_segmentation.py:370: UserWarning: Glyph 20998 (\N{CJK UNIFIED IDEOGRAPH-5206}) missing from font(s) DejaVu Sans.
  plt.savefig(os.path.join(args.output_dir, f"{base_name}_result.png"))
/Users/nina/Documents/cat500/cat500_classifier/seg/inference_segmentation.py:370: UserWarning: Glyph 21106 (\N{CJK UNIFIED IDEOGRAPH-5272}) missing from font(s) DejaVu Sans.
  plt.savefig(os.path.join(args.output_dir, f"{base_name}_result.png"))
/Users/nina/Documents/cat500/cat500_classifier/seg/inference_segmentation.py:370: UserWarning: Glyph 32080 (\N{CJK UNIFIED IDEOGRAPH-7D50}) missing from font(s) DejaVu Sans.
  plt.savefig(os.path.join(args.output_dir, f"{base_name}_result.png"))
/Users/nina/Documents/cat500/cat500_classifier/seg/inference_segmentation.py:370: UserWarning: Glyph 26524 (\N{CJK UNIFIED IDEOGRAPH-679C}) missing from font(s) DejaVu Sans.
  plt.savefig(os.path.join(args.output_dir, f"{base_name}_result.png"))
/Users/nina/Documents/cat500/cat500_classifier/seg/inference_segmentation.py:370: UserWarning: Glyph 30090 (\N{CJK UNIFIED IDEOGRAPH-758A}) missing from font(s) DejaVu Sans.
  plt.savefig(os.path.join(args.output_dir, f"{base_name}_result.png"))
/Users/nina/Documents/cat500/cat500_classifier/seg/inference_segmentation.py:370: UserWarning: Glyph 21152 (\N{CJK UNIFIED IDEOGRAPH-52A0}) missing from font(s) DejaVu Sans.
  plt.savefig(os.path.join(args.output_dir, f"{base_name}_result.png"))

檢測到的類別:

結果已保存至 segmentation_results 目錄
nina@ninadeMacBook-Air seg % 
