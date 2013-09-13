Tasks Reference (v1)
====================

audio.beats
-----------

.. dragon:task:: audio.beats
    
    Find beats in an audio file.
    
    :input url: URL of the audio file  
    :input_type url: string
    :output beats: An array containing the timestamps of the detected beats, in seconds
    :output_type beats: object

audio.convert
-------------

.. dragon:task:: audio.convert
    
    Transcode audio file (mp3, vorbis), and return audio duration.
    
    :input url: URL of the audio file to be converted.  
    :input_type url: string
    :input codec: Desired codec for the output file.  *(choices:* ``'mp3'``, ``'vorbis'`` *)*  *(default:* ``u'mp3'`` *)*
    :input_type codec: string
    :output duration: Duration of the audio file in seconds, rounded to 1/100th second.
    :output_type duration: float
    :output content_type: Output file content type.
    :output_type content_type: string
    :file output: URL of the output file.

audio.info
----------

.. dragon:task:: audio.info
    
    Return duration of audio file.
    
    If url parameter points to a video, audio.info returns the same output key/values as video.info.
    
    :input url: URL of the audio file to be scanned.  
    :input_type url: string
    :output duration: Duration of the audio file in seconds, rounded to 1/100th second.
    :output_type duration: float
    :output content_type: Content-type of the audio file.
    :output_type content_type: string
    :output codec: Codec of the audio file.
    :output_type codec: string

audio.tts
---------

.. dragon:task:: audio.tts
    
    Create audio voice-over file using Text-to-Speech (US English, male/female voices), returns duration.
    
    :input text: Text string to be transformed into audio via speech synthesys.  
    :input_type text: string
    :input voice: 1 male and 1 female US English voices are available.  *(choices:* ``'neospeech:julie'``, ``'neospeech:paul'`` *)*  *(default:* ``u'neospeech:julie'`` *)*
    :input_type voice: string
    :input codec: 1 male and 1 female US English voices are available.  *(choices:* ``'mp3'``, ``'ogg'`` *)*  *(default:* ``u'mp3'`` *)*
    :input_type codec: string
    :output duration: Duration of the audio file in seconds, rounded to 1/100th second.
    :output_type duration: float
    :output content_type: Content-type of the audio file.
    :output_type content_type: string
    :file output: URL of the output file.

audio.waveform
--------------

.. dragon:task:: audio.waveform
    
    Create a waveform image from an audio file.
    
    :input url: URL of the audio file to be scanned.  
    :input_type url: string
    :input width:    *(default:* ``1024`` *)*
    :input_type width: integer
    :input height:    *(default:* ``60`` *)*
    :input_type height: integer
    :input vmargin: vertical margin   *(default:* ``0`` *)*
    :input_type vmargin: integer
    :input fill: Color of the wave-form.   *(default:* ``u'#000000'`` *)*
    :input_type fill: string
    :input background: Color of the background.   *(default:* ``u'#FFFFFF'`` *)*
    :input_type background: string
    :input start: seconds to start from.   *(default:* ``0.0`` *)*
    :input_type start: float
    :input end:   
    :input_type end: float
    :input format:   *(choices:* ``'png'``, ``'jpeg'`` *)*  *(default:* ``u'jpeg'`` *)*
    :input_type format: string
    :output width: 
    :output_type width: integer
    :output height: 
    :output_type height: integer
    :output content_type: 
    :output_type content_type: string
    :file output: URL of the output file.

html.scrape
-----------

.. dragon:task:: html.scrape
    
    Scrap html webpage to return videos & images found
    
    :input url: URL of the html page  
    :input_type url: string
    :output hits: 
    :output_type hits: object
    :output page_title: 
    :output_type page_title: string

image.face
----------

.. dragon:task:: image.face
    
    Return an array of positions of detected faces, with type and confidence.
    
    :input url: URL of the analyzed image.  
    :input_type url: string
    :output faces: An array containing salient points coordinates.
    :output_type faces: object

