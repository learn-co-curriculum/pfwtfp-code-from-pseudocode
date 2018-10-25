# Code from Pseudocode

## Learning Goals

- Create Code from Pseudocode

## Introduction

We have pseudocode ready to go! We're finally at our last step in the Flatiron
Process: _encoding_ or _translating_ into the language that a computer can
understand.

Let's try translating this from the Real World into Ruby.

We'll provide some stub code so that the pseudocode can be tested.

```ruby
# Given code
# Creates a thing called demo_baguette that has a type (string) and length (value)
require 'ostruct'
demo_baguette = OpenStruct.new(:type => "flour", :length => 60)

# Since Ruby doesn't feature things like rulers, we'll ask the baguette to
# tell us its length
def measure(b)
  b.length
end

# Since Ruby doesn't feature things like rulers, we'll change the bread's
# length to simulate "cutting." We return the shortened bread and a String
# that represents the "piece."

def cut_bread(b,len)
  b.length -= len
  ["A piece of #{b.type} bread", b]
end

## Pseudocode
#  Procedure DivideBaguetteEvenly(baguette, n):
#    baguette_length = measure(baguette)
#    even_length = baguette_length / n
#    collection = []
#
#    while baguette_length >= even_length:
#      piece, rest = cut_bread(baguette, even_length)
#      collection.add(piece)
#
#      baguette = rest
#      baguette_length = measure(baguette)
#
#    even_pieces = collection
#    return even_pieces

def divide_baguette_evenly(baguette, n)
 # We'll translate this in the lesson. Eventually it should be replaced with
 # our Ruby version of the pseudocode.
end

# Call our method
p divide_baguette_evenly(demo_baguette, 3)
```

## Translation

Translating, or _encoding_ i.e. "writing the concept as code" is really easy
once we have our pseudocode. The only major change is to use `<<` instead of
`add` for the collection `Array`.

```ruby
def divide_baguette_evenly(baguette, n)
  baguette_length = measure(baguette)
  even_length = baguette_length / n
  collection = []

  while baguette_length >= even_length do
    piece, rest = cut_bread(baguette, even_length)
    collection << piece

    baguette = rest
    baguette_length = measure(baguette)
  end

  even_pieces = collection
  return even_pieces
end
```

And the output? Well, try it out for yourself! Put this code for the definition
of `divide_baguette_evenly` into the nearly-complete sample.

## Conclusion

Using the Flatiron Process of problem solving and the Triangle Process of
debugging we went from need, to pseudocode, to debugged pseudocode, to working
code.

If you build up your code in this fashion it will _never_ get away from you.
You will always have working code that gains capabilities to achieve larger and
larger problems.
