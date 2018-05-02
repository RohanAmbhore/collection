<a href="https://github.com/sjova/vscode-sass-format/issues/1">https://github.com/sjova/vscode-sass-format/issues/1</a><div id="articleHeader"><h1>              Error: Command failed: sass-convert --version, with sass is installed in my mac            #1    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/sldobri" target="_blank">sldobri</a>  opened this Issue
        <relative-time>on May 14, 2017</relative-time>
        · 7 comments
    </div>
  



    <h2>Comments</h2>
    <div id="discussion_bucket">
      

      <div>

        <div>

          <div>
            




            
<div>
  <div id="issue-228518888">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>$ which sass-convert<br />
/usr/local/bin/sass-convert</p>
<p>$ sass-convert --version<br />
Sass 3.4.23 (Selective Steve)</p>
<p>console of developer tools error:</p>
<p>[Extension Host] Error: Command failed: which sass-convert<br />
/usr/local/bin/sass-convert<br />
/bin/sh: sass-convert: command not found</p>
<pre><code>at checkExecSyncError (child_process.js:502:13)
at Object.execSync (child_process.js:542:13)
at Object.childProcess.(anonymous function) [as execSync] (ELECTRON_ASAR.js:685:22)
at checkDependencies (/Users/sldobri/.vscode/extensions/sasa.vscode-sass-format-1.0.0/out/src/extension.js:17:25)
at registerSassFormat (/Users/sldobri/.vscode/extensions/sasa.vscode-sass-format-1.0.0/out/src/extension.js:11:5)
at activate (/Users/sldobri/.vscode/extensions/sasa.vscode-sass-format-1.0.0/out/src/extension.js:7:32)
at Function.t._callActivateOptional (/Applications/Visual Studio Code.app/Contents/Resources/app/out/vs/workbench/node/extensionHostProcess.js:4:373080)
at Function.t._callActivate (/Applications/Visual Studio Code.app/Contents/Resources/app/out/vs/workbench/node/extensionHostProcess.js:4:372865)
at /Applications/Visual Studio Code.app/Contents/Resources/app/out/vs/workbench/node/extensionHostProcess.js:4:372640
at Object.m [as _notify] (/Applications/Visual Studio Code.app/Contents/Resources/app/out/vs/workbench/node/extensionHostProcess.js:4:62432)
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  


          

          

  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-301305952">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Hello sldobri, thanks for reporting this issue. I can't reproduce same error on my side, but let's try to debug this together.</p>
<p>I'm using latest version of macOS: <strong>macOS Sierra 10.12.4 (16E195)</strong>, and latest version of Code: <strong>1.12.1 (1.12.1)</strong>.<br />
For installing <em>sass command line tools</em> I followed official procedure from here: <a href="http://sass-lang.com/install" target="_blank">http://sass-lang.com/install</a> and installed sass tools with this command: <code>sudo gem install sass</code>. After this step <em>sass-convert</em> command is available globally on my system and can be executed from <em>macOS Terminal</em>, same as from <em>Visual Studio Code Integrated Terminal</em> and from my extension. In all cases, this is output:</p>
<pre><code>$ which node
/Users/myusername/.nvm/versions/node/v6.10.2/bin/node

$ node --version
v6.10.2

$ which gem
/usr/bin/gem

$ gem --version
2.5.1

$ which sass
/usr/local/bin/sass

$ which sass-convert
/usr/local/bin/sass-convert

$ sass --version
Sass 3.4.23 (Selective Steve)

