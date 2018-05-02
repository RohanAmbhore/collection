<a href="https://stackoverflow.com/questions/11547458/what-is-the-difference-between-jvm-jdk-jre-openjdk">https://stackoverflow.com/questions/11547458/what-is-the-difference-between-jvm-jdk-jre-openjdk</a><div id="articleHeader"><h1>What is the difference between JVM, JDK, JRE & OpenJDK?</h1></div>

            

<div id="question">

    
        
    <div>
            <div>
                

<div>
        
        <a title="This question shows research effort; it is useful and clear" target="_blank">up vote</a>
        253
        <a title="This question does not show any research effort; it is unclear or not useful" target="_blank">down vote</a>

        <a href="#" title="This is one of your favorite questions (click to undo)" target="_blank">favorite</a>
        <div><b>134</b></div>


</div>

            </div>

            
<div>
    <div>

<p>What is the difference between <strong>JVM</strong>, <strong>JDK</strong>, <strong>JRE</strong> & <strong>OpenJDK</strong>?</p>

<p>I was programming in Java and I encountered these phrases, what are the differences between them?</p>
    </div>
    
    <div>
    

    
    <div>
        <div>
    <div>
        asked Jul 18 '12 at 17:56
    </div>
    
    
</div>
    </div>
    </div>
</div>

                        <div>
                <div>
        <h2>                    <b>protected</b> by <a href="/users/-1/community" target="_blank">Community</a>♦ Nov 8 '15 at 17:55
</h2>
        <p>
This question is protected to prevent "thanks!", "me too!", or spam answers by new users. 
To answer it, you must have earned at least 10 <a href="/help/whats-reputation" target="_blank">reputation</a> on this site (the <a href="/help/privileges/new-user" target="_blank">association bonus does not count</a>).</p>
    </div>
            </div>
    
            </div>
</div>

            <div id="answers">

                
                




  

<div id="answer-11580321">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        298
        <a title="This answer is not useful" target="_blank">down vote</a>



        accepted

</div>

            </div>
            


<div>
    <div>


<p>The <strong>Java Virtual machine</strong> (JVM) is the virtual machine that runs the Java bytecodes. The JVM doesn't understand Java source code, that's why you compile your <code>*.java</code> files to obtain <code>*.class</code> files that contain the bytecodes understood by the JVM. It's also the entity that allows Java to be a "portable language" (<em>write once, run anywhere</em>). Indeed, there are specific implementations of the JVM for different systems (Windows, Linux, MacOS, <a href="http://en.wikipedia.org/wiki/List_of_Java_virtual_machines" target="_blank">see the Wikipedia list</a>), the aim is that with the same bytecodes they all give the same results.</p>

<h1>JDK and JRE</h1>

<p>To explain the difference between JDK and JRE, the best is to read the <a href="http://www.oracle.com/technetwork/java/javase/tech/index-jsp-140763.html" target="_blank">Oracle documentation</a> and consult the diagram:</p>

<blockquote>
  <p><strong>Java Runtime Environment (JRE)</strong></p>
  
  <p>The Java Runtime Environment (JRE) provides the libraries, the Java Virtual Machine, and other components to run applets and applications written in the Java programming language. In addition, two key deployment technologies are part of the JRE: Java Plug-in, which enables applets to run in popular browsers; and Java Web Start, which deploys standalone applications over a network. It is also the foundation for the technologies in the Java 2 Platform, Enterprise Edition (J2EE) for enterprise software development and deployment. The JRE does not contain tools and utilities such as compilers or debuggers for developing applets and applications.</p>
</blockquote>

<hr />

<blockquote>
  <p><strong>Java Development Kit (JDK)</strong></p>
  
  <p>The JDK is a superset of the JRE, and contains everything that is in the JRE, plus tools such as the compilers and debuggers necessary for developing applets and applications.</p>
</blockquote>

<p>Note that Oracle is not the only one to provide JDKs.</p>

<h1>OpenJDK</h1>

<p>The <strong><a href="http://openjdk.java.net/faq/" target="_blank">OpenJDK</a></strong> is the open-source implementation of the Java SE 7 JSR (<a href="http://www.jcp.org/en/jsr/detail?id=336" target="_blank">JSR 336</a>).
Now there is almost no difference between the Oracle JDK and the OpenJDK. Last year, Oracle took this decision :
<a href="https://blogs.oracle.com/henrik/entry/moving_to_openjdk_as_the" target="_blank">Moving to OpenJDK as the official Java SE 7 Reference Implementation</a> </p>

<p>The differences are stated in this <a href="https://blogs.oracle.com/henrik/entry/java_7_questions_answers" target="_blank">blog</a> :</p>

