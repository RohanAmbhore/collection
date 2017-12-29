<a href="https://gist.github.com/saetia/1623487">https://gist.github.com/saetia/1623487</a><div id="articleHeader"><h1>Clean Install – OS X 10.11 El Capitan</h1></div>
    <div>
  <div>
    Clean Install – OS X 10.11 El Capitan
  </div>
</div>


        
  
      
    
  
    <h3>OS X Preferences</h3>
<hr />
<p>most of these require logout/restart to take effect</p>
<div><pre># Enable character repeat on keydown
defaults write -g ApplePressAndHoldEnabled -bool false

# Set a shorter Delay until key repeat
defaults write NSGlobalDomain InitialKeyRepeat -int 12

# Set a blazingly fast keyboard repeat rate
defaults write NSGlobalDomain KeyRepeat -int 0

# Disable window animations ("new window" scale effect)
defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false

# Turn on dashboard-as-space
defaults write com.apple.dashboard enabled-state 2

# Use plain text mode for new TextEdit documents
defaults write com.apple.TextEdit RichText -int 0

# Make top-right hotspot start screensaver
defaults write com.apple.dock wvous-tr-corner -int 5 && \
defaults write com.apple.dock wvous-tr-modifier -int 0

# Set default Finder location to home folder (~/)
defaults write com.apple.finder NewWindowTarget -string "PfLo" && \
defaults write com.apple.finder NewWindowTargetPath -string "file://${HOME}"

# Expand save panel by default
defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode -bool true

# Disable ext change warning
defaults write com.apple.finder FXEnableExtensionChangeWarning -bool false

# Check for software updates daily, not just once per week
defaults write com.apple.SoftwareUpdate ScheduleFrequency -int 1

# Use current directory as default search scope in Finder
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

# Show Path bar in Finder
defaults write com.apple.finder ShowPathbar -bool true

# Show Status bar in Finder
defaults write com.apple.finder ShowStatusBar -bool true

# Show icons for hard drives, servers, and removable media on the desktop
defaults write com.apple.finder ShowExternalHardDrivesOnDesktop -bool true && \
defaults write com.apple.finder ShowHardDrivesOnDesktop -bool true && \
defaults write com.apple.finder ShowMountedServersOnDesktop -bool true && \
defaults write com.apple.finder ShowRemovableMediaOnDesktop -bool true

# Avoid creating .DS_Store files on network volumes
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true

# Disable disk image verification
defaults write com.apple.frameworks.diskimages skip-verify -bool true && \
defaults write com.apple.frameworks.diskimages skip-verify-locked -bool true && \
defaults write com.apple.frameworks.diskimages skip-verify-remote -bool true

# Trackpad: map bottom right corner to right-click
defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadCornerSecondaryClick -int 2 && \
defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadRightClick -bool true && \
defaults -currentHost write NSGlobalDomain com.apple.trackpad.trackpadCornerClickBehavior -int 1 && \
defaults -currentHost write NSGlobalDomain com.apple.trackpad.enableSecondaryClick -bool true

# Enable the Develop menu and the Web Inspector in Safari
defaults write com.apple.Safari IncludeInternalDebugMenu -bool true && \
defaults write com.apple.Safari IncludeDevelopMenu -bool true && \
defaults write com.apple.Safari WebKitDeveloperExtrasEnabledPreferenceKey -bool true && \
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2DeveloperExtrasEnabled -bool true && \
defaults write NSGlobalDomain WebKitDeveloperExtras -bool true

# Show the ~/Library folder
chflags nohidden ~/Library

# Show absolute path in finder's title bar. 
defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES

# Auto-play videos when opened with QuickTime Player
defaults write com.apple.QuickTimePlayerX MGPlayMovieOnOpen 1

# Enable AirDrop over Ethernet and on unsupported Macs
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool true

# Disable WebkitNightly.app's homepage
defaults write org.webkit.nightly.WebKit StartPageDisabled -bool true
</pre></div>
<p>###Shell</p>
<hr />
<p>####Switch to z-shell</p>
<div><pre>curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh</pre></div>
<p>####Homebrew</p>
<div><pre># install package manager
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# install homebrew packages
brew install \
tree \
node \
ssh-copy-id \
wget \
jpegoptim \
pngcrush \
colordiff \
ghostscript \
imagemagick --with-ghostscript \
graphicsmagick \
ack</pre></div>
<p>####Homebrew Web Server Packages</p>
<div><pre>brew install \
dnsmasq \
nginx \
mariadb \
redis \
memcached \
libmemcached \</pre></div>
<p>####Homebrew Cask Apps & Fonts</p>
<div><pre># add support for fonts
brew tap caskroom/fonts

