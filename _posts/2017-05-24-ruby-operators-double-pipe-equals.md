---
layout: post
title:  "Ruby Operators: Double Pipe Equals"
date:   2017-05-24
---

### “Hey, what does that \|\|= mean in your ruby code?”


In my first blog post as a programmer, I thought it would be appropriate to explain one of the questions that I was asked during my first day at [Flatiron School](https://flatironschool.com/). This is a question that I had come up about a month ago and one that led me down a rabbit hole of ruby forums and reddit posts (I’ll save you the trouble and link a few of the better sources at the bottom of this post).

The controversy behind “double-pipe equals” is centered around how the operator should be translated but I’d like to focus this post on the applications that I have found for it. So, what exactly does \|\|= do? My own definition is that “double-pipe equals” is an operator that assigns a value, much like = or our classic assignment operator, but will only complete the assignment if the left side of our operation returns false or nil.
Let me demonstrate.

{% highlight ruby %}
a = nil
b = 4
a = b #=> 4
a #=> 4
{% endhighlight %}

With a set to nil, it is easy to see that setting a “equal” to b using the classic assignment operator would return a with the value of 4. But what if we used “double-pipe equals” instead?

{% highlight ruby %}
a = nil
b = 4
a ||= b #=> 4
a #=> 4
{% endhighlight %}


In this case, we get the same result. When a is set to nil (or anything that evaluates to false), the \|\|= operator functions the same as = would. Let’s look at an example where a is given a “truthy” value.

{% highlight ruby %}
a = 2
b = 4
a ||= b #=> 2
a #=> 2
{% endhighlight %}

In the example above, a retains its original value even though it has been operated on through our “double-pipe equals”. This happens because the \|\| acts as a “circuit” in this method. As Peter Cooper explains,

If the left hand side of the comparison is true, there's no need to check the right hand side. When ruby saw that a was already assigned to the value of 2, it stopped executing our code. Where I have found this sort of conditional assignment most useful is in iteration. Let’s iterate through an array of popular fruits, using our \|\|= method to assign each of the strings to a.

{% highlight ruby %}
a = nil
array = ["apple","orange","banana"]
array.each do |fruit|
   a ||= fruit
end #=> ["apple","orange","banana"]
a #=> "apple"
{% endhighlight %}

We can see that, after our iteration, a is assigned to the first string in our array, “apple” . After a becomes “apple”, our “double-pipe equals” will not let anything to the right of it reassign our variable.
While ruby has methods that can return the first element of an array without iteration, it can sometimes be useful to control for whether or not a variable has been assigned with a “truthy” value. Below is a code snippet from one of my recent labs where I found \|\|= particularly useful.

{% highlight ruby %}
class School
  attr_reader :roster
  def initialize(name)    
      @name = name    
      @roster = {}  
  end
  def add_student(name, grade)
      @roster[grade] ||= []
      @roster[grade] << name  
  end
end
{% endhighlight %}

Here, I have defined a class, School, along with a couple of methods. The key thing to understand is that by calling roster on an instance of my School class, I am looking to return my list of students as a hash of grades pointing to an array of students associated with each grade.
Lets instantiate an example school and populate some students.

{% highlight ruby %}
metro = School.new("Metro High")
metro.add_student("Jared", 9)
metro.roster #=> {9=>["Jared"]}
metro.add_student("Graham", 9)
metro.roster #=> {9=>["Jared","Graham"]}
{% endhighlight %}


To add a student to the roster of my School instance, I have to pass the add_student method a name and a grade. However, we can see that when I added “Graham” and his corresponding grade, 9, his name was added to the existing array that was created when I added “Jared”. This is the magic of \|\|=. In this case, the “double-pipe equals” operator recognized that a grade key has already been added and
Had my add_student method used = instead of \|\|=, I would have overwritten my student entry “Jared” when I added another student in grade 9.

Additional resources:

[What Ruby’s Double Pipe / Or Equals Really Does](http://www.rubyinside.com/what-rubys-double-pipe-or-equals-really-does-5488.html)

[The definitive list of OR Equal threads and pages](https://www.ruby-forum.com/topic/151660/)
