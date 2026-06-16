Most of what I did is based on 3Blue1Brown's video on the Fourier transform. The whole process can be described at a very high level:

1. Take the signal you want to analyze and "wrap it" around a circle at a rate `f`
2. Each value of `f` will yield a different curve, try plugging in every frequency you wish to analyze: 1 Hz, 2 Hz, 3 Hz, and so on
3. For each resulting curve find its "center of mass", that is, the point that roughly represents the center of that curve. Like any 2D point, you can think of it as a coordinate with two values: `x` and `y`
4. Eureka! Those two values are the amplitude and phase for that specific frequency `f`
5. If you plot every value of `f` versus its corresponding `x` value, you will get the frequency spectrum of that signal

Now let's go into more detail

Before starting, there's a few things you need to know about complex numbers. Complex numbers have two components people refer to as "real" and "imaginary". A usual way to visualize them is as points in a 2D space where the X axis corresponds to the real component; and the Y axis, to the imaginary component.

In notation, they're usually represented as a sum of two parts: `ai + b`.

- `b` is the real part. It's an everyday real number. Changing its value moves the point _along_ the number line, the one you've seen in school
- `ai` is the imaginary part. `i` is the **imaginary unit**. `a` is a real number that quite literally multiples the imaginary unit: the greater it is, the farther the point is from the number line. Think of `i` as a "vertical" unit; as opposed to 1, which is "horizontal"

![](../../utilities/attachments/Pasted%20image%2020260615234629.png)

There's a series of operations you can do on complex numbers. For instance, to sum two complex numbers, you need to sum their real and imaginary components separately. Here, the orange dot represents the sum of the four complex numbers shown above.

![](../../utilities/attachments/Pasted%20image%2020260615234801.png)

You can multiply them too, though it's a bit trickier to understand intuitively. Don't worry about it. Here, the orange dot represents the product of the blue and green ones.

![](../../utilities/attachments/Pasted%20image%2020260615235956.png)

I'm gonna tell you something that's very likely not to be intuitive: **you can raise numbers to complex powers**. This is particularly hard to grasp if your only conception of exponentiation is "multiplying a number by itself a certain number of times", which is how's usually taught in school. You don't really need to understand the underlying math! All I want you to know is this:

Let's say you have a real number, different from 0 or 1, that's being raised to a complex power `ai`. If you continuously change the value of `a`, you will notice that **the resulting dot oscillates around the origin (0, 0)**.

[ft-complex-power.mp4]

Furthermore, if you multiply the exponent by yet another number `f`, you can use it to control the rate at which the dot oscillates.

[ft-complex-power-rate.mp4]

Let's say we're not interested in the dot itself, but rather in the "trajectory" that it'd take. In this case, it'd be more convenient to define a **function** `c(t)` that maps every moment in time to the position of the dot at that moment. More formally: `c(t) = 2^(fti)`

[ft-complex-valued-function.mp4]

Naturally, we've replaced `a` by the variable `t`, which represents time. Notice that increasing `f` extends the curve's range, though it doesn't seem to do anything once it comes full circle. We'll come back to this. Right now, the main idea is that you can effectively represent oscillations in function of time using complex-valued functions.

Side note: Rather than 2, the base we usually choose is the number `e`, which is roughly equal to 2.718. On the other hand, we multiply the exponent by `-2π`. Don't think too much of this, it just helps with the units.

We first mentioned that the first step of the Fourier transform is to "wrap" the signal we want to analyze around a circle. More formally, this means multiplying that signal, which we'll represent as a real-valued function `g(t)`, by the complex-valued function `c(t)` we just constructed.

We'll call this product `w(t) = g(t)c(t) = g(t)e^(-2πfti)`

Let's say `g(t)` is a simple 3 Hz sine wave.

![](../../utilities/attachments/Pasted%20image%2020260615220407.png)

This is the result of multiplying it by `c(t)`, for `f` equal to 1

![](../../utilities/attachments/Pasted%20image%2020260616023404.png)

`f` equal to 2

![](../../utilities/attachments/Pasted%20image%2020260616023651.png)

`f` equal to 3

![](../../utilities/attachments/Pasted%20image%2020260616023703.png)

Notice how different the curve looks when `f` matches the frequency of the signal we wish to analyze, which in this case is 3. This property will come in handy later on. For now, the main point is that `f`, also known as the winding frequency, significantly alters the curve resulting from `w(t)`.

[ft-w-f.mp4]
