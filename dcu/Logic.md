
## Prolog

Prolog is a programming language that is suited to symbolic, non-numeric computations. A Prolog program consists of:

- clauses
- facts
- rules
- procedures

## Getting Started

Begin with using the command

````c
edit(file('file_name.pl')).
````

Copy and paste source code if provided into file.

> Remember to call the consult command after every change to the .pl file

````c
consult('file_name.pl').
````

## Variables

> Variables always in prolog always start with a capital letter or an underscore.

-  " ; " is *OR*
-  " , " is *AND*
-  " :- " is "IF THEN"

Examples:

````c
uncle(X, Y) :- brother(X, Z), mother(Z, Y).
uncle(X, Y) :- brother(X, Z), father(Z, Y).

/* x is the uncle of y if x is a brother of z given that z is a parent of y*/
````

````c
father(X, Y) :- parents(Y, X, _).

/* this means that x is the father of y if y is the child of x*/
````

> Note: the underscore var is used as a place holder for variables we "DONT CARE" for.

## Dealing with Lists

General List Structure in Prolog:
````C
   +---+---+     +---+---+     +---+---+     +---+---+     +---+---+
   | 1 |  ------| 2 |  ------| 3 |  ------| 4 |  ------| 5 | []|    |
   +---+---+     +---+---+     +---+---+     +---+---+     +---+---+  
   
	Head|Tail     Head|Tail     Head|Tail     Head|Tail     Head|Tail
````

> Code below will recursively move through the list and check if the head is a holiday book or not 

````C
is_holiday(book(_, _, G, S)) :- S < 400, G \== study, G \== refernce.
/* returns true if...
    Size is < 400 pages.
    Genre is not Study or Refernce
*/

holiday(B, [B | _]) :- is_holiday(B).
/* checks if book at head of list is a holiday book */
holiday(B, [_ | T]) :- holiday(B, T).
/* takes the book and the tail of the list re calling the holiday predicate above checking if the next book is a holiday book or not and so on till the end of the list.
*/
````

> Use this code to build Library of all books

````C
build_library(Lib) :- findall(book(Title, Author, Genre, Size), book(Title, Author, Genre, Size), Lib).
````

Finally run command in terminal...

````C
build_library(L), holiday(B, L).
````

## Grid prolog

![[Pasted image 20230307195739.png]]

Sample Code:

````C
north(A, B) :- directly_north(A, B).
/* A is north of B if it is directly north (obv) */

north(A, B) :- directly_north(A, C), north(C, B).
/* A is north of B if A is directly north of a point C that calls recursively */

northeast(A, B) :- north(A, C), east(C, B).
````


