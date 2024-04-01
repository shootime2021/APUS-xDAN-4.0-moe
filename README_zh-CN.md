<div align="center">
  <img src="https://github.com/shootime2021/APUS-xDAN-4.0-moe/assets/75604726/d32dd5e3-b901-49c7-aa35-067d6df91bce" width="500px"/>
APUS-xDAN-4.0(MoE)
一款万亿参数MoE架构模型，性能超越Grok1，兼容4090显卡
<div align="center">
<a href="#-performance">📊性能 </a> •
<a href="#-resources">✨资源 </a> •
<a href="#-model-architecture">📖架构 </a> •
<a href="#-model-weights">📂权重 </a> •
<a href="#-install"> 🔨 安装 </a> •
<a href="#-inference">🚀推理 </a> •
<a href="#-acknowledgement">🤝 致谢 </a>

  <br />
  <br />
English | 简体中文

</div>
[!重要]

<div align="center">
<b>
📢 欢迎来到首个由xDAN和APUS联合训练的高性能万亿参数MoE架构LLM。📢
</b>
<br>
<b>
🤗 这是一个高性能的MoE模型，其数学(GSM8k_Cot:79%)，推理(MMLU:75%)表现突出！
</b>
<br>
<b>
🙏 随意使用推理代码。
</b>
</div>
新闻
🙌 04-01 APUS-xDAN-4.0(MOE)模型文件链接即将发布。敬请期待更多详情！

🙌 03-31 APUS-xDAN-4.0(MOE)开源模型，在"IQ-Quantized Tech"技术下进行1.5位、2位和4位量化，优化以在消费级4090显卡上运行。

📊 性能
与其他模型比较
由xDAN-AI & APUS对齐。 xDAN-APUS4.0)
由于提示、设置和实现细节的不同，不同评估工具包生成的性能有所不同。

评价标准	模式	APUS-xDAN-4.0(MoE)	Mixtral-8x7B(MoE)	Llama2-70B	Grok-1（MoE）
总参数	生成	134B	12B	70B	314B
活跃参数	生成	60B	12B	70B	78.5B
MMLU	困惑度	75.1	71.3	69.7	73.0
BIG-Bench-Hard	生成	66.4	67.1	64.9	71.7
GSM-8K	生成	79.2	65.7	63.4	62.9
数学	生成	29.5	22.7	12.0	23.9
✨ 资源
部署
 使用llama.cpp进行推理
 使用vLLM进行推理
📖 模型架构
APUS-xDAN-4.0(MoE)模型主要由32个相同的MoEtransformer块组成。MoEtransformer块与普通的transformer块的主要区别在于，FFN层被MoE FFN层替换。在MoE FFN层中，张量首先通过一个门控层计算每个专家的得分，然后根据专家得分从8个专家中选择前k个专家。通过前k个专家的输出聚合张量，从而获得MoE FFN层的最终输出。每个专家由3个线性层组成。值得注意的是，Mixtral MoE的所有Norm Layers也使用RMSNorm，与LLama相同。在注意力层中，Mixtral MoE的QKV矩阵具有Q矩阵形状为(4096,4096)，K和V矩阵形状为(4096,1024)。

我们按照以下方式绘制架构：

<div align="center">
  <img src="https://github.com/shootime2021/APUS-xDAN-4.0-moe/assets/75604726/5c86b15a-5858-48bd-a6b3-62d1c326b6f4" width="800px"/>
</div>
📂 模型权重
Hugging Face格式
聊天模型
原始格式
你可以通过磁力链接或Hugging Face下载检查点

通过HF下载
APUS-xDAN-4.0-MOE
如果你无法访问Hugging Face，请尝试hf-mirror

bash
Copy code
# 下载Hugging Face
git lfs install
git clone https://huggingface.co/xDAN-AI/APUS-xDAN-4.0-MOE
# 合并文件(仅适用于HF)
cd APUS-xDAN-4.0-MOE/



# 🚀 推理

## 文本完成 
```bash
./main -m APUS-xDAN-4.0-MOE.iq1_s.gguf   --n-gpu-layers 99 \
--prompt "你是一个有用的助手 " --chatml \
--interactive \
--temp 0.7 \
--ctx-size 4096
🖊️ 引用
latex
Copy code
@misc{2023opencompass,
    title={xDAN-APUS4.0: 高性能对齐模型训练器。},
    author={xDAN-APUS4.0 贡献者},
    howpublished = {\url{https://github.com/shootime2021/APUS-xDAN-4.0-moe}},
    year={2024}
}





