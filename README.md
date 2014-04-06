ruby-learning
=============

Ruby language cheat-sheet to remember everything I feel interesting about the language while I'm learning. Basically at the beggining is about the book I'm reading right now.

* Programming Ruby 1.9 3rd Edition --- Dave Thomas
* [http://www.zenspider.com/Languages/Ruby/QuickRef.html](http://www.zenspider.com/Languages/Ruby/QuickRef.html)

`irb` -> interactive ruby console 


### Function definition

    def hello(name)
      return "Hello, " + name
    end
    
    puts hello("Jordi")
    
    
### Array and Dictionaries

###### Array

    a = [ 1, 'cat', 3.14 ]
    puts "element #{a[0]}"
    
    a = %w{ ant bee cat dog elk } (I really don't understand it...)
    
###### Dictionary
    
    dict = {
      'red'  => 'FF0000',
      'blue' => '00FF00',
      'green'=> '0000FF'	}

    
### variables names

**Local variables**: lowercase with underscores as separators

**global**: starts with dollar $global_var

**instance var**: starts with **@** @x @name

**class var** : starts with **@@** 

### Symbols

instead of using constants and define a value you can use `symbols` 

`nextState(:expanded)` automatically creates a constant expanded with unique value, very useful for keys in a dictionary

    dict = { 
    	expanded: 'Expandido' 
    }
    


### Control structures

##### if / elsif / else 

    if numRetries > 3
      puts "You have a lot to do yet"
    elsif numRetries <= 0
      puts "no more retries..."
    else
      puts "something..."
    end
    
##### while 
    while line = gets
    	puts line.downcase
    end 
    
### Regular Expressions

Nicely inside the language 

`if line =~ /Perl|Python/`

`line.sub(/Perl/, 'Ruby')`

`line.gsub(/Perl|Python/, 'Ruby')`

### Blocks 

example:

    def test
      puts "Start"
      yield 
      yield
      puts "End"
    end
    
    test { puts " Middle block" }
    
When calling a function apart from the parameters we can transfer a `block`, a chunk of code that the function can execute like a callback using the keyword **yield**

example:
`animals.each {|animal| puts animal }` `upto(6) {|i| print i }`

### Classes

    class MathConcrete < SuperClass
      def initialize(arg0, arg1)
    	@arg0 = arg0
    	@arg1 = arg1
      end
    end
    def to_s
      "ARG0: #{@arg0} ARG1: #{@arg1}"
    end
    math = MathConcrete.new(3, 4)
    
`p` is a statement for prety print an object

##### Setters and getters

    def arg0 ## readonly accessor
      return @arg0
    end 

    def arg1=(arg1) ## setter
      @arg1 = arg1
    end

or also 

    class MathConcrete
      attr_reader :arg0 ## now is not necessary to define a arg0 function/accessor
      attr_accessor :arg1 ## nor the setter 
    end
    
##### Class methods Visibility

    class MyClass        def method1        end      protected        def method2        end      private        def method3        end	end
or also you can define the visibility at the end
    class X
	  def func1
	  end
	  
	  def func2
	  end	  
	  
	  protected   :func1, :func2
	  private     :func44    end     
`obj.class`
`obj.object_id`
`obj.dup` duplicates the object (java clone)

`obj.freeze` runtime error when modify the object
### Arrays and Hashes
##### Arrays 
    a = [ 1, 3, 9, 10, 100, 3.14, "HOLA"]
	a.length => 7
	a[0] => 1
	a[-1] => "HOLA"
	a[start, count] => a[0, 2] => [1, 3]
	a[-3, 2] => [100, 3.14]
	a[1..2]  => [3, 9] ## ranges from position 1 to position 2 (end 2 included)
	a[1...2] => [3] ## range from position 1 to position 2 (end not included)
	a.push "red"
	a.pop  => "red"
	a.shift => 1 ## the first element is removed
	a.first => 3
	a.last => 3.14
	a << "COSA..."
	
Some blocks with arrays and hashes

    dict.each do |key, value|
      puts "#{key}: #{value}"
    end
    
    array.each do |value| 
      puts "#{value}"
    end 
    
User on file object 

    f = File.open("AAA")
    f.each do |line|
    	puts line
    end
    f.close

python Reduce
    
    [1, 3, 5, 7].inject(0) {|sum, element| sum+element} 

python items()
    
    ['a', 'b', 'c'].each_with_index{ |item, index| index+= 1 }

if the last paramet of a function starts with & it converts the block to a local variable of type Proc that we can store, and execute later. other ways of converting a block into an object:

    x = lambda { |param| puts param } ## x is a Proc instance
    x.call "HI"

    x -> param { puts param } ## alternative way to do a lambda (1.9)
    x -> param1, param2 { puts param2 } ## with multiple parameters 

### Modules, Inheritance and mixins

#### Module example 

    module Mod
      def Mod.ttt(x)
        print x
      end
    end
    
    require Mod
    Mod.ttt(2)

you can include a Module on a class, if done all the methods of the module are mixed in the class making them available

    class Class
      include Mod
    end
    
    c = Class.new()
    c.ttt(2)

Using the ruby library we can `include Comparable`, this mixin defines 6 operators (=,<,>,<=,>=,!=) and requires that
the class that include it `def <=> (other)` to know how to sort elements. Something similar happens with `include Enumerable` and `def each` -> map, findi\_all etc..

Ruby only supports single inheritance, but just allow you to include mixins functionality. traits of a another class.

### Standard library

#### numbers

    3.times { print "X" }
    1.upto(5) { |i| print i }
    99.downto(95) { |i|...}
    50.step(80, 5)....

#### strings

   "Seconds/day: #{24*60*60}"
   "{'Ho!' * 3} Mery Christmas"
   "now is #{ def the(a) 
                  'the ' + a
              end 
              the('time' 
            } ..."

  %q/general single-quoted string/ ## other way to generate a single quoted string
  %Q!general double-quoted string! ## Q is optional and ! is the delimiter could be anything, if is (,[,{,< must match the ),],},>
  %Q{Other delimiter}

#### ranges 
    1..10
    'a'..'z'
    0..."cat".length

    1..10.to\_a ## converts to array
    1..10.max 

    (1..10) === 5 ## test if 5 in range

### Regular expressions

   "dog and cat =~ /cat/ => 8 ## 8 is when the regex match
   "dog" =~ /cat/ => nil
   "dog and cat".sub(/cat/, "mouse) ## sub -> only once gsub globally

### Methods 

Method naming:
  if returns a boolean must be suffixed with ?
  if modify the parameters must suffix with ! (as they are dangerous)
  if the method can appear on the left side of an assigment suffix with =

Optional arguments `def func(arg1="hello")`
vararg arguments   `def func(arg1, *vararg)` func(1,2,3,4) => vararg = [2,3,4]
                   `def func(arg1 *vararg, last) func(1,2,3,4) => vararg = [2,3], last= 4

func(1, 2, 3) === func 1, 2, 3


Expanding collection in method calls 
    def five(a, b, c, d, e)
    
    (1,2,3,*['a','b']) 
    five(*['a','b'],1,2,3) 
    five(*(10..14)) 
    five(*[1,2], 3, *(4..5))

If the last argument to a method is preceded by an ampersand, Ruby assumes that it is a Proc object. It removes it from the parameter list, converts the Proc object into a block, and associates it with the method.

operators 
   `def +(other)`
   `def <<(score)`
   `def [](p1, p2, p3)` ## a[5,9, 102]
   `def []=(*params)`

usage of `\`date\`` exampans to command line result like bash

like python => a, b = [1, 4] => a = 1, b = 4
            => a, b = [1, 2, 3, 4, 5] => a = 1, b = 2

defined? => returns nil if its argument is not defined

defined? strange_var => nil
defined? 1 => "expression"
defined? printf => "method"

case expressions

  case
  when song.name == "Misty"
    puts "Not again!" 
  when song.duration > 120
    puts "Too long!" 
  when Time.now.hour > 21
    puts "It's too late" 
  else
    song.play
  end

### Exceptions

    try {
    } catch( Exception e )  {
    } finally {
    }

on ruby:

    begin
     ...
    rescue
     ... # handle error
    else 
     ... ## congrats no error
    ensure
     f.close
    end

Raising a exception

    raise
    raise "bad mp3 encoding"
    raise InterfaceException, "Keyboard failure", caller


### Basic IO

Opening a file ...

    file = File.new("testfile", "r") 
    # ... process the file 
    file.close

Reading lines of a file using iterators

    File.open("file") do |file| 
      file.each_line {|line| puts "l #{line.dump}" }
    end

Writing file 
    file.puts "HELO"

