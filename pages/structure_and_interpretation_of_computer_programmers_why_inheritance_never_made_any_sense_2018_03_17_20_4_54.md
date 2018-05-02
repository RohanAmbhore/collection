<a href="https://www.sicpers.info/2018/03/why-inheritance-never-made-any-sense/">https://www.sicpers.info/2018/03/why-inheritance-never-made-any-sense/</a><div id="articleHeader"><h1>Why inheritance never made any sense</h1></div>				
<p>There are three different types of inheritance going on.</p>
<ol>
<li><em>Ontological</em> inheritance is about specialisation: this thing is a specific variety of that thing (a football <em>is a</em> sphere <em>and</em> it has this radius)</li>
<li><em>Abstract data type</em> inheritance is about substitution: this thing behaves in all the ways that thing does <em>and</em> has this behaviour (this is the Liskov substitution principle)</li>
<li><em>Implementation</em> inheritance is about code sharing: this thing takes <em>some</em> of the properties of that thing <em>and</em> overrides or augments them in this way. The inheritance in my post <a href="https://www.sicpers.info/2018/03/on-inheritance/" target="_blank">On Inheritance</a> is this type and <em>only</em> this type of inheritance.</li>
</ol>
<p>These are three different, and frequently irreconcilable, relationships. Requiring any, or even all, of them, presents no difficulty. However, requiring <em>one mechanism</em> support any two or more of them is asking for trouble.</p>
<p>A common counterexample to OO inheritance is the relationship between a square and a rectangle. Geometrically, a square <em>is</em> a specialisation of a rectangle: every square is a rectangle, not every rectangle is a square. For all s in Squares, s is a Rectangle and width of s is equal to height of s. As a type, this relationship is reversed: you can use a rectangle everywhere you can use a square (by having a rectangle with the same width and height), but you cannot use a square everywhere you can use a rectangle (for example, you can’t give it a different width and height).</p>
<p>Notice that this is incompatibility between the inheritance directions of the <em>geometric properties</em> and the <em>abstract data type properties</em> of squares and rectangles; two dimensions which are completely unrelated to each other and indeed to any form of software implementation. We have so far said nothing about implementation inheritance, so haven’t even considered writing software.</p>
<p>Smalltalk and many later languages use single inheritance for implementation inheritance, because multiple inheritance is <em>incompatible</em> with the goal of implementation inheritance due to the diamond problem (traits provide a <em>reliable</em> way for the incompatibility to manifest, and leave resolution as an exercise to the reader). On the other hand, single inheritance is <em>incompatible</em> with ontological inheritance, as a square is both a rectangle and an equilateral polygon.</p>
<p>The Smalltalk blue book describes inheritance <em>solely</em> in terms of implementation inheritance:</p>
<blockquote>
<p>A subclass specifies that its instances will be the same as instances of another class, called its <em>superclass</em>, except for the differences that are explicitly stated.</p>
</blockquote>
<p>Notice what is missing: no mention that a subclass instance must be able to replace a superclass instance everywhere in a program; no mention that a subclass instance must satisfy all conceptual tests for an instance of its superclass.</p>
<p><em>Inheritance</em> was never a problem: trying to use <em>the same tree</em> for <em>three different concepts</em> was the problem.</p>
<p>“Favour composition over inheritance” is basically giving up on implementation inheritance. We can’t work out how to make it work, so we’ll avoid it: get implementation sharing by delegation instead of by subclassing.</p>
<p>Eiffel, and particular disciplined approaches to using languages like Java, tighten up the “inheritance is subtyping” relationship by relaxing the “inheritance is re-use” relationship (if the same method appears twice in unrelated parts of the tree, you have to live with it, in order to retain the property that every subclass is a subtype of its parent). This is fine, as long as you don’t try to <em>also</em> model the problem domain using the inheritance tree, but much of the OO literature recommends that you do by talking about domain-driven design.</p>
<p>Traits approaches tighten up the “inheritance is specialisation” relationship by relaxing the “inheritance is re-use” relationship (if two super categories both provide the same property of an instance of a category, neither is provided and you have to write it yourself). This is fine, as long as you don’t try to <em>also</em> treat subclasses as covariant subtypes of their superclasses, but much of the OO literature recommends that you do by talking about Liskov Substitution Principle and how a type in a method signature means that type <em>or any subclass</em>.</p>
<p>What the literature <em>should</em> do, I believe, is say “here are the three types of inheritance, focus on any one of them at a time”. I also believe that the <em>languages</em> should support that (obviously Smalltalk, Ruby and friends <em>do</em> support that by not having any type constraints).</p>
<ul>
<li>If I’m using inheritance as a code sharing tool, it should not be assumed that my subclasses are also subtypes.</li>
<li>If I am using subtypes to tighten up interface contracts, I should be not only <em>allowed</em> to mark a class anywhere in the tree as a subtype of another class anywhere in the tree, but <em>required</em> to do so: once again, it should not be assumed that my subclasses are also subtypes.</li>
<li>If I need to indicate conceptual specialisation via classes, this should <em>also</em> not be assumed to follow the inheritance tree. I should be not only <em>allowed</em> to mark a class anywhere in the tree as a subset of another class, but <em>required</em> to do so: once again, it should not be assumed that my subclasses are also specialisations.</li>
</ul>
<p>Your domain model is not your object model. Your domain model is not your abstract data type model. Your object model is not your abstract data type model.</p>
<p>Now inheritance is easy again.</p>

<div id="jp-relatedposts">
	<h3><em>Related</em></h3>
<div><p><a href="https://www.sicpers.info/2012/07/inheritance-is-old-and-busted/" title="Inheritance is old and busted

Back when I started reading about Object-Oriented Programming (which was when Java was new, I was using Delphi and maybe the ArcGIS scripting language, which also had OO features) the entire hotness was inheritance. Class hierarchies as complicated as biological taxonomies were diagrammed, implemented and justified. Authors explained that while…" target="_blank">Inheritance is old and busted</a>July 25, 2012In "code-level"</p><p><a href="https://www.sicpers.info/2018/03/in-defense-of-id/" title="In defense of `id`

Something you can't see about my dotSwift talk on OOP in FP in Swift is that to make the conference more interesting while the AV was set up for the next speaker, Daniel Steinberg invited me over to a side table for a question and answer session. He had some…" target="_blank">In defense of `id`</a>March 6, 2018In "code-level"</p><p><a href="https://www.sicpers.info/2018/03/on-inheritance/" title="On Inheritance

I recently had the chance to give my OOP-in-FP-in-Swift talk again in NSLondon, and was asked how to build inheritance in that object system. It's a great question, I gave what I hope was a good answer, and it's worth some more thought and a more coherent response. Firstly, let's…" target="_blank">On Inheritance</a>March 1, 2018In "OOP"</p></div></div>


				