image.gif
---------

.. dragon:task:: image.gif
    
    Create an animated GIF from a list of images.
    
    :input images: The list of image URLs that will be used to create the animated GIF.  
    :input_type images: list of strings
    :input loop: The number of loops of the GIF, 0 means to loop forever.   *(default:* ``0`` *)*
    :input_type loop: integer
    :input frame_duration: The duration in seconds during which each image will be shown when the GIF is playing, rounded to 1/100th of a second.   *(default:* ``0.1`` *)*
    :input_type frame_duration: float
    :input width: The pixel width of the output GIF. Leave empty to use source images width.  
    :input_type width: integer
    :input height: The pixel height of the output GIF. Leave empty to use source images height.  
    :input_type height: integer
    :file output: The URL of the output GIF.

image.info
----------

.. dragon:task:: image.info
    
    Return image file information.
    
    :input url: URL of the image file to be scanned.  
    :input_type url: string
    :output content_type: Content-Type of the image file.
    :output_type content_type: string
    :output type: Type of the file.
    :output_type type: string
    :output width: 
    :output_type width: integer
    :output height: 
    :output_type height: integer
    :output alpha: 
    :output_type alpha: boolean
    :output rotation: The rotation that should be applied to the image to see it as it was shot, in degrees.
    :output_type rotation: float
    :output date_time: 
    :output_type date_time: string
    :output flash: 
    :output_type flash: boolean
    :output focal_length: 
    :output_type focal_length: float
    :output iso_speed: 
    :output_type iso_speed: float
    :output exposure_time: 
    :output_type exposure_time: float

image.saliency
--------------

.. dragon:task:: image.saliency
    
    Return an array of salient points coordinates within an image.
    
    :input url: URL of the analyzed image.  
    :input_type url: string
    :output points: An array containing salient points coordinates.
    :output_type points: object

image.smartcrop
---------------

.. dragon:task:: image.smartcrop
    
    Return most interesting (entropy based), non-overlapping rectangles, for a given surface ratio, within an image.
    
    :input url: URL of the image file to be scanned.  
    :input_type url: string
    :input aspect_ratio:    *(default:* ``1.7777777777777777`` *)*
    :input_type aspect_ratio: float
    :input boxes_number:    *(default:* ``10`` *)*
    :input_type boxes_number: integer
    :input step_ratio:    *(default:* ``0.03`` *)*
    :input_type step_ratio: float
    :input diag_ratio:    *(default:* ``0.3`` *)*
    :input_type diag_ratio: float
    :input reverse:    *(default:* ``False`` *)*
    :input_type reverse: boolean
    :output points: the JSON dump of the result
    :output_type points: object

image.thumb
-----------

.. dragon:task:: image.thumb
    
    Create a new image of custom dimensions and orientation from an original image.
    
    :input width: Desired thumbnail width, in pixels.  
    :input_type width: integer
    :input height: Desired thumbnail height, in pixels  
    :input_type height: integer
    :input crop: If crop is true, original image fills new image dimensions. If crop is false, original image fits new image dimensions.   *(default:* ``False`` *)*
    :input_type crop: boolean
    :input url: URL of the source image  
    :input_type url: string
    :input rotation: A counter clockwise rotation rotation to apply to the thumbnail, in degrees.  *(choices:* ``0``, ``90``, ``180``, ``270`` *)*  *(default:* ``0`` *)*
    :input_type rotation: integer
    :input poster: If true, a play icon is added in the center.   *(default:* ``False`` *)*
    :input_type poster: boolean
    :input format: The output format.  *(choices:* ``'jpeg'``, ``'gif'``, ``'png'`` *)*  *(default:* ``u'jpeg'`` *)*
    :input_type format: string
    :output width: thumbnail width
    :output_type width: integer
    :output height: thumbnail height
    :output_type height: integer
    :output original_width: original image width
    :output_type original_width: integer
    :output original_height: original height
    :output_type original_height: integer
    :file output: URL of the thumbnail.

