# YouTube-video-downloader

## Table of contents
* [General Info](#general-info)
* [Modules](#modules)
* [Files](#files)
* [Functions](#functions)

## General Info
A YouTube video downloader that given a YouTube playlist.

**Functionality:**
1. creates a .txt file that contains all the individual YouTube video URLs 
2. extracts the audio signal from the videos as .wav
3. crops and saves into a new directory the audio signal into K-second segments
4. crops and saves into a new directory the video signal into K-second segments

**Usage** 

```
$python3 preprocess_youtube.py <URL list> <path>
```

**Example:**

```  
$python3 preprocess_youtube.py 'https://www.youtube.com/playlist?list=PLP28C3ZgpKBy8G5UqubZgDEI6-vx4LGWH' '/mnt/c/Users/Alekos/Desktop/youtube_videos' 
```
#where /youtube_videos is a directory that is going to be created 

## Modules
In order to download,extract the .wav files, crop the audio files and crop the optical files<br>
you need to have following libraries installed in your system:<br>

* [pytube3](https://github.com/hbmartin/pytube3)<br>
* [natsort](https://pypi.org/project/natsort/)<br>
* [pydub](https://pypi.org/project/pydub/)

**For pytube do:**<br>
```sudo pip3 uninstall pytube ``` <br>
```sudo pip3 install pytube3 --upgrade``` 

## Files
In order to achieve your goal to download and crop the signals we created two files
named respectively: 

  1)preprocess_youtube.py <br>
  2)ffmpeg-split.py ->this file is called from cropVideo()<br>
    ffmpeg-split.py can be found here:[c0decracker/video-splitter](https://github.com/c0decracker/video-splitter/blob/master/ffmpeg-split.py)<br>
  3)video2Frames.py
    This file creates video frames, given a video signal
    
## Functions 
In the file named "preprocess_youtube.py" exist the following functions:
	
  	1)runBash(command)
		
	2)DownloadVideo(URL,path)
          This function downloads the entire playlist from youtube to the directory where
          "preprocess_youtube.py" is. In addition it saves each individual youtube videoURL
          into a .txt file named ""video_URLs.txt"" 
	
	3)getWAV(path)
	  This function gets a video signal.mp4 and creates its audio signal.wav	

	4)cropAudio(path): crop an audio signal into chunks of K seconds
	  If you want to change the seconds change this variable: chunk_length_ms
	  In addition this function creates a folder named "audio_segments" where
	  the cropped audio files are saved. 

	5)cropVideo(path): crop a video signal into chunks of K seconds
          If you need to change the seconds change -s K in the tmp variable
          #### Example: 
          change 'python2 /yourDirectory/video_segments/ffmpeg-split.py -f  -s 60' to 
          'python2 /yourDirectory/video_segments/ffmpeg-split.py -f  -s K'
          where K is the number of seconds.

          **DO NOT FORGET to set the directories especially for your system**
  
	  #do not forget to include this part:
          #### /video_segments/auxiliary.py -f  -s 10
          tmp = 'python2 /yourDirectory/video_segments/ffmpeg-split.py -f  -s 60'
          #### Example:
          tmp = 'python2 /mnt/c/Users/Alekos/Desktop/video_segments/ffmpeg-split.py -f  -s 60'  

	6)main()
          In this function we call every aforementioned function and get the user inputs 
          from the terminal

### DISCLAIMER
Sometimes the cropVideo() does not work at first! You should comment that function call in main
run the first three funtions, then comment the first three functions, and then uncomment cropVideo() in main()
and run only cropVideo()
