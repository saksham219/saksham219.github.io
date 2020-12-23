---
layout:	post
title:	"Visualising a nowhere differentiable everywhere continuous function"
date:	2020-12-23
featured-image: rudin_mandelbrot.gif
---


While going through Baby Rudin, I came across an interesting idea where Rudin constructs a function which is continous everywhere but differentiable nowhere. This was interesting. I tried to think of what could a function like this look like. The simplest function which is continuous but differentiable at a single point I could think of was the absolute value function, which is differentiable everywhere except x = 0. This looks has a V shape, so I thought if I could somehow compress the V to create more and more jagged edges then one could obtain a function which has more and more edges where the function is differentiable, but no matter how many edges you create, there are always a few points where the function is continuous.

### So how did *Rudin* construct the function?

By using the concepts of series of functions, uniform convergence and continuity.

The proof is easy to understand and in the book (Theorem 7.18, Edition 2). I will show some visual aspects of the construction here, what the finally constructed function looks like, and why it is *continuous everywhere and differentiable nowhere* on R¹(domain of the function constructed)

I don’t know how Rudin was able to think of this (as many other things in Baby Rudin) but probably the idea was to construct a series of functions where each function reduces in height by a factor, and gets compressed by another factor.

First we took the absolute value function and restricted its domain. We also made it periodic, so that we are able to cover the complete domain R¹.

![](https://cdn-images-1.medium.com/max/2000/1*v9yE4B_zSeW_P6Vs1LLH1g.png)

![The perioidic function phi(x)](https://cdn-images-1.medium.com/max/2000/1*U2HXCO0e3AiNubEUCtC-8g.png)*The perioidic function phi(x)*

Note, that this periodicity also allowed us to bound the function, a fact that will play a key role in the *convergence* proved later.

Rudin goes on to show that this function is indeed *continuous everywhere* by invoking the [Lipshitz continuity](https://users.wpi.edu/~walker/MA500/HANDOUTS/LipschitzContinuity.pdf).
> Then we define the function that we need by constructing a series from the function defined above. The key feature of this series is that every term in the series reduces in height by a factor of 3/4 and gets compressed by a factor of 4 as compared to the previous term in the sequence.

Here are some of the 
terms of this series, with all the functions of the series being periodic with a period of 2.

![](https://cdn-images-1.medium.com/max/2000/1*hkbNBUbCdByZSqS5rv80qw.png)

These are how the terms of this series visualised. Notice** how they get shorter in height and compressed.**

![](https://cdn-images-1.medium.com/max/2000/1*xBK9RSCwloMtomq49KdCmw.gif)

Then by summing up all these functions in a series, the hope is to get a function which-

1. converges *uniformly *on R¹

1. is *continuous everywhere*

1. is *differentiable nowhere*

This function,

![](https://cdn-images-1.medium.com/max/2000/1*rI3jClrfVXdu8wm8senMIA.png)

is the function that we want. But the question arises about how does this look like? And why does the sum of all these scaled and compressed functions converge at every *x? *
Well, Rudin makes an argument that since every term of this series is positive and bounded by 1, we can use the [M-Test](https://en.wikipedia.org/wiki/Weierstrass_M-test) to say that the series converges *uniformly.* To what value does the series converge at each *x *is irrelevant for the argument. *
Then one can say that the limit of a continuous series of functions is also continuous if the series converges uniformly, so f(x) is continuous.*

Let’s go ahead and see what this function will look like. For the purpose of visualising this I am taking a large number (500) as infinity.

![](https://cdn-images-1.medium.com/max/2000/1*VxJVXTiGt3XBsnQUcK1Wcg.png)

Now, that’s a weird looking function. On closer inspection it makes sense, as this function is symmetric and looks like what you will get if you add a huge(***infinite**) *amount of *compressed and scaled periodic absolute functions. *When I zoom into this function, I see lots and lots of zigzags. Well, if you’re thinking what I’m thinking then we’re both thinking Fractals! I wish I could have chosen a very very large value to see the infinite repetition on zooming, but I will just replay the gif here to kind of produce that effect.

![](https://cdn-images-1.medium.com/max/2000/1*9mN8vpsLryp_nz6RFym8qw.gif)
> Well, the idea kind of fits in if you think about it. The function is so jagged as it the series such that at every point it’s not possible to find the derivative. Rudin shows this rigorously in the book by showing that the slope of the line between two arbitrarily close points (which is the derivative) becomes arbitrarily large as the difference between the point tends to zero, *thus completing the argument.*

As a final animation, I will try to point the value this function outputs at each x in the domain (R¹), to show that it actually assumes one value at each point thus showing that the function does indeed converge at every x thus also being continuous at every x. The moving marker in the animation below is the value the function converges to (infinity assumed to be 500) at every x.

![](https://cdn-images-1.medium.com/max/2000/1*C3DHdAWAEAeoy_SyyEXwsg.gif)
