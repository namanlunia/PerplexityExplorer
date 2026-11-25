# Perplexity Explorer 🔍

> **How surprised is a language model by your sentence?**

Perplexity Explorer is an interactive, zero-dependency educational web tool that demonstrates how causal language models calculate **perplexity** to evaluate the fluency and predictability of human text.

Built with plain HTML, CSS, and modern JavaScript, it runs **distilgpt2** directly inside your browser using [Transformers.js](https://huggingface.co/docs/transformers.js).

---

## ✨ Features

- **Real In-Browser Model Inference:** Uses `Xenova/distilgpt2` (quantized `q8`) via Transformers.js v3 — no backend, API keys, or server setup required.
- **Token Probabilities & Decomposition:** Shows the exact conditional probability $P$ and surprise factor $1/P$ for every individual token, prepending the GPT-2 `<|endoftext|>` start marker (`50256`) so initial tokens are evaluated properly.
- **Three-Step Perplexity Breakdown:**
  1. **Joint Surprise Product:** Multiplies all inverse probabilities $\prod \frac{1}{P_i}$.
  2. **Sequence Normalization ($N$):** Counts total tokens for geometric mean scaling.
  3. **Perplexity Hero Score:** Calculates $\text{Perplexity} = \exp(\text{mean}(-\ln P))$ to prevent numerical overflow, featuring a smooth 600ms count-up animation and an interactive **Surprise Meter** (logarithmic scale from 1 to 1000+).
- **Next-Token Predictions:** Visualizes the top 8 tokens predicted by the model after your sentence with dynamic probability distribution bars.
- **Interactive Simulation ("Try it by hand"):** Experiment with custom tokens and probabilities live with instant validation and built-in educational presets:
  - *"I love Python"* $(0.5, 0.8, 0.2) \to 2.32$
  - *"All 1/8"* $(8 \text{ tokens at } 0.125) \to 8.00$
  - *"One surprising word"* $(0.9, 0.9, 0.9, 0.01) \to 3.42$

---

## 🎨 Design

- **Aesthetic:** Calm, modern editorial design inspired by AI research labs and Notion.
- **Typography:** Space Grotesk (headings and large numerical displays), Inter (body text), and JetBrains Mono (tokens, code, and math).
- **Color Coding:**
  - 🟢 **Expected / Confident:** $P \ge 0.30$ (Emerald `#10B981`)
  - 🟡 **Unsure / Medium:** $0.05 \le P < 0.30$ (Amber `#F59E0B`)
  - 🔴 **Surprising:** $P < 0.05$ (Rose `#F43F5E`)

---

## 🚀 Getting Started

Simply open `index.html` in any modern web browser or serve it with a local static server:

```bash
# Using Python
python3 -m http.server 8080

# Using Node.js
npx serve .
```

Navigate to `http://localhost:8080` and click **"Calculate perplexity"**. The model weights (~250MB) will download once and cache locally in your browser storage.

---

## 📄 License

MIT License.
