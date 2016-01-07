# Ruby



## Basics

REPL: `irb`

### Import Libraries

Example:
```ruby
require 'name_of_library'
```

### Method Definition

Example:
```ruby
def method_name(param1, param2)
  # Implementation here (indent with 2 spaces)
  # The value of the last statement is the return value
end
```

### Class Definition

Example:
```ruby
# The FullName class
class FullName
  def initialize(given_name, family_name)
    @gn = given_name
    @fn = family_name
  end

  def salute
    puts "Hello, #{@gn} #{@fn}!"
  end
end

# Create a new object
name = FullName.new("Kenji", "Asuka")

# Output "Hello, Kenji Asuka!"
name.salute
```

### Assignment

Example:
```ruby
answer = 42
```

### Equality

#### `==` (Value Equality)

> At the `Object` level, `==` returns `true` only if `obj` and `other` are the same object.
> Typically, this method is overridden in descendant classes to provide class-specific meaning.

#### `===` (Case Equality)

> For class `Object`, effectively the same as calling `#==`,
> but typically overridden by descendants to provide meaningful semantics in `case` statements.

Example:
```ruby
case some_object
when /a regex/
  # The regex matches
when 2..4
  # some_object is in the range 2..4
when lambda {|x| some_crazy_custom_predicate }
  # the lambda returned true
end
```

#### `eql?` (Hash Equality)

> The `eql?` method returns true if `obj` and `other` refer to the same hash key.
> This is used by `Hash` to test members for equality.
> For objects of class `Object`, `eql?` is synonymous with `==`.
> Subclasses normally continue this tradition by aliasing `eql?` to their overridden `==` method,
> but there are exceptions.
> `Numeric` types, for example, perform type conversion across `==`, but not across `eql?`,
> so:
> ```ruby
> 1 == 1.0     #=> true
> 1.eql? 1.0   #=> false
> ```

#### `equal?` (Identity Equality)

> Unlike `==`, the `equal?` method should never be overridden by subclasses:
> it is used to determine object identity
> (that is, `a.equal?(b)` iff `a` is the same object as `b`).

See: http://stackoverflow.com/q/7156955/142239



## Fixnum (Native Machine Integers)

### Arithmetic Operations

Name                | Method | Example | Result
------------------- | ------ | ------- | ------
Addition            | +      | 11 + 5  | 16
Subtraction         | -      | 11 - 5  | 6
Multiplication      | *      | 11 * 5  | 55
Euclidean Division  | /      | 11 / 5  | 2
Euclidean Modulo    | %      | 11 % 5  | 1
Exponentiation      | **     | 11 ** 5 | 161051

### Bit Operations

Name                   | Method | Example     | Result
---------------------- | ------ | ----------- | ------
Negate                 | ~      | ~11         | -12
Bitwise OR             | &#124; | 11 &#124; 5 | 15
Bitwise AND            | &      | 11 & 5      | 1
Bitwise XOR            | ^      | 11 ^ 5      | 14
Arithmetic Left Shift  | <<     | 11 << 3     | 88
Arithmetic Right Shift | >>     | 11 >> 3     | 1

### Other Operations

Name              | Method | Example | Result
----------------- | ------ | --------| ------
Convert to String | to_s   | 42.to_s | "42"


### Euclidean Division and Modulo

Division | Result | Modulo    | Result | Expression
-------- | ------ | --------- | ------ | -----------------------
11 / 5   | 2      | 11 % 5    | 1      | 11 = 5 * 2 + 1
11 / -5  | -3     | 11 % -5   | -4     | 11 = (-5) * (-3) + (-4)
-11 / 5  | -3     | -11 % 5   | 4      | -11 = 5 * (-3) + 4
-11 / -5 | 2      | -11 % -5  | -1     | -11 = (-5) * 2 + (-1)

### Visualizing Euclidean Division and Modulo

