fix bug of ServerlessLLM 0.8.0

# Installation

python env

```bash
conda create -p ./conda-env-sllm 'python<3.11' 
conda activate ./conda-env-sllm
```

vllm

```bash
pip install vllm==0.9.0.1
```

serverless-llm-store

```bash
git clone git@github.com:YitaoYuan/ServerlessLLM.git
cd ServerlessLLM
git checkout v0.8.0-bugfix
cd ./sllm_store
pip install .
```

patching

```bash
cd ..
./sllm_store/vllm_patch/patch.sh
```

# Usage

## save

```bash
# TP=2
sllm-store save --model Qwen/Qwen2.5-1.5B-Instruct-tp2 --backend vllm --local-model-path /models/preset/Qwen/Qwen2.5-1.5B-Instruct/v1.0/ --tensor-parallel-size 2
```

## load

In terminal1, start daemon:
```bash
cd ServerlessLLM
sllm-store start --storage-path $PWD/models --mem-pool-size 10GB
```

In terminal2, load by:
```bash
cd ServerlessLLM
# TP=2
sllm-store load --model Qwen/Qwen2.5-1.5B-Instruct-tp2 --backend vllm --tensor-parallel-size 2
```