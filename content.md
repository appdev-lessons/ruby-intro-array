# The Array class

Next, we have a _very_ important class: `Array`. Most of what we do as developers is manage _lists of things_. Lists of photos, likes, followers, reviews, listings, messages, rides, events, concerts, projects, etc etc etc.

The first data type we're going to learn to help us manage lists of things is `Array`. This class, unlike the ones we've seen until now, is really just a _container_ for other objects, and can hold however many objects we want.

## Creating arrays

As always, we have the formal way of creating a new object in Ruby: use the `.new` method on the parent class:

```ruby
cities = Array.new
pp cities.class
pp cities
```
{: .repl #array_new title="Array.new" points="1"}

### push 

As you can see, Ruby represents an `Array` with square brackets, `[]`. The brand new array is empty; let's add some **elements** to it with the `.push` method. Try this:

```ruby
cities = Array.new

cities.push("Chicago")
cities.push("NYC")
pp cities

cities.push("LA")
# Add some of your own, if you like

pp cities
```
{: .repl #array_push title="Array.push" points="1"}

Now we're talking! We've stored multiple strings within a single array using the `.push` method. Ruby separates the elements in an array with commas.

<aside markdown="1">
You might come across a shorthand for `.push`, the `<<` method, known as the "shovel" operator. This allows you to write something like: `cities.<<("Chicago")`

Or with the syntactic sugar that we're very accustomed to by now: `cities << "Chicago"`

I personally prefer `.push` — I think it's more readable — but feel free to use the shovel if you like it better.
</aside>

### Array literals 

Much like with `String`s, there's a shortcut to creating `Array`s. Rather than starting with `Array.new` and building it up from scratch one `.push` at a time, we can type an array "**literal**" directly into the code:

```ruby
cities = ["Chicago", "NYC", "LA"]
pp cities
```
{: .repl #array_literal title="Array literal" points="1"}

- What would happen to the previous `cities` variable if we wrote `cities = ["Berlin", "Paris", "Madrid"]` below our `pp` line?
- `cities` would contain the original cities and the new cities as two separate lists
    - Not quite, perhaps use the runnable code block to experiment
- `cities` would contain the original cities and the new cities as one combined list
    - Not quite, perhaps use the runnable code block to experiment
- We would overwrite `cities` with our new `Array` of cities
    - That's right! We can re-use variables and write new data into them
- This is an illegal operation and we would get an error message
    - Not quite, perhaps use the runnable code block to experiment
{: .choose_best #cities title="Cities" points="1" answer="3" }

## Methods

Now let's familiarize ourselves with some of `Array`'s methods.

### at

After adding elements to the list, the next most important thing we need to be able to do is retrieve an element back out from the list. Our first tool for doing that is `.at`.

The `.at` method takes an `Integer` argument, which is interpreted as the position, or **index**, in the `Array` of the element that you want to retrieve. Give it a try:

```ruby
cities = ["Chicago", "NYC", "LA", "SF", "NOLA"]

pp cities
pp cities.at(2)
```
{: .repl #at title="at" points="1"}

Whoa! Did you expect `cities.at(2)` to return `"LA"`? I sure didn't, the first time I tried it; I was expecting `"NYC"`.

It turns out that pretty much every programming language indexes the elements in an array starting at _zero_, not at one. So the first element is retrieved with `cities.at(0)`, the second element with `cities.at(1)`, etc. You'll get used to it after a while.

A couple of other things for you to experiment with:

 - What happens when you use an index greater than the length of the array?

    This is our first contact with `nil`, an object that represents **the absence of anything**. When you use an index "outside" the array, you might have expected to see an error message; but instead, Ruby returns `nil`.
 - What happens when you use a negative index?

Try it in the previous runnable code block!

- What did `.at(-1)` return on `cities`?
- NOLA
    - Yes! We can count backwards through a list of items starting with -1 (the last item)
{: .free_text #index_negative title="Negative index" points="1" answer="1" }

### at shorthand, [] 

There's a shorthand for `.at()` which is very common, so you should be familiar with it. It's the `.[]` method, so we _could_ write:

```ruby
cities = ["Chicago", "NYC", "LA", "SF", "NOLA"]

pp cities.[](2)
```
{: .repl #at_shorthand_1 title="at, .[](index)" points="1"}

You guessed it — there's some syntactic sugar coming up. When a class has a method named `.[]`, Ruby allows the dot to be dropped, but the method name has to then move immediately next to the object it's being called on (no space), and the argument moves _inside_ the method name! Altogether, this allows us to write:

```ruby
cities = ["Chicago", "NYC", "LA", "SF", "NOLA"]

pp cities[2]
```
{: .repl #at_shorthand_2 title="at, [index]" points="1"}

Which is sort of nice. I prefer `.at` because I think it reads better, but feel free to use the square brackets if you like that style better.

### first, last 

Since retrieving the elements at positions `0` (the first one) and `-1` (the last one) is so common, there are handy shortcut methods for those: `.first` and `.last`. Give them a try.

```ruby
cities = ["Chicago", "NYC", "LA", "SF", "NOLA"]

pp cities.first
pp cities.last
```
{: .repl #first_last title="first, last" points="1"}

- The code `[0, 4, 9][-1]`, the code `[0, 4, 9].at(-1)`, the code `[0, 4, 9].at(2)`, and the code `[0, 4, 9].last`...
- will return different results.
    - Nope, try to test the code in the runnable code block
- only the first two will return the same result
    - Nope, try to test the code in the runnable code block
- only the first two and fourth will return the same result
    - Nope, try to test the code in the runnable code block
- are all equivalent ways of retrieving the same value
    - Yes!
- are illegal operations, since we can't call methods directly on the array object (we need a variable first)
    - Nope, try to test the code in the runnable code block
{: .choose_best #retrieve title="Retrieve with .at or []" points="1" answer="4" }

In the graded code block below, make both tests pass by printing the square of the second to last `String` in `the_numbers` as a `Float` (recall `.to_i` and `.to_f`):

<div class="bg-red-100 py-1 px-5" markdown="1">

#### **STOP and read this before you solve the exercise**

In our graded code blocks, you will often see a grayed out area that you can't change, like the one below. This is usually a variable (or a few variables that are randomly sampled) that we provide for you to try and write code that works for _each_ of the potential inputs in the gray area. 

That means if the grayed area gave you:

```ruby
the_numbers = ["1", "3", "5", "18"]
```

You should try and only use the variable `the_numbers` to write your code and you **should not try to redefine `the_numbers` on a later line** as e.g.

```ruby{3}
the_numbers = ["1", "3", "5", "18"]
# write your program here
the_numbers = ["9", "2", "7"]

pp the_numbers[-2]
```

Rather, you would write your code such that our provided variable outputs the expected result from the question description.

In the imaginary world of our tests below each code block, the `the_numbers = ["1", "3", "5", "18"]` grayed out line is replaced by, e.g. `the_numbers = ["9", "2", "7"]`. _Our tests can modify the grayed area, but you cannot_.

The takeaway: You should not try to hard code the test requirements. Get your code to pass for all of the inputs that we supply in the grayed out area; then, when you run the tests, all of them should pass. The tests will replace the grayed area with a few different inputs to see if those cases also pass.
</div>

```ruby
the_numbers = ["1", "3", "5", "18"]
# write your program here
```
{: .repl #element_squared title="Array element squared" readonly_lines="[1]"}

```ruby
describe "Array element squared" do
  it "outputs 4.0 given the input ['9', '2', '7']" do
    path = "/tmp/code.rb"

    # replace the_numbers
    file = File.read(path)
    new_content = file.split("\n")
    new_content = new_content.map { |line| line == 'the_numbers = ["1", "3", "5", "18"]' ? 'the_numbers = ["9", "2", "7"]' : line }.join("\n")
    File.open(path, 'w') { |line| line.puts new_content }

    File.foreach(path) do |line|
      if line.match(/^p.*4.0/)
        expect(line).to_not match(/4.0/),
          "Expected graded code block to NOT print the Integer literal '4.0', but did."
      end
    end

    expect { require_relative(path) }.to output(/4.0/).to_stdout
  end
end
```
{: .repl-test #element_squared_test_1 for="element_squared" title="Array element squared outputs 4.0 given the input ['9', '2', '7']" points="1"}

```ruby
describe "Array element squared" do
  it "outputs 9.0 given the input ['4', '6', '3', '2']" do
    path = "/tmp/code.rb"

    # replace the_numbers
    file = File.read(path)
    new_content = file.split("\n")
    new_content = new_content.map { |line| line == 'the_numbers = ["1", "3", "5", "18"]' ? 'the_numbers = ["4", "6", "3", "2"]' : line }.join("\n")
    File.open(path, 'w') { |line| line.puts new_content }

    File.foreach(path) do |line|
      if line.match(/^p.*9.0/)
        expect(line).to_not match(/9.0/),
          "Expected graded code block to NOT print the Integer literal '9.0', but did."
      end
    end

    expect { require_relative(path) }.to output(/9.0/).to_stdout
  end
end
```
{: .repl-test #element_squared_test_2 for="element_squared" title="Array element squared outputs 9.0 given the input ['4', '6', '3', '2']" points="1"}

### index 

The `.index` method is sort of the inverse of `.at`: given an object, `.index` searches within the array and returns the index where it resides. Give it a try:

```ruby
cities = ["Chicago", "NYC", "LA", "SF", "NOLA"]

pp cities.index("SF")
```
{: .repl #array_index title="index" points="1"}

- What will `.index` return if the element is present in the array more than once (e.g. `[0, 1, 3, 3, 3].index(3)`)?
- The index of all the elements
    - Nope, try to test the code in the runnable code block
- The index of the first appearance of the element
    - Yes!
- An error message
    - Nope, try to test the code in the runnable code block    
- The index of the last appearance of the element
    - Nope, try to test the code in the runnable code block
- A `nil`, or empty, result
    - Nope, try to test the code in the runnable code block
{: .choose_best #index_first title="First index" points="1" answer="2" }

- What will `.index` return if the element is not present in the array at all (e.g., `[0, 1, 3, 3, 3].index(2)`)?
- The index of all the elements
    - Nope, try to test the code in the runnable code block
- An error message
    - Nope, try to test the code in the runnable code block
- The index of the last appearance of the element
    - Nope, try to test the code in the runnable code block
- A `nil`, or empty, result
    - Yes
{: .choose_best #index_none title="Index absent" points="1" answer="4" }

### String#split 

Before we proceed with more `Array` methods, I want to go back for a minute and talk about a method for the `String` class: `.split`. This method, when called on a `String`, will return an `Array` of substrings.

If you provide no argument, the string is split upon whitespace, which is handy for e.g. turning a sentence into a list of words:

```ruby
pp "alice bob carol".split
```
{: .repl #string_split title="String#split" points="1"}

If you do provide an argument to `.split`, then the string will be chopped up wherever that argument occurs instead of whitespace — for example, use `"4,8,15,16,23,42".split(",")` to split on commas.

You can also `split` with the empty string, `""`, as an argument in order to turn a string into an `Array` of its individual characters:

```ruby
a = "Hello!".split("")

pp a
pp a.at(0)
pp a.at(-1)
```
{: .repl #string_split_args title="String#split argument" points="1"}

### count 

`.count` counts how many elements are in the list, if called with no arguments. If an argument is provided, it counts how many times that argument occurs in the list.

```ruby
a = [8, 3, 1, 19, 23, 3]

pp a.count

pp a.count(3)
```
{: .repl #array_count title="count" points="1"}

- The code `["zebra", "bear", "bear", "giraffe"].count("bear")` will return...
- 2
    - Yes!
{: .free_text #count_argument title="Count arguments" points="1" answer="1" }

### sample 

Try it out:

```ruby
an_array = [8, 3, 1, 19, 23, 3]

pp an_array.sample
```
{: .repl #array_sample title="sample" points="1"}


- The code `["rock", "paper", "scissors"].sample` will return...
- `nil`, or nothing
    - Not quite, try it in the runnable code block
- an unpredictable item from the array
    - Yes!
- that's an illegal operation and would result in an error message
    - Not quite, try it in the runnable code block
{: .choose_best #rps_sample title="Rock Paper Scissors" points="1" answer="2" }

### min, max, sum

```ruby
a = [8, 3, 1, 19, 23, 3]

pp a.min
pp a.max
pp a.sum
```
{: .repl #array_min_max_sum title="min, max, sum" points="1"}


In the graded code block below, using the given `Array` of numbers, output:
  - the number with the lowest value, 
  - the number with the highest value, 
  - the difference between the highest value and the lowest value,
  - and the sum of values. 

The program should have the follow output format:

"The lowest is X, the highest is X, the difference is X, the sum is X."

Be sure your _copy matches exactly_ ("The lowest is..."), replacing "X" with your calculated numbers.

```ruby
the_array = [12, 23, 41, 73, 19, 6]
# write your program here
minimum = 
maximum = 
diff = 
sum = 
pp "The lowest is "
```
{: .repl #min_max_sum title="min, max, sum" readonly_lines="[1]"}

```ruby
describe "min, max, sum" do
  it "should print 'The lowest is 6, the highest is 73, the difference is 67, the sum is 174.'" do
    path = "/tmp/code.rb"
    File.foreach(path) do |line|
      if line.match(/^p.*"The lowest is 6, the highest is 73, the difference is 67, the sum is 174."/)
        expect(line).to_not match(/The lowest is 6, the highest is 73, the difference is 67, the sum is 174./),
          "Expected graded code block to NOT print the String literal 'The lowest is 6, the highest is 73, the difference is 67, the sum is 174.', but did."
      end
    end
    
    expect { require_relative(path) }.to output(/The lowest is 6, the highest is 73, the difference is 67, the sum is 174./).to_stdout
  end
end
```
{: .repl-test #min_max_sum_test_1 for="min_max_sum" title="min, max, sum should print 'The lowest is 6, the highest is 73, the difference is 67, the sum is 174.'" points="1"}

##  Conclusion

That's it for `Array`s. Now we'll have a look at **conditionals** with `if` statements.

- Approximately how long (in minutes) did this lesson take you to complete?
{: .free_text_number #time_taken title="Time taken" points="1" answer="any" }

<span style="font-size: large">**When you are done here, close the window and return to Canvas for the next lesson in the series.**</span>

----
