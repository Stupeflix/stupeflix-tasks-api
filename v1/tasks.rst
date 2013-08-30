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
    
    Transcode an audio file and return its duration.
    
    :input url: URL of the audio file to be converted.  
    :input_type url: string
    :input codec: Desired codec for the output file.  *(choices:* ``'mp3'``, ``'vorbis'`` *)* 
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
    
    :input url:   *(choices:* ``'mime:audio/*'`` *)* 
    :input_type url: string
    :output duration: duration in seconds, rounded to 1/100th second
    :output_type duration: float
    :output mimeType: 
    :output_type mimeType: string
    :output codec: 
    :output_type codec: string
    :output type: 
    :output_type type: string

audio.tts
---------

.. dragon:task:: audio.tts
    
    Create audio voice-over file using Text-to-Speech (US English, male/female voices), returns duration.
    
    :input text: Text string to be transformed into audio via speech synthesys.  
    :input_type text: string
    :input voice: 1 male and 1 female US English voices available.  *(choices:* ``'neospeech:julie'``, ``'neospeech:paul'`` *)*  *(default:* ``'neospeech:julie'`` *)*
    :input_type voice: string
    :input codec:   *(choices:* ``'ogg'``, ``'mp3'`` *)*  *(default:* ``'mp3'`` *)*
    :input_type codec: string
    :output duration: 
    :output_type duration: float
    :output content-type: 
    :output_type content-type: string
    :file out.ogg: 
    :file out.mp3: 

audio.waveform
--------------

.. dragon:task:: audio.waveform
    
    Create a waveform image from an audio file.
    
    :input url:   *(choices:* ``'mime:audio/*'`` *)* 
    :input_type url: string
    :input width:    *(default:* ``1024`` *)*
    :input_type width: integer
    :input height:    *(default:* ``60`` *)*
    :input_type height: integer
    :input vmargin:    *(default:* ``0`` *)*
    :input_type vmargin: integer
    :input fill:    *(default:* ``'#000000'`` *)*
    :input_type fill: color
    :input background:    *(default:* ``'#ffffff'`` *)*
    :input_type background: color
    :input start:    *(default:* ``'0.0'`` *)*
    :input_type start: float
    :input end:   
    :input_type end: float
    :input thumbtype:   *(choices:* ``'png'``, ``'jpeg'`` *)*  *(default:* ``'jpeg'`` *)*
    :input_type thumbtype: string
    :output width: 
    :output_type width: integer
    :output height: 
    :output_type height: integer
    :output content-type: 
    :output_type content-type: string
    :file out: 

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
    
    :input url:   *(choices:* ``'mime:image/*'`` *)* 
    :input_type url: string
    :output faces: Each face has a type (front/profile), image coordinates of the detected face rectangle, and a confidence degree. Frontal faces are returned first.
    :output_type faces: string

image.info
----------

.. dragon:task:: image.info
    
    Return image file information.
    
    :input url:   *(choices:* ``'mime:image/*'`` *)* 
    :input_type url: string
    :output mimeType: 
    :output_type mimeType: string
    :output type: 
    :output_type type: string
    :output width: pixel width
    :output_type width: integer
    :output height: pixel height
    :output_type height: integer
    :output alpha: 
    :output_type alpha: boolean
    :output rotation: 
    :output_type rotation: float
    :output dateTime: 
    :output_type dateTime: date
    :output flash: 
    :output_type flash: boolean
    :output focalLength: 
    :output_type focalLength: float
    :output isoSpeed: 
    :output_type isoSpeed: float
    :output exposureTime: 
    :output_type exposureTime: float

image.saliency
--------------

.. dragon:task:: image.saliency
    
    Return an array of salient points coordinates within an image.
    
    :input url:   *(choices:* ``'mime:image/*'`` *)* 
    :input_type url: string
    :output points: 
    :output_type points: string

image.smartcrop
---------------

