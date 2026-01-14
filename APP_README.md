# Edge AI Assistant - Android Application

An Android application that runs Large Language Models (LLMs) locally using llama.cpp, built with Kotlin and Jetpack Compose.

## Project Structure

```
edge ai assistant/
├── app/                          # Android application
│   ├── app/                      # Main app module
│   │   ├── src/
│   │   │   └── main/
│   │   │       ├── java/com/example/llama/
│   │   │       │   ├── MainActivity.kt          # Compose-based main activity
│   │   │       │   ├── ChatViewModel.kt         # ViewModel for chat logic
│   │   │       │   ├── ChatScreen.kt            # Main chat UI
│   │   │       │   └── ui/theme/                # Material 3 theme
│   │   │       ├── res/                         # Resources
│   │   │       └── AndroidManifest.xml
│   │   └── build.gradle.kts                     # App module build config
│   │
│   └── lib/                      # llama.cpp wrapper library
│       ├── src/main/java/com/arm/aichat/        # Kotlin/JNI wrapper
│       └── build.gradle.kts                     # Library build config
│
├── dependencies/                 # Pre-built native libraries
│   └── llama-android/
│       ├── jniLibs/              # Pre-compiled .so files
│       │   ├── arm64-v8a/        # ARM64 libraries (~103MB)
│       │   └── x86_64/           # x86_64 libraries (~90MB)
│       ├── kotlin/               # Wrapper source files
│       └── cpp/                  # JNI implementation
│
├── llama.cpp/                    # llama.cpp submodule (not built)
├── build.gradle.kts              # Root build configuration
├── settings.gradle.kts           # Project structure
└── gradlew                       # Gradle wrapper
```

## Prerequisites

- **JDK**: Java 17 or higher
- **Android Studio**: Ladybug | 2024.2.1 or newer
- **Android SDK**: API 36 (Android 15)
- **NDK**: 29.0.13113456 (not needed for pre-built libraries)
- **Minimum Android Version**: API 33 (Android 13)

## Building the Application

### From Command Line

Build the debug APK:
```bash
cd "/home/anish/Documents/edge ai assistant"
./gradlew :app:app:assembleDebug
```

Build the release APK:
```bash
./gradlew :app:app:assembleRelease
```

Install on connected device:
```bash
./gradlew :app:app:installDebug
```

### From Android Studio

1. Open Android Studio
2. File → Open → Select `/home/anish/Documents/edge ai assistant`
3. Wait for Gradle sync to complete
4. Select `app:app` configuration
5. Click Run (Shift + F10) or Build → Build Bundle(s) / APK(s)

### Output Location

Built APKs will be located at:
- Debug: `app/app/build/outputs/apk/debug/app-debug.apk`
- Release: `app/app/build/outputs/apk/release/app-release.apk`

## Using Pre-built Libraries

This project uses **pre-built llama.cpp libraries** from the `dependencies/llama-android/` directory. This eliminates the need to:
- Install NDK
- Build llama.cpp from source
- Wait for lengthy CMake builds

The native libraries are already compiled and ready to use.

### Benefits:
- ✅ **Faster builds** - No native compilation required
- ✅ **Smaller repository** - No build artifacts in git
- ✅ **Consistent builds** - Same libraries across all developers
- ✅ **Reduced dependencies** - No NDK installation needed

### Supported ABIs:
- `arm64-v8a` - Most modern Android devices (phones, tablets)
- `x86_64` - Android emulators and some tablets

## Key Features

### Modern Architecture
- **Jetpack Compose** - Declarative UI framework
- **Material 3** - Latest Material Design components
- **MVVM Pattern** - Clean separation of concerns
- **Kotlin Coroutines & Flow** - Asynchronous operations
- **ViewModel** - Lifecycle-aware state management

### llama.cpp Integration
- **Local LLM Execution** - Run models entirely on-device
- **GGUF Support** - Compatible with quantized GGUF models
- **Multiple CPU Backends** - Optimized for different ARM architectures
- **Streaming Responses** - Token-by-token generation
- **Model Selection** - Load any GGUF model from device storage

## Application Usage

1. **Launch the app**
2. **Select a GGUF model** - Tap the FAB button to choose a model file
3. **Wait for loading** - Model metadata and file will be processed
4. **Chat** - Type messages and receive AI responses

### Recommended Models

For best performance on mobile devices, use quantized models:
- **Llama 2 7B** - Q4_K_M quantization (~4GB)
- **Phi-3 Mini** - Q4_K_M quantization (~2.5GB)
- **TinyLlama** - Q4_K_M quantization (~700MB)

Download from: https://huggingface.co/models?library=gguf

## Development

### Clean Build
```bash
./gradlew clean
./gradlew :app:app:assembleDebug
```

### View Dependencies
```bash
./gradlew :app:app:dependencies
```

### Run Tests
```bash
./gradlew test
```

### Code Analysis
```bash
./gradlew lint
```

## Troubleshooting

### Build Fails - Native Libraries Not Found
Ensure the dependencies folder exists:
```bash
ls -la dependencies/llama-android/jniLibs/arm64-v8a/
```

Should show:
- libai-chat.so
- libggml.so
- libllama.so
- libggml-base.so
- libggml-cpu-*.so

### Gradle Sync Issues
```bash
./gradlew --stop
./gradlew clean
# Restart Android Studio
```

### App Crashes on Launch
Check Logcat for:
```
UnsatisfiedLinkError
```
This indicates missing native libraries.

## Size Optimization

The app uses ProGuard/R8 for code shrinking even in debug builds. To reduce APK size further:

### Split APKs by ABI
In `app/build.gradle.kts`:
```kotlin
android {
    splits {
        abi {
            isEnable = true
            reset()
            include("arm64-v8a")
            isUniversalApk = false
        }
    }
}
```

This creates separate APKs per architecture:
- arm64-v8a only: ~103MB
- Universal APK: ~193MB

## License

This application integrates llama.cpp which is licensed under MIT License.

## Contributing

When modifying the app:
1. Follow Kotlin coding conventions
2. Use Jetpack Compose for all UI
3. Maintain MVVM architecture
4. Test on physical devices when possible

## Resources

- [llama.cpp](https://github.com/ggerganov/llama.cpp)
- [Jetpack Compose](https://developer.android.com/jetpack/compose)
- [Material 3](https://m3.material.io/)
- [GGUF Models](https://huggingface.co/models?library=gguf)
