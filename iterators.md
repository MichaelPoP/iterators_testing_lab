##Descriptions of Iterators

###Instructions
Below you will find a list of methods. In the space provided below each, please provide a brief description of what this method does based upon your review of the Docs. 

###Array methods:
May be helpful to look in [Enumerable](http://ruby-doc.org/core-2.2.0/Enumerable.html) as well...
#------------------------------------------------------------------
####select:
returns an array of elements, when a given block returns a _true_ value
-
returns an Enumerator, when no block is given (*what is an enumerator?)

#######EXAMPLES#######

(1..10).find_all { |i|  i % 3 == 0 }   #=> [3, 6, 9]

[1,2,3,4,5].select { |num|  num.even?  }   #=> [2, 4]
#------------------------------------------------------------------
####reject:
returns an array of elements, when a given block returns a _false_ value
-
returns an Enumerator, when no block is given

#######EXAMPLES#######

(1..10).reject { |i|  i % 3 == 0 }   #=> [1, 2, 4, 5, 7, 8, 10]

[1, 2, 3, 4, 5].reject { |num| num.even? } #=> [1, 3, 5]
#------------------------------------------------------------------
####map:
returns an array of elements, containing the results of running a given block on every element given to it (in enum)
-
returns and Enumerator, when no block is given

#######EXAMPLES#######

(1..4).map { |i| i*i }      #=> [1, 4, 9, 16]
(1..4).collect { "cat"  }   #=> ["cat", "cat", "cat", "cat"]
#------------------------------------------------------------------
####detect:
returns the first element which is not _false_, when each element (in the array/enum) is passed into block
-
returns nil when result is not specified

#######EXAMPLES#######

(1..10).detect   { |i| i % 5 == 0 and i % 7 == 0 }   #=> nil
(1..100).find    { |i| i % 5 == 0 and i % 7 == 0 }   #=> 35
#------------------------------------------------------------------
####inject:
returns the resulting value of the combination of all elements in the array/enum, when a binary operation is performed => a method can also be performed on all elements in order to combine them

#######EXAMPLES#######

# Sum some numbers
(5..10).reduce(:+)                             #=> 45
# Same using a block and inject
(5..10).inject { |sum, n| sum + n }            #=> 45
# Multiply some numbers
(5..10).reduce(1, :*)                          #=> 151200
# Same using a block
(5..10).inject(1) { |product, n| product * n } #=> 151200
# find the longest word
longest = %w{ cat sheep bear }.inject do |memo, word|
   memo.length > word.length ? memo : word
end
longest                                        #=> "sheep"
#------------------------------------------------------------------
####partition:
returns _two_ arrays; first array, when a given block returns a _true_ value; second array, contains the rest
-
returns an Enumerator, when no block is given

#######EXAMPLES#######

(1..6).partition { |v| v.even? }  #=> [[2, 4, 6], [1, 3, 5]]
#------------------------------------------------------------------
####sort:
returns an array of sorted elements, when given an array/enum based on the their own method or an included block

#######EXAMPLES#######

%w(rhea kea flea).sort          #=> ["flea", "kea", "rhea"]
(1..10).sort { |a, b| b <=> a }  #=> [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
#------------------------------------------------------------------
####one:
returns a boolean value; returns _true_, when each element passes into a given block and returns _true_ exactly once; returns _false_, when more than one element returns true

#######EXAMPLES#######

%w{ant bear cat}.one? { |word| word.length == 4 }  #=> true
%w{ant bear cat}.one? { |word| word.length > 4 }   #=> false
%w{ant bear cat}.one? { |word| word.length < 4 }   #=> false
[ nil, true, 99 ].one?                             #=> false
[ nil, true, false ].one?                          #=> true
#------------------------------------------------------------------
####none:
returns a boolean value; returns _true_, when each element passes into a given block and never returns _true_; returns _false_ otherwise
-
returns true if none of the elements are true, when a block is not given

#######EXAMPLES#######

%w{ant bear cat}.none? { |word| word.length == 5 } #=> true
%w{ant bear cat}.none? { |word| word.length >= 4 } #=> false
[].none?                                           #=> true
[nil].none?                                        #=> true
[nil, false].none?                                 #=> true
#------------------------------------------------------------------
####all:
returns a boolean value; returns _true_, if the block never returns false or nil; returns _false_, otherwise.
-
returns true, when a block is not given, adding an implicit block of { |obj| obj} which causes all? to return _true_, when none of the collection members are false 

#######EXAMPLES#######

%w[ant bear cat].all? { |word| word.length >= 3 } #=> true
%w[ant bear cat].all? { |word| word.length >= 4 } #=> false
[nil, true, 99].all?                              #=> false
#------------------------------------------------------------------
####empty?:
returns boolean; _true_, when self(the array) contains no elements

#######EXAMPLES#######

[].empty?   #=> true
#------------------------------------------------------------------
####eql?:
returns boolean; _true_, when 'self' and 'other' are the same object or when both arrays have equal elements

#------------------------------------------------------------------
####include?:
returns a boolean; _true_, when any element fo the array/enum equals obj. (Equality is tested using ==)

#######EXAMPLES#######

a = [ "a", "b", "c" ]
a.include?("b")   #=> true
a.include?("z")   #=> false
#------------------------------------------------------------------
####nil?:
returns a boolean; _true_, when given an input of nil; _false_, otherwise
->basically only does that

#######EXAMPLES#######

Object.new.nil?   #=> false
nil.nil?          #=> true
#------------------------------------------------------------------
###Hash methods####
#------------------------------------------------------------------
####key?:
returns a boolean; _true_ when the given key is present in the hash; _false_, otherwise.

#######EXAMPLES#######

h = { "a" => 100, "b" => 200 }
h.has_key?("a")   #=> true
h.has_key?("z")   #=> false

#------------------------------------------------------------------
####keys:
returns a new array populated with the keys from the given hash

#######EXAMPLES#######

h = { "a" => 100, "b" => 200, "c" => 300, "d" => 400 }
h.keys   #=> ["a", "b", "c", "d"]
#------------------------------------------------------------------
####delete:
returns a _value_ corresponding to a key which matches a given _key_; if no key is found returns the default value
-
also, given option to return a code block when a key is not found 
ex: hash.delete("x") { |el| "#{el} not found" }   #=> "z not found"

#######EXAMPLES#######

h = { "a" => 100, "b" => 200 }
h.delete("a")                              #=> 100
h.delete("z")                              #=> nil
h.delete("z") { |el| "#{el} not found" }   #=> "z not found"
#------------------------------------------------------------------
####delete_if:
returns deleted key-value pairs, when a given block evaluates them as true.
-
returns an Emumerator, when no block is given

#######EXAMPLES#######

h = { "a" => 100, "b" => 200, "c" => 300 }
h.delete_if {|key, value| key >= "b" }   #=> {"a"=>100}




