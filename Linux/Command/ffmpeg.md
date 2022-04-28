```bash
ffmpeg -i 'input_video.mkv' -c copy -an output_video.mkv
```

```bash
ffmpeg -i 'input_video.mkv'  -vn -acodec copy output-audio.mp4
```

```bash
ffmpeg -i input_video.mp4 -vcodec h264 -acodec aac -strict -2 output_video.mp4
```