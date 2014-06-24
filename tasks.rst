Tasks Reference (v2)
====================

audio.beats
-----------

.. dragon:task:: audio.beats
    
    Find beats in an audio file.
    
    :input url_callback:   
    :input_type url_callback: string
    :input url: URL of the audio file  
    :input_type url: string
    :output beats: An array containing the timestamps of the detected beats, in seconds
    :output_type beats: object
    :output duration: The processed audio file duration in seconds
    :output_type duration: integer

audio.convert
-------------

.. dragon:task:: audio.convert
    
    Transcode audio file (mp3, vorbis), and return audio duration.
    
    :input url_callback:   
    :input_type url_callback: string
    :input url: URL of the audio file to be converted.  
    :input_type url: string
    :input codec: Desired codec for the output file.  *(choices:* ``'mp3'``, ``'vorbis'`` *)*  *(default:* ``u'mp3'`` *)*
    :input_type codec: string
    :output duration: Duration of the audio file in seconds.
    :output_type duration: float
    :output content_type: Output file content type.
    :output_type content_type: string
    :file output: URL of the output file.

audio.info
----------

.. dragon:task:: audio.info
    
    Return duration and codec of an audio file.
    
    :input url_callback:   
    :input_type url_callback: string
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
    
    :input url_callback:   
    :input_type url_callback: string
    :input text: Text string to be transformed into audio via speech synthesys.  
    :input_type text: string
    :input voice: 1 male and 1 female US English voices are available.  *(choices:* ``'neospeech:julie'`` (US), ``'neospeech:paul'``(US), ``'neospeech:kate'`` (US), ``'neospeech:neobridget'`` (UK), ``'neospeech:neovioleta'`` (Spanish)    *)*  *(default:* ``u'neospeech:julie'`` *)*
    :input_type voice: string
    :input codec: Audio codec used for the output file.  *(choices:* ``'mp3'``, ``'ogg'`` *)*  *(default:* ``u'mp3'`` *)*
    :input_type codec: string
    :output duration: Duration of the audio file in seconds.
    :output_type duration: float
    :output content_type: Content-type of the audio file.
    :output_type content_type: string
    :file output: URL of the output file.

audio.waveform
--------------

.. dragon:task:: audio.waveform
    
    Create a waveform image from an audio file.
    
    :input url_callback:   
    :input_type url_callback: string
    :input url: URL of the audio file to be scanned.  
    :input_type url: string
    :input width:    *(default:* ``1024`` *)*
    :input_type width: integer
    :input height:    *(default:* ``60`` *)*
    :input_type height: integer
    :input vmargin: Vertical margin.   *(default:* ``0`` *)*
    :input_type vmargin: integer
    :input fill: Color of the wave-form.   *(default:* ``u'#000000'`` *)*
    :input_type fill: string
    :input background: Color of the background.   *(default:* ``u'#FFFFFF'`` *)*
    :input_type background: string
    :input start: Seconds to start from.   *(default:* ``0.0`` *)*
    :input_type start: float
    :input end: Generate waveform up to this point, in seconds.  
    :input_type end: float
    :input format: Output image format.  *(choices:* ``'png'``, ``'jpeg'`` *)*  *(default:* ``u'jpeg'`` *)*
    :input_type format: string
    :output duration: Duration of the audio file in seconds.
    :output_type duration: float
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
    
    Scrape html webpage to return videos & images found
    
    :input url_callback:   
    :input_type url_callback: string
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
    
    :input url_callback:   
    :input_type url_callback: string
    :input url: URL of the analyzed image.  
    :input_type url: string
    :output faces: An array containing salient points coordinates.
    :output_type faces: object

image.gif
---------

.. dragon:task:: image.gif
    
    Create an animated GIF from a list of images.
    
    :input url_callback:   
    :input_type url_callback: string
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
    
    :input url_callback:   
    :input_type url_callback: string
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

image.thumb
-----------