<blockquote>
  <p>Q: What is the difference between the source code found in the OpenJDK repository, and the code you use to build the Oracle JDK?</p>
  
  <p>A: It is very close - our build process for Oracle JDK releases builds on OpenJDK 7 by adding just a couple of pieces, like the deployment code, which includes Oracle's implementation of the Java Plugin and Java WebStart, as well as some closed source third party components like a graphics rasterizer, some open source third party components, like Rhino, and a few bits and pieces here and there, like additional documentation or third party fonts. Moving forward, our intent is to open source all pieces of the Oracle JDK except those that we consider commercial features such as JRockit Mission Control (not yet available in Oracle JDK), and replace encumbered third party components with open source alternatives to achieve closer parity between the code bases.</p>
</blockquote>

<p>Depending on the used version, the VM can differ: <a href="https://gist.github.com/rednaxelafx/925323" target="_blank">Correspondence between Sun/Oracle JDK, OpenJDK and HotSpot VM versions</a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-11547497">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        71
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<ul>
<li>JVM is Java Virtual Machine -- the JVM actually runs Java bytecode.</li>
<li>JDK is Java Developer Kit -- the JDK is what you need to compile Java source code.</li>
<li>JRE is Java Runtime Environment -- is what you need to run a Java program and contains a JVM, among other things.</li>
</ul>

<p>OpenJDK is a specific JDK implementation.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-11547540">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        12
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>JVM</strong> is the virtual machine Java code executes on</p>

<p><strong>JRE</strong> is the environment (standard libraries and JVM) required to run Java applications</p>

<p><strong>JDK</strong> is the JRE with developer tools and documentation</p>

<p><strong>OpenJDK</strong> is an open-source version of the JDK, unlike the common JDK owned by Oracle</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 18 '12 at 18:01
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-11547559">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        22
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>A <strong>Java virtual machine (JVM)</strong> is a virtual machine that can execute Java bytecode. It is the code execution component of the Java software platform.</p>

<p>The <strong>Java Development Kit (JDK)</strong> is an Oracle Corporation product aimed at Java developers. Since the introduction of Java, it has been by far the most widely used Java Software Development Kit (SDK).</p>

<p><strong>Java Runtime Environment</strong>, is also referred to as the Java Runtime, Runtime Environment</p>

<p><strong>OpenJDK (Open Java Development Kit)</strong> is a free and open source implementation of the Java programming language. It is the result of an effort Sun Microsystems began in 2006. The implementation is licensed under the GNU General Public License (GPL) with a linking exception. </p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-16365953">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        4
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Another aspect worth mentioning:</p>

<p><strong>JDK (java development kit)</strong> </p>

<p>You will need it for development purposes like the name suggest.</p>

<p>For example: a software company will have JDK install in their computer because they will need to develop new software which involves compiling and running their Java programs as well.</p>

<p>So we can say that JDK = JRE + JVM.</p>

<p><strong>JRE (java run-time environment)</strong></p>

<p>It's needed to run Java programs. You can't compile Java programs with it . </p>

<p>For example: a regular computer user who wants to run some online games then will need JRE in his system to run Java programs.</p>

<p><strong>JVM (java virtual machine)</strong> </p>

<p>As you might know it run the bytecodes. It make Java platform independent because it executes the <code>.class</code> file which you get after you compile the Java program regardless of whether you compile it on Windows, Mac or Linux.</p>

<p><strong>Open JDK</strong></p>

<p>Well, like I said above. Now JDK is made by different company, one of them which happens to be an open source and free for public use is OpenJDK, while some others are Oracle Corporation's JRockit JDK or IBM JDK.</p>

<p>However they all might appear the same to general user.</p>

<p><strong>Conclusion</strong> </p>

<p>If you are a Java programmer you will need JDK in your system and this package will include JRE and JVM as well but if you are normal user who like to play online games then you will only need JRE and this package will not have JDK in it.</p>

<p>In other words JDK is grandfather JRE is father and JVM is their son.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-17100740">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        40
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>JDK (Java Development Kit)</strong></p>

<p>Java Developer Kit contains tools needed to develop the Java programs, and JRE to run the programs. The tools include compiler (javac.exe), Java application launcher (java.exe), Appletviewer, etc…</p>

<p>Compiler converts java code into byte code. Java application launcher opens a JRE, loads the class, and invokes its main method.</p>

<p>You need JDK, if at all you want to write your own programs, and to compile them. For running java programs, JRE is sufficient.</p>

<p>JRE is targeted for execution of Java files</p>

