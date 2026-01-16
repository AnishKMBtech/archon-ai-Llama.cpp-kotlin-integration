# Edge AI Assistant 🤖

Run powerful AI language models **completely offline** on your Android device. No internet connection required, no data sent to servers - everything runs locally on your phone.

## ✨ What Can You Do?

- 💬 **Chat with AI** - Have natural conversations with language models
- 🔒 **100% Private** - All processing happens on your device
- 📱 **Works Offline** - No internet connection needed
- ⚡ **Real-time Responses** - Stream AI responses word-by-word
- 🎨 **Beautiful Interface** - Modern, clean design

## 📱 Requirements

- **Android Device**: Android 13 or higher
- **Storage Space**: 2-8 GB free (depending on model size)
- **Recommended**: 6+ GB RAM for best performance

## 🚀 Installation

### Option 1: Install Pre-built APK (Easiest)

1. Download the latest APK from releases
2. Enable "Install from Unknown Sources" in your Android settings
3. Open the APK file and install
4. Launch Edge AI Assistant

### Option 2: Build from Source

**Requirements:**
- Android Studio Ladybug (2024.2.1) or newer
- Java 17 or higher

**Steps:**

1. Clone this repository:
   ```bash
   git clone <your-repo-url>
   cd "edge ai assistant"
   ```

2. Open in Android Studio:
   - File → Open
   - Select the `edge ai assistant` folder
   - Wait for Gradle sync

3. Build and install:
   ```bash
   ./gradlew :app:app:assembleDebug
   ./gradlew :app:app:installDebug
   ```

   Or click the Run button (▶️) in Android Studio

APK location: `app/app/build/outputs/apk/`

## 📚 How to Use

### Step 1: Download an AI Model

You need a GGUF format model file. Popular options:

**Small & Fast (1-3 GB):**
- TinyLlama 1.1B (Q4_K_M) - Great for quick responses
- Phi-2 2.7B (Q4_K_M) - Good balance of speed and quality

**Medium (3-5 GB):**
- Mistral 7B (Q4_K_M) - High quality responses
- Llama 2 7B (Q4_K_M) - Versatile conversation

**Where to download:**
- [Hugging Face](https://huggingface.co/models?sort=trending&search=gguf)
- Search for models with "GGUF" and "Q4" in the name

> 💡 **Tip**: Choose Q4_K_M or Q4_0 quantization for mobile devices

### Step 2: Load the Model

1. Open Edge AI Assistant
2. Tap the upload icon (📎) in the top bar
3. Browse and select your downloaded GGUF file
4. Wait for the model to load (15-60 seconds)

You'll see model information once it's ready!

### Step 3: Start Chatting

1. Type your message in the text box at the bottom
2. Tap the send button (📤)
3. Watch the AI response stream in real-time
4. Continue the conversation naturally

### Tips for Best Results

- **Be specific**: Clear questions get better answers
- **Use punctuation**: Helps the model understand context
- **Short messages**: Work better on mobile devices
- **Restart if slow**: Close and reopen the app if responses slow down
- **Free memory**: Close other apps for better performance

## 🎯 Use Cases

- **Learning Assistant**: Ask questions, get explanations
- **Writing Helper**: Brainstorm ideas, improve text
- **Code Companion**: Programming help and debugging
- **Creative Writing**: Story ideas, character development
- **General Knowledge**: Answers to questions on any topic
- **Language Practice**: Conversation in different languages

## ⚙️ Troubleshooting

**App crashes when loading model:**
- Model might be too large for your device
- Try a smaller model (1-3 GB)
- Close background apps to free memory

**Responses are very slow:**
- Use a smaller or more quantized model (Q4_0, Q4_K_S)
- Restart the app
- Ensure your device isn't overheating

**Can't find the model file:**
- Make sure the file has `.gguf` extension
- Check your Downloads folder
- Model might still be downloading

**Out of memory error:**
- Your device doesn't have enough RAM
- Try a smaller model (under 2 GB)
- Close all other apps

## 📖 Additional Documentation

For developers interested in the technical details:
- [Architecture Overview](md%20files%20/ARCHITECTURE.md)
- [Development Guide](md%20files%20/QUICKSTART.md)
- [Model Management](md%20files%20/MODEL_MANAGEMENT_SPEC.md)

## 🙏 Credits

Powered by [llama.cpp](https://github.com/ggerganov/llama.cpp) - the amazing open-source LLM inference engine.

## 📧 Support

Having issues? Open an issue on GitHub or check the documentation above.

---

**Your personal AI assistant, completely offline and private** 🔒

3. Copy the built libraries:
   ```bash
   cp -r lib/build/intermediates/library_jni/debug/copyDebugJniLibsProjectOnly/jni/* \
         ../../../dependencies/llama-android/jniLibs/
   ```

## Dependencies

### Gradle Dependencies
- Kotlin 2.3.0
- Jetpack Compose BOM 2025.01.00
- AndroidX Lifecycle 2.9.0
- AndroidX DataStore Preferences 1.2.0
- Material 3

### Native Libraries
- llama.cpp (MIT License)
- GGML
- OpenMP (ARM64 only)

## License

This project integrates llama.cpp which is licensed under the MIT License.
See [llama.cpp](https://github.com/ggerganov/llama.cpp) for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

- [llama.cpp](https://github.com/ggerganov/llama.cpp) - The amazing C/C++ port of LLaMA
- ARM for the original Android implementation reference
