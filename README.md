# youtube-drive

youtube-drive is totally inspired by [YouTubeDrive](https://github.com/dzhang314/YouTubeDrive), a Wolfram Language (aka Mathematica) package. I read the source code of **YouTubeDrive** and write a Python version with a little change for fun.

**youtube-drive** is a Python library encodes/decodes arbitrary data to/from simple RGB videos which are automatically uploaded to/downloaded from YouTube. Since YouTube imposes no limits on the total number or length of videos users can upload, this provides an effectively infinite but extremely slow form of file storage.

youtube-drive is a silly proof-of-concept, and I do not endorse its high-volume use either.

## Usage Example

**Upload**: Encode a file to video and upload to YouTube:

```sh
python -m youtube_drive upload examples/BesselJ.png
YouTube Video ID: EzqstWlMXyk
YouTube: https://youtu.be/EzqstWlMXyk

```

**Retrieve**: Download the video from YouTube and decode to a file:

```sh
python -m youtube_drive retrieve --video-id=EzqstWlMXyk -o BesselJ-retrieved.png
/var/folders/md/dnr_ryfs2_x128p26xx2pnnc0000gn/T/tmp6qfm_msc.mp4
[youtube] EzqstWlMXyk: Downloading webpage
[youtube] EzqstWlMXyk: Downloading MPD manifest
[download] Destination: /var/folders/md/dnr_ryfs2_x128p26xx2pnnc0000gn/T/tmp6qfm_msc.f136.mp4
[download] 100% of 1.74MiB in 00:25
[download] Destination: /var/folders/md/dnr_ryfs2_x128p26xx2pnnc0000gn/T/tmp6qfm_msc.mp4.f140
[download] 100% of 58.70KiB in 00:03
[ffmpeg] Merging formats into "/var/folders/md/dnr_ryfs2_x128p26xx2pnnc0000gn/T/tmp6qfm_msc.mp4"
Deleting original file /var/folders/md/dnr_ryfs2_x128p26xx2pnnc0000gn/T/tmp6qfm_msc.f136.mp4 (pass -k to keep)
Deleting original file /var/folders/md/dnr_ryfs2_x128p26xx2pnnc0000gn/T/tmp6qfm_msc.mp4.f140 (pass -k to keep)
```

The video, video ID is **EzqstWlMXyk**, youtube-drive produces in this example can be viewed at https://youtu.be/EzqstWlMXyk. The video is encoded from the image [BesselJ.png](https://github.com/lewangdev/youtube-drive/blob/main/examples/BesselJ.png). A 62KB image file will produce a video of size 10+MB.

Another file I uploaded to YouTube is [painting.jpg](https://github.com/lewangdev/youtube-drive/blob/main/examples/painting.jpg), it produces a video of size 127.5MB, and the original size is 476KB. The video can be viewed at https://youtu.be/gKhXk3IGW2s.

## Installation

```sh
git clone https://github.com/lewangdev/youtube-drive.git
cd youtube-drive
python -m venv .venv
. .venv/bin/activate
pip install -r requirements.txt
```

## Usage

**Commands:**

```sh
python -m youtube_drive -h
usage: youtube-drive [-h] {upload,up,retrieve,r} ...

optional arguments:
  -h, --help            show this help message and exit

Commands:
  {upload,up,retrieve,r}
    upload (up)         Upload a file to YouTube
    retrieve (r)        Retrieve a video from YouTube save as <filename>

```

**Upload:**

```sh
python -m youtube_drive upload -h
usage: youtube-drive upload [-h] filename

positional arguments:
  filename    Encode file <filename> to a video and upload to YouTube

optional arguments:
  -h, --help  show this help message and exit

```

**Retrieve:**

```sh
python -m youtube_drive r -h
usage: youtube-drive retrieve [-h] [--video-id video_id] [-o filename]

optional arguments:
  -h, --help           show this help message and exit
  --video-id video_id  Download YouTube video with <video_id>
  -o filename          Save file to <filename>

```

## The difference between **youtube-drive** and **YouTubeDrive**

I add 4 bytes at the beginning for the file for easily padding to video frames