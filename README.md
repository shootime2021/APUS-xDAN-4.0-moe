
<div align="center">
  <img src="https://github.com/shootime2021/APUS-xDAN-4.0-moe/assets/75604726/d32dd5e3-b901-49c7-aa35-067d6df91bce" width="500px"/>
  
  # APUS-xDAN-4.0(MoE)

  A Trillion-Parameter MOE Architecture Model Outperforms Grok1, Compatible with 4090 Graphics Card

  <a href="#-performance">📊Performance </a> •
  <a href="#-resources">✨Resources </a> •
  <a href="#-model-architecture">📖Architecture </a> •
  <a href="#-model-weights">📂Weights </a> •
  <a href="#-install"> 🔨 Install </a> •
  <a href="#-inference">🚀Inference </a> •
  <a href="#-acknowledgement">🤝 Acknowledgement </a>

  <br />
  <br />

  English | [简体中文](README_zh-CN.md)

</div>


> [!Important]
> <div align="center">
> <b>
> 📢 Welcome to the First High-Performance Trillion-Parameter MOE Architecture LLM trained jointly by xDAN and APUS. 📢
> </b>
> <br>
> <b>
> 🤗 This a high-performance MOE model whose Math(GSM8k_Cot:79%), Reasoning(MMLU:75%)</a>!
> </b>
> <br>
> <b>
> 🙏 Feel free to use according to the  inference code.
> </b>
> </div>


## News 

- 🙌 04-03 Model link released! [https://huggingface.co/xDAN-AI/APUS-xDAN-4.0-MOE]
- 🙌 04-01 APUS-xDAN-4.0(MOE) The model files link will be released soon. Stay tuned for more details!
- 🙌 03-31 APUS-xDAN-4.0(MOE) Open Source Model, quantized on  "IQ-Quantized Tech" in  1.5-bit, 2-bit, and 4-bit, optimized to run on consumer-grade 4090 graphics cards.

  


# 📊 Performance

## Comparison with Other Models

- Alignment By [xDAN-APUS4.0]([https://huggingface.co/xDAN-AI/APUS-xDAN-4.0-MOE)

> Performances generated from different evaluation toolkits are different due to the prompts, settings and implementation details.



| BenchMark        | Mode | APUS-xDAN-4.0(MoE) | Mixtral-8x7B(MoE) |  Llama2-70B | Grok-1（MoE） |
|-----------------|------|-----------------|--------------|-------------|-------------------|
| Total Params   |  GEN   |      136B         |     48B      |     70B     |       314B         |
| Active Params   |  GEN   |      60B         |     12B      |     70B     |       78.5B         |
| MMLU            | PPL  | **73.1**            | 71.3         | 69.7        | 73.0             |
| BIG-Bench-Hard  | GEN  | 66.4            | 67.1         | 64.9        | 71.7              | 
| GSM-8K          | GEN  | **78.2**         | 65.7         | 63.4        | 62.9              |
| MATH            | GEN  | **29.5**         | 22.7         | 12.0        | 23.9              | 

# ✨ Resources
| Model       | Quantized | Size   | Context     | Hardware Requirement     |
|-------------|-----------|--------|--------------------------| --------------------------|
| APUS-xDAN4.0-MoE-0402.Q2_K.gguf       | Q2_K        | 39G  | 32k | 2x24G GPU memory |
| APUS-xDAN4.0-MoE-0402.IQ3_XXS.gguf      | IQ3_XXS        | 41G | 32k | 2x24G GPU memory |
| APUS-xDAN4.0-MoE-0402.Q3_K_M_Matrix.gguf      | Q3_K_M        | 51G | 32k | 2x24G GPU memory |
| APUS-xDAN4.0-MoE-0402.Q4_K_M.gguf | Q4_K_M       | 64G  | 32k | 3x24G GPU memory |


## Deployment
- [x] [Inference with llama.cpp](https://github.com/ggerganov/llama.cpp)
- [x] [Inference with vLLM](https://github.com/vllm-project/vllm)

# 📖 Model Architecture

>  The APUS-xDAN-4.0(MoE) model is mainly composed of 32 identical MoEtransformer blocks. The main difference between the MoEtransformer block and the ordinary transformer block is that the FFN layer is replaced by the **MoE FFN** layer. In the MoE FFN layer, the tensor first goes through a gate layer to calculate the scores of each expert, and then selects the top-k experts from the 8 experts based on the expert scores. The tensor is aggregated through the outputs of the top-k experts, thereby obtaining the final output of the MoE FFN layer. Each expert consists of 3 linear layers. It is worth noting that all Norm Layers of APUS-xDAN4.0 MoE also use RMSNorm, which is the same as LLama. In the attention layer, the QKV matrix in the APUS-xDAN4.0 MoE has a Q matrix shape of (4096,4096) and K and V matrix shapes of (4096,1024).

We plot the architecture as the following:

<div align="center">
  <img src="https://github.com/shootime2021/APUS-xDAN-4.0-moe/assets/75604726/5c86b15a-5858-48bd-a6b3-62d1c326b6f4" width="800px"/>
</div>

# 📂 Model Weights

## Hugging Face Format

- [Download Model](https://huggingface.co/xDAN-AI/APUS-xDAN-4.0-MOE)

## Raw Format

You can download the checkpoints by magnet or Hugging Face

### Download via HF

- [APUS-xDAN-4.0-MOE](https://huggingface.co/xDAN-AI/APUS-xDAN-4.0-MOE)

> If you are unable to access Hugging Face, please try [hf-mirror](https://huggingface.co/xDAN-AI/APUS-xDAN-4.0-MOE)


```bash
# Download the Hugging Face
git lfs install
git clone https://huggingface.co/xDAN-AI/APUS-xDAN-4.0-MOE
# Merge Files(Only for HF)
cd APUS-xDAN-4.0-MOE/



# 🚀 Inference

## Text Completion 
```bash
./main -m APUS-xDAN4.0-MoE-0402.Q2_K.gguf   --n-gpu-layers 99 \
--prompt "You are a helpful assistant named APUS-xDAN4.0 MoE. " --chatml \
--interactive \
--temp 0.7 \
--ctx-size 4096
```


# 🖊️ Citation


```latex
@misc{2023opencompass,
    title={xDAN-APUS4.0: High Performance Alignment Model Trainer.},
    author={xDAN-APUS4.0 Contributors},
    howpublished = {\url{https://github.com/shootime2021/APUS-xDAN-4.0-moe}},
    year={2024}
}
```
