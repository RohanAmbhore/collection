<a href="https://jaranguda.com/instalasi-tiny-rss-di-server-linux/">https://jaranguda.com/instalasi-tiny-rss-di-server-linux/</a><div id="articleHeader"><h1>Instalasi Tiny RSS di Server Linux</h1></div>
<p>Last Updated on <time>30 November 2017</time> By <a href="https://jaranguda.com/author/jrd/" target="_blank">tommy</a> <a href="https://jaranguda.com/instalasi-tiny-rss-di-server-linux/#respond" target="_blank">Leave a Comment</a> </p></header>


<p>Tiny Tiny RSS adalah aplikasi website yang berfungsi untuk membaca feed. Tiny Tiny RSS dibuat dengan menggunakan bahasa pemrograman PHP sehingga mudah untuk di install ;) baik untuk pemula sekali pun. Disini kita akan melakukan instalasi Tiny Tiny RSS di Linux, cara ini hampir sama disetiap distro Linux ataupun di hosting anda. </p>
<p>Download source Tiny Tiny RSS dari http://tt-rss.org/redmine/projects/tt-rss/wiki. Misalkan kita akan menginstall Tiny Tiny RSS di jaranguda.com/rss dengan lokasi filenya diletakkan di /var/www/jaranguda.com/feed</p>

<div><table><tbody><tr><td><pre>cd /var/www/jaranguda.com/feed;
wget https://github.com/gothfox/Tiny-Tiny-RSS/archive/1.8.tar.gz;</pre></td></tr></tbody></table></div>

<p>ekstrak file tersebut</p>

<div><table><tbody><tr><td><pre>tar zxvf 1.8.tar.gz</pre></td></tr></tbody></table></div>

<p>hasil ekstrak file tersebut adalah folder Tiny-Tiny-RSS-1.8, pindahkan isi folder Tiny-Tiny-RSS-1.8 ke /var/www/jaranguda.com/feed</p>

<div><table><tbody><tr><td><pre>cp Tiny-Tiny-RSS-1.8/* /var/www/jaranguda.com/feed</pre></td></tr></tbody></table></div>

<p>sebelum menginstall buat terlebih dahulu database, sebut saja nama databasenya tinyrss; login ke mysql anda</p>

<div><table><tbody><tr><td><pre>mysql -u root -p</pre></td></tr></tbody></table></div>

<p>lalu buat database bernama tinyrss</p>

<div><table><tbody><tr><td><pre> create database tinyrss;</pre></td></tr></tbody></table></div>

<p>Tahap untuk download source code dan pembuatan database sudah selesai, sekarang kita masuk ke tahap instalasi.<br />
Buka alamat misalkan contoh jaranguda.com/feed atau di tempat anda localhost/feed<br />
<a href="http://media.jaranguda.com/2013/07/Tiny-Tiny-RSS-Installer-database.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://media.jaranguda.com/2013/07/Tiny-Tiny-RSS-Installer-database.png"   alt="Tiny Tiny RSS Installer - database" /></div></a><br />
pilih database MySQL, username, password dan database. Lalu klik test configuration, bila yang anda masukkan benar akan muncul dibawahnya seperti gambar dibawah ini<br />
<a href="http://media.jaranguda.com/2013/07/tinytinyrss-test-configuration.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://media.jaranguda.com/2013/07/tinytinyrss-test-configuration.png"   alt="tinytinyrss test configuration" /></div></a><br />
Klik lagi initialize database, bila muncul <em>Unfortunately, parent directory is not writable, so we’re unable to save config.php automatically.</em><br />
copy file yang ada di form lalu simpan sebagai config.php di /var/www/jaranguda.com/feed/config.php<br />
<a href="http://media.jaranguda.com/2013/07/copy-config.php_.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://media.jaranguda.com/2013/07/copy-config.php_.png"   alt="copy config.php" /></div></a><br />
ubah file permission beberapa folder dengan cara</p>

<div><table><tbody><tr><td><pre>chmod -R 777 cache/images
chmod -R 777 cache/export
chmod -R 777 feed-icons
chmod -R 777 lock
chmod -R 777 cache/upload
chmod -R 777 cache/js</pre></td></tr></tbody></table></div>

<p>hapus folder installer</p>

<div><table><tbody><tr><td><pre>rm -fr install</pre></td></tr></tbody></table></div>

<p>lalu buka kembali http://localhost/feed/<br />
<a href="http://media.jaranguda.com/2013/07/login-tiny-rss.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://media.jaranguda.com/2013/07/login-tiny-rss.png"   alt="login tiny rss" /></div></a></p>
<p>untuk loginnya :<br />
username : <strong>admin</strong><br />
password : <strong>password</strong></p>




<div>
<h3><hr />Tulisan menarik lainnya<hr /></h3>
<ul>
<li><div>
<a href="https://jaranguda.com/redirect-www-ke-non-www-di-nginx/" target="_blank">Redirect www ke non-www di Nginx</a><p>Cara untuk redirect subdomain www ke non-www di Nginx bisa dilakukan dengan cara membuat 2…</p></div>
</li>
<li><div>
<a href="https://jaranguda.com/instalasi-git-server-di-debian-7/" target="_blank">Instalasi Git Server di Debian 7</a><p>Membuat private Git untuk perusahaan ataupun pribade, dengan bermodalkan Debian, caranya sangat gampang. Disini saya…</p></div>
</li>
<li><div>
<a href="https://jaranguda.com/koneksi-ke-vnc-server-dengan-remmina-di-linux/" target="_blank">Koneksi Ke VNC Server dengan Remmina di Linux</a><p>Remmina merupakan client untuk Remote Dekstop yang mudah digunakan, dan mensupport RDP, SFTP, SSH dan…</p></div>
</li>
<li><div>
<a href="https://jaranguda.com/instalasi-nginx-php-mysql-lemp-di-debian-7/" target="_blank">Instalasi nginx PHP MySQL (LEMP) di Debian 7</a><p>Debian digabungkan dengan Nginx, PHP, dan MySQL (MariaDB) adalah kombinasi yang tepat dan powerfull untuk…</p></div>
</li>
</ul>
</div>
