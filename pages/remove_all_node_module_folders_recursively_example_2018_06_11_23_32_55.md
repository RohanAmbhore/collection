<a href="https://coderwall.com/p/guqrca/remove-all-node_module-folders-recursively">https://coderwall.com/p/guqrca/remove-all-node_module-folders-recursively</a><div id="articleHeader"><h1>Remove all node_module folders recursively</h1></div>

<div>
<p><strong>Remove all node_module folders (or any type of folder/file)</strong></p>

<pre><code>find . -name "node_modules" -exec rm -rf '{}' +</code></pre>

<p>That will delete the folder and files even if there is a space in the name.</p>

<p>That saved me about 5GB over several hundred node projects which I had not touched in a while.<br />
If I need the node modules back, I can simply run  <code>npm install</code> </p>
</div>
<div>
<div>
<h4>
Written by
<a href="/stevelacy" id="user_83366" target="_blank">
S.Lacy
</a>
</h4>
</div>
<div>
<div>


    <div id="HeartButton-react-component-b9509321-65bc-4401-9638-af45787e012a"><div>Recommend</div>
    


<a href="http://twitter.com/home?status=Remove+all+node_module+folders+recursively+by+%40SteveDeLacy%0A%0Ahttps%3A%2F%2Fcoderwall.com%2Fp%2Fguqrca" target="_blank">

Say Thanks
</a>
<div>

    <div id="ProtipSubscribeButton-react-component-6c168380-63de-49b8-b913-45973ad442d8"><div>Update Notifications Off</div>
    


<a href="/signup" target="_blank">

Respond
</a>


<div>
<div>
<h4>
2 Responses
<div>
<div>Add your response</div>

</h4>
<div id="comment_28395">
<div><time>December 19, 2016 13:01</time></div>
<div>28395</div>

<div>
<div>
<div>
<a href="/Magdy" target="_blank">
Magdy
</a>
</div>
<div><p>This helped me, thanks man :)</p>

<p>Don't you think adding <code>-type d</code> to the find command might improve it a little, so it would be</p>

<p>find . -name "node_modules" -type d -exec rm -rf '{}' +</p></div>
<div>
over 1 year ago
·


    
    

</div>



<div id="comment_28525">
<div><time>January 21, 2017 13:24</time></div>
<div>28525</div>

<div>
<div>
<div>
<a href="/maxcnunes" target="_blank">
maxcnunes
</a>
</div>
<div><p>Include the "prune" argument to not go over children node<em>modules.<br />
```<br />
find . -name "node</em>modules" -type d -prune -exec rm -rf '{}' +<br />
```</p></div>
<div>
over 1 year ago
·


    
    

</div>







