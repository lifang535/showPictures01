https://github.com/karpathy/nanoGPT

------------------------------------------------------------------------------------------------------------------------
## 1. install

安装库：
```
pip install torch numpy transformers datasets tiktoken wandb tqdm
```
------------------------------------------------------------------------------------------------------------------------
## 2. quick start

下载莎士比亚作品数据集，并转化为整数流，得到 rain.bin 和 val.bin 文件：
```
python data/shakespeare_char/prepare.py
```
用 config/train_shakespeare_char.py 配置文件提供的设置来快速地训练一个小型的 GPT 模型：
```
python train.py config/train_shakespeare_char.py
```
根据配置，模型的检查点会被写入 –out_dir 目录 out-shakespeare-char。所以当训练结束后，用采样脚本指向这个目录来从最好的模型中采样：
```
python sample.py --out_dir=out-shakespeare-char
```
[ -> nanoGPT_1.png ]

Q: 在 reproducing GPT-2 时执行 
```
python data/openwebtext/prepare.py
```
下载数据集时到 28% 就会中断报错
```
    raise DatasetGenerationError("An error occurred while generating the dataset") from e
datasets.builder.DatasetGenerationError: An error occurred while generating the dataset
```
[ -> error_1.png ]

S: ?

Q: 在 finetuning 时执行 
```
python train.py config/finetune_shakespeare.py
```
进行微调时报错
```
torch.cuda.OutOfMemoryError: CUDA out of memory. Tried to allocate 20.00 MiB (GPU 0; 11.76 GiB total capacity; 9.03 GiB already allocated; 17.25 MiB free; 9.22 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF
```

S: ?

------------------------------------------------------------------------------------------------------------------------
## 3. sampling / inference

用 nanoGPT 做推理实验：

```
python sample.py \
    --init_from=gpt2-xl \
    --start="What is the answer to life, the universe, and everything?" \
    --num_samples=5 --max_new_tokens=100
```

[-> nanoGPT_2.png ]

------------------------------------------------------------------------------------------------------------------------
