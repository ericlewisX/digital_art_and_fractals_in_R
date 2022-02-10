# The Wonders of Digital Art and Fractals 
## A Project on Visualizations Using R 
Showed the teaching capabilities of R by making digital art and fractals from scratch. I also presented this as an undergrad at MATHFEST 2016 !!! =D
 
---
## Slideshow Presentation - (html file)
WARNING : If clicking open the html file, make sure Browser is zoomed out and use Arrow Keys to navigate the slideshow.

---


## Abstract
We will present some visualization projects by mixing programming, mathematics and experimentation to showcase some artistic creations that can be made with R. 

- Digital Art
  + Surface Plots
  + Heat Maps (requires package devtools)  
  + Contour Projections
- Fractals
  + Sierpinski Shapes
  + Classical Chaotic Dynamical Systems
  + Heighway Dragon

**Supported by the Department of Education MSEIP grant # P120A150063**

Project Team: Eric Lewis, Yanna Chen, Ricky Hardiyanto and Boyan Kostadinov. 

--- 

## Introduction

**What exactly are contour projections, surface plots, heat maps?**

Heat maps are graphs where a matrix's individual values are denoted by colors. It is a 2D representation that uses colors to help explain relationships of data that would be easier to decipher than looking at a spreadsheet equivalent. 
We will implement several functions to show these images. 

<img src="http://i.imgur.com/KEhyBHO.gif" title="source: imgur.com" style="width:400px;height=400px;" /></a>


--- 

## Introduction (continued)

**What are fractals?**
Fractals are geometric figures that are self-similar across all of its scalar levels. That is to say that a smaller part of a fractal at different scales usually resembles the whole fractal. 
We will implement several well-known recursive functions and dynamical systems to demonstrate fractals.

<img src="http://i.imgur.com/TiEY9vR.jpg" title="source: imgur.com" style="width:360px;height=360px;" /></a> <img src="http://i.imgur.com/esRUfti.jpg" title="source: imgur.com" style="width:300px;height=300px;" /></a> <img src="http://i.imgur.com/vHXR8U6.jpg" title="source: imgur.com" style="width:257px;height=257px;" /></a> 

--- 

## Methodology
Our first goal is to make digital art.
To do this we make a function z(X,Y) where we assign the independent variables X and Y with their corresponding vectors of possible values that we choose. Using the function z, we will generate the surface plots and heat maps which we will then overlay with our contour projections of two-dimensional surfaces.

Our second goal is to make fractals without using the built-in R functions. To do this we will explain how to make a basic well-known fractal; The Sierpinksi Carpet. 
To make the Sierpinski Carpet we will construct a matrix: 

<img src="http://i.imgur.com/ojKquzC.png" title="source: imgur.com" style="width:300px;height=300px;"/></a>

After making this matrix, the idea will be to make a for-loop that can manipulate this matrix in such a way that when the recursive property is in-effect, each element A is treated just as the initial matrix f(A) has been treated.

--- 

## Analysis
#### Digital Art Through Surface Plots, Heat Maps and Contour Projections
Here we initialize the surface z to show the 12 points we will sample from.

```{r, echo=TRUE, warning=FALSE}
library("plot3D")         #required library for plots
x <- c(1,2,3,4)           #vector of x-values
y <- c(-1,0,1)            #vector of y-values
z <- 2*x + 5*y            #given function
M <- mesh(x,y)            #creates a rectangular full 2D or 3D grid
(zz <- 2*M$x + 5*M$y)     #Mesh in tandem with X & Y to get our 12 points
         
```


---

```{r, eval=FALSE, warning=FALSE}
plot(M$x,M$y, xlim=c(0.5,4.5), ylim=c(-1.5,1.5), pch = 16, xlab="x-values", ylab="y-values")
```
<img src="http://i.imgur.com/RwQLLLM.png" title="source: imgur.com" style="width:250px;height=250px;"/></a>

