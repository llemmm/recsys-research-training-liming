# 2026-07-16学习记录

1.使用路线：
Windows 本机 PowerShell -> conda activate lesson03 -> E:\研究生科研培训\lesson03\sasrec_smoke_demo -> 设置 CUDA_VISIBLE_DEVICES=0 -> 使用本机 NVIDIA GeForce RTX 3060 Laptop GPU（cuda:0）运行 sasrec_demo.py -> 输出保存至 outputs\run_时间戳\。
本次为本机 GPU 验证，未使用实验室服务器连接；记录中未包含密码、SSH 私钥、NAS 凭证或 Token。

2.Conda环境、Python和PyTorch版本等环境
运行平台：Windows 本机 GPU（RTX 3060 Laptop GPU，6 GB）
Conda 环境：lesson03
Python：3.10.20
PyTorch：2.12.1+cu126
CUDA runtime：12.6
设备：cuda:0

3.GPU型号和CUDA检查结果
(lesson03) PS E:\研究生科研培训\lesson03\sasrec_smoke_demo> nvidia-smi --query-gpu=name,driver_version,memory.total --format=csv,noheader
NVIDIA GeForce RTX 3060 Laptop GPU, 592.27, 6144 MiB
(lesson03) PS E:\研究生科研培训\lesson03\sasrec_smoke_demo> python sasrec_demo.py --device cuda --check-only
D:\py\envs\lesson03\lib\site-packages\torch\_subclasses\functional_tensor.py:362: UserWarning: Failed to initialize NumPy: No module named 'numpy' (Triggered internally at C:\actions-runner\_work\pytorch\pytorch\torch\csrc\utils\tensor_numpy.cpp:84.)
  cpu = _conversion_method_template(device=torch.device("cpu"))
{
  "python": "3.10.20",
  "pytorch": "2.12.1+cu126",
  "pytorch_cuda_runtime": "12.6",
  "cuda_available": true,
  "selected_device": "cuda:0",
  "gpu_name": "NVIDIA GeForce RTX 3060 Laptop GPU",
  "gpu_total_memory_mib": 6144,
  "visible_cuda_devices": 1,
  "allocator_limit_mib": 700,
  "allocator_fraction": 0.11394156425490355,
  "nvidia_smi_process_memory_mib": null
}
说明：Windows WDDM 模式下 nvidia-smi 无法返回按 PID 的显存，故记录 PyTorch allocated/reserved 显存。

