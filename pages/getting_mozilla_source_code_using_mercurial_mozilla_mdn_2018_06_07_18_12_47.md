<a href="https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Source_Code/Mercurial">https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Source_Code/Mercurial</a><div id="articleHeader"><h1>Getting Mozilla Source Code Using Mercurial</h1></div>
  

      
      

    
      
        

          
          

            
            

              

              
              

              

              
              

              
              
                
                  
                    <p><a href="/en/Mercurial" title="en/Mercurial" target="_blank">Mercurial</a> is a source-code management tool which allows users to keep track of changes to the source code locally and share their changes with others. It is used for the development of Firefox.</p>

<h3 id="Client_settings">Client settings</h3>

<h4 id="Installing_and_configuring_Mercurial">Installing and configuring Mercurial</h4>

<p>See <a href="/en/Installing_Mercurial" title="en/Installing_Mercurial" target="_blank">Installing Mercurial</a>.</p>

<h4 id="Checking_out_a_source_tree">Checking out a source tree</h4>

<p>There are multiple hg repositories hosted at mozilla.org. See <a href="https://hg.mozilla.org/" title="https://hg.mozilla.org/" target="_blank">https://hg.mozilla.org/</a> for the full list.</p>

<h4 id="mozilla-central_(main_development_tree)">mozilla-central (main development tree)</h4>

<p>Most developers write patches against the mozilla-central tree.</p>

<p>Clone mozilla-central to get a local copy of the repository and then cd into it:</p>

<pre><code># This may take a while...
hg clone https://hg.mozilla.org/mozilla-central/ firefox
cd firefox</code></pre>

<h4 id="Latest_successful_build">Latest successful build</h4>

<p>The latest committed changes in your checkout may not build successfully. You may want to <a href="/en-US/docs/Developer_Guide/Source_Code/LatestPassingSource" title="https://developer.mozilla.org/En/Developer_Guide/Source_Code/LatestPassingSource" target="_blank">get the source code that has passed the automatic tests</a>.</p>

<h4 id="mozilla-inbound_(used_for_landing_your_patches)">mozilla-inbound (used for landing your patches)</h4>

<p>Most developers also maintain a clone of mozilla-inbound, which they use for landing their patches.  You probably want to develop on top of mozilla-central, which tends to be more stable, but you should use mozilla-inbound when your patches are ready to land.  See <a href="https://wiki.mozilla.org/Tree_Rules/Inbound" title="https://wiki.mozilla.org/Tree_Rules/Inbound" target="_blank">this page</a> for how checking code into mozilla-inbound works.</p>

<pre><code>hg clone https://hg.mozilla.org/integration/mozilla-inbound/ inbound
cd inbound</code></pre>

<h4 id="mozilla-beta_(prerelease_development_tree)">mozilla-beta (prerelease development tree)</h4>

<p>When a new release of Firefox enters beta testing, the code is branched into  <a href="https://hg.mozilla.org/releases/mozilla-beta" title="https://hg.mozilla.org/releases/mozilla-beta" target="_blank"><code>mozilla-beta</code></a>. This code represents the expected next release of the Firefox browser, and should be pretty stable. If you want to build off this branch, you can clone the repository as follows:</p>

<pre><code># Pull the Mozilla source to the folder beta-src/ - may take a while 
# as hundreds of megabytes of history is downloaded to .hg
hg clone https://hg.mozilla.org/releases/mozilla-beta/ beta

cd beta</code></pre>

<h4 id="mozilla-release_(release_tree)">mozilla-release (release tree)</h4>

<p>To get the source repository for the current release of Firefox, do the following:</p>

<pre><code>hg clone https://hg.mozilla.org/releases/mozilla-release release
cd release</code></pre>

<h4 id="comm-central_(ThunderbirdSeaMonkeyCalendar)">comm-central (Thunderbird/SeaMonkey/Calendar)</h4>

<p>See <a href="/En/Developer_Guide/Source_Code/Getting_comm-central" title="En/Comm-central source code (Mercurial)" target="_blank">Comm-central source code (Mercurial)</a> for further information on pulling and building with <code>comm-central</code>.</p>

<h4 id="L10n_repos">L10n repos</h4>

<p>If you are creating a new localization based on an already-localized version of a Mozilla project, you will be interested in cloning this code. Code for all l10n projects lives in <a href="https://hg.mozilla.org/l10n-central" title="https://hg.mozilla.org/l10n-central" target="_blank">l10n-central</a> and is organized (in most cases) by the locale's two character ISO code. When cloning, use the same ISO code to name the local directory that will store it. To get this code, do the following:</p>

<pre><code># Pull the Mozilla source to the folder src/ - may take a while 
# as hundreds of megabytes of history is downloaded to .hg
hg clone https://hg.mozilla.org/l10n-central/your-ISO-code yourISOcode

cd yourISOcode</code></pre>

<h3 id="Bundles">Bundles</h3>

<p>See <a href="/en-US/docs/Developer_Guide/Source_Code/Mercurial/Bundles" title="/en-US/docs/Developer_Guide/Source_Code/Mercurial/Bundles" target="_blank">Mercurial bundles</a> for information about downloading a single large file instead of using "hg clone".</p>

<h3 id="Using_a_Unified_Repository">Using a Unified Repository</h3>

<p>There are multiple repositories for Firefox. It is common to want to interact with more than 1 of them. See <a href="https://mozilla-version-control-tools.readthedocs.org/en/latest/hgmozilla/unifiedrepo.html" target="_blank">https://mozilla-version-control-tools.readthedocs.org/en/latest/hgmozilla/unifiedrepo.html</a> for instructions on doing this efficiently.</p>

<h3 id="Building">Building</h3>

<p>By default with no configuration a similar-to-release build is done. If you wish you can <a href="/en/Configuring_Build_Options" title="en/Configuring_Build_Options" target="_blank">configure</a> the build using a <code>.mozconfig</code> file and <code>make -f client.mk</code>. Different OSs have different prerequisites for a successful build, please refer to the <a href="/en/docs/Developer_Guide/Build_Instructions" title="/en/Build_Instructions" target="_blank">build documentation</a> to verify they are available on your build machine.</p>

<h3 id="See_also">See also</h3>

<ul>
 <li>The <a href="/en/Mercurial" title="en/Mercurial" target="_blank">Mercurial</a> page has information about creating diffs, committing changes, and publishing shared repositories.</li>
 <li><a href="/en-US/docs/Git" target="_blank">Check out this link</a> if you prefer to work with git repository.</li>
</ul>


                  
                
              