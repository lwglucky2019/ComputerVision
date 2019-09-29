
# Understanding Gabor Filters
Posted on April 26, 2014	

1 mainIn the field of image processing, filters play an extremely important role. If you don’t know what a filter is, you may quickly want to read the wiki article and come back. Otherwise, this post will not make much sense to you. All image processing operations can be viewed as applying a series of filters to an image and transforming it in some way. We do this for a variety of reasons, like understanding the content of images, transforming the images into another domain, detecting the presence of something in the images, and so on. Gabor filter is a particular type of filter, and it happens to be an important one. If you google “Gabor filter”, you will get a lot of articles. So in this post, rather than looking at the mathematics behind it, we will try to understand the underlying concept. Let’s go ahead, shall we?  

## Why do we need this filter?

Let’s say you are trying to extract the edges from an image. These edges might be in any shape, size and orientation. When you apply a filter to an image, you basically modify each pixel in that image and extract some information from it. If you apply the same rule across the entire image, it might not be efficient. To give a fairly simple demonstrative example, an image might contain both horizontal and vertical edges. Now you design a filter that detects sharp horizontal edges very well. But what about those vertical edges? What about the edges that are not sharp? To take care of it, you design another filter which detects vertical edges. Going by this logic, does it mean that we need to design a separate filter for all of them? That’s not very efficient! Natural images usually tend to have a large number of shapes and sizes. How do we cater to all the different types? This is where Gabor filter comes into picture.

## What is a Gabor filter?

2 orientationGabor filters are orientation-sensitive filters, used for edge and texture analysis. It is named after Dennis Gabor, a brilliant Nobel prize winning physicist. A Gabor filter can be viewed as a sinusoidal plane of particular frequency and orientation, modulated by a Gaussian envelope. Wait, what does that even mean? Well, I can go into the mathematical explanation behind it, but that’s not what we want to do here. Basically, it means that Gabor filter is mathematically structured in such a way that it can take care of different shapes, sizes and smoothness levels in the image. A Gabor filter oriented in a particular direction gives a strong response for locations of the target images that have structures in this given direction. For example, if your target image is made up of edges in the diagonal direction, a Gabor filter set will give you a strong response only if its direction matches with the direction of the edges. It’s like pouring a solidifying liquid onto a unknown rigid structure. Once it solidifies and you take a look at the solidified form, it looks like the surface of the structure. Gabor filter does something similar for images!

## Why is this so important?

Gabor Filters have received considerable attention because they closely resemble the human visual system. All these attempts to design good filters are aimed at mimicking the human visual cortex. Humans have an uncanny ability to process visual data and distinguish things with extreme ease. Machines, not so much! The characteristics of certain cells in the visual cortex of some mammals can be approximated by these Gabor filters. In addition, these filters have been shown to possess optimal localization properties in both spatial and frequency domain. What this means is that you don’t have to worry about designing something that will fit all the cases. It will mould itself to suit different scenarios, like smoothness, orientation, scale, etc, of these edges. This is the reason they are well suited for edge detection and texture segmentation problems.

## Where are they used in real life?

Gabor filters have been used in many applications, such as:

    Texture segmentation: Gabor filters are used to separate multiple textures in an image. This analysis is critical in a lot of fields, including space missions where they have to traverse unknown terrains.
    Optical character recognition: To automatically recognize handwritten letters, number plates, billboards, etc.
    Object Recognition: Gabor filters and their modified versions are used extensively in computer vision. Since they can closely mimic the human visual system, they are used in designing object recognition systems.
    Fractal dimension management: Fractals are basically self-similar patterns. They are actually quite fascinating! You can google about it if you want to learn more.
    Edge detection: Detecting the edges in an image is preprocessing step in many image processing systems.
    Retina identification: Identifying the retina of humans reliably. Very important in security!
    Image coding: The encoding of images is used almost everywhere for transmission.

    --------------------

    
Understanding Gabor Filter

