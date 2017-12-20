<a href="https://www.youtube.com/watch?v=o2Qt1H4duYw">https://www.youtube.com/watch?v=o2Qt1H4duYw</a><div id="articleHeader"><h1>              Install Full Webserver (Apache, PHP, MySQL, phpMyAdmin) | macOS Sierra        </h1></div>

    <div id="watch7-user-header">  
  <div>
    <a href="/channel/UCVtknMzpWThcN-tllCaBODQ" target="_blank">STS</a>
  </div>
4,600  
    
  

  

    
  <div>
    <div>
      
      <div>
        <div>
            <div>
                  <h2 id="yt-dialog-title-2">
      现在可以使用 YouTube TV 了
  </h2>

            </div>
          
          <div>
                <div>观看 40 多个电视频道的实时节目，不需要机顶盒。随时可以取消。</div>

          
          
        
        
      
    
  




      


    


    <div id="watch-description"><div id="watch-description-content"><div id="watch-description-clip"><div id="watch-uploader-info"><strong>2017年2月19日发布</strong></div><div id="watch-description-text"><p id="eow-description">Want to start developing your own Web-Projects on your Mac, Macbook... ?<br />Than learn how to set up your own Webserver with Apache, PHP, MySQL, phpMyAdmin and start coding today!<br /><br />-- Download Links:<br /><br />MySQL: <br /><a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Fdev.mysql.com%2Fdownloads%2Fmysql%2F&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://dev.mysql.com/downloads/mysql/</a><br /><br />phpMyAdmin: <br /><a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=https%3A%2F%2Fwww.phpmyadmin.net%2F&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">https://www.phpmyadmin.net/</a><br /><br />-- Written Guide --<br />== = terminal commands<br /><br />------- APACHE CONFIGURATION -------<br /><a href="#" target="_blank">2:15</a> Starting Apache: == sudo apachectl start ==<br /><a href="#" target="_blank">2:40</a> Go to /Library/Webserver/Documents with Finder (WerbS. Files)<br /><br />------- PHP Configuration -------<br /><a href="#" target="_blank">3:05</a> Activate PHP: == sudo nano /etc/apache2/httpd.conf ==<br /><a href="#" target="_blank">3:15</a> Delete Hashtag before <a href="/results?search_query=%23LoadModule" target="_blank">#LoadModule</a> php5...<br /><a href="#" target="_blank">3:40</a> Restart Apache: == sudo apachectl restart ==<br /><a href="#" target="_blank">3:50</a> Set .php Files priority: == sudo nano /etc/apache2/httpd.conf ==<br /><a href="#" target="_blank">4:00</a> Add index.php into DirectoryIndex index.php index.html<br /><a href="#" target="_blank">4:30</a> Restart Apache: == sudo apachectl restart ==<br /><a href="#" target="_blank">4:40</a> Set Rights for Documents Folder<br /><a href="#" target="_blank">5:20</a> Create index.php: <br />== sudo nano /Library/WebServer/Documents/index.php ==<br /><br /><br />-------- MySQL Installation / Configuration --------<br /><a href="#" target="_blank">6:20</a> Download & Install MYSQL From:<br /><a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Fdev.mysql.com%2Fdownloads%2Fmysql%2F&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://dev.mysql.com/downloads/mysql/</a><br /><a href="#" target="_blank">7:00</a> Save First MYSQL Administrator Password<br /><a href="#" target="_blank">7:20</a> Create MYSQL Symlink Folder: == sudo mkdir /var/mysql ==<br /><a href="#" target="_blank">7:25</a> Create MYSQL Symlink: <br />== sudo ln -s /tmp/mysql.sock /var/mysql/mysql.sock ==<br /><a href="#" target="_blank">7:45</a> Start MySQL in System Preferences<br /><a href="#" target="_blank">8:05</a> Go To MYSQL Folder == cd /usr/local/mysql/bin<br /><a href="#" target="_blank">8:15</a> Log into MYSQL: == sudo ./mysql -u root -p (MYSQL Password)<br /><a href="#" target="_blank">8:40</a> Change Admin Password:<br />== Alter user 'root'@'localhost' identified by 'PASSWORD'; ==<br /><a href="#" target="_blank">9:10</a> Exit MYSQL: == exit ==<br /><br /><br />------- phpMyAdmin Installation/Configuration -------<br /><a href="#" target="_blank">9:15</a> Download phpMyAdmin (extract into Documents Folder):<br /><a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=https%3A%2F%2Fwww.phpmyadmin.net%2F&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">https://www.phpmyadmin.net/</a><br /><a href="#" target="_blank">9:20</a> Rename Extracted folder to: phpMyAdmin<br /><a href="#" target="_blank">9:40</a> Go to Documents Folder == cd /Library/WebServer/Documents<br /><a href="#" target="_blank">9:45</a> Go into phpmyadmin == cd phpMyAdmin ==<br /><a href="#" target="_blank">9:54</a> Create config folder: == sudo mkdir config ==<br /><a href="#" target="_blank">9:56</a> Adjust Rights == sudo chmod o+x config<br /><a href="#" target="_blank">10:00</a> With Browse go to: localhost/phpMyAdmin/setup<br /><a href="#" target="_blank">10:05</a> Click on NEW SERVER<br /><a href="#" target="_blank">10:10</a> In Authentication Type the Password and save<br /><a href="#" target="_blank">10:25</a> Click on Download and Drag config into phpMyAdmin folder<br /><br /><br />--- DONE ENJOY ----<br /><br />Facebook: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=https%3A%2F%2Fwww.facebook.com%2FSTSYT1&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">https://www.facebook.com/STSYT1</a><br />Twitter:  <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=https%3A%2F%2Ftwitter.com%2FSTSYoutube&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">https://twitter.com/STSYoutube</a><br /><br /><br />— With what did we create this video? —<br /><br />— Mac Setup — <br />Mac Mini: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2bqXaAJ&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2bqXaAJ</a><br />SSD: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2bqXdfX&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2bqXdfX</a><br /><br />— PC Setup — <br />Processor: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2b6yvEM&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2b6yvEM</a><br />Mainboard: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2b8FH04&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2b8FH04</a><br />Ram 4x: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2bvZck8&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2bvZck8</a><br />SSD: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2bqXdfX&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2bqXdfX</a><br />Graphic Card: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2b8H4Mm&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2b8H4Mm</a><br />Water Cooling: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2bqYumZ&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2bqYumZ</a><br /> Modded Fans: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2bqYJyC&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2bqYJyC</a><br />Power Supply: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2blWfCi&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2blWfCi</a><br /><br />— Peripherials (Both Mac & PC) —<br />Monitor 2x: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2b8KADB&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2b8KADB</a><br />Keyboard: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2bCALin&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2bCALin</a><br />Mouse: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2b8HPEY&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2b8HPEY</a><br />Sound System: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2bqZIP7&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2bqZIP7</a><br />Headset: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2bqUNMa&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2bqUNMa</a><br /><br />Chair: <a href="/redirect?v=o2Qt1H4duYw&event=video_description&q=http%3A%2F%2Famzn.to%2F2blXGkg&redir_token=RanUd3fY4cwueoLTEHnEbJCVHRp8MTUxMzgzOTQxMUAxNTEzNzUzMDEx" target="_blank">http://amzn.to/2blXGkg</a><br /><br />All the Links above are affiliate Links to amazon.com, you can still choose if and where to buy those items yourself!</p></div>  <div id="watch-description-extras">
    <ul>
            <li>
    
    <ul>
        <li><a href="/channel/UCiDF_uaU1V00dAc8ddKvNxA" target="_blank">科学和技术</a></li>
    </ul>
  </li>

            <li>
    
    <ul>
        <li>标准YouTube许可</li>
    </ul>
  </li>

    </ul>
  </div>
</div></div></div>  
  