4.SASRec运行命令、日志和输出位置
运行命令：(lesson03) PS E:\研究生科研培训\lesson03\sasrec_smoke_demo> python sasrec_demo.py `
>>   --device cuda `
>>   --epochs 10 `
>>   --batch-size 32 `
>>   --max-len 20 `
>>   --hidden-size 64 `
>>   --num-heads 2 `
>>   --num-blocks 2 `
>>   --allocator-limit-mib 700 `
>>   --gpu-budget-mib 1024
输出目录：outputs\run_20260716_001356
输出日志：D:\py\envs\lesson03\lib\site-packages\torch\_subclasses\functional_tensor.py:362: UserWarning: Failed to initialize NumPy: No module named 'numpy' (Triggered internally at C:\actions-runner\_work\pytorch\pytorch\torch\csrc\utils\tensor_numpy.cpp:84.)
  cpu = _conversion_method_template(device=torch.device("cpu"))
2026-07-16 00:13:57 | INFO | Environment: {"python": "3.10.20", "pytorch": "2.12.1+cu126", "pytorch_cuda_runtime": "12.6", "cuda_available": true, "selected_device": "cuda:0", "gpu_name": "NVIDIA GeForce RTX 3060 Laptop GPU", "gpu_total_memory_mib": 6144, "visible_cuda_devices": 1}
2026-07-16 00:13:57 | INFO | Data: users=128, items=120, interactions=3072
2026-07-16 00:13:57 | INFO | Model parameters: 59648
2026-07-16 00:13:58 | INFO | GPU memory [model initialized]: process=unavailable, torch_allocated=0.2 MiB, torch_reserved=2.0 MiB
2026-07-16 00:13:58 | INFO | GPU memory [epoch 1]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:13:58 | INFO | Epoch 01 | loss=1.3830 | valid HR@10=0.2578 | valid NDCG@10=0.1180
2026-07-16 00:13:58 | INFO | GPU memory [epoch 2]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:13:58 | INFO | Epoch 02 | loss=1.3470 | valid HR@10=0.4141 | valid NDCG@10=0.2423
2026-07-16 00:13:58 | INFO | GPU memory [epoch 3]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:13:58 | INFO | Epoch 03 | loss=1.3115 | valid HR@10=0.5547 | valid NDCG@10=0.3524
2026-07-16 00:13:58 | INFO | GPU memory [epoch 4]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:13:58 | INFO | Epoch 04 | loss=1.2670 | valid HR@10=0.6328 | valid NDCG@10=0.4510
2026-07-16 00:13:58 | INFO | GPU memory [epoch 5]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:13:58 | INFO | Epoch 05 | loss=1.2198 | valid HR@10=0.7031 | valid NDCG@10=0.4965
2026-07-16 00:13:59 | INFO | GPU memory [epoch 6]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:13:59 | INFO | Epoch 06 | loss=1.1691 | valid HR@10=0.7422 | valid NDCG@10=0.5273
2026-07-16 00:13:59 | INFO | GPU memory [epoch 7]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:13:59 | INFO | Epoch 07 | loss=1.1251 | valid HR@10=0.7578 | valid NDCG@10=0.5669
2026-07-16 00:13:59 | INFO | GPU memory [epoch 8]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:13:59 | INFO | Epoch 08 | loss=1.0786 | valid HR@10=0.7656 | valid NDCG@10=0.5916
2026-07-16 00:13:59 | INFO | GPU memory [epoch 9]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:13:59 | INFO | Epoch 09 | loss=1.0367 | valid HR@10=0.7891 | valid NDCG@10=0.6147
2026-07-16 00:13:59 | INFO | GPU memory [epoch 10]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:13:59 | INFO | Epoch 10 | loss=0.9981 | valid HR@10=0.8047 | valid NDCG@10=0.6363
2026-07-16 00:13:59 | INFO | GPU memory [final evaluation]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:13:59 | INFO | Best epoch 10 | test HR@10=0.8672 | test NDCG@10=0.6620
2026-07-16 00:13:59 | INFO | Outputs: E:\研究生科研培训\lesson03\sasrec_smoke_demo\outputs\run_20260716_001356 
最佳 epoch：10
测试集：HR@10 = 0.8672，NDCG@10 = 0.6620
显存：PyTorch allocated/reserved 峰值为 22.1/28.0 MiB；


5.进行两次基础调参实验（固定 batch-size=32、max-len=20、hidden-size=64、num-heads=2、num-blocks=2、epochs=10，仅比较学习率）

实验 A：learning-rate=0.0005
运行命令：(lesson03) PS E:\研究生科研培训\lesson03\sasrec_smoke_demo> python sasrec_demo.py --device cuda --epochs 10 --batch-size 32 --max-len 20 --hidden-size 64 --num-heads 2 --num-blocks 2 --learning-rate 0.0005 --allocator-limit-mib 700 --gpu-budget-mib 1024 --output-root outputs\tuning_lr_0005
输出目录：outputs\tuning_lr_0005\run_20260716_002037
环境：Python 3.10.20；PyTorch 2.12.1+cu126；CUDA runtime 12.6；设备 cuda:0；GPU NVIDIA GeForce RTX 3060 Laptop GPU（6144 MiB）。
模型参数量：59648
输出日志：D:\py\envs\lesson03\lib\site-packages\torch\_subclasses\functional_tensor.py:362: UserWarning: Failed to initialize NumPy: No module named 'numpy' (Triggered internally at C:\actions-runner\_work\pytorch\pytorch\torch\csrc\utils\tensor_numpy.cpp:84.)
  cpu = _conversion_method_template(device=torch.device("cpu"))
2026-07-16 00:20:37 | INFO | Environment: {"python": "3.10.20", "pytorch": "2.12.1+cu126", "pytorch_cuda_runtime": "12.6", "cuda_available": true, "selected_device": "cuda:0", "gpu_name": "NVIDIA GeForce RTX 3060 Laptop GPU", "gpu_total_memory_mib": 6144, "visible_cuda_devices": 1}
2026-07-16 00:20:37 | INFO | Data: users=128, items=120, interactions=3072
2026-07-16 00:20:37 | INFO | Model parameters: 59648
2026-07-16 00:20:38 | INFO | GPU memory [model initialized]: process=unavailable, torch_allocated=0.2 MiB, torch_reserved=2.0 MiB
2026-07-16 00:20:38 | INFO | GPU memory [epoch 1]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:20:38 | INFO | Epoch 01 | loss=1.3868 | valid HR@10=0.1875 | valid NDCG@10=0.0738
2026-07-16 00:20:38 | INFO | GPU memory [epoch 2]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:20:38 | INFO | Epoch 02 | loss=1.3687 | valid HR@10=0.2578 | valid NDCG@10=0.1102
2026-07-16 00:20:38 | INFO | GPU memory [epoch 3]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:20:38 | INFO | Epoch 03 | loss=1.3535 | valid HR@10=0.3438 | valid NDCG@10=0.1734
2026-07-16 00:20:38 | INFO | GPU memory [epoch 4]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:20:38 | INFO | Epoch 04 | loss=1.3356 | valid HR@10=0.4297 | valid NDCG@10=0.2358
2026-07-16 00:20:38 | INFO | GPU memory [epoch 5]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:20:38 | INFO | Epoch 05 | loss=1.3119 | valid HR@10=0.5312 | valid NDCG@10=0.3256
2026-07-16 00:20:39 | INFO | GPU memory [epoch 6]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:20:39 | INFO | Epoch 06 | loss=1.2874 | valid HR@10=0.5703 | valid NDCG@10=0.3654
2026-07-16 00:20:39 | INFO | GPU memory [epoch 7]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:20:39 | INFO | Epoch 07 | loss=1.2679 | valid HR@10=0.6172 | valid NDCG@10=0.4289
2026-07-16 00:20:39 | INFO | GPU memory [epoch 8]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:20:39 | INFO | Epoch 08 | loss=1.2412 | valid HR@10=0.6719 | valid NDCG@10=0.4646
2026-07-16 00:20:39 | INFO | GPU memory [epoch 9]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:20:39 | INFO | Epoch 09 | loss=1.2165 | valid HR@10=0.6953 | valid NDCG@10=0.4736
2026-07-16 00:20:39 | INFO | GPU memory [epoch 10]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:20:39 | INFO | Epoch 10 | loss=1.1908 | valid HR@10=0.7344 | valid NDCG@10=0.4989
2026-07-16 00:20:39 | INFO | GPU memory [final evaluation]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:20:39 | INFO | Best epoch 10 | test HR@10=0.7266 | test NDCG@10=0.5120
2026-07-16 00:20:39 | INFO | Outputs: outputs\tuning_lr_0005\run_20260716_002037
显存：模型初始化 torch_allocated/reserved=0.2/2.0 MiB；训练与最终评估 torch_allocated/reserved=22.1/28.0 MiB。

实验 B：learning-rate=0.002
运行命令：(lesson03) PS E:\研究生科研培训\lesson03\sasrec_smoke_demo> python sasrec_demo.py --device cuda --epochs 10 --batch-size 32 --max-len 20 --hidden-size 64 --num-heads 2 --num-blocks 2 --learning-rate 0.002 --allocator-limit-mib 700 --gpu-budget-mib 1024 --output-root outputs\tuning_lr_0002
输出目录：outputs\tuning_lr_0002\run_20260716_002111
环境：Python 3.10.20；PyTorch 2.12.1+cu126；CUDA runtime 12.6；设备 cuda:0；GPU NVIDIA GeForce RTX 3060 Laptop GPU（6144 MiB）。
模型参数量：59648
输出日志：D:\py\envs\lesson03\lib\site-packages\torch\_subclasses\functional_tensor.py:362: UserWarning: Failed to initialize NumPy: No module named 'numpy' (Triggered internally at C:\actions-runner\_work\pytorch\pytorch\torch\csrc\utils\tensor_numpy.cpp:84.)
  cpu = _conversion_method_template(device=torch.device("cpu"))
2026-07-16 00:21:11 | INFO | Environment: {"python": "3.10.20", "pytorch": "2.12.1+cu126", "pytorch_cuda_runtime": "12.6", "cuda_available": true, "selected_device": "cuda:0", "gpu_name": "NVIDIA GeForce RTX 3060 Laptop GPU", "gpu_total_memory_mib": 6144, "visible_cuda_devices": 1}
2026-07-16 00:21:11 | INFO | Data: users=128, items=120, interactions=3072
2026-07-16 00:21:11 | INFO | Model parameters: 59648
2026-07-16 00:21:12 | INFO | GPU memory [model initialized]: process=unavailable, torch_allocated=0.2 MiB, torch_reserved=2.0 MiB
2026-07-16 00:21:13 | INFO | GPU memory [epoch 1]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:21:13 | INFO | Epoch 01 | loss=1.3757 | valid HR@10=0.4062 | valid NDCG@10=0.2222
2026-07-16 00:21:13 | INFO | GPU memory [epoch 2]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:21:13 | INFO | Epoch 02 | loss=1.3038 | valid HR@10=0.6016 | valid NDCG@10=0.4169
2026-07-16 00:21:13 | INFO | GPU memory [epoch 3]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:21:13 | INFO | Epoch 03 | loss=1.2189 | valid HR@10=0.6875 | valid NDCG@10=0.5070
2026-07-16 00:21:13 | INFO | GPU memory [epoch 4]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:21:13 | INFO | Epoch 04 | loss=1.1296 | valid HR@10=0.7891 | valid NDCG@10=0.5959
2026-07-16 00:21:13 | INFO | GPU memory [epoch 5]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:21:13 | INFO | Epoch 05 | loss=1.0471 | valid HR@10=0.7891 | valid NDCG@10=0.6220
2026-07-16 00:21:13 | INFO | GPU memory [epoch 6]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:21:13 | INFO | Epoch 06 | loss=0.9720 | valid HR@10=0.8281 | valid NDCG@10=0.6549
2026-07-16 00:21:13 | INFO | GPU memory [epoch 7]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:21:13 | INFO | Epoch 07 | loss=0.9091 | valid HR@10=0.8281 | valid NDCG@10=0.6785
2026-07-16 00:21:14 | INFO | GPU memory [epoch 8]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:21:14 | INFO | Epoch 08 | loss=0.8540 | valid HR@10=0.8359 | valid NDCG@10=0.6793
2026-07-16 00:21:14 | INFO | GPU memory [epoch 9]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:21:14 | INFO | Epoch 09 | loss=0.8073 | valid HR@10=0.8359 | valid NDCG@10=0.6792
2026-07-16 00:21:14 | INFO | GPU memory [epoch 10]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:21:14 | INFO | Epoch 10 | loss=0.7647 | valid HR@10=0.8359 | valid NDCG@10=0.6940
2026-07-16 00:21:14 | INFO | GPU memory [final evaluation]: process=unavailable, torch_allocated=22.1 MiB, torch_reserved=28.0 MiB
2026-07-16 00:21:14 | INFO | Best epoch 10 | test HR@10=0.8750 | test NDCG@10=0.6923
2026-07-16 00:21:14 | INFO | Outputs: outputs\tuning_lr_0002\run_20260716_002111
显存：模型初始化 torch_allocated/reserved=0.2/2.0 MiB；训练与最终评估 torch_allocated/reserved=22.1/28.0 MiB。

调参结论：基线学习率 0.001 的验证集 NDCG@10 为 0.6363。学习率 0.0005 的验证集 NDCG@10 为 0.4989，表现较差；学习率 0.002 的验证集 NDCG@10 为 0.6940，为三组中最高。因此下一轮模型容量实验使用 learning-rate=0.002。


6.一个问题及排查过程：
首次安装报 OSError 28（C 盘临时目录空间不足），并将报错结果交由ai检查，得知是因为C 盘临时目录空间不足。
将 TEMP/TMP 临时目录设为 E:\pip-tmp，清除 pip 缓存后重试，安装成功。