fig-1, 2D gaussian times cosine wave

This is an informal tutorial on the intuitive theory behind gabor filters used for image segmantation.
Objective:

We formulate the intuitive theory behind making a gabor filters from first principles. All the detailed derivation of the formulae is laid out in the appendix, so if you just want to take these formulae as granted, a firm grasp in fourier transforms is not essential. We also try out the results of these formulae and plot them in octave.
Notation:

The following notation is used in this post.
h(t)F(p(t))h(x,y)F(p(x,y))H(u,v)g(x,y)G(u,v)exp(t)========one dimensional gaussian functionP(f) ,fourier transform of function p(t)two dimensional gaussian functionP(u,v) ,fourier transform of 2D function p(x,y)F(h(x,y)) fourier transform of 2D gaussiancomplex 2D gabor function (in various forms)F(g(x,y))same as  et
Formulate the formulae for gabor filter
Gaussian function and its fourier transform

The equation for a one dimensional gaussian function is
h(t)=12π−−√σe−t22σ2(1)

For a general function p(t)
, the fourier transform F(p(t))=P(f)

is given by,
P(f)=∫∞−∞p(t)e−i2πftdt(2)

From (41)
, fourier transform F(h(t))=H(f) of h(t) in (1)

is,
H(f)==12π−−√σ2π−−√σe−2π2f2σ2e−2π2f2σ2(3)(4)
Introducing one dimensional gabor filter

Consider the functions ge(t)=h(t)cos(2πf1t)
and go(t)=h(t)sin(2πf1t), which are gaussian functions modulated by a cosine and a sine function respectively, where f1

is a fixed frequency.

fig-0, 1d gabor functions

The plots of the functions h(t),ge(t)
and go(t)

are shown above.

The one dimensional complex gabor filter is given by
g(t)===ge(t)+igo(t)h(t)(cos(2πf1t)+isin(2πf1t))h(t)ei2πf1(5)(6)(7)

Please note that the fourier transform of the product of two functions, p(t)
, q(t), is the convolution of their respective fourier transforms, ie P(f)∗Q(f)

.

Let us do a fourier analysis of ge(t)
and go(t)

.
F(ge(t))F(ge(t))==Ge(f)Go(f)==H(f)∗C(f)H(f)∗S(f)(8)(9)

Since p(x)∗q(x)=∫∞−∞p(t)q(x−t)dt
and since convolution is commutative, and using (62), (41)

,
Ge(f)====∫∞−∞C(u)H(f−u)du12∫∞−∞H(f−u)(δ(u+f1)+δ(u−f1))du12(H(f+f1)+H(f−f1))12(e−2π2(f+f1)2σ2+e−2π2(f−f1)2σ2)(10)(11)(12)(13)

So by (5)
, the real part of the fourier transform of ge(t) is the sum of two gaussian functions separated by ±f1, and the imaginary part is the difference of two gaussian finctions separeted by ±f1

.

Similarly, Go(f)====∫∞−∞S(u)H(f−u)dui2∫∞−∞H(f−u)(δ(u+f1)−δ(u−f1))dui2(H(f+f1)−H(f−f1))i2(e−2π2(f+f1)2σ2−e−2π2(f−f1)2σ2)(14)(15)(16)(17)

Similarly, G(f)===Ge(f)+iGo(f)12(H(f+f1)+H(f−f1))−12(H(f+f1)−H(f−f1))H(f−f1)(18)(19)(20)

fig-0, 1d gabor functions fourier transforms,
Introducing two dimensional gabor filter kernel

fig-1, 2D gaussian

In fig-3, we have plotted the function h(x,y)=12πσxσye−12(x2σ2x+y2σ2y)

and

fig-1, 2D cosine wave

A general 2D cosine function is given by c(x,y)=cos(2π(u1x+v1y))
, where u1,v1

are fixed spatial frequencies. This is shown in fig-4.

