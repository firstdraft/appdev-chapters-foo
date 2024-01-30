# Float

Ruby calls decimal numbers `Float`s. To create a `Float` rather than an `Integer`, just make sure to include a decimal point:

```ruby
5.class # => Integer
5.0.class # => Float
```

## Methods

### + - * / ** (math)

The math methods work mostly like you'd expect, and similarly to [the ones for integers](https://chapters-foo.ourplatform.com/chapters/760#-------math){:target="_blank"}.

The main difference to keep in mind is with `/`. Division with floats works the way that we're used to — it returns fractional results, as a `Float`:

```ruby
12.0 / 5.0 # => 2.4
```

Try the following and see what you get:

```ruby
12 / 5
12.0 / 5
12 / 5.0
```

[Click here for a REPL to try it.](https://repl.it/@raghubetina/Float-math){:target="_blank"}

What did you discover? If _either_ side is a float, float division will be performed.

This is why `Integer`'s `.to_f` method can come in handy while doing math; at some point if you need to do division and need a fractional answer, then convert it to a `Float` first.

One other thing to keep in mind: you can use `**` in conjunction with fractions to calculate roots, since 9<sup>1/2</sup> is the same as the square root of 9, 8<sup>1/3</sup> is the same as the cube root of 8, etc.

```ruby
9 ** 0.5 # => 3.0
8 ** (1/3.0) # => 2.0
```

### round

`Float`s can round themselves. Play around with the `.round` method:

```ruby
pi = 3.1415926535897932384626433832795028841976939937510
p pi.round(3)
```

[Click here for a REPL to try it.](https://repl.it/@raghubetina/round){:target="_blank"}

### rand

The `rand` method that we met earlier can also be called with no arguments, in which case it returns a `Float` between 0 and 1. This is very handy for e.g. probabilities. Give it a try:

```ruby
p rand
```

[Click here for a REPL to try it.](https://repl.it/@raghubetina/float-rand){:target="_blank"}

## Even more Float methods

Looking for even more Float methods? See [here](https://chapters-foo.ourplatform.com/chapters/853){:target="_blank"} for some additional methods added by the `activesupport` gem (automatically available within Ruby on Rails).
