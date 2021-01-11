# Unclear comparison precedence
This rule finds comparison expressions that use 2 or more comparison operators and are not completely paranthesized. It is best to fully parenthesize complex comparison expressions to explicitly define the order of the comparison operators.


## Recommendation
Fully parenthesize complex comparison expressions to avoid confusion.


## Example

```cpp
void h() {
	int a, b, c;

	a < b != c; //parenthesize to explicitly define order of operators
	(a < b) < c; //correct: parenthesized to specify order
}

```

## References
* [Operator Precedence and Associativity](http://msdn.microsoft.com/en-us/library/126fe14k%28v=VS.80%29.aspx)
* [Operators](http://www.cplusplus.com/doc/tutorial/operators/)
* [EXP00-C. Use parentheses for precedence of operation](https://wiki.sei.cmu.edu/confluence/display/c/EXP00-C.+Use+parentheses+for+precedence+of+operation)
