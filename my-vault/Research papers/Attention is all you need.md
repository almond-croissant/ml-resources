Attention Is All You Need (2017)  [[transformers]]
link: https://proceedings.neurips.cc/paper_files/paper/2017/file/3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf
Problem:
RNNs/LSTMs process words sequentially and struggle with long-range dependencies.

Key Idea:
Replace recurrence with self-attention.

Important Concepts:
- Self-attention
- Multi-head attention
- Positional encoding
- Encoder-decoder attention

Why It Matters:
Foundation of GPT, BERT and modern LLMs.

My Understanding:
Self-attention = words in same sentence looking at each other.
Encoder-decoder attention = translator looking back at source sentence.

Questions:
- Why is attention O(n²)?
- How did GPT remove the encoder?