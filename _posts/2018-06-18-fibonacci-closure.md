---
layout: post
title:  "Fibonacci Closure"
categories: [ go ]
featured-img: algorithm
---

Referring to the [Go Tutorial](https://tour.golang.org/moretypes/25), *Go* has closures, which allows us to return functions that can access and *bound* to the variables outside of their bodies. Basically, the variable is distinct among different specific instance of closures.

Here is an implementation of the function `fibonacci` that prints successive fibonacci numbers using a closure (from Go Tutorial exercise):

{% highlight go linenos %}

// fibonacci is a function that returns
// a function that returns an int.
func fibonacci() func() int {
	now := 0
	next := 1
	return func() int {
		result := now
		temp := next
		next = next + now
		now = temp
		return result
	}
}

func main() {
	f := fibonacci()
	for i := 0; i < 10; i++ {
		fmt.Println(f())
	}
}

{% endhighlight %}
