<a href="https://www.mobileread.com/forums/showthread.php?t=61986">https://www.mobileread.com/forums/showthread.php?t=61986</a><div id="articleHeader"><h1>KindleUnpack (MobiUnpack): Extracts text, images and metadata from Kindle/Mobi files</h1></div>
	
		
		
			
			<div>
				
				<strong>KindleUnpack (MobiUnpack): Extracts text, images and metadata from Kindle/Mobi files</strong>
			</div>
			<hr />
			
		
		
		
		<div id="post_message_654996">
			
			<b>Most of this post now by pdurrant.<br />
</b><br />
KindleUnpack is a set of python scripts that take a Kindle/Mobipocket ebook and extracts the HTML, images and metadata contained in the ebook, and puts them in a form suitable for passing to KindleGen.<br /><br />For KF8 files and combined Mobipocket and KF8 files, it also can produce separated mobipocket and KF8 files, and also the original source files if those are included in the ebook. In addition, for KF8 files it can produce an 'ePub', although if the HTML isn't compliant with ePub standards, the 'ePub' won't be either.<br /><br />For Amazon's .azw4 files, it will extract the PDF that's been wrapped up in Amazon's .azw4 file format.<br /><br />Downloads available:<br />
Version 0.80 of the <a href="https://www.mobileread.com/forums/attachment.php?attachmentid=139470&stc=1&d=1434875606" target="_blank">python scripts</a> (including .pyw graphics front end)<br />
Version 0.80 of a drag&drop <a href="https://www.mobileread.com/forums/attachment.php?attachmentid=139469&stc=1&d=1434875606" target="_blank">AppleScript version</a>.<br />
A calibre plugin version of the scripts is available in <a href="https://www.mobileread.com/forums/showthread.php?t=171529" target="_blank">this thread</a>.<br /><br />For anyone not interested in KindeGen and KF8, there's a copy of the last version of the single-file script, <a href="https://www.mobileread.com/forums/attachment.php?attachmentid=89514&d=1342902594" target="_blank">mobiunpack 0.32</a>.<br /><br />The name of the script was changed to KindleUnpack with version 0.6.1.<br /><br />The Python scripts are released under GPLv3. The AppleScript Wrapper is released with <a href="http://unlicense.org/" target="_blank">unlicense</a>.<br /><br />Many thanks to adamselene for the base code which has been built on by many of the participants of this thread.<br /><br />pdurrant<br /><br />[Original Post:]<div>I reimplemented huff/cdic compression in Python, and did a few other things while I was at it.  The new script:<br /><br />* decompresses about 25x faster than mobihuff.py<br />
* uses much less memory (about 16x on my largest test file)<br />
* implements conversion of uncompressed and Palmdoc-compressed files<br />
* handles trailing data correctly in all cases<br /><br />Check it out: <a href="http://www.mit.edu/afs/athena/user/m/y/mycroft/mobiunpack.py" target="_blank">http://www.mit.edu/afs/athena/user/m.../mobiunpack.py</a><br /><br />PLEASE NOTE that this tool is only for decompressing unencrypted Mobipocket files.  It does not decrypt DRMed files.  Do not ask me for help breaking DRM.</div>
		</div>
		
	
		
		
			<div>
			
			
		
			
			
			
			
			
				
					<legend>Attached Files</legend>
					
				
			
			
			
			
			</div>
		
		
		
		
		


		
		
		
		
		
		
		
			<div>
				<hr />
				<em>
					
						Last edited by pdurrant; 06-21-2015 at 05:34 AM.
					
					
						Reason: Updated to v0.75
					
				</em>
			</div>
		
		
	
	