<p><strong>i.e.</strong> JRE = JVM + Java Packages Classes(like util, math, lang, awt,swing etc)+runtime libraries.</p>

<p>JDK is mainly targeted for java development. I.e. You can create a Java file (with the help of Java packages), compile a Java file and run a java file.</p>

<p><strong>JRE (Java Runtime Environment)</strong></p>

<p>Java Runtime Environment contains JVM, class libraries, and other supporting files. It does not contain any development tools such as compiler, debugger, etc. Actually JVM runs the program, and it uses the class libraries, and other supporting files provided in JRE. If you want to run any java program, you need to have JRE installed in the system</p>

<p>The Java Virtual Machine provides a platform-independent way of executing code;
That mean compile once in any machine and run it any where(any machine).</p>

<p><strong>JVM (Java Virtual Machine)</strong></p>

<p>As we all aware when we compile a Java file, output is not an ‘exe’ but it’s a ‘.class’ file. ‘.class’ file consists of Java byte codes which are understandable by JVM. Java Virtual Machine interprets the byte code into the machine code depending upon the underlying operating system and hardware combination. It is responsible for all the things like garbage collection, array bounds checking, etc… JVM is platform dependent.</p>

<p>The JVM is called “virtual” because it provides a machine interface that does not depend on the underlying operating system and machine hardware architecture. This independence from hardware and operating system is a cornerstone of the write-once run-anywhere value of Java programs.</p>

<p>There are different JVM implementations are there. These may differ in things like performance, reliability, speed, etc. These implementations will differ in those areas where Java specification doesn’t mention how to implement the features, like how the garbage collection process works is JVM dependent, Java spec doesn’t define any specific way to do this.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jun 14 '13 at 3:42
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-17644817">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        15
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>Simply:</strong></p>

<p><strong>JDK</strong> (Java Development Kit) :</p>

<ul>
<li>contains tools needed to develop the Java programs.</li>
<li>You need JDK, if at all you want to write your own programs, and to compile them. </li>
<li>JDK is mainly targeted for java development.</li>
</ul>

<p><strong>JRE</strong> (Java Runtime Environment)</p>

<p>Java Runtime Environment contains JVM, class libraries, and other supporting files.
JRE is targeted for execution of Java files.</p>

<p><strong>JVM</strong> (Java Virtual Machine)</p>

<p>The JVM <strong>interprets the byte code into the machine code</strong> depending upon the underlying operating system and hardware combination. It is responsible for all the things like garbage collection, array bounds checking, etc… Java Virtual Machine provides a platform-independent way of executing code.</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-19291699">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>JVM</strong> : this actually means the byte code interpreter .It is platform dependent. For eg: in      Windows platform the '<em>java.exe</em>' or '<em>javaw.exe</em>' precess is the jvm process.</p>

<p><strong>JDK</strong> : is a toolkit containing necessary libraries and utilities to develop and execute java program/application</p>

<p><strong>JRE</strong>: is the execution environment for a java application.ie, it only support runtime dependencies including jvm for compiled program. If we want to compile a java program we need jdk. </p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 10 '13 at 9:15
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-23077352">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        10
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Java Virtual Machine (JVM)</p>

<p>When you download JRE and install on your machine you got all the code required to create JVM. Java Virtual Machine is get created when you run a java program using java command e.g. java HelloWorld. JVM is responsible for converting byte code into machine specific code and that's why you have different JVM for Windows, Linux or Solaris but one JAR can run on all this operating system. Java Virtual machine is at heart of Java programming language and provide several feature to Java programmer including Memory Management and Garbage Collection, Security and other system level services. Java Virtual Machine can be customized e.g we can specify starting memory or maximum memory of heap size located inside JVM at the time of JVM creation. If we supplied invalid argument to java command it may refuse to create Java Virtual Machine by saying "failed to create Java virtual machine: invalid argument". In short Java Virtual Machine or JVM is the one who provides Platform independence to Java.</p>

<p>Java Development Kit (JDK)</p>

<p>JDK is also loosely referred as JRE but its lot more than JRE and it provides all the tools and executable require to compile debug and execute Java Program. Just like JRE, JDK is also platform specific and you need to use separate installer for installing JDK on Linux and Windows. Current Version of JDK is 1.7 which is also referred as Java7 and it contains javac (java compiler) based on programming rules of Java7 and Java which can execute java7 code with new features like String in Switch, fork-join framework or Automatic Resource Management. When you install JDK, installation folder is often referred as JAVA_HOME. All binaries are located inside JAVA_HOME/bin which includes javac, java and other binaries and they must be in your system PATH in order to compile and execute Java programs. For details on Path see how to set PATH for Java in Windows and UNIX.</p>

