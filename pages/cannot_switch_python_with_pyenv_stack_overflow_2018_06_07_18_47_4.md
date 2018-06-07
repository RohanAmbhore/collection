<a href="https://stackoverflow.com/questions/33321312/cannot-switch-python-with-pyenv">https://stackoverflow.com/questions/33321312/cannot-switch-python-with-pyenv</a><div id="articleHeader"><h1>Cannot switch Python with pyenv</h1></div>

<p>I would like to use pyenv to switch python2 and python3.</p>

<p>I successfully downloaded python2 and python3 and pyenv with following codes.</p>

<pre><code>brew install pyenv

brew install pyenv-virtualenv

pyenv install 2.7.10

pyenv install 3.5.0</code></pre>

<p>However, I cannot switch from python2 to python3..</p>

<pre><code>Soma-Suzuki:~ Soma$ python --version
Python 2.7.10
Soma-Suzuki:~ Soma$ pyenv global
2.7.10
Soma-Suzuki:~ Soma$ pyenv versions
  system
* 2.7.10 (set by /Users/Soma/.pyenv/version)
  3.5.0
Soma-Suzuki:~ Soma$ pyenv global 3.5.0
Soma-Suzuki:~ Soma$ pyenv global
3.5.0
Soma-Suzuki:~ Soma$ pyenv versions
  system
  2.7.10
* 3.5.0 (set by /Users/Soma/.pyenv/version)
Soma-Suzuki:~ Soma$ python --version
Python 2.7.10
Soma-Suzuki:~ Soma$ </code></pre>

<p>I do not understand why this happens.</p>

<p>For your information.
My python is in this directory.</p>

<pre><code>Soma-Suzuki:~ Soma$ which python
/usr/bin/python</code></pre>

<p>Thank you in advance.</p>
    