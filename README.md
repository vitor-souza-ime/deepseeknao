# NAO + DeepSeek Local Conversational System

### Real-Time Speech Interaction for the NAO Humanoid Robot Using Local LLMs via Ollama

This project implements a fully local conversational architecture for the **NAO humanoid robot**, integrating the NAOqi framework with a **local Large Language Model (LLM)** provided by **Ollama** (e.g., *deepseek-llm:latest*).
The system enables real-time spoken dialogue without requiring cloud APIs, improving privacy, reducing latency, and ensuring operation even without internet access.

---

## ✨ Features

* **Local LLM inference** using Ollama (DeepSeek or any installed model)
* **Bidirectional communication** between NAO and the language model
* **Automatic speech recognition (ASR)** through NAO's ALSpeechRecognition
* **Natural speech synthesis (TTS)** using ALTextToSpeech
* **Expanded vocabulary support** for better speech recognition
* **Latency measurement** and performance statistics of the LLM
* **Robust dialogue loop** with failure handling and safe interruption
* **Fully autonomous offline conversation capability**

---

## 🧠 System Architecture

The system follows a classic pipeline for robotic conversational agents:

1. **Speech recognition (ASR)** — NAO captures spoken input
2. **Text interpretation** — words are aggregated into a recognized sentence
3. **LLM reasoning** — DeepSeek or another model processes the user input
4. **Response synthesis** — NAO speaks the model's answer
5. **Dialogue loop** — continuous interaction with exit-word detection

All LLM processing happens **locally**, through the `ollama` CLI, avoiding cloud dependencies.

---

## 📦 Requirements

### **Hardware**

* NAO robot (tested with NAO V6; compatible with V5)
* Local machine (Linux recommended) with:

  * 8–16 GB RAM
  * CPU with AVX/AVX2 (for faster inference)
  * Optional GPU acceleration if supported by Ollama

### **Software**

* Python ≥ 3.8
* NAOqi Python SDK (`qi`)
* Ollama installed locally

  ```bash
  curl -fsSL https://ollama.com/install.sh | sh
  ```
* A local LLM model (example):

  ```bash
  ollama pull deepseek-llm:latest
  ```

---

## 🚀 Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-repo/nao-deepseek-chat.git
   cd nao-deepseek-chat
   ```

2. Install Python dependencies:

   ```bash
   pip install qi
   ```

3. Verify Ollama installation:

   ```bash
   ollama --version
   ollama list
   ```

4. Pull the DeepSeek model if necessary:

   ```bash
   ollama pull deepseek-llm:latest
   ```

---

## ⚙️ Configuration

Edit the IP address of your NAO robot in `main()`:

```python
NAO_IP = "172.15.3.253"  # replace with your robot's IP
MODEL_NAME = "deepseek-llm:latest"
```

Ensure your computer and the robot are on the same network.

---

## ▶️ Running the System

Simply execute:

```bash
python3 nao_deepseek_chat.py
```

The robot will greet the user and start listening for speech.

To stop the conversation verbally, say any of:

```
bye, goodbye, stop, quit, exit, end
```

To stop manually, press **Ctrl+C**.

---

## 🧪 Testing Speech Recognition

You can trigger a simple recognition test:

```python
chat.test_listening()
```

This verifies the microphone, ASR pipeline, and word recognition.

---

## 📡 DeepSeek Integration Details

The system communicates with the model using:

```bash
ollama run model_name "prompt text"
```

It includes:

* response cleaning (removal of prefixes and tokens)
* sentence limiting (1–2 concise sentences)
* timing metrics:

  * total inference time
  * words generated
  * throughput (words/second)
  * response/input ratio

These metrics help evaluate local LLM suitability for robotics applications.

---

## 📊 Performance Considerations

Local LLM inference reduces cloud latency, improving responsiveness in robotic interaction scenarios.
Typical results (may vary by hardware/model):

* **~600–900 ms** response generation for short queries
* **Robust offline operation**
* **No cloud costs**

---

## 🛡 Limitations

* Local models may be less capable than large cloud-based LLMs
* Speech recognition depends on NAO’s built-in ASR limitations
* Large models require substantial hardware resources
* English only (ASR/TTS configuration), unless modified manually

---

## 📁 Project Structure

```
📂 nao-deepseek-chat/
 ├── nao_deepseek_chat.py  # main implementation
 ├── README.md              # documentation
 └── requirements.txt       # optional
```

---

## 📝 License

MIT License — open for academic and research use.

---

## 🙌 Acknowledgments

This project integrates technologies from:

* SoftBank Robotics (NAOqi API)
* Ollama (local LLM runtime)
* DeepSeek (open LLM models)