$ sass-convert --version
Sass 3.4.23 (Selective Steve)
</code></pre>
<hr />
<p>Did you installed ruby and sass via a version manager tool like <a href="https://rvm.io/" target="_blank">RVM</a>, <a href="https://github.com/rbenv/rbenv" target="_blank">rbenv</a> or something similar?</p>
<p>Did you installed additional shell/terminal environment (ex. <code>$ brew install zsh</code>)?</p>
<p>Can you execute following commands from <a href="https://code.visualstudio.com/docs/editor/integrated-terminal" target="_blank">Visual Studio Code Integrated Terminal</a> and paste me output:</p>
<pre><code>$ which node
$ node --version
$ which npm
$ npm --version
$ which gem
$ gem --version
$ which sass
$ which sass-convert
$ sass-convert --version
$ echo test
$ echo $PATH
$ echo $GEM_PATH
$ cat ~/.bash_profile
$ cat ~/.profile
</code></pre>
<p>Thanks</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-301903238">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <ul>
<li>I'm using  macOS Sierra 10.12.5 (16F73), and latest version of Code: 1.12.2 (1.12.2).</li>
<li>ruby Is what already installed on Mac</li>
<li>I'm use zsh</li>
</ul>
<p>$ ruby -v<br />
ruby 2.0.0p648 (2015-12-16 revision 53162) [universal.x86_64-darwin16]</p>
<p>$ which node<br />
/usr/local/bin/node</p>
<p>$ node --version<br />
v7.10.0</p>
<p>$ which npm<br />
/usr/local/bin/npm</p>
<p>$  npm --version<br />
4.2.0</p>
<p>$ which gem<br />
/usr/bin/gem</p>
<p>$ gem --version<br />
2.0.14.1</p>
<p>$ which sass<br />
/usr/local/bin/sass</p>
<p>$ which sass-convert<br />
/usr/local/bin/sass-convert</p>
<p>$ sass-convert --version<br />
Sass 3.4.23 (Selective Steve)</p>
<p>$ echo test<br />
test</p>
<p>$ echo $PATH<br />
/usr/local/opt/php71/bin:~/.composer/vendor/bin:/usr/local/opt/sqlite/bin:/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Users/sldobri/.composer/vendor/bin</p>
<p>$ echo $GEM_PATH</p>
<p>$ cat ~/.bash_profile<br />
cat: /Users/sldobri/.bash_profile: No such file or directory</p>
<p>$ cat ~/.profile<br />
cat: /Users/sldobri/.profile: No such file or directory</p>
<p>$ cat .zshrc</p>
<pre><code>export ZSH=$HOME/.oh-my-zsh
export NODE_PATH="/usr/local/bin/node"

export PATH="/usr/bin:$PATH"
export PATH="/usr/local/sbin:$PATH"
export PATH="/usr/local/bin:$PATH"
export PATH="/usr/local/opt/sqlite/bin:$PATH"
export PATH="~/.composer/vendor/bin:$PATH"
export PATH="$(brew --prefix homebrew/php/php71)/bin:$PATH"
export EDITOR="vim"
export GIT_EDITOR="vim"
export VISUAL="code"

# Zsh Theme
#ZSH_THEME="cloud"
#ZSH_THEME="muse"
ZSH_THEME="sorin"

export LANG=en_US.UTF-8
plugins=(
  npm
  brew
  composer
  laravel5
  git
  git-extras
  bracketsime
  osx
  autocomplete
  syntax-highlighting
  history-substring-search
  theme
  vi-mode
  vi-visual-mode
)

source $ZSH/oh-my-zsh.sh


# handy keybindings
bindkey "^A" beginning-of-line
bindkey "^D" end-of-line
bindkey "^R" history-incremental-search-backward


# shortcuts
alias ..='cd ..'
alias ...='cd ../..'
alias home='cd ~/'
alias icloud='cd ~/Library/Mobile\ Documents/com~apple~CloudDocs/'
alias ls='ls -lhaG'
alias lr='ls -lhtr'
alias history='fc -il 1i'
alias c='clear'
alias f='open .'
alias t='trash --force'
alias p='phpunit'
alias rm='rm -ifr'
alias vim='vim'
alias v='mvim'
alias c:versions='rm public/css && rm public/js'

# Pretty print the path
alias path="echo $PATH | tr -s ':' '\n'"