video.convert
-------------

.. dragon:task:: video.convert
    
    Create transcoded video file with custom dimensions, and return its video.info output values.
    
    :input url: URL of the video file to convert.  
    :input_type url: string
    :input width:   
    :input_type width: integer
    :input height:   
    :input_type height: integer
    :input crop: Allows croping the video to fit in the output size   *(default:* ``False`` *)*
    :input_type crop: boolean
    :input audio_codec: Desired audio audio.  *(choices:* ``'mp2'``, ``'mp3'``, ``'aac'``, ``'wmav1'``, ``'wmav2'`` *)*  *(default:* ``u'aac'`` *)*
    :input_type audio_codec: string
    :input video_codec: Desired video codec.  *(choices:* ``'h264'`` *)*  *(default:* ``u'h264'`` *)*
    :input_type video_codec: string
    :input video_bitrate: Desired video bitrate, in kbps.   *(default:* ``512`` *)*
    :input_type video_bitrate: integer
    :input audio_bitrate: Desired audio bitrate, in kbps.   *(default:* ``64`` *)*
    :input_type audio_bitrate: integer
    :input sample_rate: Desired audio sample rate, in kHz.  *(choices:* ``22050``, ``44100``, ``48000`` *)*  *(default:* ``48000`` *)*
    :input_type sample_rate: integer
    :output content_type: Output file content type.
    :output_type content_type: string
    :output width: 
    :output_type width: integer
    :output height: 
    :output_type height: integer
    :output original_width: 
    :output_type original_width: integer
    :output original_height: 
    :output_type original_height: integer
    :output duration: Duration of in seconds
    :output_type duration: float
    :output frame_rate: 
    :output_type frame_rate: float
    :output audio_codec: 
    :output_type audio_codec: string
    :output video_codec: 
    :output_type video_codec: string
    :output alpha: 
    :output_type alpha: boolean
    :output rotation: The counter clockwise rotation that should be applied to the video to see it as it was shot, in degrees.
    :output_type rotation: float
    :file output: URL of the converted file.

video.create
------------

.. dragon:task:: video.create
    
    Create video file(s) from a `XML definition <https://stupeflix-sxml.readthedocs.org/en/latest/>`_ and video profile(s).
    
    :input definition:   
    :input_type definition: string
    :input preview:    *(default:* ``True`` *)*
    :input_type preview: boolean
    :input export:    *(default:* ``True`` *)*
    :input_type export: boolean
    :input profile:   *(choices:* ``'iphone-24p'``, ``'dvd-pal-16-9'``, ``'360p'``, ``'360p-23-976-fps'``, ``'480p-4-3-29-97-fps'``, ``'dvd-ntsc-4-3-h'``, ``'dvd-pal-4-3-h'``, ``'360p-24-fps'``, ``'360p-12-5-fps'``, ``'1080p-24-fps'``, ``'youtube-12-5fps'``, ``'dvd-pal-4-3'``, ``'480p-24-fps'``, ``'iphone-slow'``, ``'ntsc-wide-wmv'``, ``'special'``, ``'360p-11-988-fps'``, ``'dvd-mpeg1-small'``, ``'youtube-flv'``, ``'720p-12-fps'``, ``'dvd-pal-16-9-h'``, ``'youtube-slow'``, ``'720p-12-5-fps'``, ``'wmv2'``, ``'flash'``, ``'flash-hq'``, ``'mobile-small'``, ``'youtube-5fps'``, ``'flash-large-4-3'``, ``'iphone'``, ``'720p-24-fps'``, ``'iphone-flv'``, ``'iphone-16-9-12fp'``, ``'1080p'``, ``'wmv1'``, ``'240p-24-fps'``, ``'iphone-16-9'``, ``'quicktime'``, ``'720p-23-98-fps'``, ``'th720p'``, ``'360p-29-97-fps'``, ``'youtube-slow-flv'``, ``'wmv2-large-4-3'``, ``'dvd-mpeg1'``, ``'ntsc-wide'``, ``'flash-small'``, ``'dvd-ntsc-16-9'``, ``'480p'``, ``'dvd-ntsc-4-3'``, ``'mobile'``, ``'iphone-sslow'``, ``'720p'``, ``'youtube'``, ``'720p-hq'``, ``'square-400'``, ``'dvd-ntsc-16-9-h'``, ``'iphone-16-9-slow'``, ``'cine-half-hd'``, ``'flash-h264'``, ``'240p'``, ``'quicktime-small'``, ``'720p-29-97-fps'``, ``'360p-12-fps'``, ``'flash-med-16-9'`` *)*  *(default:* ``u'360p'`` *)*
    :input_type profile: string
    :input thumbnail_time:    *(default:* ``1.0`` *)*
    :input_type thumbnail_time: float
    :input url_callback:   
    :input_type url_callback: string
    :output duration: 
    :output_type duration: float
    :file preview: 
    :file export: 
    :file thumbnail: 

