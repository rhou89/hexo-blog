---
layout: post
title: How rare is a palindromic day? (回文日期)
date: 2020-02-02
tags:
- Coding
- Math
categories:
- Popular Science
- [Computer Science, Coding]
---

Today is a special day called "palindromic day", as you may have seen in the news. A palindromic day is a day, whose date, when written in certain forms, is a palindromic number. 

<!-- more -->

We start with the definition of palindromic numbers from Wiki
> "A palindromic number is a number that remains the same when its digits are reversed".

Thus, 1221 or 12221 are both palindromic numbers. Those numbers also have a mirror/reflection symmetry in the sense that they have a symmetric center "12$\vert$21" or "12$\vert$2$\vert$21". This leads to the observation that if a number has odd numbers of digits, its symmetric center can ba arbitrary "12$\vert$n$\vert$21".

When it comes to days, the situation becomes more complicated as people have different conventions in recording dates. In the following, we use "YYYY", "MM" and "DD" to denote year, month and day. In general, there are three different forms, "YYYY-MM-DD", "DD-MM-YYYY" and "MM-DD-YYYY". Thus, today is a global palindromic day, meaning the date is a palindromic number in anyone of the above forms. This is of course, very rare and the previous one comes at 1111-11-11, about 909 years ago. Now, let's release the constraint and consider only [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) standard form "YYYY-MM-DD" to see how rare a palindromic day could be?

{% img "box px-0 py-0 ml-auto mr-auto" /gallery/Palindromic-day/Palindromic-day-BeatPattern.png 720 '"Beat pattern of palindromic days." "Beat pattern of palindromic days."' %}
<br>

<!-- <figure class="ampstart-image-with-heading  m0 relative mb4">
<amp-img src="{{site.url}}assets/images/2020-2-2-Palindromic-day-BeatPattern.png" width="656" height="400" layout="responsive" alt="" class="mb3"></amp-img>
<figcaption class="absolute right-0 bottom-0 left-0">
<header class="ampstart-image-heading px2 py2 line-height-4"><h1>Beat pattern of palindromic days.</h1></header>
</figcaption>
</figure> -->

If we consider year from 1 to 2020, there are less than 10^6 days. So, we can first use a program to help us to select the palindromic numbers. For such a small state space, we do not really need any pruning so I simply search with brute force.

```Mathematica
Year = Table[yr, {yr, 1, 2030}];
Month = Table[mo, {mo, 1, 12}];
Day = Table[dy, {dy, 1, 31}];
LongMonth = {1, 0, 1, 0, 1, 0, 1, 1, 0, 1, 0, 1};

SymDate = {};
SetSharedVariable[SymDate];

ParallelTable[
  yr = Year[[yri]];
  mo = Month[[moi]];
  dy = Day[[dyi]];
  
  CHK = True;
  
  If[LongMonth[[mo]] == 0 && dy == 31, CHK = False];
  If[mo == 2,
   If[LeapYearQ[yr] && dy >= 30, CHK = False];
   If[! LeapYearQ[yr] && dy >= 29, CHK = False];
   ];
  
  NowDate = 
   IntegerString[yr, 10] ~~ IntegerString[mo, 10, 2] ~~ 
    IntegerString[dy, 10, 2];
  Table[
   If[StringPart[NowDate, ii] != 
     StringPart[NowDate, StringLength@NowDate - ii + 1],
    CHK = False]
   , {ii, 1, StringLength@NowDate}];
  If[CHK, AppendTo[SymDate, NowDate]];
  , {yri, 1, Length@Year}, {moi, 1, Length@Month}, {dyi, 1, 
   Length@Day}];
   
YearCollect = 
  ToExpression[StringTake[#, {1, StringLength@# - 4}] & /@ SymDate];
MyHash = Table[0, {ii, 1, 2020}];
(MyHash[[#]]++) & /@ YearCollect;
ListPlot[MyHash, PlotRange -> All, Joined -> True, ImageSize -> 1500, 
 AspectRatio -> 0.1, Frame -> True, FrameLabel -> {"Year", "Count"}]
```
This is the Mathematica program I used to search for the dates and it returns the plot shown above (view in a new window to see the entire plot). The program is fairly easy and I don't explain it here. The most striking feature of the final plot is that it shows certain beat patterns, namely, there're some orders in palindromic days over the past thousands of years!

To take a closer look at the date, we split the days into 4 groups, "Y-MM-DD", "YY-MM-DD", "YYY-MM-DD" and "YYYY-MM-DD", corresponding to years 1-9, 10-99, 100-999 and 1000-2020. We note that the pattern changes within each group. For the first group, we can count the total of palindromic days using

```Mathematica
Select[Sort@ToExpression@SymDate, # <= 99999 &]
Length@%
```
which turns out to be 108. If we look at the beat pattern, we would find that it as 12 palindromic days in each year. This is easy to understand as each month has a palindromic day on xth for a given year x. When it comes to year 10-99, the total would much less since it has an even number of digits. It can be counted as (9)(3)=27 because for each digital x=1-9, we have x0-11-0x, x1-11-1x and x2-11-2x satisfy the requirements. Note that all those days happened in November and now we understand how those beat patterns form.

Applying similar counting processes (yet way more complicated), we could find the total of palindromic day for the other two groups, which are summarized in the following table, with their frequencies in the given time frame.

| Year    | 1-9   | 10-99  | 100-999 | 1000-2020 |
|---------|-------|--------|---------|-----------|
| Total   | 108   | 27     | 330     | 49        |
| Percent | 1200% | 30.34% | 36.71%  | 4.80%     |


Finally, the next palindromic day is 2021-12-02, happening next year. Following that it's 2030-03-02, which will be 10 year from now. So, palindromic day is indeed rare for our generation.

## Reference
- [CNN News](https://www.cnn.com/2020/02/02/world/palindrome-day-february-2-2020-intl-scli/index.html)
- [Palindromic number - Wiki](https://en.wikipedia.org/wiki/Palindromic_number)
- [Date format by country - Wiki](https://en.wikipedia.org/wiki/Date_format_by_country)