.. dragon:task:: image.thumb
    
    Create a new image of custom dimensions and orientation from an original image.
    
    :input url_callback:   
    :input_type url_callback: string
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
    
    Create transcoded video file with custom dimensions, and return its
    video.info output values.
    
    :input url_callback:   
    :input_type url_callback: string
    :input url: URL of the source video  
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
    :input video_bitrate: Desired video bitrate, in kbps.   *(default:* ``3000`` *)*
    :input_type video_bitrate: integer
    :input audio_bitrate: Desired audio bitrate, in kbps.   *(default:* ``128`` *)*
    :input_type audio_bitrate: integer
    :input sample_rate: Desired audio sample rate, in kHz.  *(choices:* ``22050``, ``44100``, ``48000`` *)*  *(default:* ``44100`` *)*
    :input_type sample_rate: integer
    :input crf: Output constant rate factor (video)   *(default:* ``23`` *)*
    :input_type crf: integer
    :input gop: Output group of picture (GOP) size   *(default:* ``250`` *)*
    :input_type gop: integer
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
    :output duration: Duration of the video file, in seconds.
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
    
    :input url_callback:   
    :input_type url_callback: string
    :input definition:   
    :input_type definition: string
    :input preview:    *(default:* ``False`` *)*
    :input_type preview: boolean
    :input export:    *(default:* ``True`` *)*
    :input_type export: boolean
    :input profile:   *(choices:* ``'1080p'``, ``'1080p-24-fps'``, ``'240p'``, ``'240p-24-fps'``, ``'360p'``, ``'360p-11-988-fps'``, ``'360p-12-5-fps'``, ``'360p-12-fps'``, ``'360p-23-976-fps'``, ``'360p-24-fps'``, ``'360p-29-97-fps'``, ``'480p'``, ``'480p-24-fps'``, ``'480p-4-3-29-97-fps'``, ``'720p'``, ``'720p-12-5-fps'``, ``'720p-12-fps'``, ``'720p-23-98-fps'``, ``'720p-24-fps'``, ``'720p-29-97-fps'``, ``'720p-vhq-29-97-fps'``, ``'720p-hq'``, ``'cine-half-hd'``, ``'dvd-mpeg1'``, ``'dvd-mpeg1-small'``, ``'dvd-ntsc-16-9'``, ``'dvd-ntsc-16-9-h'``, ``'dvd-ntsc-4-3'``, ``'dvd-ntsc-4-3-h'``, ``'dvd-pal-16-9'``, ``'dvd-pal-16-9-h'``, ``'dvd-pal-4-3'``, ``'dvd-pal-4-3-h'``, ``'flash'``, ``'flash-h264'``, ``'flash-hq'``, ``'flash-large-4-3'``, ``'flash-med-16-9'``, ``'flash-small'``, ``'iphone'``, ``'iphone-16-9'``, ``'iphone-16-9-12fp'``, ``'iphone-16-9-slow'``, ``'iphone-24p'``, ``'iphone-flv'``, ``'iphone-slow'``, ``'iphone-sslow'``, ``'mobile'``, ``'mobile-small'``, ``'ntsc-wide'``, ``'ntsc-wide-wmv'``, ``'quicktime'``, ``'quicktime-small'``, ``'special'``, ``'square-400'``, ``'th720p'``, ``'wmv1'``, ``'wmv2'``, ``'wmv2-large-4-3'``, ``'youtube'``, ``'youtube-12-5fps'``, ``'youtube-5fps'``, ``'youtube-flv'``, ``'youtube-slow'``, ``'youtube-slow-flv'`` *)*  *(default:* ``u'360p'`` *)*
    :input_type profile: string
    :input thumbnail_time:    *(default:* ``1.0`` *)*
    :input_type thumbnail_time: float
    :output duration: 
    :output_type duration: float
    :output width: video width
    :output_type width: integer
    :output height: video height
    :output_type height: integer
    :file preview: 
    :file export: 
    :file thumbnail: 

video.info
----------

.. dragon:task:: video.info
    
    Return video file information.
    
    :input url_callback:   
    :input_type url_callback: string
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
    
    Create a reversed video file with custom dimensions, and return its
    video.info output values.
    
    :input url_callback:   
    :input_type url_callback: string
    :input url: URL of the source video  
    :input_type url: string
    :input width:   
    :input_type width: integer
    :input height:   
    :input_type height: integer
    :input crop: Allows croping the video to fit in the output size   *(default:* ``False`` *)*
    :input_type crop: boolean
    :input video_codec: Desired video codec.  *(choices:* ``'h264'`` *)*  *(default:* ``u'h264'`` *)*
    :input_type video_codec: string
    :input video_bitrate: Desired video bitrate, in kbps. Use source bitrate if left empty.  
    :input_type video_bitrate: integer
    :input crf: Output constant rate factor (video)   *(default:* ``23`` *)*
    :input_type crf: integer
    :input gop: Output group of picture (GOP) size   *(default:* ``250`` *)*
    :input_type gop: integer
    :output duration: Duration of the video file, in seconds.
    :output_type duration: float
    :file output: URL of the converted file.