This is the plot of the actual surface we generate from the given vectors of X and Y.
```{r, eval=FALSE}
persp3D( M$x, M$y, zz,colvar=zz,colkey=FALSE,shade = 0.1,box=TRUE,theta=320) #plotting the surface
```

<img src="http://i.imgur.com/1pr7OXr.png" title="source: imgur.com" style="width:250px;height=250px;"/></a>

---

This is the corresonding heat map of the matrix zz. As we can see colors are assigned to each number from the matrix to produce this heat map. Colors that are close to each other are indicative of close numbers.
```{r,echo=FALSE,eval=TRUE}
zz
```

```{r,eval=FALSE}
image(zz, axes=FALSE)
```

<img src="http://i.imgur.com/xEXuxaP.png" title="source: imgur.com" style="width:250px;height=250px;" /></a>

---- 

## Analysis(cont.)
Now that we made a heat map in 2D we are going to up the ante and the dimension by one.
We will be using the function <img src="http://i.imgur.com/AlFjTKO.jpg" title="source: imgur.com" style="width:250px;height=250px;" /></a> as our given function. Repeating the same steps as above we would generate a 3D heat map. To get a better descriptive look at the graphical interpretation of this function we must set the independent variables to all the variables within its domain. Since we are dealing with trig functions the domain is <img src="http://i.imgur.com/bo1ZhX5.jpg" title="source: imgur.com" style="width:100px;height=100px;" /></a>
```{r,eval=FALSE,echo=FALSE}
x <- seq(-2*pi,2*pi,length.out = 300)             #vector of x-values
y <- seq(-2*pi,2*pi,length.out = 300)             #vector of y-values
M <- mesh(x,y)                                    #creates a rectangular full 2D or 3D grid
z <- cos(x^2 + y^2)*exp((-1/pi)*sqrt(x^2 + y^2))  #our given function
zz <- cos(M$x^2 + M$y^2)*exp((-1/pi)*sqrt(M$x^2 + M$y^2)) #Mesh in tandem with Vectors X & Y
persp3D(M$x,M$y,zz,colvar=zz,colkey=FALSE,shade=0.5,box=FALSE,theta=60) #plotting the surface 

```

<img src="http://i.imgur.com/xahlPuO.png" title="source: imgur.com" style="width:800px;height=800px;" /></a>

<img src="http://i.imgur.com/WXnHxi2.png" title="source: imgur.com" style="width:200px;height=200px;" /></a>

--- 

## Analysis(cont.)
We will now use our proven methods our gerenating heat maps and contour plots to generate digital art.
Our new function is: <img src="http://i.imgur.com/AlFjTKO.jpg" title="source: imgur.com" style="width:250px;height=250px;" /></a>.

We will sample 27 points from the interval <img src="http://i.imgur.com/QNeySsR.jpg" title="source: imgur.com" style="width:100px;height=100px;" /></a> 
```{r,eval=FALSE,echo=FALSE}
x <- seq(-4*pi,4*pi,length.out = 27)              #vector of x-values
y <- seq(-4*pi,4*pi,length.out = 27)              #vector of y-values
M <- mesh(x,y)
z <- cos(x^2 + y^2)*exp((-1/pi)*sqrt(x^2 + y^2))  #our given function
zz <- cos(M$x^2 + M$y^2)*exp((-1/pi)*sqrt(M$x^2 + M$y^2)) #Mesh in tandem with indep. variables
persp3D(M$x,M$y,zz,colvar=zz,colkey=FALSE,shade=0.5,box=FALSE,theta=60) #plotting the surface 
```
<img src="http://i.imgur.com/jjtH6FJ.png" title="source: imgur.com" style="width:800px;height=800px;" /></a>

<img src="http://i.imgur.com/LdvniQ5.png" title="source: imgur.com" style="width:200px;height=200px;" /></a>

---