video.info
----------

.. dragon:task:: video.info
    
    Return video file information.
    
    :input url: URL of the video file to be scanned.  
    :input_type url: string
    :output content_type: Mime-type of the video file.
    :output_type content_type: string
    :output width: Video width, in pixels.
    :output_type width: integer
    :output height: Video height, in pixels.
    :output_type height: integer
    :output duration: Video duration, in seconds.
    :output_type duration: float
    :output frame_rate: Video frame rate, in frames per second.
    :output_type frame_rate: float
    :output alpha: A boolean indicating if the video has an alpha channel.
    :output_type alpha: boolean
    :output rotation: The rotation that should be applied to the video to see it as it was shot, in degrees.
    :output_type rotation: float
    :output audio_codec: Audio codec name.
    :output_type audio_codec: string
    :output video_codec: Video codec name.
    :output_type video_codec: string

video.reverse
-------------

.. dragon:task:: video.reverse
    
    Create a reversed video file with custom dimensions, and return its video.info output values.
    
    :input url: URL of the source video.  
    :input_type url: string
    :input width: Desired width of the reversed video. If left unspecified, keep the original width.  
    :input_type width: integer
    :input height: Desired height of the reversed video. If left unspecified, keep the original height.  
    :input_type height: integer
    :input audio_codec: Desired audio codec.  *(choices:* ``'mp2'``, ``'mp3'``, ``'aac'``, ``'wmav1'``, ``'wmav2'`` *)*  *(default:* ``u'aac'`` *)*
    :input_type audio_codec: string
    :input video_codec: Desired video codec.  *(choices:* ``'h264'`` *)*  *(default:* ``u'h264'`` *)*
    :input_type video_codec: string
    :input video_bitrate: Desired video bitrate, in kbps.   *(default:* ``512`` *)*
    :input_type video_bitrate: integer
    :input audio_bitrate: Desired audio bitrate, in kbps.   *(default:* ``64`` *)*
    :input_type audio_bitrate: integer
    :input sample_rate: Desired audio sample rate, in kHz.  *(choices:* ``22050``, ``44100``, ``48000`` *)*  *(default:* ``48000`` *)*
    :input_type sample_rate: integer
    :file output: URL of the reversed video file.

video.strip
-----------

