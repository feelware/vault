Most of what I did is based on 3Blue1Brown's video on the Fourier transform. The whole process can be described at a very high level:

1. Take the signal you want to analyze and "wrap it" around a circle at a certain "winding rate" named `f`
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

You can multiply them too, though it's a bit trickier to understand intuitively. Don't worry about it though.

Here, the orange dot represents the product of the blue and green ones.

![](../../utilities/attachments/Pasted%20image%2020260615235956.png)

I'm gonna tell you something that's very likely not to be intuitive: **you can raise numbers to complex powers**. This is particularly hard to grasp if your only conception of exponentiation is "multiplying a number by itself a certain number of times", which is how's usually taught in school.

You don't really need to understand the underlying math! All I want you to know is this:

Let's say you have a real number, different from 0 or 1, that's being raised to a complex power `ai`. If you continuously change the value of `a`, you will notice that **the resulting dot oscillates around the origin (0, 0)**.

[ft-complex-power.mp4]

Furthermore, if you multiply the exponent by yet another number `f`, you can use it to control the rate at which the dot oscillates.

[ft-complex-power-rate.mp4]

Let's say we're not interested in the dot itself, but rather in the "trajectory" that it'd take. In this case, it'd be more convenient to define a **function** `c(t)` that maps every moment in time to the position of the dot at that moment. More formally: `c(t) = 2^(fti)`

[ft-complex-valued-function.mp4]

Naturally, we've replaced `a` by the variable `t`, which represents time. Notice how increasing `f` extends the curve's range, though it doesn't seem to do anything once it comes full circle. It's actually more interesting that this, like we'll see later. Right now, the main idea is that you can effectively represent oscillations in function of time using complex-valued functions.

> [!Side note]
> Rather than 2, the base we usually choose for `c(t)` is the number `e`, which is roughly equal to 2.718. The exponent `fti` is usually multiplied by `-2π`. With these considerations, we redefine `c(t)` as `e^(-2πfti)`. Don't think too much of this, it just helps with the units.

We first mentioned that the first step of the Fourier transform is to "wrap" the signal we want to analyze around a circle. More formally, this means multiplying that signal, which we'll represent as a real-valued function `g(t)`, by the complex-valued function `c(t)` we constructed earlier. We'll call this product `w(t)`.

So, in other words:

`w(t) = g(t)c(t) = g(t)e^(-2πfti)`

Let's say that `g(t)`, the signal you want to analyze, is a simple 3 Hz sine wave.

![](../../utilities/attachments/Pasted%20image%2020260615220407.png)

This is what the resulting curve `w(t)` looks like when `f` is equal to 1:

![](../../utilities/attachments/Pasted%20image%2020260616023404.png)

When `f` is equal to 2

![](../../utilities/attachments/Pasted%20image%2020260616023651.png)

And when `f` is equal to 3

![](../../utilities/attachments/Pasted%20image%2020260616023703.png)

Notice how the curve becomes a perfect circle once `f` matches the exact frequency of `g(t)` (3 Hz).

When `f` becomes 4, `w(t)` is not a circle anymore.

![](../../utilities/attachments/Pasted%20image%2020260621012557.png)

You can think of `f` as the rate at which we're "winding" `g(t)` around the origin (0, 0). When it matches certain values, you get interesting curves with special properties.

[ft-w-f.mp4]

Now it's time to calculate the center of mass we talked about: the point that represents the "average" of the curve. One way to do this is to evaluate `w(t)` at multiple values of `t` and literally calculate the results' mean.

> [!Side note]
> The mean of a collection of numbers is just their sum divided by the number of elements in the collection.

As an example, let's try evaluating `w(t)` at five values of `t`: `0.2`, `0.4`, `0.6`, `0.8`, and `1`. The five blue dots represent the evaluation results; and the red one, their mean. In this example, `f` is equal to `10.5`.

![](../../utilities/attachments/Pasted%20image%2020260621183150.png)

It makes sense to think that, the more values of `t` we consider, the closer the red dot will be to the actual center of mass. For convenience, let's call that number of values "`p`".

`p = 5` seems like too little, so let's increase it to 10 instead, the values chosen for `t` being `0.1`, `0.2`, `0.3`... all the way up to `1`.

![](../../utilities/attachments/Pasted%20image%2020260621184521.png)

Notice how the red dot went from the left side of the plane to the right. More specifically, the real component went from `-0.073` to `0.076` Let's see what happens with `p = 20`.

![](../../utilities/attachments/Pasted%20image%2020260621184856.png)

The red dot is on the left side again, the real component being `-0.026`. Let's try  `p = 100`

![](../../utilities/attachments/Pasted%20image%2020260621190038.png)

Still on the left side (`-0.01`).

The red dot seems to converge towards a certain position once `p` gets large enough.

[ft-center-of-mass-p-animated.mp4]

This graph shows exactly that by comparing each value of `p` to the real component of the red dot. It starts a little weird, but you can tell how it eventually settles.

![](../../utilities/attachments/Pasted%20image%2020260621192056.png)

Wouldn't it be great if `p` was somehow equal to infinity? Right now, all values of `t` are equally spaced from each other. The greater `p` becomes, the smaller the gap is, but it's still non-zero, so you're still missing some of the curve. `p` being equal to infinity would reduce the gap to 0, causing the whole curve to be averaged and making the center of mass perfectly accurate.

 The good thing is that we have a mathematical tool that allows us to do exactly that: the integral.
