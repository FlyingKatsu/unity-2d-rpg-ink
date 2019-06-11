# Basics
This page will document the different concepts necessary for creating branching narratives with [Ink](https://www.inklestudios.com/ink/). Consider this page as a quick reference for terminology used throughout these docs.

## Choices
TBD

### Sticky Choices

### Single-Use Choices

### Default Choices

## Structures
Aside from choices, there are several other structures that help organize your story into blocks that can be accessed from any other block.

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

```

For your own sanity, it helps to indent your nested weaves and choices, but this is not a requirement.

### Stitches
TBD

### Knots
TBD

### Functions
TBD

## Scopes and Labels
A scope is a block of text that serves as a frame of reference for a particular label. Outside of this block, a label has no meaning on its own, so it must be referenced through its parent (the containing block).

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
# Get the value stored in the variable named label
{label}
# Compare the value to another value (if these things are equal, continue)
{label == magicNumber}
```

## Navigation
TBD

### Diverts
TBD

### Tunnels
TBD

### Threads
TBD
