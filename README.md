# ChaoticIFSFractal3D
Code By Michael Sherif Naguib 8/9/19
## What Are Chaotic IFS Fractals
- Chaotic IFS Fractals are fractals generated using an iterated function system. It is akin to calling a mathematical function on
 itself over and over again ```f(f(f(f(x))))```. The nth value is the function called on itself n times
- Doing this with vector functions which take a vector as an input and return the next vector 
 yeilds a system which can calculate a set of points. 
- A *chaotic* system is one which selects the function ```f``` at random from a set of functions.
 Consider the ordered set of functions ```{f(x),g(x),h(x)}``` and their coresponding probabilities ```{1/3,1/3,1/3}```. At each step 
 in the IFS calculation a random function based upon it's probability will be selected and applied. For example ```f(g(h(f(f(f(g(h(g(h(x)))))))))```. 
- Note the first point is ```p_1 = h(x)``` the seccond is ``` p_2 = g(h(x)) = g(p_1)``` ... etc ... 
- In the case of using a vector the function preforms what is called *Affine Transformations*: Consider shifting a point on the cartesian plane
left right up or down ... this is just one type of affine transformation a *shift*, There are also *Stretches*, *Skews*, and even *Rotations* (which is actually just a special skew and stretch).
- All of these operations can be simplified using *Linear Algebra*: Euler Angle Rotation Matricies as well as the concept of Matrix Multiplication and Vector
Addition enable a easy way to specify a transformation.
- A fractal according to [The Fractal Foundation](https://fractalfoundation.org/resources/what-are-fractals/) is: 
> "... is a never-ending pattern. Fractals are infinitely complex patterns that are self-similar across different scales"
- Iterated function systems generate fractals when the functions are specified are carefully designed so that the fractal stays bounded withine
a certain space. Consider a naieve IFS system for a scalar (1D 'one variable') function on itself: say ```f(x) = x^2``` then the ordered set of points 
generated by this function for a given starting point ```x_0 = 7``` would be ```{49,2401,5764801,33232930569601} ``` . As the reader can see even after only calculating the 4th term for the IFS it becomes massive! 
## About this Code
- The main reason I was able to do this code was because I found a fantastic library for visualizing the points
- ChaoticIFSFractal3D is actually faster than Chaotic-IFS-Fractal repo's code ... The reason being I found a better way to precalculate many of the variables 
used for the functions. An Affine transformation boils down to a Matrix * Point Vector  + Shift ... but often that matrix is itself a combination of other values... those can be precomputed, that is what this code does and it yeilds a signifigant (asyntotically constant) speed increase.
- As not many 3D fractal are hard to find a few of these equations were derived using a methodology which I adapted from 
[Agnes Scott College](http://larryriddle.agnesscott.org/ifs/heighway/goldenDragon.htm). I apply the 2D derivation to a 3D setting ... To best understand how 
fractal equations for IFS are designed consider looking at the Serinpenski Triangle and consider how each function is transforming the starting point.
- There are several Fractals which I have either derived or found online. These are listed in the **Create a list of IFS Functions** section in the Code.
- triangle, dragon, and orb are my derivations ... The others were found on [Paul Bourke's Site](http://paulbourke.net/fractals/ifs/). *NOTE* I dervied the dragon fractal to be a 3D variant of the 3D Right Angle Dragon Fractal. Notably When I first viewed it was very sparse making it difficult to see its true
fractal nature. I decided to adjust a scaling factor I thought would result in a more condensed fractal: to my delight it did with spectacular results...
I have coded a separate constant which allows you to modify the original: in the **Define a LOT of constants for various fractals** section look for the
variable called ```hyper_constant``` ... setting it to a value of 1 means identity/ that the calculation is as I derived it. I found values on the range [1,2] to be very interesting ... 1.8 in particular is a great number. (which was found by trial and repptition)
## Screenshots
- Here are screenshots of several of the fractals although to really see the patter it is much more interesting to actually view it in 3d rotating it to see
hidden detail that is not easily captured by one 2D image ... 
- Here is a screenshot of the Dragon Fractal: (hyper_constant = 1.8) 
![Dragon Fractal](https://raw.githubusercontent.com/Michael-Naguib/ChaoticIFSFractal3D/master/dragon_hc1.8_.PNG "Dragon")
- Here is a screenshot of the [Paul Bourke's](http://paulbourke.net/fractals/ifs/) Hedgehog Fractal: 
![Hedgehog Fractal](https://raw.githubusercontent.com/Michael-Naguib/ChaoticIFSFractal3D/master/hedgehog.PNG "Hedgehog")
- Here is a screenshot of the Serinpenski (tetrahedron) Fractal: (note the perspective is actually inside the fractal)
![Triangle Fractal](https://raw.githubusercontent.com/Michael-Naguib/ChaoticIFSFractal3D/master/triangle_inside.PNG "Triangle")

## Usage
- in the **Run a Calculation** section the point quantity, starting point, as well as the desired fractal system can be specified using the dictionary of Predefined Fractal Functions... mearly change the string value 
## Devlopment
- The way this code works in short:  I create a function makeIFSFunc which accepts a list of functions to be used as transformations ```[F(v),H(v),G(v),...]``` as well as their probabilities ```[p1,p2,p3,...]``` and returns a function that selects and returns at random according to the probabilities one of the transformation functions. Later on in the code I then specify all the constants needed for each transformation function and build a lit of transformation functions... 
- (it is easier to just see how I use it ... This was a quick (complex at first) but simple way to specify a large volume of equations and constants)
## Dependancies
- tqdm, pptk, numpy, random, math
## Features
- 3D display of points using an efficient GPU implementation
- (Planned) Coloring of points based on transfomration function used ( ... technically i had coded this but removed it as I wanted to make it an easily configurable option rather than a hardcoded generative system that colors the points ...)
- (Planned) Save the data and load the data between runs ... (fractals with many transformations take longer to compute to a convergence of point density ... i.e the fractal pattern needs more points to be recognizable as a fractal to humans ... most pc's are fast enough tho to compute these anyway in a matter of a minute)