```{r,eval=TRUE,echo=FALSE, include=FALSE}
x <- seq(-4*pi,4*pi,length.out = 27)              #vector of x-values
y <- seq(-4*pi,4*pi,length.out = 27)              #vector of y-values
M <- mesh(x,y)
z <- cos(x^2 + y^2)*exp((-1/pi)*sqrt(x^2 + y^2))  #our given function
zz <- cos(M$x^2 + M$y^2)*exp((-1/pi)*sqrt(M$x^2 + M$y^2)) #Mesh in tandem with indep. variables
persp3D(M$x,M$y,zz,colvar=zz,colkey=FALSE,shade=0.5,box=FALSE,theta=60) #plotting the surface 
```
We  show the aerial view of the function now added with contour plots to finish our digital art masterpiece.
```{r}
image2D(zz, axes=FALSE)
contour2D(zz,add=TRUE,colkey=FALSE,drawlabels=FALSE,axes=FALSE,frame=TRUE)

```

---

## Analysis(cont.)

We repeat the same steps as before this time using image() to plot the heat map. We also use contour() to superimpose the contour plot of z. Our new function is <img src="http://i.imgur.com/Uhs6eu9.jpg" title="source: imgur.com" style="width:250px;height=250px;" /></a>

We will sample 27 points from the interval <img src="http://i.imgur.com/Vozoe7P.jpg" title="source: imgur.com" style="width:100px;height=100px;" /></a>.
```{r,echo=FALSE,eval=FALSE}
x <- seq(-7*pi,7*pi,length.out = 27)
y <- seq(-7*pi,7*pi,length.out = 27)
M <- mesh(x,y) #z <- tan(x^2 + y^2)*exp((-1/pi^2)*sqrt(x^2 + y^2))
zz <- tan(M$x^2 + M$y^2)*exp((-1/pi^2)*sqrt(M$x^2 + M$y^2))
persp3D( M$x, M$y, zz, colvar=zz, colkey = FALSE, shade = 0.5, box = FALSE, theta = 60)
```
<img src="http://i.imgur.com/6kZDG8A.png" title="source: imgur.com" style="width:800px;height=800px;" /></a>

<img src="http://i.imgur.com/kcjiX6u.png" title="source: imgur.com" style="width:200px;height=200px;" /></a>

---

```{r,echo=FALSE,eval=TRUE,include=FALSE}
x <- seq(-7*pi,7*pi,length.out = 27)
y <- seq(-7*pi,7*pi,length.out = 27)
M <- mesh(x,y) #z <- tan(x^2 + y^2)*exp((-1/pi^2)*sqrt(x^2 + y^2))
zz <- tan(M$x^2 + M$y^2)*exp((-1/pi^2)*sqrt(M$x^2 + M$y^2))
persp3D( M$x, M$y, zz, colvar=zz, colkey = FALSE, shade = 0.5, box = FALSE, theta = 60)
```

```{r}
image(zz,axes=FALSE)
contour(zz,add=TRUE,colkey=FALSE,drawlabels=FALSE,axes=FALSE,frame=TRUE)
```

--- 

## Fractals
<img src="http://i.imgur.com/1GClod7.gif" title="source: imgur.com" style="width:200px;height=200px;" /></a>

To make the Sierpinksi Carpet we must first generate a matrix f(A).

<img src="http://i.imgur.com/SSDsCpX.png" title="source: imgur.com" style="width:200px;height=200px;" /></a>

An effective way to do this is with binding. R has built-in functions to bind elements by row and by column. We take advantage of this by using a couple of binds in quick-succesion. First we bind 3 copies of the element A by column to form a row of 3 elements of A. That will be our top row of our desired matrix. The middle element in the second row will eventually be our "hole" that we see through each of the iterations.
To get the second row with a zero in the middle we do the same bind except that we multiply the middle element by 0. It must be multiplied and not just inputted as zero because if the element is a matrix, the act of multipliying by zero will count as multiplying by the zero matrix. 

