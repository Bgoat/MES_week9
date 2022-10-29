# MES_week9
Optimization
Sine Function
Here are 3 implementations of the Sine function and the math.h function as a comparison. The GNU implementation is more accurate than these, as it uses a piecemeal algorithm depending on the input. 

The Taylor series is good for accurate measurement when you have a lot of computing power and can go out to many digits. There are ways to simplify this and get rid of the float and multiplication aspects using CORDIC math.

The Slope Iteration and Smoothstep both use float, with the Slope Iteration being more accurate but iterating (more cycles). 

## Ouput:
```
Math sin(0.5) = 0.479426
taylorSin(0.5) = 0.500000
Slope Iteration Method(0.5,1020) = 0.484659
zsh: segmentation fault  ./a.out
```

## Mentioned in MES
Taylor Series ( to an approximation of 3 or 4 terms)
- Use shift in the division to avoid float
- Scale input 
- Lookup Table

## Others
### Slope Iteration Method
```
float SineApproximation (float theta, float resolution)
{
    // calculate the stepDelta for our angle.
    // resolution is the number of samples we calculate from 0 to 2pi radians
    const float TwoPi = 6.28318530718f;
    const float stepDelta = (TwoPi / resolution);
 
    // initialize our starting values
    float angle = 0.0;
    float vcos = 1.0;
    float vsin = 0.0;
 
    // while we are less than our desired angle
    while(angle < theta) {
 
        // calculate our step size on the y axis for our step size on the x axis.
        float vcosscaled = vcos * stepDelta;
        float vsinscaled = vsin * stepDelta;
 
        // take a step on the x axis
        angle += stepDelta;
 
        // take a step on the y axis
        vsin += vcosscaled;
        vcos -= vsinscaled;
    }
```

### Smoothstep Method
```
float Sin (const in float _x)
{
    // make a triangle wave that has y values from 0-1, where y is 0 at x=0
	float x = abs(fract((_x - radians(90.0)) / radians(360.0))*2.0-1.0);
       
    // smoothstep the triangle wave and then scale it to the -1 to 1 range
    return smoothstep(0.0,1.0,x) * 2.0 - 1.0;
	
    // Note that you could use this instead of smoothstep above.  Same thing.
    //float x2 = x*x; 
	//return ((3.0 * x2) - (2.0 * x2 * x)) * 2.0 - 1.0;
    
    // or this:
    //return x * x * (3.0 - 2.0 * x) * 2.0 - 1.0;
}
```

### Cordic Mathematics

TBD