Just as in the case of the 1D gabor filter kernel, we define the 2D gabor filter kernel by the following equations. The complex 2D gabor filter kernel is given by g(x,y)

.
ge(x,y)go(x,y)g(x,y)====12πσxσye−12(x2σ2x+y2σ2y)cos(2π(u1x+v1y))12πσxσye−12(x2σ2x+y2σ2y)sin(2π(u1x+v1y))ge(x,y)+igo(x,y)12πσxσye−12(x2σ2x+y2σ2y)ei2π(u1x+v1y)(21)(22)(23)(24)

fig-1, 2D gaussian times cosine wave

In fig-5, we have plotted the function ge(x,y)=h(x,y).c(x,y)

.

Note that in fig-3, fig-4 and fig-5, the 3d perspective views are slightly rotated to accentuate their features for viewing decipherability.

Here is the octave code used for generating fig-5.

% octave code for showing  g_e(x, y) = gaussian times cosine function
%author kgeorge

clear all;
clc;
close all;
pkg load image



sigma_x = 0.5;
sigma_y = 0.5;

freq = 1.0;

%kernel size = 7 x 7
N=7;
NBY2 = floor(N/2);
tx=ty=linspace(-NBY2, NBY2, 50);
[xx, yy] = meshgrid(tx, ty);


%plot of a simple 2D gaussian
I = exp(-0.5 * ( (xx ./ sigma_x) .^2 +  (yy ./ sigma_y) .^2  ) );
I =  I .* (1.0/(2.0 * pi * sigma_x * sigma_y));


%plot of a 2D cosine wave
J = cos((xx + yy) .* (2 * pi * freq) );

colormap(copper)
s1 = subplot(2,1,2);
imshow(I .* J)
xlabel('x');
ylabel('y');

title(s1, sprintf("top view"));


colormap(copper)
s2 = subplot(2,1,1);
mesh(xx, yy, I .* J);
grid off;
view(33, 24);
xlabel('x');
ylabel('y');

title(s2, sprintf("perspective view, rotated for convenience"));



ha = axes('Position',[0 0 1 1],'Xlim',[0 1],'Ylim',[0 1],'Box','off','Visible','off','Units','normalized', 'clipping' , 'off');
text(0.5, 0.05, sprintf("fig 5, 2d gaussian times cos function,  \\sigma_x=%.1f,\\sigma_y=%.1f, u_1=%.1f, v_1=%.1f", sigma_x, sigma_y, freq, freq),'HorizontalAlignment','center','VerticalAlignment', 'top');
%save using a uility function
%saveInGithubBlog("gabor_2D_gssn_times_cos");


Please see (82)
for a derivation of the fourier transform of a gabor function as stated in (21). Shown below the image of the absolute value of the fourier transform for a gabor 2D function with σx=0.25,σy=0.125,u1=2 and v1=4. Note that it is an axially aligned elliptical gaussian whose origin is shifted to (u1,v1)=(2,4). Please disregard the axis lines drawn. If you look carefully, in the picture there is a black dot appearing exactly at the centre of the guassian. The black dot represents the frequency (2,4)

and was purposefully added to the image of the fft, just to verify the correctness of the shift. fig-1, 2D gaussian times cosine wave

We have now the equations for the most basic 2D gabor filter function (21)
and its fourier transform (87)

. But for using this filter function practically, we need to exploit the various ways by which this filter function can be parameterized.

First we will re-formulate (21)

using a more intuitive set of parameters.

A better way of expressing the parameters σx,σy
would be to capture the ratio between the two parameters. Thus by setting σ=σy and λ=σxσy, (21)

will become
g(x,y)==12πσxσye−12(x2σ2x+y2σ2y)ei2π(u1x+v1y)12πλσ2exp(−((xλ)2+y2)2σ2) exp(i2π(u1x+v1y))(25)(26)

