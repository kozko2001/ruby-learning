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
