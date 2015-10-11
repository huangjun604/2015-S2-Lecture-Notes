#COMP900048

##Week 1 - Introduction to Functional Programming

###Imperative languages

Imperative languages are based on *commands*, in the form of instructions and statements.

* Commands are executed
* Commands have an effect

###Functional languages

Functional languages are based on *expressions*.

* Expressions are evaluated
* Expressions have no effect

**let clause**

A let clause merely gives a name to an expression, and does not change the value of anything.

	let x = 3 + 4 in ...
	
###Equational Reasoning

The basis of functional programming is equational reasoning.

###Functions

A function definition consists of equations, each of which establishes an equality between the left and right hand sides of the equal sign.

	len [] =		0
	len (x:xs) =	1 + len xs
	
**pattern:** [] and (x:xs) are two patterns

The set of patterns should be ***exhaustive***: at least on pattern should apply for any possible call.

###Aside: syntax

**Function call**

	f fa1 fa2 fa3
	f fa1 (g ga1) fa3
	
**Comments:** 

	--this is the comments
	
###Recursion

**base case**

	len [] = 0
	
**recursive case**

	len (x:xs) = 1 + len xs
	
###Order of evaluation

**Church-Rosser theorem**

For the rewriting system knowns as the ***lambda calculus***, regardless of the order in which the original term's subterms are rewritten, the final result is always the same.

The theorem is not applicable to imperative languages.

###Side effects

A function or expression is said to have a side effect if, in addition to producing a value, it also modifies some state or has an observable interaction with calling functions or the outside world.

* modify a global or a static variable
* modify one of its arguments
* raise an exception
* write data to a display, file or network
* read data from a keyboard, mouse, file or network
* call other side-effecting functions

**Imperative vs declarative languages:** What really distinguishes pure declarative languages from imperative languages is that thy do not allow side effects.

*they do allow programs to generate exceptions

**Referential transparency:** An expression can be replaced with its value. This requires that the expression has no side effects and is pure.

**Single assignment:** In functional languages, variables are single assignment, and there are no assignment statements. You can define a variable's value, but you cannot redefine it.

##Week 1 - Workshop

QUESTION 5

```
xor :: Bool -> Bool -> Bool
xor a b | a == b = False
		| otherwise = True
		
xor a b = (a||b)&&not(a&&b)
```

QUESTION 6

```
append a [] = a
append [] a = a
append (x:xs) as = x : (append xs as)
```

QUESTION 7

```
myReverse [] = []
myReverse (x:xs) = (myReverse xs) ++ [x]
```

QUESTION 8

```
getNthElem [] n = error "bad"
getNthElem a 1 = head a
getNthElem (x:xs) = getNthElem xs (n-1)
```

## Week 2 - Section 2

### Type System

* strong: means that the system has no loopholes
* safe: means that a running program is guaranteed never to crash due to a type error.
* static: means that types are checked when the program is compiled, not when the program is run.

### List

List is not a type; it is a ***type constructor***.

### Function types

```
> :t isEmptyisEmpty :: [t] -> Bool
```

#### Function Type Declarations

The syntax for this is similar to the notation printed by ghci: the function name, a double colon, and the type.

```
module Emptiness whereisEmpty :: [t] -> Bool 
isEmpty [] = True 
isEmpty _ = False
```

### Number types

```
Prelude> :t 33 :: (Num t) => t Prelude> :t [1, 2][1, 2] :: (Num a) => [a]
```

The notation (Num t) means “the type t is a member of type class Num”. Num is the class of numeric types, including the four types above.

### if-then-else

#### Definition A

```
iota n = if n == 0 then [] else iota (n-1) ++ [n]
```

* The else arm is not optional
* The then and else arms are expressions, not statements

#### Definition B - Guards

```
iota n|n==0 = []|n >0 = iota(n-1)++[n]
```

#### Structured definitions

```
-- Definition C 
iota n =	if n == 0 
	then		[] 
	else		iota (n-1) ++ [n]
```

* the keywords then and else, if they start a line, must be at the same level of indentation as the corresponding if.
* if the then and else expressions are on their own lines, these must be more indented than those keywords.

## Week 2 - Section 3

###Type Definitions

```
data Gender = Female | Male
data Role = Staff | Student
```
Both types are also considered arity-0 type constructor.
Given zero arguments types, they each construct a type.

####Data Constructor

The four values are also called ***data constructors***.
Given zero arguments, they each construct a value.