video.strip
-----------

.. dragon:task:: video.strip
    
    Create a film strip image of custom dimensions showing stitched frames of a
    video, return video.info output values for original video.
    
    :input url_callback:   
    :input_type url_callback: string
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
    :output_type duration: float
    :output frame_rate: Frame rate of the input video file, in frames per second.
    :output_type frame_rate: float
    :output content_type: Mime-type of the output image.
    :output_type content_type: string
    :file output: URL of the output image.

video.thumb
-----------

.. dragon:task:: video.thumb
    
    Create a reversed video file with custom dimensions, and return its
    video.info output values.
    
    :input url_callback:   
    :input_type url_callback: string
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
    :input poster: If true, a play icon is added in the center.   *(default:* ``False`` *)*
    :input_type poster: boolean
    :output width: Width of the output image in pixels.
    :output_type width: integer
    :output height: Height of the output image in pixels.
    :output_type height: integer
    :output original_width: Width of the input video file.
    :output_type original_width: integer
    :output original_height: Width of the input video file.
    :output_type original_height: integer
    :output duration: Duration of the input video file, in seconds.
    :output_type duration: float
    :output content_type: Mime-type of the output image.
    :output_type content_type: string
    :file output: URL of the output image.

video.upload.fb
---------------

.. dragon:task:: video.upload.fb
    
    Upload a video to Facebook.
    
    :input url_callback:   
    :input_type url_callback: string
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
    :output duration: Duration of the input video file, in seconds.
    :output_type duration: float
    :file output: URL of the uploaded video on Facebook.

video.upload.vimeo
------------------

.. dragon:task:: video.upload.vimeo
    
    Upload a video from user url on Vimeo.
    `Register your app to get a consumer key and secret <https://developer.vimeo.com/apps>`_.
    Then retrieve an access token key and a secret following `these instructions on Oauth for the Vimeo API <https://developer.vimeo.com/apis/advanced#oauth>`_.
    
    :input url_callback:   
    :input_type url_callback: string
    :input url: Video url to upload  
    :input_type url: string
    :input title: Video title  
    :input_type title: string
    :input description: Video description  
    :input_type description: string
    :input consumer_key: Application consumer key  
    :input_type consumer_key: string
    :input consumer_secret: Application consumer secret  
    :input_type consumer_secret: string
    :input access_token_key: User access token key  
    :input_type access_token_key: string
    :input access_token_secret: User access token secret  
    :input_type access_token_secret: string
    :output free_space: 
    :output_type free_space: integer
    :output uploaded_file_size: 
    :output_type uploaded_file_size: integer
    :output output: URL of the uploaded video on Vimeo.
    :output_type output: string

video.upload.youtube
--------------------

.. dragon:task:: video.upload.youtube
    
    Upload a video to Youtube using the version 3 of the API with OAuth2 Bearer authentication.
    `Register your app <https://cloud.google.com/console>`_ and retrieve an access token following `these instructions <https://developers.google.com/youtube/v3/guides/authentication>`_.

    Otherwise, you can also get a `token with us from there <http://developer.stupeflix.com/youtube/>`_
    
    :input url: URL of the source video.  
    :input_type url: string
    :input access_token: Target user's access token with upload authorization.  
    :input_type access_token: string
    :input developer_key: Youtube developer key of a registered app.  
    :input_type developer_key: string
    :input title: Video title.  
    :input_type title: string
    :input description: Video description.  
    :input_type description: string
    :input tags:    *(default:* ``[]`` *)*
    :input_type tags: list of strings
    :input category_id: Video category ID number.The default value is 22, which refers to the People & Blogs category.  
    :input_type category_id: integer
    :input privacy_status: Privacy status of the video.  *(choices:* ``'public'``, ``'private'``, ``'unlisted'`` *)*  *(default:* ``u'public'`` *)*
    :input_type privacy_status: string
    :input url_callback:   
    :input_type url_callback: string
    :output output: URL of the uploaded video on Youtube.
    :output_type output: string
    :output duration: Duration of the input video file, in seconds.
    :output_type duration: float

