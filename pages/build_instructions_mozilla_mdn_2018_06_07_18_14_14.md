<a href="https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Build_Instructions">https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Build_Instructions</a><div id="articleHeader"><h1>Build Instructions</h1></div>
  
  
  

      
      

    
      
        

          
          

            
            

              

              
              

              

              
              

              
              
                
                  
                    <div>
<p>The mechanism used to build Firefox for Android also <a href="https://developer.mozilla.org/en-US/docs/Simple_Firefox_for_Android_build" target="_blank">has its own page</a>.</p>

<p>The mechanism used to build Firefox for iOS also <a href="https://github.com/mozilla/firefox-ios" target="_blank">has its own github</a>.</p>
</div>

<h2 id="This_page_is_about_building_Firefox_Desktop"><strong>This page is about building Firefox Desktop</strong></h2>

<p>The Mozilla build system, like the rest of the Mozilla codebase, is cross-platform. It uses traditional Unix-style <a href="http://www.gnu.org/software/autoconf/" target="_blank">autoconf</a> and <a href="http://www.gnu.org/software/make/" target="_blank">make</a> tools to build the various applications (even on non-unix operating systems).</p>

<p>Because the Mozilla codebase builds many different applications and has many options, it is complex to use and learn. Please read these instructions carefully before attempting a build.</p>

<p>These build pages are for the projects which use the autoconf-based build system: Firefox, Thunderbird, Mozilla Suite / SeaMonkey, XULRunner, Sunbird, and standalone Composer.</p>

<p>For build information on other Mozilla projects, visit their project or build page: <a href="http://wiki.caminobrowser.org/Development:Building" target="_blank">Camino</a>, <a href="/en/NSPR_build_instructions" title="en/NSPR_build_instructions" target="_blank">NSPR</a>, <a href="/en-US/SpiderMonkey/Build_Documentation" title="En/SpiderMonkey/Build_Documentation" target="_blank">Spidermonkey</a>, <a href="http://www.mozilla.org/projects/security/pki/nss/" target="_blank">NSS</a>, and <a href="http://wiki.mozilla.org/LDAP_C_SDK" target="_blank">Directory SDK for C</a>.</p>

<p>If you are having build problems, please post questions to the newsgroup <a href="news://news.mozilla.org/mozilla.dev.builds" target="_blank">mozilla.dev.builds</a> (<a href="http://groups.google.com/group/mozilla.dev.builds" target="_blank">access via Google Groups</a>). Make your post as precise as possible, including details about your operating system, your mozconfig/configure flags, and the precise error you are experiencing.</p>

<p>You may also want to check the <a href="https://treeherder.mozilla.org/" target="_blank">TreeHerder</a> to make sure the product you are working with is currently compiling in your environment.</p>

<h2 id="Getting_started">For the impatient</h2>

<p>The quickest way to build Mozilla is to use the instructions at the simple build pages:</p>



<p>For more detail, see below.</p>

<h2 id="Getting_started">Getting started</h2>

<h3 id="Build_prerequisites">Build prerequisites</h3>

<p>Before you try to build, make sure you have the correct tools, and have configured these tools correctly.</p>



<h3 id="Get_the_source">Get the source</h3>

<dl>
 <dt><a href="/en-US/docs/Developer_Guide/Source_Code/Downloading_Source_Archives" title="en/Mozilla_Source_Code_(HTTP//FTP)" target="_blank">Download Mozilla Source Code</a></dt>
 <dd>Source code for releases is available for download via FTP/HTTP.</dd>
 <dt><a href="/en-US/docs/Developer_Guide/Source_Code/Mercurial" title="en/Mozilla_Source_Code_(Mercurial)" target="_blank">Mozilla Source Code via Mercurial</a></dt>
 <dd>Those doing active development on Firefox can check out the latest source using Mercurial. This is the preferred method if you plan to provide patches and fix bugs, as it lets you get up-to-the-minute changes and merge them with your own.</dd>
 <dt><a href="/en-US/docs/Developer_Guide/Source_Code/Getting_comm-central" title="en/Comm-central_source_code_(Mercurial)" target="_blank">Comm-central Source Code via Mercurial</a></dt>
 <dd>Those doing active development on Thunderbird/SeaMonkey/Firefox can check out the latest source using Mercurial. This method includes all the code for the applications mentioned, so you can work on Firefox development, and still build Thunderbird or SeaMonkey as well.</dd>
</dl>

<h3 id="Configuring_build_options">Configuring build options</h3>

<p>Running configure and make with the default options will not give you a good working build. You should use a <code>.mozconfig</code> file to obtain a reasonable release build. Please read <a href="/en/Configuring_Build_Options" title="en/Configuring_Build_Options" target="_blank">Configuring Build Options</a> carefully before building.</p>

<h3 id="Build_and_install">Build and install</h3>

<p>After setting up your environment, downloading the source, and configuring the build, refer to the following per-app instructions on how to build:</p>



<h2 id="Random_FAQs_and_Developer_Documentation">Random FAQs and Developer Documentation</h2>



<ul>
 <li><a href="/en-US/docs/tag/Build documentation" title="All articles tagged as build documentation." target="_blank">All build documentation</a></li>
</ul>

<h2 id="Hacking_the_Build_System">Hacking the Build System</h2>


                  
                
              