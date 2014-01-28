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