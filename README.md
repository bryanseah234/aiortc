# aiortc

An implementation of WebRTC and ORTC in Python

## Description

aiortc is a Python library for Web Real-Time Communication (WebRTC) and Object Real-Time Communication (ORTC). Built on top of asyncio, Python's standard asynchronous I/O framework, it provides a pythonic API that closely follows its JavaScript counterpart while using coroutines instead of promises and emitting events using pyee.EventEmitter.

## Features

- SDP generation and parsing
- Interactive Connectivity Establishment (ICE), including half-trickle
- DTLS key/certificate generation and handshake with encryption/decryption
- SRTP keying, encryption and decryption for RTP and RTCP
- Pure Python SCTP implementation with Data Channels support
- Sending and receiving audio (Opus / PCMU / PCMA)
- Sending and receiving video (VP8 / H.264)
- Bundling audio / video / data channels
- RTCP reports, including NACK / PLI for packet loss recovery

## Technologies Used

- Python 3
- asyncio (Python's asynchronous I/O framework)
- aioice (ICE implementation)
- av (FFmpeg bindings for audio/video)
- cryptography (for DTLS)
- pyee (event emitter)
- pylibsrtp (SRTP implementation)
- OpenSSL, FFmpeg, LibVPX, Opus (system dependencies)

## Installation

```bash
# Clone the repository
git clone https://github.com/bryanseah234/aiortc.git

# Navigate to project directory
cd aiortc

# Install system dependencies (Debian/Ubuntu)
sudo apt install libavdevice-dev libavfilter-dev libopus-dev libvpx-dev pkg-config

# Install system dependencies (macOS)
brew install ffmpeg opus libvpx pkg-config

# Install Python package
pip install aiortc
```

## Usage

```python
import asyncio
from aiortc import RTCPeerConnection, RTCSessionDescription

async def main():
    pc = RTCPeerConnection()
    
    # Create a data channel
    channel = pc.createDataChannel("chat")
    
    # Create and set local description
    offer = await pc.createOffer()
    await pc.setLocalDescription(offer)
    
    # Handle the offer (send to remote peer via signaling)
    print(pc.localDescription.sdp)

asyncio.run(main())
```

Check out the `examples/` directory for more comprehensive demos including:
- Audio, video, and data channel server with browser integration
- Datachannel CLI for command-line communication
- File transfer over data channels
- VPN over data channels
- Webcam streaming examples

## Demo

For a live demo, run the server example:

```bash
cd examples/server
pip install aiohttp aiortc opencv-python
python server.py
```

Then browse to http://127.0.0.1:8080

## Disclaimer

1. FOR EDUCATIONAL PURPOSES ONLY
2. USE AT YOUR OWN DISCRETION

## License

BSD License

---

**Author:** <a href="https://github.com/bryanseah234">bryanseah234</a>
