# OpenCV FFMpeg RTMP Stream

Example of live video streaming over RTMP protocol using OpenCV and FFMpeg.

For streaming without using OpenCV check [ffmpeg-webcam-rtmp-stream](https://github.com/jkuri/ffmpeg-webcam-rtmp-stream) repository.

### Installation Guide

#### Install FFMpeg

On MacOS.

```sh
brew install ffmpeg --with-sdl2 --with-freetype
```

On Ubuntu Linux.

```sh
sudo apt-get install ffmpeg libavcodec-dev libavformat-dev libavutil-dev libswscale-dev libavresample-dev libavdevice-dev -y
```

#### Install OpenCV

For installing OpenCV there's a script inside `scripts/` folder:

```sh
./scripts/install-opencv.sh
```

#### Run RTMP Server Docker image

```sh
docker run -it -p 1935:1935 --name rtmp-server jkuri/rtmp-server
```

### Compile & run

To compile source code just run:

```sh
mkdir -p build && cd build
cmake .. && make
```

Run the program to start streaming:

```sh
./build/rtmp-stream
```

To set up different options for stream, here is `./rtmp-stream -h` output

```sh
SYNOPSIS
        ./rtmp-stream [-c <camera>] [-o <output>] [-f <fps>] [-w <width>] [-h <height>] [-b <bitrate>] [-p <profile>] [-l <log>]

OPTIONS
        -c, --camera <camera>
                    camera ID (default: 0)

        -o, --output <output>
                    output RTMP server (default: rtmp://localhost/live/stream)

        -f, --fps <fps>
                    frames-per-second (default: 30)

        -w, --width <width>
                    video width (default: 800)

        -h, --height <height>
                    video height (default: 640)

        -b, --bitrate <bitrate>
                    stream bitrate in kb/s (default: 300000)

        -p, --profile <profile>
                    H264 codec profile (baseline | high | high10 | high422 | high444 | main) (default: high444)

        -l, --log <log>
                    print debug output (default: false)
```

Use VLC or `ffplay` to connect to live video stream:

```sh
ffplay -sync ext rtmp://localhost/live/stream
```

If everything worked you should see live-stream video.

<p align="center">
  <img src="https://user-images.githubusercontent.com/1796022/38590611-907bb7ba-3d32-11e8-994c-d3efe5b3651d.png">
</p>

### LICENCE

MIT
