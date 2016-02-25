---
title       : Adapting DIGR for Coaching
subtitle    : (Or 'Using Stats to Make More Effective Practice Plans')
author      : Tommy O'Brien
job         : OCS Goaltending
logo        : OCSlogo_dark.png
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax,bootstrap]# {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Motivation (Or 'Why Am I Reading This?')
The simple answer is because you want your goalie to be better, but you aren't a goalie coach (or you are and your goalie isn't getting better).

<div style="background-color: #D8D8D8; margin-left: 20px; margin-right: 20px; padding-bottom: 8px; padding-left: 8px; padding-right: 8px; padding-top: 8px; outline: #000000 solid thick; width: 400px";>
<font color=#8A0808 size='4'><b>Can't I Just Hire A Goalie Guy?</b></font>
</div>
<p><font size='3'>
Yes. Yes you can. Here's our <a href='http://www.ocsgoaltending.com/about-us.html'>contact page</a>. But in all seriousness, we believe that first and foremost, a goalie should be his own best coach. The idea behind the approach we're presenting is to teach them (and you, and whatever goalie guy you have).
</font></p>

<div style="background-color: #D8D8D8; margin-left: 20px; margin-right: 20px; padding-bottom: 8px; padding-left: 8px; padding-right: 8px; padding-top: 8px; outline: #000000 solid thick; width: 400px">
<font color=#8A0808 size='4'><b>What Do You Mean DIGR? Or Even 'Stats'?</b></font>
</div>
<p><font size='3'>
For now, don't worry about what DIGR is specifically, just know that its an advanced statistic in the goalie world. If you don't know what I mean by advanced statistics, you obviously need to play more <a url='http://sports.yahoo.com/fantasy/'>fantasy sports</a>.
</font></p>