|        |     |     |         |     |     |
| ------ | --- | --- | ------- | --- | --- |
| 5 * 3  | 15  |     | -5 * 3  | -15 |     |
|        | 11  |     |         | -11 |     |
| 5 * 2  | 10  | *   | -5 * 2  | -10 | *   |
| 5 * 1  | 5   |     | -5 * 1  | -5  |     |
| 5 * 0  | 0   |     | -5 * 0  | 0   |     |
| 5 * -1 | -5  |     | -5 * -1 | 5   |     |
| 5 * -2 | -10 |     | -5 * -2 | 10  |     |
|        | -11 |     |         | 11  |     |
| 5 * -3 | -15 | *   | -5 * -3 | 15  | *   |

Observation:
The one which is "equal to or just less than" the dividend is selected as the "product",
then the quotient and the remainder follow.

5.times { print "Hello" }

Documentation: http://ruby-doc.org/core/Fixnum.html



## Strings

Single quote (no escape sequence): `'Hello\tworld'` == `"Hello\\tworld"`

Double quote (escape sequence available): `"Hello\tworld"`

### Methods

#### General Operations

Name          | Method   | Example           | Result
------------- | -------- | ----------------- | ------------
Length        | length   | "Kenji".length    | 5
Concatenation | +        | "Kenji" + 65.to_s | "Kenji65"
Append        | <<       | "Kenji" << 65     | "KenjiA"
Copy          | *        | "Kenji" * 2       | "KenjiKenji"
Format        | %        | "%05d" % 123      | "00123"
Reverse       | reverse  | "Kenji".reverse   | "ijneK"
Lowercase | downcase |
Remove Characters | delete |
Split the string based on a delimiter | split | "K:e:n:j:i".split(":") |
Strip leading and trailing whitespace | strip | " Kenji ".strip | "Kenji"

#### Element Operations

Name               | Method   | Example               | Result
------------------ | -------- | --------------------- | ---------------------------------
Element Reference  | []       | "Kenji"[3, 2]         | "ji"
Element Reference  | []       | "Kenji"["en"]         | "en"
Element Assignment | []=      | "Kenji"["e"] = "a"    | "a" (the variable becomes "Kanji"
Containment        | include? | "Kenji".include? "en" | true

#### Conversion Operations

Name                           | Method | Example                     | Result
------------------------------ | ------ | --------------------------- | -------------------------------
Convert to array of bytes      | bytes  | "Kenji".bytes               | [75, 101, 110, 106, 105]
Convert to array of characters | chars  | "Kenji".chars               | ["K", "e", "n", "j", "i"]
Convert to array of lines      | lines  | "Hello\nWorld\nKenji".lines | ["Hello\n", "World\n", "Kenji"]

Documentation: http://ruby-doc.org/core/String.html



## Arrays

Empty Array: `[]`

Non-empty Array: `[12, 47, 35]`

### Methods

Name                               | Method | Example             | Result
---------------------------------- | ------ | ------------------- | ------------
Length                             | length | [12, 47, 35].length | 3
Index                              | []     | [12, 47, 35][2]     | 35
Maximum                            | max    | [12, 47, 35].max    | 47
Sort (returns new copy)            | sort   | [12, 47, 35].sort   | [12, 35, 47]
Sort (in place)                    | sort!  | [12, 47, 35].sort!  | [12, 35, 47]
Join the elements to form a string | join   | [12, 47, 35].join   | "124735"

[12, 47, 35].each { |x| print x + 1, " " } | [12, 47, 35] (prints "13 48 36 ")

Documentation: http://ruby-doc.org/core/Array.html



## Hashes

Empty Hash: `{}`, `Hash.new(0)`

Non-empty Hash: `{"Hello"=>1, "World"=>2}`

### Methods

Name      | Method | Example                           | Result
--------- | ------ | --------------------------------- | ------------------
Length    | length | {"Hello"=>1, "World"=>2}.length   | 2
Index     | []     | {"Hello"=>1, "World"=>2}["Hello"] | 1
Key Set   | keys   | {"Hello"=>1, "World"=>2}.keys     | ["Hello", "World"]
Value Set | values | {"Hello"=>1, "World"=>2}.values   | [1, 2]

Documentation: http://ruby-doc.org/core/Hash.html



## Symbols

:hp

:mp

Documentation: http://ruby-doc.org/core/Symbol.html


## Kernel

Documentation: http://ruby-doc.org/core/Kernel.html