---

We will first generate the matrix above which is the same as a Level 1 Sierpinski Carpet.

<img src="http://i.imgur.com/L9hNsif.png" title="source: imgur.com" style="width:700px;height=700px;" /></a>
<img src="http://i.imgur.com/8Py3mnf.png" title="source: imgur.com" style="width:400px;height=400px;" /></a>

```{r,echo=FALSE, eval=FALSE}
IterateCarpet <- function(A){
  B <- cbind(A,A,A)               #Binds three elements names A into a row of A.
  C <- cbind(A,0*A,A)             #Multiplied by 0 to indicate the hole in the level 1 carpet.
  D <- rbind(B,C,B)               #Binds three rows together to form a 3x3 Matrix
  return(D)                       
}
S <- matrix(1,1,1);
S <- IterateCarpet(S);
image(S,col=c(0, 12), axes=FALSE, asp=1)
```

---

Now that we have the Level 1 Carpet we must add a (for-loop) that will allow us to add the recursion that will show the self-similar property that fractals are known for.

<img src="http://i.imgur.com/X61nIi8.png" title="source: imgur.com" style="width:700px;height=700px;" /></a>
<img src="http://i.imgur.com/cK7LmKw.png" title="source: imgur.com" style="width:300px;height=300px;" /></a>

```{r,echo=FALSE,eval=FALSE}
IterateCarpet <- function(A){
  B <- cbind(A,A,A)
  C <- cbind(A,0*A,A)
  D <- rbind(B,C,B)
  return(D)
}
S <- matrix(1,1,1);

for(i in 1:2)
  S <- IterateCarpet(S);

image(S,col=c(0, 12), axes=FALSE, asp=1)
```

---

Level 6 Sierpinski Carpet:

```{r,echo=FALSE}
IterateCarpet <- function(A){
  B <- cbind(A,A,A)
  C <- cbind(A,0*A,A)
  D <- rbind(B,C,B)
  return(D)
}
S <- matrix(1,1,1);

for(i in 1:6)
  S <- IterateCarpet(S);

image(S,col=c(0, 12), axes=FALSE, asp=1)
```

As you can see we manipulate recursion by changing the number of iteration in the (for-loop).
Now that we know our function is reliable in finding fractals we get creative by manipulating the initial matrix f(A) solely to get various fractals. 

--- 

Level 6 Sierpinski Triangle &
Level 5 Sierpinski Snowflake

<img src="http://i.imgur.com/0FYtcU2.png" title="source: imgur.com" style="width:900px;height=900px;" /></a>

```{r,echo=FALSE,eval=FALSE}
IterateStar <- function(A){
  B <- cbind(A,   A*0,  A)
  C <- cbind(A*0, A,    A*0)
  D <- cbind(A,   A*0,  A)
  E <- rbind(B,C,D)
  return(E)
}

t <- matrix(1,1,1);
for(i in 1:5) 
  t <- IterateStar(t);

image(t,col=c(0, 12), axes=FALSE, asp=1)
```

```{r,echo=FALSE,eval=FALSE}
IterateModified <- function(A){
  B <- cbind(A*0  , A*0,   A)
  C <- cbind(A*0  , A,   A)
  D <- cbind(A  , A,   A)
  E <- rbind(B,C,D)
  return(E)
}

t <- matrix(1,1,1);
for(i in 1:6) t <- IterateModified(t);

image(t,col=c(0, 12), axes=FALSE, asp=1)
```

---

## Dynamical Systems
Fractals can also be created by simulating different kinds of dynamical systems.

<img src="http://i.imgur.com/9LNakEu.png" title="source: imgur.com" style="width:600px;height=600px;" /></a>
<img src="http://i.imgur.com/J9VH8MT.png" title="source: imgur.com" style="width:300px;height=300px;" /></a>

