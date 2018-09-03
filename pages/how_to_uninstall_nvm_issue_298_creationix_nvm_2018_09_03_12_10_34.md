<a href="https://github.com/creationix/nvm/issues/298#issuecomment-30654686">https://github.com/creationix/nvm/issues/298#issuecomment-30654686</a><div id="articleHeader"><h1>              How to uninstall nvm?            #298    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/mehulkar" target="_blank">mehulkar</a>  opened this Issue
        <relative-time>on Sep 25, 2013</relative-time>
        · 27 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        <div>

          <div>
            




            
<div id="issue-20012391">
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I want to uninstall nvm completely. Is there documentation on how to do this?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>

          </div>

          

  


  
<div>
    
  <div>

  




  
<div id="issuecomment-25054572">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-25054572" id="issuecomment-25054572-permalink" target="_blank"><relative-time>on Sep 25, 2013</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Essentially you'd need to reverse the steps in <code>install.sh</code> - remove any nvm lines from <code>~/.bash_profile</code> (and/or <code>~/.profile</code>), <code>rm -rf ~/.nvm</code>, and either reopen your shell, or re-source your bash profile.</p>
<p>However, simply removing the nvm commands from your <code>.bash_profile</code> or <code>.profile</code> should be more than sufficient.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-30618281">
    
  <div>

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/mibamur" target="_blank">mibamur</a>
  

    </strong>

    commented

    <a href="#issuecomment-30618281" id="issuecomment-30618281-permalink" target="_blank"><relative-time>on Dec 16, 2013</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mehulkar" target="_blank">@mehulkar</a></p>
<h2>just remove directory</h2>
<div><pre>rm -rf ~/.nvm
rm -rf ~/.npm
rm -rf ~/.bower</pre></div>
<p>and as ljharb say find and remove line <code>source ~/.nvm</code> from yours .bashrc or .zshrc</p>
<p><a href="https://github.com/creationix" target="_blank">@creationix</a> please close this issue</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  


  
<div>
    
  <div>

  




  
<div id="issuecomment-30654686">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/mibamur" target="_blank">@mibamur</a> There is no need for such emphasis in your comments. And it is probably better to use the <code>$NVM_DIR</code> variable, as not everyone has nvm installed in <code>~/.nvm</code>.</p>
<p>Oneliner:</p>
<pre><code>rm -rf $NVM_DIR ~/.npm ~/.bower
</code></pre>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-30663426">
    
  <div>

    
<div>
  

    
    
      Contributor
    



  <h3>

    <strong>
      

  <a href="/mibamur" target="_blank">mibamur</a>
  

    </strong>

    commented

    <a href="#issuecomment-30663426" id="issuecomment-30663426-permalink" target="_blank"><relative-time>on Dec 16, 2013</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/koenpunt" target="_blank">@koenpunt</a>  yeh, you right</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  


  
<div>
    
  <div>

  




  
<div id="issuecomment-30684767">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-30684767" id="issuecomment-30684767-permalink" target="_blank"><relative-time>on Dec 17, 2013</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>To ensure this isn't found by someone unwitting: you do not need to do anything to <code>~/.npm</code> or <code>~/.bower</code> - you'll be needlessly blowing away caches.</p>
<p>To uninstall npm with the smallest possible impact, <em>only</em> remove the source lines from your profile. You may also <code>rm -rf $NVM_DIR</code> if you like but it's not necessary.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-30695077">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/ljharb" target="_blank">@ljharb</a> Ah you're right, it's about uninstalling nvm, not node. Although by removing the nvm directory you'll remove node as well.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-30697949">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-30697949" id="issuecomment-30697949-permalink" target="_blank"><relative-time>on Dec 17, 2013</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/koenpunt" target="_blank">@koenpunt</a> not if node is also installed globally. I install node from source globally (which is simply running 4 commands in the repo) but use <code>nvm</code> to manage it for my user profile, and I definitely run shells with <code>nvm deactivate</code> so I can use my global node.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-152174108">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>For additional info, nvm may be installed via Homebrew or npm. Check your installed packages for the proper way to remove the binary files.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-152255091">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-152255091" id="issuecomment-152255091-permalink" target="_blank"><relative-time>on Oct 30, 2015</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/scott-joe" target="_blank">@scott-joe</a> <code>nvm</code> should never be installed via homebrew - it's entirely unsupported. See <a href="https://github.com/creationix/nvm/issues/469" target="_blank">#469</a>. In addition, the <code>nvm</code> on <code>npm</code> is NOT the correct one, and <em>will not work anyways</em> - see <a href="https://github.com/creationix/nvm/issues/304" target="_blank">#304</a>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  


  
<div>
    
  <div>

  




  