.. dragon:task:: video.strip
    
    Create a film strip image of custom dimensions showing stitched frames of a video, return video.info output values for original video.
    
    :input url: URL of the source video.  
    :input_type url: string
    :input width: Pixel width of each frame stitched into film strip.  
    :input_type width: integer
    :input height: Pixel height of each frame stitched into film strip.  
    :input_type height: integer
    :input crop: If false, video frames fit each strip section. If true, video frames fill each strip section, aligning centers.   *(default:* ``False`` *)*
    :input_type crop: boolean
    :input wrap: Number of video frames that can be stitched horizontally before stitching starts onto a new line. Use it to create a two dimensional film strip, with count = int * wrap. If left unspecified, all frames are stitched on a single line.  
    :input_type wrap: integer
    :input start: Time of first frame extracted from video - by default first frame of video.   *(default:* ``0.0`` *)*
    :input_type start: float
    :input end: Time of last frame extracted from video - by default last frame of video.  
    :input_type end: float
    :input count: Number of frames extracted from video, at equal time intervals between start and end times.   *(default:* ``10`` *)*
    :input_type count: integer
    :input format: Output image file format  *(choices:* ``'jpeg'``, ``'png'`` *)*  *(default:* ``u'jpeg'`` *)*
    :input_type format: string
    :output count: Actual number of frames in the output.
    :output_type count: integer
    :output width: Width of the output image in pixels.
    :output_type width: integer
    :output height: Height of the output image in pixels.
    :output_type height: integer
    :output original_width: Width of the input video file, in pixels.
    :output_type original_width: integer
    :output original_height: Width of the input video file, in pixels.
    :output_type original_height: integer
    :output duration: Duration of the input video file, in seconds.
    :output_type duration: integer
    :output frame_rate: Frame rate of the input video file, in frames per second.
    :output_type frame_rate: float
    :output content_type: Mime-type of the output image.
    :output_type content_type: string
    :file output: URL of the output image.

video.thumb
-----------

.. dragon:task:: video.thumb
    
    Create an image of custom dimensions extracted at a specified time in a video.
    
    :input url: URL of the source video.  
    :input_type url: string
    :input width: Width of output image file, in pixels. The default is to use the original video width.  
    :input_type width: integer
    :input height: Height of output image file, in pixels. The default is to use the original video height.  
    :input_type height: integer
    :input crop: If false, video frame fits output image. If true, video frame fills output image.   *(default:* ``False`` *)*
    :input_type crop: boolean
    :input time: Timestamp of the video frame to extract, in seconds.   *(default:* ``0.0`` *)*
    :input_type time: float
    :input format: Output image file format.  *(choices:* ``'jpeg'``, ``'png'`` *)*  *(default:* ``u'jpeg'`` *)*
    :input_type format: string
    :output width: Width of the output image in pixels.
    :output_type width: integer
    :output height: Height of the output image in pixels.
    :output_type height: integer
    :output original_width: Width of the input video file.
    :output_type original_width: integer
    :output original_height: Width of the input video file.
    :output_type original_height: integer
    :output content_type: Mime-type of the output image.
    :output_type content_type: string
    :file output: URL of the output image.

video.upload.fb
---------------

.. dragon:task:: video.upload.fb
    
    Upload a video to Facebook.
    
    :input url: URL of the source video.  
    :input_type url: string
    :input api_key: Facebook API key.  
    :input_type api_key: string
    :input app_secret: Facebook app secret.  
    :input_type app_secret: string
    :input access_token: Target user's access token.  
    :input_type access_token: string
    :input title: Video title.  
    :input_type title: string
    :input description: Video description.  
    :input_type description: string
    :file output: URL of the uploaded video on Facebook.

video.upload.yt
---------------

.. dragon:task:: video.upload.yt
    
    Upload a video to Youtube.
    
    :input url: URL of the source video.  
    :input_type url: string
    :input developer_key: Youtube developer key.  
    :input_type developer_key: string
    :input access_token: Target user's access token.  
    :input_type access_token: string
    :input title: Video title.  
    :input_type title: string
    :input description: Video description.  
    :input_type description: string
    :input tags: Video tags.  
    :input_type tags: string
    :input channels: Video channels.  
    :input_type channels: string
    :input acl: Video access control list.   *(default:* ``u'public'`` *)*
    :input_type acl: string
    :file output: URL of the uploaded video on Youtube.

