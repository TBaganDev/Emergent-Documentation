# Coding your first Automaton
Welcome to the Emergent language! Within this tutorial, we will cover the step by step process for creating a Game of Life Cellular Automata within Emergent. If you haven't already, make sure to [install the Emergent compiler](install.md) and have an understanding on how to [compile using the Emergent compiler](compile.md).

## Identifying the rules with the Game of Life Automaton
With some quick research, you will find out some properties the Conway's Game of Life CA:
- 2D Cellular Automata
- The neighbours are any adjacent cells including diagonals (the moore neighbourhood)
- Cells can be in 2 states, *live* or *dead* following these rules:
  - *live* -> *dead* if less than 2, or more than 3 of its neighbours are *live*
  - *dead* -> *live* if exactly 3 neighbours are *live*
  - *live* -> *live* if 2 or 3 of its neighbours are *live*
  - *dead* -> *dead* for all other cases

## Translating into Emergent
This definition can be simply translated into Emergent. First let's begin with the neighbourhood.

### Neighbourhood
The Moore Neighbourhoood used works within 2 dimensions, considering only adjacent cells on the orthogonal and diagonals. The standard layout of a Neighbourhood within Emergent is shown below:
```
neighbourhood <name> : <dimension> { 
  <neighbours>
}
```
We are already aware of the dimension and a suitable name, but how do we represent the neighbours? Within Emergent, any neighbour is defined by `[x, y]` for 2D CA and `[x]` for 1D CA. Therefore, we list the neighbours using comma seperation, to create the following neighbourhood shown below:
```
neighbourhood moore : 2 {
   [-1, 1], [0, 1], [1, 1],
   [-1, 0],         [1, 0],
   [-1,-1], [0,-1], [1,-1],
}
```

### Model
With the neighbourhood determined, next we will construct the model, which is the structure that contains all the rules and state names. The model specifies the associated neighbourhood, and enumerates all the state definitions as so:
```
model <name> : <neighbourhood> {
  default state <name_a> '<any character>'
  
  state <name_b> '<any character>' {
    <rules to make name_b>
  }
  ...
}
```
The "default" tag used is a required state, which as the name implies, is the default state if none of the other state definitions fit. The rules within a state definition are the rules which produce that state. So, with our example, the *live* cells are only produced if 2 or 3 of its neighbours are *live*, meaning our model would be in the following format:
```
model conway : moore {
  default state dead '-'
  
  state live '@' {
    |set cell in all: cell == live| <= 3 and 
    |set cell in all: cell == live| >= 2
  }
}
```
Note that the inside expression is an aggregating notation for counting all neighbours which fulfill the predicate:
> `|set <variable> in <subset>: <predicate>|`

Our implementation of this cardinality operation uses the "all" keyword, which specifies that all neighbours are considered here.

### Final Implementation
Our final implementation looks like so:
```
neighbourhood moore : 2 {
   [-1, 1], [0, 1], [1, 1],
   [-1, 0],         [1, 0],
   [-1,-1], [0,-1], [1,-1],
}

model conway : moore {
  default state dead '-'
  
  state live '@' {
    |set cell in all: cell == live| <= 3 and 
    |set cell in all: cell == live| >= 2
  }
}
```
The initial input for this CA would have to be a 2D Grid of ASCII characters of which the model accepts, i.e:
```
----
--@-
-@@@
--@-
```

## Other Tutorials
- [Installing Emergent](install.md)
- [Compiling Emergent](compile.md)
