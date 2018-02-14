<a href="https://stackoverflow.com/questions/37712255/is-it-possible-to-integrate-forest-admin-into-parse-server">https://stackoverflow.com/questions/37712255/is-it-possible-to-integrate-forest-admin-into-parse-server</a><div id="articleHeader"><h1>Is it possible to integrate Forest admin into parse server?</h1></div>

            

<div id="question">

        <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        1
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>2</b></div>


</div>

            </td>
            
<td>
<div>
    <div>

<p>Would really like to be able to integrate <a href="http://www.forestadmin.com/" target="_blank">forest</a> into parse server. Currently they have a npm plugin that works with express+mongoose, was wondering if it was possible to configure parse server as an express app with mongoose?</p>
    </div>
    
    
</div>
</td>
        </tr>
                
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-37712255">

                <a title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>        </tbody></table>
</div>

            <div id="answers">

                
                




  

<div id="answer-37757468">
    <table>
        <tbody><tr>
            <td>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        1
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </td>
            


<td>
    <div>
<p><a href="https://github.com/ParsePlatform/parse-server" target="_blank">Parser server</a> is built on top of Express.js. <a href="http://www.forestadmin.com" target="_blank">Forest Admin</a> already supports Express with Mongoose, Sequelize and Loopback.</p>

<p>You cannot use <code>forest-express-mongoose</code> directly because the Forest npm plugin (the Liana) will try to analyze the database schema through mongoose, which does not exist in Parse-server.</p>

<p><a href="http://www.forestadmin.com" target="_blank">Forest Admin</a> supports <a href="https://loopback.io" target="_blank">Loopback</a> today with the npm plugin (the Liana) <a href="https://github.com/ForestAdmin/forest-loopback" target="_blank">forest-loopback</a>. The Parse server support is similar to the Loopback.</p>

<p>You can create a forest-parse plugin with the same architecture. Both modules just need to use the common <code>forest-express</code> module to generate the Admin API. The only responsability of the forest-express-mongoose, forest-express-sequelize, forest-loopback and forest-parse is to analyze the database schema through the ORM used and map it to a "Forest valid schema" (also called apimap in the documentation: <a href="http://doc.forestadmin.com/api-reference/#initializing-your-admin" target="_blank">http://doc.forestadmin.com/api-reference/#initializing-your-admin</a>).</p>
    </div>
    
</td>
        </tr>
    
<tr>
    <td></td>
    <td>
	    

        <div id="comments-link-37757468">

                <a title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”." target="_blank">add a comment</a>
            
        </div>         
    </td>
</tr>    </tbody></table>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    






                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/express" title="show questions tagged 'express'" target="_blank">express</a> <a href="/questions/tagged/parse.com" title="show questions tagged 'parse.com'" target="_blank">parse.com</a> <a href="/questions/tagged/parse-server" title="show questions tagged 'parse-server'" target="_blank">parse-server</a> <a href="/questions/tagged/forestadmin" title="show questions tagged 'forestadmin'" target="_blank">forestadmin</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        