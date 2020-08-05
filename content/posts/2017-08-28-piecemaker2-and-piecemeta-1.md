+++
author = "Naoto Hieda"
title = "Piecemaker2 and Piecemeta 1"
date = "2017-08-28"
description = "report"
tags = [ "ccl" ]
+++

![](/images/2017-08-28-piecemaker2-and-piecemeta-1.jpg)

The project "Generative Pathways" is a collaboration between Naoto Hieda and Lisa Parra starting in September 2017. Extending the concept of [EEG Experiments](https://naotohieda.com/blog/eeg-experiments), the initial aim is to research the intersection of geometric choreography and neurotechnology. There are two elements. First, we need a computer program to inspire or to choreograph a dancer. Fortunately we have access to the source code of [Pathfinder](http://waltzbinaire.com/work/pathfinder/) project, which later I rewrote as [Pathrefinder](https://github.com/micuat/Pathrefinder). Second, the movements will be archived in the forms of video, movement data and bio/neurosignals to be reviewed and analyzed later on. We had discussions with [Motion Bank](http://motionbank.org/) through Choreographic Coding Labs and a meeting at its headquarters and we decided to use [Piecemaker2](http://motionbank.org/en/content/education-piecemaker) and [Piecemeta](https://app.piecemeta.com/) platforms. Piecemaker2 is a web service to archive videos and annotations in a single timeline. Piecemeta is also a web platform but to store numeric data with constant frame rate (e.g., motion tracking). To create an account and to receive a tutorial guide, please contact Motion Bank directly. In this article, I would like to describe my initial attempt to use Piecemaker2/Piecemeta and the current issues.

To begin with, I danced with Pathfinder projected on a wall and recorded it with Yi Action Camera and Kinect 2. Therefore, the available data are:

* Video (action camera)
* Depth video (Kinect)
* Skeletal tracking (Kinect)
* Pathfinder score

The following video shows how the skeleton (left) and video from the action camera (right) appear:

{{< rawhtml >}}
<blockquote class="instagram-media" data-instgrm-version="7" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; max-width:658px; padding:0; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:8px;"> <div style=" background:#F8F8F8; line-height:0; margin-top:40px; padding:28.194444444444443% 0; text-align:center; width:100%;"> <div style=" background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAsCAMAAAApWqozAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAAAMUExURczMzPf399fX1+bm5mzY9AMAAADiSURBVDjLvZXbEsMgCES5/P8/t9FuRVCRmU73JWlzosgSIIZURCjo/ad+EQJJB4Hv8BFt+IDpQoCx1wjOSBFhh2XssxEIYn3ulI/6MNReE07UIWJEv8UEOWDS88LY97kqyTliJKKtuYBbruAyVh5wOHiXmpi5we58Ek028czwyuQdLKPG1Bkb4NnM+VeAnfHqn1k4+GPT6uGQcvu2h2OVuIf/gWUFyy8OWEpdyZSa3aVCqpVoVvzZZ2VTnn2wU8qzVjDDetO90GSy9mVLqtgYSy231MxrY6I2gGqjrTY0L8fxCxfCBbhWrsYYAAAAAElFTkSuQmCC); display:block; height:44px; margin:0 auto -44px; position:relative; top:-22px; width:44px;"></div></div><p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;"><a href="https://www.instagram.com/p/BYMxLWsFmLs/" style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none;" target="_blank">A post shared by Naoto Hiéda (@micuat)</a> on <time style=" font-family:Arial,sans-serif; font-size:14px; line-height:17px;" datetime="2017-08-25T02:10:19+00:00">Aug 24, 2017 at 7:10pm PDT</time></p></div></blockquote> <script async defer src="//platform.instagram.com/en_US/embeds.js"></script>
{{< /rawhtml >}}

The data seem to be synchronized in the video but it is because I manually started playing back the Kinect recording and action camera video at the right time. Also they are two separate programs (skeletal tracking and video player), which should be shown in a single program. The goal is to use Piecemaker2/Piecemeta so that one can review all the data streams in sync by simply hitting a play button (or even navigate through a timeline). Challenges are:

* Uploading videos and aligning the timestamps
* Outputting the Pathfinder score and uploading it to Piecemaker2/Piecemeta
* Extracting skeletal tracking and uploading it to Piecemeta

Uploading videos and aligning the timestamps
--------

The easiest way is to upload the videos on YouTube (if you wish you can select "unlisted" so only those who have a URL can watch the video) and embed them to Piecemaker2. The problem is aligning two or more videos. One solution is to use [QR codes](https://github.com/motionbank/piecemaker-processing/tree/master/time-sync/qr_sync_encoder_html) to visually encode timestamps, which should look like this:

{{< rawhtml >}}
<div class="youtube-container">
<iframe width="560" height="315" src="https://www.youtube.com/embed/j9Ln_iIhK5Q" frameborder="0" allowfullscreen></iframe>
</div>
{{< /rawhtml >}}

This is a good solution for accurate timing but you need to find a video frame a with visible QR code, decode the timestamp and calculate the timestamp at the first frame. So far I have not found an automation script to do this, and hopefully I have time to write it soon (**TODO1**). Alternatively, if your camera has an audio input jack, which my action camera does not have, you can use linear timecode to make your life easier. This time I decided to manually align timestamps by marking the frame in video when I clapped my hands.

Outputting the Pathfinder score and uploading it to Piecemaker2/Piecemeta
--------

I modified the Pathfinder code so that it dumps the score as text:

    26.124 r: +00.000 -> +01.571 tx: -06.000 -> +00.000 ... tri: +00.000 -> +01.000

The first field is the timestamp in seconds since Pathfinder is launched. Then labels "r", "tx", "ty", "sx", "sy" and "tri" follow, which are rotation, translation (x/y), scaling (x/y) and triangle deformation parameters, respectively. Every parameter is followed by "origin" -> "destination" so that from this score, one can recover the Pathfinder geometry, which is not implemented yet (**TODO2**). To align the timestamps with the video, I extracted the timestamp of the video from Piecemaker2 (something looks like 1503625428.717). Again I manually marked when the Pathfinder starts in the video. So, for example, if the video's timestamp is 1503625428.717 and Pathfinder starts after 3.5 seconds, the score should start at 1503625432.217. I assume that this can be simplified and automated if the clocks of the camera and a computer that runs Pathfinder are synchronized. Then,with no effort, absolute timestamps should be aligned (**TODO3**).

I found uploading the score data to Piecemaker2/Piecemeta to be challenging. I manually made "scene" markers on Piecemaker2 with the corrected timestamps. The advantage of Piecemaker2 is that you can jump from one scene of the video to another just by clicking on the scenes on the web platform. However, it seems there is no API to upload markers so if you have tens or hundreds of scenes, this is not practical. Next time I will use Piecemeta instead. The advantage is that data upload can be simplified by outputting csv or trac data (explained later). Nevertheless, you need to develop your own app to review the data with the video since the interface on Piecemeta is quite basic. Also you need to reformat the score into data with a constant framerate, say 30 frames per second, while points between the score can vary (usually 6-12 seconds).

Extracting skeletal tracking and uploading it to Piecemeta
--------

Kinect SDK comes with Kinect Studio, which allows you to record color and depth streams in an xef file and play them back from apps that use Kinect SDK. It is a powerful tool, and I used it for recording. As a post process, the recorded data is streamed to [OSCeleton](https://github.com/Zillode/OSCeleton-KinectSDK2) and output to a csv file using it's logging feature (you need to enable logging from a command line option or use [my branch](https://github.com/micuat/OSCeleton-KinectSDK2/tree/piecemeta)). This branch also includes a [script](https://github.com/micuat/OSCeleton-KinectSDK2/blob/piecemeta/osceleton_piecemeta/osceleton_piecemeta.py) to convert the output csv file into a trac format that is supported by Piecemeta. Once converted into trac, the joints are automatically labeled (e.g., SpineShoulder / X). You can find some data [here](https://app.piecemeta.com/packages/d06fa439-1218-49b3-b3eb-69a5011840f4/show).

The only issue is timestamping. Since the time when you hit the play button on Kinect Studio to stream data to OSCeleton is arbitrary, it is almost impossible to programmatically align the timestamp of the skeletal tracking and the original video. It seems there is a [Kinect Studio API](https://msdn.microsoft.com/en-us/library/dn785306.aspx) so you may be able to extract the timestamps when they are recorded. But this also means that modification to the OSCeleton code is needed (**TODO4**). Another problem with timestamping is that OSCeleton is not running at the fixed framerate so you need to upsample the output skeletal tracking data to meet your desired framerate (**TODO5**).

Currently I have problems described above but, at least, I succeeded in retrieving the uploaded data from Piecemaker2/Piecemeta and playing back the video with skeletal tracking by modifying [the Processing sketch](https://gist.github.com/fjenett/248d1d7ccfb8414c54a5) by Florian Jenett:

{{< rawhtml >}}
<blockquote class="instagram-media" data-instgrm-version="7" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; max-width:658px; padding:0; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:8px;"> <div style=" background:#F8F8F8; line-height:0; margin-top:40px; padding:26.180555555555557% 0; text-align:center; width:100%;"> <div style=" background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAsCAMAAAApWqozAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAAAMUExURczMzPf399fX1+bm5mzY9AMAAADiSURBVDjLvZXbEsMgCES5/P8/t9FuRVCRmU73JWlzosgSIIZURCjo/ad+EQJJB4Hv8BFt+IDpQoCx1wjOSBFhh2XssxEIYn3ulI/6MNReE07UIWJEv8UEOWDS88LY97kqyTliJKKtuYBbruAyVh5wOHiXmpi5we58Ek028czwyuQdLKPG1Bkb4NnM+VeAnfHqn1k4+GPT6uGQcvu2h2OVuIf/gWUFyy8OWEpdyZSa3aVCqpVoVvzZZ2VTnn2wU8qzVjDDetO90GSy9mVLqtgYSy231MxrY6I2gGqjrTY0L8fxCxfCBbhWrsYYAAAAAElFTkSuQmCC); display:block; height:44px; margin:0 auto -44px; position:relative; top:-22px; width:44px;"></div></div><p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;"><a href="https://www.instagram.com/p/BYTUqIiFAbk/" style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none;" target="_blank">A post shared by Naoto Hiéda (@micuat)</a> on <time style=" font-family:Arial,sans-serif; font-size:14px; line-height:17px;" datetime="2017-08-27T15:15:47+00:00">Aug 27, 2017 at 8:15am PDT</time></p></div></blockquote> <script async defer src="//platform.instagram.com/en_US/embeds.js"></script>
{{< /rawhtml >}}

Obviously data are not in sync, but I wanted to write this report in order to clarify where I am and what has to be done. Hopefully in the next post I will have a better picture of the workflow to record, to upload and to review multiple data streams.
