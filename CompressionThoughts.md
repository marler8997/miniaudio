# Compression Thoughts

This document contains some thoughts I have about compression.

I've come up with a model on how to think about compression.

When coming up with a compression format, it's a mistake to start by designing
a set of bit patterns that are used to encode/decode data.  This should be the
last step in creating a compression format.

What should come first is the logic that is used to generate the final
decoded data.  Every compression format can be thought of as a set of commands
that will generate the final decoded data.  Even a raw format can be thought of
this way.  Every bit in the raw format is simply a command that means "copy
this value to the decoded output".

I belive that thinking of compression in this way helps in designing an optimal
compression format because you can seperate the logic and techniques to decode/generate
domain specific data from the bit patterns to represent that logic. This is beneficial
because these 2 stages of compression can be optimized using differet techniques, and by
seperating them you prevent intermixing logic that doesn't need to be intermixed
thus making each part less complex.

I'm including a practical example for demonstration of this.

Say you have a set of numbers you wish to compress.
The first step should be to come up with a technique to generate those numbers
in the least number of commands.  This technique may also use "lossy" strategies
that result in some acceptable loss of data, but reduce the number of commands
it takes to generate the data.

There may also be a set of different techniques to generate the data, or even
different techniques to generate parts of the data.

Each technique is defined as a set of commands that will generate the final decoded output.

Each technique must be known to both the encoding program and the decoding program.
The technique being used must also be included in the compressed data so a strategy
for compressing this data must also be addressed.

For each technique, the set of commands it uses can also use a compression strategy.
Maybe that means including some sort of command format within the compressed data
as well.
