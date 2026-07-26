# Local AI Coding Assistant Setup Guide (Windows 11)

This guide details how to set up the **Qwen 2.5 Coder 7B** model locally on your HP EliteBook 840 G11 (Intel Core Ultra 7 / 16GB RAM) to assist with your coding projects inside VS Code.

---

## 🛠️ System Requirements Check
* **OS:** Windows 11
* **Hardware:** Intel Core Ultra 7 (with built-in Intel Arc Graphics)
* **Memory:** 16GB DDR5 Shared System RAM
* **Target Model:** Qwen 2.5 Coder 7B (Q4_K_M Quantization ~4.7 GB)

---

## 🚀 Setup Steps

### Step 1: Install LM Studio
1. Download and install [LM Studio for Windows](https://lmstudio.ai).
2. Open LM Studio and click on the **Search icon** (magnifying glass) on the left sidebar.
3. Search for `qwen2.5-coder-7b`.
4. Locate the repository by **Bartowski** or **Qwen**.
5. Find the **Q4_K_M** variant (balanced 4-bit) and click **Download**.

### Step 2: Configure Intel Arc GPU Acceleration
To prevent system lag, force the built-in Intel Arc graphics engine to process the model math:
1. Navigate to the **Chat** or **Local Server** tab in LM Studio.
2. Open the **Hardware Settings** panel on the right side.
3. Toggle **GPU Offload** to **ON**.
4. Set the GPU Backend to **Vulkan** or **DirectML** (select *Intel Arc Graphics*).
5. Move the allocation slider to **Max (100%)** to ensure the CPU is not bottlenecked.

### Step 3: Launch the Local Inference Server
1. Click the **Local Server** icon (double arrows `<->`) on the left sidebar.
2. Click the green **Start Server** button.
3. The server is now broadcasting a local API at: `http://localhost:1234`

### Step 4: Integrate with VS Code (Continue Extension)
1. Open **VS Code** on Windows 11.
2. Install the **Continue** extension from the Extensions Marketplace (`Ctrl + Shift + X`).
3. Click the gear icon on the Continue sidebar panel to open your `config.json` file.
4. Replace or update the `models` section with the following block:

```json
{
  "models": [
    {
      "title": "Qwen 7B Coder (HP Local)",
      "provider": "openai",
      "model": "qwen2.5-coder-7b",
      "apiBase": "http://localhost:1234/v1"
    }
  ],
  "tabAutocompleteModel": {
    "title": "Qwen 7B Coder (HP Local)",
    "provider": "openai",
    "model": "qwen2.5-coder-7b",
    "apiBase": "http://localhost:1234/v1"
  }
}
```

---

## 💡 How to Use in Your Project
* **Inline Completion:** Simply start typing code, and the local 7B model will generate ghost-text suggestions. Press `Tab` to accept.
* **Code Refactoring:** Highlight a block of code, press `Ctrl + I`, and type instructions (e.g., *"Refactor this function to handle null pointer exceptions"*).
* **Project Chat:** Press `Ctrl + L` to open the sidebar chat panel to ask architectural questions about your file.

