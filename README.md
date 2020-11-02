# Ludii stuff

This is just a repo with some of my [Ludii](https://ludii.games/) experiments and learnings.

See [resources.md](resources.md) for links to other documents and tutorials.


## To see all the Ludii files

Extract the files from a Ludii `.jar` file with the command: `jar xf Ludii-filename.jar` (Note you probably want to do this in an empty folder.)

Then you'll find the `.lud` files in a folder named `lud`.


## There is a built-in Ludii editor!

In the Ludii app, go to "File->Editor..." to open the editor. The two options are "packed" and "expanded". You probably want packed, but expanded removes all the functions (essentially just unrolling them into the definition).

Make changes and click compile to see them in action. (Re-loading the game will lose your changes, so be careful to copy anything you want to save to an external file.)

Right-click on a ludeme to see its possible values and/or alternatives.


## Basics

The 5 parameters for the GAME ludeme are: name, players, mode, equipment, and rules.

If any of them are missing, it's assumed that the "defaults" are from Tic-tac-toe.


## Different game boards

These examples are all inside `(game (equipment { ` HERE ` } ) )` unless otherwise specified.


### standard 8x8 square grid

```
        (board 8) 
```

### standard 8x8 square grid with checker pattern

```
        (board 8) 
```

... But also, outside of the `(game ...` ludeme:

```
(metadata (graphics {
        (board Style Chess)
} ) )
```

### hex5 board

```
        (board (hex 5))
```

### hex4 board rotated 90 degrees

```
        (board (rotate 90 (hex 4))) 
```


## Playing on the intersections

Playing in the center of the board spaces is the default. Add `use:Vertex` to your board definition to specify playing on the intersections (or verticies).

### Go board example

```
        (board (square 19) use:Vertex)
```


## Starting with pieces on the board vs off the board

You’ll need to define your pieces in the “game -> equipment” ludeme. If none of the pieces start on the board, that’s all you need to do. (see example game: Hex)

If you want pieces to start on the board, you then need to reference them in a “game -> rules -> start -> place” ludeme. There are a number of ways to do this. (see example game: Chess)



## Piece Movement

Piece placement is the default. To move pieces already on the board is more work.


### Jumping pieces

See checkers (english draughts).


### Capturing a piece

From "Game of the Pawns":

```
            (piece "Pawn"
                Each
                (or
                    {
                        (move Step Forward (to if:(is Empty (to))))
                        (move
                            Step
                            (directions { FR FL })
                            (to
                                if:(is Enemy (who at:(to)))
                                (apply (remove (to)))
                            )
                        )
                    }
                )
            )
```


## Aliases

If your game has multiple names, you can specify other names in the “metadata -> info -> aliases” ludeme. (And it will be searchable by those names!) 

```
(metadata
    (info {
        (aliases {“Other Name”})
     } )
)
```