.. dragon:task:: image.smartcrop
    
    Return most interesting (entropy based), non-overlapping rectangles, for a given surface ratio, within an image.
    
    :input url:   *(choices:* ``'mime:image/*'`` *)* 
    :input_type url: string
    :input aspectRatio:    *(default:* ``1.7777777777777777`` *)*
    :input_type aspectRatio: float
    :input boxesNumber:    *(default:* ``10`` *)*
    :input_type boxesNumber: integer
    :input stepRatio:    *(default:* ``0.03`` *)*
    :input_type stepRatio: float
    :input diagRatio:    *(default:* ``0.3`` *)*
    :input_type diagRatio: float
    :input reverse:    *(default:* ``False`` *)*
    :input_type reverse: boolean
    :output points: 
    :output_type points: string

image.thumb
-----------

.. dragon:task:: image.thumb
    
    Create a new image of custom dimensions and orientation from an original image.
    
    :input width: desired thumbnail width  
    :input_type width: integer
    :input height: desired thumbnail height  
    :input_type height: integer
    :input crop: If crop is true, original image fills new image dimensions. If crop is false, original image fits new image dimensions.   *(default:* ``False`` *)*
    :input_type crop: boolean
    :input url: URL of the source image  
    :input_type url: string
    :input rot: Rotation is counterclockwise  *(choices:* ``0``, ``90``, ``180``, ``270`` *)*  *(default:* ``0`` *)*
    :input_type rot: integer
    :input poster: if true, a play icon is added in the center.   *(default:* ``False`` *)*
    :input_type poster: boolean
    :input format: the output format, must be jpeg, png or gif  *(choices:* ``'jpeg'``, ``'gif'``, ``'png'`` *)*  *(default:* ``u'jpeg'`` *)*
    :input_type format: string
    :output width: thumbnail width
    :output_type width: integer
    :output height: thumbnail height
    :output_type height: integer
    :output original_width: original image width
    :output_type original_width: integer
    :output original_height: original height
    :output_type original_height: integer
    :file output: path of the thumbnail

video.convert
-------------

.. dragon:task:: video.convert
    
    Create transcoded video file with custom dimensions, and return its video.info output values.
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: string
    :input width:   
    :input_type width: integer
    :input height:   
    :input_type height: integer
    :input crop:    *(default:* ``False`` *)*
    :input_type crop: boolean
    :input acodec:   *(choices:* ``'mp2'``, ``'mp3'``, ``'aac'``, ``'wmav1'``, ``'wmav2'`` *)*  *(default:* ``'aac'`` *)*
    :input_type acodec: string
    :input vcodec:   *(choices:* ``'h264'`` *)*  *(default:* ``'h264'`` *)*
    :input_type vcodec: string
    :input format:   *(choices:* ``'mp4'`` *)*  *(default:* ``'mp4'`` *)*
    :input_type format: string
    :input video_br: This map is used for a 640x360 video (unit is kbits): {'h264': 512}   *(default:* ``'512'`` *)*
    :input_type video_br: integer
    :input audio_br:    *(default:* ``'64'`` *)*
    :input_type audio_br: integer
    :input samplerate:    *(default:* ``'48000'`` *)*
    :input_type samplerate: integer
    :input crf:    *(default:* ``'24'`` *)*
    :input_type crf: integer
    :input gop:    *(default:* ``'25'`` *)*
    :input_type gop: integer
    :output content-type: 
    :output_type content-type: string
    :output width: 
    :output_type width: integer
    :output height: 
    :output_type height: integer
    :output original_width: 
    :output_type original_width: integer
    :output original_height: 
    :output_type original_height: integer
    :output duration: 
    :output_type duration: float
    :output framerate: 
    :output_type framerate: float
    :output acodec: 
    :output_type acodec: string
    :output vcodec: 
    :output_type vcodec: string
    :output alpha: 
    :output_type alpha: boolean
    :output rotation: 
    :output_type rotation: float
    :file out.mp4: 

video.create
------------

