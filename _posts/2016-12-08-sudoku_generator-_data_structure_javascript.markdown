---
layout: post
title:  "Sudoku Generator- data structure (javascript)"
date:   2016-12-08 23:02:30 +0000
---

## The Challange
I had already coded a *tic-tac-toe* a *snake* and a (rather stupid) *connect-4*. I needed something to write and Sudoku seemed like a reasonable challange.

### What it should be able to do
* Generate a puzzle
* Be user friendly
* Be able to check if the puzzle is solved

**I won't be pasting all the code, in order to keep it relevant**

I'm assuming you're familiar with Sudoku..
## Creating the board
The board is a 9x9 grid, so every board has 81 spots.
Each one of those 81 spots is part of three groups: the **vertical** line, the **horizontal** line, and the 3x3 **box** that it is part of.

So I wanted an efficiant way to jump from the vertical aspect of a spot to the horizontal without reinventing mathematics every single time..

The following function returns a Sudoku board object.

```
  function Sudoku() {
    var board = [],

    (function() {
      function Pos(gridPos) {
        this.x;
        this.y;
        this.box;
        this.gridPos = gridPos;
        this.val = ' ';
      }
      for (var i = 0; i < 81; i++) {
        board[i] = new Pos(i);
      };
    }());

    this.xLines = initX(board);
    this.yLines = initY(board);
    this.boxes = initBoxes(board);
    this.board = board;

  } // end Sudoku
```

I start with a "constructor" function called Sudoku.
The resulting object includes the following properties: 
1.  board
2.  xLines
3.  yLines
4.  boxes

The *board* property containes the entire thing in one array and the others are an array of arrays, splitting the board into groups.

**board** an array that includes 81 elements.
Each element is a reference to an Object created by the Pos "constructor" function.

```
  function Pos(gridPos) {
        this.x;
        this.y;
        this.box;
        this.gridPos = gridPos;
        this.val = ' ';
      }
```

Each Element knows what vertical line, horizontal line, and box it is part of.

**xLines and yLines and boxes** are arrays that contain arrays of 9 elements each.
The beauty is that each one of those elements is a reference to one of the 81 elements that are contained within the **board** property! so any change I do to one would affect all the others (which makes sense since they are all part of the same board).

That means that if I access a spot through *xLines* and change it's value, this will change it in *yLines*, *boxes* and *board*!
This makes it easy to look at the board in different ways, which can help me while I'm generating a new puzzle.

## Checking the board
The following code contains 2 functions.
*checkLineForDbl* will check a line for any doubles :)
*checkBoard* will send the all the different groups into *checkLineForDbl* to be checked for doubles, making it very simple to check the entire board.


```
  function checkLineForDbl(line) {
    return line.some(function(e, i) {
      if (e.val == ' ') {return false }
			
      return line.some(function(v, j) {
        return (e.val == v.val && i !== j)
      });
    });
  }

  function checkBoard(board) {
    return board.xLines.some(function(xLine) {
      return checkLineForDbl(xLine);
    }) || board.yLines.some(function(yLine) {
      return checkLineForDbl(yLine);
    }) || board.boxes.some(function(box) {
      return checkLineForDbl(box);
    });
  }
```

The Sudoku object makes this easy.


I'm a little self-conscious about posting the actual finished product because I wrote it a while ago and the code is not really up to standard.. but here it is anyways.. Don't judge me! (to edit you can drag, click, or use the keyboard)

http://codepen.io/dovid1234/full/PZbmMx/

hopefully one day I'll have time to rewrite it with beautiful, organized, and readable code but until then.. Enjoy!
