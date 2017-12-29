<a href="https://gist.github.com/brandonb927/3195465">https://gist.github.com/brandonb927/3195465</a><div id="articleHeader"><h1>Yosemite/El Capitan Edition. This script tries not to be *too* opinionated and any major changes to your system require a prompt. You've been warned.</h1></div>
    <div>
  <div>
    OSX for Hackers: Yosemite/El Capitan Edition. This script tries not to be *too* opinionated and any major changes to your system require a prompt. You've been warned.
  </div>
</div>


        
  
      
    

  
      <table>
      <tbody><tr>
        <td id="file-osx-for-hackers-sh-L1"></td>
        <td id="file-osx-for-hackers-sh-LC1">#!/bin/sh</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L4"></td>
        <td id="file-osx-for-hackers-sh-LC4"># SOME COMMANDS WILL NOT WORK ON macOS (Sierra or newer)</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L5"></td>
        <td id="file-osx-for-hackers-sh-LC5"># For Sierra or newer, see https://github.com/mathiasbynens/dotfiles/blob/master/.macos</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L8"></td>
        <td id="file-osx-for-hackers-sh-LC8"># Alot of these configs have been taken from the various places</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L9"></td>
        <td id="file-osx-for-hackers-sh-LC9"># on the web, most from here</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L10"></td>
        <td id="file-osx-for-hackers-sh-LC10"># https://github.com/mathiasbynens/dotfiles/blob/5b3c8418ed42d93af2e647dc9d122f25cc034871/.osx</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L12"></td>
        <td id="file-osx-for-hackers-sh-LC12"># Set the colours you can use</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L13"></td>
        <td id="file-osx-for-hackers-sh-LC13">black='\033[0;30m'</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L14"></td>
        <td id="file-osx-for-hackers-sh-LC14">white='\033[0;37m'</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L15"></td>
        <td id="file-osx-for-hackers-sh-LC15">red='\033[0;31m'</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L16"></td>
        <td id="file-osx-for-hackers-sh-LC16">green='\033[0;32m'</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L17"></td>
        <td id="file-osx-for-hackers-sh-LC17">yellow='\033[0;33m'</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L18"></td>
        <td id="file-osx-for-hackers-sh-LC18">blue='\033[0;34m'</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L19"></td>
        <td id="file-osx-for-hackers-sh-LC19">magenta='\033[0;35m'</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L20"></td>
        <td id="file-osx-for-hackers-sh-LC20">cyan='\033[0;36m'</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L22"></td>
        <td id="file-osx-for-hackers-sh-LC22"># Resets the style</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L23"></td>
        <td id="file-osx-for-hackers-sh-LC23">reset=`tput sgr0`</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L25"></td>
        <td id="file-osx-for-hackers-sh-LC25"># Color-echo. Improved. [Thanks @joaocunha]</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L26"></td>
        <td id="file-osx-for-hackers-sh-LC26"># arg $1 = message</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L27"></td>
        <td id="file-osx-for-hackers-sh-LC27"># arg $2 = Color</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L28"></td>
        <td id="file-osx-for-hackers-sh-LC28">cecho() {</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L29"></td>
        <td id="file-osx-for-hackers-sh-LC29">  echo "${2}${1}${reset}"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L30"></td>
        <td id="file-osx-for-hackers-sh-LC30">  return</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L33"></td>
        <td id="file-osx-for-hackers-sh-LC33"># Set continue to false by default</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L34"></td>
        <td id="file-osx-for-hackers-sh-LC34">CONTINUE=false</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L36"></td>
        <td id="file-osx-for-hackers-sh-LC36">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L37"></td>
        <td id="file-osx-for-hackers-sh-LC37">cecho "###############################################" $red</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L38"></td>
        <td id="file-osx-for-hackers-sh-LC38">cecho "#        DO NOT RUN THIS SCRIPT BLINDLY       #" $red</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L39"></td>
        <td id="file-osx-for-hackers-sh-LC39">cecho "#         YOU'LL PROBABLY REGRET IT...        #" $red</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L40"></td>
        <td id="file-osx-for-hackers-sh-LC40">cecho "#                                             #" $red</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L41"></td>
        <td id="file-osx-for-hackers-sh-LC41">cecho "#              READ IT THOROUGHLY             #" $red</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L42"></td>
        <td id="file-osx-for-hackers-sh-LC42">cecho "#         AND EDIT TO SUIT YOUR NEEDS         #" $red</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L43"></td>
        <td id="file-osx-for-hackers-sh-LC43">cecho "###############################################" $red</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L44"></td>
        <td id="file-osx-for-hackers-sh-LC44">echo ""</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L47"></td>
        <td id="file-osx-for-hackers-sh-LC47">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L48"></td>
        <td id="file-osx-for-hackers-sh-LC48">cecho "Have you read through the script you're about to run and " $red</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L49"></td>
        <td id="file-osx-for-hackers-sh-LC49">cecho "understood that it will make changes to your computer? (y/n)" $red</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L50"></td>
        <td id="file-osx-for-hackers-sh-LC50">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L51"></td>
        <td id="file-osx-for-hackers-sh-LC51">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L52"></td>
        <td id="file-osx-for-hackers-sh-LC52">  CONTINUE=true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L55"></td>
        <td id="file-osx-for-hackers-sh-LC55">if ! $CONTINUE; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L56"></td>
        <td id="file-osx-for-hackers-sh-LC56">  # Check if we're continuing and output a message if not</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L57"></td>
        <td id="file-osx-for-hackers-sh-LC57">  cecho "Please go read the script, it only takes a few minutes" $red</td>
      </tr>
      
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L61"></td>
        <td id="file-osx-for-hackers-sh-LC61"># Here we go.. ask for the administrator password upfront and run a</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L62"></td>
        <td id="file-osx-for-hackers-sh-LC62"># keep-alive to update existing `sudo` time stamp until script has finished</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L63"></td>
        <td id="file-osx-for-hackers-sh-LC63">sudo -v</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L64"></td>
        <td id="file-osx-for-hackers-sh-LC64">while true; do sudo -n true; sleep 60; kill -0 "$$" || exit; done 2&gt;/dev/null &</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L66"></td>
        <td id="file-osx-for-hackers-sh-LC66">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L67"></td>
        <td id="file-osx-for-hackers-sh-LC67"># General UI/UX</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L68"></td>
        <td id="file-osx-for-hackers-sh-LC68">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L70"></td>
        <td id="file-osx-for-hackers-sh-LC70">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L71"></td>
        <td id="file-osx-for-hackers-sh-LC71">echo "Would you like to set your computer name (as done via System Preferences &gt;&gt; Sharing)?  (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L72"></td>
        <td id="file-osx-for-hackers-sh-LC72">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L73"></td>
        <td id="file-osx-for-hackers-sh-LC73">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L74"></td>
        <td id="file-osx-for-hackers-sh-LC74">  echo "What would you like it to be?"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L75"></td>
        <td id="file-osx-for-hackers-sh-LC75">  read COMPUTER_NAME</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L76"></td>
        <td id="file-osx-for-hackers-sh-LC76">  sudo scutil --set ComputerName $COMPUTER_NAME</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L77"></td>
        <td id="file-osx-for-hackers-sh-LC77">  sudo scutil --set HostName $COMPUTER_NAME</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L78"></td>
        <td id="file-osx-for-hackers-sh-LC78">  sudo scutil --set LocalHostName $COMPUTER_NAME</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L79"></td>
        <td id="file-osx-for-hackers-sh-LC79">  sudo defaults write /Library/Preferences/SystemConfiguration/com.apple.smb.server NetBIOSName -string $COMPUTER_NAME</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L82"></td>
        <td id="file-osx-for-hackers-sh-LC82">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L83"></td>
        <td id="file-osx-for-hackers-sh-LC83">echo "Hide the Time Machine, Volume, User, and Bluetooth icons?  (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L84"></td>
        <td id="file-osx-for-hackers-sh-LC84">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L85"></td>
        <td id="file-osx-for-hackers-sh-LC85">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L86"></td>
        <td id="file-osx-for-hackers-sh-LC86">  # Get the system Hardware UUID and use it for the next menubar stuff</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L87"></td>
        <td id="file-osx-for-hackers-sh-LC87">  for domain in ~/Library/Preferences/ByHost/com.apple.systemuiserver.*; do</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L88"></td>
        <td id="file-osx-for-hackers-sh-LC88">    defaults write "${domain}" dontAutoLoad -array \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L89"></td>
        <td id="file-osx-for-hackers-sh-LC89">      "/System/Library/CoreServices/Menu Extras/TimeMachine.menu" \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L90"></td>
        <td id="file-osx-for-hackers-sh-LC90">      "/System/Library/CoreServices/Menu Extras/Volume.menu" \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L91"></td>
        <td id="file-osx-for-hackers-sh-LC91">      "/System/Library/CoreServices/Menu Extras/User.menu"</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L94"></td>
        <td id="file-osx-for-hackers-sh-LC94">  defaults write com.apple.systemuiserver menuExtras -array \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L95"></td>
        <td id="file-osx-for-hackers-sh-LC95">    "/System/Library/CoreServices/Menu Extras/Bluetooth.menu" \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L96"></td>
        <td id="file-osx-for-hackers-sh-LC96">    "/System/Library/CoreServices/Menu Extras/AirPort.menu" \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L97"></td>
        <td id="file-osx-for-hackers-sh-LC97">    "/System/Library/CoreServices/Menu Extras/Battery.menu" \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L98"></td>
        <td id="file-osx-for-hackers-sh-LC98">    "/System/Library/CoreServices/Menu Extras/Clock.menu"</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L101"></td>
        <td id="file-osx-for-hackers-sh-LC101">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L102"></td>
        <td id="file-osx-for-hackers-sh-LC102">echo "Hide the Spotlight icon? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L103"></td>
        <td id="file-osx-for-hackers-sh-LC103">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L104"></td>
        <td id="file-osx-for-hackers-sh-LC104">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L105"></td>
        <td id="file-osx-for-hackers-sh-LC105">  sudo chmod 600 /System/Library/CoreServices/Search.bundle/Contents/MacOS/Search</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L108"></td>
        <td id="file-osx-for-hackers-sh-LC108">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L109"></td>
        <td id="file-osx-for-hackers-sh-LC109">echo "Disable Spotlight indexing for any volume that gets mounted and has not yet been indexed before? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L110"></td>
        <td id="file-osx-for-hackers-sh-LC110">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L111"></td>
        <td id="file-osx-for-hackers-sh-LC111">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L112"></td>
        <td id="file-osx-for-hackers-sh-LC112">  echo 'Use `sudo mdutil -i off "/Volumes/foo"` to stop indexing any volume.'</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L113"></td>
        <td id="file-osx-for-hackers-sh-LC113">  sudo defaults write /.Spotlight-V100/VolumeConfiguration Exclusions -array "/Volumes"</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L116"></td>
        <td id="file-osx-for-hackers-sh-LC116">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L117"></td>
        <td id="file-osx-for-hackers-sh-LC117">echo "Change indexing order and disable some search results in Spotlight? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L118"></td>
        <td id="file-osx-for-hackers-sh-LC118">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L119"></td>
        <td id="file-osx-for-hackers-sh-LC119">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L120"></td>
        <td id="file-osx-for-hackers-sh-LC120">  # Yosemite-specific search results (remove them if your are using OS X 10.9 or older):</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L121"></td>
        <td id="file-osx-for-hackers-sh-LC121">  #   MENU_DEFINITION</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L122"></td>
        <td id="file-osx-for-hackers-sh-LC122">  #   MENU_CONVERSION</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L123"></td>
        <td id="file-osx-for-hackers-sh-LC123">  #   MENU_EXPRESSION</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L124"></td>
        <td id="file-osx-for-hackers-sh-LC124">  #   MENU_SPOTLIGHT_SUGGESTIONS (send search queries to Apple)</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L125"></td>
        <td id="file-osx-for-hackers-sh-LC125">  #   MENU_WEBSEARCH             (send search queries to Apple)</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L126"></td>
        <td id="file-osx-for-hackers-sh-LC126">  #   MENU_OTHER</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L127"></td>
        <td id="file-osx-for-hackers-sh-LC127">  defaults write com.apple.spotlight orderedItems -array \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L128"></td>
        <td id="file-osx-for-hackers-sh-LC128">    '{"enabled" = 1;"name" = "APPLICATIONS";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L129"></td>
        <td id="file-osx-for-hackers-sh-LC129">    '{"enabled" = 1;"name" = "SYSTEM_PREFS";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L130"></td>
        <td id="file-osx-for-hackers-sh-LC130">    '{"enabled" = 1;"name" = "DIRECTORIES";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L131"></td>
        <td id="file-osx-for-hackers-sh-LC131">    '{"enabled" = 1;"name" = "PDF";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L132"></td>
        <td id="file-osx-for-hackers-sh-LC132">    '{"enabled" = 1;"name" = "FONTS";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L133"></td>
        <td id="file-osx-for-hackers-sh-LC133">    '{"enabled" = 0;"name" = "DOCUMENTS";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L134"></td>
        <td id="file-osx-for-hackers-sh-LC134">    '{"enabled" = 0;"name" = "MESSAGES";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L135"></td>
        <td id="file-osx-for-hackers-sh-LC135">    '{"enabled" = 0;"name" = "CONTACT";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L136"></td>
        <td id="file-osx-for-hackers-sh-LC136">    '{"enabled" = 0;"name" = "EVENT_TODO";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L137"></td>
        <td id="file-osx-for-hackers-sh-LC137">    '{"enabled" = 0;"name" = "IMAGES";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L138"></td>
        <td id="file-osx-for-hackers-sh-LC138">    '{"enabled" = 0;"name" = "BOOKMARKS";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L139"></td>
        <td id="file-osx-for-hackers-sh-LC139">    '{"enabled" = 0;"name" = "MUSIC";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L140"></td>
        <td id="file-osx-for-hackers-sh-LC140">    '{"enabled" = 0;"name" = "MOVIES";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L141"></td>
        <td id="file-osx-for-hackers-sh-LC141">    '{"enabled" = 0;"name" = "PRESENTATIONS";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L142"></td>
        <td id="file-osx-for-hackers-sh-LC142">    '{"enabled" = 0;"name" = "SPREADSHEETS";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L143"></td>
        <td id="file-osx-for-hackers-sh-LC143">    '{"enabled" = 0;"name" = "SOURCE";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L144"></td>
        <td id="file-osx-for-hackers-sh-LC144">    '{"enabled" = 0;"name" = "MENU_DEFINITION";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L145"></td>
        <td id="file-osx-for-hackers-sh-LC145">    '{"enabled" = 0;"name" = "MENU_OTHER";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L146"></td>
        <td id="file-osx-for-hackers-sh-LC146">    '{"enabled" = 0;"name" = "MENU_CONVERSION";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L147"></td>
        <td id="file-osx-for-hackers-sh-LC147">    '{"enabled" = 0;"name" = "MENU_EXPRESSION";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L148"></td>
        <td id="file-osx-for-hackers-sh-LC148">    '{"enabled" = 0;"name" = "MENU_WEBSEARCH";}' \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L149"></td>
        <td id="file-osx-for-hackers-sh-LC149">    '{"enabled" = 0;"name" = "MENU_SPOTLIGHT_SUGGESTIONS";}'</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L150"></td>
        <td id="file-osx-for-hackers-sh-LC150">  # Load new settings before rebuilding the index</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L151"></td>
        <td id="file-osx-for-hackers-sh-LC151">  killall mds &gt; /dev/null 2&gt;&1</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L152"></td>
        <td id="file-osx-for-hackers-sh-LC152">  # Make sure indexing is enabled for the main volume</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L153"></td>
        <td id="file-osx-for-hackers-sh-LC153">  sudo mdutil -i on / &gt; /dev/null</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L154"></td>
        <td id="file-osx-for-hackers-sh-LC154">  # Rebuild the index from scratch</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L155"></td>
        <td id="file-osx-for-hackers-sh-LC155">  sudo mdutil -E / &gt; /dev/null</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L158"></td>
        <td id="file-osx-for-hackers-sh-LC158">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L159"></td>
        <td id="file-osx-for-hackers-sh-LC159">echo "Expanding the save panel by default"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L160"></td>
        <td id="file-osx-for-hackers-sh-LC160">defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L161"></td>
        <td id="file-osx-for-hackers-sh-LC161">defaults write NSGlobalDomain PMPrintingExpandedStateForPrint -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L162"></td>
        <td id="file-osx-for-hackers-sh-LC162">defaults write NSGlobalDomain PMPrintingExpandedStateForPrint2 -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L164"></td>
        <td id="file-osx-for-hackers-sh-LC164">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L165"></td>
        <td id="file-osx-for-hackers-sh-LC165">echo "Automatically quit printer app once the print jobs complete"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L166"></td>
        <td id="file-osx-for-hackers-sh-LC166">defaults write com.apple.print.PrintingPrefs "Quit When Finished" -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L168"></td>
        <td id="file-osx-for-hackers-sh-LC168"># Try e.g. `cd /tmp; unidecode "\x{0000}" &gt; cc.txt; open -e cc.txt`</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L169"></td>
        <td id="file-osx-for-hackers-sh-LC169">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L170"></td>
        <td id="file-osx-for-hackers-sh-LC170">echo "Displaying ASCII control characters using caret notation in standard text views"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L171"></td>
        <td id="file-osx-for-hackers-sh-LC171">defaults write NSGlobalDomain NSTextShowsControlCharacters -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L173"></td>
        <td id="file-osx-for-hackers-sh-LC173">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L174"></td>
        <td id="file-osx-for-hackers-sh-LC174">echo "Save to disk, rather than iCloud, by default? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L175"></td>
        <td id="file-osx-for-hackers-sh-LC175">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L176"></td>
        <td id="file-osx-for-hackers-sh-LC176">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L177"></td>
        <td id="file-osx-for-hackers-sh-LC177">  defaults write NSGlobalDomain NSDocumentSaveNewDocumentsToCloud -bool false</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L180"></td>
        <td id="file-osx-for-hackers-sh-LC180">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L181"></td>
        <td id="file-osx-for-hackers-sh-LC181">echo "Reveal IP address, hostname, OS version, etc. when clicking the clock in the login window"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L182"></td>
        <td id="file-osx-for-hackers-sh-LC182">sudo defaults write /Library/Preferences/com.apple.loginwindow AdminHostInfo HostName</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L184"></td>
        <td id="file-osx-for-hackers-sh-LC184">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L185"></td>
        <td id="file-osx-for-hackers-sh-LC185">echo "Check for software updates daily, not just once per week"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L186"></td>
        <td id="file-osx-for-hackers-sh-LC186">defaults write com.apple.SoftwareUpdate ScheduleFrequency -int 1</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L188"></td>
        <td id="file-osx-for-hackers-sh-LC188">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L189"></td>
        <td id="file-osx-for-hackers-sh-LC189">echo "Removing duplicates in the 'Open With' menu"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L190"></td>
        <td id="file-osx-for-hackers-sh-LC190">/System/Library/Frameworks/CoreServices.framework/Frameworks/LaunchServices.framework/Support/lsregister -kill -r -domain local -domain system -domain user</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L192"></td>
        <td id="file-osx-for-hackers-sh-LC192">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L193"></td>
        <td id="file-osx-for-hackers-sh-LC193">echo "Disable smart quotes and smart dashes? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L194"></td>
        <td id="file-osx-for-hackers-sh-LC194">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L195"></td>
        <td id="file-osx-for-hackers-sh-LC195">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L196"></td>
        <td id="file-osx-for-hackers-sh-LC196">  defaults write NSGlobalDomain NSAutomaticQuoteSubstitutionEnabled -bool false</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L197"></td>
        <td id="file-osx-for-hackers-sh-LC197">  defaults write NSGlobalDomain NSAutomaticDashSubstitutionEnabled -bool false</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L200"></td>
        <td id="file-osx-for-hackers-sh-LC200">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L201"></td>
        <td id="file-osx-for-hackers-sh-LC201">echo "Add ability to toggle between Light and Dark mode in Yosemite using ctrl+opt+cmd+t? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L202"></td>
        <td id="file-osx-for-hackers-sh-LC202"># http://www.reddit.com/r/apple/comments/2jr6s2/1010_i_found_a_way_to_dynamically_switch_between/</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L203"></td>
        <td id="file-osx-for-hackers-sh-LC203">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L204"></td>
        <td id="file-osx-for-hackers-sh-LC204">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L205"></td>
        <td id="file-osx-for-hackers-sh-LC205">  sudo defaults write /Library/Preferences/.GlobalPreferences.plist _HIEnableThemeSwitchHotKey -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L208"></td>
        <td id="file-osx-for-hackers-sh-LC208">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L209"></td>
        <td id="file-osx-for-hackers-sh-LC209">echo "Disable Photos.app from starting everytime a device is plugged in"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L210"></td>
        <td id="file-osx-for-hackers-sh-LC210">defaults -currentHost write com.apple.ImageCapture disableHotPlug -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L213"></td>
        <td id="file-osx-for-hackers-sh-LC213">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L214"></td>
        <td id="file-osx-for-hackers-sh-LC214"># General Power and Performance modifications</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L215"></td>
        <td id="file-osx-for-hackers-sh-LC215">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L217"></td>
        <td id="file-osx-for-hackers-sh-LC217">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L218"></td>
        <td id="file-osx-for-hackers-sh-LC218">echo "Disable hibernation? (speeds up entering sleep mode) (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L219"></td>
        <td id="file-osx-for-hackers-sh-LC219">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L220"></td>
        <td id="file-osx-for-hackers-sh-LC220">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L221"></td>
        <td id="file-osx-for-hackers-sh-LC221">  sudo pmset -a hibernatemode 0</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L224"></td>
        <td id="file-osx-for-hackers-sh-LC224">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L225"></td>
        <td id="file-osx-for-hackers-sh-LC225">echo "Remove the sleep image file to save disk space? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L226"></td>
        <td id="file-osx-for-hackers-sh-LC226">echo "(If you're on a &lt;128GB SSD, this helps but can have adverse affects on performance. You've been warned.)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L227"></td>
        <td id="file-osx-for-hackers-sh-LC227">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L228"></td>
        <td id="file-osx-for-hackers-sh-LC228">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L229"></td>
        <td id="file-osx-for-hackers-sh-LC229">  sudo rm /Private/var/vm/sleepimage</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L230"></td>
        <td id="file-osx-for-hackers-sh-LC230">  echo "Creating a zero-byte file instead"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L231"></td>
        <td id="file-osx-for-hackers-sh-LC231">  sudo touch /Private/var/vm/sleepimage</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L232"></td>
        <td id="file-osx-for-hackers-sh-LC232">  echo "and make sure it can't be rewritten"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L233"></td>
        <td id="file-osx-for-hackers-sh-LC233">  sudo chflags uchg /Private/var/vm/sleepimage</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L236"></td>
        <td id="file-osx-for-hackers-sh-LC236">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L237"></td>
        <td id="file-osx-for-hackers-sh-LC237">echo "Disable the sudden motion sensor? (it's not useful for SSDs/current MacBooks) (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L238"></td>
        <td id="file-osx-for-hackers-sh-LC238">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L239"></td>
        <td id="file-osx-for-hackers-sh-LC239">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L240"></td>
        <td id="file-osx-for-hackers-sh-LC240">  sudo pmset -a sms 0</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L243"></td>
        <td id="file-osx-for-hackers-sh-LC243">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L244"></td>
        <td id="file-osx-for-hackers-sh-LC244">echo "Disable system-wide resume? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L245"></td>
        <td id="file-osx-for-hackers-sh-LC245">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L246"></td>
        <td id="file-osx-for-hackers-sh-LC246">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L247"></td>
        <td id="file-osx-for-hackers-sh-LC247">  defaults write com.apple.systempreferences NSQuitAlwaysKeepsWindows -bool false</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L250"></td>
        <td id="file-osx-for-hackers-sh-LC250">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L251"></td>
        <td id="file-osx-for-hackers-sh-LC251">echo "Disable the menubar transparency? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L252"></td>
        <td id="file-osx-for-hackers-sh-LC252">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L253"></td>
        <td id="file-osx-for-hackers-sh-LC253">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L254"></td>
        <td id="file-osx-for-hackers-sh-LC254">  defaults write com.apple.universalaccess reduceTransparency -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L257"></td>
        <td id="file-osx-for-hackers-sh-LC257">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L258"></td>
        <td id="file-osx-for-hackers-sh-LC258">echo "Speeding up wake from sleep to 24 hours from an hour"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L259"></td>
        <td id="file-osx-for-hackers-sh-LC259"># http://www.cultofmac.com/221392/quick-hack-speeds-up-retina-macbooks-wake-from-sleep-os-x-tips/</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L260"></td>
        <td id="file-osx-for-hackers-sh-LC260">sudo pmset -a standbydelay 86400</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L263"></td>
        <td id="file-osx-for-hackers-sh-LC263">################################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L264"></td>
        <td id="file-osx-for-hackers-sh-LC264"># Trackpad, mouse, keyboard, Bluetooth accessories, and input</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L265"></td>
        <td id="file-osx-for-hackers-sh-LC265">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L267"></td>
        <td id="file-osx-for-hackers-sh-LC267">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L268"></td>
        <td id="file-osx-for-hackers-sh-LC268">echo "Increasing sound quality for Bluetooth headphones/headsets"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L269"></td>
        <td id="file-osx-for-hackers-sh-LC269">defaults write com.apple.BluetoothAudioAgent "Apple Bitpool Min (editable)" -int 40</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L271"></td>
        <td id="file-osx-for-hackers-sh-LC271">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L272"></td>
        <td id="file-osx-for-hackers-sh-LC272">echo "Enabling full keyboard access for all controls (enable Tab in modal dialogs, menu windows, etc.)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L273"></td>
        <td id="file-osx-for-hackers-sh-LC273">defaults write NSGlobalDomain AppleKeyboardUIMode -int 3</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L275"></td>
        <td id="file-osx-for-hackers-sh-LC275">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L276"></td>
        <td id="file-osx-for-hackers-sh-LC276">echo "Disabling press-and-hold for special keys in favor of key repeat"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L277"></td>
        <td id="file-osx-for-hackers-sh-LC277">defaults write NSGlobalDomain ApplePressAndHoldEnabled -bool false</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L279"></td>
        <td id="file-osx-for-hackers-sh-LC279">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L280"></td>
        <td id="file-osx-for-hackers-sh-LC280">echo "Setting a blazingly fast keyboard repeat rate"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L281"></td>
        <td id="file-osx-for-hackers-sh-LC281">defaults write NSGlobalDomain KeyRepeat -int 0</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L283"></td>
        <td id="file-osx-for-hackers-sh-LC283">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L284"></td>
        <td id="file-osx-for-hackers-sh-LC284">echo "Disable auto-correct? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L285"></td>
        <td id="file-osx-for-hackers-sh-LC285">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L286"></td>
        <td id="file-osx-for-hackers-sh-LC286">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L287"></td>
        <td id="file-osx-for-hackers-sh-LC287">  defaults write NSGlobalDomain NSAutomaticSpellingCorrectionEnabled -bool false</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L290"></td>
        <td id="file-osx-for-hackers-sh-LC290">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L291"></td>
        <td id="file-osx-for-hackers-sh-LC291">echo "Setting trackpad & mouse speed to a reasonable number"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L292"></td>
        <td id="file-osx-for-hackers-sh-LC292">defaults write -g com.apple.trackpad.scaling 2</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L293"></td>
        <td id="file-osx-for-hackers-sh-LC293">defaults write -g com.apple.mouse.scaling 2.5</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L295"></td>
        <td id="file-osx-for-hackers-sh-LC295">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L296"></td>
        <td id="file-osx-for-hackers-sh-LC296">echo "Turn off keyboard illumination when computer is not used for 5 minutes"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L297"></td>
        <td id="file-osx-for-hackers-sh-LC297">defaults write com.apple.BezelServices kDimTime -int 300</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L299"></td>
        <td id="file-osx-for-hackers-sh-LC299">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L300"></td>
        <td id="file-osx-for-hackers-sh-LC300">echo "Disable display from automatically adjusting brightness? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L301"></td>
        <td id="file-osx-for-hackers-sh-LC301">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L302"></td>
        <td id="file-osx-for-hackers-sh-LC302">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L303"></td>
        <td id="file-osx-for-hackers-sh-LC303">  sudo defaults write /Library/Preferences/com.apple.iokit.AmbientLightSensor "Automatic Display Enabled" -bool false</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L306"></td>
        <td id="file-osx-for-hackers-sh-LC306">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L307"></td>
        <td id="file-osx-for-hackers-sh-LC307">echo "Disable keyboard from automatically adjusting backlight brightness in low light? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L308"></td>
        <td id="file-osx-for-hackers-sh-LC308">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L309"></td>
        <td id="file-osx-for-hackers-sh-LC309">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L310"></td>
        <td id="file-osx-for-hackers-sh-LC310">  sudo defaults write /Library/Preferences/com.apple.iokit.AmbientLightSensor "Automatic Keyboard Enabled" -bool false</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L313"></td>
        <td id="file-osx-for-hackers-sh-LC313">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L314"></td>
        <td id="file-osx-for-hackers-sh-LC314"># Screen</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L315"></td>
        <td id="file-osx-for-hackers-sh-LC315">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L317"></td>
        <td id="file-osx-for-hackers-sh-LC317">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L318"></td>
        <td id="file-osx-for-hackers-sh-LC318">echo "Requiring password immediately after sleep or screen saver begins"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L319"></td>
        <td id="file-osx-for-hackers-sh-LC319">defaults write com.apple.screensaver askForPassword -int 1</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L320"></td>
        <td id="file-osx-for-hackers-sh-LC320">defaults write com.apple.screensaver askForPasswordDelay -int 0</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L322"></td>
        <td id="file-osx-for-hackers-sh-LC322">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L323"></td>
        <td id="file-osx-for-hackers-sh-LC323">echo "Where do you want screenshots to be stored? (hit ENTER if you want ~/Desktop as default)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L324"></td>
        <td id="file-osx-for-hackers-sh-LC324"># Thanks https://github.com/omgmog</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L325"></td>
        <td id="file-osx-for-hackers-sh-LC325">read screenshot_location</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L326"></td>
        <td id="file-osx-for-hackers-sh-LC326">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L327"></td>
        <td id="file-osx-for-hackers-sh-LC327">if [ -z "${screenshot_location}" ]</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L329"></td>
        <td id="file-osx-for-hackers-sh-LC329">  # If nothing specified, we default to ~/Desktop</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L330"></td>
        <td id="file-osx-for-hackers-sh-LC330">  screenshot_location="${HOME}/Desktop"</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L332"></td>
        <td id="file-osx-for-hackers-sh-LC332">  # Otherwise we use input</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L333"></td>
        <td id="file-osx-for-hackers-sh-LC333">  if [[ "${screenshot_location:0:1}" != "/" ]]</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L335"></td>
        <td id="file-osx-for-hackers-sh-LC335">    # If input doesn't start with /, assume it's relative to home</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L336"></td>
        <td id="file-osx-for-hackers-sh-LC336">    screenshot_location="${HOME}/${screenshot_location}"</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L339"></td>
        <td id="file-osx-for-hackers-sh-LC339">echo "Setting location to ${screenshot_location}"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L340"></td>
        <td id="file-osx-for-hackers-sh-LC340">defaults write com.apple.screencapture location -string "${screenshot_location}"</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L342"></td>
        <td id="file-osx-for-hackers-sh-LC342">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L343"></td>
        <td id="file-osx-for-hackers-sh-LC343">echo "What format should screenshots be saved as? (hit ENTER for PNG, options: BMP, GIF, JPG, PDF, TIFF) "</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L344"></td>
        <td id="file-osx-for-hackers-sh-LC344">read screenshot_format</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L345"></td>
        <td id="file-osx-for-hackers-sh-LC345">if [ -z "$1" ]</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L347"></td>
        <td id="file-osx-for-hackers-sh-LC347">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L348"></td>
        <td id="file-osx-for-hackers-sh-LC348">  echo "Setting screenshot format to PNG"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L349"></td>
        <td id="file-osx-for-hackers-sh-LC349">  defaults write com.apple.screencapture type -string "png"</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L351"></td>
        <td id="file-osx-for-hackers-sh-LC351">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L352"></td>
        <td id="file-osx-for-hackers-sh-LC352">  echo "Setting screenshot format to $screenshot_format"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L353"></td>
        <td id="file-osx-for-hackers-sh-LC353">  defaults write com.apple.screencapture type -string "$screenshot_format"</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L356"></td>
        <td id="file-osx-for-hackers-sh-LC356">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L357"></td>
        <td id="file-osx-for-hackers-sh-LC357">echo "Enabling subpixel font rendering on non-Apple LCDs"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L358"></td>
        <td id="file-osx-for-hackers-sh-LC358">defaults write NSGlobalDomain AppleFontSmoothing -int 2</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L360"></td>
        <td id="file-osx-for-hackers-sh-LC360">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L361"></td>
        <td id="file-osx-for-hackers-sh-LC361">echo "Enabling HiDPI display modes (requires restart)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L362"></td>
        <td id="file-osx-for-hackers-sh-LC362">sudo defaults write /Library/Preferences/com.apple.windowserver DisplayResolutionEnabled -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L364"></td>
        <td id="file-osx-for-hackers-sh-LC364">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L365"></td>
        <td id="file-osx-for-hackers-sh-LC365"># Finder</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L366"></td>
        <td id="file-osx-for-hackers-sh-LC366">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L368"></td>
        <td id="file-osx-for-hackers-sh-LC368">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L369"></td>
        <td id="file-osx-for-hackers-sh-LC369">echo "Show icons for hard drives, servers, and removable media on the desktop? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L370"></td>
        <td id="file-osx-for-hackers-sh-LC370">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L371"></td>
        <td id="file-osx-for-hackers-sh-LC371">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L372"></td>
        <td id="file-osx-for-hackers-sh-LC372">  defaults write com.apple.finder ShowExternalHardDrivesOnDesktop -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L375"></td>
        <td id="file-osx-for-hackers-sh-LC375">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L376"></td>
        <td id="file-osx-for-hackers-sh-LC376">echo "Show hidden files in Finder by default? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L377"></td>
        <td id="file-osx-for-hackers-sh-LC377">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L378"></td>
        <td id="file-osx-for-hackers-sh-LC378">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L379"></td>
        <td id="file-osx-for-hackers-sh-LC379">  defaults write com.apple.Finder AppleShowAllFiles -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L382"></td>
        <td id="file-osx-for-hackers-sh-LC382">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L383"></td>
        <td id="file-osx-for-hackers-sh-LC383">echo "Show dotfiles in Finder by default? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L384"></td>
        <td id="file-osx-for-hackers-sh-LC384">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L385"></td>
        <td id="file-osx-for-hackers-sh-LC385">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L386"></td>
        <td id="file-osx-for-hackers-sh-LC386">  defaults write com.apple.finder AppleShowAllFiles TRUE</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L389"></td>
        <td id="file-osx-for-hackers-sh-LC389">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L390"></td>
        <td id="file-osx-for-hackers-sh-LC390">echo "Show all filename extensions in Finder by default? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L391"></td>
        <td id="file-osx-for-hackers-sh-LC391">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L392"></td>
        <td id="file-osx-for-hackers-sh-LC392">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L393"></td>
        <td id="file-osx-for-hackers-sh-LC393">  defaults write NSGlobalDomain AppleShowAllExtensions -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L396"></td>
        <td id="file-osx-for-hackers-sh-LC396">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L397"></td>
        <td id="file-osx-for-hackers-sh-LC397">echo "Show status bar in Finder by default? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L398"></td>
        <td id="file-osx-for-hackers-sh-LC398">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L399"></td>
        <td id="file-osx-for-hackers-sh-LC399">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L400"></td>
        <td id="file-osx-for-hackers-sh-LC400">  defaults write com.apple.finder ShowStatusBar -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L403"></td>
        <td id="file-osx-for-hackers-sh-LC403">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L404"></td>
        <td id="file-osx-for-hackers-sh-LC404">echo "Display full POSIX path as Finder window title? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L405"></td>
        <td id="file-osx-for-hackers-sh-LC405">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L406"></td>
        <td id="file-osx-for-hackers-sh-LC406">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L407"></td>
        <td id="file-osx-for-hackers-sh-LC407">  defaults write com.apple.finder _FXShowPosixPathInTitle -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L410"></td>
        <td id="file-osx-for-hackers-sh-LC410">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L411"></td>
        <td id="file-osx-for-hackers-sh-LC411">echo "Disable the warning when changing a file extension? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L412"></td>
        <td id="file-osx-for-hackers-sh-LC412">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L413"></td>
        <td id="file-osx-for-hackers-sh-LC413">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L414"></td>
        <td id="file-osx-for-hackers-sh-LC414">  defaults write com.apple.finder FXEnableExtensionChangeWarning -bool false</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L417"></td>
        <td id="file-osx-for-hackers-sh-LC417">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L418"></td>
        <td id="file-osx-for-hackers-sh-LC418">echo "Use column view in all Finder windows by default? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L419"></td>
        <td id="file-osx-for-hackers-sh-LC419">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L420"></td>
        <td id="file-osx-for-hackers-sh-LC420">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L421"></td>
        <td id="file-osx-for-hackers-sh-LC421">  defaults write com.apple.finder FXPreferredViewStyle Clmv</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L424"></td>
        <td id="file-osx-for-hackers-sh-LC424">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L425"></td>
        <td id="file-osx-for-hackers-sh-LC425">echo "Avoid creation of .DS_Store files on network volumes? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L426"></td>
        <td id="file-osx-for-hackers-sh-LC426">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L427"></td>
        <td id="file-osx-for-hackers-sh-LC427">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L428"></td>
        <td id="file-osx-for-hackers-sh-LC428">  defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L431"></td>
        <td id="file-osx-for-hackers-sh-LC431">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L432"></td>
        <td id="file-osx-for-hackers-sh-LC432">echo "Disable disk image verification? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L433"></td>
        <td id="file-osx-for-hackers-sh-LC433">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L434"></td>
        <td id="file-osx-for-hackers-sh-LC434">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L435"></td>
        <td id="file-osx-for-hackers-sh-LC435">  defaults write com.apple.frameworks.diskimages skip-verify -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L436"></td>
        <td id="file-osx-for-hackers-sh-LC436">  defaults write com.apple.frameworks.diskimages skip-verify-locked -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L437"></td>
        <td id="file-osx-for-hackers-sh-LC437">  defaults write com.apple.frameworks.diskimages skip-verify-remote -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L440"></td>
        <td id="file-osx-for-hackers-sh-LC440">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L441"></td>
        <td id="file-osx-for-hackers-sh-LC441">echo "Allowing text selection in Quick Look/Preview in Finder by default"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L442"></td>
        <td id="file-osx-for-hackers-sh-LC442">defaults write com.apple.finder QLEnableTextSelection -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L444"></td>
        <td id="file-osx-for-hackers-sh-LC444">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L445"></td>
        <td id="file-osx-for-hackers-sh-LC445">echo "Show item info near icons on the desktop and in other icon views? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L446"></td>
        <td id="file-osx-for-hackers-sh-LC446">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L447"></td>
        <td id="file-osx-for-hackers-sh-LC447">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L448"></td>
        <td id="file-osx-for-hackers-sh-LC448">  /usr/libexec/PlistBuddy -c "Set :DesktopViewSettings:IconViewSettings:showItemInfo true" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L449"></td>
        <td id="file-osx-for-hackers-sh-LC449">  /usr/libexec/PlistBuddy -c "Set :FK_StandardViewSettings:IconViewSettings:showItemInfo true" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L450"></td>
        <td id="file-osx-for-hackers-sh-LC450">  /usr/libexec/PlistBuddy -c "Set :StandardViewSettings:IconViewSettings:showItemInfo true" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L453"></td>
        <td id="file-osx-for-hackers-sh-LC453">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L454"></td>
        <td id="file-osx-for-hackers-sh-LC454">echo "Show item info to the right of the icons on the desktop? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L455"></td>
        <td id="file-osx-for-hackers-sh-LC455">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L456"></td>
        <td id="file-osx-for-hackers-sh-LC456">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L457"></td>
        <td id="file-osx-for-hackers-sh-LC457">  /usr/libexec/PlistBuddy -c "Set DesktopViewSettings:IconViewSettings:labelOnBottom false" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L460"></td>
        <td id="file-osx-for-hackers-sh-LC460">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L461"></td>
        <td id="file-osx-for-hackers-sh-LC461">echo "Enable snap-to-grid for icons on the desktop and in other icon views? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L462"></td>
        <td id="file-osx-for-hackers-sh-LC462">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L463"></td>
        <td id="file-osx-for-hackers-sh-LC463">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L464"></td>
        <td id="file-osx-for-hackers-sh-LC464">  /usr/libexec/PlistBuddy -c "Set :DesktopViewSettings:IconViewSettings:arrangeBy grid" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L465"></td>
        <td id="file-osx-for-hackers-sh-LC465">  /usr/libexec/PlistBuddy -c "Set :FK_StandardViewSettings:IconViewSettings:arrangeBy grid" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L466"></td>
        <td id="file-osx-for-hackers-sh-LC466">  /usr/libexec/PlistBuddy -c "Set :StandardViewSettings:IconViewSettings:arrangeBy grid" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L469"></td>
        <td id="file-osx-for-hackers-sh-LC469">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L470"></td>
        <td id="file-osx-for-hackers-sh-LC470">echo "Increase grid spacing for icons on the desktop and in other icon views? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L471"></td>
        <td id="file-osx-for-hackers-sh-LC471">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L472"></td>
        <td id="file-osx-for-hackers-sh-LC472">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L473"></td>
        <td id="file-osx-for-hackers-sh-LC473">  /usr/libexec/PlistBuddy -c "Set :DesktopViewSettings:IconViewSettings:gridSpacing 100" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L474"></td>
        <td id="file-osx-for-hackers-sh-LC474">  /usr/libexec/PlistBuddy -c "Set :FK_StandardViewSettings:IconViewSettings:gridSpacing 100" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L475"></td>
        <td id="file-osx-for-hackers-sh-LC475">  /usr/libexec/PlistBuddy -c "Set :StandardViewSettings:IconViewSettings:gridSpacing 100" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L478"></td>
        <td id="file-osx-for-hackers-sh-LC478">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L479"></td>
        <td id="file-osx-for-hackers-sh-LC479">echo "Increase the size of icons on the desktop and in other icon views? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L480"></td>
        <td id="file-osx-for-hackers-sh-LC480">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L481"></td>
        <td id="file-osx-for-hackers-sh-LC481">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L482"></td>
        <td id="file-osx-for-hackers-sh-LC482">  /usr/libexec/PlistBuddy -c "Set :DesktopViewSettings:IconViewSettings:iconSize 80" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L483"></td>
        <td id="file-osx-for-hackers-sh-LC483">  /usr/libexec/PlistBuddy -c "Set :FK_StandardViewSettings:IconViewSettings:iconSize 80" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L484"></td>
        <td id="file-osx-for-hackers-sh-LC484">  /usr/libexec/PlistBuddy -c "Set :StandardViewSettings:IconViewSettings:iconSize 80" ~/Library/Preferences/com.apple.finder.plist</td>
      </tr>
      
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L488"></td>
        <td id="file-osx-for-hackers-sh-LC488">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L489"></td>
        <td id="file-osx-for-hackers-sh-LC489"># Dock & Mission Control</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L490"></td>
        <td id="file-osx-for-hackers-sh-LC490">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L492"></td>
        <td id="file-osx-for-hackers-sh-LC492">echo "Wipe all (default) app icons from the Dock? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L493"></td>
        <td id="file-osx-for-hackers-sh-LC493">echo "(This is only really useful when setting up a new Mac, or if you don't use the Dock to launch apps.)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L494"></td>
        <td id="file-osx-for-hackers-sh-LC494">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L495"></td>
        <td id="file-osx-for-hackers-sh-LC495">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L496"></td>
        <td id="file-osx-for-hackers-sh-LC496">  defaults write com.apple.dock persistent-apps -array</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L499"></td>
        <td id="file-osx-for-hackers-sh-LC499">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L500"></td>
        <td id="file-osx-for-hackers-sh-LC500">echo "Setting the icon size of Dock items to 36 pixels for optimal size/screen-realestate"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L501"></td>
        <td id="file-osx-for-hackers-sh-LC501">defaults write com.apple.dock tilesize -int 36</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L503"></td>
        <td id="file-osx-for-hackers-sh-LC503">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L504"></td>
        <td id="file-osx-for-hackers-sh-LC504">echo "Speeding up Mission Control animations and grouping windows by application"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L505"></td>
        <td id="file-osx-for-hackers-sh-LC505">defaults write com.apple.dock expose-animation-duration -float 0.1</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L506"></td>
        <td id="file-osx-for-hackers-sh-LC506">defaults write com.apple.dock "expose-group-by-app" -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L508"></td>
        <td id="file-osx-for-hackers-sh-LC508">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L509"></td>
        <td id="file-osx-for-hackers-sh-LC509">echo "Disable the over-the-top focus ring animation"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L510"></td>
        <td id="file-osx-for-hackers-sh-LC510">defaults write NSGlobalDomain NSUseAnimatedFocusRing -bool false</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L512"></td>
        <td id="file-osx-for-hackers-sh-LC512">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L513"></td>
        <td id="file-osx-for-hackers-sh-LC513">echo "Hide the menu bar? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L514"></td>
        <td id="file-osx-for-hackers-sh-LC514">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L515"></td>
        <td id="file-osx-for-hackers-sh-LC515">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L516"></td>
        <td id="file-osx-for-hackers-sh-LC516">  defaults write "Apple Global Domain" "_HIHideMenuBar" 1</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L519"></td>
        <td id="file-osx-for-hackers-sh-LC519">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L520"></td>
        <td id="file-osx-for-hackers-sh-LC520">echo "Set Dock to auto-hide and remove the auto-hiding delay? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L521"></td>
        <td id="file-osx-for-hackers-sh-LC521">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L522"></td>
        <td id="file-osx-for-hackers-sh-LC522">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L523"></td>
        <td id="file-osx-for-hackers-sh-LC523">  defaults write com.apple.dock autohide -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L524"></td>
        <td id="file-osx-for-hackers-sh-LC524">  defaults write com.apple.dock autohide-delay -float 0</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L525"></td>
        <td id="file-osx-for-hackers-sh-LC525">  defaults write com.apple.dock autohide-time-modifier -float 0</td>
      </tr>
      
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L529"></td>
        <td id="file-osx-for-hackers-sh-LC529">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L530"></td>
        <td id="file-osx-for-hackers-sh-LC530"># Chrome, Safari, & WebKit</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L531"></td>
        <td id="file-osx-for-hackers-sh-LC531">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L533"></td>
        <td id="file-osx-for-hackers-sh-LC533">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L534"></td>
        <td id="file-osx-for-hackers-sh-LC534">echo "Privacy: Don't send search queries to Apple"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L535"></td>
        <td id="file-osx-for-hackers-sh-LC535">defaults write com.apple.Safari UniversalSearchEnabled -bool false</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L536"></td>
        <td id="file-osx-for-hackers-sh-LC536">defaults write com.apple.Safari SuppressSearchSuggestions -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L538"></td>
        <td id="file-osx-for-hackers-sh-LC538">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L539"></td>
        <td id="file-osx-for-hackers-sh-LC539">echo "Hiding Safari's bookmarks bar by default"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L540"></td>
        <td id="file-osx-for-hackers-sh-LC540">defaults write com.apple.Safari ShowFavoritesBar -bool false</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L542"></td>
        <td id="file-osx-for-hackers-sh-LC542">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L543"></td>
        <td id="file-osx-for-hackers-sh-LC543">echo "Hiding Safari's sidebar in Top Sites"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L544"></td>
        <td id="file-osx-for-hackers-sh-LC544">defaults write com.apple.Safari ShowSidebarInTopSites -bool false</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L546"></td>
        <td id="file-osx-for-hackers-sh-LC546">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L547"></td>
        <td id="file-osx-for-hackers-sh-LC547">echo "Disabling Safari's thumbnail cache for History and Top Sites"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L548"></td>
        <td id="file-osx-for-hackers-sh-LC548">defaults write com.apple.Safari DebugSnapshotsUpdatePolicy -int 2</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L550"></td>
        <td id="file-osx-for-hackers-sh-LC550">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L551"></td>
        <td id="file-osx-for-hackers-sh-LC551">echo "Enabling Safari's debug menu"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L552"></td>
        <td id="file-osx-for-hackers-sh-LC552">defaults write com.apple.Safari IncludeInternalDebugMenu -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L554"></td>
        <td id="file-osx-for-hackers-sh-LC554">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L555"></td>
        <td id="file-osx-for-hackers-sh-LC555">echo "Making Safari's search banners default to Contains instead of Starts With"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L556"></td>
        <td id="file-osx-for-hackers-sh-LC556">defaults write com.apple.Safari FindOnPageMatchesWordStartsOnly -bool false</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L558"></td>
        <td id="file-osx-for-hackers-sh-LC558">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L559"></td>
        <td id="file-osx-for-hackers-sh-LC559">echo "Removing useless icons from Safari's bookmarks bar"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L560"></td>
        <td id="file-osx-for-hackers-sh-LC560">defaults write com.apple.Safari ProxiesInBookmarksBar "()"</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L562"></td>
        <td id="file-osx-for-hackers-sh-LC562">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L563"></td>
        <td id="file-osx-for-hackers-sh-LC563">echo "Enabling the Develop menu and the Web Inspector in Safari"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L564"></td>
        <td id="file-osx-for-hackers-sh-LC564">defaults write com.apple.Safari IncludeDevelopMenu -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L565"></td>
        <td id="file-osx-for-hackers-sh-LC565">defaults write com.apple.Safari WebKitDeveloperExtrasEnabledPreferenceKey -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L566"></td>
        <td id="file-osx-for-hackers-sh-LC566">defaults write com.apple.Safari "com.apple.Safari.ContentPageGroupIdentifier.WebKit2DeveloperExtrasEnabled" -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L568"></td>
        <td id="file-osx-for-hackers-sh-LC568">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L569"></td>
        <td id="file-osx-for-hackers-sh-LC569">echo "Adding a context menu item for showing the Web Inspector in web views"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L570"></td>
        <td id="file-osx-for-hackers-sh-LC570">defaults write NSGlobalDomain WebKitDeveloperExtras -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L572"></td>
        <td id="file-osx-for-hackers-sh-LC572">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L573"></td>
        <td id="file-osx-for-hackers-sh-LC573">echo "Disabling the annoying backswipe in Chrome"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L574"></td>
        <td id="file-osx-for-hackers-sh-LC574">defaults write com.google.Chrome AppleEnableSwipeNavigateWithScrolls -bool false</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L575"></td>
        <td id="file-osx-for-hackers-sh-LC575">defaults write com.google.Chrome.canary AppleEnableSwipeNavigateWithScrolls -bool false</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L577"></td>
        <td id="file-osx-for-hackers-sh-LC577">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L578"></td>
        <td id="file-osx-for-hackers-sh-LC578">echo "Using the system-native print preview dialog in Chrome"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L579"></td>
        <td id="file-osx-for-hackers-sh-LC579">defaults write com.google.Chrome DisablePrintPreview -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L580"></td>
        <td id="file-osx-for-hackers-sh-LC580">defaults write com.google.Chrome.canary DisablePrintPreview -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L583"></td>
        <td id="file-osx-for-hackers-sh-LC583">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L584"></td>
        <td id="file-osx-for-hackers-sh-LC584"># Mail</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L585"></td>
        <td id="file-osx-for-hackers-sh-LC585">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L587"></td>
        <td id="file-osx-for-hackers-sh-LC587">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L588"></td>
        <td id="file-osx-for-hackers-sh-LC588">echo "Setting email addresses to copy as 'foo@example.com' instead of 'Foo Bar &lt;foo@example.com&gt;' in Mail.app"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L589"></td>
        <td id="file-osx-for-hackers-sh-LC589">defaults write com.apple.mail AddressesIncludeNameOnPasteboard -bool false</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L592"></td>
        <td id="file-osx-for-hackers-sh-LC592">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L593"></td>
        <td id="file-osx-for-hackers-sh-LC593"># Terminal</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L594"></td>
        <td id="file-osx-for-hackers-sh-LC594">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L596"></td>
        <td id="file-osx-for-hackers-sh-LC596">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L597"></td>
        <td id="file-osx-for-hackers-sh-LC597">echo "Enabling UTF-8 ONLY in Terminal.app and setting the Pro theme by default"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L598"></td>
        <td id="file-osx-for-hackers-sh-LC598">defaults write com.apple.terminal StringEncodings -array 4</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L599"></td>
        <td id="file-osx-for-hackers-sh-LC599">defaults write com.apple.Terminal "Default Window Settings" -string "Pro"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L600"></td>
        <td id="file-osx-for-hackers-sh-LC600">defaults write com.apple.Terminal "Startup Window Settings" -string "Pro"</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L603"></td>
        <td id="file-osx-for-hackers-sh-LC603">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L604"></td>
        <td id="file-osx-for-hackers-sh-LC604"># Time Machine</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L605"></td>
        <td id="file-osx-for-hackers-sh-LC605">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L607"></td>
        <td id="file-osx-for-hackers-sh-LC607">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L608"></td>
        <td id="file-osx-for-hackers-sh-LC608">echo "Prevent Time Machine from prompting to use new hard drives as backup volume? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L609"></td>
        <td id="file-osx-for-hackers-sh-LC609">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L610"></td>
        <td id="file-osx-for-hackers-sh-LC610">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L611"></td>
        <td id="file-osx-for-hackers-sh-LC611">  defaults write com.apple.TimeMachine DoNotOfferNewDisksForBackup -bool true</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L614"></td>
        <td id="file-osx-for-hackers-sh-LC614">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L615"></td>
        <td id="file-osx-for-hackers-sh-LC615">echo "Disable local Time Machine backups? (This can take up a ton of SSD space on &lt;128GB SSDs) (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L616"></td>
        <td id="file-osx-for-hackers-sh-LC616">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L617"></td>
        <td id="file-osx-for-hackers-sh-LC617">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L618"></td>
        <td id="file-osx-for-hackers-sh-LC618">  hash tmutil &&gt; /dev/null && sudo tmutil disablelocal</td>
      </tr>
      
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L622"></td>
        <td id="file-osx-for-hackers-sh-LC622">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L623"></td>
        <td id="file-osx-for-hackers-sh-LC623"># Messages                                                                    #</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L624"></td>
        <td id="file-osx-for-hackers-sh-LC624">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L626"></td>
        <td id="file-osx-for-hackers-sh-LC626">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L627"></td>
        <td id="file-osx-for-hackers-sh-LC627">echo "Disable automatic emoji substitution in Messages.app? (i.e. use plain text smileys) (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L628"></td>
        <td id="file-osx-for-hackers-sh-LC628">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L629"></td>
        <td id="file-osx-for-hackers-sh-LC629">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L630"></td>
        <td id="file-osx-for-hackers-sh-LC630">  defaults write com.apple.messageshelper.MessageController SOInputLineSettings -dict-add "automaticEmojiSubstitutionEnablediMessage" -bool false</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L633"></td>
        <td id="file-osx-for-hackers-sh-LC633">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L634"></td>
        <td id="file-osx-for-hackers-sh-LC634">echo "Disable smart quotes in Messages.app? (it's annoying for messages that contain code) (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L635"></td>
        <td id="file-osx-for-hackers-sh-LC635">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L636"></td>
        <td id="file-osx-for-hackers-sh-LC636">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L637"></td>
        <td id="file-osx-for-hackers-sh-LC637">  defaults write com.apple.messageshelper.MessageController SOInputLineSettings -dict-add "automaticQuoteSubstitutionEnabled" -bool false</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L640"></td>
        <td id="file-osx-for-hackers-sh-LC640">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L641"></td>
        <td id="file-osx-for-hackers-sh-LC641">echo "Disable continuous spell checking in Messages.app? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L642"></td>
        <td id="file-osx-for-hackers-sh-LC642">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L643"></td>
        <td id="file-osx-for-hackers-sh-LC643">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L644"></td>
        <td id="file-osx-for-hackers-sh-LC644">  defaults write com.apple.messageshelper.MessageController SOInputLineSettings -dict-add "continuousSpellCheckingEnabled" -bool false</td>
      </tr>
      
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L648"></td>
        <td id="file-osx-for-hackers-sh-LC648">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L649"></td>
        <td id="file-osx-for-hackers-sh-LC649"># Transmission.app                                                            #</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L650"></td>
        <td id="file-osx-for-hackers-sh-LC650">###############################################################################</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L653"></td>
        <td id="file-osx-for-hackers-sh-LC653">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L654"></td>
        <td id="file-osx-for-hackers-sh-LC654">echo "Do you use Transmission for torrenting? (y/n)"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L655"></td>
        <td id="file-osx-for-hackers-sh-LC655">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L656"></td>
        <td id="file-osx-for-hackers-sh-LC656">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L657"></td>
        <td id="file-osx-for-hackers-sh-LC657">  mkdir -p ~/Downloads/Incomplete</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L659"></td>
        <td id="file-osx-for-hackers-sh-LC659">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L660"></td>
        <td id="file-osx-for-hackers-sh-LC660">  echo "Setting up an incomplete downloads folder in Downloads"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L661"></td>
        <td id="file-osx-for-hackers-sh-LC661">  defaults write org.m0k.transmission UseIncompleteDownloadFolder -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L662"></td>
        <td id="file-osx-for-hackers-sh-LC662">  defaults write org.m0k.transmission IncompleteDownloadFolder -string "${HOME}/Downloads/Incomplete"</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L664"></td>
        <td id="file-osx-for-hackers-sh-LC664">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L665"></td>
        <td id="file-osx-for-hackers-sh-LC665">  echo "Setting auto-add folder to be Downloads"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L666"></td>
        <td id="file-osx-for-hackers-sh-LC666">  defaults write org.m0k.transmission AutoImportDirectory -string "${HOME}/Downloads"</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L668"></td>
        <td id="file-osx-for-hackers-sh-LC668">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L669"></td>
        <td id="file-osx-for-hackers-sh-LC669">  echo "Don't prompt for confirmation before downloading"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L670"></td>
        <td id="file-osx-for-hackers-sh-LC670">  defaults write org.m0k.transmission DownloadAsk -bool false</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L672"></td>
        <td id="file-osx-for-hackers-sh-LC672">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L673"></td>
        <td id="file-osx-for-hackers-sh-LC673">  echo "Trash original torrent files after adding them"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L674"></td>
        <td id="file-osx-for-hackers-sh-LC674">  defaults write org.m0k.transmission DeleteOriginalTorrent -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L676"></td>
        <td id="file-osx-for-hackers-sh-LC676">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L677"></td>
        <td id="file-osx-for-hackers-sh-LC677">  echo "Hiding the donate message"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L678"></td>
        <td id="file-osx-for-hackers-sh-LC678">  defaults write org.m0k.transmission WarningDonate -bool false</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L680"></td>
        <td id="file-osx-for-hackers-sh-LC680">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L681"></td>
        <td id="file-osx-for-hackers-sh-LC681">  echo "Hiding the legal disclaimer"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L682"></td>
        <td id="file-osx-for-hackers-sh-LC682">  defaults write org.m0k.transmission WarningLegal -bool false</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L684"></td>
        <td id="file-osx-for-hackers-sh-LC684">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L685"></td>
        <td id="file-osx-for-hackers-sh-LC685">  echo "Auto-resizing the window to fit transfers"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L686"></td>
        <td id="file-osx-for-hackers-sh-LC686">  defaults write org.m0k.transmission AutoSize -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L688"></td>
        <td id="file-osx-for-hackers-sh-LC688">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L689"></td>
        <td id="file-osx-for-hackers-sh-LC689">  echo "Auto updating to betas"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L690"></td>
        <td id="file-osx-for-hackers-sh-LC690">  defaults write org.m0k.transmission AutoUpdateBeta -bool true</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L692"></td>
        <td id="file-osx-for-hackers-sh-LC692">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L693"></td>
        <td id="file-osx-for-hackers-sh-LC693">  echo "Setting up the best block list"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L694"></td>
        <td id="file-osx-for-hackers-sh-LC694">  defaults write org.m0k.transmission EncryptionRequire -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L695"></td>
        <td id="file-osx-for-hackers-sh-LC695">  defaults write org.m0k.transmission BlocklistAutoUpdate -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L696"></td>
        <td id="file-osx-for-hackers-sh-LC696">  defaults write org.m0k.transmission BlocklistNew -bool true</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L697"></td>
        <td id="file-osx-for-hackers-sh-LC697">  defaults write org.m0k.transmission BlocklistURL -string "http://john.bitsurge.net/public/biglist.p2p.gz"</td>
      </tr>
      
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L701"></td>
        <td id="file-osx-for-hackers-sh-LC701">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L702"></td>
        <td id="file-osx-for-hackers-sh-LC702"># Sublime Text</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L703"></td>
        <td id="file-osx-for-hackers-sh-LC703">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L704"></td>
        <td id="file-osx-for-hackers-sh-LC704">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L705"></td>
        <td id="file-osx-for-hackers-sh-LC705">echo "Do you use Sublime Text 3 as your editor of choice, and is it installed?"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L706"></td>
        <td id="file-osx-for-hackers-sh-LC706">read -r response</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L707"></td>
        <td id="file-osx-for-hackers-sh-LC707">if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L708"></td>
        <td id="file-osx-for-hackers-sh-LC708">  # Installing from homebrew cask does the following for you!</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L709"></td>
        <td id="file-osx-for-hackers-sh-LC709">  # echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L710"></td>
        <td id="file-osx-for-hackers-sh-LC710">  # echo "Linking Sublime Text for command line usage as subl"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L711"></td>
        <td id="file-osx-for-hackers-sh-LC711">  # ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L713"></td>
        <td id="file-osx-for-hackers-sh-LC713">  echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L714"></td>
        <td id="file-osx-for-hackers-sh-LC714">  echo "Setting Git to use Sublime Text as default editor"</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L715"></td>
        <td id="file-osx-for-hackers-sh-LC715">  git config --global core.editor "subl -n -w"</td>
      </tr>
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L718"></td>
        <td id="file-osx-for-hackers-sh-LC718">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L719"></td>
        <td id="file-osx-for-hackers-sh-LC719"># Optional Extras</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L720"></td>
        <td id="file-osx-for-hackers-sh-LC720">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L722"></td>
        <td id="file-osx-for-hackers-sh-LC722"># Create a nice last-change git log message, from https://twitter.com/elijahmanor/status/697055097356943360</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L723"></td>
        <td id="file-osx-for-hackers-sh-LC723">git config --global alias.lastchange 'log -p --follow -n 1'</td>
      </tr>
      
      
      
      <tr>
        <td id="file-osx-for-hackers-sh-L727"></td>
        <td id="file-osx-for-hackers-sh-LC727">###############################################################################</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L728"></td>
        <td id="file-osx-for-hackers-sh-LC728"># Kill affected applications</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L729"></td>
        <td id="file-osx-for-hackers-sh-LC729">###############################################################################</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L731"></td>
        <td id="file-osx-for-hackers-sh-LC731">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L732"></td>
        <td id="file-osx-for-hackers-sh-LC732">cecho "Done!" $cyan</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L733"></td>
        <td id="file-osx-for-hackers-sh-LC733">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L734"></td>
        <td id="file-osx-for-hackers-sh-LC734">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L735"></td>
        <td id="file-osx-for-hackers-sh-LC735">cecho "################################################################################" $white</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L736"></td>
        <td id="file-osx-for-hackers-sh-LC736">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L737"></td>
        <td id="file-osx-for-hackers-sh-LC737">echo ""</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L738"></td>
        <td id="file-osx-for-hackers-sh-LC738">cecho "Note that some of these changes require a logout/restart to take effect." $red</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L739"></td>
        <td id="file-osx-for-hackers-sh-LC739">cecho "Killing some open applications in order to take effect." $red</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L740"></td>
        <td id="file-osx-for-hackers-sh-LC740">echo ""</td>
      </tr>
      
      <tr>
        <td id="file-osx-for-hackers-sh-L742"></td>
        <td id="file-osx-for-hackers-sh-LC742">find ~/Library/Application\ Support/Dock -name "*.db" -maxdepth 1 -delete</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L743"></td>
        <td id="file-osx-for-hackers-sh-LC743">for app in "Activity Monitor" "Address Book" "Calendar" "Contacts" "cfprefsd" \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L744"></td>
        <td id="file-osx-for-hackers-sh-LC744">  "Dock" "Finder" "Mail" "Messages" "Safari" "SystemUIServer" \</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L745"></td>
        <td id="file-osx-for-hackers-sh-LC745">  "Terminal" "Transmission"; do</td>
      </tr>
      <tr>
        <td id="file-osx-for-hackers-sh-L746"></td>
        <td id="file-osx-for-hackers-sh-LC746">  killall "${app}" &gt; /dev/null 2&gt;&1</td>
      </tr>
      
</tbody></table>


  