#add dev/beta versions
brew tap caskroom/versions

#install mac apps & fonts
brew cask install \
font-source-code-pro \
adobe-creative-cloud \
blueharvest \
cleanmymac \
cocktail \
ghostlab \
coda \
sublime-text-dev \
virtualbox \
coderunner \
google-chrome \
firefox \
codekit \
iterm2-beta \
sequel-pro \
querious \
imageoptim \
imagealpha \
xquartz \
simpholders-2-alpha \
handbrake \
vagrant \
ksdiff \
spotify</pre></div>
<p>####Update .zshrc</p>
<div><pre>wget https://gist.githubusercontent.com/saetia/2764210/raw/ab099b587689640eb32cbc1afdb6a19b62be7fb0/.zshrc -O \
~/.zshrc

#syntax highlighting
git clone git://github.com/zsh-users/zsh-syntax-highlighting.git \
~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting</pre></div>
<p>####Set hostname</p>
<div><pre>sudo scutil --set HostName Work</pre></div>
<p>###Agree To Xcode</p>
<div><pre>sudo xcrun cc</pre></div>
<p>###Git</p>
<hr />
<p>####Setup Github</p>
<div><pre>ssh-keygen -t rsa -C "saetia@gmail.com"

#copy ssh key to clipboard for adding to github.com
pbcopy &lt; ~/.ssh/id_rsa.pub

#test connection
ssh -T git@github.com

#set git config values
git config --global user.name "Joel Glovacki" && \
git config --global user.email "saetia@gmail.com" && \
git config --global github.user saetia && \
git config --global core.editor "subl -w" && \
git config --global color.ui true && \
git config --global push.default simple

#token
git config --global github.token your_token_here</pre></div>
<div><pre>#diff-so-fancy
brew install diff-so-fancy
git config --global pager.diff "diff-so-fancy | less --tabs=4 -RFX" && \
git config --global pager.show "diff-so-fancy | less --tabs=4 -RFX"</pre></div>
<p>###Coda</p>
<hr />
<p>####Install markdown support</p>
<div><pre>git clone https://github.com/bobthecow/Markdown.mode.git \
~/Library/Application\ Support/Coda\ 2/modes/Markdown.mode</pre></div>
<p>###Sublime Text</p>
<hr />
<p>####Install Soda Theme</p>
<div><pre>git clone git://github.com/buymeasoda/soda-theme.git \
~/Library/Application\ Support/Sublime\ Text\ 3/Packages/Theme\ -\ Soda</pre></div>
<p>####Install Tomorrow Night Eighties Themes</p>
<div><pre>#Sublime Text
git clone git://github.com/chriskempson/textmate-tomorrow-theme.git \
~/Library/Application\ Support/Sublime\ Text\ 3/Packages/Color\ Scheme\ -\ Tomorrow

#iTerm2
wget https://raw.githubusercontent.com/mbadolato/iTerm2-Color-Schemes/master/schemes/Tomorrow%20Night%20Eighties.itermcolors \
-O ~/Downloads/Tomorrow\ Night\ Eighties.itermcolors && open ~/Downloads/Tomorrow\ Night\ Eighties.itermcolors

#Xcode
mkdir -p ~/Library/Developer/Xcode/UserData/FontAndColorThemes && \
wget https://raw.githubusercontent.com/chriskempson/tomorrow-theme/master/Xcode%204/Tomorrow%20Night%20Eighties.dvtcolortheme -O \
~/Library/Developer/Xcode/UserData/FontAndColorThemes/Tomorrow\ Night\ Eighties.dvtcolortheme</pre></div>
<p>####Settings</p>
<div><pre>{
	"close_windows_when_empty": true,
	"color_scheme": "Packages/Color Scheme - Tomorrow/Tomorrow-Night-Eighties.tmTheme",
	"draw_indent_guides": false,
	"font_face": "Source Code Pro",
	"font_size": 22.0,
	"highlight_modified_tabs": true,
	"ignored_packages":
	[
		"Vintage"
	],
	"show_full_path": true,
	"show_tab_close_buttons": false,
	"spell_check": false,
	"tab_size": 2,
	"theme": "Soda Light.sublime-theme",
	"word_separators": "./\\()\"'-:,.;&lt;&gt;~!@#%^&*|+=[]{}`~?"
}
</pre></div>
<p>####Key Bindings</p>
<div><pre>[
	{ "keys": ["super+b"], "command": "expand_selection", "args": {"to": "brackets"} },
	{ "keys": ["super+f"], "command": "show_panel", "args": {"panel": "replace"} },
	{ "keys": ["super+alt+f"], "command": "show_panel", "args": {"panel": "find"} }
]</pre></div>
<p>####Snippets</p>
<div><pre>git clone git@github.com:co-b/sublime-snippets.git \
~/Library/Application\ Support/Sublime\ Text\ 3/Packages/CoB</pre></div>

