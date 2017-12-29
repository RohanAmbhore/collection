<a href="https://gist.github.com/LeCoupa/122b12050f5fb267e75f">https://gist.github.com/LeCoupa/122b12050f5fb267e75f</a><div id="articleHeader"><h1>Bash CheatSheet for UNIX Systems --> UPDATED VERSION --> https://github.com/LeCoupa/awesome-cheatsheets</h1></div>
      <table>
      <tbody><tr>
        <td id="file-bash-cheatsheet-sh-L1"></td>
        <td id="file-bash-cheatsheet-sh-LC1">#!/bin/bash</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L2"></td>
        <td id="file-bash-cheatsheet-sh-LC2">#####################################################</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L3"></td>
        <td id="file-bash-cheatsheet-sh-LC3"># Name: Bash CheatSheet for Mac OSX</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L5"></td>
        <td id="file-bash-cheatsheet-sh-LC5"># A little overlook of the Bash basics</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L7"></td>
        <td id="file-bash-cheatsheet-sh-LC7"># Usage:</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L9"></td>
        <td id="file-bash-cheatsheet-sh-LC9"># Author: J. Le Coupanec</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L10"></td>
        <td id="file-bash-cheatsheet-sh-LC10"># Date: 2014/11/04</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L11"></td>
        <td id="file-bash-cheatsheet-sh-LC11">#####################################################</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L14"></td>
        <td id="file-bash-cheatsheet-sh-LC14"># 0. Shortcuts.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L17"></td>
        <td id="file-bash-cheatsheet-sh-LC17">CTRL+A  # move to beginning of line</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L18"></td>
        <td id="file-bash-cheatsheet-sh-LC18">CTRL+B  # moves backward one character</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L19"></td>
        <td id="file-bash-cheatsheet-sh-LC19">CTRL+C  # halts the current command</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L20"></td>
        <td id="file-bash-cheatsheet-sh-LC20">CTRL+D  # deletes one character backward or logs out of current session, similar to exit</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L21"></td>
        <td id="file-bash-cheatsheet-sh-LC21">CTRL+E  # moves to end of line</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L22"></td>
        <td id="file-bash-cheatsheet-sh-LC22">CTRL+F  # moves forward one character</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L23"></td>
        <td id="file-bash-cheatsheet-sh-LC23">CTRL+G  # aborts the current editing command and ring the terminal bell</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L24"></td>
        <td id="file-bash-cheatsheet-sh-LC24">CTRL+J  # same as RETURN</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L25"></td>
        <td id="file-bash-cheatsheet-sh-LC25">CTRL+K  # deletes (kill) forward to end of line</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L26"></td>
        <td id="file-bash-cheatsheet-sh-LC26">CTRL+L  # clears screen and redisplay the line</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L27"></td>
        <td id="file-bash-cheatsheet-sh-LC27">CTRL+M  # same as RETURN</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L28"></td>
        <td id="file-bash-cheatsheet-sh-LC28">CTRL+N  # next line in command history</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L29"></td>
        <td id="file-bash-cheatsheet-sh-LC29">CTRL+O  # same as RETURN, then displays next line in history file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L30"></td>
        <td id="file-bash-cheatsheet-sh-LC30">CTRL+P  # previous line in command history</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L31"></td>
        <td id="file-bash-cheatsheet-sh-LC31">CTRL+R  # searches backward</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L32"></td>
        <td id="file-bash-cheatsheet-sh-LC32">CTRL+S  # searches forward</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L33"></td>
        <td id="file-bash-cheatsheet-sh-LC33">CTRL+T  # transposes two characters</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L34"></td>
        <td id="file-bash-cheatsheet-sh-LC34">CTRL+U  # kills backward from point to the beginning of line</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L35"></td>
        <td id="file-bash-cheatsheet-sh-LC35">CTRL+V  # makes the next character typed verbatim</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L36"></td>
        <td id="file-bash-cheatsheet-sh-LC36">CTRL+W  # kills the word behind the cursor</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L37"></td>
        <td id="file-bash-cheatsheet-sh-LC37">CTRL+X  # lists the possible filename completefions of the current word</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L38"></td>
        <td id="file-bash-cheatsheet-sh-LC38">CTRL+Y  # retrieves (yank) last item killed</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L39"></td>
        <td id="file-bash-cheatsheet-sh-LC39">CTRL+Z  # stops the current command, resume with fg in the foreground or bg in the background</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L41"></td>
        <td id="file-bash-cheatsheet-sh-LC41">DELETE  # deletes one character backward</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L42"></td>
        <td id="file-bash-cheatsheet-sh-LC42">!!      # repeats the last command</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L43"></td>
        <td id="file-bash-cheatsheet-sh-LC43">exit    # logs out of current session</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L46"></td>
        <td id="file-bash-cheatsheet-sh-LC46"># 1. Bash Basics.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L49"></td>
        <td id="file-bash-cheatsheet-sh-LC49">export              # displays all environment variables</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L51"></td>
        <td id="file-bash-cheatsheet-sh-LC51">echo $SHELL         # displays the shell you're using</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L52"></td>
        <td id="file-bash-cheatsheet-sh-LC52">echo $BASH_VERSION  # displays bash version</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L54"></td>
        <td id="file-bash-cheatsheet-sh-LC54">bash                # if you want to use bash (type exit to go back to your normal shell)</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L55"></td>
        <td id="file-bash-cheatsheet-sh-LC55">whereis bash        # finds out where bash is on your system</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L57"></td>
        <td id="file-bash-cheatsheet-sh-LC57">clear               # clears content on window (hide displayed lines)</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L60"></td>
        <td id="file-bash-cheatsheet-sh-LC60"># 1.1. File Commands.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L63"></td>
        <td id="file-bash-cheatsheet-sh-LC63">ls                            # lists your files</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L64"></td>
        <td id="file-bash-cheatsheet-sh-LC64">ls -l                         # lists your files in 'long format', which contains the exact size of the file, who owns the file and who has the right to look at it, and when it was last modified</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L65"></td>
        <td id="file-bash-cheatsheet-sh-LC65">ls -a                         # lists all files, including hidden files</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L66"></td>
        <td id="file-bash-cheatsheet-sh-LC66">ln -s &lt;filename&gt; &lt;link&gt;       # creates symbolic link to file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L67"></td>
        <td id="file-bash-cheatsheet-sh-LC67">touch &lt;filename&gt;              # creates or updates your file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L68"></td>
        <td id="file-bash-cheatsheet-sh-LC68">cat &gt; &lt;filename&gt;              # places standard input into file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L69"></td>
        <td id="file-bash-cheatsheet-sh-LC69">more &lt;filename&gt;               # shows the first part of a file (move with space and type q to quit)</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L70"></td>
        <td id="file-bash-cheatsheet-sh-LC70">head &lt;filename&gt;               # outputs the first 10 lines of file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L71"></td>
        <td id="file-bash-cheatsheet-sh-LC71">tail &lt;filename&gt;               # outputs the last 10 lines of file (useful with -f option)</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L72"></td>
        <td id="file-bash-cheatsheet-sh-LC72">emacs &lt;filename&gt;              # lets you create and edit a file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L73"></td>
        <td id="file-bash-cheatsheet-sh-LC73">mv &lt;filename1&gt; &lt;filename2&gt;    # moves a file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L74"></td>
        <td id="file-bash-cheatsheet-sh-LC74">cp &lt;filename1&gt; &lt;filename2&gt;    # copies a file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L75"></td>
        <td id="file-bash-cheatsheet-sh-LC75">rm &lt;filename&gt;                 # removes a file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L76"></td>
        <td id="file-bash-cheatsheet-sh-LC76">diff &lt;filename1&gt; &lt;filename2&gt;  # compares files, and shows where they differ</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L77"></td>
        <td id="file-bash-cheatsheet-sh-LC77">wc &lt;filename&gt;                 # tells you how many lines, words and characters there are in a file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L78"></td>
        <td id="file-bash-cheatsheet-sh-LC78">chmod -options &lt;filename&gt;     # lets you change the read, write, and execute permissions on your files</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L79"></td>
        <td id="file-bash-cheatsheet-sh-LC79">gzip &lt;filename&gt;               # compresses files</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L80"></td>
        <td id="file-bash-cheatsheet-sh-LC80">gunzip &lt;filename&gt;             # uncompresses files compressed by gzip</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L81"></td>
        <td id="file-bash-cheatsheet-sh-LC81">gzcat &lt;filename&gt;              # lets you look at gzipped file without actually having to gunzip it</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L82"></td>
        <td id="file-bash-cheatsheet-sh-LC82">lpr &lt;filename&gt;                # print the file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L83"></td>
        <td id="file-bash-cheatsheet-sh-LC83">lpq                           # check out the printer queue</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L84"></td>
        <td id="file-bash-cheatsheet-sh-LC84">lprm &lt;jobnumber&gt;              # remove something from the printer queue</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L85"></td>
        <td id="file-bash-cheatsheet-sh-LC85">genscript                     # converts plain text files into postscript for printing and gives you some options for formatting</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L86"></td>
        <td id="file-bash-cheatsheet-sh-LC86">dvips &lt;filename&gt;              # print .dvi files (i.e. files produced by LaTeX)</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L87"></td>
        <td id="file-bash-cheatsheet-sh-LC87">grep &lt;pattern&gt; &lt;filenames&gt;    # looks for the string in the files</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L88"></td>
        <td id="file-bash-cheatsheet-sh-LC88">grep -r &lt;pattern&gt; &lt;dir&gt;       # search recursively for pattern in directory</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L91"></td>
        <td id="file-bash-cheatsheet-sh-LC91"># 1.2. Directory Commands.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L94"></td>
        <td id="file-bash-cheatsheet-sh-LC94">mkdir &lt;dirname&gt;  # makes a new directory</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L95"></td>
        <td id="file-bash-cheatsheet-sh-LC95">cd               # changes to home</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L96"></td>
        <td id="file-bash-cheatsheet-sh-LC96">cd &lt;dirname&gt;     # changes directory</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L97"></td>
        <td id="file-bash-cheatsheet-sh-LC97">pwd              # tells you where you currently are</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L100"></td>
        <td id="file-bash-cheatsheet-sh-LC100"># 1.3. SSH, System Info & Network Commands.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L103"></td>
        <td id="file-bash-cheatsheet-sh-LC103">ssh user@host            # connects to host as user</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L104"></td>
        <td id="file-bash-cheatsheet-sh-LC104">ssh -p &lt;port&gt; user@host  # connects to host on specified port as user</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L105"></td>
        <td id="file-bash-cheatsheet-sh-LC105">ssh-copy-id user@host    # adds your ssh key to host for user to enable a keyed or passwordless login</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L107"></td>
        <td id="file-bash-cheatsheet-sh-LC107">whoami                   # returns your username</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L108"></td>
        <td id="file-bash-cheatsheet-sh-LC108">passwd                   # lets you change your password</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L109"></td>
        <td id="file-bash-cheatsheet-sh-LC109">quota -v                 # shows what your disk quota is</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L110"></td>
        <td id="file-bash-cheatsheet-sh-LC110">date                     # shows the current date and time</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L111"></td>
        <td id="file-bash-cheatsheet-sh-LC111">cal                      # shows the month's calendar</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L112"></td>
        <td id="file-bash-cheatsheet-sh-LC112">uptime                   # shows current uptime</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L113"></td>
        <td id="file-bash-cheatsheet-sh-LC113">w                        # displays whois online</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L114"></td>
        <td id="file-bash-cheatsheet-sh-LC114">finger &lt;user&gt;            # displays information about user</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L115"></td>
        <td id="file-bash-cheatsheet-sh-LC115">uname -a                 # shows kernel information</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L116"></td>
        <td id="file-bash-cheatsheet-sh-LC116">man &lt;command&gt;            # shows the manual for specified command</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L117"></td>
        <td id="file-bash-cheatsheet-sh-LC117">df                       # shows disk usage</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L118"></td>
        <td id="file-bash-cheatsheet-sh-LC118">du &lt;filename&gt;            # shows the disk usage of the files and directories in filename (du -s give only a total)</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L119"></td>
        <td id="file-bash-cheatsheet-sh-LC119">last &lt;yourUsername&gt;      # lists your last logins</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L120"></td>
        <td id="file-bash-cheatsheet-sh-LC120">ps -u yourusername       # lists your processes</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L121"></td>
        <td id="file-bash-cheatsheet-sh-LC121">kill &lt;PID&gt;               # kills (ends) the processes with the ID you gave</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L122"></td>
        <td id="file-bash-cheatsheet-sh-LC122">killall &lt;processname&gt;    # kill all processes with the name</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L123"></td>
        <td id="file-bash-cheatsheet-sh-LC123">top                      # displays your currently active processes</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L124"></td>
        <td id="file-bash-cheatsheet-sh-LC124">bg                       # lists stopped or background jobs ; resume a stopped job in the background</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L125"></td>
        <td id="file-bash-cheatsheet-sh-LC125">fg                       # brings the most recent job in the foreground</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L126"></td>
        <td id="file-bash-cheatsheet-sh-LC126">fg &lt;job&gt;                 # brings job to the foreground</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L128"></td>
        <td id="file-bash-cheatsheet-sh-LC128">ping &lt;host&gt;              # pings host and outputs results</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L129"></td>
        <td id="file-bash-cheatsheet-sh-LC129">whois &lt;domain&gt;           # gets whois information for domain</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L130"></td>
        <td id="file-bash-cheatsheet-sh-LC130">dig &lt;domain&gt;             # gets DNS information for domain</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L131"></td>
        <td id="file-bash-cheatsheet-sh-LC131">dig -x &lt;host&gt;            # reverses lookup host</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L132"></td>
        <td id="file-bash-cheatsheet-sh-LC132">wget &lt;file&gt;              # downloads file</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L135"></td>
        <td id="file-bash-cheatsheet-sh-LC135"># 2. Basic Shell Programming.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L138"></td>
        <td id="file-bash-cheatsheet-sh-LC138"># 2.1. Variables.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L141"></td>
        <td id="file-bash-cheatsheet-sh-LC141">varname=value                # defines a variable</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L142"></td>
        <td id="file-bash-cheatsheet-sh-LC142">varname=value command        # defines a variable to be in the environment of a particular subprocess</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L143"></td>
        <td id="file-bash-cheatsheet-sh-LC143">echo $varname                # checks a variable's value</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L144"></td>
        <td id="file-bash-cheatsheet-sh-LC144">echo $$                      # prints process ID of the current shell</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L145"></td>
        <td id="file-bash-cheatsheet-sh-LC145">echo $!                      # prints process ID of the most recently invoked background job</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L146"></td>
        <td id="file-bash-cheatsheet-sh-LC146">echo $?                      # displays the exit status of the last command</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L147"></td>
        <td id="file-bash-cheatsheet-sh-LC147">export VARNAME=value         # defines an environment variable (will be available in subprocesses)</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L149"></td>
        <td id="file-bash-cheatsheet-sh-LC149">array[0] = val               # several ways to define an array</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L150"></td>
        <td id="file-bash-cheatsheet-sh-LC150">array[1] = val</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L151"></td>
        <td id="file-bash-cheatsheet-sh-LC151">array[2] = val</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L152"></td>
        <td id="file-bash-cheatsheet-sh-LC152">array=([2]=val [0]=val [1]=val)</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L153"></td>
        <td id="file-bash-cheatsheet-sh-LC153">array(val val val)</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L155"></td>
        <td id="file-bash-cheatsheet-sh-LC155">${array[i]}                  # displays array's value for this index. If no index is supplied, array element 0 is assumed</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L156"></td>
        <td id="file-bash-cheatsheet-sh-LC156">${#array[i]}                 # to find out the length of any element in the array</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L157"></td>
        <td id="file-bash-cheatsheet-sh-LC157">${#array[@]}                 # to find out how many values there are in the array</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L159"></td>
        <td id="file-bash-cheatsheet-sh-LC159">declare -a                   # the variables are treaded as arrays</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L160"></td>
        <td id="file-bash-cheatsheet-sh-LC160">declare -f                   # uses funtion names only</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L161"></td>
        <td id="file-bash-cheatsheet-sh-LC161">declare -F                   # displays function names without definitions</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L162"></td>
        <td id="file-bash-cheatsheet-sh-LC162">declare -i                   # the variables are treaded as integers</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L163"></td>
        <td id="file-bash-cheatsheet-sh-LC163">declare -r                   # makes the variables read-only</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L164"></td>
        <td id="file-bash-cheatsheet-sh-LC164">declare -x                   # marks the variables for export via the environment</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L166"></td>
        <td id="file-bash-cheatsheet-sh-LC166">${varname:-word}             # if varname exists and isn't null, return its value; otherwise return word</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L167"></td>
        <td id="file-bash-cheatsheet-sh-LC167">${varname:=word}             # if varname exists and isn't null, return its value; otherwise set it word and then return its value</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L168"></td>
        <td id="file-bash-cheatsheet-sh-LC168">${varname:?message}          # if varname exists and isn't null, return its value; otherwise print varname, followed by message and abort the current command or script</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L169"></td>
        <td id="file-bash-cheatsheet-sh-LC169">${varname:+word}             # if varname exists and isn't null, return word; otherwise return null</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L170"></td>
        <td id="file-bash-cheatsheet-sh-LC170">${varname:offset:length}     # performs substring expansion. It returns the substring of $varname starting at offset and up to length characters</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L172"></td>
        <td id="file-bash-cheatsheet-sh-LC172">${variable#pattern}          # if the pattern matches the beginning of the variable's value, delete the shortest part that matches and return the rest</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L173"></td>
        <td id="file-bash-cheatsheet-sh-LC173">${variable##pattern}         # if the pattern matches the beginning of the variable's value, delete the longest part that matches and return the rest</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L174"></td>
        <td id="file-bash-cheatsheet-sh-LC174">${variable%pattern}          # if the pattern matches the end of the variable's value, delete the shortest part that matches and return the rest</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L175"></td>
        <td id="file-bash-cheatsheet-sh-LC175">${variable%%pattern}         # if the pattern matches the end of the variable's value, delete the longest part that matches and return the rest</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L176"></td>
        <td id="file-bash-cheatsheet-sh-LC176">${variable/pattern/string}   # the longest match to pattern in variable is replaced by string. Only the first match is replaced</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L177"></td>
        <td id="file-bash-cheatsheet-sh-LC177">${variable//pattern/string}  # the longest match to pattern in variable is replaced by string. All matches are replaced</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L179"></td>
        <td id="file-bash-cheatsheet-sh-LC179">${#varname}                  # returns the length of the value of the variable as a character string</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L181"></td>
        <td id="file-bash-cheatsheet-sh-LC181">*(patternlist)               # matches zero or more occurences of the given patterns</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L182"></td>
        <td id="file-bash-cheatsheet-sh-LC182">+(patternlist)               # matches one or more occurences of the given patterns</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L183"></td>
        <td id="file-bash-cheatsheet-sh-LC183">?(patternlist)               # matches zero or one occurence of the given patterns</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L184"></td>
        <td id="file-bash-cheatsheet-sh-LC184">@(patternlist)               # matches exactly one of the given patterns</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L185"></td>
        <td id="file-bash-cheatsheet-sh-LC185">!(patternlist)               # matches anything except one of the given patterns</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L187"></td>
        <td id="file-bash-cheatsheet-sh-LC187">$(UNIX command)              # command substitution: runs the command and returns standard output</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L190"></td>
        <td id="file-bash-cheatsheet-sh-LC190"># 2.2. Functions.</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L191"></td>
        <td id="file-bash-cheatsheet-sh-LC191"># The function refers to passed arguments by position (as if they were positional parameters), that is, $1, $2, and so forth.</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L192"></td>
        <td id="file-bash-cheatsheet-sh-LC192"># $@ is equal to "$1" "$2"... "$N", where N is the number of positional parameters. $# holds the number of positional parameters.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L195"></td>
        <td id="file-bash-cheatsheet-sh-LC195">functname() {</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L196"></td>
        <td id="file-bash-cheatsheet-sh-LC196">  shell commands</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L199"></td>
        <td id="file-bash-cheatsheet-sh-LC199">unset -f functname  # deletes a function definition</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L200"></td>
        <td id="file-bash-cheatsheet-sh-LC200">declare -f          # displays all defined functions in your login session</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L203"></td>
        <td id="file-bash-cheatsheet-sh-LC203"># 2.3. Flow Control.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L206"></td>
        <td id="file-bash-cheatsheet-sh-LC206">statement1 && statement2  # and operator</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L207"></td>
        <td id="file-bash-cheatsheet-sh-LC207">statement1 || statement2  # or operator</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L209"></td>
        <td id="file-bash-cheatsheet-sh-LC209">-a                        # and operator inside a test conditional expression</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L210"></td>
        <td id="file-bash-cheatsheet-sh-LC210">-o                        # or operator inside a test conditional expression</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L212"></td>
        <td id="file-bash-cheatsheet-sh-LC212">str1=str2                 # str1 matches str2</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L213"></td>
        <td id="file-bash-cheatsheet-sh-LC213">str1!=str2                # str1 does not match str2</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L214"></td>
        <td id="file-bash-cheatsheet-sh-LC214">str1&lt;str2                 # str1 is less than str2</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L215"></td>
        <td id="file-bash-cheatsheet-sh-LC215">str1&gt;str2                 # str1 is greater than str2</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L216"></td>
        <td id="file-bash-cheatsheet-sh-LC216">-n str1                   # str1 is not null (has length greater than 0)</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L217"></td>
        <td id="file-bash-cheatsheet-sh-LC217">-z str1                   # str1 is null (has length 0)</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L219"></td>
        <td id="file-bash-cheatsheet-sh-LC219">-a file                   # file exists</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L220"></td>
        <td id="file-bash-cheatsheet-sh-LC220">-d file                   # file exists and is a directory</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L221"></td>
        <td id="file-bash-cheatsheet-sh-LC221">-e file                   # file exists; same -a</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L222"></td>
        <td id="file-bash-cheatsheet-sh-LC222">-f file                   # file exists and is a regular file (i.e., not a directory or other special type of file)</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L223"></td>
        <td id="file-bash-cheatsheet-sh-LC223">-r file                   # you have read permission</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L224"></td>
        <td id="file-bash-cheatsheet-sh-LC224">-r file                   # file exists and is not empty</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L225"></td>
        <td id="file-bash-cheatsheet-sh-LC225">-w file                   # your have write permission</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L226"></td>
        <td id="file-bash-cheatsheet-sh-LC226">-x file                   # you have execute permission on file, or directory search permission if it is a directory</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L227"></td>
        <td id="file-bash-cheatsheet-sh-LC227">-N file                   # file was modified since it was last read</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L228"></td>
        <td id="file-bash-cheatsheet-sh-LC228">-O file                   # you own file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L229"></td>
        <td id="file-bash-cheatsheet-sh-LC229">-G file                   # file's group ID matches yours (or one of yours, if you are in multiple groups)</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L230"></td>
        <td id="file-bash-cheatsheet-sh-LC230">file1 -nt file2           # file1 is newer than file2</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L231"></td>
        <td id="file-bash-cheatsheet-sh-LC231">file1 -ot file2           # file1 is older than file2</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L233"></td>
        <td id="file-bash-cheatsheet-sh-LC233">-lt                       # less than</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L234"></td>
        <td id="file-bash-cheatsheet-sh-LC234">-le                       # less than or equal</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L235"></td>
        <td id="file-bash-cheatsheet-sh-LC235">-eq                       # equal</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L236"></td>
        <td id="file-bash-cheatsheet-sh-LC236">-ge                       # greater than or equal</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L237"></td>
        <td id="file-bash-cheatsheet-sh-LC237">-gt                       # greater than</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L238"></td>
        <td id="file-bash-cheatsheet-sh-LC238">-ne                       # not equal</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L240"></td>
        <td id="file-bash-cheatsheet-sh-LC240">if condition</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L242"></td>
        <td id="file-bash-cheatsheet-sh-LC242">  statements</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L243"></td>
        <td id="file-bash-cheatsheet-sh-LC243">[elif condition</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L244"></td>
        <td id="file-bash-cheatsheet-sh-LC244">  then statements...]</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L245"></td>
        <td id="file-bash-cheatsheet-sh-LC245">[else</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L246"></td>
        <td id="file-bash-cheatsheet-sh-LC246">  statements]</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L249"></td>
        <td id="file-bash-cheatsheet-sh-LC249">for x := 1 to 10 do</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L250"></td>
        <td id="file-bash-cheatsheet-sh-LC250">begin</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L251"></td>
        <td id="file-bash-cheatsheet-sh-LC251">  statements</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L254"></td>
        <td id="file-bash-cheatsheet-sh-LC254">for name [in list]</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L256"></td>
        <td id="file-bash-cheatsheet-sh-LC256">  statements that can use $name</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L259"></td>
        <td id="file-bash-cheatsheet-sh-LC259">for (( initialisation ; ending condition ; update ))</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L261"></td>
        <td id="file-bash-cheatsheet-sh-LC261">  statements...</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L264"></td>
        <td id="file-bash-cheatsheet-sh-LC264">case expression in</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L265"></td>
        <td id="file-bash-cheatsheet-sh-LC265">  pattern1 )</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L266"></td>
        <td id="file-bash-cheatsheet-sh-LC266">    statements ;;</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L267"></td>
        <td id="file-bash-cheatsheet-sh-LC267">  pattern2 )</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L268"></td>
        <td id="file-bash-cheatsheet-sh-LC268">    statements ;;</td>
      </tr>
      
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L272"></td>
        <td id="file-bash-cheatsheet-sh-LC272">select name [in list]</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L274"></td>
        <td id="file-bash-cheatsheet-sh-LC274">  statements that can use $name</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L277"></td>
        <td id="file-bash-cheatsheet-sh-LC277">while condition; do</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L278"></td>
        <td id="file-bash-cheatsheet-sh-LC278">  statements</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L281"></td>
        <td id="file-bash-cheatsheet-sh-LC281">until condition; do</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L282"></td>
        <td id="file-bash-cheatsheet-sh-LC282">  statements</td>
      </tr>
      
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L286"></td>
        <td id="file-bash-cheatsheet-sh-LC286"># 3. Command-Line Processing Cycle.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L289"></td>
        <td id="file-bash-cheatsheet-sh-LC289"># The default order for command lookup is functions, followed by built-ins, with scripts and executables last.</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L290"></td>
        <td id="file-bash-cheatsheet-sh-LC290"># There are three built-ins that you can use to override this order: `command`, `builtin` and `enable`.</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L292"></td>
        <td id="file-bash-cheatsheet-sh-LC292">command  # removes alias and function lookup. Only built-ins and commands found in the search path are executed</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L293"></td>
        <td id="file-bash-cheatsheet-sh-LC293">builtin  # looks up only built-in commands, ignoring functions and commands found in PATH</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L294"></td>
        <td id="file-bash-cheatsheet-sh-LC294">enable   # enables and disables shell built-ins</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L296"></td>
        <td id="file-bash-cheatsheet-sh-LC296">eval     # takes arguments and run them through the command-line processing steps all over again</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L299"></td>
        <td id="file-bash-cheatsheet-sh-LC299"># 4. Input/Output Redirectors.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L302"></td>
        <td id="file-bash-cheatsheet-sh-LC302">cmd1|cmd2  # pipe; takes standard output of cmd1 as standard input to cmd2</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L303"></td>
        <td id="file-bash-cheatsheet-sh-LC303">&gt; file     # directs standard output to file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L304"></td>
        <td id="file-bash-cheatsheet-sh-LC304">&lt; file     # takes standard input from file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L305"></td>
        <td id="file-bash-cheatsheet-sh-LC305">&gt;&gt; file    # directs standard output to file; append to file if it already exists</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L306"></td>
        <td id="file-bash-cheatsheet-sh-LC306">&gt;|file     # forces standard output to file even if noclobber is set</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L307"></td>
        <td id="file-bash-cheatsheet-sh-LC307">n&gt;|file    # forces output to file from file descriptor n even if noclobber is set</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L308"></td>
        <td id="file-bash-cheatsheet-sh-LC308">&lt;&gt; file    # uses file as both standard input and standard output</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L309"></td>
        <td id="file-bash-cheatsheet-sh-LC309">n&lt;&gt;file    # uses file as both input and output for file descriptor n</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L310"></td>
        <td id="file-bash-cheatsheet-sh-LC310">&lt;&lt;label    # here-document</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L311"></td>
        <td id="file-bash-cheatsheet-sh-LC311">n&gt;file     # directs file descriptor n to file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L312"></td>
        <td id="file-bash-cheatsheet-sh-LC312">n&lt;file     # takes file descriptor n from file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L313"></td>
        <td id="file-bash-cheatsheet-sh-LC313">n&gt;&gt;file    # directs file description n to file; append to file if it already exists</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L314"></td>
        <td id="file-bash-cheatsheet-sh-LC314">n&gt;&        # duplicates standard output to file descriptor n</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L315"></td>
        <td id="file-bash-cheatsheet-sh-LC315">n&lt;&        # duplicates standard input from file descriptor n</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L316"></td>
        <td id="file-bash-cheatsheet-sh-LC316">n&gt;&m       # file descriptor n is made to be a copy of the output file descriptor</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L317"></td>
        <td id="file-bash-cheatsheet-sh-LC317">n&lt;&m       # file descriptor n is made to be a copy of the input file descriptor</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L318"></td>
        <td id="file-bash-cheatsheet-sh-LC318">&&gt;file     # directs standard output and standard error to file</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L319"></td>
        <td id="file-bash-cheatsheet-sh-LC319">&lt;&-        # closes the standard input</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L320"></td>
        <td id="file-bash-cheatsheet-sh-LC320">&gt;&-        # closes the standard output</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L321"></td>
        <td id="file-bash-cheatsheet-sh-LC321">n&gt;&-       # closes the ouput from file descriptor n</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L322"></td>
        <td id="file-bash-cheatsheet-sh-LC322">n&lt;&-       # closes the input from file descripor n</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L325"></td>
        <td id="file-bash-cheatsheet-sh-LC325"># 5. Process Handling.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L328"></td>
        <td id="file-bash-cheatsheet-sh-LC328"># To suspend a job, type CTRL+Z while it is running. You can also suspend a job with CTRL+Y.</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L329"></td>
        <td id="file-bash-cheatsheet-sh-LC329"># This is slightly different from CTRL+Z in that the process is only stopped when it attempts to read input from terminal.</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L330"></td>
        <td id="file-bash-cheatsheet-sh-LC330"># Of course, to interupt a job, type CTRL+C.</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L332"></td>
        <td id="file-bash-cheatsheet-sh-LC332">myCommand &  # runs job in the background and prompts back the shell</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L334"></td>
        <td id="file-bash-cheatsheet-sh-LC334">jobs         # lists all jobs (use with -l to see associated PID)</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L336"></td>
        <td id="file-bash-cheatsheet-sh-LC336">fg           # brings a background job into the foreground</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L337"></td>
        <td id="file-bash-cheatsheet-sh-LC337">fg %+        # brings most recently invoked background job</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L338"></td>
        <td id="file-bash-cheatsheet-sh-LC338">fg %-        # brings second most recently invoked background job</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L339"></td>
        <td id="file-bash-cheatsheet-sh-LC339">fg %N        # brings job number N</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L340"></td>
        <td id="file-bash-cheatsheet-sh-LC340">fg %string   # brings job whose command begins with string</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L341"></td>
        <td id="file-bash-cheatsheet-sh-LC341">fg %?string  # brings job whose command contains string</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L343"></td>
        <td id="file-bash-cheatsheet-sh-LC343">kill -l      # returns a list of all signals on the system, by name and number</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L344"></td>
        <td id="file-bash-cheatsheet-sh-LC344">kill PID     # terminates process with specified PID</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L346"></td>
        <td id="file-bash-cheatsheet-sh-LC346">ps           # prints a line of information about the current running login shell and any processes running under it</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L347"></td>
        <td id="file-bash-cheatsheet-sh-LC347">ps -a        # selects all processes with a tty except session leaders</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L349"></td>
        <td id="file-bash-cheatsheet-sh-LC349">trap cmd sig1 sig2  # executes a command when a signal is received by the script</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L350"></td>
        <td id="file-bash-cheatsheet-sh-LC350">trap "" sig1 sig2   # ignores that signals</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L351"></td>
        <td id="file-bash-cheatsheet-sh-LC351">trap - sig1 sig2    # resets the action taken when the signal is received to the default</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L353"></td>
        <td id="file-bash-cheatsheet-sh-LC353">disown &lt;PID|JID&gt;    # removes the process from the list of jobs</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L355"></td>
        <td id="file-bash-cheatsheet-sh-LC355">wait                # waits until all background jobs have finished</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L358"></td>
        <td id="file-bash-cheatsheet-sh-LC358"># 6. Tips and Tricks.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L361"></td>
        <td id="file-bash-cheatsheet-sh-LC361"># set an alias</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L362"></td>
        <td id="file-bash-cheatsheet-sh-LC362">cd; nano .bash_profile</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L363"></td>
        <td id="file-bash-cheatsheet-sh-LC363">&gt; alias gentlenode='ssh admin@gentlenode.com -p 3404'  # add your alias in .bash_profile</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L365"></td>
        <td id="file-bash-cheatsheet-sh-LC365"># to quickly go to a specific directory</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L366"></td>
        <td id="file-bash-cheatsheet-sh-LC366">cd; nano .bashrc</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L367"></td>
        <td id="file-bash-cheatsheet-sh-LC367">&gt; shopt -s cdable_vars</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L368"></td>
        <td id="file-bash-cheatsheet-sh-LC368">&gt; export websites="/Users/mac/Documents/websites"</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L370"></td>
        <td id="file-bash-cheatsheet-sh-LC370">source .bashrc</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L371"></td>
        <td id="file-bash-cheatsheet-sh-LC371">cd websites</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L374"></td>
        <td id="file-bash-cheatsheet-sh-LC374"># 7. Debugging Shell Programs.</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L377"></td>
        <td id="file-bash-cheatsheet-sh-LC377">bash -n scriptname  # don't run commands; check for syntax errors only</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L378"></td>
        <td id="file-bash-cheatsheet-sh-LC378">set -o noexec       # alternative (set option in script)</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L380"></td>
        <td id="file-bash-cheatsheet-sh-LC380">bash -v scriptname  # echo commands before running them</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L381"></td>
        <td id="file-bash-cheatsheet-sh-LC381">set -o verbose      # alternative (set option in script)</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L383"></td>
        <td id="file-bash-cheatsheet-sh-LC383">bash -x scriptname  # echo commands after command-line processing</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L384"></td>
        <td id="file-bash-cheatsheet-sh-LC384">set -o xtrace       # alternative (set option in script)</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L386"></td>
        <td id="file-bash-cheatsheet-sh-LC386">trap 'echo $varname' EXIT  # useful when you want to print out the values of variables at the point that your script exits</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L388"></td>
        <td id="file-bash-cheatsheet-sh-LC388">function errtrap {</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L389"></td>
        <td id="file-bash-cheatsheet-sh-LC389">  es=$?</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L390"></td>
        <td id="file-bash-cheatsheet-sh-LC390">  echo "ERROR line $1: Command exited with status $es."</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L393"></td>
        <td id="file-bash-cheatsheet-sh-LC393">trap 'errtrap $LINENO' ERR  # is run whenever a command in the surrounding script or function exists with non-zero status </td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L395"></td>
        <td id="file-bash-cheatsheet-sh-LC395">function dbgtrap {</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L396"></td>
        <td id="file-bash-cheatsheet-sh-LC396">  echo "badvar is $badvar"</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L399"></td>
        <td id="file-bash-cheatsheet-sh-LC399">trap dbgtrap DEBUG  # causes the trap code to be executed before every statement in a function or script</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L400"></td>
        <td id="file-bash-cheatsheet-sh-LC400"># ...section of code in which the problem occurs...</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L401"></td>
        <td id="file-bash-cheatsheet-sh-LC401">trap - DEBUG  # turn off the DEBUG trap</td>
      </tr>
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L403"></td>
        <td id="file-bash-cheatsheet-sh-LC403">function returntrap {</td>
      </tr>
      <tr>
        <td id="file-bash-cheatsheet-sh-L404"></td>
        <td id="file-bash-cheatsheet-sh-LC404">  echo "A return occured"</td>
      </tr>
      
      
      <tr>
        <td id="file-bash-cheatsheet-sh-L407"></td>
        <td id="file-bash-cheatsheet-sh-LC407">trap returntrap RETURN  # is executed each time a shell function or a script executed with the . or source commands finishes executing</td>
      </tr>
      
</tbody></table>


  