Also, consider the term (u1x+v1y)
. If we set f1=u21+v21−−−−−−√, then we can introduce an angle parameter θ where, u1=f1cos(θ) and v1=f1sin(θ). With this the equation, (25)

becomes,

g(x,y)=12πλσ2exp(−((xλ)2+y2)2σ2) exp(i2πf1(xcos(θ)+ysin(θ)))(27)
The fourier transform of the above representation in (27) is given by (94)

, which is reproduced here.
G(u,v)=H(u−f1cos(θ);λσ)H(v−f1sin(θ);σ)(28)

A pictorial description of the fourier transform in (28)
is given by fig 6-b, which is expectedly a gaussian shifted by (f1cos(θ),f1sin(θ)). Note the black dot, which is deliberately added at (f1cos(θ),f1sin(θ)), to verify the correctness of the shift. Also please note that, since lambda=0.5

, the transform is elliptical.

fig-4,2D cosine function with varying f_1s

In fact if we plot the graph in the spatial domain, that also will be elliptical, as noted in the following figure, fig-4,2D cosine function with varying f_1s. You may wonder why, the eccentricity of the elliptical figure is reversed in the transform image when compared to the spatial image, this is because, the fourier transform of a gaussian function with a given σ=σ1
, is a differently scaled gaussian function with whose σ value is 1σ1

.
A bank of 2D gabor filter functions

Where are we heading? We need to come up with a bank of gabor filter functions, so that, effectively they cover, the entire transform space. This is shown as a rough outline in fig 6d below. fig-4,2D cosine function with varying f_1s

In order to achieve this varied set of gabor functions, we need to start playing around with these existing set of parameters σ,λ,f1,θ

and see how the gabor function changes. Later we will add a few more parameters.

Since we are just studying the effects of these parameters, let us continue to focus on the real part ge(x,y)

of this filter.

fig-3, real part of 2D gabor function with varying sigma-s In fig-7, we have plotted the real part of the gabor 2D filter with varying values of σ
and λ. Note that, as the λ-values vary, the eccentricities of the gaussian ellipse, changes, but nevertheless remains axially aligned. Also, we have kept f1=3 and θ=0

the same.

Let us now try varying f1
and θ. To illustrate this, just for the purpose of clarity, we are going to plot only the cosine function, ie cos(2πf1(xcos(θ)+ysin(θ)))

. Its effect on the modulation with gaussian function is self explanatory.

fig-4,2D cosine function with varying f_1s

You can see from fig-8, the changes in the frequency f1

, of the cosine wave.

Let us vary θ

now.

fig-4,2D cosine function with varying thetass

In all the considerations till now, the gaussian function was elliptical, but axially aligned. Intuitively, it would help to design better filter banks, if the gaussian function is tilted in the same manner as θ

. This can be accomplished by introducting a rotation transformation while computing the gaussian function.

fig-5,2D rotation of axes

The above rotation can be accomplished by the following co-ordinate transform,
R[x′y′]==[cos(θ)−sin(θ)sin(θ)cos(θ)]R[xy](29)(30)

fig-6,2D cosine function with varying rotation around axes Shown in figure 12, above is the real part of the 2D gabor function with the effect of the gaussian function rotated by the above transformation given in (29)

.

Another parameter that we can introduce is a phase factor ϕ
in the sinusoidal component, which becomes, exp(i2πf1(xcos(θ)+ysin(θ)+ϕ))

. The cosine part of this sinusoidal function (ie the real part) is plotted below as fig 12. fig-5,2D rotation of axes

Putting all these together, the gabor kernel is defined as
x′y′g(x,y)===xcos(θ)+ysin(θ)−xsin(θ)+ycos(θ)12πλσ2exp(−((x′λ)2+y′2)2σ2) exp(i2πf1(x′+ϕ))(31)(32)(33)