<div id="issuecomment-168914490">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>What's the reasoning for not hosting nvm on npm? This would make nvm easy to uninstall with <code>npm uninstall -g nvm</code>.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-168914881">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-168914881" id="issuecomment-168914881-permalink" target="_blank"><relative-time>on Jan 5, 2016</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/trusktr" target="_blank">@trusktr</a> it's not "reasoning", it's that it's a different project that's now deprecated. I've been given ownership of it, and at some point in the future (see <a href="https://github.com/creationix/nvm/issues/304" target="_blank">#304</a>), I'll replace it with something that bootstraps the proper <code>nvm</code>.</p>
<p>Also, when using <code>nvm</code>, <code>npm</code> is managed by <code>nvm</code>. Uninstalling <code>nvm</code> would delete <code>npm</code>. Why would it make <em>any</em> sense to uninstall <code>nvm</code> with a tool that <code>nvm</code> installed for you?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-168925137">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>It might not make sense. It'd just be nice to uninstall it easily. Maybe it can prompt at the command like something like "This will uninstall versions of node installed by nvm too. Continue?".</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-169158070">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Wait, I'm not even sure that's possible. Oh well, I was able to remove it manually any ways, and I can use Arch Linxu's <code>pacman</code> to see which files don't belong to any package and remove those too.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-169158188">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-169158188" id="issuecomment-169158188-permalink" target="_blank"><relative-time>on Jan 6, 2016</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>it's pretty simple. <code>rm -rf $NVM_DIR</code> and remove the two lines in your profile file.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  


  


  
<div>
    
  <div>

  




  
<div id="issuecomment-245722721">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>can we get an <code>nvm uninstall-nvm</code> command?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-245743920">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-245743920" id="issuecomment-245743920-permalink" target="_blank"><relative-time>on Sep 9, 2016</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/chovy" target="_blank">@chovy</a> that would require modifying one or more of your profile files, otherwise it'd just be <code>rm -rf "$NVM_DIR"</code> - that's pretty destructive, and not something I'd want to encourage.</p>
<p>Disk space is cheap, so the best way to uninstall it is to simply disable it by removing the sourcing lines from your profile files - which has to be done manually.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-269970245">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>I've removed the directory (on Windows 7) and I still can execute nvm from git bash, what going on?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-270004489">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-270004489" id="issuecomment-270004489-permalink" target="_blank"><relative-time>on Jan 3, 2017</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/jcubic" target="_blank">@jcubic</a> you may need to restart git bash and/or Windows. Sourced shell functions stay in memory even if the files are deleted.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-290318972">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>step1 - check env:</p>
<pre><code>[root@demo tatia]# echo $PATH
/usr/local/bin:/usr/local/sbin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/.nvm/versions/node/v6.2.2/bin
</code></pre>
<p>step2 (remove nvm env from envs):</p>
<pre><code>export PATH=/usr/local/bin:/usr/local/sbin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
</code></pre>
<p>then, remove <code>/root/.nvm/*</code><br />
done.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-290319142">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-290319142" id="issuecomment-290319142-permalink" target="_blank"><relative-time>on Mar 30, 2017</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/sconts" target="_blank">@sconts</a> to uninstall, yes. when installed, however, the nvm paths should be <em>first</em>, or else it won't work properly. (however, <code>nvm unload</code>  and <code>nvm deactivate</code> both remove it for you)</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-296452280">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>rm -rf $NVM_DIR ~/.npm ~/.bower && unset NVM_DIR</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-296456485">
    
  <div>

    
<div>
  

    
    
      Collaborator
    



  <h3>

    <strong>
      

  <a href="/ljharb" target="_blank">ljharb</a>
  

    </strong>

    commented

    <a href="#issuecomment-296456485" id="issuecomment-296456485-permalink" target="_blank"><relative-time>on Apr 24, 2017</relative-time></a>


    
      
    
  </h3>
</div>


    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/myisjon" target="_blank">@myisjon</a> <code>~/.npm</code> and <code>~/.bower</code> are for npm and bower, respectively; you don't necessarily want to <code>~/.npm</code> when removing <code>nvm</code>. (of course, you'll want to remove bower in every case)</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  


  
<div>
    
  <div>

  




  
<div id="issuecomment-319722512">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>How about adding this in README?</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-377314332">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p>Please add uninstall instructions to the README. One preference for using package managers to install node or anything else is ease of removal. Should be explicitly defined somewhere the best practice in completely removing it...</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>

  
<div>
    
  <div>

  




  
<div id="issuecomment-377339459">
    
  <div>

    



    <div>

      
<task-lists>
<table>
  <tbody>
    <tr>
      <td>

          <p><a href="https://github.com/creationix/nvm/pull/1134" target="_blank">#1134</a> did it, but it has not yet been merged.</p>
      </td>
    </tr>
  </tbody>
</table>
</task-lists>


        



    </div>

  </div>
</div>


</div>

</div>










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

  

  


  
</div>

          
      </div>

</div>


        </div>
      