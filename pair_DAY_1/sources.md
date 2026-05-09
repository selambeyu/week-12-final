## Sources

1. Vaswani et al. (2017) — *Attention Is All You Need*  
https://arxiv.org/abs/1706.03762  
Introduces self-attention, the mechanism that enables KV caching in transformer inference.

2. Kwon et al. (2023) — *vLLM: PagedAttention for Efficient LLM Serving*  
https://arxiv.org/abs/2309.06180  
Explains KV cache management and memory-efficient inference systems used in production LLM serving.

3. Hugging Face Documentation — Text Generation & KV Cache  
https://huggingface.co/docs/transformers/main/en/llm_tutorial  
Practical explanation of how cached key-value states are reused during autoregressive decoding.