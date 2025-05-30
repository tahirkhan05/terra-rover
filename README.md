# Terra Rover - Vision 

## Computer Vision and AI-Powered Real-Time Stream Analysis System Integrated with AWS Services

Terra Rover is an advanced real-time video analysis system integrated with AWS services that combines computer vision, speech recognition, and visual language modeling to process RTSP video streams, detect objects, and answer natural language questions about the visual scene.

## 🌟 Features

- **Real-Time Object Detection**: Uses YOLO11s for efficient, accurate object detection in video streams
- **Voice Interaction**: Ask questions about what the system sees using natural speech
- **Visual Language Model Integration**: Processes frames with Claude 3 Sonnet for intelligent scene analysis
- **High-Performance Architecture**: Optimized for low-latency, high-throughput video processing
- **AWS Integration**: Scalable cloud storage and AI processing capabilities, services used bedrock, lex, s3.
- **Multi-threaded Processing**: Parallel task execution for smooth performance

## 🛠️ System Architecture

```
terra-rover/
├── config/        # Configuration settings
├── data/          # Local data storage
├── models/        # AI model processors
├── services/      # Core system services
├── utils/         # Utility functions
├── main.py        # Main application entry point
└── model_loader.py # Model loading utilities
```

## 📋 Requirements

- Python 3.8+
- CUDA-compatible GPU (recommended)
- AWS account with appropriate permissions
- Webcam or RTSP stream source
- Microphone for voice interaction

## 🔧 Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/tahirkhan05/terra-rover.git
cd terra-rover
```

### 2. Create a virtual environment (recommended)

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure AWS credentials

Create an `.env` file in the project root directory and add your AWS credentials:

```
# AWS Credentials
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=us-east-1
S3_BUCKET=terra-rover-bucket 

# RTSP Stream (use IP Webcam app for testing)
RTSP_URL=rtsp://your_camera_ip/h264_pcm.sdp
RTSP_RECONNECT_DELAY=2
RTSP_MAX_RETRIES=10
RTSP_MAX_CONSECUTIVE_FAILURES=30

# High FPS Configuration
FPS=60
FRAME_WIDTH=1280
FRAME_HEIGHT=720

# Model Settings
OBJECT_DETECTION_MODEL=yolo11s.pt
VLM_MODEL_ID=anthropic.claude-3-sonnet-20240229-v1:0

# Speech Configuration
LEX_BOT_ID=your_lex_bot_id
LEX_BOT_ALIAS_ID=your_lex_alias_id
LEX_LOCALE_ID=en_US

# System Configuration
MAX_WORKERS=8
LOG_LEVEL=INFO  #use DEBUG for detailed logs
DEBUG=True
LOCAL_SAVE_PATH=data/captured_frames

# Performance Tuning
MAX_QUEUE_SIZE=60
PROCESSING_INTERVAL=0.01
DETECTION_CONF_THRESHOLD=0.25
IOU_THRESHOLD=0.45
```

### 5. Set up AWS resources

1. Create an S3 bucket named `terra-rover-bucket` (or update the name in your `.env` file)
2. Configure Amazon Lex bot for speech processing
3. Set up appropriate IAM permissions for Claude 3 Sonnet VLM access

## 🚀 Running the Application

Start the Terra Rover system:

```bash
python main.py
```

### Controls

- Press `s` to start a voice query about what you see
- Press `q` to quit the application

## 💬 Voice Interaction

When you press `s`, the system will:

1. Record audio from your microphone
2. Transcribe your speech using Amazon Lex
3. Capture the current video frame
4. Process your question about the frame using Claude 3 Sonnet
5. Display the answer on the screen and in the console

Example questions:
- "What objects do you see in this image?"
- "Can you describe this scene?"
- "How many people are in the frame?"
- "What is happening in this image?"

## 🔍 Advanced Configuration

You can adjust various system parameters in the `.env` file:

- **Performance Tuning**:
  - `MAX_WORKERS`: Number of parallel processing threads
  - `MAX_QUEUE_SIZE`: Frame buffer size
  - `PROCESSING_INTERVAL`: Time between frame processing

- **Detection Settings**:
  - `DETECTION_CONF_THRESHOLD`: Confidence threshold for object detection
  - `IOU_THRESHOLD`: Intersection over Union threshold for NMS

## 🛠️ Troubleshooting

### No video stream appears
- Check your RTSP URL in the `.env` file
- Ensure your camera is powered on and accessible
- Check network connectivity to the camera

### Voice recognition doesn't work
- Verify your microphone is connected and working
- Check AWS Lex configuration in the `.env` file
- Ensure you have proper AWS permissions

### Poor performance
- Try reducing resolution in the `.env` file
- Ensure you have a CUDA-compatible GPU with updated drivers
- Adjust `MAX_WORKERS` based on your CPU capabilities

## 🙏 Acknowledgements

- [Ultralytics YOLO](https://github.com/ultralytics/ultralytics) for object detection
- [OpenCV](https://opencv.org/) for video processing
- [Anthropic Claude](https://www.anthropic.com/) for visual language modeling
- [AWS](https://aws.amazon.com/) for cloud infrastructure
