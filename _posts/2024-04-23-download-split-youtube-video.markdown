---
layout: post
title:  "युट्युब भिडियो सेगमेन्ट डाउनलोड गर्ने तरिका"
date:   2024-04-23 13:24:12 +0545
categories: tools, python
---
s
<pre>
# Install necessary libraries
# !pip install pytube ffmpeg-python

from pytube import YouTube
import ffmpeg

# Download the YouTube video
video_url = 'https://www.youtube.com/watch?v=xxxxEp7zs'
yt = YouTube(video_url)
video = yt.streams.get_highest_resolution()
video.download('/content/')

# Define the start and end times
split_times = [
    {'start': '00:02:00', 'end': '00:03:00'},
    {'start': '00:03:29', 'end': '00:04:33'}
]

# Use ffmpeg to split the video for each set of start and end times
for i, split_time in enumerate(split_times):
    start_time = split_time['start']
    end_time = split_time['end']
    output_file = f'/content/output_{start_time}_{end_time}.mp4'

    try:
        ffmpeg.input(input_file, ss=start_time, to=end_time).output(output_file).run(overwrite_output=True, capture_stderr=True)
    except ffmpeg.Error as e:
        print(f"Error splitting segment {i+1}: {e.stderr.decode()}")
</pre>
