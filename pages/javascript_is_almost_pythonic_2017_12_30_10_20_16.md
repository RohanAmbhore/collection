<a href="https://dev.to/massa142/javascript-is-almost-pythonic-3f8?utm_source=mybridge&utm_medium=web&utm_campaign=read_more">https://dev.to/massa142/javascript-is-almost-pythonic-3f8?utm_source=mybridge&utm_medium=web&utm_campaign=read_more</a><div id="articleHeader"><h1>      JavaScript is almost pythonic    </h1></div>
    <h3>
      
        
        
      Dec 05, 2017
        <em>Updated on Dec 12, 2017 </em>
      
    </h3>
    
  
  


  
    

<h2>Multi-line String</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>print("""string text line 1
string text line 2""")
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>console.log(`string text line 1
string text line 2`)
</pre></div>



<h2>Expression Interpolation</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>a = 5
b = 10
print(f'Fifteen is {a + b} and not {2 * a + b}.')
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>var a = 5
var b = 10
console.log(`Fifteen is ${a + b} and not ${2 * a + b}.`)
</pre></div>



<h2>Arrow function</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>numbers = [1, 2, 3, 4]

list(map(lambda x: x * 2, numbers))
# or [x * 2 for x in numbers]
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>var numbers = [1, 2, 3, 4]
numbers.map(v =&gt; v * 2)
</pre></div>



<h2>Destructuring</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>numbers = (1, 2, 3)
x, y, z = numbers
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>var numbers = [1, 2, 3]
var [x, y, z] = numbers
</pre></div>



<h2>Spread Operator</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>import datetime
date_fields = (2017, 12, 4)
date = datetime.date(*date_fields)

numbers = [1, 2, 3, 4]
first, *remaining = numbers

first = [1, 2]
second = [3, 4]
combined = first + second
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>var dateFields = [2017, 12, 4]
var date = new Date(...dateFields)

var numbers = [1, 2, 3, 4]
var [first, ...remaining] = numbers

var first = [1, 2]
var second = [3, 4]
var combined = [...first, ...second]
</pre></div>



<h2>Rest Operator</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>from functools import reduce
def product(*numbers):
    return reduce(lambda x, y: x * y, numbers)

print(product(1, 2, 3, 4))
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>function product(...numbers) {
    return numbers.reduce((x, y) =&gt; x * y)
}
console.log(product(1, 2, 3, 4))
</pre></div>



<h2>Default Parameter</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>def multiply(a, b=1):
    return a * b
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>function multiply(a, b = 1) {
  return a * b
}
</pre></div>



<h2>Class</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    def __str__(self):
        return f"({self.x}, {self.y})"
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>class Point {
    constructor(x, y) {
        this.x = x
        this.y = y
    }
    toString() {
        return `(${this.x}, ${this.y})`
    }
}
</pre></div>



<h2>Sub Class</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>class ColorPoint(Point):
    def __init__(self, x, y, color):
        super().__init__(x, y)
        self.color = color
    def __str__(self):
        return "{} in color {}".format(super().__str__(), self.color)
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>class ColorPoint extends Point {
    constructor(x, y, color) {
        super(x, y)
        this.color = color
    }
    toString() {
        return `${super.toString()} in ${this.color}`
    }
}
</pre></div>



<h2>Getter & Setter</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>class SmartPoint(Point):
    @property
    def hypotenuse(self):
        return sqrt(self.x ** 2 + self.y ** 2)

    @hypotenuse.setter
    def hypotenuse(self, z):
        self.y = sqrt(z ** 2 - self.x ** 2)
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>class SmartPoint extends Point {
    get hypotenuse() {
        return Math.sqrt(this.x ** 2 + this.y ** 2)
    }
    set hypotenuse(z) {
        this.y = Math.sqrt(z ** 2 - this.x ** 2)
    }
}
</pre></div>



<h2>Module</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>import math
print(math.log(42))

from math import log
print(log(42))

from math import *
print(log(42))
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>import math from 'math'
console.log(math.log(42))

import { log } from 'math'
console.log(log(42))

import * from 'math'
console.log(log(42))
</pre></div>



<h2>Async Function</h2>

<ul>
<li>Python3.6</li>
</ul>



<div><pre>async def getProcessedData(url):
    try:
        v = await downloadData(url)
    except Exception:
        v = await downloadFallbackData(url)
    await processDataInWorker(v)
</pre></div>



<ul>
<li>ES2017</li>
</ul>



<div><pre>async function getProcessedData(url) {
  let v
  try {
    v = await downloadData(url) 
  } catch (e) {
    v = await downloadFallbackData(url)
  }
  return processDataInWorker(v)
}
</pre></div>



<h2>Reference</h2>





  