<p>Java Runtime Environment (JRE)</p>

<p>Java is every where in browser, in mobile, in TV or in set-top boxes and if you are into Java programming language than you know that Java code which is bundled in JAR (Java archive) file require Java virtual machine JVM to execute it. Now JVM is an executable or program like any other program and you can install that into your machine. You have seen browser often suggesting download JRE to run a Java Applet downloaded from Internet. Various version of JRE are available in java.oracle.com and most of the user who just want to execute Java program inside browser or standalone downloads JRE. All browsers including Internet Explorer, Firefox and Chrome can work with JRE.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Apr 15 '14 at 7:37
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-24786712">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>Java is the language and includes a strict and strongly typed syntax with which you should be very familiar by now.</p>

<p>Java 2 Platform, Standard Edition, also known as J2SE, referred to the platform and included the classes in the java.lang and java.io packages, among others. It was the building block that Java applications were built upon.</p>

<p>A Java Virtual Machine, or JVM, is a software virtual machine that runs compiled Java code. Because compiled Java code is merely bytecode, the JVM is responsible for compiling that bytecode to machine code before running it. (This is often called the Just In Time Compiler or JIT Compiler.) The JVM also takes care of memory management so that application code doesn’t have to.</p>

<p>The Java Development Kit, or JDK, was and remains the piece of software Java developers use to create Java applications. It contains a Java language compiler, a documentation generator, tools for working with native code, and (typically) the Java source code for the platform to enable debugging platform classes.</p>

<p>The Java Runtime Environment, or JRE, was and remains the piece of software end users download to run compiled Java applications. It includes a JVM but does not contain any of the development tools bundled in the JDK. The JDK, however, does contain a JRE.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 16 '14 at 17:07
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-26560139">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>JVM</strong> Java Virtual Machine , actually executes the java bytecode.
It is the execution block on the JAVA platform. It converts the bytecode to the machine code.</p>

<p><strong>JRE</strong> Java Runtime Environment , provides the minimum requirements for executing a Java application; it consists of the Java Virtual Machine (JVM), core classes, and supporting files.</p>

<p><strong>JDK</strong> Java Development Kit, it has all the tools to develop your application software. It is as JRE+JVM</p>

<p><strong>Open JDK</strong>  is a free and open source implementation of the Java Platform.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Oct 25 '14 at 7:12
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-28458376">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>In layman terms:- <em>JDK = JRE + Development/debugging tools</em>, where JDK is our complete package to work with Java, from creating compiling till running it.On the other hand JRE is just of running of code(Byte Code).</p>

<p>Note:- Whether we are installing JDK or JRE, JVM would come bundled with both the packages and JVM is the part where JIT compiler converts the byte code into the machine specific code.</p>

<p>Just read the article on <a href="http://www.ufthelp.com/2015/02/key-components-of-java.html" target="_blank">JDK,JRE ,JVM and JIT</a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Feb 11 '15 at 15:40
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-29766499">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>JVM</strong></p>

<p>JVM (Java Virtual Machine) is an abstract machine. It is a specification that provides runtime environment in which java bytecode can be executed.
JVMs are available for many hardware and software platforms. </p>

<p><strong>JRE</strong></p>

<p>JRE is an acronym for Java Runtime Environment.It is used to provide runtime environment.It is the implementation of JVM.It physically exists.It contains set of libraries + other files that JVM uses at runtime.</p>

<p><strong>JDK</strong></p>

<p>JDK is an acronym for Java Development Kit.It physically exists.It contains JRE + development tools.</p>

<p>Link :- <a href="http://www.javatpoint.com/difference-between-jdk-jre-and-jvm" target="_blank">http://www.javatpoint.com/difference-between-jdk-jre-and-jvm</a></p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-31751352">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        3
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>JDK</strong> - Compiles java to Byte Code. Consists of debuggers, Compilers etc</p>

<pre><code>javac file.java // Is executed using JDK</code></pre>

<p><strong>JVM</strong> - Executes the byte code. JVM is the one which makes java platform independent. But JVM varies for platforms  </p>

<p><strong>JRE</strong> - JRE comprises of JVM along with java runtime libraries to execute java programs.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 31 '15 at 16:54
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-31846342">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>In simple words :</p>

<p><strong>JVM :</strong> A specification which describes the the way/resources to run a java program. Actually executes the byte code and make java platform independent. In doing so, it is different for different platform. JVM for windows cannot work as JVM for UNIX.</p>

<p><strong>JRE :</strong> Implementation of JVM. (JVM + run time libraries)</p>

<p><strong>JDK :</strong> JRE + java compiler and other essential tools to build a java program from scratch</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-39122531">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>JDK</strong>: The complete package which you need to write and run java code</p>