<div style="background-color: #D8D8D8; margin-left: 20px; margin-right: 20px; padding-bottom: 8px; padding-left: 8px; padding-right: 8px; padding-top: 8px; outline: #000000 solid thick; width: 400px">
<font color=#8A0808 size='4'><b>Aren't Stats for Evaluation, Not Development?</b></font>
</div>
<p><font size='3'>
Of course they are. Goalies are evaluated using <a href='http://www.nhl.com/stats/'>basic stats</a> and even some <a href='http://www.rosterresource.com/nhl-goalie-power-rankings/'>advanced ones</a>. The point here is to dive into how the stats are calculated and use that process to gain insight into a goalie's strengths and weaknesses. The final stats themselves don't do much for us (unless you want to pay us for scouting, in which case they're our specialty.) 
</font></p>

---

## What is DIGR?
Defense-Independent Goaltender Rating (DIGR) is an attempt to rank goalies that accounts for the strength of their team's defense. A very nice paper from the MIT Sloan Conference can be found <a url='http://www.sloansportsconference.com/wp-content/uploads/2011/08/DIGR-A-Defense-Independent-Rating-of-NHL-Goaltenders-using-Spatially-Smoothed-Save-Percentage-Maps.pdf'>here</a> (Poster version <a url='http://www.sloansportsconference.com/wp-content/uploads/2011/08/50-Michael-Schuckers2.pdf'>here</a>).

## How does is work?
1. Divide shots faced by each goaltender into bins (e.g. by location or type)
2. Use league-wide shot data to find the 'average' fraction of shots a goalie faces in each bin
3. Use goalie's shot data to find his/her save percentage for each bin
4. Compare how goalie would do against an 'average' shot distribution

## The Math...
While the stat is mostly intuitive, there is some simple math. If math gives you nightmares, but you want to help your goalie despite your shortcomings, gird your loins...

--- &twocol

## Deriving DIGR
We will use Dr. Schucker's notation when its convenient, but usually we won't (sorry Dr. Schuker...'E' is hard to associate with 'Shots'). Let $N$ be the number of shots, $S$ be the number of saves, and $b$ be the bin that a certain shot falls into.
*** =left
<div style="background-color: #D8D8D8; margin-left: 20px; margin-right: 20px; padding-bottom: 8px; padding-left: 8px; padding-right: 8px; padding-top: 8px; outline: #000000 solid thick;">
<font color=#8A0808><b>Recast the Save Pct</b></font>
<font size='4'>
$$\begin{aligned}
SV\% &= \frac{S}{N} \nonumber \\
     &= \sum_{b} \frac{S(b)}{N} \nonumber \\
     &= \sum_{b} \frac{S(b)}{N(b)}\frac{N(b)}{N} \nonumber \\
     &\equiv \sum_b \delta(b) \Gamma(b)
\end{aligned}$$
</font>
</div>

*** =right
<div style="background-color: #8A0808; margin-left: 20px; margin-right: 20px; padding-bottom: 8px; padding-left: 8px; padding-right: 8px; padding-top: 8px; outline: #000000 solid thick;">
<font color=#FFFFFF><b>Think about what you just did</b></font>
</div><br>

<font size='4'>We just defined two variables that give a tremendous amount of insight into a goaltender's game (and it took only a few lines and that time-honored tradition in math of multiplying by 1)
</font>

<p><br>
<div style="background-color: #F3F781; margin-left: 20px; margin-right: 20px; padding-bottom: 8px; padding-left: 8px; padding-right: 8px; padding-top: 8px;">
$\delta(b)$ : save percentage of goalie for a $particular$ shot bin
</div>

<div style="background-color: #F3F781; margin-left: 20px; margin-right: 20px; padding-bottom: 8px; padding-left: 8px; padding-right: 8px; padding-top: 8px;">
$\Gamma(b)$ : the fraction of shots a goalie faces from a particular bin
</div>
</p>

--- &twocol

## Finishing with DIGR

Now replace $\Gamma(b)$ with $\overline{\Gamma(b)}$, where the bar means 'league average'. Maybe you've seen it in that math class you took 20 years ago as $<\Gamma(b)>$.

<p>
<div style="background-color: #F3F781; margin-left: 20px; margin-right: 20px; padding-bottom: 8px; padding-left: 8px; padding-right: 8px; padding-top: 8px;">
\begin{equation}
DIGR = \sum_b \delta(b) \overline{\Gamma(b)}
\end{equation}
</div>
<p>

*** =left
<div style="background-color: #D8D8D8; margin-left: 20px; margin-right: 20px; padding-bottom: 8px; padding-left: 8px; padding-right: 8px; padding-top: 8px;">
<font color=#8A0808><b>Great. Now What?</b></font>
</div><p><br></p>

<div style="margin-left: 20px; margin-right: 20px; padding-bottom: 8px; padding-left: 8px; padding-right: 8px; padding-top: 8px;">
<p>
The best way to see what this tells us about our (your) goalie is to run through an example calculation. We will use <a href='https://www.r-project.org/'>R</a> for this.
</p>
</div>


*** =right
<div style="background-color: #D8D8D8; margin-left: 20px; margin-right: 20px; padding-bottom: 8px; padding-left: 8px; padding-right: 8px; padding-top: 8px;">
<font color=#8A0808><b>What Did We Need?</b></font>
</div>

<p><br>
1. Each shot with any bin data you want <br>
2. A unemployed friend to take said data
</p>

---

## Example (Part I: Get and Check Data)

Read all the shots from around the [four team example] league and check the format. Note that the dataset is included with the code to this presentation and is hosted on our gitHub if you feel so inclined.

```r
shotData <- read.csv('code/SlidifyDatabase.csv',header=T,sep=",")
head(shotData,n=2)  #This is a comment. Print out the first two rows.
```

```
##   Goaltender     IceX     IceY Save
## 1      Brown 49.19338 25.08911   No
## 2      Brown 59.84767 47.98779  Yes
```
Each shot in this database seems to have an X,Y location it was taken from on the ice as well as the goalie who saved (or didn't save) it. It would be helpful to know how many shots we have and how many goalies they are distributed across.

---

## Example (Part I: Get and Check Data) Cont'd

There's a long way to do this...

```r
dim(shotData)[1] #dim() returns [rows,cols]. [1] gives just [rows]
```

```
## [1] 1728
```

```r
unique(shotData$Goaltender) #unique goalie names
```

```
## [1] Brown   Smith   Jones   Johnson
## Levels: Brown Johnson Jones Smith
```

---

## Example (Part I: Get and Check Data) Cont'd 

And a short way (if you're into that stuff)...

```r
aggregate(Save ~ Goaltender, data = shotData, FUN = length)
```

```
##   Goaltender Save
## 1      Brown  515
## 2    Johnson  245
## 3      Jones  511
## 4      Smith  457
```

Note that 'Save' here means the length of the 'Save' column, not the number of saves. The sum should be total number of shots. So it looks like there are four goalies and a total of 1728 shots. Neat. Let's move on.

---

<style>
.title-slide {
  background-color: #D8D8D8; /* #EDE0CF; ; #CA9F9D*/
}
.title-slide hgroup > h2 {
  color: #8A0808 ;  /* ; #EF5150*/
}
.title-slide hgroup > h1 {
  color: #2E2E2E;
}
slide:not(.segue) h2{
  font-family: 'Calibri', Arial, sans-serif;
  font-size: 52px;
  font-style: normal;
  font-weight: bold;
  text-transform: normal;
  letter-spacing: -2px;
  line-height: 1.2em;
  color: #8A0808;
}
</style>




