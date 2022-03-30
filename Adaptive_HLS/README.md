clone the repository 

cd Adaptive_HLS
npm install

cd src/mediaContent
move your video file insid the mediaContent directory.I have named the video file as sample.mp4 put the same name in ffmpeg command

make  the resolution folders inside mediaContent directory for example 240p   for 240x360p video trasport stream
similarly 360p , 480p, 720p etc .Note you cannot upscale the resolution than the original content resolution .

cd to 240p 
ffmpeg -i ../sample.mp4 -c:a aac -strict experimental -c:v libx264 -s 360x240 -aspect 16:9 -f hls -hls_list_size 1000000 -hls_time 2 240_out.m3u8
here libx264 says the video is in h.264 format check the format using  gst-discoverer-1.0 <video name>
  
do the same for all the other resolutions 
  cd  ../..
  vi mediaFilePlaylist.m3u8
  set the bitrate inside the mediaFilePlaylist.m3u8 along with the resolution you have obtained .
  cd ..
  node app.js
  set the IP of your device in client.html
open the browser
  http://localhost:3000
  and same stream can be obtained on other devices using http://<serverIP>:3000