# Atualizar brew
alias bubu="brew update && brew upgrade && brew cleanup"


# diversos
alias bat="pmset -g batt"
alias speed="speed-test"
alias update="sudo softwareupdate -v -i -a"
alias tempo="curl http://wttr.in/pereira_barreto"


# ZSH
alias sz='source ~/.zshrc'
alias zsh='code ~/.zshrc'
alias ohmyzsh="code ~/.oh-my-zsh"
alias zshup="upgrade_oh_my_zsh"


# Git
alias g:aa="git add ."
alias g:s="git status"
alias g:l="git log"
alias g:c="git commit -m"
alias g:p="git push"
alias g:ps="dig a bitbucket.org && git push && git status"
#alias g:ps="ssh-add -K ~/.ssh/id_rsa && ssh -Tv git@bitbucket.org && git push && git status"
alias g:nah='git reset --hard && git clean -df'
alias g:aac='git add . && git commit -m'


# dev
alias ll='cd ~/Code/arturia'
alias gg='ll && g:ps'
# alias ss="m:start && cd ~/Code/arturia/server && reload && art serve"
# alias cc="cd ~/Code/arturia/client && npm run dev"
alias cc="ll && npm run dev"
alias kk="ll && code ."
alias l:reset="php artisan migrate:refresh --seed && php artisan passport:install"

alias bit='dig a bitbucket.org'


# npm
alias n:rd='npm run dev'
alias n:rb='npm run build'


# Laravel
alias art="php artisan"
alias l:s="art serve"
alias l:rl="art route:list"
alias l:mr="art migrate:refresh"
alias l:mrs="art migrate:refresh --seed"
alias l:t="php artisan tinker"
alias renew="l:mr && reload"
alias reload='composer dump-autoload &&  art view:clear && art cache:clear && art clear-compiled && art config:cache && art route:cache && art optimize'
alias t:db="rm database/database.sqlite; touch database/database.sqlite"
alias pu="./vendor/bin/phpunit"


# Mysql/MariaDB
alias m:start="mysql.server start"
alias m:s="mysql.server start"
alias m:stop="mysql.server stop"
alias m:restart="mysql.server restart"
alias m:status="mysql.server status"
</code></pre>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-301905530">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>I install the new version 1.0.1 and is work fine, thanks a lot!!!</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-302010758">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>only work if i add the sass-convert path:</p>
<p>const sassConvertCommand = '/usr/local/bin/sass-convert'; // <code>Sass Formatter</code> dependency</p>
<p>I tink is because zsh.</p>
<p>Suggestion, create <strong>sassPath</strong> paramater:</p>
<p>"sassFormat.sassPath": "/usr/local/bin"</p>
<p>value default: null</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-302220155">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Please update extension to the latest version, set: <code>"sassFormat.sassPath": "/usr/local/bin"</code> and let me know if everything works fine. Thanks.</p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  






  


  


  
<div>
    
<div>
  




  
<div>
    
  <div id="issuecomment-351091526">

    



    <div>

      
<table>
  <tbody>
    <tr>
      <td>
          <p>Thank you. For anyone else having issues, run the command:</p>
<p><code>which sass-convert</code></p>
<p>and copy the portion of your path before <code>sass-convert</code> and set it as the value of the <code>sassFormat.sassPath</code> variable in your VS Code user settings.</p>
<p>In my case, I installed Ruby with RVM, so my path was:</p>
<p><code>/Users/(my user name)/.rvm/gems/ruby-2.4.1/bin/</code></p>
      </td>
    </tr>
  </tbody>
</table>


        



    </div>

  















        


        <div>
              
<div>
  

    
      



      <div>
        
          <div>
  


  
  <div>

    

    

        <p>
    
    
        Attach files by dragging & dropping,
        selecting them, or pasting
        from the clipboard.
    
    
    
    
    
    
    
    
    
  </p>


    
  </div>

  

  


  


          
      




        
      

    
    
  