# Python 与 PyTorch 笔记

## 学习目标

- 能阅读和修改常见 Python 项目。
- 能用 pandas 完成基础数据处理。
- 能理解 PyTorch 中的数据、模型、损失、优化和评价流程。
- 能根据报错定位依赖、路径、形状和设备问题。

## Python 项目检查顺序

1. 阅读 `README.md`，确认运行入口和数据要求。
2. 查看 `requirements.txt`、`environment.yml` 或 `pyproject.toml`。
3. 建立独立环境，记录 Python 和关键依赖版本。
4. 找到入口脚本、配置文件和默认参数。
5. 先使用最小数据或默认配置运行，再逐步修改。

## PyTorch 训练循环骨架

```python
model.train()
for batch in dataloader:
    optimizer.zero_grad()
    predictions = model(batch)
    loss = criterion(predictions, batch["label"])
    loss.backward()
    optimizer.step()
```

阅读时需要确认：

- `batch` 中每个字段的含义和形状。
- 模型输入、输出和标签是否匹配。
- 损失函数为什么适合当前任务。
- 优化器、学习率、批大小和训练轮数。
- 训练与评价阶段是否正确切换 `train()` 和 `eval()`。

## 常用环境检查

```powershell
python --version
python -m pip list
python -c "import torch; print(torch.__version__)"
python -c "import torch; print(torch.cuda.is_available())"
```

## 待补充

- pandas 数据清洗与分组聚合示例。
- `Dataset`、`DataLoader` 和负采样。
- 张量形状追踪与常见维度错误。
- 推荐系统训练脚本的完整阅读记录。

