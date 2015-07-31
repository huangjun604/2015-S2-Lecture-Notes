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

