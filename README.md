
<html lang="en">

<head>

<meta charset="iso-8859-1">

<meta http-equiv="X-UA-Compatible" content="IE=edge">

<meta name="viewport" content="width=device-width, initial-scale=1">

<meta name="format-detection" content="telephone=no">

<title>

stata tutorials

</title>

<style>
html { -webkit-text-size-adjust: 100%; }
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 14px; line-height: 1.428;
  max-width: 1000px;
  margin: 0 auto; padding: 0 15px;
}
h1, h2, h3, h4, h5, h6 { margin: 20px 0 10px; }
h1 { font-size: 28px; } h2 { font-size: 24px; }
h3 { font-size: 18px; } h4 { font-size: 16px; }
h5 { font-size: 14px; } h6 { font-size: 12px; }
a { color: #337AB7; text-decoration: none; }
a:hover { text-decoration: underline; }
img { max-width: 100%; height: auto; }
ul, ol { padding-left: 30px; }
pre, code, samp {
  font-size: 13px;
  font-family: Courier, monospace;
}
code, samp {
  background-color: #F5F5F5;
  border-radius: 3px; padding: 3px;
}
pre code, pre samp {
  white-space: pre; background: transparent;
  border: none; padding: 0;
}
pre {
  line-height: 1.33; background-color: #F5F5F5;
  border: 1px solid #CCCCCC; border-radius: 3px;
  padding: 8px; overflow: auto;
}
</style>

<style>
.stlog { color: #000000; background-color: #F0F3F9; }
.stres { color: #324F58; }
.stinp { font-weight: bold; color: #000000; }
.stcmd .stcmt { font-style: italic; opacity: 0.5; }
.stlog .stcmt { font-style: italic; opacity: 0.5; }
.stoom, .stcnp { font-style: italic; }
@media screen { .stcnp { display: none; }}
</style>

</head>

<body>

<h1>

Handling Data with stata.

</h1>

<p>

STATA offers high profile data management capabilities which can be
usefull for anay data analyst.In this tutorial we are going to handle
various ways we can use to solve problems relating data.

</p>

<h4>

Contents

</h4>

<div class="toc">

<ul>

<li>

<a href="#h-1"><span class="toc-secnum">1 </span> Getting the data into
the stata working session.</a>

</li>

<li>

<a href="#h-2"><span class="toc-secnum">2 </span> Viewing the
dataset.</a>

</li>

<li>

<a href="#h-3"><span class="toc-secnum">3 </span> Dataset Structure.</a>

</li>

<li>

<a href="#h-4"><span class="toc-secnum">4 </span> Selecting
Observations</a>

<ul>

<li>

<a href="#h-4-1"><span class="toc-secnum">4.1 </span> The
<code>in</code> method</a>

</li>

<li>

<a href="#h-4-2"><span class="toc-secnum">4.2 </span> Selecting Data by
condition <CODE>if</CODE></a>

</li>

</ul>

</li>

<li>

<a href="#h-5"><span class="toc-secnum">5 </span> Missing Data</a>

</li>

<li>

<a href="#h-6"><span class="toc-secnum">6 </span> Descriptive
Statistics</a>

</li>

<li>

<a href="#h-7"><span class="toc-secnum">7 </span> Merging datasets</a>

</li>

<li>

<a href="#h-8"><span class="toc-secnum">8 </span> Dropping variables and
observations.</a>

<ul>

<li>

<a href="#h-8-1"><span class="toc-secnum">8.1 </span> Variables</a>

</li>

<li>

<a href="#h-8-2"><span class="toc-secnum">8.2 </span> Observations.</a>

</li>

<li>

<a href="#h-8-3"><span class="toc-secnum">8.3 </span> Using keep.</a>

</li>

</ul>

</li>

</ul>

</div>

<h2 id="h-1">

<span class="heading-secnum">1 </span> Getting the data into the stata
working session.

</h2>

<P>

For a faster view into how to ingest data into stata you can
<a href="#"> see this post</a>.As for this one I will quickly ingest
system data here quickly.

</P>

<pre id="stlog-1" class="stlog"><samp><span class="stinp">. sysuse auto.dta,clear</span>
(1978 Automobile Data)
</samp></pre>

<h2 id="h-2">

<span class="heading-secnum">2 </span> Viewing the dataset.

</h2>

<p>

In STATA once you have loaded your dataset you can get a view of your
dataset by running the <code>list</code> comand.Further you can specify
how many rows by adding <code>in 1/number of rows</code> comand where
the number of rows us an integer representing the number of
observations.

</p>

<pre id="stlog-2" class="stlog"><samp><span class="stinp">. list in 1/5 <span class="stcmt">//lists the first five rows of data</span></span>

     +------------------------------------------------------------------------------------------------------------------+
     | <span class="stres">make            price   mpg   rep78   headroom   trunk   weight   length   turn   displa~t   gear_r~o    foreign </span>|
     |------------------------------------------------------------------------------------------------------------------|
  1. | <span class="stres">AMC Concord     4,099    22       3        2.5      11    2,930      186     40        121       3.58   Domestic </span>|
  2. | <span class="stres">AMC Pacer       4,749    17       3        3.0      11    3,350      173     40        258       2.53   Domestic </span>|
  3. | <span class="stres">AMC Spirit      3,799    22       .        3.0      12    2,640      168     35        121       3.08   Domestic </span>|
  4. | <span class="stres">Buick Century   4,816    20       3        4.5      16    3,250      196     40        196       2.93   Domestic </span>|
  5. | <span class="stres">Buick Electra   7,827    15       4        4.0      20    4,080      222     43        350       2.41   Domestic </span>|
     +------------------------------------------------------------------------------------------------------------------+
</samp></pre>

<p>

The <code>browse</code> and <code>edit</code> commmands can also be used
to to open an interactive data viewing and editing modes respectively in
stata pop up windows.

</p>

<pre>
browse //<i>opens stata data browser window</i>
edit // <i>opens stata data editor window</i>
</pre>

<P>

Also note that in the data editor window you can rename your variable.

</P>

<h2 id="h-3">

<span class="heading-secnum">3 </span> Dataset Structure.

</h2>

<p>

For a quick glimpse into the dataset structure you can run the
<code>describe</code> command.This gives you information on how
variables are stored in STATA

</p>

<pre id="stlog-3" class="stlog"><samp><span class="stinp">. describe</span>

Contains data from <span class="stres">C:\Program Files (x86)\Stata13\ado\base/a/auto.dta</span>
  obs:<span class="stres">            74                          1978 Automobile Data</span>
 vars:<span class="stres">            12                          13 Apr 2013 17:45</span>
 size:<span class="stres">         3,182                          (_dta has notes)</span>
-----------------------------------------------------------------------------------------------------------------------------------------------------------
              storage   display    value
variable name   type    format     label      variable label
-----------------------------------------------------------------------------------------------------------------------------------------------------------
<span class="stres">make           </span> str18   %-18s                 <span class="stres">Make and Model</span>
<span class="stres">price          </span> int     %8.0gc                <span class="stres">Price</span>
<span class="stres">mpg            </span> int     %8.0g                 <span class="stres">Mileage (mpg)</span>
<span class="stres">rep78          </span> int     %8.0g                 <span class="stres">Repair Record 1978</span>
<span class="stres">headroom       </span> float   %6.1f                 <span class="stres">Headroom (in.)</span>
<span class="stres">trunk          </span> int     %8.0g                 <span class="stres">Trunk space (cu. ft.)</span>
<span class="stres">weight         </span> int     %8.0gc                <span class="stres">Weight (lbs.)</span>
<span class="stres">length         </span> int     %8.0g                 <span class="stres">Length (in.)</span>
<span class="stres">turn           </span> int     %8.0g                 <span class="stres">Turn Circle (ft.)</span>
<span class="stres">displacement   </span> int     %8.0g                 <span class="stres">Displacement (cu. in.)</span>
<span class="stres">gear_ratio     </span> float   %6.2f                 <span class="stres">Gear Ratio</span>
<span class="stres">foreign        </span> byte    %8.0g      origin     <span class="stres">Car type</span>
-----------------------------------------------------------------------------------------------------------------------------------------------------------
Sorted by:  <span class="stres">foreign</span>
</samp></pre>

<P>

We can see that the data has 74 observations and 12 features.The
variable names ate also given and their labels alongside storage types.

</P>

<p>

For a more refined detail about the dataset you are working with in
stata ,<code>codebook</code> can be of great help in stata.When followed
with a specific variable name the codebook returns infomation only
concerning the variable else all

</p>

<pre id="stlog-4" class="stlog"><samp><span class="stinp">. codebook price </span>

-----------------------------------------------------------------------------------------------------------------------------------------------------------
<span class="stres">price                                                                                                                                                 Price</span>
-----------------------------------------------------------------------------------------------------------------------------------------------------------

                  type:  numeric (<span class="stres">int</span>)

                 range:  [<span class="stres">3291</span>,<span class="stres">15906</span>]                 units:  <span class="stres">1</span>
<span class="stres">         </span>unique values:  <span class="stres">74                       </span>missing .:  <span class="stres">0</span>/<span class="stres">74</span>

                  mean:<span class="stres">   6165.26</span>
              std. dev:<span class="stres">    2949.5</span>

           percentiles:        10%       25%       50%       75%       90%
<span class="stres">                              3895      4195    5006.5      6342     11385</span>
</samp></pre>

<h2 id="h-4">

<span class="heading-secnum">4 </span> Selecting Observations

</h2>

<h3 id="h-4-1">

<span class="heading-secnum">4.1 </span> The <code>in</code> method

</h3>

<p>

In stata we are able to select observations using the <code>in</code>
method which specifies the number of observations we need in a given
range.

</p>

<p>

For example.

</p>

<pre id="stlog-5" class="stlog"><samp><span class="stinp">. list price in 40/45 </span>

     +--------+
     | <span class="stres"> price </span>|
     |--------|
 40. | <span class="stres"> 4,195 </span>|
 41. | <span class="stres">10,371 </span>|
 42. | <span class="stres"> 4,647 </span>|
 43. | <span class="stres"> 4,425 </span>|
 44. | <span class="stres"> 4,482 </span>|
     |--------|
 45. | <span class="stres"> 6,486 </span>|
     +--------+
</samp></pre>

<p>

Lists 40<sup>th</sup> to 45<sup>th</sup> observations in the price
variable in our dataset.In case of negative numbers STATA will return
observations from the end.

</p>

<p>

The <code>in</code> keyword can also accept leters for example if you
are intrested of viewing the last 5 (tail) observations of your dataset
you can just tipe the code below.

</p>

<pre id="stlog-6" class="stlog"><samp><span class="stinp">. list in -5/L</span>

     +----------------------------------------------------------------------------------------------------------------+
     | <span class="stres">make           price   mpg   rep78   headroom   trunk   weight   length   turn   displa~t   gear_r~o   foreign </span>|
     |----------------------------------------------------------------------------------------------------------------|
 70. | <span class="stres">VW Dasher      7,140    23       4        2.5      12    2,160      172     36         97       3.74   Foreign </span>|
 71. | <span class="stres">VW Diesel      5,397    41       5        3.0      15    2,040      155     35         90       3.78   Foreign </span>|
 72. | <span class="stres">VW Rabbit      4,697    25       4        3.0      15    1,930      155     35         89       3.78   Foreign </span>|
 73. | <span class="stres">VW Scirocco    6,850    25       4        2.0      16    1,990      156     36         97       3.78   Foreign </span>|
 74. | <span class="stres">Volvo 260     11,995    17       5        2.5      14    3,170      193     37        163       2.98   Foreign </span>|
     +----------------------------------------------------------------------------------------------------------------+
</samp></pre>

<h3 id="h-4-2">

<span class="heading-secnum">4.2 </span> Selecting Data by condition
<CODE>if</CODE>

</h3>

<p>

This is used in cases where a dataset needs to be split into multiple
files.Lets say you want to devide the dataset into two groups namely
foreign or domestic or if its demographic data and you want males and
females separated.

</p>

<p>

Lets see miles per galon of the domestic cars that have a price greater
than 15000 .

</p>

<pre id="stlog-7" class="stlog"><samp><span class="stinp">. list mpg if foreign == 0 &amp; price &gt; 12000</span>

     +-----+
     | <span class="stres">mpg </span>|
     |-----|
 12. | <span class="stres"> 14 </span>|
 13. | <span class="stres"> 21 </span>|
 27. | <span class="stres"> 12 </span>|
 28. | <span class="stres"> 14 </span>|
     +-----+
</samp></pre>

<p>

Only four cars meet the condition set above.The & opperator makes stata
to check if both conditions are met then scrapes off the data that
satisfies it.Its important to note that in this dataset ,the label
domestic was coded 0 and 1 for foreign.

</p>

<h2 id="h-5">

<span class="heading-secnum">5 </span> Missing Data

</h2>

To check any missing data in stata ,we can run the <code>if
missing</code> comand as shown below.

<pre id="stlog-8" class="stlog"><samp><span class="stinp">. list if missing()</span>
</samp></pre>

We can see that there is no missing information from the data above.

Within the missing parentheses ,a particular variable can be added to
specify where the missing data is being sought.

Also before the missing <code>if</code> command,a list of variable can
be specified.

<pre id="stlog-9" class="stlog"><samp><span class="stinp">. list mpg rep78 trunk if missing(gear_ratio)</span>
</samp></pre>

The code above tells stata to return observations in the mpg,rep and
trunk variables where missing values are found.

<h2 id="h-6">

<span class="heading-secnum">6 </span> Descriptive Statistics

</h2>

So what information is comtained in that dataset you are using?To get a
quick glimpse of the summary statistics,You can run the
<code>summary</code> command in the console.

The summary command can be specified with a variable/variables infront
of it,to summarize all the variables,it should be left empty.

Note also that the summarize command can be shortened as sum and still
the summary is gotten.

<pre id="stlog-10" class="stlog"><samp><span class="stinp">. summarize rep78 foreign</span>

    Variable |       Obs        Mean    Std. Dev.       Min        Max
-------------+--------------------------------------------------------
       rep78 |<span class="stres">        69    3.405797    .9899323          1          5</span>
     foreign |<span class="stres">        74    .2972973    .4601885          0          1</span>
</samp></pre>

<h2 id="h-7">

<span class="heading-secnum">7 </span> Merging datasets

</h2>

To merge datsets ,we call the <code>merge</code> command and specify
which columns to use for merging.

Merge has so many options to choose from.

<ol type="a">

<li>

One-to-one merging;

</li>

<li>

Many-to-one merging

</li>

<li>

One-to-many merging

</li>

<li>

Many-to-many merging

</li>

<li>

One-to-one merging by specified observation

</li>

</ol>

Merge produces a new variable ,\_merge,containing ,numeric codes
concerning the source and the cotents of each observation in the merged
dataset.

<pre id="stlog-11" class="stlog"><samp><span class="stinp">. use "C:\Users\RuralNet011\Desktop\datascience\analysis\StataTest\Question 1 Stata Files\11.dta", clear</span>

<span class="stinp">. </span>
<span class="stinp">. <span class="stcmt">// 1:1 merging</span></span>
<span class="stinp">. </span>
<span class="stinp">. merge 1:1 partid using "C:\Users\RuralNet011\Desktop\datascience\analysis\StataTest\Question 1 Stata Files\12.dta"</span>
(note: variable TimeStamp was str15, now str16 to accommodate using data's values)

    Result                           # of obs.
    -----------------------------------------
    not matched              <span class="stres">               0</span>
    matched                  <span class="stres">             395</span>  (_merge==3)
    -----------------------------------------
</samp></pre>

<h2 id="h-8">

<span class="heading-secnum">8 </span> Dropping variables and
observations.

</h2>

<p>

At sompoint we may need to drop some varibles or observations in a data
set.This is majorly caused by overprescence of missing vaulues or maybe
the ate not just needed for analysis.Lets see how to work out this.

</p>

<h3 id="h-8-1">

<span class="heading-secnum">8.1 </span> Variables

</h3>

<p>

To drop a variable we use <code>drop</code> command followed with the
variable names list.Below i am dropning the price variable.

</p>

<pre id="stlog-12" class="stlog"><samp><span class="stinp">. sysuse auto.dta ,clear</span>
(1978 Automobile Data)

<span class="stinp">. drop price</span>
</samp></pre>

<h3 id="h-8-2">

<span class="heading-secnum">8.2 </span> Observations.

</h3>

<p>

To drop an observation,we use an <code>if</code> and/or <code>in</code>
qualifier after the <code>drop command.</code>

</p>

<P>

By using logical operators you can specify more than one condition for
dropping observations.

</P>

<p>

Below i am going to drop observations where the variable foreign column
is domestic and price is greater than $ 6000.

</p>

<pre id="stlog-13" class="stlog"><samp><span class="stinp">. sysuse auto.dta ,clear</span>
(1978 Automobile Data)

<span class="stinp">. drop if foreign == 1 &amp; price &gt; 6000</span>
(9 observations deleted)
</samp></pre>

<p>

And we can see that 9 observations are deleted.As mentioned above whe
can use in to specify the number of observations to delete.

</p>

<p>

Below am dropping 5 observations from the dataset.

</p>

<pre id="stlog-14" class="stlog"><samp><span class="stinp">. drop in 1/5</span>
(5 observations deleted)
</samp></pre>

<h3 id="h-8-3">

<span class="heading-secnum">8.3 </span> Using keep.

</h3>

<p>

By using keep,you are telling stata to drop all variables except those
that are specified or by using an if and/or in expression.

</p>

<pre id="stlog-15" class="stlog"><samp><span class="stinp">. <span class="stcmt">// keeping only price,mpg and foreign variables </span></span>
<span class="stinp">. </span>
<span class="stinp">. keep price mpg foreign</span>

<span class="stinp">. </span>
<span class="stinp">. list in 1/5</span>

     +-------------------------+
     | <span class="stres"> price   mpg    foreign </span>|
     |-------------------------|
  1. | <span class="stres"> 5,788    18   Domestic </span>|
  2. | <span class="stres"> 4,453    26   Domestic </span>|
  3. | <span class="stres"> 5,189    20   Domestic </span>|
  4. | <span class="stres">10,372    16   Domestic </span>|
  5. | <span class="stres"> 4,082    19   Domestic </span>|
     +-------------------------+

<span class="stinp">. </span>
<span class="stinp">. <span class="stcmt">// Deleting 19 observations</span></span>
<span class="stinp">. </span>
<span class="stinp">. keep in 10</span>
(59 observations deleted)

<span class="stinp">. </span>
<span class="stinp">. list </span>

     +------------------------+
     | <span class="stres">price   mpg    foreign </span>|
     |------------------------|
  1. | <span class="stres">5,705    16   Domestic </span>|
     +------------------------+

<span class="stinp">. </span>
<span class="stinp">. <span class="stcmt">// keeping observation by condition</span></span>
<span class="stinp">. </span>
<span class="stinp">. keep if price &gt; 2000</span>
(0 observations deleted)

<span class="stinp">. </span>
<span class="stinp">. list</span>

     +------------------------+
     | <span class="stres">price   mpg    foreign </span>|
     |------------------------|
  1. | <span class="stres">5,705    16   Domestic </span>|
     +------------------------+
</samp></pre>

</body>

</html>