<hr />
<div><pre>sudo gem install cocoapods
pod setup</pre></div>

<hr />
<h4>Ruby version manager</h4>
<div><pre>curl -L https://get.rvm.io | bash -s stable --rails</pre></div>

<div><pre>gem install pygmentize growl guard guard-phpunit bropages</pre></div>

<hr />
<h4>Packages</h4>
<div><pre>npm install -g coffee-script bower</pre></div>
<h3>Vagrant</h3>
<hr />
<div><pre>vagrant plugin install vagrant-hostsupdater</pre></div>

<hr />
<div><pre>#switch from SecureTransport
brew reinstall --with-openssl curl

#install php-fpm
brew tap homebrew/dupes && \
brew tap homebrew/versions && \
brew tap homebrew/dupes && \
brew install php70 \
--with-fpm \
--without-apache \
--with-mysql \
--with-homebrew-curl \
--with-homebrew-openssl \ 
--without-snmp

#setup daemon
ln -sfv /usr/local/opt/php70/*.plist ~/Library/LaunchAgents && \
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.php70.plist</pre></div>
<p>####PHP-Redis</p>
<div><pre>#brew install php70-redis
brew install --HEAD homebrew/php/php70-redis</pre></div>
<p>####Imagemagick</p>
<div><pre>brew install homebrew/php/php70-imagick</pre></div>
<p>####MariaDB</p>
<div><pre>#setup daemon
ln -sfv /usr/local/opt/mariadb/*.plist ~/Library/LaunchAgents && \
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mariadb.plist

#initial setup
mysql_install_db

#secure mariadb
mysql_secure_installation</pre></div>
<p>####NGINX</p>
<div><pre>sudo cp -v /usr/local/opt/nginx/*.plist /Library/LaunchDaemons/ && 
sudo chown root:wheel /Library/LaunchDaemons/homebrew.mxcl.nginx.plist &&
sudo launchctl load /Library/LaunchDaemons/homebrew.mxcl.nginx.plist</pre></div>
<h3>Local Web Server</h3>
<hr />
<h4>Add DNS Domains, Enable dnsmasq daemon</h4>
<p>This will route requests to any url ending in <strong>.build</strong> back to your own computer. The goal is to use urls like <a href="http://example.com.build" target="_blank">http://example.com.build</a> for development while you work on <a href="http://example.com" target="_blank">http://example.com</a></p>
<div><pre>mkdir -pv $(brew --prefix)/etc/ && \
echo 'address=/.build/127.0.0.1' &gt; $(brew --prefix)/etc/dnsmasq.conf && \
sudo cp -v $(brew --prefix dnsmasq)/homebrew.mxcl.dnsmasq.plist /Library/LaunchDaemons && \
sudo launchctl load -w /Library/LaunchDaemons/homebrew.mxcl.dnsmasq.plist && \
sudo mkdir -v /etc/resolver && \
sudo zsh -c 'echo "nameserver 127.0.0.1" &gt; /etc/resolver/build'

#flush cache
sudo discoveryutil mdnsflushcache && scutil --dns</pre></div>
<p>####Enable virtual hosts</p>
<p>This will allow you to serve folders under ~/Sites/ as websites.</p>
<ul>
<li>~/Sites
<ul>
<li>example.com
<ul>
<li>htdocs
<ul>
<li>index.html</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<p>to access this site, visit <a href="http://example.com.build" target="_blank">http://example.com.build</a></p>
<p>####Match production server paths</p>
<div><pre>sudo mkdir -p /var/ && sudo ln -s ~/Sites /var/www</pre></div>
<p><a href="https://camo.githubusercontent.com/de0dc056fd00df2afb9e367c62b1776bd85e6456/687474703a2f2f692e696d6775722e636f6d2f416d4661782e676966" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://camo.githubusercontent.com/de0dc056fd00df2afb9e367c62b1776bd85e6456/687474703a2f2f692e696d6775722e636f6d2f416d4661782e676966" alt="aww yeah" /></div></a></p>
