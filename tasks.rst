Tasks Reference
===============

.. dragon:task:: audio.beats
    
    Extract beat data from an audio file.
    
    :input url:   *(choices:* ``'mime:audio/*'`` *)* 
    :input_type url: url
    :file out:   *(choices:* ``'application/xml'`` *)* 
    :file_type out: mime

.. dragon:task:: audio.convert
    
    Transcode audio file (mp3, vorbis), and return audio duration.
    
    :input url:   *(choices:* ``'mime:audio/*'`` *)* 
    :input_type url: url
    :input codec:   *(choices:* ``'mp3'``, ``'vorbis'`` *)*  *(default:* ``'mp3'`` *)*
    :input_type codec: str
    :output duration: duration in seconds, rounded to 1/100th second  
    :output_type duration: float
    :output content-type:   *(choices:* ``'audio/vorbis'``, ``'audio/mp3'`` *)* 
    :output_type content-type: str
    :file out:   *(choices:* ``'audio'`` *)* 
    :file_type out: mime

.. dragon:task:: audio.structure
    
    Return audio structure from an audio file.
    
    :input url:   *(choices:* ``'mime:audio/*'`` *)* 
    :input_type url: url
    :file out:   *(choices:* ``'application/xml'`` *)* 
    :file_type out: mime

.. dragon:task:: audio.tts
    
    Create audio voice-over file using Text-to-Speech (US English, male/female voices), returns duration.
    
    :input text: Text string to be transformed into audio via speech synthesys.  
    :input_type text: str
    :input voice: 1 male and 1 female US English voices available.  *(choices:* ``'neospeech:julie'``, ``'neospeech:paul'`` *)*  *(default:* ``'neospeech:julie'`` *)*
    :input_type voice: str
    :input codec:   *(choices:* ``'ogg'``, ``'mp3'`` *)*  *(default:* ``'mp3'`` *)*
    :input_type codec: str
    :output duration:   
    :output_type duration: float
    :output content-type:   *(choices:* ``'audio/ogg'``, ``'audio/mp3'`` *)* 
    :output_type content-type: str
    :file out.ogg:   *(choices:* ``'audio/ogg'`` *)* 
    :file_type out.ogg: mime
    :file out.mp3:   *(choices:* ``'audio/mp3'`` *)* 
    :file_type out.mp3: mime

.. dragon:task:: audio.waveform
    
    Create a waveform image from an audio file.
    
    :input url:   *(choices:* ``'mime:audio/*'`` *)* 
    :input_type url: url
    :input width:    *(default:* ``1024`` *)*
    :input_type width: int
    :input height:    *(default:* ``60`` *)*
    :input_type height: int
    :input vmargin:    *(default:* ``0`` *)*
    :input_type vmargin: int
    :input fill:    *(default:* ``'#000000'`` *)*
    :input_type fill: color
    :input background:    *(default:* ``'#ffffff'`` *)*
    :input_type background: color
    :input start:    *(default:* ``'0.0'`` *)*
    :input_type start: float
    :input end:   
    :input_type end: float
    :input thumbtype:   *(choices:* ``'png'``, ``'jpeg'`` *)*  *(default:* ``'jpeg'`` *)*
    :input_type thumbtype: str
    :output width:   
    :output_type width: int
    :output height:   
    :output_type height: int
    :output content-type:   *(choices:* ``'image/png'``, ``'image/jpeg'`` *)* 
    :output_type content-type: str
    :file out:   *(choices:* ``'image'`` *)* 
    :file_type out: mime

.. dragon:task:: html.scrape
    
    Scrap html webpage to return videos & images found
    
    :input url: URL of the html page  
    :input_type url: StringField
    :output hits:   
    :output_type hits: JsonField
    :output page_title:   
    :output_type page_title: StringField

.. dragon:task:: image.thumb
    
    Create a new image of custom dimensions and orientation from an original image.
    
    :input width: desired thumbnail width  
    :input_type width: IntegerField
    :input height: desired thumbnail height  
    :input_type height: IntegerField
    :input crop: If crop is true, original image fills new image dimensions. If crop is false, original image fits new image dimensions.   *(default:* ``False`` *)*
    :input_type crop: BooleanField
    :input url: URL of the source image  
    :input_type url: StringField
    :input rot: Rotation is counterclockwise  *(choices:* ``0``, ``90``, ``180``, ``270`` *)*  *(default:* ``0`` *)*
    :input_type rot: IntegerField
    :input poster: if true, a play icon is added in the center.   *(default:* ``False`` *)*
    :input_type poster: BooleanField
    :output width: thumbnail width  
    :output_type width: IntegerField
    :output height: thumbnail height  
    :output_type height: IntegerField
    :output original_width: original image width  
    :output_type original_width: IntegerField
    :output original_height: original height  
    :output_type original_height: IntegerField
    :file output: path of the thumbnail  
    :file_type output: StoredFileField

