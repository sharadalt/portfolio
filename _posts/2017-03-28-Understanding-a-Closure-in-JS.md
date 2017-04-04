---
layout: post
<span title: style="font-size:12px">What is a Closure ?</span>
---
<h3>Introduction</h3>
<p>
When I was facing the first interview in web development, my mentor specifically told me to be prepared with 'Closures'. According to, “Master the JavaScript Interview”,  you can’t get very far with JavaScript without learning about 'Closures'. If you ask anyone in Front end development for interview tips, they invariably touch upon 'Closures'. 
</p>

<h3>Explanation</h3>

<p><h4>What is a Closure?</h4>
Closure is one when the function remembers the surrounding context (the lexical context) in which it was declared. In other words we can say, A closure is nothing but function with preserved data.</p>

Now let us see the code below:

{% highlight js %}

var globalVar = 50;

function a (){
  var asLocalVar = 75;
  console.log(globalVar);
  console.log(asLocalVar);
	
  function b(){
    var bsLocalVar = 100;
    console.log(globalVar);
    console.log(asLocalVar);
    console.log(bsLocalVar);	
  }
  b();
}

console.log(globalVar); // prints 50
a(); // prints 50, 75, 50, 75, 100 on separate lines
{% endhighlight %}


<p>
The globalVar has access to global scope. The global scope does not have access to the scope of either a() or b(). Function a() can access the global scope and it's local scope, but not the scope of function b(). Function b() can access the global scope, the scope of function a() and it's own local scope. 
</p>

<p>In other words, Any outer function, cannot access the scope of any inner function. The innermost function of nested functions scope chain however, has access to all the variables that exist both within and outside of it. Here the inner function is executed within it's lexical scope. </p>

The code below allows us to execute a function outside of its lexical scope.


{% highlight js %}

function a (){
  var asLocalVar = 75;
	
  function b(){
    console.log(asLocalVar);
  }
  return b;
}

var c = a(); 

c(); // prints 75
{% endhighlight %}

In this code, In addition to just focussing on local variable of function a(), The function a() now returns actual function b(), instead of invoking it. We assigned the function a() to a variable c which exists outside of function a().

Variable 'c' is a <b>Closure.</b>

When we invoke c(), we invoke b() which has access to the inner scope of a(), without executing function a().

<p> This is how A closure gives you, access to an outer function’s inner scope from an inner function, from outside it's original context. </p>

In JavaScript, closure is created every time an outer function returns a reference to an inner function.

The inner function will have access to the variables in the outer function scope, even after the outer function has returned/closed.

<h3>Examples</h3>
Closures are commonly used to give objects data privacy. Data privacy is an essential property that helps us program to an interface, not an implementation.

An example use of closure is using counter, 

Suppose you want to use a variable for counting something, and you want this counter to be available to all functions.

You could use a global variable, and a function to increase the counter. In this case,  any script on the page can change the counter, as it is a global variable. If we have declared the variable counter within the function, no one else other than the function will be able to access the counter, but the count does not work. Everytime the function is invoked, it will show the same value. The solution to this problem is using Closure.

{% highlight js %}

var count = (function () {
  var counter = 0;
  return function () {return counter += 1;}
})();

count();
count();
count(); // Prints 3

{% endhighlight %}

<p>
As per the code above, The variable count is assigned the return value of a self-invoking function. The self-invoking function only runs once. It sets the counter to zero (0), and returns a function expression. This way count becomes a function and it can access the counter in the parent scope.
</p>

<p>
Another example of Closure is, Partial addition:

{% highlight js %}
var addTo = function(varPassed) {
  var add = function(varInner){
    return varPassed + varInner; 
  }
  return add;
};

var addThree = new addTo(3);
var addFour  = new addTo(4);

console.log(addThree(1)); // prints the value 4
console.log(addFour(1));  // prints the value 5

{% endhighlight %}

In the above code, In addThree, it preserves the value of 3. When it is executed it uses this preserved data. This is closure. Again, addFour is a closure. The value of inner is what we are passing in console.log, which is 1.

<h3>Conclusion</h3>
When I was preparing for the interview, I used all the material above and felt quite confident about my basic knowledge of Closure. Hope the same confidence you will have about Closure after reading this article. Good Luck!  

</p>
<h3>References</h3>
(1)Inputs from Jeff Lau, Mentor at Bloc <br>
(2)Bloc Tutorial Material <br>
(3)w3schools.com <br>
(4)Master the JavaScript Interview from medium.com <br>
(5)techsith.com