####Using defined types vs using booleans

```
show1 :: Bool -> Bool -> String
show1 True False = 'female staff'
```
```
data Gender = Female | Male
data Role = Staff | Student
show2 :: Gender -> Role -> String
show2 Female Staff = 'female staff'
```

#### Cards

```
data Suit = Club | Diamond | Heart | Spade 
data Rank= R2 | R3 | R4 | R5 | R6 | R7 | R8 | R9 | R10 | Jack | Queen | King | Ace
```
```
data Card = Card Suit Rank
```
On the right hand side of the definition of the type Card, Card is the ***name of the data constructor***, while Suit and Rank are the types of its two arguments.

###Show Eq and Ord

#### Show

You can tell Haskell that the show function for values of the type Rank is showrank:```
instance Show Rank where show = showrank
```

This of course requires defining showrank. If you don’t want to do that, you can get Haskell to define the show function for a type by adding ***deriving Show*** to the type’s definition, like this:

```
data Rank = 
	R2 | R3 | R4 | R5 | R6 | R7 | R8 | R9 | R10 | Jack | Queen | King | Ace	deriving Show
```

#### Eq

To be able to use Haskell's == comparison operation for a type.

#### Ord

To compare values of a type for order (using <, <=, etc.) 

Left is less than Right

```
data Suit = Club | Diamond | Heart | Spade deriving (Show, Eq, Ord)
```

### Discriminated Union Types

Haskell has discriminated union types, which can include both disjunction and conjunction at once.

```
data JokerColor = Red | Black 
data JCard = NormalCard Suit Rank | JokerCard JokerColor
```

A value of type JCard is constructed

* either using the NormalCard constructor, in which case it contains a value of type Suit and a value of type Rank
* or using the JokerCard constructor, in which case it contains a value of type JokerColor

### Maybe type

```
data Maybe t = Nothing | Just t
```

For any type t, a value of type Maybe t is either Nothing, or Just x, where x is a value of type t.      
              
##Week 3 - Section 4

###Representing expressions

```
data Expr
    = Number Int
    | Variable String
    | Binop Binop Expr Expr
    | Unop Unop Expr
    
data Binop = Add | Plus .....
data Unop = 
```

###Comparing 

####errors

####memory

The C representation requires more memory: seven words for every expression, whereas the Java and Haskell representations needs a maximum of four (one for the kind, and three for arguments/members).
 
####maintenance

###Switching on alternatives

```
is_static :: Expr -> Bool
is_static expr = 
	case expr of
		Number _ -> True
		Variable _ -> False
		Unop _ expr1 -> is_static expr1
		Binop _ expr1 expr2 -> is_static expr1 & is_static expr2
```

###Binary search trees

```
data Tree = Leaf | Node String Int Tree Tree
```

####Counting nodes in a BST

```
countnodes :: Tree -> Int
countnodes Leaf = 0
countnodes (Node _ _ l r) =
	1 + (countnodes l) + (countnodes r)
```

####Searching a BST

```
search_bst :: Tree -> String -> Maybe Int
search_bst Leaf _ = Nothing
search_bst (Node k v l r) sk = 
	if sk == k then
		Just v
	else if sk < k  then
		search_bst l sk
	else
		search_bst r sk
```

##Week 4 - Section 5



## Week 4-2 - Section 7

###filter

```
filter :: (a -> Bool) -> [a] -> [a]
filter _ [] = []
filter f (x:xs) = 
    if f x then x:fxs else fxs
    where fxs = filter f xs
```

###Anonymous functions

defined by lambda expressions, based on the lambda calculus.

	filter (\x -> (mod x 2) == 0) [1, 2, 3, 4]
	
	is_even :: Int -> Bool
	is_even x = if (mod x 2) == 0 then True else False
	
###Map

Given a function and a list, map applies the function to every member of the list

```
map :: (a -> b) -> [a] -> [b]
map _ [] = []
map f (x:xs) = (f x) : (map f xs)
```
	
###Partial application

```
is_longer :: Int -> String -> Bool
is_longer limit x = length x > limit

filter (is_longer 4) ["ab", "abcd", "abcdef"]
```

* is_longer 4 "ab"
* is_longer 4 "abcd"
* is_longer 4 "abcdef"

###Operators and sections

If you enclose an infix operator in parentheses, you can partially apply it by enclosing its left or right operand with it; this is called a ***section***.