.. dragon:task:: video.create
    
    Render XML with the legacy renderer.
    
    :input definition:   
    :input_type definition: StringField
    :input preview:    *(default:* ``True`` *)*
    :input_type preview: BooleanField
    :input export:    *(default:* ``True`` *)*
    :input_type export: BooleanField
    :input profile:   *(choices:* ``'iphone-24p'``, ``'dvd-pal-16-9'``, ``'360p'``, ``'360p-23-976-fps'``, ``'480p-4-3-29-97-fps'``, ``'dvd-ntsc-4-3-h'``, ``'dvd-pal-4-3-h'``, ``'360p-24-fps'``, ``'360p-12-5-fps'``, ``'1080p-24-fps'``, ``'youtube-12-5fps'``, ``'dvd-pal-4-3'``, ``'480p-24-fps'``, ``'iphone-slow'``, ``'ntsc-wide-wmv'``, ``'special'``, ``'360p-11-988-fps'``, ``'dvd-mpeg1-small'``, ``'youtube-flv'``, ``'720p-12-fps'``, ``'dvd-pal-16-9-h'``, ``'youtube-slow'``, ``'720p-12-5-fps'``, ``'wmv2'``, ``'flash'``, ``'flash-hq'``, ``'mobile-small'``, ``'youtube-5fps'``, ``'flash-large-4-3'``, ``'iphone'``, ``'720p-24-fps'``, ``'iphone-flv'``, ``'iphone-16-9-12fp'``, ``'1080p'``, ``'wmv1'``, ``'240p-24-fps'``, ``'iphone-16-9'``, ``'quicktime'``, ``'720p-23-98-fps'``, ``'th720p'``, ``'360p-29-97-fps'``, ``'youtube-slow-flv'``, ``'wmv2-large-4-3'``, ``'dvd-mpeg1'``, ``'ntsc-wide'``, ``'flash-small'``, ``'dvd-ntsc-16-9'``, ``'480p'``, ``'dvd-ntsc-4-3'``, ``'mobile'``, ``'iphone-sslow'``, ``'720p'``, ``'youtube'``, ``'720p-hq'``, ``'square-400'``, ``'dvd-ntsc-16-9-h'``, ``'iphone-16-9-slow'``, ``'cine-half-hd'``, ``'flash-h264'``, ``'240p'``, ``'quicktime-small'``, ``'720p-29-97-fps'``, ``'360p-12-fps'``, ``'flash-med-16-9'`` *)*  *(default:* ``u'360p'`` *)*
    :input_type profile: StringField
    :input thumbnail_time:    *(default:* ``1.0`` *)*
    :input_type thumbnail_time: FloatField
    :input url_callback:   
    :input_type url_callback: UrlCallbackField
    :output duration:   
    :output_type duration: FloatField
    :file preview:   
    :file_type preview: OutputFileField
    :file video:   
    :file_type video: StoredFileField
    :file thumbnail:   
    :file_type thumbnail: StoredFileField

.. dragon:task:: video.info
    
    Return video file information.
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: url
    :output mimeType:   
    :output_type mimeType: str
    :output type:   *(choices:* ``'video'`` *)* 
    :output_type type: str
    :output width:   
    :output_type width: int
    :output height:   
    :output_type height: int
    :output duration:   
    :output_type duration: float
    :output framerate:   
    :output_type framerate: float
    :output alpha:   
    :output_type alpha: boolean
    :output rotation:   
    :output_type rotation: float
    :output acodec:   
    :output_type acodec: str
    :output vcodec:   
    :output_type vcodec: str

