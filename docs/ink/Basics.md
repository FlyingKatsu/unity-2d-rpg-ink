# Basics
This page will document the different concepts necessary for creating branching narratives with [Ink](https://www.inklestudios.com/ink/). Consider this page a quick reference for terminology used throughout these docs.

## Choices
Choices are the usual way to branch your story into different directions. A set of choices located at the same branching point can be called a decision block.

Choices are made up of three parts: A bullet style (sticky `+`, single-use `*`), choice option text (in or before `[`brackets`]`), and resulting text (after `]`). 

Simple example: `+  Choice Text`
```
// Before AND after choosing, the player will see
Choice Text
```

Standard example: `+  [Choice Option Text] Resulting Text`
```
// Before choosing
Choice Option Text

// After choosing
Resulting Text
```

Complex example: `+  Choice [Option Text] Resulting Text`
```
// Before choosing
Choice Option Text

// After choosing
Choice Resulting Text
```

### Sticky Choices
Sticky choices are always available, no matter how many times the player has accessed the same decision block and made the same choice. To vary the text each time the decision block is accessed, see [Alternative Text](#alternative-text).

Sticky choices are marked by plus sign:  
`+  [Choice Option Text] Resulting Text`

### Single-Use Choices
Single-use choices can only be selected once during the entire game. The next time the player access the same decision block, the previously chosen options will no longer be available.

Single-use choices are marked by an asterisk:  
`*  [Choice Option Text] Resulting Text`

### Fallback Choices
You can set a default choice for a decision block in case the player runs out of single-use choices and has no other options available.

Default choices just normal choices without any choice text. Use a [Divert](#diverts) arrow to distinguish the resulting text from a normal choice text, or to jump to a different branch.
`+  -> You have no other options`

## Structures
Aside from choice and text blocks, there are several other structures that help organize your story into blocks that can be accessed from any other block.

### Weaves
Weaves gather a set of branches into a conclusive line. These can be used to ensure that the player will always move forward,  
no matter where their choices lead. This is good for chaining together consecutive decisions.

Use a single dash to mark a weave:  
`- Every path leads here`

It is possible to make simple interactive fiction using just weaves and choices.

#### Nested Weaves
More complex stories may have nested weaves. Note that a weave will only gather branches at the same nesting level.

Add an extra symbol to nest weaves and choices one level deeper:  
```
A decision block
* Choice A
  ** A1
  ** A2
  -- The end of A
  
* Choice B
  ** B1
  ** B2
  -- The end of B
  
- The end of the block, regardless of your choices
```

For your own sanity, it helps to indent your nested weaves and choices, but this is not a requirement.

### Stitches
Use a single equal sign to label the start of a stitch.  
`= stitch`

Stitches can also act like functions by accepting parameters to pass on to their weaves/choices.  
`= stitch(parameter)`

If you use a stitch, you must also tell the game which stitch to start the game with (see [Diverts](#diverts))

### Knots
Use double equal signs to label the start of a knot.  
`== knot ==`

Knots can also act like functions by accepting parameters to pass on to their stitches, and weaves/choices.  
`== knot(parameter) ==`

If you use a knot, you must also tell the game which knot/stitch to start the game with (see [Diverts](#diverts))

### Functions
Functions can be used to separate complex logic from your writing. You can make calculations and either change an existing variable,  
return a new value, return the result of another function, or jump to a labeled block of content (knot, stitch, weave, or choice).

Use triple equal signs to label the start of a function.  
`=== function ===`

Functions can accept parameters.  
`== function(parameter) ==`

For more on using functions, see [Ink Docs/Functions](https://github.com/inkle/ink/blob/master/Documentation/WritingWithInk.md#5-functions) and [Ink Docs/Built-in Functions](https://github.com/inkle/ink/blob/master/Documentation/WritingWithInk.md#7-game-queries-and-functions)

## Navigation
Instead of just presenting the player with a chain of choices that eventually reach the same end, you can divert them to completely distinct paths.

### Diverts
To divert (jump) to a different block of content, use a forward arrow
`->label`

This is helpful for when your script contains reusable branches or sets of branches that you don't want to copypaste several times. Jump within the same block scope to form a simple loop:  
```
- (loop) You entered a continuous loop...
+ [continue] ->loop
+ [escape]
- You got out!
```

Some pre-defined diverts, `->DONE` and `->END`, are used to mark the end of a sequence or game, and are required if you use knots and stitches.

Note that if you have many knots and stitches, you will need to be more specific about which label a divert shold use (see [Scopes](#scopes))

### Tunnels
Tunnels allow you to divert to another location temporarily, and then return to the current location once the other location's business is finished.

You can create a tunnel by simply adding an extra arrow to the end of a divert:
`-> label ->`

You can chain tunnels as well, and end on a normal divert:  
`-> first_stop -> second_stop -> third_stop -> DONE`

In order to use a tunnel, the branches referenced by the labels must eventually end with `->->` so that the game knows when to return to the original location:  
```
TODO: put an example here
```

See [Ink Docs/Tunnels](https://github.com/inkle/ink/blob/master/Documentation/WritingWithInk.md#1-tunnels)

### Threads
Threads are the most complex part of an Ink story, and are probably rarely needed by most writers. However, it may prove incredibly useful for a standard RPG-style game.

Create a thread with a reversed arrow `<-`:  
`<-label`

Threads combine several blocks of text, along with any choices, and presents them as one huge decision block.

```
TODO: put an example here
```

See [Ink Docs/Threads](https://github.com/inkle/ink/blob/master/Documentation/WritingWithInk.md#2-threads)

## Scopes and Labels
A scope is a block of text that serves as a frame of reference for a particular label. Outside of this block, a label has no meaning on its own, so it must be referenced through its parent (the containing block).

### Labels

Every structure in Ink can be given a label:  
```
=== functionLabel(parameter)
== knotLabel
= stitchLabel
- (weaveLabel) weave text
+ (choiceLabel) [choice text] result text
* (choiceLabel) [choice text] result text
```

Additionally, labels store a numerical value representing how many times the Player has accessed a structure. The following loop will tell you how many times you've accessed `loop`, using a plural if the count is greater than 1.  
```
- (loop) You are in a continuous loop...
+ [continue] ->loop
+ [escape]
- You got out after {loop} {loop > 1: loops | loop}!
```

Thus, labels are actually variables. Variables hold values that can be accessed and compared via curly brackets:  
```
// Get the value stored in the variable named label
You accessed the label {label} times!

// Compare the value to another value (if these things are equal, continue)
{label == magicNumber} You won the lottery!

// Display a choice only if the player accessed label at least once (shorthand for {label > 0})
* {label} [I've seen the label already] 

// Display a choice only if the player never accessed label before (shorthand for {label == 0})
* {not label} [Can you show me the label?]
```

For more info on the types of operations you can do to variables, see [Ink Docs/Variables and Logic](https://github.com/inkle/ink/blob/master/Documentation/WritingWithInk.md#part-3-variables-and-logic)

### Scopes

A label inside its scope is accessible as is, but outside its scope must be refered to by its parent (containing block).

KnotLabel.StitchLabel.Choice/WeaveLabel

- Knots must have unique names throughout the story
  - If a knot has stitches, diverting to it will pull the first stitch by default
- Stitches must have unique names within the scope of their knot, and cannot share a name with their knot
- Choices and weaves, if labeled, should have unique names within the scope of their containing stitch/knot
  - Nesting does not change this, so nested choices and weaves must be unique regardless of nesting level
  - If a labeled choice/weave appears inside of a stitch, it is okay to reuse the same label in another stitch, and each one will have its own count
  - If the labeled choice/weave appears inside of a knot, but not inside of a stitch, its scope becomes the entire knot, and its label cannot be reused by any other structure in the knot (including the knot itself, any stitches, and any other weaves/knots in those stitches)

### Additional Concepts

#### Alternative Text
You can have text change each time the player accesses the same structure. See [Ink Docs/Variable Text](https://github.com/inkle/ink/blob/master/Documentation/WritingWithInk.md#6-variable-text)

#### Lists
Lists are a flexible way to keep track of state changes. See [Ink Docs/Lists](https://github.com/inkle/ink/blob/master/Documentation/WritingWithInk.md#part-5-advanced-state-tracking)
