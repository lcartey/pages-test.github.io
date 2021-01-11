# Lossy pointer cast
This rule finds expressions of pointer type which are (implicitly or explicitly) converted to an integer type of smaller size. This results in truncation of the most significant bits of the larger integer type.

Such conversions are highly non-portable, since the relative size of integer and pointer types may differ between architectures. For example, while on a 32-bit architecture both type `int` and type `char*` are four bytes wide, the latter occupies eight bytes on a 64-bit machine.


## Recommendation
Avoid converting between pointer types and integer types.


## Example

```cpp
void f(char *p) {
	int my_ptr = p; //Wrong: pointer assigned to int, would be incorrect if sizeof(char*) 
	                //is larger than sizeof(int)
	//...
}

```

## References
* MSDN Library: [Type Conversions and Type Safety (Modern C++)](http://msdn.microsoft.com/en-us/library/hh279667.aspx).
* Cplusplus.com: [Type conversions](http://www.cplusplus.com/doc/tutorial/typecasting/).