(105)
gives the fourier transform of such a gabor function described in (31). Shown below is the absolute value of the fourier transform of such an example gabor function, with σx=0.25,σy=0.125,u1=2,u2=4 and α=π2. Note that the spectrum is still an axially aligned ellipse and is shifted to u1=2,v1=4. Please disregard the axis lines drawn. Also, we have added a black dot to the transform image at the frequency (2,4)

, to signify and verify the correctness of the shift. fig-6,2D cosine function with varying phase
Appendix
Derivation of fourier transform of a 1-D gaussian function.

How do we find the fourier transform F(h(t))=H(f)
of a one dimensional gaussian function h(t)

?

For a general function p(t)
, the fourier transform F(p(t))=P(f) is given by (2)

.

On a simpler note, let us work on a simple function h(t)=e−at2
and try to find its fourier transform H(f)

.
H(f)====∫∞−∞h(t)e−i2πftdt∫∞−∞e−at2e−i2πftdt∫∞−∞e−at2(cos(2πft)−i.sin(2πft))dt∫∞−∞e−at2cos(2πft)−i.∫∞−∞e−at2sin(2πft)dt(34)(35)(36)(37)

Please remember that for an odd function o(t)
, ∫0−∞o(t)=−∫∞0o(t) and so ∫∞−∞o(t)=0

.

Since e−at2
is an even function and sin(2πft) is an odd function, ∫∞−∞e−at2sin(2πft)=0

.

So the above equation simplifies to
H(f)==∫∞−∞e−at2cos(2πft) dt2∫∞0e−at2cos(2πft) dt(38)(39)

Using [1], Abramovitz et. al., ∫∞0e−at2cos(2xt) dt=12πa−−√e−x2a

. So the above equation translates to,
H(f)=πa−−√e−π2f2a(40)

Putting a=12σ2
, in (40), fourier transform H(w) of h(t) in (1)

is,
H(f)==12π−−√σ2π−−√σe−2π2f2σ2e−2π2f2σ2(41)(42)
Derivation of fourier transform of a 2D gaussian function.

A 2D gaussian function is given by (43)
h(x,y)=12πσxσye−12(x2σ2x+y2σ2y)(43)

Note that (43)
can be written as, h1(x)h2(y)h(x,y)===12π−−√σxe−0.5x2σ2x12π−−√σye−0.5y2σ2yh1(x)h2(y)(44)(45)(46)

