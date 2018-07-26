<a href="https://gist.github.com/umidjons/8a15ba3813039626553929458e3ad1fc">https://gist.github.com/umidjons/8a15ba3813039626553929458e3ad1fc</a><div id="articleHeader"><h1>Download Audio from YouTube</h1></div>
<p><code>-i</code> - ignore errors</p>
<p><code>-c</code> - continue</p>
<p><code>-t</code> - use video title as file name</p>
<p><code>--extract-audio</code> - extract audio track</p>
<p><code>--audio-format mp3</code> - convert to mp3</p>
<p><code>--audio-quality 0</code> - the best audio quality</p>
<p><code>--yes-playlist</code> - affirm that url points to a playlist</p>
<p><code>YT_URL</code> - video url from youtube</p>
<div><pre># Download single entry
youtube-dl -i --extract-audio --audio-format mp3 --audio-quality 0 YT_URL

# Download playlist
youtube-dl -ict --yes-playlist --extract-audio --audio-format mp3 --audio-quality 0 https://www.youtube.com/playlist?list=UUCvVpbYRgYjMN7mG7qQN0Pg

# Download playlist, --download-archive downloaded.txt add successfully downloaded files into downloaded.txt
youtube-dl --download-archive downloaded.txt --no-overwrites -ict --yes-playlist --extract-audio --audio-format mp3 --audio-quality 0 --socket-timeout 5 https://www.youtube.com/playlist?list=UUCvVpbYRgYjMN7mG7qQN0Pg

# Retry until success, no -i option
while ! youtube-dl --download-archive downloaded.txt --no-overwrites -ct --yes-playlist --extract-audio --audio-format mp3 --audio-quality 0 --socket-timeout 5 &lt;YT_PlayList_URL&gt;; do echo DISCONNECTED; sleep 5; done</pre></div>
</article>
  