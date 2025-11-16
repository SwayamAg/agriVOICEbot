# 🌱 AgriVOICEbot

A voice-enabled plant classification application that uses AI to identify plants from images and provides audio feedback. Built with FastAPI, speech recognition, and text-to-speech technologies.

## 📋 Features

- **Plant Classification**: Upload plant images and get AI-powered predictions
- **Voice Input**: Interact with the bot using voice commands (via `voice_model.py`)
- **Audio Output**: Receive predictions as audio responses using text-to-speech
- **RESTful API**: FastAPI-based web service for easy integration
- **CORS Enabled**: Ready for frontend integration

## 🏗️ Architecture

The project consists of two main components:

1. **`app.py`**: FastAPI web application that provides REST endpoints for plant classification
2. **`voice_model.py`**: Voice interaction module with speech recognition and TTS capabilities

## 🚀 Quick Start

### Prerequisites

- Python 3.11.9 (as specified in `runtime.txt`)
- Microphone (for voice input functionality)
- Internet connection (for API calls and TTS)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd AgriVOICEbot
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure the image path** (for voice model)
   - Edit `voice_model.py` and update `DEFAULT_IMAGE_PATH` with your plant image path

### Running the Application

#### Option 1: Web API (FastAPI)

Start the FastAPI server:
```bash
python app.py
```

The API will be available at `http://localhost:8000`

**API Endpoints:**

- `GET /` - Health check endpoint
- `POST /predict/` - Upload a plant image and get prediction with audio
  - **Request**: Multipart form data with `file` field containing the image
  - **Response**: JSON with `message` (prediction text) and `audio_url` (path to audio file)
- `GET /get_audio` - Download the generated audio file

**Example using curl:**
```bash
curl -X POST "http://localhost:8000/predict/" \
  -F "file=@path/to/plant/image.jpg"
```

#### Option 2: Voice Interaction Mode

Run the voice-enabled script:
```bash
python voice_model.py
```

**Voice Commands:**
- Say "Predict the plant" to analyze the configured image
- Say "exit", "stop", or "quit" to exit the application

## 📦 Dependencies

- `fastapi` - Modern web framework for building APIs
- `uvicorn` - ASGI server for FastAPI
- `pillow` - Image processing library
- `requests` - HTTP library for API calls
- `gtts` - Google Text-to-Speech for audio generation
- `pyttsx3` - Offline text-to-speech engine
- `opencv-python-headless` - Computer vision library
- `SpeechRecognition` - Speech recognition library
- `sounddevice` - Audio I/O library
- `wavio` - Audio file I/O

## 🌐 Deployment

The project is configured for deployment on Heroku:

- **Procfile**: Defines the web process using uvicorn
- **runtime.txt**: Specifies Python 3.11.9
- **requirements.txt**: Lists all Python dependencies

### Deploy to Heroku

1. Create a Heroku app
2. Push your code:
   ```bash
   git push heroku main
   ```

The app will automatically use the port provided by Heroku's `PORT` environment variable.

## 🔧 Configuration

### External API

The plant classification model is hosted externally. The API endpoint used in `voice_model.py` is from the [Plant-Identification](https://github.com/SwayamAg/Plant-Identification) repository, which is a FastAPI-based image classification API that identifies 24 plant species using a TensorFlow/Keras CNN.

Update the API endpoint in `voice_model.py` if needed:

```python
API_ENDPOINT = "https://web-production-b516.up.railway.app/predict"
```

### CORS Settings

By default, CORS is enabled for all origins in `app.py`. For production, restrict this to your frontend domain:

```python
allow_origins=["https://yourfrontend.com"]
```

## 📁 Project Structure

```
AgriVOICEbot/
├── app.py              # FastAPI web application
├── voice_model.py      # Voice interaction module
├── requirements.txt    # Python dependencies
├── Procfile           # Heroku deployment configuration
├── runtime.txt        # Python version specification
└── static/            # Generated audio files (created at runtime)
```

## 🎯 Use Cases

- Agricultural research and education
- Plant identification for farmers and gardeners
- Educational tools for botany students
- Accessible plant identification for visually impaired users

## ⚠️ Notes

- The voice model requires a configured image path in `DEFAULT_IMAGE_PATH`
- Internet connection is required for:
  - Google Speech Recognition API
  - Google Text-to-Speech (gTTS)
  - External plant classification API
- Audio files are saved in the `static/` directory

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is licensed under the MIT License.

---

## 🙏 Acknowledgments

- TensorFlow team for the deep learning framework
- FastAPI team for the excellent web framework
- The plant dataset contributors

---

## 📞 Support

For issues and questions:
- Create an issue in the repository
- Check the API documentation at `/docs` when running locally
- Review the health endpoint at `/health` for system status

---

## 👤 Made by Swayam

- **LinkedIn**: [Swayam Agarwal](https://www.linkedin.com/in/swayam-agarwal)
- **GitHub**: [SwayamAg](https://github.com/SwayamAg)

---

**Built with ❤️ for agriculture and accessibility**

