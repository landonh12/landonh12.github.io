# Camera performance

## Gstreamer

> I.MX8GstreamerUserGuide

>https://community.nxp.com/t5/i-MX-Processors-Knowledge-Base/i-MX-8-GStreamer-User-Guide/ta-p/1098942?attachment-id=101553


### Take an image
```
gst-launch-1.0 -v v4l2src num-buffers=1 ! jpegenc ! filesink location=capture1.jpeg
```

### Recording Video
```
gst-launch-1.0 v4l2src device=/dev/video3 ! video/x-raw,height=1920,width=1080,framerate=30/1 ! vpuenc_h264 ! avimux ! filesink location='/home/user/video.avi'
```
Output:
```
WARNING: erroneous pipeline: could not link v4l2src0 to vpuenc_h264-0, vpuenc_h264-0 can't handle caps video/x-raw, height=(int)1920, width=(int)1080, framerate=(fraction)30/1
```

Oops! Let's fix that..

Found this in the link below:

>imxvideoconvert_g2d

Let's try that.

```
gst-launch-1.0 v4l2src device=/dev/video3 ! imxvideoconvert_g2d ! "video/x-raw, height=640, width=480, framerate=30/1" ! vpuenc_h264 ! filesink location='/home/user/video.mp4'
```

This works! Let's see what the video looks like.

The video doesn't work!

What if we try avimux?

```
gst-launch-1.0 v4l2src device=/dev/video3 ! imxvideoconvert_g2d ! "video/x-raw, height=640, width=480, framerate=30/1" ! vpuenc_h264 ! avimux ! filesink location='/home/user/video.avi'
```

This worked great! The video is in this folder and is called `video.avi`.

What if we don't encode as h264?

```
gst-launch-1.0 v4l2src device=/dev/video3 ! imxvideoconvert_g2d ! "video/x-raw, height=640, width=480, framerate=30/1" ! avimux ! filesink location='/home/user/video_noh264.avi'
```

The file size is HUGE! ~100MB per 3 seconds of video.

### OpenCV

We can get 30fps in OpenCV! Just use the following VideoCapture pipeline:
```
cap = cv2.VideoCapture('v4l2src device=/dev/video3 ! video/x-raw,framerate=30/1,width=640,height=480 ! appsink', cv2.CAP_GSTREAMER)
```


## Resources
> i.MX 8M Plus Gstreamer Application Notes

https://www.hackster.io/flint-weller/make-an-ip-camera-with-the-i-mx-8m-plus-and-gstreamer-82a191