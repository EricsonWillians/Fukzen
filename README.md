# The Lilith Programming Language
### An open-source programming language written in Python.

![Lilith](https://s4.postimg.org/kv8u9hnd9/logo.png)

```
[o] <- *Hello World!* ->
```

#### Present state of development:
* Arithmetic expression evaluation.
* Logical expression evaluation.
* Output of expressions.
* Assignment of expressions to variables.

Example of assignment:

```
x = 11 ->
y = 22 ->
[o] <- x + y ->
```

#### In progress:
* Condition blocks

Example of a condition block (The syntax is ok, but the parsing is not working):

```
x = 4 ->
y = 8 ->
? y < 5 <?
	x = 7 -> 
?> ?? y > 5 <?
  x = 9 ->
?> ??? <?
  x = 11 ->
?> ->
[o] <- x ->
```

#### Next:
* Loops

#### Goal:
The goal of the Lilith Programming Language is to develop an entirely new programming language from Python, in order to experiment with features that can be added to a programming language, to expand our knowledge, and to create an alternative that is as powerful as Python, borrowing its native libraries. For now, Lilith is an interpreted programming language, but eventually it will be compiled to Python, so that it can run with the same speed. 

#### Disclaimer:
The syntax **shall** be completely different from Python, and even C. Lilith is rebellious to her God and his "Zen of Python", so if you're a conservative, it's best for you to stay in heaven.

#### Grammar:
```
plus : '+'
minus: '-'
mult: '*'
div: '/'
mod: '%'
pow: '^'
open_parenthesis: '('
close_parenthesis: ')'
end: '->'
identifier: [a...Z] | [a...Z] identifier
number: [0...9] # Any number.
program : statement
		| program statement
statement : condition_statement end
		  | expression end
		  | assignment end
		  | io_operation end
compound_statement : statement
				   | statement compound_statement
expression : expression plus term 
		   | expression minus term 
		   | expression greater_than_relational_operator term 
		   | expression greater_than_or_equal_to_relational_operator term 
		   | expression less_than_relational_operator term 
		   | expression less_than_or_equal_to_relational_operator term
		   | term
		   | string
term : term mult factor 
	 | term div factor 
	 | term mod factor
	 | term pow factor
	 | term equal_to_relational_operator factor 
	 | term not_equal_to_relational_operator factor 
	 | term alt_not_equal_to_relational_operator factor 
	 | factor
factor : open_parenthesis expression close_parenthesis 
	   | identifier 
	   | number
name : identifier
simple_assignment_operator: '='
addition_assignment_operator: '+='
subtraction_assignment_operator: '-='
multiplication_assignment_operator: '*='
division_assignment_operator: '/='
modulo_assignment_operator: '%='
assignment_operator : simple_assignment_operator
				    | addition_assignment_operator
				    | subtraction_assignment_operator
				    | multiplication_assignment_operator
				    | division_assignment_operator
				    | modulo_assignment_operator
assignment : identifier assignment_operator expression
input_operator : '[i]'
output_operator : '[o]'
send_operator : '<-'
io_operation : input_operation
			 | output_operation
input_operation : identifier send_operator input_operator
				| identifier send_operator input_operator send_operator expression
output_operation : output_operator send_operator expression
greater_than_relational_operator : '>'
greater_than_or_equal_to_relational_operator : '>='
less_than_relational_operator : '<'
less_than_or_equal_to_relational_operator : '<='
equal_to_relational_operator : '=='
not_equal_to_relational_operator : '<>'
alt_not_equal_to_relational_operator : '!='
relational_operator : equal_to_relational_operator
					| not_equal_to_relational_operator
					| greater_than_relational_operator
					| less_than_relational_operator
					| greater_than_or_equal_to
					| less_than_or_equal_to
condition_specification_operator : '?'
alternative_condition_specification_operator : '??'
else_operator : '???'
post_condition_evaluation_block_opening_operator : '<?'
post_condition_evaluation_block_closing_operator : '?>'
post_condition_evaluation_block : post_condition_evaluation_block_opening_operator compound_statement post_condition_evaluation_block_closing_operator
condition_statement : condition_specification_operator expression post_condition_evaluation_block
					| condition_specification_operator expression post_condition_evaluation_block condition_extension
condition_extension : alternative_condition_specification_operator expression post_condition_evaluation_block
					| alternative_condition_specification_operator expression post_condition_evaluation_block condition_extension
					| else
else : else_operator post_condition_evaluation_block
```

#### How?
[PLY (Python Lex-Yacc)](http://www.dabeaz.com/ply/)

#### Want to contribute?
Send me a pull request. Let us discuss any flaw in the grammar and in the code, your help would be really relevant.