<p><strong>OpenJDK</strong>: An independent implementation of JDK for making it much better</p>

<p><strong>JVM</strong>: Converts Java code into bytecode and provides the specifications which tells how should a Java code be compiled, loaded, verified, checked for errors and executed.</p>

<p><strong>JRE</strong>: Implementation of the JVM with which some Java libraries are used to Run the program</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Aug 24 '16 at 11:49
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-41660381">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>JVM : virtual machine of java. tells machine what to do with the Java Code. You cannot download JVM as is. It comes packaged in some other component.</p>

<p>JRE: Some other component referred as above is the JRE. 
It is JVM+ other jars to create runtime environmeny</p>

<p>JDK: contains JRE(which in turn contains JVM). Once you get JDK you need not install JRE and JVM separately. It contains compiler which compiles your .java files to .class files</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jan 15 '17 at 11:02
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-43547586">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>JRE</strong> executes the application but JVM reads the instructions line by line so it's interpreter.</p>

<p><strong>JDK</strong>=JRE+Development Tools</p>

<p><strong>JRE</strong>=JVM+Library Classes</p>
    </div>
    
</div>
    
        </div>
</div>

  

<div id="answer-45010741">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        2
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p><strong>JRE</strong> - stands for Java run-time and it's required to run Java application.</p>

<p><strong>JDK</strong> - stands for Java development kit and provides tools to develop Java program e.g. Java compiler. It also contains JRE. </p>

<p><strong>JVM</strong> - stands for Java virtual machine and it's the process responsible for running Java application. </p>

<p><strong>JIT</strong> - stands for Just In Time compilation and helps to boost the performance of Java application by converting Java byte code into native code when the crossed certain threshold i.e. mainly hot code is converted into native code.</p>

<p><a href="https://i.stack.imgur.com/tiXze.jpg" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://i.stack.imgur.com/tiXze.jpg" /></div></a></p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Jul 10 '17 at 11:21
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>

  

<div id="answer-47699840">
    <div>
            <div>
                

<div>
        
        <a title="This answer is useful" target="_blank">up vote</a>
        0
        <a title="This answer is not useful" target="_blank">down vote</a>




</div>

            </div>
            


<div>
    <div>
<p>To understand the difference between these three, let us consider the following diagram.
difference</p>

<p><strong>JDK</strong> – Java Development Kit (in short JDK) is Kit which provides the environment to develop and execute(run) the Java program. JDK is a kit(or package) which includes two things
            Development Tools(to provide an environment to develop your java programs)
            JRE (to execute your java program).</p>

<pre><code>Note : JDK is only used by Java Developers.</code></pre>

<p><strong>JRE</strong> – Java Runtime Environment (to say JRE) is an installation package which provides environment to only run(not develop) the java program(or application)onto your machine. JRE is only used by them who only wants to run the Java Programs i.e. end users of your system.</p>

<p><strong>JVM</strong> – Java Virtual machine(JVM) is a very important part of both JDK and JRE because it is contained or inbuilt in both. Whatever Java program you run using JRE or JDK goes into JVM and JVM is responsible for executing the java program line by line hence it is also known as interpreter.</p>
    </div>
    <div>
    
            


    <div>
       

    <div>
    <div>
        answered Dec 7 '17 at 16:46
    </div>
    
    
</div>
    </div>
    </div>
</div>
    
        </div>
</div>
                                    
                        
                            
                            
                            
                            <h2>Your Answer</h2>


            
    




<div id="post-editor">

    <div> 
        <div>
            <div id="mdhelp">
    <ul id="mdhelp-tabs">
        <li>Links</li>
        <li>Images</li>
        <li>Styling/Headers</li>
        <li>Lists</li>
        <li>Blockquotes</li>
        
        
        <li><a href="/editing-help" target="_blank">advanced help »</a></li>
    </ul>
    
    

    
    
    

    

    

    

    
</div>
            
        </div>
    </div>

    
    

    

    


    
    
    



</div>

                            

                                                            <div>
                                        
                                    <a href="#" target="_blank">discard</a>
                                </div>
                        



                        <h2>
Not the answer you're looking for?                            Browse other questions tagged <a href="/questions/tagged/java" title="show questions tagged 'java'" target="_blank">java</a> <a href="/questions/tagged/jvm" title="show questions tagged 'jvm'" target="_blank">jvm</a> <a href="/questions/tagged/difference" title="show questions tagged 'difference'" target="_blank">difference</a>  or <a href="/questions/ask" target="_blank">ask your own question</a>.                        </h2>
            </div>
        