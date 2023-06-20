https://github.com/karpathy/nanoGPT

------------------------------------------------------------------------------------------------------------------------
1. install
安装库：
$ pip install torch numpy transformers datasets tiktoken wandb tqdm

------------------------------------------------------------------------------------------------------------------------
2. quick start
下载莎士比亚作品数据集，并转化为整数流，得到 rain.bin 和 val.bin 文件：
$ python data/shakespeare_char/prepare.py
用 config/train_shakespeare_char.py 配置文件提供的设置来快速地训练一个小型的 GPT 模型：
$ python train.py config/train_shakespeare_char.py
根据配置，模型的检查点会被写入 –out_dir 目录 out-shakespeare-char。所以当训练结束后，用采样脚本指向这个目录来从最好的模型中采样：
$ python sample.py --out_dir=out-shakespeare-char
-> nanoGPT_1.png

------------------------------------------------------------------------------------------------------------------------
3. sampling / inference
用 nanoGPT 做推理实验
$ python sample.py \
    --init_from=gpt2-xl \
    --start="What is the answer to life, the universe, and everything?" \
    --num_samples=5 --max_new_tokens=100
-> nanoGPT_2.png

------------------------------------------------------------------------------------------------------------------------
