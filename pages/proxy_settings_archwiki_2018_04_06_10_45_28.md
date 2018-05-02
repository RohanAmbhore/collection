<a href="https://wiki.archlinux.org/index.php/Proxy_settings">https://wiki.archlinux.org/index.php/Proxy_settings</a><div id="articleHeader"><h1>Proxy settings</h1></div>
									
									
								
												
				
<p>A proxy is "an interface for a service, especially for one that is remote, resource-intensive, or otherwise difficult to use directly". Source: <a href="http://en.wiktionary.org/wiki/proxy" target="_blank">Proxy - Wiktionary</a>.
</p>


<h2>Environment variables</h2>
<p>Some programs, such as <a href="/index.php/Wget" title="Wget" target="_blank">wget</a> and (used by <a href="/index.php/Pacman" title="Pacman" target="_blank">pacman</a>) <i>curl</i>, use environment variables of the form "protocol_proxy" to determine the proxy for a given protocol (e.g. HTTP, FTP, ...).
</p><p>Below is an example on how to set these variables in a shell:
</p>
<pre> export http_proxy=http://10.203.0.1:5187/
 export https_proxy=$http_proxy
 export ftp_proxy=$http_proxy
 export rsync_proxy=$http_proxy
 export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"
</pre>
<p>Some programs look for the all caps version of the environment variables.
</p><p>If the proxy environment variables are to be made available to all users and all applications, the above mentioned export commands may be added to a script, say "proxy.sh" inside /etc/profile.d/. The script has to be then made executable. This method is helpful while using a Desktop Environment like <a href="/index.php/Xfce" title="Xfce" target="_blank">Xfce</a> which does not provide an option for proxy configuration. For example, <a href="/index.php/Chromium" title="Chromium" target="_blank">Chromium</a> browser will make use of the variables set using this method while running XFCE. 
</p><p>Alternatively, there's a tool named <a href="https://github.com/himanshub16/ProxyMan" target="_blank">ProxyMan</a> which claims to configure system-wide proxy settings easily. It also handles proxy configurations of other software like [git], [npm], Dropbox, etc. The project is inspired from Alan Pope's idea of making a script.
</p><p>Alternatively you can automate the toggling of the variables by adding a function to your .bashrc (thanks to Alan Pope for original script idea)
</p>
<pre>function proxy_on() {
    export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"

    if (( $# &gt; 0 )); then
        valid=$(echo $@ | sed -n 's/\([0-9]\{1,3\}.\)\{4\}:\([0-9]\+\)/&/p')
        if [[ $valid != $@ ]]; then
            &gt;&2 echo "Invalid address"
            return 1
        fi

        export http_proxy="http://$1/" \
               https_proxy=$http_proxy \
               ftp_proxy=$http_proxy \
               rsync_proxy=$http_proxy
        echo "Proxy environment variable set."
        return 0
    fi

    echo -n "username: "; read username
    if [[ $username != "" ]]; then
        echo -n "password: "
        read -es password
        local pre="$username:$password@"
    fi

    echo -n "server: "; read server
    echo -n "port: "; read port
    export http_proxy="http://$pre$server:$port/" \
           https_proxy=$http_proxy \
           ftp_proxy=$http_proxy \
           rsync_proxy=$http_proxy \
           HTTP_PROXY=$http_proxy \
           HTTPS_PROXY=$http_proxy \
           FTP_PROXY=$http_proxy \ 
           RSYNC_PROXY=$http_proxy
}

function proxy_off(){
    unset http_proxy https_proxy ftp_proxy rsync_proxy \
          HTTP_PROXY HTTPS_PROXY FTP_PROXY RSYNC_PROXY
    echo -e "Proxy environment variable removed."
}

</pre>
<p>Omit username or password if they are not needed.
</p><p>As an alternative, you may want to use the following script.
Change the strings "YourUserName", "ProxyServerAddress:Port", "LocalAddress" and "LocalDomain" to match your own data,
then edit your <code>~/.bashrc</code> to include the edited functions.
Any new bash window will have the new functions. In existing bash windows, type <code>source ~/.bashrc</code>.
You may prefer to put function definitions in a separate file like <code>functions</code> then add <code>source functions</code> to <code>.bashrc</code> instead of putting everything in <code>.bashrc</code>.
You may also want to change the name "myProxy" into something short and easy to write.
</p>
<pre> #!/bin/bash

 assignProxy(){
   PROXY_ENV="http_proxy ftp_proxy https_proxy all_proxy HTTP_PROXY HTTPS_PROXY FTP_PROXY ALL_PROXY"
   for envar in $PROXY_ENV
   do
      export $envar=$1
   done
   for envar in "no_proxy NO_PROXY"
   do
      export $envar=$2
   done
 }

 clrProxy(){
    PROXY_ENV="http_proxy ftp_proxy https_proxy all_proxy HTTP_PROXY HTTPS_PROXY FTP_PROXY ALL_PROXY"
    for envar in $PROXY_ENV
    do
       unset $envar
    done
 }

 myProxy(){
   user=YourUserName
   read -p "Password: " -s pass &&  echo -e " "
   proxy_value="http://$user:$pass@ProxyServerAddress:Port"
   no_proxy_value="localhost,127.0.0.1,LocalAddress,LocalDomain.com"
   assignProxy $proxy_value $no_proxy_value
 }
 
</pre>
<h3>Keep proxy through sudo</h3>
<p>If the proxy environment variables are set for the user only (say, from manual commands or .bashrc) they will get lost when running commands with <a href="/index.php/Sudo" title="Sudo" target="_blank">sudo</a> (or when programs use sudo internally).
</p><p>A way to prevent that is to add the following line to the sudo configuration file (accessible with visudo) :
</p>
<pre>Defaults env_keep += "http_proxy https_proxy ftp_proxy"
</pre>
<p>You may also add any other environment variable, like rsync_proxy, or no_proxy.
</p>
<h3>Automation with network managers</h3>
<ul><li><a href="/index.php/NetworkManager" title="NetworkManager" target="_blank">NetworkManager</a> cannot change the environment variables.</li>
<li><a href="/index.php/Netctl" title="Netctl" target="_blank">netctl</a> could set-up these environment variables but they would not be seen by other applications as they are not child of netctl.</li></ul>
<h2>About libproxy</h2>
<p><a href="http://code.google.com/p/libproxy/" target="_blank">libproxy</a> (which is available in the extra repository) is an abstraction library which should be used by all applications that want to access a network resource. It still is in development but could lead to a unified and automated handling of proxies in GNU/Linux if widely adopted.
</p><p>The role of libproxy is to read the proxy settings form different sources and make them available to applications which use the library. The interesting part with libproxy is that it offers an implementation of the <a href="https://en.wikipedia.org/wiki/Web_Proxy_Autodiscovery_Protocol" title="wikipedia:Web Proxy Autodiscovery Protocol" target="_blank">Web Proxy Autodiscovery Protocol</a> and an implementation of <a href="https://en.wikipedia.org/wiki/Proxy_auto-config" title="wikipedia:Proxy auto-config" target="_blank">Proxy Auto-Config</a> that goes with it.
</p><p>The <code>/usr/bin/proxy</code> binary takes URL(s) as argument(s) and returns the proxy/proxies that could be used to fetch this/these network resource(s).
</p>
<div><strong>Note:</strong> the version 0.4.11 does not support http_proxy='wpad:' because <code>{ pkg-config 'mozjs185 &gt;= 1.8.5'; }</code> fails .</div>
<p>As of 06/04/2009 libproxy is required by libsoup. It is then indirectly used by the <a href="https://www.archlinux.org/packages/?name=midori" target="_blank">midori</a> browser.
</p>
<h2>Web Proxy Options</h2>
<ul><li> <a href="/index.php/Squid" title="Squid" target="_blank">Squid</a> is a very popular caching/optimizing proxy</li>
<li> <a href="/index.php/Privoxy" title="Privoxy" target="_blank">Privoxy</a> is an anonymizing and ad-blocking proxy</li>
<li> For a simple proxy, ssh with port forwarding can be used</li></ul>
<h3>Simple Proxy with SSH</h3>
<p>Connect to a server (HOST) on which you have an account (USER) as follows
</p>
<pre>ssh -D PORT USER@HOST
</pre>
<p>For PORT, choose some number which is not an IANA registered port. This specifies that traffic on the local PORT will be forwarded to the remote HOST. ssh will act as a <a href="https://en.wikipedia.org/wiki/SOCKS" title="wikipedia:SOCKS" target="_blank">SOCKS</a> server. Software supporting SOCKS proxy servers can simply be configured to connect to PORT on localhost.
</p>
<h2>Using a SOCKS proxy</h2>
<p>There are two cases:
</p>
<ul><li>the application you want to use handles <a href="https://en.wikipedia.org/wiki/SOCKS#SOCKS5" title="wikipedia:SOCKS" target="_blank">SOCKS5</a> proxies (for example <a href="/index.php/Firefox" title="Firefox" target="_blank">Firefox</a>), then you just have to configure it to use the proxy.</li>
<li>the application you want to use does not handle SOCKS proxies, then you can try to use <a href="https://www.archlinux.org/packages/?name=tsocks" target="_blank">tsocks</a> or <a href="https://www.archlinux.org/packages/?name=proxychains-ng" target="_blank">proxychains-ng</a>.</li></ul>
<p>In Firefox, you can use the SOCKS proxy in the menu Preferences &gt; Network &gt; Settings. Choose "Manual Proxy Configuration", and set the SOCKS Host (and only this one, make sure the other fields, such as HTTP Proxy or SSL Proxy are left empty). For example, if a SOCKS5 proxy is running on localhost port 8080, put "127.0.0.1" in the SOCKS Host field, "8080" in the Port field, and validate.
</p><p>If using <i>proxychains-ng</i>, the configuration takes place in <code>/etc/proxychains.conf</code>. You may have to uncomment the last line (set by default to use <a href="/index.php/Tor" title="Tor" target="_blank">Tor</a>), and replace it with the parameters of the SOCKS proxy. For example, if you are using the same SOCKS5 proxy as above, you will have to replace the last line by:
</p>
<pre>socks5 127.0.0.1 8080
</pre>
<p>Then, <i>proxychains-ng</i> can be launched with 
</p>
<pre>proxychains &lt;program&gt;
</pre>
<p>Where &lt;program&gt; can be any program already installed on your system (e.g. xterm, gnome-terminal, etc).
</p><p>If using <i>tsocks</i>, the configuration takes place in <code>/etc/tsocks.conf</code>. See <a href="https://jlk.fjfi.cvut.cz/arch/manpages/man/tsocks.conf.5" target="_blank">tsocks.conf(5)</a> for the options. An example minimum configuration looks like this:
</p>
<pre>/etc/tsocks.conf</pre>
<pre>server = 127.0.0.1
server_port = 8080
server_type = 5</pre>
<h3>curl and pacman</h3>
<p>You may set the <code>all_proxy</code> environment variable to let curl and pacman (which uses curl) use your socks5 proxy:
</p>
<pre>$ export all_proxy="socks5://your.proxy:1080"</pre>
<h2>Proxy settings on GNOME3</h2>
<p>Some programs like <a href="/index.php/Chromium" title="Chromium" target="_blank">Chromium</a> prefer to use the settings stored by gnome. These settings can be modified through the gnome-control-center front end and also through gsettings.
</p>
<pre>gsettings set org.gnome.system.proxy mode 'manual' 
gsettings set org.gnome.system.proxy.http host 'proxy.localdomain.com'
gsettings set org.gnome.system.proxy.http port 8080
gsettings set org.gnome.system.proxy.ftp host 'proxy.localdomain.com'
gsettings set org.gnome.system.proxy.ftp port 8080
gsettings set org.gnome.system.proxy.https host 'proxy.localdomain.com'
gsettings set org.gnome.system.proxy.https port 8080
gsettings set org.gnome.system.proxy ignore-hosts "['localhost', '127.0.0.0/8', '10.0.0.0/8', '192.168.0.0/16', '172.16.0.0/12' , '*.localdomain.com' ]"
</pre>
<p>This configuration can also be set to automatically execute when <a href="/index.php/NetworkManager#Proxy_settings" title="NetworkManager" target="_blank">Network Manager</a> connects to specific networks , by using the package <a href="https://aur.archlinux.org/packages/proxydriver/" target="_blank">proxydriver</a><sup><small>AUR</small></sup> from the <a href="/index.php/AUR" title="AUR" target="_blank">AUR</a>
</p>
<h2>Microsoft NTLM proxy</h2>
<p>In a Windows network, NT LAN Manager (NTLM) is a suite of Microsoft security protocols which provides authentication, integrity, and confidentiality to users.  
</p><p><a href="https://aur.archlinux.org/packages/cntlm/" target="_blank">cntlm</a><sup><small>AUR</small></sup> from the <a href="/index.php/AUR" title="AUR" target="_blank">AUR</a> stands between your applications and the NTLM proxy, adding NTLM authentication on-the-fly. You can specify several "parent" proxies and Cntlm will try one after another until one works. All authenticated connections are cached and reused to achieve high efficiency.
</p>
<pre>(NTLM PROXY IP:PORT + CREDENTIALS + OTHER INFO) -----&gt; <b>(127.0.0.1:PORT)</b>
</pre>
<h3>Configuration</h3>
<p>Change settings in <code>/etc/cntlm.conf</code> as needed, except for the password. Then run:
</p>
<pre>$ cntlm -H
</pre>
<p>This will generate encrypted password hashes according to your proxy hostname, username and password.
</p>
<div><strong>Warning:</strong> <a href="https://www.archlinux.org/packages/?name=ettercap" target="_blank">ettercap</a> can easily sniff your password over LAN when using plain-text passwords instead of encrypted hashes.</div>
<p>Edit <code>/etc/cntlm.conf</code> again and include all three generated hashes, then <a href="/index.php/Enable" title="Enable" target="_blank">enable</a> <code>cntlm.service</code>.
</p><p>To test settings, run:
</p>
<pre>$ cntlm -v
</pre>
<h3>Usage</h3>
<p>Use <code>127.0.0.1:&lt;port&gt;</code> or <code>localhost:&lt;port&gt;</code> as a proxy adress. <code>&lt;port&gt;</code> matches the <code>Listen</code> parameter in <code>/etc/cntlm.conf</code>, which by default is <code>3128</code>.
</p>