.. dragon:task:: video.create
    
    Create video file(s) from a XML definition and video profile(s).
    
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
    :file video: 
    :file thumbnail: 

video.info
----------

.. dragon:task:: video.info
    
    Return video file information.
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: string
    :output mimeType: 
    :output_type mimeType: string
    :output type: 
    :output_type type: string
    :output width: 
    :output_type width: integer
    :output height: 
    :output_type height: integer
    :output duration: 
    :output_type duration: float
    :output framerate: 
    :output_type framerate: float
    :output alpha: 
    :output_type alpha: boolean
    :output rotation: 
    :output_type rotation: float
    :output acodec: 
    :output_type acodec: string
    :output vcodec: 
    :output_type vcodec: string

video.reverse
-------------

.. dragon:task:: video.reverse
    
    Create a reversed video file with custom dimensions, and return its video.info output values.
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: string
    :input width:   
    :input_type width: integer
    :input height:   
    :input_type height: integer
    :input crop:    *(default:* ``False`` *)*
    :input_type crop: boolean
    :input acodec:   *(choices:* ``'mp2'``, ``'mp3'``, ``'aac'``, ``'wmav1'``, ``'wmav2'`` *)*  *(default:* ``'aac'`` *)*
    :input_type acodec: string
    :input vcodec:   *(choices:* ``'h264'`` *)*  *(default:* ``'h264'`` *)*
    :input_type vcodec: string
    :input format:   *(choices:* ``'mp4'`` *)*  *(default:* ``'mp4'`` *)*
    :input_type format: string
    :input video_br: This map is used for a 640x360 video (unit is kbits): {'h264': 512}   *(default:* ``'512'`` *)*
    :input_type video_br: integer
    :input audio_br:    *(default:* ``'64'`` *)*
    :input_type audio_br: integer
    :input samplerate:    *(default:* ``'48000'`` *)*
    :input_type samplerate: integer
    :input crf:    *(default:* ``'24'`` *)*
    :input_type crf: integer
    :input gop:    *(default:* ``'25'`` *)*
    :input_type gop: integer
    :output content-type: 
    :output_type content-type: string
    :output width: 
    :output_type width: integer
    :output height: 
    :output_type height: integer
    :output original_width: 
    :output_type original_width: integer
    :output original_height: 
    :output_type original_height: integer
    :output duration: 
    :output_type duration: float
    :output framerate: 
    :output_type framerate: float
    :output acodec: 
    :output_type acodec: string
    :output vcodec: 
    :output_type vcodec: string
    :output alpha: 
    :output_type alpha: boolean
    :output rotation: 
    :output_type rotation: float
    :file out.mp4: 

video.stabilize
---------------

.. dragon:task:: video.stabilize
    
    Return optimal camera path for stabilized video, and return info on original video.
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: string
    :input shakiness:    *(default:* ``6.0`` *)*
    :input_type shakiness: float
    :input contenttype:   *(choices:* ``'xml'``, ``'json'`` *)*  *(default:* ``'xml'`` *)*
    :input_type contenttype: string
    :input aspectRatio:    *(default:* ``1.7777777777777777`` *)*
    :input_type aspectRatio: float
    :output width: 
    :output_type width: integer
    :output height: 
    :output_type height: integer
    :output framerate: 
    :output_type framerate: float
    :output duration: 
    :output_type duration: float
    :output content-type: 
    :output_type content-type: string
    :file out.json: 
    :file out.xml: 

video.strip
-----------

