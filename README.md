# Title

## Learning Goals

- Create Code from Pseudocode

## Introduction

We have pseudocode ready to go! Let's code it up.

## Step 6: Step 6: Verify the Procedure's Output

Let's try working with the pseudocode. Here is the code again.

```text
Procedure DivideBaguetteEvenly(baguette, n):
  baguette_length = measure(baguette)
  even_length = baguette_length / n
  collection = []

  while baguette_length > even_length:
    piece, rest = cut_bread(baguette, even_length)
    collection.add(piece)

    baguette = rest
    baguette_length = measure(baguette)

  even_pieces = collection
  return even_pieces
```

An awesome technique for debugging pseudocode problems (and an awesome
technique in whiteboard interviews too) is to build a variable table. List all
the inputs (Step 4), the state of the output (Step 2), and any local variables
used in the implementation:

|Variable|State|State|State|State|State|State|State|State|State|
|--------|-----|-----|-----|-----|-----|-----|-----|-----|-----|
|Input: `baguette`|||||||||||
|Input: _n_|||||||||||
|Output: even_pieces|||||||||||
|Local: `baguette_length`|||||||||||
|Local: `even_length`|||||||||||
|Local: `collection`|||||||||||

Let's fill in this table together for the first pass.

|Variable|State|State|State|State|State|State|State|State|State|
|--------|-----|-----|-----|-----|-----|-----|-----|-----|-----|
|Input: `baguette`|||||||||||
|Input: _n_|||||||||||
|Output: even_pieces|||||||||||
|Local: `baguette_length`|||||||||||
|Local: `even_length`|||||||||||
|Local: `collection`|||||||||||

We don't know what's in `baguette`, so let's just put `thing with a length` in
there. Maybe it will be an instance of a class, maybe it'll be a `Hash`. Who
knows. It might not even matter.

`n` will wind up staying constant (the number of friends). For testing our
pseudocode, let's set it to `3`.

`even_pieces` is something we'll return at the end, but as we start the
Procedure, it's empty.

`baguette_length` is something that we're counting on a made-up helper to help
us figure out. Let's assume that the helper does its job correctly. Let's just
pick a good value to work with. We'll use `60`.

The remaining `Locals` are empty.

Step through the pseudocode and make changes to this table in a piece of paper.
See whether this code works like it should.

## Checking your Variable State Table

Again, while we're not testing _code_ we can use some of its conventions to
help test our _pseudocode_. Imagine calling our Procedure with a baguette and a
3-person party.

```text
DivideBaguetteEvenly( <60cm length baguette>, 3)
```

Here's how the table fill out:

|Variable|State|State|State|State|State|State|State|State|State|
|--------|-----|-----|-----|-----|-----|-----|-----|-----|-----|
|Input: `baguette`| (something with a length)|40cm baguette|20cm baguette||||||||
|Input: _n_|3||||||||||
|Output: even_pieces|[]|[20cm piece, 20cm piece]|||||||||
|Local: `baguette_length`|(stub: 60)|40|20||||||||
|Local: `even_length`|20||||||||||
|Local: `collection`|[20cm piece]|[20cm piece, 20cm piece]|||||||||
|Local: `rest`|40cm baguette|20cm baguette|||||||||
|Local: `piece`|20cm piece|20cm piece|||||||||

Output: `[20cm piece, 20cm piece]`

That's not right. 60cm among 3 should be 3 pieces. Using the table, we should
be able to debug what went wrong.


## Introducing the Triangle Process of Debugging

Whenever we debug we should always "block off" the code or pseudocode that's
causing the problem. In this case we're going to be looking at the Procedure.

* Were its inputs correct?
* Were its outputs correct?
* Was the implementation correct

* Our inputs were correct.
* Our output was incorrect
* What went wrong in our implementation?

Let's make some hypotheses about what a "working" method would have:

* How *many* pieces do we expect? Did we get that many?
* How *long* should the baguette be at the end. Was it?

The state table tells us clearly:

* `3`
* No

What _was_ the length of the baguette? It was 20cm. Had a 60cm baguette been
cut evenly among 3 people, the baguette's length should have been 0 in the last
loop. It wasn't. `20cm` is the `even_length`, that's probably not a
coincidence...what if the `baguette_length` equals the `even_length`? Nothing.

Try stepping through the Procedure with `(60cm baguette,1)`. Do you see why you
get, _bafflingly_, nothing back?

Our bug is we should have used `>=`. Update your pseudocode and test it with a
table to verify that the fix works.

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

Uh-oh, yet again a bug has crept into our code!

## Resources
