---
title: Mathematica Tricks
date: 2016-10-12
tags: Coding
categories: [Computer Science, Coding]
---

This note records some useful tricks I learnt in the past years of using Mathematica (MMA). MMA provides a very powerful language system that realizes almost any functionality one would image. However, such a huge library means large learning cost.

Some exmaples are available in my [MMA Repository](https://github.com/ryanhau94/Mathamatica) and you can check there for more fun stuffs!

<!-- more -->

## Cracking word puzzles
Recently, when I was playing some word puzzles, I suddenly came to realize that I can take advantages of using programs to look up the dictionary with some given patterns. MMA does support this feature with a built-in function `DictionaryLookup[]`.

First, you can check if it supports a certain language by typing `DictionaryLookup[All]`.

Now, to search for word with specific pattern, e.g., English words starting with 'a' and ending with 'k' and have only 5 letters, you can just type

```Mathematica
Select[DictionaryLookup[{"English", "a" ~~ ___ ~~ "k"}], 
 StringLength[#] == 5 &]
```

Next, if you want to get a word using given letters and restrict its length to be 4, you could use

```Mathematica
StringJoin /@ 
 Select[Tuples[{"e", "a", "r", "t", "h"}, 4], 
  DeleteDuplicates[#] == # && 
    Length[DictionaryLookup[StringJoin[#]]] != 0 &]
```

Besides these, this function can be used for a lot fun thins! You can count the number of the words starting with 'a' to 'z'

`Length[DictionaryLookup[# ~~ ___]] & /@ CharacterRange["a", "z"]`

or find all the [palindromic words]({{site.url}}{{site.baseurl}}{{"Palindromic-day"}})

`DictionaryLookup[x__ /; x === StringReverse[x]]`

### Reference
- [Wolfram Documentation Center - "DictionaryLookup"](https://reference.wolfram.com/language/ref/DictionaryLookup.html)

## Numerical derivative of a list
In MMA, you may easily take partial derivative using `D[f(x), x]` or even the total derivative `Dt[f(x), x]`. However, most models I encountered in researches are not analytic so that the functions are usually stored as an array $f(x_i)$, where $x_i$ is an array of discrete points. I've searched on [stackoverflow](https://stackoverflow.com/questions/6502440/numerical-differentiation-of-list-in-mathematica), [stackExchange](https://mathematica.stackexchange.com/questions/15262/how-do-i-plot-the-derivative-of-a-set-of-experimental-points) and [Wolfram Community](https://community.wolfram.com/groups/-/m/t/275096), but I never found a satisfactory solution. Thus, I have to write another subroutine myself to realize this functionality for the past years. Recently, I came across to the function `DerivativeFilter` and finally, it works! To take $n$/$m$-th order derivative with respect to $x$/$y$, you just type

`DerivativeFilter[array, {n,m}]`,

where the array should be 2D here. The function applies to any array or even image!

### Reference
- [Wolfram Documentation Center - "DerivativeFilter"](https://reference.wolfram.com/language/ref/DerivativeFilter.html)

## fftshift in MMA
As I have to deal with wave functions, it is common for me to work between real/momentum spaces, which are connected through Fourier transform. I was so spoiled by `fftshift` in MatLab so I didn't know what to do when I cannot find a similar function in MMA. In fact, this can be easily realized through

```Mathematica
(*wfx is an array representing the wave function in real space*)
wfk = Fourier[wfx, FourierParameters->1];
wfk = RotateRight[wfx, Floor[(Length@wfk-1)/2]]
```
Now, the zero momentum component has been shifted to the center! Why this works? Check out [DFT](https://en.wikipedia.org/wiki/Discrete_Fourier_transform) and [FFT](https://en.wikipedia.org/wiki/Fast_Fourier_transform) on wiki (or the last two reference if you read Chinese).

### Reference
- [Equivalent to Matlab fftshift in Mathematica](https://community.wolfram.com/groups/-/m/t/259229)
- [MATALAB中的fft、fftshift相关原理说明](https://blog.csdn.net/haoaoweitt/article/details/83012477)
- [FFT算法讲解——麻麻我终于会FFT了！](https://blog.csdn.net/WADuan2/article/details/79529900?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)