```
map (5 `mod`) [3, 4, 5, 6, 7]
[2,1,0,5,5]
```

###Types of partial application

	f :: at1 -> ((at2, ... atn) -> rt)
	
###Currying

The transformation from a function type in which all arguments are supplied together to a function type in which the arguments are supplied one by one is called currying.

In Haskell, all function types are curried.

	f :: at1 -> (at2 -> (at3 -> ... (atn -> rt)))
	
###Composing functions

All functions that makes a higher order function call or creates a closure is a ***second order function***.

The builtin operator '.' composes two functions.

	(f . g) x = f (g x)
	min = head . sort
	max = head . reverse . sort
	
##Week 5-1 - Section 8

###folds

The usual reduction operations are folds.

* left ((((I o X1) o X2)...) o Xn)
* right (X1 o (X2 o (...(Xn o I))))
* balanced ((X1 o X2) o (X3 o X4)) o ...

o devotes the folding operation

I devotes the identity element of that operation.

```
foldl :: (v -> e -> v) -> v -> [e] -> v
foldl _ base [] = base
foldl f base (x:xs) =
	let newbase = f base x in
	foldl f newbase xs
	
suml :: [Integer] -> Integer
suml = foldl (+) 0

concatl :: [[a]] -> [a]
concatl = foldl (++) []
```

```
foldr :: (e -> v -> v) -> v -> [e] -> v
foldr _ base [] = base
foldr f base (x:xs) = 
	let fxs = foldr f base xs in
	f x fxs
```

###Balanced fold

```
balanced_fold :: (e -> e -> e) -> e -> [e] -> e
balanced_fold _ b [] = b
balanced_fold _ _ (x:[]) = x
balanced_fold f b l

...
```

###QUIZ: Hypotenuse

Here is a definition of hypotenuse:
	
	square x = x ^ 2
	hypotenuse sides = sqrt (sum (map square sides))
	
Rewrite the hypotenuse function in point-free style.

```
hypotenuse :: [Integer] -> Integer
hypotenuse = sqrt . sum . (map square)
```

###List comprehensions

List comprehensions can be used for things other than filtering a single list.

A list comprehension consists of

* a template
* one or more generator
* zero or more tests
* zero or more let expressions defining local variables.

```
qs2 [] = []
qs2 (x:xs) = qs2(littles) ++ [x] ++ qs2(bigs)
	where
		littles = [l | l <- xs, l < x]
		bigs = [b | b <- xs, b >=x]
```

```
columns = "abcdefgh"
rows = "12345678"
chess_squares = [[c,r] | c <- columns, r <- rows]

pairs = [(a, b) | a<- [1,2,3], b <- [1,2,3]]
```

##Week 6-1 - Section 10

##Week 6-2 - Section 11

###Relations

**predicate:** The name of a relation is called a predicate.

	parent(queen_elizabeth, prince_charles).
	
####Facts

	parent(queen_elizabeth, prince_charles).

It may take many facts to define a relation.

####Variables

Each predicate argument may be a variable, which in Prolog begins with a capital letter or underscore and follows with letters, digits, and underscores.
	
###Rules

	Head :- Body,
	
where *Head* has the form of a fact and *Body* has the form of a query. The :- is read 'if', and the clause means that the *Head* is true if the Body is.

	grandparent(X,Z) :- parent(X, Y), parent(Y, Z).
	
####Recursion

Rules can be recursive.

```
% A person's ancestors are their parents and ancestors of their parents.
ancestor(Anc, Desc) :-
	parent(Anc, Desc).
ancestor(Anc, Desc) :-
	parent(Parent, Desc),
	ancestor(Anc, Parent).
```

**inner join** or **conjunction**: comma ,

	parent(queen_elizabeth, X), parent(X, Y).
	
**disjunction**: semicomma ;

	parent(queen_elizabeth, X) ; parent(princess_diana, X).
	
**negation**: \+

	parent(X, prince_william), \+ X = prince_charles.
	
**disequality**: \=

	parent(X, prince_william), X \= prince_charles.
	
`X \= Y` is same as `\+ X = Y`

###Negation as failure

In prolog, failing goals can never bind variable, so any variable bindings make in solving G are thrown away when \+G fails. Therefore, \+G cannot solve for any variables, and goals such as these cannot work properly.

The solution to this problem is simple: ensure all variables in a negated goal are bound before the goal is executed.