Given any 2D function p(x,y)
, its fourier transform F(p(x,y)=P(u,v)

is given by
P(u,v)=∫∞−∞∫∞−∞p(x,y)e−i2π(ux+vy) dxdy(47)

A 2D function p(x,y)
is separable, if it can be written as p(x,y)=p1(x).p2(y). If P1(u) and P2(v) are the fourier transforms of p1 and p2

respectively, then,
P(u,v)===∫∞−∞∫∞−∞p1(x)p2(y)e−i2π(ux+vy) dxdy∫∞−∞∫∞−∞p1(x)e−i2πuxdx p2(y)e−i2πvydyP1(u)P2(v)(48)(49)(50)

From (44)
, (48), and (41), we derive the fourier transform F(h(x,y))=H(u,v)

of a gaussian as,
H(u,v)=e−2π2(u2σ2x+v2σ2y)(51)
Derivation of fourier transform of sine and cosine functions

Consider a simple cosine and a sine function, c(t)
and s(t) respectively, what would be their fourier transforms F(c(t))=C(f) and F(s(t))=S(f)

?
c(t)==cos(2πf1t)12(exp(−i2πf1t)+exp(i2πf1t))(52)(53)
s(t)==sin(2πf1t)i2(e−i2πf1t−ei2πf1t)(54)(55)

From (52)

,
C(f)===∫∞−∞c(t)e−i2πftdt∫∞−∞12(e−i2πf1t+ei2πf1t)e−i2πftdt∫∞−∞12(e−i2π(f+f1)t+e−i2π(f−f1)t)dt(56)(57)(58)

Consider the integral ∫∞−∞e−i2πftdt
, That is the fourier transform I(f) of the identity function i(t)=1

.

The fourier inversion theorem states the following, if P(f)=∫∞−∞e−i2πftp(t) dt
, then ∫∞−∞ei2πfxP(f)df=p(x)

. For a proof, please see [2], Proof of Fourier inversion theorem

Now considering, the dirac delta function δ(t)
with the property ∫∞−∞δ(t−a)p(t)=p(a), the integral below, evaluates to 1 or the identity function i(x)

.
∫∞−∞ei2πfxδ(f)df==1i(x)(59)(60)

Applying the fourier inversion theorem, (59)

translates to
∫∞−∞e−i2πfxi(x)dx=δ(f)(61)

So (56)

can be continued as,
C(f)==∫∞−∞12(e−i2π(f+f1)t+e−i2π(f−f1)t)dt12(δ(f+f1)+δ(f−f1))(62)(63)

Similarly, from (54)
, fourier transform S(f)of sine function s(t)=sin(2πf1t)

is given by,
S(f)=i2(δ(f+f1)−δ(f−f1))(64)
Fourier transform of a rotated 2D signal

Let F(p(x,y))=P(u,v)
. Consider the rotation given in (29)

, and shown in fig 10.
R[x′y′]==[cos(θ)−sin(θ)sin(θ)cos(θ)]R[xy](65)(66)

Another way to express this relationship is x′
ad y′ are functions of x,y

given by,
x′(x,y)y′(x,y)==xcos(θ)+ysin(θ)−xsin(θ)+ycos(θ)(67)(68)

Similarly, x
ad y are functions of x′,y′ given by, x(x′,y′)y(x′,y′)==x′cos(θ)−y′sin(θ)x′sin(θ)+y′cos(θ)(69)(70)

Please note the following identity for taking derivatives for transformations,

dxdy===∣∣∣∣∂x∂x′∂y∂x′∂x∂y′∂y∂y′∣∣∣∣dx′dy′∣∣∣cos(θ)sin(θ)−sin(θ)cos(θ)∣∣∣dx′dy′dx′dy′(71)(72)(73)
If we set, u′v′==ucos(θ)+ysin(θ)−usin(θ)+ycos(θ)(74)(75)

By (47)
, (71) and (74), and if we denote q(x,y)=p(x′(x,y),y′(x,y)), the the corresponding fourier transform F(q(x,y))=Q(u,v)

is given by,
Q(u,v)======∫∞−∞∫∞−∞p(x′,y′) exp(−i2π(ux+vy)) dxdy∫∞−∞∫∞−∞p(x′,y′) exp(−i2π(ux′cos(θ)−uy′sin(θ)+vx′sin(θ)+vy′cos(θ))) dxdy∫∞−∞∫∞−∞p(x′,y′) exp(−i2π(ux′cos(θ)+vx′sin(θ)−uy′sin(θ)+vy′cos(θ))) dxdy∫∞−∞∫∞−∞p(x′,y′) exp(−i2π(u′x′+v′y′) dxdy∫∞−∞∫∞−∞p(x′,y′) exp(−i2π(u′x′+v′y′) dx′dy′P(u′,v′)(76)(77)(78)(79)(80)(81)

This means that, fourier transform Q(u,v)
of a rotated signal q(x,y)=p(x′(x,y),y′(x,y)), is the fourier transform P(u′(u,v),v′(u,v)) which will be the fourier transform P(u,v) after a rotation of θ

, as shown in the figure below.

fig-4,2D cosine function with varying f_1s
Derivation of fourier transform of a 2D gabor function.

Since there are several variants of the 2D functions mentioned in this article, let us first focus on the most basic of these, as described in (21)

.
fourier transform of simple 2D gabor function given in (21)

From (21)

,
g(x,y)Let g1(x)and g2(y)then, g(x,y)=====ge(x,y)+igo(x,y)12πσxσy exp(−12(x2σ2x+y2σ2y)) exp(i2π(u1x+v1y))12π−−√σx exp(−x22σ2x) exp(i2πu1x)12π−−√σy exp(−y22σ2y) exp(i2πv1y)g1(x) g2(y)(82)(83)(84)(85)(86)

So by the separability feature of fourier transform as shown in (48)
and by (18), the fourier transform F(g(x,y))=G(u,v) of a 2D gabor function given in (82)

is,
G(u,v)==G1(u) G2(v)H(u−u1)H(v−v1)(87)(88)

Note that H(u−u1)
is F(h(t)) of the gaussian h(t), translated to the frequency u1

.

Now let us move to more general and parametric forms of the 2D gabor function.
fourier transform of 2D gabor function (with λ
and θ
parameters) as described in (27)

We will be working with (27)

.

The fourier transform of the 1D gaussian function F(h(t))=H(f)
, can be expressed moe accurately with the parameter σ as H(f;σ)

.

So we can rewrite (41)

as
H(f;σ)=exp(−2π2f2σ2)(89)

From (27)
g(x,y)Let g1(x)and g2(y)g(x,y)====12πλσ2exp(−((xλ)2+y2)2σ2) exp(i2πf1(xcos(θ)+ysin(θ)))12π−−√λσexp(−x22(λσ)2) exp(i2πf1xcos(θ))12π−−√σexp(−y22σ2) exp(i2πf1ysin(θ))g1(x) g2(y)(90)(91)(92)(93)

So again by the separability feature of fourier transform as shown in (48)
and by (18) , F(g(x,y))

will translate to
G(u,v)=H(u−f1cos(θ);λσ) H(v−f1sin(θ);σ)(94)
fourier transform of 2D gabor function (with λ
, θ
and rotated gaussian)

The most generalized form of the 2D gabor function was given by (31)

, which is reproduced below,
g(x,y)=12πλσ2exp(−((x′λ)2+y′2)2σ2) exp(i2πf1(x′+ϕ))

Let us try to come up with a formula for its fourier transform F(g(x,y)=G(u,v)

.

Consider the function, p(x,y)=12πλσ2exp(−((xλ)2+y2)2σ2) exp(i2πf1(x+ϕ))
in (95)

,

p(x,y)p1(x)p2(y)p(x,y)====12πλσ2exp(−((xλ)2+y2)2σ2) exp(i2πf1(x+ϕ))12π−−√λσexp(−x22(λσ)2) exp(i2πf1x)12π−−√σexp(−y22σ2)p1(x) p2(y) exp(i2πf1ϕ)(95)(96)(97)(98)
Note that g(x,y)=p(x′(x,y),y′(x,y)). Here we used the notation in (67) that x′, and y′ are functions of x and y

.

The fourier transform F(p(x,y)=P(u,v)

derived below.

Due to the separability feature of the fourier transform, we have,
P(u,v)=H(u−f1;λσ) H(v;σ) exp(i2πf1ϕ)(99)
G(u,v)u′v′=====F(g(x,y))F(p(x′(x,y),y′(x,y)))P(u′,v′) as in (76) whereucos(θ)+vsin(θ)−usin(θ)+vcos(θ)(100)(101)(102)(103)(104)

Finally we have,
G(u,v)=H(u′−f1;λσ) H(v′;σ) exp(i2πf1ϕ)(105)
References

    Abramowitz, M. and Stegun, I. A. (Eds.). Handbook of Mathematical Functions with Formulas, Graphs, and Mathematical Tables, 9th printing. New York: Dover, p. 302,

    [Proof of Fourier inversion theorem] (http://math.columbia.edu/~nsnyder/tutorial/lecture3.pdf)

    ← Previous
    Archive
    Next →

blog comments powered by Disqus
Published
04 February 2016
Tags

    image processing 1
    fourier transform 1
    convolution 1
    signal processing 1
    feature extraction 1

© Koshy George 2012 with help from Jekyll Bo
