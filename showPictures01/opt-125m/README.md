https://github.com/facebookresearch/metaseq/blob/main/docs/faster-transformer.md

------------------------------------------------------------------------------------------------------------------------
## 1. Clone metaseq and download metaseq checkpoints

Q: 创建文件夹的时候有问题。例如直接创建时得到 `'checkpoints'`，而使用教程中的指令创建得到 `'ch'$'\n''eckpoints'`，但是显示在 vscode
和 mobaxterm 上显示的都是 `'checkpoints'`。造成文件系统管理混乱。

S: 全部使用教程中的指令直接在 `/home/lifang535` 工作文件夹下创建 `'metaseq'` 和 `'checkpoints'`，避免上述情况。

Q: `git clone` 失败。

S: 关闭重开网络代理，或者直接输入网址 download。

------------------------------------------------------------------------------------------------------------------------
## 2. Install FasterTransformer

Q: 输入路径时出现问题，报错信息显示需要绝对路径。

S: 全部改为绝对路径。

Q: 报错
```
nvidia-docker: command not found
```
S: 使用 `docker` 代替。

Q: 执行
```
docker run -tid --rm --shm-size 5g --name ft \
	-w "${HOME}" -e SRC_DIR="${SRC_DIR}" -e CKPT_DIR="${CKPT_DIR}" \
	-v "${SRC_DIR}:${SRC_DIR}" -v "${CKPT_DIR}:${CKPT_DIR}" \
	nvcr.io/nvidia/pytorch:23.05-py3 bash
```
后，`python ...` 和 `mpirun ...` 都无法执行。

S: 添加 `--gpus all`
```
docker run --gpus all -tid --rm --shm-size 5g --name ft \
	-w "${HOME}" -e SRC_DIR="${SRC_DIR}" -e CKPT_DIR="${CKPT_DIR}" \
	-v "${SRC_DIR}:${SRC_DIR}" -v "${CKPT_DIR}:${CKPT_DIR}" \
	nvcr.io/nvidia/pytorch:22.09-py3 bash
```
并将其中 `nvcr.io/nvidia/pytorch:23.05-py3` 改成 `nvcr.io/nvidia/pytorch:22.09-py3`。

Q: 中间操作失误在服务器 `'/'` 下创建了 `'lifang535'` 文件夹。

S: 没有权限无法删除误创建的文件夹。

------------------------------------------------------------------------------------------------------------------------
## 3. Convert metaseq checkpoints

Q: 无法执行教程中 `python ...`，报错找不到模型。

S: 将 python 部分指令中 `reshard-model_part-*.pt` 改为 `reshard-model_part-0.pt`。

------------------------------------------------------------------------------------------------------------------------
## 4. Run interactive script

Q: 执行
```
FT_PATH="lib/libth_transformer.so" 
```
后无法执行 `mpirun ...`，报错显示未设置环境变量。

S: 更改为 
```
export FT_PATH="/home/lifang535/FasterTransformer/build/lib/libth_transformer.so"。
```
-> opt-125m.png

------------------------------------------------------------------------------------------------------------------------
