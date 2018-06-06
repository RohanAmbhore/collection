<a href="https://gist.github.com/kemmason/1043716">https://gist.github.com/kemmason/1043716</a><div id="articleHeader"><h1>disable password ssh authentication on mac os</h1></div>
    <div>
  <div>
    disable password ssh authentication on mac os
  </div>
</div>


        
  
      
    

  
      <table>
      <tbody><tr>
        <td id="file-no-ssh-password-mac-txt-L1"></td>
        <td id="file-no-ssh-password-mac-txt-LC1">make sure the following lines are set in /etc/sshd_config (or /etc/ssh/sshd_config on ubuntu)</td>
      </tr>
      <tr>
        <td id="file-no-ssh-password-mac-txt-L2"></td>
        <td id="file-no-ssh-password-mac-txt-LC2">(they all exist already, but are commented, some may have a value of yes)</td>
      </tr>
      
      <tr>
        <td id="file-no-ssh-password-mac-txt-L4"></td>
        <td id="file-no-ssh-password-mac-txt-LC4">PasswordAuthentication no</td>
      </tr>
      <tr>
        <td id="file-no-ssh-password-mac-txt-L5"></td>
        <td id="file-no-ssh-password-mac-txt-LC5">ChallengeResponseAuthentication no</td>
      </tr>
      <tr>
        <td id="file-no-ssh-password-mac-txt-L6"></td>
        <td id="file-no-ssh-password-mac-txt-LC6">UsePAM no</td>
      </tr>
      
      <tr>
        <td id="file-no-ssh-password-mac-txt-L8"></td>
        <td id="file-no-ssh-password-mac-txt-LC8">then restart the ssh server (uncheck / recheck 'Remote Login' in the 'System Preferences' -&gt; 'Sharing' panel)</td>
      </tr>
</tbody></table>


  