Prolog executes goals in a query from first to last.

###Datalog



### The closed World Assumption

Prolog assumes that all true things can be derived from the program.

##Week 7-1 

###Terms
In Prolog, all data structures are called ***terms***. A term can be atomic or compound, or it can be a variable.

####atom

An atom begins with a **lower case letter** and follows with letters, digits and underscores, for example, `a`, `queen_elizabeth`, or `banana`.

#####Compound Terms

each compound term is a ***functor (function symbol)*** followed by zero or more arguments.

	node(leaf, 1, node(leaf, 2, leaf))
	
####Variables

It denotes a single unknown term. A variable name begins with **an upper case letter or underscore**, followed by any number of letters, digits, and underscores.

A single underscore `_` is special: it specifies a different variable each time it appears.

###List syntax

empty list: []

a list with the three elements 1, 2 and 3: [1,2,3]

a list whose head is `x` and whose tails is `xs`: [X | Xs]

`x1: x2: xs` : [X1, X2 | Xs]

**Ground term**: it contains no variables. `3`, `f(a, b)`

**Nonground term**: it contains at least one variable. `f(a, X)`

###Substitutions

A substitution is a mapping from variables to terms.

Any ground Prolog term has only one instance, while a nonground Prolog terms has an infinite number of instances.

###Unification

###Proper lists

```
proper_list([]).
proper_list([Head|Tail]):-
   proper_list(Tail).
```

###Detour: singleton variables

we should begin the variable name Head with an underscore, or just name the variable _.

###Append

```
append([], C, C).
append([A|B], C, [A|BC] :-
	append(B, C, BC).
```

###Take

```
take(N, List, Front) :-
	length(Front, N),
	append(Front, _, List).
```

###Member

```
member1(Elt, List) :- append(_, [Elt|_], List).
```

```
member2(Elt, [Elt|_]).
member2(Elt, [_|Rest]) :- member2(Elt, Rest).
```

the second is a bit more efficient because the first builds and ignores the list of elements before Elt in List, and the second does not.

QUIZ: uNIFICATION
{x -> a, Y-> b}
The two terns are not unifiable, since a substitution cannot map X to both a and b

##Week 7-2 - Section 13

###Arithmetic

```
?- X = 6 * 7.
X = 6 * 7.

?- X is 6 * 7.
X = 42.
```


##Week 8-1 - Section 13

###Quiz

##Week 9-2 - Section 15

##Week 10-1

##Section 16

###Input/Output

####character type

Prolog also has predicates to read (get0/1) and write (put/1) single character codes, and to emit a newline (nl/0).

```
?- X = "Hi!".

?- get0(X), get0(Y).
```

####QUIZ:Printing strings

Write a predicate print_string(Codes) that prints out a Prolog string (list of character).

```
print_string([]).
print_string
```

###Comparing terms

Variables < Numbers < Atoms < CompoundTerms: @<, @=<, @> and @>=

###Sorting

```
?- sort([h,e,l,l,o], L). 
L = [e, h, l, o].?- msort([h,e,l,l,o], L). 
L = [e, h, l, l, o].?- keysort([7-a, 3-b, 3-c, 8-d, 3-a], L). 
L = [3-b, 3-c, 3-a, 7-a, 8-d]
```

###Determining term types

integer/1

```
?- integer(3).true.?- integer(a).false.?- integer(X).false.
?- float(3.0).
true.
?- compound(var(X)).
```

###Handling Terms in General

functor/3 gives the functor of any non-variable.

```
?- functor(p(1,q(3)), F, A). F = p,A = 2.
```

## Week 10-2 - Section 17

#### Eager evaluation

each expression is evaluated as soon as it gets bound to a variable

#### Lazy evaluation

### Lazyness and infinite data structures

	head [1..]
	take 10 [1..]
	
### Evaluating laze values only once

####QUIZ: Using lazyness

Write a function

recycle :: [t] -> [t]
to generate an infinite list of repetitions of the elements of its input.

```
recycle :: [t] -> [t]
recycle l = recycle' l l

recycle' [] l = recycle' l '
recycle (x:xs) l = x: recycle' xs l
```
or
```
recycle l = l ++ recycle l

```

####QUIZ: Using

	min = head . sort
	
What is the complexity of min if sort is implemented using quicksort?

Quadratic(worse case). Linear in the best and average cases : 2n.

What is the complexity of max if sort is implemented using quicksort?

