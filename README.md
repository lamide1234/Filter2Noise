# Experimental Modifications on Filter2Noise: Self-Supervised Attention-Guided Bilateral Filtering

This branch contains my experimental updates on the original Filter2Noise model. The goal was to investigate how architectural changes impact denoising performance, particularly in terms of perceptual quality and inference time.

---

## 🧪 Experimental Modifications and Results

| Modification                          | Description                                                             | PSNR   | SSIM   | Inference Time (s) | Observed Effect                                            |
|--------------------------------------|-------------------------------------------------------------------------|--------|--------|--------------------|------------------------------------------------------------|
| **Original**                         | Baseline architecture (no positional encoding, default LayerNorm)       | 38.79  | 0.9053 | 26.36              | Good performance with efficient inference                  |
| + Relational + Absolute Positional   | Added positional encodings for spatial awareness                        | 38.73  | 0.9058 | 48.10              | Slight SSIM gain; inference time nearly doubled            |
| + Pre-LN                             | Switched to Pre-LayerNorm                                               | 38.66  | 0.9055 | 47.37              | Slight drop in metrics; may help deeper models             |
| + Residual (on Pre-LN)               | Added residuals on top of Pre-LN version                                | 38.71  | 0.9064 | 46.67              | Better SSIM, restores some lost details                    |
| + Residual (on Post-LN)              | Residuals added to baseline (Post-LN)                                   | 38.79  | 0.9077 | 68.51              | Best SSIM; same PSNR; highest inference cost               |

---

## 📌 Interpretation Summary

- **Best SSIM** (perceptual quality): Achieved with **residual + Post-LN**, though with the longest inference time.
- **Positional encodings** slightly improve spatial understanding but significantly increase computation.
- **Pre-LN** alone degrades performance, but **residuals mitigate this**.
- **Baseline remains strong**, but SSIM can be improved through architectural tuning.

---

## 🔗 Notes

This repository is a **fork** of the original Filter2Noise implementation. My experimental updates are available in this [`experimental-updates`](https://github.com/lamide1234/Filter2Noise/tree/experimental-version) branch.

I performed the architectural adjustments to explore **efficiency–accuracy tradeoffs** in self-supervised denoising, especially for resource-constrained scenarios where inference speed is critical.

---

## 📧 Contact

Feel free to reach out if you’d like to discuss the experiments or the architecture further.
