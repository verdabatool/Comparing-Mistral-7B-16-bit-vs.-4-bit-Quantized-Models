# Comparing-Mistral-7B-16-bit-vs.-4-bit-Quantized-Models
This repository explores the performance differences between a 16-bit and a 4-bit quantized version of the Mistral-7B model. I have analyzed inference speed, memory consumption, and overall efficiency.

## 1. Problem Statement
In this project, I have explored the performance differences between a standard **16-bit (non-quantized)** version of the Mistral-7B model and a **4-bit quantized** version. The goal is to measure how quantization impacts:
- **Inference Speed** (time to generate output)
- **Memory Consumption** (VRAM usage during inference)
- **Model Size** on disk
- **Tokens Generated per Second** (throughput)

By quantizing models, efficiency is obtained in memory usage and faster inference times at the potential cost of some loss in model accuracy. This comparison helps determine whether a 4-bit quantized Mistral-7B model is a viable option for real-world applications where resources are constrained.

---

## 2. Quantized vs. Non-Quantized Models

### Non-Quantized (16-bit) Models
- Typically use floating-point representations (e.g., FP16 or FP32).  
- Provide higher numerical precision.  
- Require significantly more memory and often run more slowly on resource-limited hardware.

### Quantized (4-bit) Models
- Convert model parameters to lower-precision representations (4 bits in this case).  
- Greatly reduce the model’s size on disk and in memory.  
- Often allow faster inference, especially on GPUs that support efficient low-precision operations.  
- May experience a slight drop in performance or accuracy due to reduced precision.

---

## 3. Mistral-7B Overview
Mistral-7B is a 7-billion-parameter language model designed for a variety of natural language processing tasks. Some of its key features are:
- **Size**: 7B parameters, making it relatively lightweight compared to larger models (e.g., 13B or 70B).  
- **Versatility**: Can handle text generation, summarization, question answering, and more.  
- **Potential for Quantization**: Its moderate parameter count makes it a good candidate for experimentation with lower precision, as memory savings and speed gains can be quite significant.

---

## 4. # Project Steps and Results

### Step 1: Import Required Libraries

## Libraries and Tools
- **Transformers**: For loading the Mistral-7B model and tokenizer.
- **BitsAndBytesConfig**: Helps configure 4-bit quantization in the transformers library.
- **PyTorch**: For model operations.
- **Matplotlib**: For plotting performance metrics.

---

## Step 2: Define a Function to Evaluate Model Performance
- **Inference Time**: Measure how long it takes to generate a fixed number of tokens.
- **VRAM Usage**: Track GPU memory usage before and after inference.
- **Tokens per Second**: Calculate the throughput.

---

## Step 3: Load and Evaluate the 4-bit Quantized Model
- **Configuration**: Use `BitsAndBytesConfig` to configure 4-bit quantization.
- **Model Loading**: Load Mistral-7B with the 4-bit weights.
- **Evaluation**: Run the performance evaluation function and record:
  - Inference time
  - VRAM usage
  - Tokens per second

---

## Step 4: Load and Evaluate the 16-bit (Non-Quantized) Model
- **Model Loading**: Load Mistral-7B in standard FP16 format.
- **Evaluation**: Run the same performance evaluation function.
- **Comparison**: Compare the metrics directly with the quantized model results.

---

## Step 5: Visualization of Performance Metrics
- **Bar Charts**: Create charts to compare:
  - Inference Time
  - Tokens per Second
  - VRAM Usage (side by side for quantized vs. non-quantized models)
- **Model Size**: Compare the on-disk size of both models (in MB).

---

## 5. Results

### 5.1 Performance Comparison
Below is a summary table extracted from the bar chart results:

| **Metric**            | **Non-Quantized** | **Quantized** |
|-----------------------|-------------------|---------------|
| **Inference Time (s)**| 214.55            | 19.00         |
| **Tokens / Second**   | 0.95              | 9.14          |
| **VRAM Used (MB)**    | 275.62            | 321.96        |

- **Inference Time**: The quantized model is significantly faster (19s vs. ~214s).
- **Tokens per Second**: The quantized model achieves much higher throughput (9.14 vs. 0.95).
- **VRAM Usage**: In this particular test, the recorded VRAM usage for the quantized model is slightly higher than the non-quantized model. This can happen depending on how the underlying library allocates memory for 4-bit weights and additional overhead.

### 5.2 Model Size Comparison
The second chart shows the on-disk model size for each version:

| **Model**         | **Size (MB)** |
|-------------------|---------------|
| **Non-Quantized** | ~13,000       |
| **Quantized**     | ~4,000        |

- The 4-bit quantized model is roughly **70% smaller** on disk compared to the 16-bit model.

---

## 6. Conclusions

- **Speed Gains**: Moving to 4-bit quantization yielded a dramatic decrease in inference time and a large increase in tokens generated per second.
- **Memory Trade-offs**: While the on-disk size dropped significantly for the quantized model, VRAM usage did not strictly decrease in this particular test. This might be influenced by the specific quantization library or additional overhead.
- **Practical Implications**:
  - If you need to serve many requests simultaneously or run on memory-constrained hardware, the 4-bit quantized model is an attractive choice.
  - Careful evaluation is still needed if exact accuracy or VRAM savings is critical for your application.

---

## Future Work
- **Accuracy and Quality**: Investigate how quantization affects the model’s performance on specific NLP benchmarks.
- **Different Quantization Methods**: Explore 8-bit or mixed-precision approaches to find a balance between speed, memory, and accuracy.
- **Hardware-Specific Optimizations**: Test on different GPUs or CPUs to see if VRAM usage differs across platforms.

---

**Thank you for reading!**  
If you have any questions or feedback, feel free to open an issue or submit a pull request.