.. dragon:task:: video.strip
    
    Create a film strip image of custom dimensions showing stitched frames of a video, return video.info output values for original video. 
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: url
    :input width: Pixel width of each frame stitched into film strip.  
    :input_type width: int
    :input height: Pixel height of each frame stitched into film strip.  
    :input_type height: int
    :input crop: If false, video frames fit each strip section. If true, video frames fill each strip section, aligning centers.   *(default:* ``False`` *)*
    :input_type crop: boolean
    :input wrap: Number of video frames that can be stitched horizontally before stitching starts onto a new line. Use it to create a two dimensional film strip, with count = int * wrap.  
    :input_type wrap: int
    :input start: Time of first frame extracted from video - by default first frame of video.   *(default:* ``'0.0'`` *)*
    :input_type start: float
    :input end: Time of last frame extracted from video - by default last frame of video.  
    :input_type end: float
    :input count: Number of frames extracted from video, at equal time intervals between start and end times.   *(default:* ``'10'`` *)*
    :input_type count: int
    :input thumbtype:   *(choices:* ``'png'``, ``'jpeg'`` *)*  *(default:* ``'jpeg'`` *)*
    :input_type thumbtype: str
    :output count:   
    :output_type count: int
    :output content-type:   *(choices:* ``'image/jpeg'``, ``'image/png'`` *)* 
    :output_type content-type: str
    :output width:   
    :output_type width: int
    :output height:   
    :output_type height: int
    :output original_width:   
    :output_type original_width: int
    :output original_height:   
    :output_type original_height: int
    :output duration:   
    :output_type duration: float
    :output framerate:   
    :output_type framerate: float
    :output acodec:   
    :output_type acodec: str
    :output vcodec:   
    :output_type vcodec: str
    :output alpha:   
    :output_type alpha: boolean
    :output rotation:   
    :output_type rotation: float
    :file out.jpeg:   *(choices:* ``'image/jpeg'`` *)* 
    :file_type out.jpeg: mime
    :file out.png:   *(choices:* ``'image/png'`` *)* 
    :file_type out.png: mime

.. dragon:task:: video.thumb
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: url
    :input width: Pixel width of output image file.  
    :input_type width: int
    :input height: Pixel height of output image file.  
    :input_type height: int
    :input crop: If false, video frame fits output image. If true, video frame fills output image.   *(default:* ``False`` *)*
    :input_type crop: boolean
    :input time: Timestamp of extracted video frame in seconds   *(default:* ``0.0`` *)*
    :input_type time: float
    :input thumbtype:   *(choices:* ``'png'``, ``'jpeg'`` *)*  *(default:* ``'jpeg'`` *)*
    :input_type thumbtype: str
    :output content-type:   *(choices:* ``'image/png'``, ``'image/jpeg'`` *)* 
    :output_type content-type: str
    :output width:   
    :output_type width: int
    :output height:   
    :output_type height: int
    :output original_width:   
    :output_type original_width: int
    :output original_height:   
    :output_type original_height: int
    :output duration:   
    :output_type duration: float
    :output framerate:   
    :output_type framerate: float
    :output acodec:   
    :output_type acodec: str
    :output vcodec:   
    :output_type vcodec: str
    :output alpha:   
    :output_type alpha: boolean
    :output rotation:   
    :output_type rotation: float
    :file out.jpeg:   *(choices:* ``'image/jpeg'`` *)* 
    :file_type out.jpeg: mime
    :file out.png:   *(choices:* ``'image/png'`` *)* 
    :file_type out.png: mime

.. dragon:task:: video.upload.fb
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: url
    :input apikey:   
    :input_type apikey: str
    :input appsecret:   
    :input_type appsecret: str
    :input sid:   
    :input_type sid: str
    :input title:   
    :input_type title: str
    :input description:   
    :input_type description: str
    :output url:   
    :output_type url: url

.. dragon:task:: video.upload.yt
    
    :input url:   *(choices:* ``'mime:video/*'`` *)* 
    :input_type url: url
    :input login:   
    :input_type login: str
    :input password:   
    :input_type password: str
    :input developerkey:   
    :input_type developerkey: str
    :input sid:   
    :input_type sid: str
    :input oauthconsumerkey:   
    :input_type oauthconsumerkey: str
    :input oauthconsumersecret:   
    :input_type oauthconsumersecret: str
    :input oauthtoken:   
    :input_type oauthtoken: str
    :input oauthtokensecret:   
    :input_type oauthtokensecret: str
    :input channels:   
    :input_type channels: str
    :input tags:   
    :input_type tags: str
    :input description:   
    :input_type description: str
    :input title:   
    :input_type title: str
    :input source:   
    :input_type source: str
    :input location:   
    :input_type location: str
    :input acl:   
    :input_type acl: str
    :output url:   
    :output_type url: url