```{r,eval=FALSE,echo=FALSE}
wallpaper<-function(n=4E4,x0=1,y0=1,a=1,b=4,c=60){
  x<-c(x0,rep(NA,n-1))
  y<-c(y0,rep(NA,n-1))
  cor<-rep(0,n)
  
  for (i in 2:n){
    x[i] = y[i-1] - sign(x[i-1])*sqrt(abs( b*x[i-1] - c) )
    y[i] = a - x[i-1]
    cor[i]<-round(sqrt((x[i]-x[i-1])^2+(y[i]-y[i-1])^2),0)
  }
  n.c<-length(unique(cor))
  cores<-heat.colors(n.c)
  
  plot(x,y,pch=".",col=cores[cor])
}
wallpaper()

```

---

Here we use Euler's Method to simulate chaotic dynamical systems.
```{r}
library("rgl")

LiSys <- function(n, a=5, b=16, c=1, x0=5, y0=4, z0=10){
  x<-c(x0,rep(NA,n-1))
  y<-c(y0,rep(NA,n-1))
  z<-c(z0,rep(NA,n-1))
  h<-0.01
  for (i in 2:n){
    x[i] = x[i-1] + h*(a*(y[i-1]-x[i-1]))
    y[i] = y[i-1] + h*(x[i-1]*z[i-1] - y[i-1])
    z[i] = z[i-1] + h*(b - x[i-1]*y[i-1] - c*z[i-1])
  }
  require(rgl)
  rgl.clear()
  rgl.points(x,y,z, color=heat.colors(n), size=2)
}
LiSys(20000)
```

---

## Chaotic Dynamical Systems
Li System

<img src="http://i.imgur.com/EtcNFmq.jpg" title="source: imgur.com" style="width:490px;height=490px;" /></a>
<img src="http://i.imgur.com/fyXYKOq.jpg" title="source: imgur.com" style="width:275px;height=275px;" /></a>
<img src="http://i.imgur.com/toJc5JZ.jpg" title="source: imgur.com" style="width:200px;height=200px;" /></a>

---

```{r}
ThoSys <- function(n, b=0.209, x0=0.5, y0=0.4, z0=0.8){
  x<-c(x0,rep(NA,n-1))
  y<-c(y0,rep(NA,n-1))
  z<-c(z0,rep(NA,n-1))
  h<-0.01
  for (i in 2:n){
    x[i] = x[i-1] + h*(sin(y[i-1]) - b*x[i-1])
    y[i] = y[i-1] + h*(sin(z[i-1]) - b*y[i-1])
    z[i] = z[i-1] + h*(sin(x[i-1]) - b*z[i-1])
  }
  require(rgl)
  rgl.clear()
  rgl.points(x,y,z, color=heat.colors(n), size=2)
}

ThoSys(20000)
```

---

## Chaotic Dynamical Systems
Thomas System

<img src="http://i.imgur.com/zivlZsy.jpg" title="source: imgur.com" style="width:500px;height=500px;" /></a>
<img src="http://i.imgur.com/cOxc5Dt.jpg" title="source: imgur.com" style="width:215px;height=215px;" /></a>
<img src="http://i.imgur.com/vsMNiEF.jpg" title="source: imgur.com" style="width:200px;height=200px;" /></a>



---

## The Heighway Dragon
The Fractal Dragon has many names, The Dragon Curve, The Heighway Dragon or even The Jurassic Park Fractal. It is very difficult to code but the concept is very easy to understand. This code is borrowed from Rosetta Code to show this impressive image.

<img src="http://i.imgur.com/Ee6nc8A.png" title="source: imgur.com" style="width:800px;height=800px;" /></a>

---

<img src="http://i.imgur.com/XtZlsHD.png" title="source: imgur.com" style="width:800px;height=800px;" /></a>

<img src="http://i.imgur.com/RYzEjST.png" title="source: imgur.com" style="width:350px;height=350px;" /></a> Level 2

