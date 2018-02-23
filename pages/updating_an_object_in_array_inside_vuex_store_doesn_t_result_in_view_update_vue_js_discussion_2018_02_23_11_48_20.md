<a href="https://forum-archive.vuejs.org/topic/2243/updating-an-object-in-array-inside-vuex-store-doesn-t-result-in-view-update">https://forum-archive.vuejs.org/topic/2243/updating-an-object-in-array-inside-vuex-store-doesn-t-result-in-view-update</a><div id="articleHeader"><h1>															updating an object in array inside vuex store doesn't result in view update		</h1></div>

		

		<hr />

		
							
					

					
					

<div>
	

	<small>
		<strong>
			<a href="/user/kamalakar" target="_blank">kamalakar</a>
		</strong>



		

		<div>
			<a href="/post/5425" target="_blank">2 years ago</a>

			

			<small>last edited by kamalakar </small>

			

			
				
			
		</div>
		

	</small>





	<p>vuex store has</p>
<pre><code>countries = [ 
        { name: ' USA ',
          slug : 'usa',
         'destinations' : []
       },
      {
          name : 'India',
         slug : 'india',
        destinations : [ { name : 'delhi', slug : 'delhi'} ..... ];
      } ,
      .
      .
      .
       ] 
</code></pre>
<p>this is data is loaded when component is ready.<br />
I need to allow the user to add/ modify new country / destination.</p>
<p>adding is working fine --- <code>results in view update</code></p>
<p>but whenever i update( changing name of country/destination) an object at specific index position  ( be it countries or destinations array) --  <code>view doesn't get updated</code></p>
<p>but it's working once i delete</p>
<p>updating country ( not working )</p>
<pre><code>  var country = state.countries[atIndex];
  state.countries[atIndex] = newcountry;
</code></pre>
<p>updating country ( working ) -- deleting & adding back at specific index</p>
<pre><code>state.countries.splice(atIndex,1);
state.countries.splice(atIndex,0,newcountry);
</code></pre>
<p>adding is working fine as i am pushing new object at end of the array ?</p>
<p>any work around for this?</p>