.. dragon:task:: video.strip
    
    Create a film strip image of custom dimensions showing stitched frames of a video, return video.info output values for original video. 
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: string
    :input width: Pixel width of each frame stitched into film strip.  
    :input_type width: integer
    :input height: Pixel height of each frame stitched into film strip.  
    :input_type height: integer
    :input crop: If false, video frames fit each strip section. If true, video frames fill each strip section, aligning centers.   *(default:* ``False`` *)*
    :input_type crop: boolean
    :input wrap: Number of video frames that can be stitched horizontally before stitching starts onto a new line. Use it to create a two dimensional film strip, with count = int * wrap.  
    :input_type wrap: integer
    :input start: Time of first frame extracted from video - by default first frame of video.   *(default:* ``'0.0'`` *)*
    :input_type start: float
    :input end: Time of last frame extracted from video - by default last frame of video.  
    :input_type end: float
    :input count: Number of frames extracted from video, at equal time intervals between start and end times.   *(default:* ``'10'`` *)*
    :input_type count: integer
    :input thumbtype:   *(choices:* ``'png'``, ``'jpeg'`` *)*  *(default:* ``'jpeg'`` *)*
    :input_type thumbtype: string
    :output count: 
    :output_type count: integer
    :output content-type: 
    :output_type content-type: string
    :output width: 
    :output_type width: integer
    :output height: 
    :output_type height: integer
    :output original_width: 
    :output_type original_width: integer
    :output original_height: 
    :output_type original_height: integer
    :output duration: 
    :output_type duration: float
    :output framerate: 
    :output_type framerate: float
    :output acodec: 
    :output_type acodec: string
    :output vcodec: 
    :output_type vcodec: string
    :output alpha: 
    :output_type alpha: boolean
    :output rotation: 
    :output_type rotation: float
    :file out.jpeg: 
    :file out.png: 

video.thumb
-----------

.. dragon:task:: video.thumb
    
    Create an image of custom dimensions extracted at a specified time in a video.
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: string
    :input width: Pixel width of output image file.  
    :input_type width: integer
    :input height: Pixel height of output image file.  
    :input_type height: integer
    :input crop: If false, video frame fits output image. If true, video frame fills output image.   *(default:* ``False`` *)*
    :input_type crop: boolean
    :input time: Timestamp of extracted video frame in seconds   *(default:* ``0.0`` *)*
    :input_type time: float
    :input thumbtype:   *(choices:* ``'png'``, ``'jpeg'`` *)*  *(default:* ``'jpeg'`` *)*
    :input_type thumbtype: string
    :output content-type: 
    :output_type content-type: string
    :output width: 
    :output_type width: integer
    :output height: 
    :output_type height: integer
    :output original_width: 
    :output_type original_width: integer
    :output original_height: 
    :output_type original_height: integer
    :output duration: 
    :output_type duration: float
    :output framerate: 
    :output_type framerate: float
    :output acodec: 
    :output_type acodec: string
    :output vcodec: 
    :output_type vcodec: string
    :output alpha: 
    :output_type alpha: boolean
    :output rotation: 
    :output_type rotation: float
    :file out.jpeg: 
    :file out.png: 

video.upload.fb
---------------

.. dragon:task:: video.upload.fb
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: string
    :input apikey:   
    :input_type apikey: string
    :input appsecret:   
    :input_type appsecret: string
    :input sid:   
    :input_type sid: string
    :input title:   
    :input_type title: string
    :input description:   
    :input_type description: string
    :output url: 
    :output_type url: string

video.upload.yt
---------------

.. dragon:task:: video.upload.yt
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: string
    :input login:   
    :input_type login: string
    :input password:   
    :input_type password: string
    :input developerkey:   
    :input_type developerkey: string
    :input sid:   
    :input_type sid: string
    :input oauthconsumerkey:   
    :input_type oauthconsumerkey: string
    :input oauthconsumersecret:   
    :input_type oauthconsumersecret: string
    :input oauthtoken:   
    :input_type oauthtoken: string
    :input oauthtokensecret:   
    :input_type oauthtokensecret: string
    :input channels:   
    :input_type channels: string
    :input tags:   
    :input_type tags: string
    :input description:   
    :input_type description: string
    :input title:   
    :input_type title: string
    :input source:   
    :input_type source: string
    :input location:   
    :input_type location: string
    :input acl:   
    :input_type acl: string
    :output url: 
    :output_type url: string