<img src="http://i.imgur.com/jSJDJnz.png" title="source: imgur.com" style="width:350px;height=350px;" /></a> Level 3

---

## The Heighway Dragon - Level 15
<img src="http://i.imgur.com/qdK037g.png" title="source: imgur.com" style="width:800px;height=800px;" /></a>

```{r,eval=FALSE,echo=FALSE}
Dragon <- function(Iters)
  {
    Rotation<-matrix(c(0,-1,1,0),ncol=2,byrow=T)  #Rotation multiplication matrix
    Iteration<-list()                   #Set up list for segment matrices for 1st
    Iteration[[1]] <- matrix(rep(0,16), ncol = 4)
    Iteration[[1]][1,]<-c(0,0,1,0)
    Iteration[[1]][2,]<-c(1,0,1,-1)
    Moveposition<-rep(0,Iters)          #Which point should be shifted to origin
    Moveposition[1]<-4
    if(Iters > 1)                       #where to move to get to origin
      {                      
      for(l in 2:Iters)                 #only if >1, because 1 set before for loop
        {                
          Moveposition[l]<-(Moveposition[l-1]*2)-2
          #sets vector of all positions in matrix where last point is
        }
      }
    Move<-list()             #vector to add to all points to shift start at origin
    for (i in 1:Iters)
      {
        half<-dim(Iteration[[i]])[1]/2
        half<-1:half
        
        for(j in half)
          {                         #Rotate all points 90 degrees clockwise
            Iteration[[i]][j+length(half),]<-c(Iteration[[i]][j,1:2]%*%Rotation,Iteration[[i]][j,3:4]%*%Rotation)
          }
        Move[[i]]<-matrix(rep(0,4),ncol=4)
        Move[[i]][1,1:2]<-Move[[i]][1,3:4]<-(Iteration[[i]][Moveposition[i],c(3,4)]*-1)
        Iteration[[i+1]]<-matrix(rep(0,2*dim(Iteration[[i]])[1]*4),ncol=4)  #move the dragon, set next Iteration's matrix
        for(k in 1:dim(Iteration[[i]])[1])
          {     #move dragon by shifting all previous iterations point 
            Iteration[[i+1]][k,]<-Iteration[[i]][k,]+Move[[i]]                #so the start is at the origin
          }
        xlimits<-c(min(Iteration[[i]][,3])-2,max(Iteration[[i]][,3]+2))#Plot
        ylimits<-c(min(Iteration[[i]][,4])-2,max(Iteration[[i]][,4]+2))
        plot(0,0,type='n',axes=FALSE,xlab="",ylab="",xlim=xlimits,ylim=ylimits)
        s<-dim(Iteration[[i]])[1]
        s<-1:s
        segments(Iteration[[i]][s,1], Iteration[[i]][s,2], Iteration[[i]][s,3], Iteration[[i]][s,4], col= c('purple'))
      }
  }

```

---

## Conclusion 
R is mainly known for its value in statistics and its number crunching abilities. However it is not well known that R is a software that you can use to make innovative designs. We used mathematics to show heat maps and fractals, both with ubiquitous application in the world. We have proved that R is a viable way to show these amazing artistic creations.

--- 

## References
1. Fischer, Ericka. N.p., n.d. Web. 30 May 2016. <https://www.pinterest.com/pin/301600506266463011/?from_navigate=true>.
2. "Dragon Curve." - Rosetta Code. N.p., n.d. Web. 01 Aug. 2016.
3. Rouse, Margaret. "Heat Map Definition." Search Business Analytics. N.p., n.d. Web. 30 May 2016. <http://searchbusinessanalytics.techtarget.com/definition/heat-map>.
Tom. "What Are Fractals?" Frax. N.p., n.d. Web. 30 May 2016. <http://fract.al/background>.
4. Photographic, Warren. Image Library of Nature & Pets. N.p., n.d. Web. 30 May 2016. <http://www.warrenphotographic.co.uk/08811-ammonite>.


---
