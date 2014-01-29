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

    x -> param { puts param } ## alternative way to do a lambda    