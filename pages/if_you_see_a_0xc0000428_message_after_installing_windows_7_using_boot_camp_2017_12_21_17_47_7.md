<a href="https://support.apple.com/en-us/HT205052">https://support.apple.com/en-us/HT205052</a><div id="articleHeader"><h1>If you see a ‘0xc0000428‘ message after installing Windows 7 using Boot Camp</h1></div>
<div><p>If you see a black screen with the message '0xc0000428' in Windows, you might need to reinstall Windows 7.</p>
</div>


<div id="sections">
<div><p>When installing Windows 7, you need to <a href="https://support.apple.com/kb/HT205016" target="_blank">download the correct Windows support software (drivers) for your Mac</a> from the Apple Support website. You might see this message if you used Boot Camp Assistant to download this software as part of installation. The Windows support software available from Boot Camp Assistant is designed for newer versions of Windows.</p>
<p>To correct this issue, remove your existing Windows partition, then reinstall Windows 7 using the steps in this article.</p>
</div><div><h2>Remove the existing Windows partition</h2><p><a href="https://support.apple.com/kb/HT204009" target="_blank">Removing the existing Windows partition</a> erases the documents and data stored on that partition. Make sure there is no important data on this partition before you remove it.</p>
</div><div><h2>Perform a new install of Windows 7</h2><p>Use these steps if you're installing Windows 7 on your Mac for the first time.</p>
<ol>
<li><a href="https://support.apple.com/kb/HT204417" target="_blank">Start up your Mac in macOS.</a></li>
<li>Make sure you have <a href="https://support.apple.com/kb/HT205016" target="_blank">a Mac that works with Windows 7</a>.</li>
<li>If your copy of Windows 7 came on a DVD, <a href="https://support.apple.com/kb/HT203909" target="_blank">create a disk image of the install disc</a> for use with Boot Camp.</li>
<li>Connect a 16 GB or larger USB flash drive that you can erase. Leave this flash drive connected to your Mac until Windows installation is finished.</li>
<li>Open Boot Camp Assistant from the Utilities folder (or use <a href="https://support.apple.com/kb/HT201285" target="_blank">Spotlight</a> to find it) and click Continue.</li>
<li>Select only the options to create a Windows install disk and to download the latest Windows support software from Apple. Then click Continue.<div class="readableLargeImageContainer"><img src="/library/content/dam/edam/applecare/images/en_US/osx/yosemite-bootcamp-assistant.png"  alt=" " /></div></li>
<li>Choose the ISO of your Windows install disc, then click Continue. Boot Camp erases your USB flash drive and prepares it for Windows installation. After the flash drive is prepared, close the Boot Camp Assistant window to quit the app.</li>
<li>Use the <a href="https://support.apple.com/kb/HT205016#tables" target="_blank">Windows 7 compatibility tables</a> to find the Windows support software (drivers) you need for the version of Windows and the Mac that you're using.</li>
<li>Click the link in the table to download the related software.</li>
<li>After the file downloads, double-click it from the Finder to decompress (unzip) it.</li>
<li>Open the resulting folder. Locate the following files in this folder and drag them to your USB Flash drive. When prompted if you want to replace the existing items on the flash drive, click Yes.<br /><br />$WinPEDriver$ (folder)<br />
AutoUnattend.xml<br />
BootCamp (folder)</li>
<li>Open Boot Camp Assistant again, then click Continue.</li>
<li>Select only the option to "Install Windows… or later version."<div class="readableLargeImageContainer"><img src="/library/content/dam/edam/applecare/images/en_US/osx/yosemite-bootcamp-assistant-install-windows8-later.png"  alt=" " /></div></li>
<li>Click Install, then follow the onscreen prompts to repartition your drive and install Windows.</li>
<li>When you complete the assistant, your Mac restarts to the Windows installer. When you're asked where you want to install Windows, select the BOOTCAMP partition, then <a href="https://support.apple.com/kb/HT204009" target="_blank">click Drive Options and format your Boot Camp partition</a>.</li>
<li>Follow the onscreen prompts to finish installing Windows.</li>
</ol>


<div><p>Information about products not manufactured by Apple, or independent websites not controlled or tested by Apple, is provided without recommendation or endorsement. Apple assumes no responsibility with regard to the selection, performance, or use of third-party websites or products. Apple makes no representations regarding third-party website accuracy or reliability. Risks are inherent in the use of the Internet. <a href="https://support.apple.com/kb/HT201777" target="_blank">Contact the vendor</a> for additional information. Other company and product names may be trademarks of their respective owners.</p>
</div>
        





















<div>Published Date:<time> Nov 14, 2017</time>
  </div>
  

