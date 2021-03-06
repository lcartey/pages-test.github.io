# Incorrect constructor delegation
Prior to C++11, there is no mechanism for a constructor to delegate part of the object initialization to another, although other languages provide this feature. Consequently, any instance where a constructor call appears in the body of a constructor without being used is suspect.


## Recommendation
The rule flags constructor calls in constructors which are not used in some way. This is usually a misguided attempt to share some initialization code between multiple constructors, or to provide sensible defaults for some constructor parameters. The effect of a flagged expression would be to initialize an instance of the current class on the stack, and then let it go out of scope at the end of the constructor call.

There are several ways to address the underlying issue of sharing initialization code, and the most appropriate needs to picked in each case. Roughly speaking, the options are:

* Introduce actual default values for the constructor parameters.
* Duplicate the initialization code in each constructor.
* Factor out the initialization code into a member function that is called from each constructor.
* If your compiler supports it, use C++11's constructor delegation feature.

## Example
```cpp

class Circle {
private:
  double m_x;
  double m_y;
  double m_radius;
  
  double m_area;
  
public:
  // Real constructor:
  Circle(double x, double y, double radius) :
    m_x(x), m_y(y), m_radius(radius)
  {
    m_area = 3.14159 * m_radius * m_radius;
  }
  
  Circle() {
    // WRONG: Attempt to define the unit circle by default fails.
    Circle(0, 0, 1);
  }
};

```

## References
* Dr Dobb's Journal: [ Delegating constructors?](http://www.drdobbs.com/delegating-constructors/184401647)
* Wikipedia: [ Object construction improvement in C++11](http://en.wikipedia.org/wiki/C%2B%2B11#Object_construction_improvement).
