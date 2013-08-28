---
title: Signal Analysis Experiment with dc.js & crossfilter
author: Timely Portfolio
github: {user: timelyportfolio, repo: rCharts_crossfilter_dcjs, branch: "gh-pages"}
framework: bootstrap
mode: selfcontained
highlighter: prettify
hitheme: twitter-bootstrap
assets:
  css:
  - "http://fonts.googleapis.com/css?family=Raleway:300"
  - "http://fonts.googleapis.com/css?family=Oxygen"
  - "css/dc.css"
  jshead:
  - "http://d3js.org/d3.v3.js"
  - "js/crossfilter.js"
  - "js/dc.js"
---
  
<style>
body{
  font-family: 'Oxygen', sans-serif;
  font-size: 8px;
  line-height: 15px;
}

h1,h2,h3,h4 {
font-family: 'Raleway', sans-serif;
}

.container { width: 1200px; }

h3 {
background-color: #D4DAEC;
  text-indent: 100px; 
}

h4 {
text-indent: 100px;
}
</style>
  
<a href="https://github.com/timelyportfolio/rCharts_crossfilter_dcjs"><img style="position: absolute; top: 0; right: 0; border: 0;" src="https://s3.amazonaws.com/github/ribbons/forkme_right_darkblue_121621.png" alt="Fork me on GitHub"></a>

# Signal Analysis on S&P 500 using [dc.js](http://nickqizhu.github.io/dc.js/) & [crossfilter](http://square.github.io/crossfilter/)
## With Help from [R](http://r-project.org) and [slidify](http://slidify.org)

<div class = "row">
  <div id = "bar-count" class = "span4"><h3>Signal Histogram</h3></div>
  <div id = "line-perf" class = "span4"><h3>Avg Return By Signal</h3></div>
  <div id = "line-year" class = "span4"><h3>Count By Year</h3></div>
</div>

<script>
var spx = 
[
 {
 "date":  -7303,
"name": "GSPC.Close",
"price":  16.66,
"rsi": null,
"ret": null 
},
{
 "date":  -7302,
"name": "GSPC.Close",
"price":  16.85,
"rsi": null,
"ret": 0.011405 
},
{
 "date":  -7301,
"name": "GSPC.Close",
"price":  16.93,
"rsi": null,
"ret": 0.0047478 
},
{
 "date":  -7300,
"name": "GSPC.Close",
"price":  16.98,
"rsi": null,
"ret": 0.0029533 
},
{
 "date":  -7297,
"name": "GSPC.Close",
"price":  17.08,
"rsi": null,
"ret": 0.0058893 
},
{
 "date":  -7296,
"name": "GSPC.Close",
"price":  17.03,
"rsi": null,
"ret": -0.0029274 
},
{
 "date":  -7295,
"name": "GSPC.Close",
"price":  17.09,
"rsi": null,
"ret": 0.0035232 
},
{
 "date":  -7294,
"name": "GSPC.Close",
"price":  16.76,
"rsi": null,
"ret": -0.01931 
},
{
 "date":  -7293,
"name": "GSPC.Close",
"price":  16.67,
"rsi": null,
"ret": -0.0053699 
},
{
 "date":  -7290,
"name": "GSPC.Close",
"price":  16.72,
"rsi": null,
"ret": 0.0029994 
},
{
 "date":  -7289,
"name": "GSPC.Close",
"price":  16.86,
"rsi": null,
"ret": 0.0083732 
},
{
 "date":  -7288,
"name": "GSPC.Close",
"price":  16.85,
"rsi": null,
"ret": -0.00059312 
},
{
 "date":  -7287,
"name": "GSPC.Close",
"price":  16.87,
"rsi": null,
"ret": 0.0011869 
},
{
 "date":  -7286,
"name": "GSPC.Close",
"price":   16.9,
"rsi": null,
"ret": 0.0017783 
},
{
 "date":  -7283,
"name": "GSPC.Close",
"price":  16.92,
"rsi": null,
"ret": 0.0011834 
},
{
 "date":  -7282,
"name": "GSPC.Close",
"price":  16.86,
"rsi": 60.656,
"ret": -0.0035461 
},
{
 "date":  -7281,
"name": "GSPC.Close",
"price":  16.74,
"rsi": 57.605,
"ret": -0.0071174 
},
{
 "date":  -7280,
"name": "GSPC.Close",
"price":  16.73,
"rsi": 51.974,
"ret": -0.00059737 
},
{
 "date":  -7279,
"name": "GSPC.Close",
"price":  16.82,
"rsi": 51.522,
"ret": 0.0053796 
},
{
 "date":  -7276,
"name": "GSPC.Close",
"price":  17.02,
"rsi":  55.29,
"ret": 0.011891 
},
{
 "date":  -7275,
"name": "GSPC.Close",
"price":  17.05,
"rsi": 62.303,
"ret": 0.0017626 
},
{
 "date":  -7274,
"name": "GSPC.Close",
"price":  17.05,
"rsi": 63.235,
"ret":      0 
},
{
 "date":  -7273,
"name": "GSPC.Close",
"price":  17.23,
"rsi": 63.235,
"ret": 0.010557 
},
{
 "date":  -7272,
"name": "GSPC.Close",
"price":  17.29,
"rsi": 68.629,
"ret": 0.0034823 
},
{
 "date":  -7269,
"name": "GSPC.Close",
"price":  17.32,
"rsi": 70.199,
"ret": 0.0017351 
},
{
 "date":  -7268,
"name": "GSPC.Close",
"price":  17.23,
"rsi":  70.98,
"ret": -0.0051963 
},
{
 "date":  -7267,
"name": "GSPC.Close",
"price":  17.21,
"rsi": 65.434,
"ret": -0.0011608 
},
{
 "date":  -7266,
"name": "GSPC.Close",
"price":  17.28,
"rsi": 64.233,
"ret": 0.0040674 
},
{
 "date":  -7265,
"name": "GSPC.Close",
"price":  17.24,
"rsi": 66.548,
"ret": -0.0023148 
},
{
 "date":  -7261,
"name": "GSPC.Close",
"price":  17.06,
"rsi": 63.999,
"ret": -0.010441 
},
{
 "date":  -7260,
"name": "GSPC.Close",
"price":  17.06,
"rsi": 53.981,
"ret":      0 
},
{
 "date":  -7259,
"name": "GSPC.Close",
"price":  16.99,
"rsi": 53.981,
"ret": -0.0041032 
},
{
 "date":  -7258,
"name": "GSPC.Close",
"price":  17.15,
"rsi": 50.421,
"ret": 0.0094173 
},
{
 "date":  -7255,
"name": "GSPC.Close",
"price":   17.2,
"rsi": 57.345,
"ret": 0.0029155 
},
{
 "date":  -7254,
"name": "GSPC.Close",
"price":  17.17,
"rsi":  59.26,
"ret": -0.0017442 
},
{
 "date":  -7252,
"name": "GSPC.Close",
"price":  17.21,
"rsi": 57.589,
"ret": 0.0023296 
},
{
 "date":  -7251,
"name": "GSPC.Close",
"price":  17.28,
"rsi": 59.239,
"ret": 0.0040674 
},
{
 "date":  -7248,
"name": "GSPC.Close",
"price":  17.28,
"rsi": 62.023,
"ret":      0 
},
{
 "date":  -7247,
"name": "GSPC.Close",
"price":  17.22,
"rsi": 62.023,
"ret": -0.0034722 
},
{
 "date":  -7246,
"name": "GSPC.Close",
"price":  17.24,
"rsi":  58.08,
"ret": 0.0011614 
},
{
 "date":  -7245,
"name": "GSPC.Close",
"price":  17.23,
"rsi": 59.015,
"ret": -0.00058005 
},
{
 "date":  -7244,
"name": "GSPC.Close",
"price":  17.29,
"rsi": 58.314,
"ret": 0.0034823 
},
{
 "date":  -7241,
"name": "GSPC.Close",
"price":  17.32,
"rsi": 61.285,
"ret": 0.0017351 
},
{
 "date":  -7240,
"name": "GSPC.Close",
"price":   17.2,
"rsi": 62.715,
"ret": -0.0069284 
},
{
 "date":  -7239,
"name": "GSPC.Close",
"price":  17.19,
"rsi": 54.104,
"ret": -0.0005814 
},
{
 "date":  -7238,
"name": "GSPC.Close",
"price":  17.07,
"rsi": 53.445,
"ret": -0.0069808 
},
{
 "date":  -7237,
"name": "GSPC.Close",
"price":  17.09,
"rsi":  46.18,
"ret": 0.0011716 
},
{
 "date":  -7234,
"name": "GSPC.Close",
"price":  17.12,
"rsi": 47.462,
"ret": 0.0017554 
},
{
 "date":  -7233,
"name": "GSPC.Close",
"price":  17.25,
"rsi": 49.408,
"ret": 0.0075935 
},
{
 "date":  -7232,
"name": "GSPC.Close",
"price":  17.45,
"rsi": 56.866,
"ret": 0.011594 
},
{
 "date":  -7231,
"name": "GSPC.Close",
"price":  17.49,
"rsi": 65.332,
"ret": 0.0022923 
},
{
 "date":  -7230,
"name": "GSPC.Close",
"price":  17.45,
"rsi": 66.739,
"ret": -0.002287 
},
{
 "date":  -7227,
"name": "GSPC.Close",
"price":  17.44,
"rsi": 63.945,
"ret": -0.00057307 
},
{
 "date":  -7226,
"name": "GSPC.Close",
"price":  17.45,
"rsi": 63.233,
"ret": 0.00057339 
},
{
 "date":  -7225,
"name": "GSPC.Close",
"price":  17.55,
"rsi": 63.669,
"ret": 0.0057307 
},
{
 "date":  -7224,
"name": "GSPC.Close",
"price":  17.56,
"rsi": 67.783,
"ret": 0.0005698 
},
{
 "date":  -7223,
"name": "GSPC.Close",
"price":  17.56,
"rsi": 68.171,
"ret":      0 
},
{
 "date":  -7220,
"name": "GSPC.Close",
"price":  17.46,
"rsi": 68.171,
"ret": -0.0056948 
},
{
 "date":  -7219,
"name": "GSPC.Close",
"price":  17.53,
"rsi": 59.813,
"ret": 0.0040092 
},
{
 "date":  -7218,
"name": "GSPC.Close",
"price":  17.44,
"rsi": 63.213,
"ret": -0.0051341 
},
{
 "date":  -7217,
"name": "GSPC.Close",
"price":   17.3,
"rsi": 56.585,
"ret": -0.0080275 
},
{
 "date":  -7216,
"name": "GSPC.Close",
"price":  17.29,
"rsi": 48.131,
"ret": -0.00057803 
},
{
 "date":  -7213,
"name": "GSPC.Close",
"price":  17.53,
"rsi": 47.584,
"ret": 0.013881 
},
{
 "date":  -7212,
"name": "GSPC.Close",
"price":  17.55,
"rsi": 59.483,
"ret": 0.0011409 
},
{
 "date":  -7211,
"name": "GSPC.Close",
"price":  17.63,
"rsi": 60.292,
"ret": 0.0045584 
},
{
 "date":  -7210,
"name": "GSPC.Close",
"price":  17.78,
"rsi": 63.436,
"ret": 0.0085082 
},
{
 "date":  -7206,
"name": "GSPC.Close",
"price":  17.85,
"rsi": 68.477,
"ret": 0.003937 
},
{
 "date":  -7205,
"name": "GSPC.Close",
"price":  17.75,
"rsi":  70.52,
"ret": -0.0056022 
},
{
 "date":  -7204,
"name": "GSPC.Close",
"price":  17.94,
"rsi": 64.127,
"ret": 0.010704 
},
{
 "date":  -7203,
"name": "GSPC.Close",
"price":  17.98,
"rsi":  69.74,
"ret": 0.0022297 
},
{
 "date":  -7202,
"name": "GSPC.Close",
"price":  17.96,
"rsi": 70.777,
"ret": -0.0011123 
},
{
 "date":  -7199,
"name": "GSPC.Close",
"price":  17.88,
"rsi": 69.495,
"ret": -0.0044543 
},
{
 "date":  -7198,
"name": "GSPC.Close",
"price":  18.03,
"rsi": 64.465,
"ret": 0.0083893 
},
{
 "date":  -7197,
"name": "GSPC.Close",
"price":  18.05,
"rsi": 68.996,
"ret": 0.0011093 
},
{
 "date":  -7196,
"name": "GSPC.Close",
"price":  17.93,
"rsi": 69.553,
"ret": -0.0066482 
},
{
 "date":  -7195,
"name": "GSPC.Close",
"price":  17.96,
"rsi": 62.314,
"ret": 0.0016732 
},
{
 "date":  -7192,
"name": "GSPC.Close",
"price":  17.83,
"rsi": 63.341,
"ret": -0.0072383 
},
{
 "date":  -7191,
"name": "GSPC.Close",
"price":  17.83,
"rsi": 56.193,
"ret":      0 
},
{
 "date":  -7190,
"name": "GSPC.Close",
"price":  17.76,
"rsi": 56.193,
"ret": -0.003926 
},
{
 "date":  -7189,
"name": "GSPC.Close",
"price":  17.86,
"rsi": 52.493,
"ret": 0.0056306 
},
{
 "date":  -7188,
"name": "GSPC.Close",
"price":  17.96,
"rsi": 56.863,
"ret": 0.0055991 
},
{
 "date":  -7185,
"name": "GSPC.Close",
"price":  18.22,
"rsi":  60.75,
"ret": 0.014477 
},
{
 "date":  -7184,
"name": "GSPC.Close",
"price":  18.11,
"rsi": 68.659,
"ret": -0.0060373 
},
{
 "date":  -7183,
"name": "GSPC.Close",
"price":  18.27,
"rsi": 62.886,
"ret": 0.0088349 
},
{
 "date":  -7182,
"name": "GSPC.Close",
"price":  18.12,
"rsi": 67.205,
"ret": -0.0082102 
},
{
 "date":  -7181,
"name": "GSPC.Close",
"price":  18.22,
"rsi": 60.139,
"ret": 0.0055188 
},
{
 "date":  -7178,
"name": "GSPC.Close",
"price":  18.27,
"rsi": 62.937,
"ret": 0.0027442 
},
{
 "date":  -7177,
"name": "GSPC.Close",
"price":  18.27,
"rsi": 64.286,
"ret":      0 
},
{
 "date":  -7176,
"name": "GSPC.Close",
"price":  18.29,
"rsi": 64.286,
"ret": 0.0010947 
},
{
 "date":  -7175,
"name": "GSPC.Close",
"price":  18.29,
"rsi":  64.88,
"ret":      0 
},
{
 "date":  -7174,
"name": "GSPC.Close",
"price":  18.18,
"rsi":  64.88,
"ret": -0.0060142 
},
{
 "date":  -7171,
"name": "GSPC.Close",
"price":  18.26,
"rsi": 58.663,
"ret": 0.0044004 
},
{
 "date":  -7170,
"name": "GSPC.Close",
"price":  18.44,
"rsi": 61.549,
"ret": 0.0098576 
},
{
 "date":  -7169,
"name": "GSPC.Close",
"price":  18.52,
"rsi": 67.112,
"ret": 0.0043384 
},
{
 "date":  -7168,
"name": "GSPC.Close",
"price":  18.56,
"rsi": 69.242,
"ret": 0.0021598 
},
{
 "date":  -7167,
"name": "GSPC.Close",
"price":  18.68,
"rsi": 70.278,
"ret": 0.0064655 
},
{
 "date":  -7164,
"name": "GSPC.Close",
"price":   18.6,
"rsi": 73.196,
"ret": -0.0042827 
},
{
 "date":  -7163,
"name": "GSPC.Close",
"price":  18.71,
"rsi": 68.377,
"ret": 0.005914 
},
{
 "date":  -7162,
"name": "GSPC.Close",
"price":  18.69,
"rsi": 71.186,
"ret": -0.0010689 
},
{
 "date":  -7161,
"name": "GSPC.Close",
"price":  18.69,
"rsi": 69.969,
"ret":      0 
},
{
 "date":  -7160,
"name": "GSPC.Close",
"price":  18.67,
"rsi": 69.969,
"ret": -0.0010701 
},
{
 "date":  -7157,
"name": "GSPC.Close",
"price":  18.72,
"rsi": 68.608,
"ret": 0.0026781 
},
{
 "date":  -7155,
"name": "GSPC.Close",
"price":  18.78,
"rsi":  70.17,
"ret": 0.0032051 
},
{
 "date":  -7154,
"name": "GSPC.Close",
"price":  18.77,
"rsi": 71.972,
"ret": -0.00053248 
},
{
 "date":  -7153,
"name": "GSPC.Close",
"price":  18.79,
"rsi":   71.2,
"ret": 0.0010655 
},
{
 "date":  -7150,
"name": "GSPC.Close",
"price":   18.6,
"rsi":  71.85,
"ret": -0.010112 
},
{
 "date":  -7149,
"name": "GSPC.Close",
"price":  18.88,
"rsi": 58.367,
"ret": 0.015054 
},
{
 "date":  -7148,
"name": "GSPC.Close",
"price":  18.93,
"rsi": 67.921,
"ret": 0.0026483 
},
{
 "date":  -7147,
"name": "GSPC.Close",
"price":  19.14,
"rsi": 69.277,
"ret": 0.011094 
},
{
 "date":  -7146,
"name": "GSPC.Close",
"price":  19.26,
"rsi": 74.207,
"ret": 0.0062696 
},
{
 "date":  -7143,
"name": "GSPC.Close",
"price":   19.4,
"rsi": 76.526,
"ret": 0.007269 
},
{
 "date":  -7142,
"name": "GSPC.Close",
"price":  19.25,
"rsi": 78.908,
"ret": -0.007732 
},
{
 "date":  -7141,
"name": "GSPC.Close",
"price":  18.98,
"rsi": 70.637,
"ret": -0.014026 
},
{
 "date":  -7140,
"name": "GSPC.Close",
"price":  18.93,
"rsi": 58.709,
"ret": -0.0026344 
},
{
 "date":  -7139,
"name": "GSPC.Close",
"price":  18.97,
"rsi": 56.796,
"ret": 0.002113 
},
{
 "date":  -7136,
"name": "GSPC.Close",
"price":  18.92,
"rsi": 57.976,
"ret": -0.0026357 
},
{
 "date":  -7135,
"name": "GSPC.Close",
"price":  18.83,
"rsi": 55.921,
"ret": -0.0047569 
},
{
 "date":  -7134,
"name": "GSPC.Close",
"price":     19,
"rsi": 52.325,
"ret": 0.0090281 
},
{
 "date":  -7133,
"name": "GSPC.Close",
"price":  19.16,
"rsi":  57.84,
"ret": 0.0084211 
},
{
 "date":  -7132,
"name": "GSPC.Close",
"price":  19.14,
"rsi": 62.264,
"ret": -0.0010438 
},
{
 "date":  -7129,
"name": "GSPC.Close",
"price":  18.11,
"rsi": 61.396,
"ret": -0.053814 
},
{
 "date":  -7128,
"name": "GSPC.Close",
"price":  17.91,
"rsi": 34.638,
"ret": -0.011044 
},
{
 "date":  -7127,
"name": "GSPC.Close",
"price":  18.11,
"rsi": 31.744,
"ret": 0.011167 
},
{
 "date":  -7126,
"name": "GSPC.Close",
"price":  17.44,
"rsi": 37.377,
"ret": -0.036996 
},
{
 "date":  -7125,
"name": "GSPC.Close",
"price":  17.69,
"rsi": 28.802,
"ret": 0.014335 
},
{
 "date":  -7122,
"name": "GSPC.Close",
"price":  17.64,
"rsi": 34.812,
"ret": -0.0028265 
},
{
 "date":  -7120,
"name": "GSPC.Close",
"price":  17.81,
"rsi":  34.19,
"ret": 0.0096372 
},
{
 "date":  -7119,
"name": "GSPC.Close",
"price":  17.91,
"rsi": 38.229,
"ret": 0.0056148 
},
{
 "date":  -7118,
"name": "GSPC.Close",
"price":  17.67,
"rsi":  40.54,
"ret": -0.0134 
},
{
 "date":  -7115,
"name": "GSPC.Close",
"price":  17.59,
"rsi": 36.965,
"ret": -0.0045274 
},
{
 "date":  -7114,
"name": "GSPC.Close",
"price":  17.32,
"rsi": 35.831,
"ret": -0.01535 
},
{
 "date":  -7113,
"name": "GSPC.Close",
"price":  16.87,
"rsi": 32.236,
"ret": -0.025982 
},
{
 "date":  -7112,
"name": "GSPC.Close",
"price":  16.69,
"rsi": 27.316,
"ret": -0.01067 
},
{
 "date":  -7111,
"name": "GSPC.Close",
"price":  16.87,
"rsi": 25.631,
"ret": 0.010785 
},
{
 "date":  -7108,
"name": "GSPC.Close",
"price":  16.68,
"rsi": 30.264,
"ret": -0.011263 
},
{
 "date":  -7107,
"name": "GSPC.Close",
"price":  17.06,
"rsi": 28.262,
"ret": 0.022782 
},
{
 "date":  -7106,
"name": "GSPC.Close",
"price":  17.36,
"rsi": 37.206,
"ret": 0.017585 
},
{
 "date":  -7105,
"name": "GSPC.Close",
"price":  17.61,
"rsi": 43.224,
"ret": 0.014401 
},
{
 "date":  -7104,
"name": "GSPC.Close",
"price":  17.59,
"rsi": 47.721,
"ret": -0.0011357 
},
{
 "date":  -7101,
"name": "GSPC.Close",
"price":  17.48,
"rsi": 47.397,
"ret": -0.0062536 
},
{
 "date":  -7100,
"name": "GSPC.Close",
"price":  17.23,
"rsi": 45.568,
"ret": -0.014302 
},
{
 "date":  -7099,
"name": "GSPC.Close",
"price":  17.27,
"rsi": 41.636,
"ret": 0.0023215 
},
{
 "date":  -7098,
"name": "GSPC.Close",
"price":   17.5,
"rsi": 42.491,
"ret": 0.013318 
},
{
 "date":  -7097,
"name": "GSPC.Close",
"price":  17.69,
"rsi": 47.275,
"ret": 0.010857 
},
{
 "date":  -7094,
"name": "GSPC.Close",
"price":  17.84,
"rsi": 50.908,
"ret": 0.0084794 
},
{
 "date":  -7093,
"name": "GSPC.Close",
"price":  18.02,
"rsi": 53.625,
"ret": 0.01009 
},
{
 "date":  -7092,
"name": "GSPC.Close",
"price":  17.95,
"rsi":  56.72,
"ret": -0.0038846 
},
{
 "date":  -7091,
"name": "GSPC.Close",
"price":  17.99,
"rsi": 55.178,
"ret": 0.0022284 
},
{
 "date":  -7090,
"name": "GSPC.Close",
"price":  18.14,
"rsi": 55.915,
"ret": 0.008338 
},
{
 "date":  -7087,
"name": "GSPC.Close",
"price":  18.41,
"rsi": 58.663,
"ret": 0.014884 
},
{
 "date":  -7086,
"name": "GSPC.Close",
"price":  18.46,
"rsi": 63.119,
"ret": 0.0027159 
},
{
 "date":  -7085,
"name": "GSPC.Close",
"price":  18.61,
"rsi": 63.895,
"ret": 0.0081257 
},
{
 "date":  -7084,
"name": "GSPC.Close",
"price":  18.48,
"rsi": 66.193,
"ret": -0.0069855 
},
{
 "date":  -7083,
"name": "GSPC.Close",
"price":  18.28,
"rsi": 62.481,
"ret": -0.010823 
},
{
 "date":  -7080,
"name": "GSPC.Close",
"price":  18.29,
"rsi": 57.169,
"ret": 0.00054705 
},
{
 "date":  -7079,
"name": "GSPC.Close",
"price":  18.32,
"rsi": 57.364,
"ret": 0.0016402 
},
{
 "date":  -7078,
"name": "GSPC.Close",
"price":  18.34,
"rsi": 57.983,
"ret": 0.0010917 
},
{
 "date":  -7077,
"name": "GSPC.Close",
"price":  18.54,
"rsi": 58.416,
"ret": 0.010905 
},
{
 "date":  -7076,
"name": "GSPC.Close",
"price":  18.68,
"rsi": 62.571,
"ret": 0.0075512 
},
{
 "date":  -7073,
"name": "GSPC.Close",
"price":   18.7,
"rsi": 65.194,
"ret": 0.0010707 
},
{
 "date":  -7072,
"name": "GSPC.Close",
"price":  18.68,
"rsi": 65.565,
"ret": -0.0010695 
},
{
 "date":  -7071,
"name": "GSPC.Close",
"price":  18.82,
"rsi":  64.82,
"ret": 0.0074946 
},
{
 "date":  -7070,
"name": "GSPC.Close",
"price":  18.79,
"rsi": 67.594,
"ret": -0.001594 
},
{
 "date":  -7069,
"name": "GSPC.Close",
"price":  18.54,
"rsi": 66.386,
"ret": -0.013305 
},
{
 "date":  -7066,
"name": "GSPC.Close",
"price":  18.53,
"rsi": 57.212,
"ret": -0.00053937 
},
{
 "date":  -7065,
"name": "GSPC.Close",
"price":  18.54,
"rsi": 56.873,
"ret": 0.00053967 
},
{
 "date":  -7064,
"name": "GSPC.Close",
"price":  18.43,
"rsi": 57.146,
"ret": -0.0059331 
},
{
 "date":  -7063,
"name": "GSPC.Close",
"price":  18.42,
"rsi": 53.159,
"ret": -0.00054259 
},
{
 "date":  -7062,
"name": "GSPC.Close",
"price":  18.55,
"rsi": 52.798,
"ret": 0.0070575 
},
{
 "date":  -7058,
"name": "GSPC.Close",
"price":  18.68,
"rsi": 56.893,
"ret": 0.0070081 
},
{
 "date":  -7057,
"name": "GSPC.Close",
"price":  18.54,
"rsi": 60.576,
"ret": -0.0074946 
},
{
 "date":  -7056,
"name": "GSPC.Close",
"price":  18.59,
"rsi": 55.115,
"ret": 0.0026969 
},
{
 "date":  -7055,
"name": "GSPC.Close",
"price":  18.75,
"rsi": 56.619,
"ret": 0.0086068 
},
{
 "date":  -7052,
"name": "GSPC.Close",
"price":  18.61,
"rsi": 61.111,
"ret": -0.0074667 
},
{
 "date":  -7051,
"name": "GSPC.Close",
"price":  18.87,
"rsi": 55.678,
"ret": 0.013971 
},
{
 "date":  -7050,
"name": "GSPC.Close",
"price":  19.09,
"rsi": 62.369,
"ret": 0.011659 
},
{
 "date":  -7049,
"name": "GSPC.Close",
"price":  19.18,
"rsi": 66.919,
"ret": 0.0047145 
},
{
 "date":  -7048,
"name": "GSPC.Close",
"price":  19.29,
"rsi": 68.592,
"ret": 0.0057351 
},
{
 "date":  -7045,
"name": "GSPC.Close",
"price":  19.37,
"rsi": 70.553,
"ret": 0.0041472 
},
{
 "date":  -7044,
"name": "GSPC.Close",
"price":  19.31,
"rsi": 71.925,
"ret": -0.0030976 
},
{
 "date":  -7043,
"name": "GSPC.Close",
"price":  19.21,
"rsi": 69.316,
"ret": -0.0051787 
},
{
 "date":  -7042,
"name": "GSPC.Close",
"price":  19.37,
"rsi": 65.078,
"ret": 0.008329 
},
{
 "date":  -7041,
"name": "GSPC.Close",
"price":  19.44,
"rsi": 68.406,
"ret": 0.0036138 
},
{
 "date":  -7038,
"name": "GSPC.Close",
"price":  19.42,
"rsi": 69.764,
"ret": -0.0010288 
},
{
 "date":  -7037,
"name": "GSPC.Close",
"price":  19.14,
"rsi": 68.853,
"ret": -0.014418 
},
{
 "date":  -7036,
"name": "GSPC.Close",
"price":  19.41,
"rsi": 57.534,
"ret": 0.014107 
},
{
 "date":  -7035,
"name": "GSPC.Close",
"price":  19.42,
"rsi": 63.727,
"ret": 0.0005152 
},
{
 "date":  -7034,
"name": "GSPC.Close",
"price":  19.45,
"rsi": 63.936,
"ret": 0.0015448 
},
{
 "date":  -7031,
"name": "GSPC.Close",
"price":  19.69,
"rsi": 64.598,
"ret": 0.012339 
},
{
 "date":  -7030,
"name": "GSPC.Close",
"price":  19.66,
"rsi": 69.428,
"ret": -0.0015236 
},
{
 "date":  -7029,
"name": "GSPC.Close",
"price":     20,
"rsi": 68.176,
"ret": 0.017294 
},
{
 "date":  -7028,
"name": "GSPC.Close",
"price":  19.89,
"rsi": 73.918,
"ret": -0.0055 
},
{
 "date":  -7027,
"name": "GSPC.Close",
"price":  20.12,
"rsi": 69.546,
"ret": 0.011564 
},
{
 "date":  -7024,
"name": "GSPC.Close",
"price":     20,
"rsi": 73.125,
"ret": -0.0059642 
},
{
 "date":  -7023,
"name": "GSPC.Close",
"price":  19.78,
"rsi": 68.596,
"ret": -0.011 
},
{
 "date":  -7022,
"name": "GSPC.Close",
"price":  19.86,
"rsi":  61.12,
"ret": 0.0040445 
},
{
 "date":  -7020,
"name": "GSPC.Close",
"price":  19.85,
"rsi": 62.712,
"ret": -0.00050352 
},
{
 "date":  -7017,
"name": "GSPC.Close",
"price":  19.71,
"rsi": 62.368,
"ret": -0.0070529 
},
{
 "date":  -7016,
"name": "GSPC.Close",
"price":  19.89,
"rsi": 57.609,
"ret": 0.0091324 
},
{
 "date":  -7015,
"name": "GSPC.Close",
"price":  20.01,
"rsi":  61.66,
"ret": 0.0060332 
},
{
 "date":  -7014,
"name": "GSPC.Close",
"price":  20.02,
"rsi": 64.121,
"ret": 0.00049975 
},
{
 "date":  -7013,
"name": "GSPC.Close",
"price":  19.96,
"rsi": 64.327,
"ret": -0.002997 
},
{
 "date":  -7010,
"name": "GSPC.Close",
"price":  19.96,
"rsi": 62.031,
"ret":      0 
},
{
 "date":  -7009,
"name": "GSPC.Close",
"price":  20.08,
"rsi": 62.031,
"ret": 0.006012 
},
{
 "date":  -7008,
"name": "GSPC.Close",
"price":  20.05,
"rsi": 64.934,
"ret": -0.001494 
},
{
 "date":  -7007,
"name": "GSPC.Close",
"price":  19.61,
"rsi": 63.624,
"ret": -0.021945 
},
{
 "date":  -7006,
"name": "GSPC.Close",
"price":  19.77,
"rsi": 48.251,
"ret": 0.0081591 
},
{
 "date":  -7003,
"name": "GSPC.Close",
"price":  19.61,
"rsi": 52.724,
"ret": -0.0080931 
},
{
 "date":  -7002,
"name": "GSPC.Close",
"price":  19.53,
"rsi": 48.234,
"ret": -0.0040796 
},
{
 "date":  -7001,
"name": "GSPC.Close",
"price":  19.56,
"rsi": 46.119,
"ret": 0.0015361 
},
{
 "date":  -7000,
"name": "GSPC.Close",
"price":  19.73,
"rsi": 47.057,
"ret": 0.0086912 
},
{
 "date":  -6999,
"name": "GSPC.Close",
"price":  19.85,
"rsi": 52.139,
"ret": 0.0060821 
},
{
 "date":  -6996,
"name": "GSPC.Close",
"price":  19.36,
"rsi": 55.394,
"ret": -0.024685 
},
{
 "date":  -6994,
"name": "GSPC.Close",
"price":  19.56,
"rsi": 42.641,
"ret": 0.010331 
},
{
 "date":  -6993,
"name": "GSPC.Close",
"price":  19.79,
"rsi": 47.912,
"ret": 0.011759 
},
{
 "date":  -6992,
"name": "GSPC.Close",
"price":  19.94,
"rsi": 53.234,
"ret": 0.0075796 
},
{
 "date":  -6989,
"name": "GSPC.Close",
"price":  20.01,
"rsi": 56.366,
"ret": 0.0035105 
},
{
 "date":  -6988,
"name": "GSPC.Close",
"price":  19.86,
"rsi": 57.786,
"ret": -0.0074963 
},
{
 "date":  -6987,
"name": "GSPC.Close",
"price":  19.82,
"rsi": 53.748,
"ret": -0.0020141 
},
{
 "date":  -6986,
"name": "GSPC.Close",
"price":  19.72,
"rsi": 52.691,
"ret": -0.0050454 
},
{
 "date":  -6985,
"name": "GSPC.Close",
"price":  19.86,
"rsi": 50.041,
"ret": 0.0070994 
},
{
 "date":  -6982,
"name": "GSPC.Close",
"price":  19.93,
"rsi": 53.562,
"ret": 0.0035247 
},
{
 "date":  -6981,
"name": "GSPC.Close",
"price":  19.88,
"rsi":  55.26,
"ret": -0.0025088 
},
{
 "date":  -6980,
"name": "GSPC.Close",
"price":  20.16,
"rsi": 53.748,
"ret": 0.014085 
},
{
 "date":  -6978,
"name": "GSPC.Close",
"price":  20.32,
"rsi": 60.299,
"ret": 0.0079365 
},
{
 "date":  -6975,
"name": "GSPC.Close",
"price":  20.18,
"rsi": 63.482,
"ret": -0.0068898 
},
{
 "date":  -6974,
"name": "GSPC.Close",
"price":  19.56,
"rsi": 59.023,
"ret": -0.030723 
},
{
 "date":  -6973,
"name": "GSPC.Close",
"price":  19.37,
"rsi": 44.212,
"ret": -0.0097137 
},
{
 "date":  -6972,
"name": "GSPC.Close",
"price":  19.51,
"rsi": 40.831,
"ret": 0.0072277 
},
{
 "date":  -6971,
"name": "GSPC.Close",
"price":  19.66,
"rsi": 44.216,
"ret": 0.0076884 
},
{
 "date":  -6968,
"name": "GSPC.Close",
"price":     19,
"rsi": 47.671,
"ret": -0.033571 
},
{
 "date":  -6967,
"name": "GSPC.Close",
"price":  19.31,
"rsi": 36.856,
"ret": 0.016316 
},
{
 "date":  -6966,
"name": "GSPC.Close",
"price":  19.45,
"rsi": 43.356,
"ret": 0.0072501 
},
{
 "date":  -6965,
"name": "GSPC.Close",
"price":   19.4,
"rsi": 46.057,
"ret": -0.0025707 
},
{
 "date":  -6964,
"name": "GSPC.Close",
"price":   19.4,
"rsi": 45.228,
"ret":      0 
},
{
 "date":  -6961,
"name": "GSPC.Close",
"price":  19.72,
"rsi": 45.228,
"ret": 0.016495 
},
{
 "date":  -6960,
"name": "GSPC.Close",
"price":  19.68,
"rsi": 51.686,
"ret": -0.0020284 
},
{
 "date":  -6959,
"name": "GSPC.Close",
"price":  19.67,
"rsi": 50.878,
"ret": -0.00050813 
},
{
 "date":  -6958,
"name": "GSPC.Close",
"price":  19.43,
"rsi": 50.665,
"ret": -0.012201 
},
{
 "date":  -6957,
"name": "GSPC.Close",
"price":  19.33,
"rsi": 45.716,
"ret": -0.0051467 
},
{
 "date":  -6954,
"name": "GSPC.Close",
"price":  19.85,
"rsi": 43.796,
"ret": 0.026901 
},
{
 "date":  -6953,
"name": "GSPC.Close",
"price":  19.96,
"rsi": 54.497,
"ret": 0.0055416 
},
{
 "date":  -6952,
"name": "GSPC.Close",
"price":  19.97,
"rsi": 56.388,
"ret": 0.000501 
},
{
 "date":  -6951,
"name": "GSPC.Close",
"price":  19.98,
"rsi": 56.565,
"ret": 0.00050075 
},
{
 "date":  -6950,
"name": "GSPC.Close",
"price":  20.07,
"rsi": 56.754,
"ret": 0.0045045 
},
{
 "date":  -6946,
"name": "GSPC.Close",
"price":  19.92,
"rsi": 58.502,
"ret": -0.0074738 
},
{
 "date":  -6945,
"name": "GSPC.Close",
"price":   20.3,
"rsi": 54.545,
"ret": 0.019076 
},
{
 "date":  -6944,
"name": "GSPC.Close",
"price":  20.38,
"rsi": 61.626,
"ret": 0.0039409 
},
{
 "date":  -6943,
"name": "GSPC.Close",
"price":  20.43,
"rsi": 62.936,
"ret": 0.0024534 
},
{
 "date":  -6939,
"name": "GSPC.Close",
"price":  20.77,
"rsi": 63.768,
"ret": 0.016642 
},
{
 "date":  -6938,
"name": "GSPC.Close",
"price":  20.69,
"rsi": 68.883,
"ret": -0.0038517 
},
{
 "date":  -6937,
"name": "GSPC.Close",
"price":  20.87,
"rsi": 66.504,
"ret": 0.0086999 
},
{
 "date":  -6936,
"name": "GSPC.Close",
"price":  20.87,
"rsi": 69.091,
"ret":      0 
},
{
 "date":  -6933,
"name": "GSPC.Close",
"price":     21,
"rsi": 69.091,
"ret": 0.006229 
},
{
 "date":  -6932,
"name": "GSPC.Close",
"price":  21.12,
"rsi": 70.968,
"ret": 0.0057143 
},
{
 "date":  -6931,
"name": "GSPC.Close",
"price":  20.85,
"rsi": 72.622,
"ret": -0.012784 
},
{
 "date":  -6930,
"name": "GSPC.Close",
"price":  21.19,
"rsi": 63.815,
"ret": 0.016307 
},
{
 "date":  -6929,
"name": "GSPC.Close",
"price":  21.11,
"rsi": 68.925,
"ret": -0.0037754 
},
{
 "date":  -6926,
"name": "GSPC.Close",
"price":   21.3,
"rsi": 66.544,
"ret": 0.0090005 
},
{
 "date":  -6925,
"name": "GSPC.Close",
"price":  21.46,
"rsi": 69.261,
"ret": 0.0075117 
},
{
 "date":  -6924,
"name": "GSPC.Close",
"price":  21.55,
"rsi": 71.369,
"ret": 0.0041938 
},
{
 "date":  -6923,
"name": "GSPC.Close",
"price":   21.4,
"rsi": 72.511,
"ret": -0.0069606 
},
{
 "date":  -6922,
"name": "GSPC.Close",
"price":  21.36,
"rsi": 67.666,
"ret": -0.0018692 
},
{
 "date":  -6919,
"name": "GSPC.Close",
"price":  21.18,
"rsi": 66.392,
"ret": -0.008427 
},
{
 "date":  -6918,
"name": "GSPC.Close",
"price":  21.26,
"rsi": 60.842,
"ret": 0.0037771 
},
{
 "date":  -6917,
"name": "GSPC.Close",
"price":  21.16,
"rsi": 62.348,
"ret": -0.0047037 
},
{
 "date":  -6916,
"name": "GSPC.Close",
"price":  21.03,
"rsi": 59.278,
"ret": -0.0061437 
},
{
 "date":  -6915,
"name": "GSPC.Close",
"price":  21.26,
"rsi": 55.455,
"ret": 0.010937 
},
{
 "date":  -6912,
"name": "GSPC.Close",
"price":  21.67,
"rsi":  60.33,
"ret": 0.019285 
},
{
 "date":  -6911,
"name": "GSPC.Close",
"price":  21.74,
"rsi": 67.217,
"ret": 0.0032303 
},
{
 "date":  -6910,
"name": "GSPC.Close",
"price":  21.66,
"rsi": 68.231,
"ret": -0.0036799 
},
{
 "date":  -6909,
"name": "GSPC.Close",
"price":  21.77,
"rsi": 65.729,
"ret": 0.0050785 
},
{
 "date":  -6908,
"name": "GSPC.Close",
"price":  21.96,
"rsi": 67.494,
"ret": 0.0087276 
},
{
 "date":  -6905,
"name": "GSPC.Close",
"price":   22.2,
"rsi": 70.336,
"ret": 0.010929 
},
{
 "date":  -6904,
"name": "GSPC.Close",
"price":  22.12,
"rsi":  73.49,
"ret": -0.0036036 
},
{
 "date":  -6903,
"name": "GSPC.Close",
"price":  21.99,
"rsi": 70.788,
"ret": -0.005877 
},
{
 "date":  -6902,
"name": "GSPC.Close",
"price":  22.09,
"rsi":  66.51,
"ret": 0.0045475 
},
{
 "date":  -6901,
"name": "GSPC.Close",
"price":  22.17,
"rsi": 68.107,
"ret": 0.0036215 
},
{
 "date":  -6897,
"name": "GSPC.Close",
"price":  22.18,
"rsi": 69.365,
"ret": 0.00045106 
},
{
 "date":  -6896,
"name": "GSPC.Close",
"price":  22.12,
"rsi": 69.527,
"ret": -0.0027051 
},
{
 "date":  -6895,
"name": "GSPC.Close",
"price":     22,
"rsi": 67.232,
"ret": -0.005425 
},
{
 "date":  -6894,
"name": "GSPC.Close",
"price":  22.13,
"rsi": 62.769,
"ret": 0.0059091 
},
{
 "date":  -6891,
"name": "GSPC.Close",
"price":  21.83,
"rsi": 65.445,
"ret": -0.013556 
},
{
 "date":  -6890,
"name": "GSPC.Close",
"price":  21.79,
"rsi": 55.526,
"ret": -0.0018323 
},
{
 "date":  -6889,
"name": "GSPC.Close",
"price":  21.86,
"rsi": 54.343,
"ret": 0.0032125 
},
{
 "date":  -6887,
"name": "GSPC.Close",
"price":  21.92,
"rsi": 56.105,
"ret": 0.0027447 
},
{
 "date":  -6884,
"name": "GSPC.Close",
"price":  21.93,
"rsi": 57.615,
"ret": 0.0004562 
},
{
 "date":  -6883,
"name": "GSPC.Close",
"price":  21.76,
"rsi": 57.875,
"ret": -0.0077519 
},
{
 "date":  -6882,
"name": "GSPC.Close",
"price":   21.8,
"rsi":  52.03,
"ret": 0.0018382 
},
{
 "date":  -6881,
"name": "GSPC.Close",
"price":  21.85,
"rsi": 53.227,
"ret": 0.0022936 
},
{
 "date":  -6880,
"name": "GSPC.Close",
"price":  21.93,
"rsi": 54.747,
"ret": 0.0036613 
},
{
 "date":  -6877,
"name": "GSPC.Close",
"price":  21.79,
"rsi": 57.147,
"ret": -0.0063839 
},
{
 "date":  -6876,
"name": "GSPC.Close",
"price":  21.79,
"rsi": 51.955,
"ret":      0 
},
{
 "date":  -6875,
"name": "GSPC.Close",
"price":  21.86,
"rsi": 51.955,
"ret": 0.0032125 
},
{
 "date":  -6874,
"name": "GSPC.Close",
"price":  21.95,
"rsi": 54.359,
"ret": 0.0041171 
},
{
 "date":  -6873,
"name": "GSPC.Close",
"price":  21.95,
"rsi": 57.317,
"ret":      0 
},
{
 "date":  -6870,
"name": "GSPC.Close",
"price":   21.7,
"rsi": 57.317,
"ret": -0.01139 
},
{
 "date":  -6869,
"name": "GSPC.Close",
"price":  21.41,
"rsi": 47.417,
"ret": -0.013364 
},
{
 "date":  -6868,
"name": "GSPC.Close",
"price":  21.25,
"rsi": 39.002,
"ret": -0.0074731 
},
{
 "date":  -6867,
"name": "GSPC.Close",
"price":  21.29,
"rsi": 35.282,
"ret": 0.0018824 
},
{
 "date":  -6866,
"name": "GSPC.Close",
"price":  21.64,
"rsi": 36.902,
"ret": 0.01644 
},
{
 "date":  -6863,
"name": "GSPC.Close",
"price":  21.56,
"rsi": 48.948,
"ret": -0.0036969 
},
{
 "date":  -6862,
"name": "GSPC.Close",
"price":  21.52,
"rsi": 46.751,
"ret": -0.0018553 
},
{
 "date":  -6861,
"name": "GSPC.Close",
"price":  21.64,
"rsi": 45.647,
"ret": 0.0055762 
},
{
 "date":  -6860,
"name": "GSPC.Close",
"price":  21.73,
"rsi": 49.498,
"ret": 0.004159 
},
{
 "date":  -6856,
"name": "GSPC.Close",
"price":  21.53,
"rsi": 52.231,
"ret": -0.0092039 
},
{
 "date":  -6855,
"name": "GSPC.Close",
"price":  21.51,
"rsi": 46.242,
"ret": -0.00092894 
},
{
 "date":  -6854,
"name": "GSPC.Close",
"price":  21.26,
"rsi": 45.678,
"ret": -0.011623 
},
{
 "date":  -6853,
"name": "GSPC.Close",
"price":  21.33,
"rsi": 39.235,
"ret": 0.0032926 
},
{
 "date":  -6852,
"name": "GSPC.Close",
"price":  21.48,
"rsi": 41.714,
"ret": 0.0070323 
},
{
 "date":  -6849,
"name": "GSPC.Close",
"price":  21.32,
"rsi": 46.729,
"ret": -0.0074488 
},
{
 "date":  -6848,
"name": "GSPC.Close",
"price":  21.26,
"rsi": 42.526,
"ret": -0.0028143 
},
{
 "date":  -6847,
"name": "GSPC.Close",
"price":   21.4,
"rsi": 41.035,
"ret": 0.0065851 
},
{
 "date":  -6846,
"name": "GSPC.Close",
"price":  21.69,
"rsi": 45.808,
"ret": 0.013551 
},
{
 "date":  -6845,
"name": "GSPC.Close",
"price":  21.72,
"rsi": 54.097,
"ret": 0.0013831 
},
{
 "date":  -6842,
"name": "GSPC.Close",
"price":  21.68,
"rsi": 54.866,
"ret": -0.0018416 
},
{
 "date":  -6841,
"name": "GSPC.Close",
"price":  21.65,
"rsi": 53.578,
"ret": -0.0013838 
},
{
 "date":  -6840,
"name": "GSPC.Close",
"price":  21.64,
"rsi":  52.58,
"ret": -0.00046189 
},
{
 "date":  -6839,
"name": "GSPC.Close",
"price":  21.83,
"rsi": 52.231,
"ret": 0.00878 
},
{
 "date":  -6838,
"name": "GSPC.Close",
"price":  22.09,
"rsi": 57.945,
"ret": 0.01191 
},
{
 "date":  -6835,
"name": "GSPC.Close",
"price":  22.04,
"rsi": 64.247,
"ret": -0.0022635 
},
{
 "date":  -6834,
"name": "GSPC.Close",
"price":  22.09,
"rsi": 62.313,
"ret": 0.0022686 
},
{
 "date":  -6833,
"name": "GSPC.Close",
"price":  22.13,
"rsi": 63.497,
"ret": 0.0018108 
},
{
 "date":  -6832,
"name": "GSPC.Close",
"price":  22.04,
"rsi": 64.458,
"ret": -0.0040669 
},
{
 "date":  -6831,
"name": "GSPC.Close",
"price":  22.04,
"rsi": 60.591,
"ret":      0 
},
{
 "date":  -6828,
"name": "GSPC.Close",
"price":  22.05,
"rsi": 60.591,
"ret": 0.00045372 
},
{
 "date":  -6827,
"name": "GSPC.Close",
"price":  21.96,
"rsi": 60.893,
"ret": -0.0040816 
},
{
 "date":  -6826,
"name": "GSPC.Close",
"price":  21.97,
"rsi": 56.679,
"ret": 0.00045537 
},
{
 "date":  -6825,
"name": "GSPC.Close",
"price":  22.16,
"rsi": 57.035,
"ret": 0.0086482 
},
{
 "date":  -6824,
"name": "GSPC.Close",
"price":  22.39,
"rsi": 63.217,
"ret": 0.010379 
},
{
 "date":  -6821,
"name": "GSPC.Close",
"price":  22.43,
"rsi": 69.026,
"ret": 0.0017865 
},
{
 "date":  -6820,
"name": "GSPC.Close",
"price":  22.53,
"rsi": 69.916,
"ret": 0.0044583 
},
{
 "date":  -6819,
"name": "GSPC.Close",
"price":  22.62,
"rsi": 72.076,
"ret": 0.0039947 
},
{
 "date":  -6818,
"name": "GSPC.Close",
"price":  22.81,
"rsi": 73.893,
"ret": 0.0083996 
},
{
 "date":  -6817,
"name": "GSPC.Close",
"price":  22.77,
"rsi": 77.257,
"ret": -0.0017536 
},
{
 "date":  -6814,
"name": "GSPC.Close",
"price":  22.63,
"rsi": 75.064,
"ret": -0.0061484 
},
{
 "date":  -6813,
"name": "GSPC.Close",
"price":  22.61,
"rsi": 67.809,
"ret": -0.00088378 
},
{
 "date":  -6812,
"name": "GSPC.Close",
"price":  22.64,
"rsi": 66.816,
"ret": 0.0013268 
},
{
 "date":  -6811,
"name": "GSPC.Close",
"price":  22.51,
"rsi": 67.583,
"ret": -0.005742 
},
{
 "date":  -6810,
"name": "GSPC.Close",
"price":  22.33,
"rsi": 61.001,
"ret": -0.0079964 
},
{
 "date":  -6807,
"name": "GSPC.Close",
"price":  22.18,
"rsi": 53.266,
"ret": -0.0067174 
},
{
 "date":  -6806,
"name": "GSPC.Close",
"price":  21.76,
"rsi": 47.823,
"ret": -0.018936 
},
{
 "date":  -6805,
"name": "GSPC.Close",
"price":  21.69,
"rsi":  36.56,
"ret": -0.0032169 
},
{
 "date":  -6804,
"name": "GSPC.Close",
"price":  21.91,
"rsi": 35.077,
"ret": 0.010143 
},
{
 "date":  -6803,
"name": "GSPC.Close",
"price":  21.51,
"rsi": 42.914,
"ret": -0.018257 
},
{
 "date":  -6800,
"name": "GSPC.Close",
"price":  21.46,
"rsi":  34.71,
"ret": -0.0023245 
},
{
 "date":  -6799,
"name": "GSPC.Close",
"price":  21.36,
"rsi": 33.839,
"ret": -0.0046598 
},
{
 "date":  -6798,
"name": "GSPC.Close",
"price":  21.16,
"rsi": 32.104,
"ret": -0.0093633 
},
{
 "date":  -6797,
"name": "GSPC.Close",
"price":  21.05,
"rsi": 28.912,
"ret": -0.0051985 
},
{
 "date":  -6796,
"name": "GSPC.Close",
"price":  21.03,
"rsi": 27.304,
"ret": -0.00095012 
},
{
 "date":  -6793,
"name": "GSPC.Close",
"price":  21.21,
"rsi":  27.01,
"ret": 0.0085592 
},
{
 "date":  -6792,
"name": "GSPC.Close",
"price":  21.35,
"rsi": 33.911,
"ret": 0.0066007 
},
{
 "date":  -6790,
"name": "GSPC.Close",
"price":  21.52,
"rsi": 38.761,
"ret": 0.0079625 
},
{
 "date":  -6789,
"name": "GSPC.Close",
"price":  21.48,
"rsi": 44.123,
"ret": -0.0018587 
},
{
 "date":  -6786,
"name": "GSPC.Close",
"price":  21.24,
"rsi": 43.165,
"ret": -0.011173 
},
{
 "date":  -6785,
"name": "GSPC.Close",
"price":  21.33,
"rsi": 37.856,
"ret": 0.0042373 
},
{
 "date":  -6784,
"name": "GSPC.Close",
"price":  21.48,
"rsi": 40.797,
"ret": 0.0070323 
},
{
 "date":  -6783,
"name": "GSPC.Close",
"price":  21.56,
"rsi": 45.432,
"ret": 0.0037244 
},
{
 "date":  -6782,
"name": "GSPC.Close",
"price":  21.49,
"rsi":  47.78,
"ret": -0.0032468 
},
{
 "date":  -6779,
"name": "GSPC.Close",
"price":  21.61,
"rsi": 45.918,
"ret": 0.005584 
},
{
 "date":  -6778,
"name": "GSPC.Close",
"price":  21.52,
"rsi": 49.547,
"ret": -0.0041647 
},
{
 "date":  -6777,
"name": "GSPC.Close",
"price":  21.55,
"rsi":     47,
"ret": 0.0013941 
},
{
 "date":  -6776,
"name": "GSPC.Close",
"price":  21.84,
"rsi":  47.96,
"ret": 0.013457 
},
{
 "date":  -6775,
"name": "GSPC.Close",
"price":  22.04,
"rsi":  56.22,
"ret": 0.0091575 
},
{
 "date":  -6772,
"name": "GSPC.Close",
"price":  22.05,
"rsi": 60.837,
"ret": 0.00045372 
},
{
 "date":  -6771,
"name": "GSPC.Close",
"price":  22.02,
"rsi": 61.058,
"ret": -0.0013605 
},
{
 "date":  -6770,
"name": "GSPC.Close",
"price":  21.91,
"rsi": 59.964,
"ret": -0.0049955 
},
{
 "date":  -6769,
"name": "GSPC.Close",
"price":  21.78,
"rsi": 56.003,
"ret": -0.0059334 
},
{
 "date":  -6768,
"name": "GSPC.Close",
"price":  21.55,
"rsi": 51.659,
"ret": -0.01056 
},
{
 "date":  -6765,
"name": "GSPC.Close",
"price":  21.29,
"rsi": 45.007,
"ret": -0.012065 
},
{
 "date":  -6764,
"name": "GSPC.Close",
"price":   21.3,
"rsi": 38.909,
"ret": 0.0004697 
},
{
 "date":  -6763,
"name": "GSPC.Close",
"price":  21.37,
"rsi":  39.25,
"ret": 0.0032864 
},
{
 "date":  -6762,
"name": "GSPC.Close",
"price":   21.1,
"rsi": 41.703,
"ret": -0.012635 
},
{
 "date":  -6761,
"name": "GSPC.Close",
"price":  20.96,
"rsi": 35.713,
"ret": -0.0066351 
},
{
 "date":  -6758,
"name": "GSPC.Close",
"price":   21.1,
"rsi": 33.061,
"ret": 0.0066794 
},
{
 "date":  -6757,
"name": "GSPC.Close",
"price":  21.23,
"rsi": 38.017,
"ret": 0.0061611 
},
{
 "date":  -6755,
"name": "GSPC.Close",
"price":  21.64,
"rsi":  42.29,
"ret": 0.019312 
},
{
 "date":  -6754,
"name": "GSPC.Close",
"price":  21.64,
"rsi": 53.239,
"ret":      0 
},
{
 "date":  -6751,
"name": "GSPC.Close",
"price":  21.73,
"rsi": 53.239,
"ret": 0.004159 
},
{
 "date":  -6750,
"name": "GSPC.Close",
"price":  21.63,
"rsi": 55.393,
"ret": -0.0046019 
},
{
 "date":  -6749,
"name": "GSPC.Close",
"price":  21.68,
"rsi": 52.499,
"ret": 0.0023116 
},
{
 "date":  -6748,
"name": "GSPC.Close",
"price":   21.8,
"rsi": 53.799,
"ret": 0.0055351 
},
{
 "date":  -6747,
"name": "GSPC.Close",
"price":  21.98,
"rsi":  56.85,
"ret": 0.0082569 
},
{
 "date":  -6744,
"name": "GSPC.Close",
"price":  21.73,
"rsi": 61.011,
"ret": -0.011374 
},
{
 "date":  -6743,
"name": "GSPC.Close",
"price":  21.92,
"rsi": 53.321,
"ret": 0.0087437 
},
{
 "date":  -6742,
"name": "GSPC.Close",
"price":  21.88,
"rsi": 57.686,
"ret": -0.0018248 
},
{
 "date":  -6741,
"name": "GSPC.Close",
"price":  21.84,
"rsi": 56.489,
"ret": -0.0018282 
},
{
 "date":  -6740,
"name": "GSPC.Close",
"price":  21.88,
"rsi": 55.253,
"ret": 0.0018315 
},
{
 "date":  -6737,
"name": "GSPC.Close",
"price":   22.1,
"rsi": 56.283,
"ret": 0.010055 
},
{
 "date":  -6736,
"name": "GSPC.Close",
"price":  22.44,
"rsi": 61.526,
"ret": 0.015385 
},
{
 "date":  -6735,
"name": "GSPC.Close",
"price":  22.32,
"rsi": 67.928,
"ret": -0.0053476 
},
{
 "date":  -6734,
"name": "GSPC.Close",
"price":  22.47,
"rsi": 63.887,
"ret": 0.0067204 
},
{
 "date":  -6733,
"name": "GSPC.Close",
"price":  22.53,
"rsi": 66.565,
"ret": 0.0026702 
},
{
 "date":  -6730,
"name": "GSPC.Close",
"price":  22.63,
"rsi":   67.6,
"ret": 0.0044385 
},
{
 "date":  -6729,
"name": "GSPC.Close",
"price":   22.4,
"rsi": 69.305,
"ret": -0.010163 
},
{
 "date":  -6728,
"name": "GSPC.Close",
"price":  22.51,
"rsi": 61.313,
"ret": 0.0049107 
},
{
 "date":  -6727,
"name": "GSPC.Close",
"price":  22.82,
"rsi": 63.482,
"ret": 0.013772 
},
{
 "date":  -6726,
"name": "GSPC.Close",
"price":  22.85,
"rsi": 68.792,
"ret": 0.0013146 
},
{
 "date":  -6723,
"name": "GSPC.Close",
"price":  23.01,
"rsi": 69.258,
"ret": 0.0070022 
},
{
 "date":  -6722,
"name": "GSPC.Close",
"price":  23.03,
"rsi": 71.685,
"ret": 0.00086919 
},
{
 "date":  -6721,
"name": "GSPC.Close",
"price":  22.93,
"rsi": 71.983,
"ret": -0.0043422 
},
{
 "date":  -6720,
"name": "GSPC.Close",
"price":  22.84,
"rsi": 68.125,
"ret": -0.003925 
},
{
 "date":  -6719,
"name": "GSPC.Close",
"price":  22.79,
"rsi":  64.76,
"ret": -0.0021891 
},
{
 "date":  -6716,
"name": "GSPC.Close",
"price":   22.8,
"rsi": 62.901,
"ret": 0.00043879 
},
{
 "date":  -6715,
"name": "GSPC.Close",
"price":   22.7,
"rsi": 63.129,
"ret": -0.004386 
},
{
 "date":  -6714,
"name": "GSPC.Close",
"price":  22.79,
"rsi": 59.212,
"ret": 0.0039648 
},
{
 "date":  -6713,
"name": "GSPC.Close",
"price":  22.87,
"rsi": 61.526,
"ret": 0.0035103 
},
{
 "date":  -6712,
"name": "GSPC.Close",
"price":  22.94,
"rsi": 63.508,
"ret": 0.0030608 
},
{
 "date":  -6709,
"name": "GSPC.Close",
"price":  22.93,
"rsi": 65.197,
"ret": -0.00043592 
},
{
 "date":  -6708,
"name": "GSPC.Close",
"price":  22.83,
"rsi": 64.736,
"ret": -0.0043611 
},
{
 "date":  -6707,
"name": "GSPC.Close",
"price":  22.75,
"rsi": 60.155,
"ret": -0.0035042 
},
{
 "date":  -6706,
"name": "GSPC.Close",
"price":   22.9,
"rsi": 56.698,
"ret": 0.0065934 
},
{
 "date":  -6705,
"name": "GSPC.Close",
"price":  22.88,
"rsi":   61.2,
"ret": -0.00087336 
},
{
 "date":  -6702,
"name": "GSPC.Close",
"price":  22.85,
"rsi":   60.3,
"ret": -0.0013112 
},
{
 "date":  -6701,
"name": "GSPC.Close",
"price":   22.9,
"rsi":   58.9,
"ret": 0.0021882 
},
{
 "date":  -6700,
"name": "GSPC.Close",
"price":  23.08,
"rsi": 60.544,
"ret": 0.0078603 
},
{
 "date":  -6699,
"name": "GSPC.Close",
"price":  23.24,
"rsi": 65.841,
"ret": 0.0069324 
},
{
 "date":  -6698,
"name": "GSPC.Close",
"price":  23.28,
"rsi":  69.73,
"ret": 0.0017212 
},
{
 "date":  -6694,
"name": "GSPC.Close",
"price":  23.28,
"rsi": 70.631,
"ret":      0 
},
{
 "date":  -6693,
"name": "GSPC.Close",
"price":  23.42,
"rsi": 70.631,
"ret": 0.0060137 
},
{
 "date":  -6692,
"name": "GSPC.Close",
"price":  23.47,
"rsi": 73.795,
"ret": 0.0021349 
},
{
 "date":  -6691,
"name": "GSPC.Close",
"price":  23.53,
"rsi": 74.837,
"ret": 0.0025565 
},
{
 "date":  -6688,
"name": "GSPC.Close",
"price":  23.62,
"rsi": 76.068,
"ret": 0.0038249 
},
{
 "date":  -6687,
"name": "GSPC.Close",
"price":   23.5,
"rsi":  77.82,
"ret": -0.0050804 
},
{
 "date":  -6686,
"name": "GSPC.Close",
"price":   23.6,
"rsi": 70.417,
"ret": 0.0042553 
},
{
 "date":  -6685,
"name": "GSPC.Close",
"price":  23.71,
"rsi": 72.744,
"ret": 0.004661 
},
{
 "date":  -6684,
"name": "GSPC.Close",
"price":  23.69,
"rsi": 75.067,
"ret": -0.00084353 
},
{
 "date":  -6681,
"name": "GSPC.Close",
"price":  23.62,
"rsi": 73.835,
"ret": -0.0029548 
},
{
 "date":  -6680,
"name": "GSPC.Close",
"price":  23.59,
"rsi": 69.533,
"ret": -0.0012701 
},
{
 "date":  -6679,
"name": "GSPC.Close",
"price":  23.59,
"rsi": 67.712,
"ret":      0 
},
{
 "date":  -6678,
"name": "GSPC.Close",
"price":  23.57,
"rsi": 67.712,
"ret": -0.00084782 
},
{
 "date":  -6677,
"name": "GSPC.Close",
"price":   23.4,
"rsi": 66.368,
"ret": -0.0072126 
},
{
 "date":  -6674,
"name": "GSPC.Close",
"price":   23.3,
"rsi": 56.165,
"ret": -0.0042735 
},
{
 "date":  -6673,
"name": "GSPC.Close",
"price":  23.38,
"rsi":  51.18,
"ret": 0.0034335 
},
{
 "date":  -6672,
"name": "GSPC.Close",
"price":   23.4,
"rsi": 54.648,
"ret": 0.00085543 
},
{
 "date":  -6671,
"name": "GSPC.Close",
"price":  23.27,
"rsi": 55.499,
"ret": -0.0055556 
},
{
 "date":  -6670,
"name": "GSPC.Close",
"price":  23.26,
"rsi": 49.055,
"ret": -0.00042974 
},
{
 "date":  -6667,
"name": "GSPC.Close",
"price":  23.47,
"rsi": 48.588,
"ret": 0.0090284 
},
{
 "date":  -6666,
"name": "GSPC.Close",
"price":  23.64,
"rsi": 57.701,
"ret": 0.0072433 
},
{
 "date":  -6665,
"name": "GSPC.Close",
"price":  23.79,
"rsi": 63.362,
"ret": 0.0063452 
},
{
 "date":  -6664,
"name": "GSPC.Close",
"price":  23.72,
"rsi": 67.496,
"ret": -0.0029424 
},
{
 "date":  -6663,
"name": "GSPC.Close",
"price":  23.78,
"rsi": 63.874,
"ret": 0.0025295 
},
{
 "date":  -6660,
"name": "GSPC.Close",
"price":  23.75,
"rsi": 65.579,
"ret": -0.0012616 
},
{
 "date":  -6659,
"name": "GSPC.Close",
"price":  23.65,
"rsi": 63.954,
"ret": -0.0042105 
},
{
 "date":  -6658,
"name": "GSPC.Close",
"price":  23.61,
"rsi": 58.729,
"ret": -0.0016913 
},
{
 "date":  -6657,
"name": "GSPC.Close",
"price":   23.7,
"rsi": 56.732,
"ret": 0.0038119 
},
{
 "date":  -6653,
"name": "GSPC.Close",
"price":  23.85,
"rsi": 60.025,
"ret": 0.0063291 
},
{
 "date":  -6652,
"name": "GSPC.Close",
"price":  23.77,
"rsi":  64.83,
"ret": -0.0033543 
},
{
 "date":  -6651,
"name": "GSPC.Close",
"price":  23.69,
"rsi": 60.644,
"ret": -0.0033656 
},
{
 "date":  -6650,
"name": "GSPC.Close",
"price":  23.67,
"rsi": 56.701,
"ret": -0.00084424 
},
{
 "date":  -6649,
"name": "GSPC.Close",
"price":  23.32,
"rsi": 55.725,
"ret": -0.014787 
},
{
 "date":  -6646,
"name": "GSPC.Close",
"price":  22.75,
"rsi": 42.081,
"ret": -0.024443 
},
{
 "date":  -6645,
"name": "GSPC.Close",
"price":  22.84,
"rsi":  29.44,
"ret": 0.003956 
},
{
 "date":  -6644,
"name": "GSPC.Close",
"price":  23.03,
"rsi": 32.869,
"ret": 0.0083187 
},
{
 "date":  -6643,
"name": "GSPC.Close",
"price":  22.96,
"rsi": 39.548,
"ret": -0.0030395 
},
{
 "date":  -6642,
"name": "GSPC.Close",
"price":  22.81,
"rsi": 38.046,
"ret": -0.0065331 
},
{
 "date":  -6639,
"name": "GSPC.Close",
"price":  22.69,
"rsi": 34.981,
"ret": -0.0052609 
},
{
 "date":  -6638,
"name": "GSPC.Close",
"price":  22.66,
"rsi":  32.71,
"ret": -0.0013222 
},
{
 "date":  -6637,
"name": "GSPC.Close",
"price":  22.94,
"rsi": 32.148,
"ret": 0.012357 
},
{
 "date":  -6636,
"name": "GSPC.Close",
"price":   23.1,
"rsi": 42.138,
"ret": 0.0069747 
},
{
 "date":  -6635,
"name": "GSPC.Close",
"price":  22.93,
"rsi": 46.945,
"ret": -0.0073593 
},
{
 "date":  -6632,
"name": "GSPC.Close",
"price":  22.82,
"rsi":  42.87,
"ret": -0.0047972 
},
{
 "date":  -6630,
"name": "GSPC.Close",
"price":  22.49,
"rsi": 40.424,
"ret": -0.014461 
},
{
 "date":  -6629,
"name": "GSPC.Close",
"price":  22.47,
"rsi": 34.134,
"ret": -0.00088928 
},
{
 "date":  -6628,
"name": "GSPC.Close",
"price":  22.75,
"rsi": 33.791,
"ret": 0.012461 
},
{
 "date":  -6624,
"name": "GSPC.Close",
"price":  22.79,
"rsi": 42.506,
"ret": 0.0017582 
},
{
 "date":  -6623,
"name": "GSPC.Close",
"price":  22.85,
"rsi": 43.647,
"ret": 0.0026327 
},
{
 "date":  -6622,
"name": "GSPC.Close",
"price":  22.84,
"rsi": 45.398,
"ret": -0.00043764 
},
{
 "date":  -6621,
"name": "GSPC.Close",
"price":  22.82,
"rsi": 45.146,
"ret": -0.00087566 
},
{
 "date":  -6618,
"name": "GSPC.Close",
"price":  22.73,
"rsi": 44.613,
"ret": -0.0039439 
},
{
 "date":  -6617,
"name": "GSPC.Close",
"price":  22.68,
"rsi":   42.2,
"ret": -0.0021997 
},
{
 "date":  -6616,
"name": "GSPC.Close",
"price":  22.64,
"rsi": 40.877,
"ret": -0.0017637 
},
{
 "date":  -6614,
"name": "GSPC.Close",
"price":   22.4,
"rsi": 39.801,
"ret": -0.010601 
},
{
 "date":  -6611,
"name": "GSPC.Close",
"price":  22.43,
"rsi":  34.02,
"ret": 0.0013393 
},
{
 "date":  -6610,
"name": "GSPC.Close",
"price":  22.66,
"rsi": 35.285,
"ret": 0.010254 
},
{
 "date":  -6609,
"name": "GSPC.Close",
"price":  22.61,
"rsi": 44.132,
"ret": -0.0022065 
},
{
 "date":  -6608,
"name": "GSPC.Close",
"price":  22.67,
"rsi": 42.764,
"ret": 0.0026537 
},
{
 "date":  -6607,
"name": "GSPC.Close",
"price":  22.88,
"rsi": 44.969,
"ret": 0.0092633 
},
{
 "date":  -6604,
"name": "GSPC.Close",
"price":  23.01,
"rsi": 51.948,
"ret": 0.0056818 
},
{
 "date":  -6603,
"name": "GSPC.Close",
"price":  23.14,
"rsi": 55.694,
"ret": 0.0056497 
},
{
 "date":  -6602,
"name": "GSPC.Close",
"price":  23.07,
"rsi": 59.126,
"ret": -0.0030251 
},
{
 "date":  -6601,
"name": "GSPC.Close",
"price":  23.34,
"rsi": 56.584,
"ret": 0.011704 
},
{
 "date":  -6600,
"name": "GSPC.Close",
"price":  23.38,
"rsi": 63.162,
"ret": 0.0017138 
},
{
 "date":  -6597,
"name": "GSPC.Close",
"price":  23.42,
"rsi": 64.031,
"ret": 0.0017109 
},
{
 "date":  -6596,
"name": "GSPC.Close",
"price":   23.3,
"rsi": 64.923,
"ret": -0.0051238 
},
{
 "date":  -6595,
"name": "GSPC.Close",
"price":  23.37,
"rsi": 60.109,
"ret": 0.0030043 
},
{
 "date":  -6594,
"name": "GSPC.Close",
"price":  23.39,
"rsi": 61.884,
"ret": 0.0008558 
},
{
 "date":  -6593,
"name": "GSPC.Close",
"price":  23.37,
"rsi": 62.399,
"ret": -0.00085507 
},
{
 "date":  -6590,
"name": "GSPC.Close",
"price":  23.41,
"rsi": 61.505,
"ret": 0.0017116 
},
{
 "date":  -6589,
"name": "GSPC.Close",
"price":  23.49,
"rsi": 62.658,
"ret": 0.0034173 
},
{
 "date":  -6588,
"name": "GSPC.Close",
"price":  23.57,
"rsi": 64.921,
"ret": 0.0034057 
},
{
 "date":  -6587,
"name": "GSPC.Close",
"price":  23.57,
"rsi": 67.071,
"ret":      0 
},
{
 "date":  -6586,
"name": "GSPC.Close",
"price":  23.51,
"rsi": 67.071,
"ret": -0.0025456 
},
{
 "date":  -6583,
"name": "GSPC.Close",
"price":  23.54,
"rsi": 63.677,
"ret": 0.0012761 
},
{
 "date":  -6581,
"name": "GSPC.Close",
"price":  23.44,
"rsi":  64.64,
"ret": -0.0042481 
},
{
 "date":  -6580,
"name": "GSPC.Close",
"price":  23.65,
"rsi": 59.021,
"ret": 0.008959 
},
{
 "date":  -6579,
"name": "GSPC.Close",
"price":  23.69,
"rsi": 65.754,
"ret": 0.0016913 
},
{
 "date":  -6576,
"name": "GSPC.Close",
"price":  23.77,
"rsi":  66.87,
"ret": 0.003377 
},
{
 "date":  -6574,
"name": "GSPC.Close",
"price":   23.8,
"rsi": 69.044,
"ret": 0.0012621 
},
{
 "date":  -6573,
"name": "GSPC.Close",
"price":  23.88,
"rsi": 69.843,
"ret": 0.0033613 
},
{
 "date":  -6572,
"name": "GSPC.Close",
"price":  23.92,
"rsi": 71.925,
"ret": 0.001675 
},
{
 "date":  -6569,
"name": "GSPC.Close",
"price":  23.91,
"rsi": 72.931,
"ret": -0.00041806 
},
{
 "date":  -6568,
"name": "GSPC.Close",
"price":  23.82,
"rsi": 72.234,
"ret": -0.0037641 
},
{
 "date":  -6567,
"name": "GSPC.Close",
"price":  23.74,
"rsi": 66.111,
"ret": -0.0033585 
},
{
 "date":  -6566,
"name": "GSPC.Close",
"price":  23.86,
"rsi":  61.15,
"ret": 0.0050548 
},
{
 "date":  -6565,
"name": "GSPC.Close",
"price":  23.98,
"rsi":  65.35,
"ret": 0.0050293 
},
{
 "date":  -6562,
"name": "GSPC.Close",
"price":  24.16,
"rsi": 68.964,
"ret": 0.0075063 
},
{
 "date":  -6561,
"name": "GSPC.Close",
"price":  24.06,
"rsi": 73.439,
"ret": -0.0041391 
},
{
 "date":  -6560,
"name": "GSPC.Close",
"price":  24.09,
"rsi": 67.607,
"ret": 0.0012469 
},
{
 "date":  -6559,
"name": "GSPC.Close",
"price":   24.2,
"rsi": 68.417,
"ret": 0.0045662 
},
{
 "date":  -6558,
"name": "GSPC.Close",
"price":  24.25,
"rsi": 71.257,
"ret": 0.0020661 
},
{
 "date":  -6555,
"name": "GSPC.Close",
"price":  24.46,
"rsi": 72.468,
"ret": 0.0086598 
},
{
 "date":  -6554,
"name": "GSPC.Close",
"price":  24.66,
"rsi": 76.877,
"ret": 0.0081766 
},
{
 "date":  -6553,
"name": "GSPC.Close",
"price":  24.54,
"rsi": 80.139,
"ret": -0.0048662 
},
{
 "date":  -6552,
"name": "GSPC.Close",
"price":  24.56,
"rsi": 73.444,
"ret": 0.000815 
},
{
 "date":  -6551,
"name": "GSPC.Close",
"price":  24.55,
"rsi": 73.837,
"ret": -0.00040717 
},
{
 "date":  -6548,
"name": "GSPC.Close",
"price":  24.61,
"rsi": 73.254,
"ret": 0.002444 
},
{
 "date":  -6547,
"name": "GSPC.Close",
"price":  24.57,
"rsi": 74.552,
"ret": -0.0016254 
},
{
 "date":  -6546,
"name": "GSPC.Close",
"price":  24.23,
"rsi": 72.042,
"ret": -0.013838 
},
{
 "date":  -6545,
"name": "GSPC.Close",
"price":  24.14,
"rsi": 55.073,
"ret": -0.0037144 
},
{
 "date":  -6544,
"name": "GSPC.Close",
"price":   24.3,
"rsi": 51.608,
"ret": 0.006628 
},
{
 "date":  -6541,
"name": "GSPC.Close",
"price":  24.12,
"rsi": 56.811,
"ret": -0.0074074 
},
{
 "date":  -6540,
"name": "GSPC.Close",
"price":  24.11,
"rsi": 50.263,
"ret": -0.00041459 
},
{
 "date":  -6539,
"name": "GSPC.Close",
"price":  24.18,
"rsi": 49.919,
"ret": 0.0029034 
},
{
 "date":  -6538,
"name": "GSPC.Close",
"price":  24.11,
"rsi": 52.378,
"ret": -0.002895 
},
{
 "date":  -6537,
"name": "GSPC.Close",
"price":  24.24,
"rsi": 49.748,
"ret": 0.005392 
},
{
 "date":  -6534,
"name": "GSPC.Close",
"price":  24.11,
"rsi": 54.334,
"ret": -0.005363 
},
{
 "date":  -6532,
"name": "GSPC.Close",
"price":  23.92,
"rsi": 49.472,
"ret": -0.0078805 
},
{
 "date":  -6531,
"name": "GSPC.Close",
"price":  23.87,
"rsi": 43.364,
"ret": -0.0020903 
},
{
 "date":  -6530,
"name": "GSPC.Close",
"price":  23.86,
"rsi": 41.898,
"ret": -0.00041894 
},
{
 "date":  -6527,
"name": "GSPC.Close",
"price":  23.74,
"rsi": 41.596,
"ret": -0.0050293 
},
{
 "date":  -6526,
"name": "GSPC.Close",
"price":  23.36,
"rsi": 38.042,
"ret": -0.016007 
},
{
 "date":  -6525,
"name": "GSPC.Close",
"price":  23.09,
"rsi": 29.459,
"ret": -0.011558 
},
{
 "date":  -6524,
"name": "GSPC.Close",
"price":  23.16,
"rsi": 25.122,
"ret": 0.0030316 
},
{
 "date":  -6520,
"name": "GSPC.Close",
"price":  23.23,
"rsi": 28.079,
"ret": 0.0030225 
},
{
 "date":  -6519,
"name": "GSPC.Close",
"price":  23.15,
"rsi": 31.012,
"ret": -0.0034438 
},
{
 "date":  -6518,
"name": "GSPC.Close",
"price":  23.18,
"rsi":  29.53,
"ret": 0.0012959 
},
{
 "date":  -6517,
"name": "GSPC.Close",
"price":  23.29,
"rsi": 30.864,
"ret": 0.0047455 
},
{
 "date":  -6516,
"name": "GSPC.Close",
"price":  23.26,
"rsi": 35.674,
"ret": -0.0012881 
},
{
 "date":  -6513,
"name": "GSPC.Close",
"price":  23.29,
"rsi":  34.96,
"ret": 0.0012898 
},
{
 "date":  -6512,
"name": "GSPC.Close",
"price":  23.68,
"rsi": 36.333,
"ret": 0.016745 
},
{
 "date":  -6511,
"name": "GSPC.Close",
"price":  23.71,
"rsi": 50.857,
"ret": 0.0012669 
},
{
 "date":  -6510,
"name": "GSPC.Close",
"price":  23.69,
"rsi": 51.768,
"ret": -0.00084353 
},
{
 "date":  -6509,
"name": "GSPC.Close",
"price":  23.72,
"rsi": 51.088,
"ret": 0.0012664 
},
{
 "date":  -6506,
"name": "GSPC.Close",
"price":   23.6,
"rsi": 52.105,
"ret": -0.005059 
},
{
 "date":  -6505,
"name": "GSPC.Close",
"price":  23.62,
"rsi": 47.823,
"ret": 0.00084746 
},
{
 "date":  -6504,
"name": "GSPC.Close",
"price":  23.73,
"rsi": 48.581,
"ret": 0.0046571 
},
{
 "date":  -6503,
"name": "GSPC.Close",
"price":  23.75,
"rsi": 52.657,
"ret": 0.00084282 
},
{
 "date":  -6502,
"name": "GSPC.Close",
"price":  23.75,
"rsi": 53.381,
"ret":      0 
},
{
 "date":  -6499,
"name": "GSPC.Close",
"price":  23.92,
"rsi": 53.381,
"ret": 0.0071579 
},
{
 "date":  -6498,
"name": "GSPC.Close",
"price":  23.87,
"rsi": 59.486,
"ret": -0.0020903 
},
{
 "date":  -6497,
"name": "GSPC.Close",
"price":  23.82,
"rsi": 57.117,
"ret": -0.0020947 
},
{
 "date":  -6496,
"name": "GSPC.Close",
"price":  23.89,
"rsi": 54.768,
"ret": 0.0029387 
},
{
 "date":  -6495,
"name": "GSPC.Close",
"price":  23.93,
"rsi": 57.408,
"ret": 0.0016743 
},
{
 "date":  -6492,
"name": "GSPC.Close",
"price":  23.93,
"rsi": 58.886,
"ret":      0 
},
{
 "date":  -6491,
"name": "GSPC.Close",
"price":  23.79,
"rsi": 58.886,
"ret": -0.0058504 
},
{
 "date":  -6490,
"name": "GSPC.Close",
"price":  23.78,
"rsi": 51.619,
"ret": -0.00042034 
},
{
 "date":  -6489,
"name": "GSPC.Close",
"price":  23.99,
"rsi": 51.133,
"ret": 0.008831 
},
{
 "date":  -6488,
"name": "GSPC.Close",
"price":  24.18,
"rsi": 59.703,
"ret": 0.00792 
},
{
 "date":  -6485,
"name": "GSPC.Close",
"price":  24.37,
"rsi": 65.584,
"ret": 0.0078577 
},
{
 "date":  -6484,
"name": "GSPC.Close",
"price":  24.18,
"rsi": 70.258,
"ret": -0.0077965 
},
{
 "date":  -6483,
"name": "GSPC.Close",
"price":  24.12,
"rsi": 61.293,
"ret": -0.0024814 
},
{
 "date":  -6482,
"name": "GSPC.Close",
"price":  24.12,
"rsi": 58.744,
"ret":      0 
},
{
 "date":  -6481,
"name": "GSPC.Close",
"price":  24.02,
"rsi": 58.744,
"ret": -0.0041459 
},
{
 "date":  -6478,
"name": "GSPC.Close",
"price":   23.8,
"rsi": 54.373,
"ret": -0.009159 
},
{
 "date":  -6477,
"name": "GSPC.Close",
"price":  23.91,
"rsi": 46.224,
"ret": 0.0046218 
},
{
 "date":  -6476,
"name": "GSPC.Close",
"price":  23.94,
"rsi":  50.24,
"ret": 0.0012547 
},
{
 "date":  -6475,
"name": "GSPC.Close",
"price":  24.11,
"rsi": 51.308,
"ret": 0.0071011 
},
{
 "date":  -6471,
"name": "GSPC.Close",
"price":  23.95,
"rsi": 56.946,
"ret": -0.0066363 
},
{
 "date":  -6470,
"name": "GSPC.Close",
"price":  23.65,
"rsi": 50.964,
"ret": -0.012526 
},
{
 "date":  -6469,
"name": "GSPC.Close",
"price":  23.58,
"rsi": 42.046,
"ret": -0.0029598 
},
{
 "date":  -6468,
"name": "GSPC.Close",
"price":  23.41,
"rsi": 40.275,
"ret": -0.0072095 
},
{
 "date":  -6467,
"name": "GSPC.Close",
"price":   23.5,
"rsi": 36.278,
"ret": 0.0038445 
},
{
 "date":  -6464,
"name": "GSPC.Close",
"price":  23.69,
"rsi":  39.69,
"ret": 0.0080851 
},
{
 "date":  -6463,
"name": "GSPC.Close",
"price":  23.58,
"rsi": 46.235,
"ret": -0.0046433 
},
{
 "date":  -6462,
"name": "GSPC.Close",
"price":  23.48,
"rsi": 43.305,
"ret": -0.0042409 
},
{
 "date":  -6461,
"name": "GSPC.Close",
"price":  23.43,
"rsi": 40.775,
"ret": -0.0021295 
},
{
 "date":  -6460,
"name": "GSPC.Close",
"price":  23.54,
"rsi": 39.532,
"ret": 0.0046948 
},
{
 "date":  -6457,
"name": "GSPC.Close",
"price":  23.55,
"rsi": 43.607,
"ret": 0.00042481 
},
{
 "date":  -6456,
"name": "GSPC.Close",
"price":  23.49,
"rsi": 43.976,
"ret": -0.0025478 
},
{
 "date":  -6455,
"name": "GSPC.Close",
"price":  23.32,
"rsi":  42.19,
"ret": -0.0072371 
},
{
 "date":  -6454,
"name": "GSPC.Close",
"price":  23.17,
"rsi": 37.536,
"ret": -0.0064322 
},
{
 "date":  -6453,
"name": "GSPC.Close",
"price":  23.56,
"rsi": 33.975,
"ret": 0.016832 
},
{
 "date":  -6450,
"name": "GSPC.Close",
"price":  23.66,
"rsi": 47.832,
"ret": 0.0042445 
},
{
 "date":  -6449,
"name": "GSPC.Close",
"price":  23.67,
"rsi":  50.69,
"ret": 0.00042265 
},
{
 "date":  -6448,
"name": "GSPC.Close",
"price":  23.81,
"rsi": 50.979,
"ret": 0.0059147 
},
{
 "date":  -6447,
"name": "GSPC.Close",
"price":  23.86,
"rsi": 54.961,
"ret": 0.0021 
},
{
 "date":  -6446,
"name": "GSPC.Close",
"price":  23.84,
"rsi": 56.326,
"ret": -0.00083822 
},
{
 "date":  -6443,
"name": "GSPC.Close",
"price":  23.75,
"rsi":   55.6,
"ret": -0.0037752 
},
{
 "date":  -6442,
"name": "GSPC.Close",
"price":  23.78,
"rsi": 52.333,
"ret": 0.0012632 
},
{
 "date":  -6441,
"name": "GSPC.Close",
"price":  23.68,
"rsi": 53.318,
"ret": -0.0042052 
},
{
 "date":  -6440,
"name": "GSPC.Close",
"price":   23.6,
"rsi": 49.636,
"ret": -0.0033784 
},
{
 "date":  -6439,
"name": "GSPC.Close",
"price":  23.56,
"rsi":  46.85,
"ret": -0.0016949 
},
{
 "date":  -6436,
"name": "GSPC.Close",
"price":  23.61,
"rsi": 45.475,
"ret": 0.0021222 
},
{
 "date":  -6435,
"name": "GSPC.Close",
"price":  23.74,
"rsi": 47.547,
"ret": 0.0055061 
},
{
 "date":  -6434,
"name": "GSPC.Close",
"price":  23.78,
"rsi": 52.591,
"ret": 0.0016849 
},
{
 "date":  -6433,
"name": "GSPC.Close",
"price":  23.91,
"rsi": 54.055,
"ret": 0.0054668 
},
{
 "date":  -6432,
"name": "GSPC.Close",
"price":  23.89,
"rsi": 58.537,
"ret": -0.00083647 
},
{
 "date":  -6429,
"name": "GSPC.Close",
"price":  23.94,
"rsi": 57.606,
"ret": 0.0020929 
},
{
 "date":  -6428,
"name": "GSPC.Close",
"price":  23.88,
"rsi": 59.347,
"ret": -0.0025063 
},
{
 "date":  -6427,
"name": "GSPC.Close",
"price":  23.84,
"rsi": 56.356,
"ret": -0.001675 
},
{
 "date":  -6426,
"name": "GSPC.Close",
"price":  23.86,
"rsi": 54.389,
"ret": 0.00083893 
},
{
 "date":  -6422,
"name": "GSPC.Close",
"price":   23.8,
"rsi":  55.23,
"ret": -0.0025147 
},
{
 "date":  -6421,
"name": "GSPC.Close",
"price":  23.78,
"rsi": 52.123,
"ret": -0.00084034 
},
{
 "date":  -6420,
"name": "GSPC.Close",
"price":  23.95,
"rsi": 51.091,
"ret": 0.0071489 
},
{
 "date":  -6419,
"name": "GSPC.Close",
"price":   24.1,
"rsi": 58.595,
"ret": 0.006263 
},
{
 "date":  -6418,
"name": "GSPC.Close",
"price":  24.26,
"rsi": 63.863,
"ret": 0.006639 
},
{
 "date":  -6415,
"name": "GSPC.Close",
"price":  24.37,
"rsi": 68.471,
"ret": 0.0045342 
},
{
 "date":  -6414,
"name": "GSPC.Close",
"price":  24.23,
"rsi": 71.191,
"ret": -0.0057448 
},
{
 "date":  -6413,
"name": "GSPC.Close",
"price":  24.31,
"rsi": 63.663,
"ret": 0.0033017 
},
{
 "date":  -6412,
"name": "GSPC.Close",
"price":  24.31,
"rsi": 65.883,
"ret":      0 
},
{
 "date":  -6411,
"name": "GSPC.Close",
"price":  24.37,
"rsi": 65.883,
"ret": 0.0024681 
},
{
 "date":  -6408,
"name": "GSPC.Close",
"price":   24.3,
"rsi": 67.605,
"ret": -0.0028724 
},
{
 "date":  -6407,
"name": "GSPC.Close",
"price":  24.33,
"rsi": 63.574,
"ret": 0.0012346 
},
{
 "date":  -6406,
"name": "GSPC.Close",
"price":  24.43,
"rsi":  64.55,
"ret": 0.0041102 
},
{
 "date":  -6405,
"name": "GSPC.Close",
"price":  24.51,
"rsi": 67.659,
"ret": 0.0032747 
},
{
 "date":  -6404,
"name": "GSPC.Close",
"price":  24.59,
"rsi": 69.931,
"ret": 0.003264 
},
{
 "date":  -6401,
"name": "GSPC.Close",
"price":  24.56,
"rsi": 72.045,
"ret": -0.00122 
},
{
 "date":  -6400,
"name": "GSPC.Close",
"price":   24.6,
"rsi": 70.056,
"ret": 0.0016287 
},
{
 "date":  -6399,
"name": "GSPC.Close",
"price":  24.66,
"rsi": 71.198,
"ret": 0.002439 
},
{
 "date":  -6398,
"name": "GSPC.Close",
"price":  24.75,
"rsi":  72.87,
"ret": 0.0036496 
},
{
 "date":  -6397,
"name": "GSPC.Close",
"price":  24.83,
"rsi": 75.195,
"ret": 0.0032323 
},
{
 "date":  -6394,
"name": "GSPC.Close",
"price":  24.96,
"rsi": 77.076,
"ret": 0.0052356 
},
{
 "date":  -6393,
"name": "GSPC.Close",
"price":  25.12,
"rsi": 79.762,
"ret": 0.0064103 
},
{
 "date":  -6392,
"name": "GSPC.Close",
"price":  25.06,
"rsi": 82.483,
"ret": -0.0023885 
},
{
 "date":  -6391,
"name": "GSPC.Close",
"price":  25.05,
"rsi": 78.236,
"ret": -0.00039904 
},
{
 "date":  -6387,
"name": "GSPC.Close",
"price":  24.97,
"rsi": 77.519,
"ret": -0.0031936 
},
{
 "date":  -6386,
"name": "GSPC.Close",
"price":  24.96,
"rsi": 71.851,
"ret": -0.00040048 
},
{
 "date":  -6385,
"name": "GSPC.Close",
"price":  24.86,
"rsi":  71.15,
"ret": -0.0040064 
},
{
 "date":  -6384,
"name": "GSPC.Close",
"price":  24.81,
"rsi": 64.391,
"ret": -0.0020113 
},
{
 "date":  -6383,
"name": "GSPC.Close",
"price":  24.98,
"rsi": 61.257,
"ret": 0.0068521 
},
{
 "date":  -6380,
"name": "GSPC.Close",
"price":  25.03,
"rsi": 67.117,
"ret": 0.0020016 
},
{
 "date":  -6379,
"name": "GSPC.Close",
"price":  25.16,
"rsi":  68.62,
"ret": 0.0051938 
},
{
 "date":  -6378,
"name": "GSPC.Close",
"price":  25.16,
"rsi": 72.181,
"ret":      0 
},
{
 "date":  -6377,
"name": "GSPC.Close",
"price":  25.05,
"rsi": 72.181,
"ret": -0.004372 
},
{
 "date":  -6376,
"name": "GSPC.Close",
"price":  24.85,
"rsi": 64.948,
"ret": -0.007984 
},
{
 "date":  -6373,
"name": "GSPC.Close",
"price":  24.95,
"rsi": 54.296,
"ret": 0.0040241 
},
{
 "date":  -6372,
"name": "GSPC.Close",
"price":     25,
"rsi": 58.005,
"ret": 0.002004 
},
{
 "date":  -6371,
"name": "GSPC.Close",
"price":  25.11,
"rsi": 59.763,
"ret": 0.0044 
},
{
 "date":  -6370,
"name": "GSPC.Close",
"price":  25.24,
"rsi": 63.394,
"ret": 0.0051772 
},
{
 "date":  -6369,
"name": "GSPC.Close",
"price":  25.16,
"rsi": 67.165,
"ret": -0.0031696 
},
{
 "date":  -6366,
"name": "GSPC.Close",
"price":   25.2,
"rsi": 62.873,
"ret": 0.0015898 
},
{
 "date":  -6365,
"name": "GSPC.Close",
"price":  25.26,
"rsi": 64.108,
"ret": 0.002381 
},
{
 "date":  -6364,
"name": "GSPC.Close",
"price":  25.37,
"rsi": 65.938,
"ret": 0.0043547 
},
{
 "date":  -6363,
"name": "GSPC.Close",
"price":   25.4,
"rsi": 69.054,
"ret": 0.0011825 
},
{
 "date":  -6362,
"name": "GSPC.Close",
"price":  25.45,
"rsi": 69.864,
"ret": 0.0019685 
},
{
 "date":  -6359,
"name": "GSPC.Close",
"price":  25.43,
"rsi": 71.216,
"ret": -0.00078585 
},
{
 "date":  -6358,
"name": "GSPC.Close",
"price":  25.46,
"rsi": 69.866,
"ret": 0.0011797 
},
{
 "date":  -6357,
"name": "GSPC.Close",
"price":  25.44,
"rsi": 70.761,
"ret": -0.00078555 
},
{
 "date":  -6356,
"name": "GSPC.Close",
"price":  25.52,
"rsi": 69.283,
"ret": 0.0031447 
},
{
 "date":  -6355,
"name": "GSPC.Close",
"price":  25.55,
"rsi": 71.819,
"ret": 0.0011755 
},
{
 "date":  -6352,
"name": "GSPC.Close",
"price":  25.52,
"rsi": 72.728,
"ret": -0.0011742 
},
{
 "date":  -6351,
"name": "GSPC.Close",
"price":  25.31,
"rsi": 70.286,
"ret": -0.0082288 
},
{
 "date":  -6350,
"name": "GSPC.Close",
"price":  25.28,
"rsi": 56.089,
"ret": -0.0011853 
},
{
 "date":  -6349,
"name": "GSPC.Close",
"price":  25.28,
"rsi": 54.399,
"ret":      0 
},
{
 "date":  -6348,
"name": "GSPC.Close",
"price":   25.2,
"rsi": 54.399,
"ret": -0.0031646 
},
{
 "date":  -6345,
"name": "GSPC.Close",
"price":  24.94,
"rsi": 49.761,
"ret": -0.010317 
},
{
 "date":  -6344,
"name": "GSPC.Close",
"price":  24.89,
"rsi": 38.324,
"ret": -0.0020048 
},
{
 "date":  -6343,
"name": "GSPC.Close",
"price":  24.95,
"rsi": 36.583,
"ret": 0.0024106 
},
{
 "date":  -6342,
"name": "GSPC.Close",
"price":  24.98,
"rsi":   40.1,
"ret": 0.0012024 
},
{
 "date":  -6341,
"name": "GSPC.Close",
"price":  24.99,
"rsi": 41.837,
"ret": 0.00040032 
},
{
 "date":  -6338,
"name": "GSPC.Close",
"price":  24.87,
"rsi": 42.436,
"ret": -0.0048019 
},
{
 "date":  -6337,
"name": "GSPC.Close",
"price":  24.83,
"rsi":  37.45,
"ret": -0.0016084 
},
{
 "date":  -6336,
"name": "GSPC.Close",
"price":  24.94,
"rsi": 35.935,
"ret": 0.0044301 
},
{
 "date":  -6335,
"name": "GSPC.Close",
"price":  24.97,
"rsi": 42.791,
"ret": 0.0012029 
},
{
 "date":  -6334,
"name": "GSPC.Close",
"price":  25.03,
"rsi": 44.535,
"ret": 0.0024029 
},
{
 "date":  -6330,
"name": "GSPC.Close",
"price":  25.15,
"rsi": 47.951,
"ret": 0.0047942 
},
{
 "date":  -6329,
"name": "GSPC.Close",
"price":  25.25,
"rsi": 54.048,
"ret": 0.0039761 
},
{
 "date":  -6328,
"name": "GSPC.Close",
"price":  25.24,
"rsi": 58.419,
"ret": -0.00039604 
},
{
 "date":  -6327,
"name": "GSPC.Close",
"price":  25.21,
"rsi": 57.826,
"ret": -0.0011886 
},
{
 "date":  -6324,
"name": "GSPC.Close",
"price":  25.11,
"rsi": 55.992,
"ret": -0.0039667 
},
{
 "date":  -6323,
"name": "GSPC.Close",
"price":  24.86,
"rsi": 50.268,
"ret": -0.0099562 
},
{
 "date":  -6322,
"name": "GSPC.Close",
"price":  24.69,
"rsi": 39.419,
"ret": -0.0068383 
},
{
 "date":  -6321,
"name": "GSPC.Close",
"price":  24.72,
"rsi": 34.039,
"ret": 0.0012151 
},
{
 "date":  -6320,
"name": "GSPC.Close",
"price":  24.71,
"rsi": 35.707,
"ret": -0.00040453 
},
{
 "date":  -6317,
"name": "GSPC.Close",
"price":  24.45,
"rsi": 35.386,
"ret": -0.010522 
},
{
 "date":  -6316,
"name": "GSPC.Close",
"price":  24.53,
"rsi": 28.267,
"ret": 0.003272 
},
{
 "date":  -6315,
"name": "GSPC.Close",
"price":  24.58,
"rsi":  32.75,
"ret": 0.0020383 
},
{
 "date":  -6314,
"name": "GSPC.Close",
"price":  24.51,
"rsi": 35.465,
"ret": -0.0028478 
},
{
 "date":  -6313,
"name": "GSPC.Close",
"price":  24.57,
"rsi":  33.43,
"ret": 0.002448 
},
{
 "date":  -6310,
"name": "GSPC.Close",
"price":  24.59,
"rsi": 36.778,
"ret": 0.000814 
},
{
 "date":  -6309,
"name": "GSPC.Close",
"price":   24.7,
"rsi": 37.899,
"ret": 0.0044734 
},
{
 "date":  -6308,
"name": "GSPC.Close",
"price":  24.79,
"rsi": 43.802,
"ret": 0.0036437 
},
{
 "date":  -6307,
"name": "GSPC.Close",
"price":  24.81,
"rsi": 48.145,
"ret": 0.00080678 
},
{
 "date":  -6306,
"name": "GSPC.Close",
"price":  24.73,
"rsi": 49.086,
"ret": -0.0032245 
},
{
 "date":  -6303,
"name": "GSPC.Close",
"price":  24.68,
"rsi": 45.525,
"ret": -0.0020218 
},
{
 "date":  -6302,
"name": "GSPC.Close",
"price":  24.54,
"rsi": 43.406,
"ret": -0.0056726 
},
{
 "date":  -6301,
"name": "GSPC.Close",
"price":  24.48,
"rsi": 38.063,
"ret": -0.002445 
},
{
 "date":  -6300,
"name": "GSPC.Close",
"price":  24.52,
"rsi": 36.016,
"ret": 0.001634 
},
{
 "date":  -6299,
"name": "GSPC.Close",
"price":   24.5,
"rsi": 38.394,
"ret": -0.00081566 
},
{
 "date":  -6296,
"name": "GSPC.Close",
"price":  24.44,
"rsi": 37.641,
"ret": -0.002449 
},
{
 "date":  -6295,
"name": "GSPC.Close",
"price":   24.4,
"rsi": 35.397,
"ret": -0.0016367 
},
{
 "date":  -6294,
"name": "GSPC.Close",
"price":  24.58,
"rsi": 33.945,
"ret": 0.007377 
},
{
 "date":  -6293,
"name": "GSPC.Close",
"price":  24.57,
"rsi": 44.902,
"ret": -0.00040683 
},
{
 "date":  -6292,
"name": "GSPC.Close",
"price":  24.55,
"rsi": 44.461,
"ret": -0.000814 
},
{
 "date":  -6288,
"name": "GSPC.Close",
"price":  24.48,
"rsi": 43.539,
"ret": -0.0028513 
},
{
 "date":  -6287,
"name": "GSPC.Close",
"price":  24.06,
"rsi": 40.384,
"ret": -0.017157 
},
{
 "date":  -6286,
"name": "GSPC.Close",
"price":  23.91,
"rsi": 27.505,
"ret": -0.0062344 
},
{
 "date":  -6285,
"name": "GSPC.Close",
"price":   24.2,
"rsi":   24.5,
"ret": 0.012129 
},
{
 "date":  -6282,
"name": "GSPC.Close",
"price":  24.13,
"rsi": 38.492,
"ret": -0.0028926 
},
{
 "date":  -6281,
"name": "GSPC.Close",
"price":  24.07,
"rsi": 36.723,
"ret": -0.0024865 
},
{
 "date":  -6280,
"name": "GSPC.Close",
"price":   23.8,
"rsi": 35.228,
"ret": -0.011217 
},
{
 "date":  -6279,
"name": "GSPC.Close",
"price":  23.87,
"rsi": 29.425,
"ret": 0.0029412 
},
{
 "date":  -6278,
"name": "GSPC.Close",
"price":  24.03,
"rsi": 32.528,
"ret": 0.006703 
},
{
 "date":  -6275,
"name": "GSPC.Close",
"price":  24.09,
"rsi": 39.118,
"ret": 0.0024969 
},
{
 "date":  -6274,
"name": "GSPC.Close",
"price":  24.13,
"rsi": 41.428,
"ret": 0.0016604 
},
{
 "date":  -6273,
"name": "GSPC.Close",
"price":  24.15,
"rsi": 42.982,
"ret": 0.00082884 
},
{
 "date":  -6272,
"name": "GSPC.Close",
"price":  24.15,
"rsi": 43.784,
"ret":      0 
},
{
 "date":  -6271,
"name": "GSPC.Close",
"price":  24.52,
"rsi": 43.784,
"ret": 0.015321 
},
{
 "date":  -6268,
"name": "GSPC.Close",
"price":   24.6,
"rsi": 56.826,
"ret": 0.0032626 
},
{
 "date":  -6266,
"name": "GSPC.Close",
"price":  24.67,
"rsi": 59.039,
"ret": 0.0028455 
},
{
 "date":  -6265,
"name": "GSPC.Close",
"price":  24.77,
"rsi": 60.926,
"ret": 0.0040535 
},
{
 "date":  -6264,
"name": "GSPC.Close",
"price":  24.78,
"rsi": 63.512,
"ret": 0.00040371 
},
{
 "date":  -6261,
"name": "GSPC.Close",
"price":  24.77,
"rsi": 63.771,
"ret": -0.00040355 
},
{
 "date":  -6259,
"name": "GSPC.Close",
"price":  24.65,
"rsi": 63.288,
"ret": -0.0048446 
},
{
 "date":  -6258,
"name": "GSPC.Close",
"price":  24.71,
"rsi": 57.653,
"ret": 0.0024341 
},
{
 "date":  -6257,
"name": "GSPC.Close",
"price":  24.75,
"rsi":  59.59,
"ret": 0.0016188 
},
{
 "date":  -6254,
"name": "GSPC.Close",
"price":   24.8,
"rsi": 60.875,
"ret": 0.0020202 
},
{
 "date":  -6253,
"name": "GSPC.Close",
"price":  25.16,
"rsi": 62.482,
"ret": 0.014516 
},
{
 "date":  -6252,
"name": "GSPC.Close",
"price":  25.33,
"rsi": 71.541,
"ret": 0.0067568 
},
{
 "date":  -6251,
"name": "GSPC.Close",
"price":  25.28,
"rsi": 74.654,
"ret": -0.0019739 
},
{
 "date":  -6250,
"name": "GSPC.Close",
"price":  25.27,
"rsi": 72.154,
"ret": -0.00039557 
},
{
 "date":  -6247,
"name": "GSPC.Close",
"price":  25.42,
"rsi": 71.638,
"ret": 0.0059359 
},
{
 "date":  -6246,
"name": "GSPC.Close",
"price":  25.36,
"rsi": 74.578,
"ret": -0.0023603 
},
{
 "date":  -6245,
"name": "GSPC.Close",
"price":  25.52,
"rsi":  71.39,
"ret": 0.0063091 
},
{
 "date":  -6243,
"name": "GSPC.Close",
"price":  25.66,
"rsi": 74.518,
"ret": 0.0054859 
},
{
 "date":  -6240,
"name": "GSPC.Close",
"price":  25.68,
"rsi": 76.898,
"ret": 0.00077942 
},
{
 "date":  -6239,
"name": "GSPC.Close",
"price":  25.74,
"rsi": 77.226,
"ret": 0.0023364 
},
{
 "date":  -6238,
"name": "GSPC.Close",
"price":  25.71,
"rsi": 78.222,
"ret": -0.0011655 
},
{
 "date":  -6237,
"name": "GSPC.Close",
"price":  25.61,
"rsi": 76.421,
"ret": -0.0038895 
},
{
 "date":  -6236,
"name": "GSPC.Close",
"price":  25.62,
"rsi": 70.587,
"ret": 0.00039047 
},
{
 "date":  -6233,
"name": "GSPC.Close",
"price":  25.76,
"rsi": 70.827,
"ret": 0.0054645 
},
{
 "date":  -6232,
"name": "GSPC.Close",
"price":  25.93,
"rsi": 74.021,
"ret": 0.0065994 
},
{
 "date":  -6231,
"name": "GSPC.Close",
"price":  25.98,
"rsi": 77.275,
"ret": 0.0019283 
},
{
 "date":  -6230,
"name": "GSPC.Close",
"price":  25.96,
"rsi": 78.142,
"ret": -0.00076982 
},
{
 "date":  -6229,
"name": "GSPC.Close",
"price":  26.04,
"rsi": 76.878,
"ret": 0.0030817 
},
{
 "date":  -6226,
"name": "GSPC.Close",
"price":  26.04,
"rsi": 78.384,
"ret":      0 
},
{
 "date":  -6225,
"name": "GSPC.Close",
"price":  26.07,
"rsi": 78.384,
"ret": 0.0011521 
},
{
 "date":  -6224,
"name": "GSPC.Close",
"price":  26.04,
"rsi": 78.979,
"ret": -0.0011507 
},
{
 "date":  -6223,
"name": "GSPC.Close",
"price":  26.03,
"rsi": 76.704,
"ret": -0.00038402 
},
{
 "date":  -6222,
"name": "GSPC.Close",
"price":  26.15,
"rsi": 75.919,
"ret": 0.0046101 
},
{
 "date":  -6219,
"name": "GSPC.Close",
"price":   26.3,
"rsi": 78.732,
"ret": 0.0057361 
},
{
 "date":  -6218,
"name": "GSPC.Close",
"price":  26.19,
"rsi": 81.622,
"ret": -0.0041825 
},
{
 "date":  -6217,
"name": "GSPC.Close",
"price":  26.21,
"rsi": 73.712,
"ret": 0.00076365 
},
{
 "date":  -6215,
"name": "GSPC.Close",
"price":  26.25,
"rsi": 74.201,
"ret": 0.0015261 
},
{
 "date":  -6212,
"name": "GSPC.Close",
"price":   26.4,
"rsi": 75.196,
"ret": 0.0057143 
},
{
 "date":  -6211,
"name": "GSPC.Close",
"price":  26.59,
"rsi": 78.539,
"ret": 0.007197 
},
{
 "date":  -6210,
"name": "GSPC.Close",
"price":  26.57,
"rsi": 81.871,
"ret": -0.00075216 
},
{
 "date":  -6208,
"name": "GSPC.Close",
"price":  26.54,
"rsi": 80.455,
"ret": -0.0011291 
},
{
 "date":  -6205,
"name": "GSPC.Close",
"price":  26.66,
"rsi": 78.268,
"ret": 0.0045215 
},
{
 "date":  -6204,
"name": "GSPC.Close",
"price":  26.48,
"rsi": 80.546,
"ret": -0.0067517 
},
{
 "date":  -6203,
"name": "GSPC.Close",
"price":  26.37,
"rsi": 68.882,
"ret": -0.0041541 
},
{
 "date":  -6202,
"name": "GSPC.Close",
"price":  26.33,
"rsi": 62.889,
"ret": -0.0015169 
},
{
 "date":  -6201,
"name": "GSPC.Close",
"price":  26.08,
"rsi": 60.817,
"ret": -0.0094949 
},
{
 "date":  -6198,
"name": "GSPC.Close",
"price":  25.86,
"rsi": 49.777,
"ret": -0.0084356 
},
{
 "date":  -6197,
"name": "GSPC.Close",
"price":  26.02,
"rsi": 42.471,
"ret": 0.0061872 
},
{
 "date":  -6196,
"name": "GSPC.Close",
"price":  26.08,
"rsi": 48.403,
"ret": 0.0023059 
},
{
 "date":  -6195,
"name": "GSPC.Close",
"price":  26.13,
"rsi": 50.465,
"ret": 0.0019172 
},
{
 "date":  -6194,
"name": "GSPC.Close",
"price":  26.02,
"rsi": 52.181,
"ret": -0.0042097 
},
{
 "date":  -6191,
"name": "GSPC.Close",
"price":  26.01,
"rsi": 48.224,
"ret": -0.00038432 
},
{
 "date":  -6190,
"name": "GSPC.Close",
"price":  26.14,
"rsi": 47.869,
"ret": 0.0049981 
},
{
 "date":  -6189,
"name": "GSPC.Close",
"price":  26.09,
"rsi": 52.744,
"ret": -0.0019128 
},
{
 "date":  -6188,
"name": "GSPC.Close",
"price":  26.12,
"rsi": 50.777,
"ret": 0.0011499 
},
{
 "date":  -6187,
"name": "GSPC.Close",
"price":  26.07,
"rsi": 51.935,
"ret": -0.0019142 
},
{
 "date":  -6184,
"name": "GSPC.Close",
"price":  26.02,
"rsi": 49.831,
"ret": -0.0019179 
},
{
 "date":  -6183,
"name": "GSPC.Close",
"price":  26.05,
"rsi": 47.747,
"ret": 0.001153 
},
{
 "date":  -6182,
"name": "GSPC.Close",
"price":  26.13,
"rsi": 49.122,
"ret": 0.003071 
},
{
 "date":  -6181,
"name": "GSPC.Close",
"price":   26.2,
"rsi": 52.696,
"ret": 0.0026789 
},
{
 "date":  -6180,
"name": "GSPC.Close",
"price":  26.38,
"rsi": 55.632,
"ret": 0.0068702 
},
{
 "date":  -6177,
"name": "GSPC.Close",
"price":  26.51,
"rsi": 62.141,
"ret": 0.004928 
},
{
 "date":  -6176,
"name": "GSPC.Close",
"price":  26.54,
"rsi": 66.018,
"ret": 0.0011316 
},
{
 "date":  -6175,
"name": "GSPC.Close",
"price":  26.42,
"rsi": 66.861,
"ret": -0.0045215 
},
{
 "date":  -6174,
"name": "GSPC.Close",
"price":  26.15,
"rsi": 60.403,
"ret": -0.01022 
},
{
 "date":  -6173,
"name": "GSPC.Close",
"price":  26.51,
"rsi": 48.948,
"ret": 0.013767 
},
{
 "date":  -6170,
"name": "GSPC.Close",
"price":  25.69,
"rsi": 59.875,
"ret": -0.030932 
},
{
 "date":  -6169,
"name": "GSPC.Close",
"price":  25.62,
"rsi": 39.261,
"ret": -0.0027248 
},
{
 "date":  -6168,
"name": "GSPC.Close",
"price":  25.64,
"rsi": 38.057,
"ret": 0.00078064 
},
{
 "date":  -6166,
"name": "GSPC.Close",
"price":  25.74,
"rsi": 38.636,
"ret": 0.0039002 
},
{
 "date":  -6163,
"name": "GSPC.Close",
"price":  25.65,
"rsi": 41.578,
"ret": -0.0034965 
},
{
 "date":  -6162,
"name": "GSPC.Close",
"price":   25.5,
"rsi": 39.732,
"ret": -0.005848 
},
{
 "date":  -6161,
"name": "GSPC.Close",
"price":  25.48,
"rsi": 36.799,
"ret": -0.00078431 
},
{
 "date":  -6160,
"name": "GSPC.Close",
"price":  25.57,
"rsi": 36.413,
"ret": 0.0035322 
},
{
 "date":  -6159,
"name": "GSPC.Close",
"price":  25.63,
"rsi": 39.489,
"ret": 0.0023465 
},
{
 "date":  -6155,
"name": "GSPC.Close",
"price":  25.75,
"rsi": 41.519,
"ret": 0.004682 
},
{
 "date":  -6154,
"name": "GSPC.Close",
"price":  25.91,
"rsi": 45.461,
"ret": 0.0062136 
},
{
 "date":  -6153,
"name": "GSPC.Close",
"price":  25.95,
"rsi": 50.274,
"ret": 0.0015438 
},
{
 "date":  -6152,
"name": "GSPC.Close",
"price":   25.9,
"rsi": 51.428,
"ret": -0.0019268 
},
{
 "date":  -6149,
"name": "GSPC.Close",
"price":  25.93,
"rsi":  49.87,
"ret": 0.0011583 
},
{
 "date":  -6148,
"name": "GSPC.Close",
"price":     26,
"rsi": 50.833,
"ret": 0.0026996 
},
{
 "date":  -6147,
"name": "GSPC.Close",
"price":  25.78,
"rsi": 53.096,
"ret": -0.0084615 
},
{
 "date":  -6146,
"name": "GSPC.Close",
"price":  25.79,
"rsi":  45.94,
"ret": 0.0003879 
},
{
 "date":  -6145,
"name": "GSPC.Close",
"price":  25.84,
"rsi": 46.294,
"ret": 0.0019387 
},
{
 "date":  -6142,
"name": "GSPC.Close",
"price":  25.83,
"rsi": 48.125,
"ret": -0.000387 
},
{
 "date":  -6141,
"name": "GSPC.Close",
"price":  25.91,
"rsi": 47.774,
"ret": 0.0030972 
},
{
 "date":  -6140,
"name": "GSPC.Close",
"price":  26.12,
"rsi":  50.86,
"ret": 0.008105 
},
{
 "date":  -6139,
"name": "GSPC.Close",
"price":  26.13,
"rsi": 57.893,
"ret": 0.00038285 
},
{
 "date":  -6138,
"name": "GSPC.Close",
"price":  26.18,
"rsi":   58.2,
"ret": 0.0019135 
},
{
 "date":  -6135,
"name": "GSPC.Close",
"price":  26.22,
"rsi": 59.778,
"ret": 0.0015279 
},
{
 "date":  -6134,
"name": "GSPC.Close",
"price":  26.33,
"rsi": 61.045,
"ret": 0.0041953 
},
{
 "date":  -6133,
"name": "GSPC.Close",
"price":  26.24,
"rsi": 64.369,
"ret": -0.0034182 
},
{
 "date":  -6132,
"name": "GSPC.Close",
"price":  26.22,
"rsi": 59.868,
"ret": -0.0007622 
},
{
 "date":  -6131,
"name": "GSPC.Close",
"price":  26.18,
"rsi": 58.882,
"ret": -0.0015256 
},
{
 "date":  -6128,
"name": "GSPC.Close",
"price":  26.02,
"rsi": 56.866,
"ret": -0.0061115 
},
{
 "date":  -6127,
"name": "GSPC.Close",
"price":  26.17,
"rsi": 49.557,
"ret": 0.0057648 
},
{
 "date":  -6126,
"name": "GSPC.Close",
"price":   26.1,
"rsi": 55.351,
"ret": -0.0026748 
},
{
 "date":  -6125,
"name": "GSPC.Close",
"price":  25.95,
"rsi":  52.33,
"ret": -0.0057471 
},
{
 "date":  -6124,
"name": "GSPC.Close",
"price":  25.99,
"rsi": 46.477,
"ret": 0.0015414 
},
{
 "date":  -6121,
"name": "GSPC.Close",
"price":  25.61,
"rsi": 48.143,
"ret": -0.014621 
},
{
 "date":  -6120,
"name": "GSPC.Close",
"price":  25.29,
"rsi": 36.516,
"ret": -0.012495 
},
{
 "date":  -6119,
"name": "GSPC.Close",
"price":  25.25,
"rsi": 29.955,
"ret": -0.0015817 
},
{
 "date":  -6118,
"name": "GSPC.Close",
"price":  25.23,
"rsi": 29.248,
"ret": -0.00079208 
},
{
 "date":  -6114,
"name": "GSPC.Close",
"price":  24.61,
"rsi": 28.881,
"ret": -0.024574 
},
{
 "date":  -6113,
"name": "GSPC.Close",
"price":  24.71,
"rsi":  20.35,
"ret": 0.0040634 
},
{
 "date":  -6112,
"name": "GSPC.Close",
"price":  24.93,
"rsi": 24.237,
"ret": 0.0089033 
},
{
 "date":  -6111,
"name": "GSPC.Close",
"price":  24.88,
"rsi": 32.089,
"ret": -0.0020056 
},
{
 "date":  -6110,
"name": "GSPC.Close",
"price":  24.82,
"rsi": 31.295,
"ret": -0.0024116 
},
{
 "date":  -6107,
"name": "GSPC.Close",
"price":  24.77,
"rsi": 30.326,
"ret": -0.0020145 
},
{
 "date":  -6106,
"name": "GSPC.Close",
"price":  24.86,
"rsi": 29.505,
"ret": 0.0036334 
},
{
 "date":  -6105,
"name": "GSPC.Close",
"price":  24.96,
"rsi": 33.018,
"ret": 0.0040225 
},
{
 "date":  -6104,
"name": "GSPC.Close",
"price":  24.91,
"rsi": 36.786,
"ret": -0.0020032 
},
{
 "date":  -6103,
"name": "GSPC.Close",
"price":  24.62,
"rsi": 35.705,
"ret": -0.011642 
},
{
 "date":  -6100,
"name": "GSPC.Close",
"price":  24.73,
"rsi": 30.164,
"ret": 0.0044679 
},
{
 "date":  -6099,
"name": "GSPC.Close",
"price":  24.67,
"rsi": 34.327,
"ret": -0.0024262 
},
{
 "date":  -6098,
"name": "GSPC.Close",
"price":  24.46,
"rsi": 33.166,
"ret": -0.0085124 
},
{
 "date":  -6097,
"name": "GSPC.Close",
"price":  24.19,
"rsi": 29.415,
"ret": -0.011038 
},
{
 "date":  -6096,
"name": "GSPC.Close",
"price":   24.2,
"rsi": 25.433,
"ret": 0.00041339 
},
{
 "date":  -6093,
"name": "GSPC.Close",
"price":  24.34,
"rsi": 25.833,
"ret": 0.0057851 
},
{
 "date":  -6092,
"name": "GSPC.Close",
"price":  24.52,
"rsi": 31.389,
"ret": 0.0073952 
},
{
 "date":  -6091,
"name": "GSPC.Close",
"price":  24.68,
"rsi": 37.837,
"ret": 0.0065253 
},
{
 "date":  -6090,
"name": "GSPC.Close",
"price":  24.62,
"rsi": 42.968,
"ret": -0.0024311 
},
{
 "date":  -6089,
"name": "GSPC.Close",
"price":  24.73,
"rsi": 41.582,
"ret": 0.0044679 
},
{
 "date":  -6086,
"name": "GSPC.Close",
"price":     25,
"rsi": 45.079,
"ret": 0.010918 
},
{
 "date":  -6085,
"name": "GSPC.Close",
"price":  25.03,
"rsi": 52.584,
"ret": 0.0012 
},
{
 "date":  -6084,
"name": "GSPC.Close",
"price":     25,
"rsi": 53.346,
"ret": -0.0011986 
},
{
 "date":  -6083,
"name": "GSPC.Close",
"price":   24.9,
"rsi": 52.438,
"ret": -0.004 
},
{
 "date":  -6082,
"name": "GSPC.Close",
"price":   24.9,
"rsi": 49.417,
"ret":      0 
},
{
 "date":  -6079,
"name": "GSPC.Close",
"price":  24.91,
"rsi": 49.417,
"ret": 0.00040161 
},
{
 "date":  -6078,
"name": "GSPC.Close",
"price":  24.74,
"rsi": 49.753,
"ret": -0.0068246 
},
{
 "date":  -6077,
"name": "GSPC.Close",
"price":  24.71,
"rsi": 44.362,
"ret": -0.0012126 
},
{
 "date":  -6076,
"name": "GSPC.Close",
"price":  24.85,
"rsi": 43.467,
"ret": 0.0056657 
},
{
 "date":  -6075,
"name": "GSPC.Close",
"price":  24.84,
"rsi": 48.672,
"ret": -0.00040241 
},
{
 "date":  -6072,
"name": "GSPC.Close",
"price":  24.75,
"rsi": 48.329,
"ret": -0.0036232 
},
{
 "date":  -6071,
"name": "GSPC.Close",
"price":   24.7,
"rsi": 45.246,
"ret": -0.0020202 
},
{
 "date":  -6070,
"name": "GSPC.Close",
"price":  24.93,
"rsi": 43.582,
"ret": 0.0093117 
},
{
 "date":  -6069,
"name": "GSPC.Close",
"price":  25.06,
"rsi": 52.275,
"ret": 0.0052146 
},
{
 "date":  -6068,
"name": "GSPC.Close",
"price":  25.03,
"rsi": 56.367,
"ret": -0.0011971 
},
{
 "date":  -6065,
"name": "GSPC.Close",
"price":  24.99,
"rsi": 55.191,
"ret": -0.0015981 
},
{
 "date":  -6064,
"name": "GSPC.Close",
"price":  24.87,
"rsi": 53.586,
"ret": -0.0048019 
},
{
 "date":  -6063,
"name": "GSPC.Close",
"price":  24.64,
"rsi": 48.982,
"ret": -0.0092481 
},
{
 "date":  -6062,
"name": "GSPC.Close",
"price":  24.46,
"rsi": 41.605,
"ret": -0.0073052 
},
{
 "date":  -6061,
"name": "GSPC.Close",
"price":  24.54,
"rsi": 36.919,
"ret": 0.0032706 
},
{
 "date":  -6058,
"name": "GSPC.Close",
"price":  24.15,
"rsi": 40.146,
"ret": -0.015892 
},
{
 "date":  -6057,
"name": "GSPC.Close",
"price":  24.22,
"rsi": 31.646,
"ret": 0.0028986 
},
{
 "date":  -6056,
"name": "GSPC.Close",
"price":  24.18,
"rsi": 34.334,
"ret": -0.0016515 
},
{
 "date":  -6055,
"name": "GSPC.Close",
"price":  24.03,
"rsi": 33.523,
"ret": -0.0062035 
},
{
 "date":  -6054,
"name": "GSPC.Close",
"price":  24.09,
"rsi": 30.603,
"ret": 0.0024969 
},
{
 "date":  -6051,
"name": "GSPC.Close",
"price":  24.01,
"rsi": 33.113,
"ret": -0.0033209 
},
{
 "date":  -6050,
"name": "GSPC.Close",
"price":   23.6,
"rsi": 31.478,
"ret": -0.017076 
},
{
 "date":  -6049,
"name": "GSPC.Close",
"price":  23.54,
"rsi": 24.739,
"ret": -0.0025424 
},
{
 "date":  -6048,
"name": "GSPC.Close",
"price":  23.75,
"rsi": 23.932,
"ret": 0.008921 
},
{
 "date":  -6047,
"name": "GSPC.Close",
"price":  23.82,
"rsi": 32.265,
"ret": 0.0029474 
},
{
 "date":  -6044,
"name": "GSPC.Close",
"price":  23.62,
"rsi": 34.828,
"ret": -0.0083963 
},
{
 "date":  -6043,
"name": "GSPC.Close",
"price":  23.55,
"rsi": 31.196,
"ret": -0.0029636 
},
{
 "date":  -6042,
"name": "GSPC.Close",
"price":  23.85,
"rsi": 30.016,
"ret": 0.012739 
},
{
 "date":  -6041,
"name": "GSPC.Close",
"price":  23.84,
"rsi": 40.416,
"ret": -0.00041929 
},
{
 "date":  -6040,
"name": "GSPC.Close",
"price":  23.84,
"rsi": 40.202,
"ret":      0 
},
{
 "date":  -6037,
"name": "GSPC.Close",
"price":  23.96,
"rsi": 40.202,
"ret": 0.0050336 
},
{
 "date":  -6036,
"name": "GSPC.Close",
"price":  24.12,
"rsi": 44.314,
"ret": 0.0066778 
},
{
 "date":  -6035,
"name": "GSPC.Close",
"price":  24.09,
"rsi": 49.319,
"ret": -0.0012438 
},
{
 "date":  -6034,
"name": "GSPC.Close",
"price":  24.19,
"rsi":  48.44,
"ret": 0.0041511 
},
{
 "date":  -6033,
"name": "GSPC.Close",
"price":  24.21,
"rsi":  51.54,
"ret": 0.00082679 
},
{
 "date":  -6030,
"name": "GSPC.Close",
"price":  24.14,
"rsi":  52.16,
"ret": -0.0028914 
},
{
 "date":  -6029,
"name": "GSPC.Close",
"price":  24.14,
"rsi": 49.762,
"ret":      0 
},
{
 "date":  -6028,
"name": "GSPC.Close",
"price":  24.24,
"rsi": 49.762,
"ret": 0.0041425 
},
{
 "date":  -6027,
"name": "GSPC.Close",
"price":  24.31,
"rsi": 53.318,
"ret": 0.0028878 
},
{
 "date":  -6026,
"name": "GSPC.Close",
"price":  24.36,
"rsi": 55.683,
"ret": 0.0020568 
},
{
 "date":  -6023,
"name": "GSPC.Close",
"price":  24.38,
"rsi": 57.345,
"ret": 0.00082102 
},
{
 "date":  -6022,
"name": "GSPC.Close",
"price":  24.51,
"rsi": 58.023,
"ret": 0.0053322 
},
{
 "date":  -6021,
"name": "GSPC.Close",
"price":   24.5,
"rsi": 62.227,
"ret": -0.000408 
},
{
 "date":  -6020,
"name": "GSPC.Close",
"price":  24.43,
"rsi": 61.715,
"ret": -0.0028571 
},
{
 "date":  -6019,
"name": "GSPC.Close",
"price":  24.41,
"rsi": 58.111,
"ret": -0.00081867 
},
{
 "date":  -6016,
"name": "GSPC.Close",
"price":  24.17,
"rsi": 57.085,
"ret": -0.009832 
},
{
 "date":  -6015,
"name": "GSPC.Close",
"price":  24.08,
"rsi": 46.481,
"ret": -0.0037236 
},
{
 "date":  -6014,
"name": "GSPC.Close",
"price":  24.15,
"rsi": 43.237,
"ret": 0.002907 
},
{
 "date":  -6013,
"name": "GSPC.Close",
"price":  24.18,
"rsi": 46.372,
"ret": 0.0012422 
},
{
 "date":  -6012,
"name": "GSPC.Close",
"price":  24.35,
"rsi": 47.704,
"ret": 0.0070306 
},
{
 "date":  -6009,
"name": "GSPC.Close",
"price":  24.22,
"rsi": 54.592,
"ret": -0.0053388 
},
{
 "date":  -6008,
"name": "GSPC.Close",
"price":  24.16,
"rsi":  49.25,
"ret": -0.0024773 
},
{
 "date":  -6007,
"name": "GSPC.Close",
"price":  24.19,
"rsi": 46.966,
"ret": 0.0012417 
},
{
 "date":  -6006,
"name": "GSPC.Close",
"price":  24.23,
"rsi": 48.258,
"ret": 0.0016536 
},
{
 "date":  -6005,
"name": "GSPC.Close",
"price":  24.23,
"rsi": 50.007,
"ret":      0 
},
{
 "date":  -6002,
"name": "GSPC.Close",
"price":  24.07,
"rsi": 50.007,
"ret": -0.0066034 
},
{
 "date":  -6001,
"name": "GSPC.Close",
"price":  24.11,
"rsi": 43.228,
"ret": 0.0016618 
},
{
 "date":  -6000,
"name": "GSPC.Close",
"price":  24.26,
"rsi": 45.227,
"ret": 0.0062215 
},
{
 "date":  -5999,
"name": "GSPC.Close",
"price":  24.49,
"rsi": 52.046,
"ret": 0.0094806 
},
{
 "date":  -5998,
"name": "GSPC.Close",
"price":  24.75,
"rsi": 60.223,
"ret": 0.010617 
},
{
 "date":  -5995,
"name": "GSPC.Close",
"price":  24.84,
"rsi": 67.061,
"ret": 0.0036364 
},
{
 "date":  -5994,
"name": "GSPC.Close",
"price":  24.78,
"rsi": 69.045,
"ret": -0.0024155 
},
{
 "date":  -5993,
"name": "GSPC.Close",
"price":  24.68,
"rsi": 66.183,
"ret": -0.0040355 
},
{
 "date":  -5992,
"name": "GSPC.Close",
"price":   24.8,
"rsi": 61.601,
"ret": 0.0048622 
},
{
 "date":  -5991,
"name": "GSPC.Close",
"price":  24.78,
"rsi": 64.754,
"ret": -0.00080645 
},
{
 "date":  -5988,
"name": "GSPC.Close",
"price":  24.75,
"rsi": 63.814,
"ret": -0.0012107 
},
{
 "date":  -5987,
"name": "GSPC.Close",
"price":  24.72,
"rsi": 62.351,
"ret": -0.0012121 
},
{
 "date":  -5986,
"name": "GSPC.Close",
"price":  24.78,
"rsi": 60.848,
"ret": 0.0024272 
},
{
 "date":  -5985,
"name": "GSPC.Close",
"price":  24.73,
"rsi":  62.78,
"ret": -0.0020178 
},
{
 "date":  -5984,
"name": "GSPC.Close",
"price":  24.62,
"rsi": 60.118,
"ret": -0.004448 
},
{
 "date":  -5981,
"name": "GSPC.Close",
"price":  24.56,
"rsi":  54.63,
"ret": -0.002437 
},
{
 "date":  -5980,
"name": "GSPC.Close",
"price":  24.46,
"rsi": 51.849,
"ret": -0.0040717 
},
{
 "date":  -5979,
"name": "GSPC.Close",
"price":  24.31,
"rsi": 47.509,
"ret": -0.0061325 
},
{
 "date":  -5978,
"name": "GSPC.Close",
"price":  24.29,
"rsi":  41.85,
"ret": -0.00082271 
},
{
 "date":  -5977,
"name": "GSPC.Close",
"price":  24.35,
"rsi": 41.147,
"ret": 0.0024702 
},
{
 "date":  -5974,
"name": "GSPC.Close",
"price":  24.09,
"rsi": 44.179,
"ret": -0.010678 
},
{
 "date":  -5973,
"name": "GSPC.Close",
"price":  23.93,
"rsi": 35.615,
"ret": -0.0066418 
},
{
 "date":  -5972,
"name": "GSPC.Close",
"price":  23.86,
"rsi": 31.561,
"ret": -0.0029252 
},
{
 "date":  -5971,
"name": "GSPC.Close",
"price":  23.79,
"rsi": 29.954,
"ret": -0.0029338 
},
{
 "date":  -5970,
"name": "GSPC.Close",
"price":  23.74,
"rsi": 28.397,
"ret": -0.0021017 
},
{
 "date":  -5967,
"name": "GSPC.Close",
"price":  23.32,
"rsi": 27.306,
"ret": -0.017692 
},
{
 "date":  -5966,
"name": "GSPC.Close",
"price":  23.42,
"rsi":  20.26,
"ret": 0.0042882 
},
{
 "date":  -5965,
"name": "GSPC.Close",
"price":  23.56,
"rsi": 25.208,
"ret": 0.0059778 
},
{
 "date":  -5964,
"name": "GSPC.Close",
"price":  23.51,
"rsi": 31.607,
"ret": -0.0021222 
},
{
 "date":  -5963,
"name": "GSPC.Close",
"price":  23.57,
"rsi":   30.6,
"ret": 0.0025521 
},
{
 "date":  -5959,
"name": "GSPC.Close",
"price":  23.61,
"rsi": 33.344,
"ret": 0.0016971 
},
{
 "date":  -5958,
"name": "GSPC.Close",
"price":  23.65,
"rsi": 35.184,
"ret": 0.0016942 
},
{
 "date":  -5957,
"name": "GSPC.Close",
"price":  23.41,
"rsi": 37.056,
"ret": -0.010148 
},
{
 "date":  -5956,
"name": "GSPC.Close",
"price":  23.14,
"rsi":  31.23,
"ret": -0.011534 
},
{
 "date":  -5953,
"name": "GSPC.Close",
"price":  22.71,
"rsi": 26.233,
"ret": -0.018583 
},
{
 "date":  -5952,
"name": "GSPC.Close",
"price":   22.9,
"rsi": 20.584,
"ret": 0.0083664 
},
{
 "date":  -5951,
"name": "GSPC.Close",
"price":  23.01,
"rsi": 27.965,
"ret": 0.0048035 
},
{
 "date":  -5950,
"name": "GSPC.Close",
"price":  23.07,
"rsi": 31.911,
"ret": 0.0026076 
},
{
 "date":  -5949,
"name": "GSPC.Close",
"price":  22.95,
"rsi": 34.033,
"ret": -0.0052016 
},
{
 "date":  -5946,
"name": "GSPC.Close",
"price":  22.88,
"rsi": 31.892,
"ret": -0.0030501 
},
{
 "date":  -5945,
"name": "GSPC.Close",
"price":   23.2,
"rsi":  30.68,
"ret": 0.013986 
},
{
 "date":  -5944,
"name": "GSPC.Close",
"price":  23.23,
"rsi": 41.609,
"ret": 0.0012931 
},
{
 "date":  -5943,
"name": "GSPC.Close",
"price":  23.24,
"rsi": 42.524,
"ret": 0.00043048 
},
{
 "date":  -5942,
"name": "GSPC.Close",
"price":   23.3,
"rsi": 42.845,
"ret": 0.0025818 
},
{
 "date":  -5939,
"name": "GSPC.Close",
"price":  23.45,
"rsi": 44.839,
"ret": 0.0064378 
},
{
 "date":  -5938,
"name": "GSPC.Close",
"price":  23.49,
"rsi": 49.574,
"ret": 0.0017058 
},
{
 "date":  -5937,
"name": "GSPC.Close",
"price":  23.35,
"rsi": 50.788,
"ret": -0.00596 
},
{
 "date":  -5936,
"name": "GSPC.Close",
"price":  23.49,
"rsi": 46.565,
"ret": 0.0059957 
},
{
 "date":  -5935,
"name": "GSPC.Close",
"price":  23.59,
"rsi": 50.956,
"ret": 0.0042571 
},
{
 "date":  -5932,
"name": "GSPC.Close",
"price":  23.48,
"rsi": 53.872,
"ret": -0.004663 
},
{
 "date":  -5931,
"name": "GSPC.Close",
"price":  23.39,
"rsi": 50.327,
"ret": -0.003833 
},
{
 "date":  -5930,
"name": "GSPC.Close",
"price":  23.58,
"rsi": 47.569,
"ret": 0.0081231 
},
{
 "date":  -5929,
"name": "GSPC.Close",
"price":  23.62,
"rsi": 53.378,
"ret": 0.0016964 
},
{
 "date":  -5928,
"name": "GSPC.Close",
"price":  23.66,
"rsi": 54.521,
"ret": 0.0016935 
},
{
 "date":  -5924,
"name": "GSPC.Close",
"price":  23.57,
"rsi":  55.69,
"ret": -0.0038039 
},
{
 "date":  -5923,
"name": "GSPC.Close",
"price":  23.68,
"rsi": 52.424,
"ret": 0.0046669 
},
{
 "date":  -5922,
"name": "GSPC.Close",
"price":  23.95,
"rsi": 55.833,
"ret": 0.011402 
},
{
 "date":  -5921,
"name": "GSPC.Close",
"price":  24.14,
"rsi": 62.867,
"ret": 0.0079332 
},
{
 "date":  -5918,
"name": "GSPC.Close",
"price":  24.16,
"rsi": 66.866,
"ret": 0.0008285 
},
{
 "date":  -5917,
"name": "GSPC.Close",
"price":  24.17,
"rsi": 67.265,
"ret": 0.00041391 
},
{
 "date":  -5916,
"name": "GSPC.Close",
"price":  24.19,
"rsi": 67.476,
"ret": 0.00082747 
},
{
 "date":  -5915,
"name": "GSPC.Close",
"price":   24.3,
"rsi": 67.922,
"ret": 0.0045473 
},
{
 "date":  -5914,
"name": "GSPC.Close",
"price":  24.35,
"rsi": 70.331,
"ret": 0.0020576 
},
{
 "date":  -5911,
"name": "GSPC.Close",
"price":  24.31,
"rsi": 71.383,
"ret": -0.0016427 
},
{
 "date":  -5910,
"name": "GSPC.Close",
"price":  24.26,
"rsi": 69.267,
"ret": -0.0020568 
},
{
 "date":  -5909,
"name": "GSPC.Close",
"price":  24.29,
"rsi": 66.609,
"ret": 0.0012366 
},
{
 "date":  -5908,
"name": "GSPC.Close",
"price":  24.58,
"rsi": 67.417,
"ret": 0.011939 
},
{
 "date":  -5907,
"name": "GSPC.Close",
"price":  24.54,
"rsi": 73.972,
"ret": -0.0016273 
},
{
 "date":  -5904,
"name": "GSPC.Close",
"price":  24.66,
"rsi": 71.826,
"ret": 0.00489 
},
{
 "date":  -5902,
"name": "GSPC.Close",
"price":  24.51,
"rsi":  74.24,
"ret": -0.0060827 
},
{
 "date":  -5901,
"name": "GSPC.Close",
"price":  24.64,
"rsi": 66.561,
"ret": 0.005304 
},
{
 "date":  -5900,
"name": "GSPC.Close",
"price":  24.61,
"rsi": 69.505,
"ret": -0.0012175 
},
{
 "date":  -5897,
"name": "GSPC.Close",
"price":  24.66,
"rsi": 68.017,
"ret": 0.0020317 
},
{
 "date":  -5896,
"name": "GSPC.Close",
"price":  24.37,
"rsi":   69.2,
"ret": -0.01176 
},
{
 "date":  -5894,
"name": "GSPC.Close",
"price":  24.46,
"rsi": 56.207,
"ret": 0.0036931 
},
{
 "date":  -5893,
"name": "GSPC.Close",
"price":  24.54,
"rsi": 58.793,
"ret": 0.0032706 
},
{
 "date":  -5890,
"name": "GSPC.Close",
"price":  24.38,
"rsi": 60.997,
"ret": -0.00652 
},
{
 "date":  -5889,
"name": "GSPC.Close",
"price":  24.25,
"rsi": 54.695,
"ret": -0.0053322 
},
{
 "date":  -5888,
"name": "GSPC.Close",
"price":  24.29,
"rsi":  50.16,
"ret": 0.0016495 
},
{
 "date":  -5887,
"name": "GSPC.Close",
"price":   24.4,
"rsi": 51.492,
"ret": 0.0045286 
},
{
 "date":  -5886,
"name": "GSPC.Close",
"price":  24.44,
"rsi": 55.052,
"ret": 0.0016393 
},
{
 "date":  -5883,
"name": "GSPC.Close",
"price":  24.36,
"rsi": 56.308,
"ret": -0.0032733 
},
{
 "date":  -5882,
"name": "GSPC.Close",
"price":   24.5,
"rsi": 53.112,
"ret": 0.0057471 
},
{
 "date":  -5881,
"name": "GSPC.Close",
"price":  24.52,
"rsi": 57.642,
"ret": 0.00081633 
},
{
 "date":  -5879,
"name": "GSPC.Close",
"price":  24.66,
"rsi": 58.263,
"ret": 0.0057096 
},
{
 "date":  -5876,
"name": "GSPC.Close",
"price":  24.76,
"rsi": 62.413,
"ret": 0.0040552 
},
{
 "date":  -5875,
"name": "GSPC.Close",
"price":  24.78,
"rsi": 65.084,
"ret": 0.00080775 
},
{
 "date":  -5874,
"name": "GSPC.Close",
"price":  24.95,
"rsi":  65.61,
"ret": 0.0068604 
},
{
 "date":  -5873,
"name": "GSPC.Close",
"price":  24.97,
"rsi":  69.78,
"ret": 0.0008016 
},
{
 "date":  -5872,
"name": "GSPC.Close",
"price":  24.98,
"rsi": 70.237,
"ret": 0.00040048 
},
{
 "date":  -5869,
"name": "GSPC.Close",
"price":  24.95,
"rsi": 70.477,
"ret": -0.001201 
},
{
 "date":  -5868,
"name": "GSPC.Close",
"price":  24.87,
"rsi": 68.684,
"ret": -0.0032064 
},
{
 "date":  -5867,
"name": "GSPC.Close",
"price":  24.84,
"rsi": 64.007,
"ret": -0.0012063 
},
{
 "date":  -5866,
"name": "GSPC.Close",
"price":  24.78,
"rsi": 62.294,
"ret": -0.0024155 
},
{
 "date":  -5865,
"name": "GSPC.Close",
"price":  24.76,
"rsi": 58.899,
"ret": -0.0008071 
},
{
 "date":  -5862,
"name": "GSPC.Close",
"price":  24.69,
"rsi": 57.769,
"ret": -0.0028271 
},
{
 "date":  -5861,
"name": "GSPC.Close",
"price":  24.71,
"rsi": 53.873,
"ret": 0.00081004 
},
{
 "date":  -5860,
"name": "GSPC.Close",
"price":  24.96,
"rsi":  54.81,
"ret": 0.010117 
},
{
 "date":  -5859,
"name": "GSPC.Close",
"price":  24.94,
"rsi": 64.521,
"ret": -0.00080128 
},
{
 "date":  -5858,
"name": "GSPC.Close",
"price":  24.99,
"rsi": 63.348,
"ret": 0.0020048 
},
{
 "date":  -5855,
"name": "GSPC.Close",
"price":  24.95,
"rsi": 65.058,
"ret": -0.0016006 
},
{
 "date":  -5854,
"name": "GSPC.Close",
"price":  24.76,
"rsi": 62.544,
"ret": -0.0076152 
},
{
 "date":  -5853,
"name": "GSPC.Close",
"price":  24.69,
"rsi": 52.222,
"ret": -0.0028271 
},
{
 "date":  -5852,
"name": "GSPC.Close",
"price":   24.8,
"rsi": 49.012,
"ret": 0.0044552 
},
{
 "date":  -5848,
"name": "GSPC.Close",
"price":  24.71,
"rsi": 53.816,
"ret": -0.003629 
},
{
 "date":  -5847,
"name": "GSPC.Close",
"price":  24.55,
"rsi": 49.691,
"ret": -0.0064751 
},
{
 "date":  -5846,
"name": "GSPC.Close",
"price":  24.76,
"rsi": 43.333,
"ret": 0.008554 
},
{
 "date":  -5845,
"name": "GSPC.Close",
"price":  24.81,
"rsi": 52.012,
"ret": 0.0020194 
},
{
 "date":  -5841,
"name": "GSPC.Close",
"price":  24.95,
"rsi": 53.826,
"ret": 0.0056429 
},
{
 "date":  -5840,
"name": "GSPC.Close",
"price":   25.1,
"rsi": 58.549,
"ret": 0.006012 
},
{
 "date":  -5839,
"name": "GSPC.Close",
"price":  25.14,
"rsi": 62.925,
"ret": 0.0015936 
},
{
 "date":  -5838,
"name": "GSPC.Close",
"price":  25.06,
"rsi": 64.016,
"ret": -0.0031822 
},
{
 "date":  -5837,
"name": "GSPC.Close",
"price":  24.93,
"rsi":   60.2,
"ret": -0.0051875 
},
{
 "date":  -5834,
"name": "GSPC.Close",
"price":   24.8,
"rsi": 54.515,
"ret": -0.0052146 
},
{
 "date":  -5833,
"name": "GSPC.Close",
"price":  24.93,
"rsi": 49.482,
"ret": 0.0052419 
},
{
 "date":  -5832,
"name": "GSPC.Close",
"price":  25.07,
"rsi":  54.05,
"ret": 0.0056157 
},
{
 "date":  -5831,
"name": "GSPC.Close",
"price":  25.19,
"rsi": 58.412,
"ret": 0.0047866 
},
{
 "date":  -5830,
"name": "GSPC.Close",
"price":  25.43,
"rsi": 61.763,
"ret": 0.0095276 
},
{
 "date":  -5827,
"name": "GSPC.Close",
"price":  25.43,
"rsi": 67.417,
"ret":      0 
},
{
 "date":  -5826,
"name": "GSPC.Close",
"price":  25.68,
"rsi": 67.417,
"ret": 0.0098309 
},
{
 "date":  -5825,
"name": "GSPC.Close",
"price":  25.75,
"rsi": 72.355,
"ret": 0.0027259 
},
{
 "date":  -5824,
"name": "GSPC.Close",
"price":  25.79,
"rsi": 73.563,
"ret": 0.0015534 
},
{
 "date":  -5823,
"name": "GSPC.Close",
"price":  25.85,
"rsi": 74.256,
"ret": 0.0023265 
},
{
 "date":  -5820,
"name": "GSPC.Close",
"price":  25.93,
"rsi": 75.301,
"ret": 0.0030948 
},
{
 "date":  -5819,
"name": "GSPC.Close",
"price":  26.09,
"rsi": 76.661,
"ret": 0.0061705 
},
{
 "date":  -5818,
"name": "GSPC.Close",
"price":  26.01,
"rsi": 79.136,
"ret": -0.0030663 
},
{
 "date":  -5817,
"name": "GSPC.Close",
"price":  26.02,
"rsi": 74.861,
"ret": 0.00038447 
},
{
 "date":  -5816,
"name": "GSPC.Close",
"price":  26.08,
"rsi": 75.043,
"ret": 0.0023059 
},
{
 "date":  -5813,
"name": "GSPC.Close",
"price":  25.99,
"rsi": 76.155,
"ret": -0.0034509 
},
{
 "date":  -5812,
"name": "GSPC.Close",
"price":  25.92,
"rsi": 71.041,
"ret": -0.0026933 
},
{
 "date":  -5811,
"name": "GSPC.Close",
"price":  26.01,
"rsi": 67.257,
"ret": 0.0034722 
},
{
 "date":  -5810,
"name": "GSPC.Close",
"price":   26.2,
"rsi": 69.506,
"ret": 0.0073049 
},
{
 "date":  -5809,
"name": "GSPC.Close",
"price":   26.3,
"rsi": 73.624,
"ret": 0.0038168 
},
{
 "date":  -5806,
"name": "GSPC.Close",
"price":  26.23,
"rsi": 75.499,
"ret": -0.0026616 
},
{
 "date":  -5805,
"name": "GSPC.Close",
"price":  26.17,
"rsi": 71.659,
"ret": -0.0022875 
},
{
 "date":  -5804,
"name": "GSPC.Close",
"price":  26.14,
"rsi": 68.444,
"ret": -0.0011464 
},
{
 "date":  -5803,
"name": "GSPC.Close",
"price":  26.06,
"rsi":  66.83,
"ret": -0.0030604 
},
{
 "date":  -5802,
"name": "GSPC.Close",
"price":  26.12,
"rsi": 62.591,
"ret": 0.0023024 
},
{
 "date":  -5799,
"name": "GSPC.Close",
"price":  26.04,
"rsi": 64.415,
"ret": -0.0030628 
},
{
 "date":  -5798,
"name": "GSPC.Close",
"price":  25.81,
"rsi": 60.202,
"ret": -0.0088326 
},
{
 "date":  -5797,
"name": "GSPC.Close",
"price":  25.86,
"rsi": 50.064,
"ret": 0.0019372 
},
{
 "date":  -5796,
"name": "GSPC.Close",
"price":  25.86,
"rsi": 51.958,
"ret":      0 
},
{
 "date":  -5795,
"name": "GSPC.Close",
"price":  25.92,
"rsi": 51.958,
"ret": 0.0023202 
},
{
 "date":  -5791,
"name": "GSPC.Close",
"price":  25.83,
"rsi": 54.367,
"ret": -0.0034722 
},
{
 "date":  -5790,
"name": "GSPC.Close",
"price":  25.83,
"rsi": 50.294,
"ret":      0 
},
{
 "date":  -5789,
"name": "GSPC.Close",
"price":  25.91,
"rsi": 50.294,
"ret": 0.0030972 
},
{
 "date":  -5788,
"name": "GSPC.Close",
"price":  26.15,
"rsi": 53.858,
"ret": 0.0092628 
},
{
 "date":  -5785,
"name": "GSPC.Close",
"price":  26.25,
"rsi": 62.536,
"ret": 0.0038241 
},
{
 "date":  -5784,
"name": "GSPC.Close",
"price":  26.32,
"rsi": 65.452,
"ret": 0.0026667 
},
{
 "date":  -5783,
"name": "GSPC.Close",
"price":  26.32,
"rsi": 67.366,
"ret":      0 
},
{
 "date":  -5782,
"name": "GSPC.Close",
"price":  26.41,
"rsi": 67.366,
"ret": 0.0034195 
},
{
 "date":  -5781,
"name": "GSPC.Close",
"price":  26.52,
"rsi": 69.857,
"ret": 0.0041651 
},
{
 "date":  -5778,
"name": "GSPC.Close",
"price":  26.45,
"rsi": 72.609,
"ret": -0.0026395 
},
{
 "date":  -5777,
"name": "GSPC.Close",
"price":  26.51,
"rsi": 68.334,
"ret": 0.0022684 
},
{
 "date":  -5776,
"name": "GSPC.Close",
"price":  26.57,
"rsi": 69.966,
"ret": 0.0022633 
},
{
 "date":  -5775,
"name": "GSPC.Close",
"price":  26.69,
"rsi": 71.546,
"ret": 0.0045164 
},
{
 "date":  -5774,
"name": "GSPC.Close",
"price":  26.69,
"rsi": 74.441,
"ret":      0 
},
{
 "date":  -5771,
"name": "GSPC.Close",
"price":  26.57,
"rsi": 74.441,
"ret": -0.0044961 
},
{
 "date":  -5770,
"name": "GSPC.Close",
"price":  26.56,
"rsi": 66.583,
"ret": -0.00037636 
},
{
 "date":  -5769,
"name": "GSPC.Close",
"price":  26.62,
"rsi": 65.959,
"ret": 0.002259 
},
{
 "date":  -5768,
"name": "GSPC.Close",
"price":  26.73,
"rsi": 67.905,
"ret": 0.0041322 
},
{
 "date":  -5767,
"name": "GSPC.Close",
"price":  26.81,
"rsi":  71.16,
"ret": 0.0029929 
},
{
 "date":  -5764,
"name": "GSPC.Close",
"price":  26.79,
"rsi": 73.282,
"ret": -0.00074599 
},
{
 "date":  -5763,
"name": "GSPC.Close",
"price":   26.6,
"rsi": 71.859,
"ret": -0.0070922 
},
{
 "date":  -5762,
"name": "GSPC.Close",
"price":  26.47,
"rsi": 59.944,
"ret": -0.0048872 
},
{
 "date":  -5761,
"name": "GSPC.Close",
"price":  26.42,
"rsi": 53.418,
"ret": -0.0018889 
},
{
 "date":  -5760,
"name": "GSPC.Close",
"price":  26.56,
"rsi": 51.113,
"ret": 0.005299 
},
{
 "date":  -5757,
"name": "GSPC.Close",
"price":  26.66,
"rsi": 56.741,
"ret": 0.0037651 
},
{
 "date":  -5756,
"name": "GSPC.Close",
"price":  26.69,
"rsi": 60.261,
"ret": 0.0011253 
},
{
 "date":  -5755,
"name": "GSPC.Close",
"price":  26.94,
"rsi": 61.278,
"ret": 0.0093668 
},
{
 "date":  -5754,
"name": "GSPC.Close",
"price":  27.17,
"rsi": 68.515,
"ret": 0.0085375 
},
{
 "date":  -5753,
"name": "GSPC.Close",
"price":  27.21,
"rsi": 73.434,
"ret": 0.0014722 
},
{
 "date":  -5750,
"name": "GSPC.Close",
"price":  27.26,
"rsi": 74.189,
"ret": 0.0018376 
},
{
 "date":  -5749,
"name": "GSPC.Close",
"price":  27.01,
"rsi": 75.141,
"ret": -0.0091709 
},
{
 "date":  -5748,
"name": "GSPC.Close",
"price":  27.11,
"rsi": 62.697,
"ret": 0.0037023 
},
{
 "date":  -5747,
"name": "GSPC.Close",
"price":  27.38,
"rsi": 65.181,
"ret": 0.0099594 
},
{
 "date":  -5746,
"name": "GSPC.Close",
"price":  27.38,
"rsi": 70.829,
"ret":      0 
},
{
 "date":  -5743,
"name": "GSPC.Close",
"price":  27.57,
"rsi": 70.829,
"ret": 0.0069394 
},
{
 "date":  -5742,
"name": "GSPC.Close",
"price":  27.64,
"rsi": 74.239,
"ret": 0.002539 
},
{
 "date":  -5741,
"name": "GSPC.Close",
"price":  27.85,
"rsi": 75.381,
"ret": 0.0075977 
},
{
 "date":  -5740,
"name": "GSPC.Close",
"price":  27.94,
"rsi": 78.465,
"ret": 0.0032316 
},
{
 "date":  -5736,
"name": "GSPC.Close",
"price":  27.76,
"rsi": 79.642,
"ret": -0.0064424 
},
{
 "date":  -5735,
"name": "GSPC.Close",
"price":  27.75,
"rsi": 71.254,
"ret": -0.00036023 
},
{
 "date":  -5734,
"name": "GSPC.Close",
"price":  27.64,
"rsi": 70.808,
"ret": -0.003964 
},
{
 "date":  -5733,
"name": "GSPC.Close",
"price":  27.68,
"rsi": 65.918,
"ret": 0.0014472 
},
{
 "date":  -5732,
"name": "GSPC.Close",
"price":  27.78,
"rsi": 66.815,
"ret": 0.0036127 
},
{
 "date":  -5729,
"name": "GSPC.Close",
"price":  27.88,
"rsi": 69.012,
"ret": 0.0035997 
},
{
 "date":  -5728,
"name": "GSPC.Close",
"price":  27.71,
"rsi": 71.074,
"ret": -0.0060976 
},
{
 "date":  -5727,
"name": "GSPC.Close",
"price":  27.76,
"rsi": 63.355,
"ret": 0.0018044 
},
{
 "date":  -5726,
"name": "GSPC.Close",
"price":  28.18,
"rsi": 64.574,
"ret": 0.01513 
},
{
 "date":  -5725,
"name": "GSPC.Close",
"price":  28.26,
"rsi": 72.767,
"ret": 0.0028389 
},
{
 "date":  -5722,
"name": "GSPC.Close",
"price":  28.21,
"rsi":     74,
"ret": -0.0017693 
},
{
 "date":  -5721,
"name": "GSPC.Close",
"price":  28.28,
"rsi": 71.811,
"ret": 0.0024814 
},
{
 "date":  -5720,
"name": "GSPC.Close",
"price":  28.29,
"rsi": 73.015,
"ret": 0.00035361 
},
{
 "date":  -5719,
"name": "GSPC.Close",
"price":  28.51,
"rsi": 73.191,
"ret": 0.0077766 
},
{
 "date":  -5718,
"name": "GSPC.Close",
"price":  28.65,
"rsi": 76.781,
"ret": 0.0049106 
},
{
 "date":  -5715,
"name": "GSPC.Close",
"price":  28.62,
"rsi": 78.732,
"ret": -0.0010471 
},
{
 "date":  -5714,
"name": "GSPC.Close",
"price":  28.49,
"rsi": 77.234,
"ret": -0.0045423 
},
{
 "date":  -5713,
"name": "GSPC.Close",
"price":  28.72,
"rsi": 70.935,
"ret": 0.008073 
},
{
 "date":  -5712,
"name": "GSPC.Close",
"price":  28.56,
"rsi": 74.844,
"ret": -0.005571 
},
{
 "date":  -5711,
"name": "GSPC.Close",
"price":   28.8,
"rsi": 67.993,
"ret": 0.0084034 
},
{
 "date":  -5708,
"name": "GSPC.Close",
"price":  28.84,
"rsi": 72.116,
"ret": 0.0013889 
},
{
 "date":  -5707,
"name": "GSPC.Close",
"price":  28.85,
"rsi": 72.747,
"ret": 0.00034674 
},
{
 "date":  -5706,
"name": "GSPC.Close",
"price":  28.72,
"rsi": 72.911,
"ret": -0.0045061 
},
{
 "date":  -5705,
"name": "GSPC.Close",
"price":  28.82,
"rsi":  67.22,
"ret": 0.0034819 
},
{
 "date":  -5704,
"name": "GSPC.Close",
"price":  28.99,
"rsi": 69.211,
"ret": 0.0058987 
},
{
 "date":  -5701,
"name": "GSPC.Close",
"price":     29,
"rsi": 72.292,
"ret": 0.00034495 
},
{
 "date":  -5700,
"name": "GSPC.Close",
"price":  28.93,
"rsi": 72.466,
"ret": -0.0024138 
},
{
 "date":  -5699,
"name": "GSPC.Close",
"price":  29.17,
"rsi": 69.181,
"ret": 0.0082959 
},
{
 "date":  -5698,
"name": "GSPC.Close",
"price":  29.05,
"rsi":   73.6,
"ret": -0.0041138 
},
{
 "date":  -5697,
"name": "GSPC.Close",
"price":  29.19,
"rsi": 68.325,
"ret": 0.0048193 
},
{
 "date":  -5693,
"name": "GSPC.Close",
"price":  29.19,
"rsi": 70.942,
"ret":      0 
},
{
 "date":  -5692,
"name": "GSPC.Close",
"price":  29.16,
"rsi": 70.942,
"ret": -0.0010277 
},
{
 "date":  -5691,
"name": "GSPC.Close",
"price":  29.15,
"rsi": 69.515,
"ret": -0.00034294 
},
{
 "date":  -5690,
"name": "GSPC.Close",
"price":   29.1,
"rsi": 69.016,
"ret": -0.0017153 
},
{
 "date":  -5687,
"name": "GSPC.Close",
"price":  28.99,
"rsi": 66.451,
"ret": -0.0037801 
},
{
 "date":  -5686,
"name": "GSPC.Close",
"price":  28.34,
"rsi": 61.072,
"ret": -0.022422 
},
{
 "date":  -5685,
"name": "GSPC.Close",
"price":  28.15,
"rsi":  40.31,
"ret": -0.0067043 
},
{
 "date":  -5684,
"name": "GSPC.Close",
"price":  28.34,
"rsi": 36.413,
"ret": 0.0067496 
},
{
 "date":  -5683,
"name": "GSPC.Close",
"price":  28.58,
"rsi": 42.409,
"ret": 0.0084686 
},
{
 "date":  -5680,
"name": "GSPC.Close",
"price":  28.62,
"rsi": 48.956,
"ret": 0.0013996 
},
{
 "date":  -5679,
"name": "GSPC.Close",
"price":  28.83,
"rsi": 49.977,
"ret": 0.0073375 
},
{
 "date":  -5678,
"name": "GSPC.Close",
"price":  29.04,
"rsi": 55.058,
"ret": 0.0072841 
},
{
 "date":  -5677,
"name": "GSPC.Close",
"price":  28.96,
"rsi": 59.489,
"ret": -0.0027548 
},
{
 "date":  -5676,
"name": "GSPC.Close",
"price":  29.04,
"rsi": 57.177,
"ret": 0.0027624 
},
{
 "date":  -5673,
"name": "GSPC.Close",
"price":  29.06,
"rsi": 58.898,
"ret": 0.00068871 
},
{
 "date":  -5672,
"name": "GSPC.Close",
"price":  29.08,
"rsi": 59.337,
"ret": 0.00068823 
},
{
 "date":  -5671,
"name": "GSPC.Close",
"price":  29.13,
"rsi": 59.801,
"ret": 0.0017194 
},
{
 "date":  -5670,
"name": "GSPC.Close",
"price":  29.26,
"rsi": 60.998,
"ret": 0.0044628 
},
{
 "date":  -5669,
"name": "GSPC.Close",
"price":   29.2,
"rsi": 63.998,
"ret": -0.0020506 
},
{
 "date":  -5666,
"name": "GSPC.Close",
"price":  29.28,
"rsi": 61.641,
"ret": 0.0027397 
},
{
 "date":  -5665,
"name": "GSPC.Close",
"price":  29.43,
"rsi": 63.568,
"ret": 0.005123 
},
{
 "date":  -5664,
"name": "GSPC.Close",
"price":  29.21,
"rsi": 66.923,
"ret": -0.0074754 
},
{
 "date":  -5663,
"name": "GSPC.Close",
"price":  29.21,
"rsi": 58.425,
"ret":      0 
},
{
 "date":  -5662,
"name": "GSPC.Close",
"price":  29.59,
"rsi": 58.425,
"ret": 0.013009 
},
{
 "date":  -5658,
"name": "GSPC.Close",
"price":  29.92,
"rsi": 66.856,
"ret": 0.011152 
},
{
 "date":  -5657,
"name": "GSPC.Close",
"price":  29.94,
"rsi":  72.14,
"ret": 0.00066845 
},
{
 "date":  -5656,
"name": "GSPC.Close",
"price":  29.94,
"rsi": 72.427,
"ret":      0 
},
{
 "date":  -5655,
"name": "GSPC.Close",
"price":  30.14,
"rsi": 72.427,
"ret": 0.00668 
},
{
 "date":  -5652,
"name": "GSPC.Close",
"price":  30.12,
"rsi": 75.368,
"ret": -0.00066357 
},
{
 "date":  -5651,
"name": "GSPC.Close",
"price":  30.02,
"rsi": 74.512,
"ret": -0.0033201 
},
{
 "date":  -5650,
"name": "GSPC.Close",
"price":  30.09,
"rsi": 70.217,
"ret": 0.0023318 
},
{
 "date":  -5649,
"name": "GSPC.Close",
"price":  30.19,
"rsi": 71.458,
"ret": 0.0033234 
},
{
 "date":  -5648,
"name": "GSPC.Close",
"price":  30.06,
"rsi": 73.176,
"ret": -0.0043061 
},
{
 "date":  -5645,
"name": "GSPC.Close",
"price":  29.98,
"rsi": 67.488,
"ret": -0.0026613 
},
{
 "date":  -5644,
"name": "GSPC.Close",
"price":  29.84,
"rsi": 64.181,
"ret": -0.0046698 
},
{
 "date":  -5643,
"name": "GSPC.Close",
"price":  30.03,
"rsi": 58.756,
"ret": 0.0063673 
},
{
 "date":  -5642,
"name": "GSPC.Close",
"price":  30.27,
"rsi": 63.291,
"ret": 0.007992 
},
{
 "date":  -5641,
"name": "GSPC.Close",
"price":  30.31,
"rsi": 68.068,
"ret": 0.0013214 
},
{
 "date":  -5638,
"name": "GSPC.Close",
"price":  30.34,
"rsi": 68.796,
"ret": 0.00098977 
},
{
 "date":  -5637,
"name": "GSPC.Close",
"price":  30.52,
"rsi": 69.361,
"ret": 0.0059328 
},
{
 "date":  -5636,
"name": "GSPC.Close",
"price":  30.58,
"rsi": 72.569,
"ret": 0.0019659 
},
{
 "date":  -5635,
"name": "GSPC.Close",
"price":  30.69,
"rsi": 73.563,
"ret": 0.0035971 
},
{
 "date":  -5634,
"name": "GSPC.Close",
"price":  30.88,
"rsi": 75.327,
"ret": 0.0061909 
},
{
 "date":  -5631,
"name": "GSPC.Close",
"price":  30.99,
"rsi": 78.052,
"ret": 0.0035622 
},
{
 "date":  -5630,
"name": "GSPC.Close",
"price":  30.93,
"rsi": 79.466,
"ret": -0.0019361 
},
{
 "date":  -5629,
"name": "GSPC.Close",
"price":   30.9,
"rsi": 76.569,
"ret": -0.00096993 
},
{
 "date":  -5628,
"name": "GSPC.Close",
"price":  30.77,
"rsi": 75.094,
"ret": -0.0042071 
},
{
 "date":  -5627,
"name": "GSPC.Close",
"price":  30.38,
"rsi": 68.902,
"ret": -0.012675 
},
{
 "date":  -5624,
"name": "GSPC.Close",
"price":  30.12,
"rsi": 54.409,
"ret": -0.0085583 
},
{
 "date":  -5623,
"name": "GSPC.Close",
"price":  30.37,
"rsi":  47.27,
"ret": 0.0083001 
},
{
 "date":  -5622,
"name": "GSPC.Close",
"price":  30.72,
"rsi": 53.577,
"ret": 0.011525 
},
{
 "date":  -5621,
"name": "GSPC.Close",
"price":  30.59,
"rsi":  60.67,
"ret": -0.0042318 
},
{
 "date":  -5620,
"name": "GSPC.Close",
"price":  30.72,
"rsi": 57.176,
"ret": 0.0042498 
},
{
 "date":  -5617,
"name": "GSPC.Close",
"price":  31.05,
"rsi": 59.677,
"ret": 0.010742 
},
{
 "date":  -5616,
"name": "GSPC.Close",
"price":  31.12,
"rsi": 65.228,
"ret": 0.0022544 
},
{
 "date":  -5615,
"name": "GSPC.Close",
"price":  31.09,
"rsi": 66.289,
"ret": -0.00096401 
},
{
 "date":  -5614,
"name": "GSPC.Close",
"price":  31.16,
"rsi": 65.369,
"ret": 0.0022515 
},
{
 "date":  -5613,
"name": "GSPC.Close",
"price":  31.21,
"rsi": 66.536,
"ret": 0.0016046 
},
{
 "date":  -5610,
"name": "GSPC.Close",
"price":     31,
"rsi": 67.381,
"ret": -0.0067286 
},
{
 "date":  -5609,
"name": "GSPC.Close",
"price":  30.87,
"rsi": 60.471,
"ret": -0.0041935 
},
{
 "date":  -5608,
"name": "GSPC.Close",
"price":  30.65,
"rsi": 56.601,
"ret": -0.0071267 
},
{
 "date":  -5607,
"name": "GSPC.Close",
"price":  30.57,
"rsi": 50.689,
"ret": -0.0026101 
},
{
 "date":  -5606,
"name": "GSPC.Close",
"price":  30.66,
"rsi": 48.697,
"ret": 0.0029441 
},
{
 "date":  -5603,
"name": "GSPC.Close",
"price":  30.35,
"rsi": 51.028,
"ret": -0.010111 
},
{
 "date":  -5602,
"name": "GSPC.Close",
"price":  29.83,
"rsi": 43.667,
"ret": -0.017133 
},
{
 "date":  -5601,
"name": "GSPC.Close",
"price":  30.04,
"rsi":  34.64,
"ret": 0.0070399 
},
{
 "date":  -5600,
"name": "GSPC.Close",
"price":  30.27,
"rsi": 40.032,
"ret": 0.0076565 
},
{
 "date":  -5599,
"name": "GSPC.Close",
"price":   30.5,
"rsi": 45.349,
"ret": 0.0075983 
},
{
 "date":  -5595,
"name": "GSPC.Close",
"price":  30.66,
"rsi": 50.113,
"ret": 0.0052459 
},
{
 "date":  -5594,
"name": "GSPC.Close",
"price":  30.68,
"rsi": 53.171,
"ret": 0.00065232 
},
{
 "date":  -5593,
"name": "GSPC.Close",
"price":  30.73,
"rsi": 53.554,
"ret": 0.0016297 
},
{
 "date":  -5592,
"name": "GSPC.Close",
"price":  30.84,
"rsi": 54.555,
"ret": 0.0035796 
},
{
 "date":  -5589,
"name": "GSPC.Close",
"price":  31.12,
"rsi": 56.764,
"ret": 0.0090791 
},
{
 "date":  -5588,
"name": "GSPC.Close",
"price":  31.28,
"rsi": 61.846,
"ret": 0.0051414 
},
{
 "date":  -5587,
"name": "GSPC.Close",
"price":  31.29,
"rsi":  64.42,
"ret": 0.00031969 
},
{
 "date":  -5586,
"name": "GSPC.Close",
"price":  31.46,
"rsi": 64.581,
"ret": 0.005433 
},
{
 "date":  -5585,
"name": "GSPC.Close",
"price":  31.71,
"rsi": 67.288,
"ret": 0.0079466 
},
{
 "date":  -5582,
"name": "GSPC.Close",
"price":  31.57,
"rsi":  70.82,
"ret": -0.004415 
},
{
 "date":  -5581,
"name": "GSPC.Close",
"price":  31.79,
"rsi": 66.491,
"ret": 0.0069686 
},
{
 "date":  -5580,
"name": "GSPC.Close",
"price":     32,
"rsi": 69.632,
"ret": 0.0066059 
},
{
 "date":  -5579,
"name": "GSPC.Close",
"price":  32.18,
"rsi": 72.302,
"ret": 0.005625 
},
{
 "date":  -5578,
"name": "GSPC.Close",
"price":   32.4,
"rsi": 74.381,
"ret": 0.0068365 
},
{
 "date":  -5575,
"name": "GSPC.Close",
"price":  32.53,
"rsi": 76.684,
"ret": 0.0040123 
},
{
 "date":  -5574,
"name": "GSPC.Close",
"price":  32.69,
"rsi": 77.946,
"ret": 0.0049185 
},
{
 "date":  -5573,
"name": "GSPC.Close",
"price":   32.5,
"rsi": 79.422,
"ret": -0.0058122 
},
{
 "date":  -5572,
"name": "GSPC.Close",
"price":  32.31,
"rsi":  73.16,
"ret": -0.0058462 
},
{
 "date":  -5571,
"name": "GSPC.Close",
"price":  32.29,
"rsi": 67.434,
"ret": -0.000619 
},
{
 "date":  -5568,
"name": "GSPC.Close",
"price":  32.47,
"rsi": 66.841,
"ret": 0.0055745 
},
{
 "date":  -5567,
"name": "GSPC.Close",
"price":  32.63,
"rsi": 69.446,
"ret": 0.0049276 
},
{
 "date":  -5566,
"name": "GSPC.Close",
"price":  32.76,
"rsi": 71.582,
"ret": 0.0039841 
},
{
 "date":  -5565,
"name": "GSPC.Close",
"price":  32.69,
"rsi": 73.221,
"ret": -0.0021368 
},
{
 "date":  -5564,
"name": "GSPC.Close",
"price":  32.67,
"rsi": 70.852,
"ret": -0.00061181 
},
{
 "date":  -5561,
"name": "GSPC.Close",
"price":  32.41,
"rsi": 70.153,
"ret": -0.0079584 
},
{
 "date":  -5560,
"name": "GSPC.Close",
"price":  32.28,
"rsi": 61.647,
"ret": -0.0040111 
},
{
 "date":  -5559,
"name": "GSPC.Close",
"price":  32.27,
"rsi": 57.868,
"ret": -0.00030979 
},
{
 "date":  -5558,
"name": "GSPC.Close",
"price":  31.88,
"rsi": 57.576,
"ret": -0.012086 
},
{
 "date":  -5557,
"name": "GSPC.Close",
"price":  31.71,
"rsi": 47.498,
"ret": -0.0053325 
},
{
 "date":  -5554,
"name": "GSPC.Close",
"price":  31.83,
"rsi": 43.891,
"ret": 0.0037843 
},
{
 "date":  -5553,
"name": "GSPC.Close",
"price":  31.91,
"rsi": 46.953,
"ret": 0.0025134 
},
{
 "date":  -5552,
"name": "GSPC.Close",
"price":  32.17,
"rsi": 48.953,
"ret": 0.0081479 
},
{
 "date":  -5551,
"name": "GSPC.Close",
"price":  32.13,
"rsi": 54.904,
"ret": -0.0012434 
},
{
 "date":  -5550,
"name": "GSPC.Close",
"price":  32.13,
"rsi": 53.864,
"ret":      0 
},
{
 "date":  -5547,
"name": "GSPC.Close",
"price":  31.96,
"rsi": 53.864,
"ret": -0.005291 
},
{
 "date":  -5546,
"name": "GSPC.Close",
"price":  31.94,
"rsi": 49.263,
"ret": -0.00062578 
},
{
 "date":  -5545,
"name": "GSPC.Close",
"price":  32.02,
"rsi": 48.735,
"ret": 0.0025047 
},
{
 "date":  -5544,
"name": "GSPC.Close",
"price":  31.88,
"rsi": 50.995,
"ret": -0.0043723 
},
{
 "date":  -5543,
"name": "GSPC.Close",
"price":  31.68,
"rsi": 47.083,
"ret": -0.0062735 
},
{
 "date":  -5540,
"name": "GSPC.Close",
"price":  31.79,
"rsi": 42.113,
"ret": 0.0034722 
},
{
 "date":  -5538,
"name": "GSPC.Close",
"price":  32.44,
"rsi":  45.52,
"ret": 0.020447 
},
{
 "date":  -5537,
"name": "GSPC.Close",
"price":  32.82,
"rsi": 60.362,
"ret": 0.011714 
},
{
 "date":  -5536,
"name": "GSPC.Close",
"price":  32.71,
"rsi": 66.166,
"ret": -0.0033516 
},
{
 "date":  -5533,
"name": "GSPC.Close",
"price":  33.02,
"rsi": 63.278,
"ret": 0.0094772 
},
{
 "date":  -5532,
"name": "GSPC.Close",
"price":  33.15,
"rsi": 67.573,
"ret": 0.003937 
},
{
 "date":  -5531,
"name": "GSPC.Close",
"price":  33.18,
"rsi": 69.201,
"ret": 0.00090498 
},
{
 "date":  -5530,
"name": "GSPC.Close",
"price":  33.47,
"rsi":  69.58,
"ret": 0.0087402 
},
{
 "date":  -5529,
"name": "GSPC.Close",
"price":  33.54,
"rsi": 73.037,
"ret": 0.0020914 
},
{
 "date":  -5526,
"name": "GSPC.Close",
"price":  33.47,
"rsi": 73.811,
"ret": -0.0020871 
},
{
 "date":  -5525,
"name": "GSPC.Close",
"price":  33.57,
"rsi": 71.598,
"ret": 0.0029878 
},
{
 "date":  -5524,
"name": "GSPC.Close",
"price":  33.63,
"rsi":  72.85,
"ret": 0.0017873 
},
{
 "date":  -5523,
"name": "GSPC.Close",
"price":  33.44,
"rsi": 73.602,
"ret": -0.0056497 
},
{
 "date":  -5522,
"name": "GSPC.Close",
"price":  33.45,
"rsi":  67.25,
"ret": 0.00029904 
},
{
 "date":  -5519,
"name": "GSPC.Close",
"price":  33.58,
"rsi":  67.41,
"ret": 0.0038864 
},
{
 "date":  -5518,
"name": "GSPC.Close",
"price":  34.03,
"rsi": 69.489,
"ret": 0.013401 
},
{
 "date":  -5517,
"name": "GSPC.Close",
"price":  34.22,
"rsi": 75.351,
"ret": 0.0055833 
},
{
 "date":  -5515,
"name": "GSPC.Close",
"price":  34.55,
"rsi": 77.332,
"ret": 0.0096435 
},
{
 "date":  -5512,
"name": "GSPC.Close",
"price":  34.54,
"rsi": 80.293,
"ret": -0.00028944 
},
{
 "date":  -5511,
"name": "GSPC.Close",
"price":  34.24,
"rsi": 79.952,
"ret": -0.0086856 
},
{
 "date":  -5510,
"name": "GSPC.Close",
"price":  33.99,
"rsi": 70.309,
"ret": -0.0073014 
},
{
 "date":  -5509,
"name": "GSPC.Close",
"price":  34.18,
"rsi": 63.442,
"ret": 0.0055899 
},
{
 "date":  -5508,
"name": "GSPC.Close",
"price":  34.49,
"rsi": 66.148,
"ret": 0.0090696 
},
{
 "date":  -5505,
"name": "GSPC.Close",
"price":  34.76,
"rsi": 70.044,
"ret": 0.0078284 
},
{
 "date":  -5504,
"name": "GSPC.Close",
"price":  34.92,
"rsi": 72.963,
"ret": 0.004603 
},
{
 "date":  -5503,
"name": "GSPC.Close",
"price":  34.86,
"rsi": 74.546,
"ret": -0.0017182 
},
{
 "date":  -5502,
"name": "GSPC.Close",
"price":  34.69,
"rsi": 72.824,
"ret": -0.0048766 
},
{
 "date":  -5501,
"name": "GSPC.Close",
"price":  34.56,
"rsi":  68.03,
"ret": -0.0037475 
},
{
 "date":  -5498,
"name": "GSPC.Close",
"price":  34.59,
"rsi": 64.531,
"ret": 0.00086806 
},
{
 "date":  -5497,
"name": "GSPC.Close",
"price":  34.35,
"rsi": 64.979,
"ret": -0.0069384 
},
{
 "date":  -5496,
"name": "GSPC.Close",
"price":  34.56,
"rsi": 58.607,
"ret": 0.0061135 
},
{
 "date":  -5495,
"name": "GSPC.Close",
"price":  34.93,
"rsi": 62.108,
"ret": 0.010706 
},
{
 "date":  -5494,
"name": "GSPC.Close",
"price":  35.92,
"rsi": 67.349,
"ret": 0.028342 
},
{
 "date":  -5491,
"name": "GSPC.Close",
"price":  35.33,
"rsi": 76.653,
"ret": -0.016425 
},
{
 "date":  -5490,
"name": "GSPC.Close",
"price":  35.38,
"rsi": 64.802,
"ret": 0.0014152 
},
{
 "date":  -5489,
"name": "GSPC.Close",
"price":  35.34,
"rsi": 65.291,
"ret": -0.0011306 
},
{
 "date":  -5488,
"name": "GSPC.Close",
"price":  35.37,
"rsi": 64.518,
"ret": 0.0008489 
},
{
 "date":  -5484,
"name": "GSPC.Close",
"price":  35.07,
"rsi": 64.854,
"ret": -0.0084818 
},
{
 "date":  -5483,
"name": "GSPC.Close",
"price":  35.43,
"rsi": 58.848,
"ret": 0.010265 
},
{
 "date":  -5482,
"name": "GSPC.Close",
"price":  35.74,
"rsi": 63.247,
"ret": 0.0087496 
},
{
 "date":  -5481,
"name": "GSPC.Close",
"price":  35.74,
"rsi": 66.561,
"ret":      0 
},
{
 "date":  -5480,
"name": "GSPC.Close",
"price":  35.98,
"rsi": 66.561,
"ret": 0.0067152 
},
{
 "date":  -5477,
"name": "GSPC.Close",
"price":  36.75,
"rsi": 69.066,
"ret": 0.021401 
},
{
 "date":  -5476,
"name": "GSPC.Close",
"price":  36.42,
"rsi": 75.426,
"ret": -0.0089796 
},
{
 "date":  -5475,
"name": "GSPC.Close",
"price":  35.52,
"rsi": 68.889,
"ret": -0.024712 
},
{
 "date":  -5474,
"name": "GSPC.Close",
"price":  35.04,
"rsi": 54.911,
"ret": -0.013514 
},
{
 "date":  -5473,
"name": "GSPC.Close",
"price":  35.33,
"rsi":  49.18,
"ret": 0.0082763 
},
{
 "date":  -5470,
"name": "GSPC.Close",
"price":  35.79,
"rsi": 52.412,
"ret": 0.01302 
},
{
 "date":  -5469,
"name": "GSPC.Close",
"price":  35.68,
"rsi": 57.075,
"ret": -0.0030735 
},
{
 "date":  -5468,
"name": "GSPC.Close",
"price":  35.58,
"rsi":  55.67,
"ret": -0.0028027 
},
{
 "date":  -5467,
"name": "GSPC.Close",
"price":  35.43,
"rsi":  54.36,
"ret": -0.0042159 
},
{
 "date":  -5466,
"name": "GSPC.Close",
"price":  35.28,
"rsi":  52.37,
"ret": -0.0042337 
},
{
 "date":  -5463,
"name": "GSPC.Close",
"price":  34.58,
"rsi": 50.383,
"ret": -0.019841 
},
{
 "date":  -5462,
"name": "GSPC.Close",
"price":   34.8,
"rsi": 42.315,
"ret": 0.0063621 
},
{
 "date":  -5461,
"name": "GSPC.Close",
"price":  34.96,
"rsi": 45.281,
"ret": 0.0045977 
},
{
 "date":  -5460,
"name": "GSPC.Close",
"price":  35.13,
"rsi": 47.399,
"ret": 0.0048627 
},
{
 "date":  -5459,
"name": "GSPC.Close",
"price":  35.44,
"rsi":  49.63,
"ret": 0.0088244 
},
{
 "date":  -5456,
"name": "GSPC.Close",
"price":  35.52,
"rsi": 53.502,
"ret": 0.0022573 
},
{
 "date":  -5455,
"name": "GSPC.Close",
"price":  35.51,
"rsi": 54.475,
"ret": -0.00028153 
},
{
 "date":  -5454,
"name": "GSPC.Close",
"price":  35.95,
"rsi": 54.322,
"ret": 0.012391 
},
{
 "date":  -5453,
"name": "GSPC.Close",
"price":  35.99,
"rsi": 59.687,
"ret": 0.0011127 
},
{
 "date":  -5452,
"name": "GSPC.Close",
"price":  36.19,
"rsi": 60.145,
"ret": 0.0055571 
},
{
 "date":  -5449,
"name": "GSPC.Close",
"price":  36.63,
"rsi": 62.444,
"ret": 0.012158 
},
{
 "date":  -5448,
"name": "GSPC.Close",
"price":  36.72,
"rsi": 66.959,
"ret": 0.002457 
},
{
 "date":  -5447,
"name": "GSPC.Close",
"price":  36.61,
"rsi": 67.811,
"ret": -0.0029956 
},
{
 "date":  -5446,
"name": "GSPC.Close",
"price":  36.44,
"rsi": 65.584,
"ret": -0.0046435 
},
{
 "date":  -5445,
"name": "GSPC.Close",
"price":  36.96,
"rsi": 62.185,
"ret": 0.01427 
},
{
 "date":  -5442,
"name": "GSPC.Close",
"price":  36.96,
"rsi":   67.7,
"ret":      0 
},
{
 "date":  -5441,
"name": "GSPC.Close",
"price":  36.46,
"rsi":   67.7,
"ret": -0.013528 
},
{
 "date":  -5440,
"name": "GSPC.Close",
"price":  36.75,
"rsi":  58.23,
"ret": 0.0079539 
},
{
 "date":  -5439,
"name": "GSPC.Close",
"price":  37.08,
"rsi": 61.586,
"ret": 0.0089796 
},
{
 "date":  -5438,
"name": "GSPC.Close",
"price":  37.15,
"rsi":  65.03,
"ret": 0.0018878 
},
{
 "date":  -5435,
"name": "GSPC.Close",
"price":  36.89,
"rsi": 65.731,
"ret": -0.0069987 
},
{
 "date":  -5434,
"name": "GSPC.Close",
"price":  36.89,
"rsi": 60.847,
"ret":      0 
},
{
 "date":  -5433,
"name": "GSPC.Close",
"price":  36.77,
"rsi": 60.847,
"ret": -0.0032529 
},
{
 "date":  -5432,
"name": "GSPC.Close",
"price":  36.84,
"rsi":  58.52,
"ret": 0.0019037 
},
{
 "date":  -5431,
"name": "GSPC.Close",
"price":  36.89,
"rsi": 59.493,
"ret": 0.0013572 
},
{
 "date":  -5428,
"name": "GSPC.Close",
"price":  36.85,
"rsi": 60.211,
"ret": -0.0010843 
},
{
 "date":  -5426,
"name": "GSPC.Close",
"price":  36.82,
"rsi": 59.306,
"ret": -0.00081411 
},
{
 "date":  -5425,
"name": "GSPC.Close",
"price":  36.62,
"rsi": 58.594,
"ret": -0.0054318 
},
{
 "date":  -5424,
"name": "GSPC.Close",
"price":  36.57,
"rsi": 53.944,
"ret": -0.0013654 
},
{
 "date":  -5421,
"name": "GSPC.Close",
"price":  36.76,
"rsi": 52.815,
"ret": 0.0051955 
},
{
 "date":  -5420,
"name": "GSPC.Close",
"price":  36.83,
"rsi": 56.536,
"ret": 0.0019042 
},
{
 "date":  -5419,
"name": "GSPC.Close",
"price":  37.15,
"rsi": 57.855,
"ret": 0.0086886 
},
{
 "date":  -5418,
"name": "GSPC.Close",
"price":  37.29,
"rsi": 63.331,
"ret": 0.0037685 
},
{
 "date":  -5417,
"name": "GSPC.Close",
"price":  37.52,
"rsi": 65.447,
"ret": 0.0061679 
},
{
 "date":  -5414,
"name": "GSPC.Close",
"price":  37.28,
"rsi": 68.647,
"ret": -0.0063966 
},
{
 "date":  -5413,
"name": "GSPC.Close",
"price":  36.58,
"rsi": 62.176,
"ret": -0.018777 
},
{
 "date":  -5412,
"name": "GSPC.Close",
"price":  36.22,
"rsi": 47.972,
"ret": -0.0098414 
},
{
 "date":  -5411,
"name": "GSPC.Close",
"price":  36.45,
"rsi": 42.584,
"ret": 0.0063501 
},
{
 "date":  -5410,
"name": "GSPC.Close",
"price":  35.82,
"rsi": 46.702,
"ret": -0.017284 
},
{
 "date":  -5407,
"name": "GSPC.Close",
"price":  34.96,
"rsi": 38.546,
"ret": -0.024009 
},
{
 "date":  -5406,
"name": "GSPC.Close",
"price":  35.71,
"rsi": 30.671,
"ret": 0.021453 
},
{
 "date":  -5405,
"name": "GSPC.Close",
"price":  35.98,
"rsi": 41.832,
"ret": 0.0075609 
},
{
 "date":  -5404,
"name": "GSPC.Close",
"price":  36.12,
"rsi": 45.249,
"ret": 0.0038911 
},
{
 "date":  -5403,
"name": "GSPC.Close",
"price":  36.18,
"rsi": 46.988,
"ret": 0.0016611 
},
{
 "date":  -5400,
"name": "GSPC.Close",
"price":  35.95,
"rsi": 47.754,
"ret": -0.0063571 
},
{
 "date":  -5399,
"name": "GSPC.Close",
"price":  36.17,
"rsi": 45.066,
"ret": 0.0061196 
},
{
 "date":  -5398,
"name": "GSPC.Close",
"price":  36.64,
"rsi": 48.076,
"ret": 0.012994 
},
{
 "date":  -5397,
"name": "GSPC.Close",
"price":  36.93,
"rsi":  53.89,
"ret": 0.0079148 
},
{
 "date":  -5396,
"name": "GSPC.Close",
"price":  36.96,
"rsi": 57.083,
"ret": 0.00081235 
},
{
 "date":  -5393,
"name": "GSPC.Close",
"price":  36.83,
"rsi": 57.412,
"ret": -0.0035173 
},
{
 "date":  -5392,
"name": "GSPC.Close",
"price":  36.85,
"rsi": 55.431,
"ret": 0.00054304 
},
{
 "date":  -5391,
"name": "GSPC.Close",
"price":  36.52,
"rsi": 55.685,
"ret": -0.0089552 
},
{
 "date":  -5390,
"name": "GSPC.Close",
"price":  36.58,
"rsi": 50.578,
"ret": 0.0016429 
},
{
 "date":  -5389,
"name": "GSPC.Close",
"price":  36.95,
"rsi": 51.449,
"ret": 0.010115 
},
{
 "date":  -5386,
"name": "GSPC.Close",
"price":  36.83,
"rsi": 56.541,
"ret": -0.0032476 
},
{
 "date":  -5385,
"name": "GSPC.Close",
"price":  36.98,
"rsi": 54.543,
"ret": 0.0040728 
},
{
 "date":  -5384,
"name": "GSPC.Close",
"price":  37.17,
"rsi": 56.607,
"ret": 0.0051379 
},
{
 "date":  -5383,
"name": "GSPC.Close",
"price":  37.34,
"rsi": 59.138,
"ret": 0.0045736 
},
{
 "date":  -5379,
"name": "GSPC.Close",
"price":  37.44,
"rsi": 61.312,
"ret": 0.0026781 
},
{
 "date":  -5378,
"name": "GSPC.Close",
"price":  37.66,
"rsi": 62.574,
"ret": 0.0058761 
},
{
 "date":  -5377,
"name": "GSPC.Close",
"price":  37.71,
"rsi": 65.258,
"ret": 0.0013277 
},
{
 "date":  -5376,
"name": "GSPC.Close",
"price":  37.79,
"rsi": 65.857,
"ret": 0.0021215 
},
{
 "date":  -5375,
"name": "GSPC.Close",
"price":  37.96,
"rsi": 66.842,
"ret": 0.0044985 
},
{
 "date":  -5372,
"name": "GSPC.Close",
"price":  38.27,
"rsi": 68.897,
"ret": 0.0081665 
},
{
 "date":  -5371,
"name": "GSPC.Close",
"price":  38.22,
"rsi": 72.271,
"ret": -0.0013065 
},
{
 "date":  -5370,
"name": "GSPC.Close",
"price":  38.28,
"rsi": 70.934,
"ret": 0.0015699 
},
{
 "date":  -5369,
"name": "GSPC.Close",
"price":  38.32,
"rsi": 71.613,
"ret": 0.0010449 
},
{
 "date":  -5368,
"name": "GSPC.Close",
"price":  38.01,
"rsi": 72.081,
"ret": -0.0080898 
},
{
 "date":  -5365,
"name": "GSPC.Close",
"price":  38.11,
"rsi": 63.364,
"ret": 0.0026309 
},
{
 "date":  -5364,
"name": "GSPC.Close",
"price":  38.31,
"rsi": 64.841,
"ret": 0.005248 
},
{
 "date":  -5363,
"name": "GSPC.Close",
"price":  38.11,
"rsi":  67.65,
"ret": -0.0052206 
},
{
 "date":  -5362,
"name": "GSPC.Close",
"price":  37.68,
"rsi":  62.29,
"ret": -0.011283 
},
{
 "date":  -5361,
"name": "GSPC.Close",
"price":  37.96,
"rsi": 52.635,
"ret": 0.007431 
},
{
 "date":  -5358,
"name": "GSPC.Close",
"price":  38.04,
"rsi": 57.279,
"ret": 0.0021075 
},
{
 "date":  -5357,
"name": "GSPC.Close",
"price":   37.7,
"rsi":  58.53,
"ret": -0.008938 
},
{
 "date":  -5356,
"name": "GSPC.Close",
"price":  37.64,
"rsi": 51.612,
"ret": -0.0015915 
},
{
 "date":  -5355,
"name": "GSPC.Close",
"price":  37.82,
"rsi": 50.479,
"ret": 0.0047821 
},
{
 "date":  -5354,
"name": "GSPC.Close",
"price":  37.89,
"rsi":  53.76,
"ret": 0.0018509 
},
{
 "date":  -5351,
"name": "GSPC.Close",
"price":  37.93,
"rsi": 55.009,
"ret": 0.0010557 
},
{
 "date":  -5350,
"name": "GSPC.Close",
"price":  37.85,
"rsi": 55.744,
"ret": -0.0021091 
},
{
 "date":  -5349,
"name": "GSPC.Close",
"price":  37.42,
"rsi": 53.848,
"ret": -0.011361 
},
{
 "date":  -5348,
"name": "GSPC.Close",
"price":   37.2,
"rsi": 44.991,
"ret": -0.0058792 
},
{
 "date":  -5347,
"name": "GSPC.Close",
"price":  37.44,
"rsi": 41.253,
"ret": 0.0064516 
},
{
 "date":  -5344,
"name": "GSPC.Close",
"price":  37.02,
"rsi": 46.478,
"ret": -0.011218 
},
{
 "date":  -5343,
"name": "GSPC.Close",
"price":  36.97,
"rsi": 39.805,
"ret": -0.0013506 
},
{
 "date":  -5342,
"name": "GSPC.Close",
"price":  37.28,
"rsi": 39.086,
"ret": 0.0083852 
},
{
 "date":  -5341,
"name": "GSPC.Close",
"price":  37.49,
"rsi": 45.645,
"ret": 0.005633 
},
{
 "date":  -5340,
"name": "GSPC.Close",
"price":  37.74,
"rsi": 49.604,
"ret": 0.0066684 
},
{
 "date":  -5337,
"name": "GSPC.Close",
"price":  37.48,
"rsi": 53.907,
"ret": -0.0068892 
},
{
 "date":  -5336,
"name": "GSPC.Close",
"price":  37.46,
"rsi": 49.201,
"ret": -0.00053362 
},
{
 "date":  -5335,
"name": "GSPC.Close",
"price":   37.6,
"rsi": 48.848,
"ret": 0.0037373 
},
{
 "date":  -5334,
"name": "GSPC.Close",
"price":  37.85,
"rsi": 51.475,
"ret": 0.0066489 
},
{
 "date":  -5333,
"name": "GSPC.Close",
"price":  37.93,
"rsi": 55.835,
"ret": 0.0021136 
},
{
 "date":  -5329,
"name": "GSPC.Close",
"price":  37.91,
"rsi": 57.162,
"ret": -0.00052729 
},
{
 "date":  -5328,
"name": "GSPC.Close",
"price":  37.96,
"rsi": 56.704,
"ret": 0.0013189 
},
{
 "date":  -5327,
"name": "GSPC.Close",
"price":  38.01,
"rsi": 57.619,
"ret": 0.0013172 
},
{
 "date":  -5326,
"name": "GSPC.Close",
"price":  38.37,
"rsi": 58.562,
"ret": 0.0094712 
},
{
 "date":  -5323,
"name": "GSPC.Close",
"price":  39.69,
"rsi": 64.662,
"ret": 0.034402 
},
{
 "date":  -5322,
"name": "GSPC.Close",
"price":  39.96,
"rsi": 77.653,
"ret": 0.0068027 
},
{
 "date":  -5321,
"name": "GSPC.Close",
"price":  39.22,
"rsi": 79.327,
"ret": -0.018519 
},
{
 "date":  -5320,
"name": "GSPC.Close",
"price":  39.01,
"rsi": 64.963,
"ret": -0.0053544 
},
{
 "date":  -5319,
"name": "GSPC.Close",
"price":  39.25,
"rsi": 61.557,
"ret": 0.0061523 
},
{
 "date":  -5316,
"name": "GSPC.Close",
"price":  39.62,
"rsi": 63.887,
"ret": 0.0094268 
},
{
 "date":  -5315,
"name": "GSPC.Close",
"price":  39.67,
"rsi":  67.19,
"ret": 0.001262 
},
{
 "date":  -5314,
"name": "GSPC.Close",
"price":  39.89,
"rsi": 67.621,
"ret": 0.0055458 
},
{
 "date":  -5313,
"name": "GSPC.Close",
"price":  39.96,
"rsi": 69.518,
"ret": 0.0017548 
},
{
 "date":  -5312,
"name": "GSPC.Close",
"price":   40.1,
"rsi": 70.117,
"ret": 0.0035035 
},
{
 "date":  -5309,
"name": "GSPC.Close",
"price":  40.14,
"rsi": 71.333,
"ret": 0.00099751 
},
{
 "date":  -5308,
"name": "GSPC.Close",
"price":  40.51,
"rsi": 71.687,
"ret": 0.0092177 
},
{
 "date":  -5307,
"name": "GSPC.Close",
"price":   40.6,
"rsi":  74.79,
"ret": 0.0022217 
},
{
 "date":  -5306,
"name": "GSPC.Close",
"price":  40.75,
"rsi": 75.494,
"ret": 0.0036946 
},
{
 "date":  -5305,
"name": "GSPC.Close",
"price":  40.96,
"rsi": 76.663,
"ret": 0.0051534 
},
{
 "date":  -5302,
"name": "GSPC.Close",
"price":  40.99,
"rsi": 78.229,
"ret": 0.00073242 
},
{
 "date":  -5301,
"name": "GSPC.Close",
"price":  40.77,
"rsi": 78.451,
"ret": -0.0053672 
},
{
 "date":  -5300,
"name": "GSPC.Close",
"price":  40.79,
"rsi": 72.593,
"ret": 0.00049056 
},
{
 "date":  -5299,
"name": "GSPC.Close",
"price":  41.03,
"rsi": 72.792,
"ret": 0.0058838 
},
{
 "date":  -5298,
"name": "GSPC.Close",
"price":  41.19,
"rsi": 75.125,
"ret": 0.0038996 
},
{
 "date":  -5294,
"name": "GSPC.Close",
"price":  41.69,
"rsi": 76.568,
"ret": 0.012139 
},
{
 "date":  -5293,
"name": "GSPC.Close",
"price":  43.18,
"rsi": 80.394,
"ret": 0.03574 
},
{
 "date":  -5292,
"name": "GSPC.Close",
"price":  42.58,
"rsi": 87.135,
"ret": -0.013895 
},
{
 "date":  -5291,
"name": "GSPC.Close",
"price":  42.64,
"rsi": 75.828,
"ret": 0.0014091 
},
{
 "date":  -5288,
"name": "GSPC.Close",
"price":  42.75,
"rsi": 76.162,
"ret": 0.0025797 
},
{
 "date":  -5287,
"name": "GSPC.Close",
"price":  42.75,
"rsi": 76.793,
"ret":      0 
},
{
 "date":  -5286,
"name": "GSPC.Close",
"price":  42.24,
"rsi": 76.793,
"ret": -0.01193 
},
{
 "date":  -5285,
"name": "GSPC.Close",
"price":  42.25,
"rsi": 67.219,
"ret": 0.00023674 
},
{
 "date":  -5284,
"name": "GSPC.Close",
"price":   42.4,
"rsi": 67.305,
"ret": 0.0035503 
},
{
 "date":  -5281,
"name": "GSPC.Close",
"price":  42.36,
"rsi": 68.635,
"ret": -0.0009434 
},
{
 "date":  -5280,
"name": "GSPC.Close",
"price":   42.1,
"rsi": 67.842,
"ret": -0.0061379 
},
{
 "date":  -5279,
"name": "GSPC.Close",
"price":  42.23,
"rsi": 62.767,
"ret": 0.0030879 
},
{
 "date":  -5278,
"name": "GSPC.Close",
"price":  42.64,
"rsi": 64.209,
"ret": 0.0097087 
},
{
 "date":  -5277,
"name": "GSPC.Close",
"price":     43,
"rsi": 68.369,
"ret": 0.0084428 
},
{
 "date":  -5274,
"name": "GSPC.Close",
"price":  43.48,
"rsi": 71.501,
"ret": 0.011163 
},
{
 "date":  -5273,
"name": "GSPC.Close",
"price":  43.58,
"rsi": 75.049,
"ret": 0.0022999 
},
{
 "date":  -5272,
"name": "GSPC.Close",
"price":  43.76,
"rsi": 75.727,
"ret": 0.0041303 
},
{
 "date":  -5271,
"name": "GSPC.Close",
"price":   43.5,
"rsi": 76.941,
"ret": -0.0059415 
},
{
 "date":  -5270,
"name": "GSPC.Close",
"price":  43.52,
"rsi": 71.385,
"ret": 0.00045977 
},
{
 "date":  -5267,
"name": "GSPC.Close",
"price":  42.93,
"rsi": 71.555,
"ret": -0.013557 
},
{
 "date":  -5266,
"name": "GSPC.Close",
"price":  43.03,
"rsi": 60.186,
"ret": 0.0023294 
},
{
 "date":  -5265,
"name": "GSPC.Close",
"price":  43.09,
"rsi": 61.308,
"ret": 0.0013944 
},
{
 "date":  -5264,
"name": "GSPC.Close",
"price":  42.36,
"rsi":     62,
"ret": -0.016941 
},
{
 "date":  -5263,
"name": "GSPC.Close",
"price":  42.56,
"rsi": 50.229,
"ret": 0.0047214 
},
{
 "date":  -5260,
"name": "GSPC.Close",
"price":  42.31,
"rsi": 52.869,
"ret": -0.0058741 
},
{
 "date":  -5259,
"name": "GSPC.Close",
"price":  41.75,
"rsi": 49.345,
"ret": -0.013236 
},
{
 "date":  -5258,
"name": "GSPC.Close",
"price":  41.74,
"rsi":  42.51,
"ret": -0.00023952 
},
{
 "date":  -5257,
"name": "GSPC.Close",
"price":  42.13,
"rsi": 42.398,
"ret": 0.0093436 
},
{
 "date":  -5256,
"name": "GSPC.Close",
"price":  42.21,
"rsi": 48.179,
"ret": 0.0018989 
},
{
 "date":  -5253,
"name": "GSPC.Close",
"price":  42.17,
"rsi": 49.304,
"ret": -0.00094764 
},
{
 "date":  -5252,
"name": "GSPC.Close",
"price":  41.86,
"rsi": 48.734,
"ret": -0.0073512 
},
{
 "date":  -5251,
"name": "GSPC.Close",
"price":   41.9,
"rsi": 44.451,
"ret": 0.00095557 
},
{
 "date":  -5250,
"name": "GSPC.Close",
"price":  41.84,
"rsi": 45.121,
"ret": -0.001432 
},
{
 "date":  -5249,
"name": "GSPC.Close",
"price":  42.02,
"rsi": 44.258,
"ret": 0.0043021 
},
{
 "date":  -5246,
"name": "GSPC.Close",
"price":  41.98,
"rsi": 47.501,
"ret": -0.00095193 
},
{
 "date":  -5245,
"name": "GSPC.Close",
"price":  42.55,
"rsi": 46.849,
"ret": 0.013578 
},
{
 "date":  -5244,
"name": "GSPC.Close",
"price":  42.61,
"rsi":   56.1,
"ret": 0.0014101 
},
{
 "date":  -5243,
"name": "GSPC.Close",
"price":   42.8,
"rsi": 56.949,
"ret": 0.004459 
},
{
 "date":  -5242,
"name": "GSPC.Close",
"price":  42.99,
"rsi": 59.614,
"ret": 0.0044393 
},
{
 "date":  -5239,
"name": "GSPC.Close",
"price":  42.96,
"rsi": 62.138,
"ret": -0.00069784 
},
{
 "date":  -5238,
"name": "GSPC.Close",
"price":  42.92,
"rsi": 61.484,
"ret": -0.0009311 
},
{
 "date":  -5237,
"name": "GSPC.Close",
"price":  43.18,
"rsi":  60.57,
"ret": 0.0060578 
},
{
 "date":  -5236,
"name": "GSPC.Close",
"price":  43.37,
"rsi": 64.288,
"ret": 0.0044002 
},
{
 "date":  -5235,
"name": "GSPC.Close",
"price":   43.6,
"rsi": 66.755,
"ret": 0.0053032 
},
{
 "date":  -5231,
"name": "GSPC.Close",
"price":  43.86,
"rsi": 69.502,
"ret": 0.0059633 
},
{
 "date":  -5230,
"name": "GSPC.Close",
"price":  43.85,
"rsi": 72.289,
"ret": -0.000228 
},
{
 "date":  -5229,
"name": "GSPC.Close",
"price":  43.88,
"rsi": 72.016,
"ret": 0.00068415 
},
{
 "date":  -5228,
"name": "GSPC.Close",
"price":  43.89,
"rsi": 72.353,
"ret": 0.00022789 
},
{
 "date":  -5225,
"name": "GSPC.Close",
"price":  44.19,
"rsi": 72.472,
"ret": 0.0068353 
},
{
 "date":  -5224,
"name": "GSPC.Close",
"price":   44.8,
"rsi": 75.831,
"ret": 0.013804 
},
{
 "date":  -5223,
"name": "GSPC.Close",
"price":  44.99,
"rsi": 80.928,
"ret": 0.0042411 
},
{
 "date":  -5222,
"name": "GSPC.Close",
"price":  44.75,
"rsi": 82.188,
"ret": -0.0053345 
},
{
 "date":  -5221,
"name": "GSPC.Close",
"price":  45.09,
"rsi": 75.411,
"ret": 0.0075978 
},
{
 "date":  -5218,
"name": "GSPC.Close",
"price":  45.16,
"rsi": 78.159,
"ret": 0.0015525 
},
{
 "date":  -5217,
"name": "GSPC.Close",
"price":  45.13,
"rsi": 78.687,
"ret": -0.0006643 
},
{
 "date":  -5216,
"name": "GSPC.Close",
"price":  45.39,
"rsi": 77.818,
"ret": 0.0057611 
},
{
 "date":  -5215,
"name": "GSPC.Close",
"price":  45.39,
"rsi":  79.89,
"ret":      0 
},
{
 "date":  -5214,
"name": "GSPC.Close",
"price":  45.63,
"rsi":  79.89,
"ret": 0.0052875 
},
{
 "date":  -5211,
"name": "GSPC.Close",
"price":  42.61,
"rsi": 81.717,
"ret": -0.066185 
},
{
 "date":  -5210,
"name": "GSPC.Close",
"price":  43.58,
"rsi": 36.619,
"ret": 0.022765 
},
{
 "date":  -5209,
"name": "GSPC.Close",
"price":  44.31,
"rsi": 46.779,
"ret": 0.016751 
},
{
 "date":  -5208,
"name": "GSPC.Close",
"price":  44.03,
"rsi": 52.898,
"ret": -0.0063191 
},
{
 "date":  -5207,
"name": "GSPC.Close",
"price":  43.67,
"rsi":   50.5,
"ret": -0.0081762 
},
{
 "date":  -5204,
"name": "GSPC.Close",
"price":  42.49,
"rsi": 47.517,
"ret": -0.027021 
},
{
 "date":  -5203,
"name": "GSPC.Close",
"price":  42.82,
"rsi": 39.318,
"ret": 0.0077665 
},
{
 "date":  -5202,
"name": "GSPC.Close",
"price":  42.99,
"rsi": 42.316,
"ret": 0.0039701 
},
{
 "date":  -5201,
"name": "GSPC.Close",
"price":   42.7,
"rsi": 43.854,
"ret": -0.0067458 
},
{
 "date":  -5200,
"name": "GSPC.Close",
"price":  42.38,
"rsi": 41.806,
"ret": -0.0074941 
},
{
 "date":  -5197,
"name": "GSPC.Close",
"price":  41.15,
"rsi": 39.607,
"ret": -0.029023 
},
{
 "date":  -5196,
"name": "GSPC.Close",
"price":   40.8,
"rsi": 32.527,
"ret": -0.0085055 
},
{
 "date":  -5195,
"name": "GSPC.Close",
"price":  41.52,
"rsi": 30.837,
"ret": 0.017647 
},
{
 "date":  -5194,
"name": "GSPC.Close",
"price":  41.39,
"rsi": 37.974,
"ret": -0.003131 
},
{
 "date":  -5193,
"name": "GSPC.Close",
"price":  41.22,
"rsi": 37.227,
"ret": -0.0041073 
},
{
 "date":  -5190,
"name": "GSPC.Close",
"price":  41.35,
"rsi": 36.224,
"ret": 0.0031538 
},
{
 "date":  -5189,
"name": "GSPC.Close",
"price":  41.65,
"rsi": 37.609,
"ret": 0.0072551 
},
{
 "date":  -5188,
"name": "GSPC.Close",
"price":  42.07,
"rsi": 40.803,
"ret": 0.010084 
},
{
 "date":  -5187,
"name": "GSPC.Close",
"price":  42.59,
"rsi": 45.046,
"ret": 0.01236 
},
{
 "date":  -5186,
"name": "GSPC.Close",
"price":  42.59,
"rsi": 49.839,
"ret":      0 
},
{
 "date":  -5183,
"name": "GSPC.Close",
"price":  42.91,
"rsi": 49.839,
"ret": 0.0075135 
},
{
 "date":  -5182,
"name": "GSPC.Close",
"price":  42.63,
"rsi": 52.779,
"ret": -0.0065253 
},
{
 "date":  -5181,
"name": "GSPC.Close",
"price":  42.29,
"rsi": 50.017,
"ret": -0.0079756 
},
{
 "date":  -5180,
"name": "GSPC.Close",
"price":  42.34,
"rsi": 46.813,
"ret": 0.0011823 
},
{
 "date":  -5179,
"name": "GSPC.Close",
"price":  42.37,
"rsi": 47.347,
"ret": 0.00070855 
},
{
 "date":  -5176,
"name": "GSPC.Close",
"price":  42.34,
"rsi": 47.687,
"ret": -0.00070805 
},
{
 "date":  -5175,
"name": "GSPC.Close",
"price":  42.28,
"rsi": 47.358,
"ret": -0.0014171 
},
{
 "date":  -5174,
"name": "GSPC.Close",
"price":  42.35,
"rsi": 46.665,
"ret": 0.0016556 
},
{
 "date":  -5173,
"name": "GSPC.Close",
"price":  43.24,
"rsi": 47.628,
"ret": 0.021015 
},
{
 "date":  -5172,
"name": "GSPC.Close",
"price":  43.96,
"rsi": 58.008,
"ret": 0.016651 
},
{
 "date":  -5169,
"name": "GSPC.Close",
"price":  44.15,
"rsi": 64.191,
"ret": 0.0043221 
},
{
 "date":  -5167,
"name": "GSPC.Close",
"price":  44.61,
"rsi": 65.629,
"ret": 0.010419 
},
{
 "date":  -5166,
"name": "GSPC.Close",
"price":  44.72,
"rsi": 68.888,
"ret": 0.0024658 
},
{
 "date":  -5165,
"name": "GSPC.Close",
"price":  45.24,
"rsi": 69.629,
"ret": 0.011628 
},
{
 "date":  -5162,
"name": "GSPC.Close",
"price":  46.41,
"rsi": 72.915,
"ret": 0.025862 
},
{
 "date":  -5161,
"name": "GSPC.Close",
"price":  46.21,
"rsi": 78.541,
"ret": -0.0043094 
},
{
 "date":  -5160,
"name": "GSPC.Close",
"price":  45.91,
"rsi": 75.648,
"ret": -0.0064921 
},
{
 "date":  -5159,
"name": "GSPC.Close",
"price":  45.59,
"rsi":   71.4,
"ret": -0.0069702 
},
{
 "date":  -5158,
"name": "GSPC.Close",
"price":  45.54,
"rsi": 67.074,
"ret": -0.0010967 
},
{
 "date":  -5155,
"name": "GSPC.Close",
"price":  45.22,
"rsi": 66.397,
"ret": -0.0070268 
},
{
 "date":  -5154,
"name": "GSPC.Close",
"price":  45.66,
"rsi": 62.078,
"ret": 0.0097302 
},
{
 "date":  -5153,
"name": "GSPC.Close",
"price":  45.72,
"rsi":  65.41,
"ret": 0.0013141 
},
{
 "date":  -5151,
"name": "GSPC.Close",
"price":  45.68,
"rsi":  65.85,
"ret": -0.00087489 
},
{
 "date":  -5148,
"name": "GSPC.Close",
"price":  45.38,
"rsi": 65.254,
"ret": -0.0065674 
},
{
 "date":  -5147,
"name": "GSPC.Close",
"price":  45.56,
"rsi": 60.804,
"ret": 0.0039665 
},
{
 "date":  -5146,
"name": "GSPC.Close",
"price":  45.51,
"rsi": 62.458,
"ret": -0.0010975 
},
{
 "date":  -5145,
"name": "GSPC.Close",
"price":  45.35,
"rsi": 61.679,
"ret": -0.0035157 
},
{
 "date":  -5144,
"name": "GSPC.Close",
"price":  45.44,
"rsi": 59.138,
"ret": 0.0019846 
},
{
 "date":  -5141,
"name": "GSPC.Close",
"price":   45.7,
"rsi": 60.133,
"ret": 0.0057218 
},
{
 "date":  -5140,
"name": "GSPC.Close",
"price":   45.7,
"rsi":  62.94,
"ret":      0 
},
{
 "date":  -5139,
"name": "GSPC.Close",
"price":  45.55,
"rsi":  62.94,
"ret": -0.0032823 
},
{
 "date":  -5138,
"name": "GSPC.Close",
"price":  45.82,
"rsi": 60.108,
"ret": 0.0059276 
},
{
 "date":  -5137,
"name": "GSPC.Close",
"price":  45.89,
"rsi": 63.309,
"ret": 0.0015277 
},
{
 "date":  -5134,
"name": "GSPC.Close",
"price":  45.42,
"rsi": 64.112,
"ret": -0.010242 
},
{
 "date":  -5133,
"name": "GSPC.Close",
"price":  45.45,
"rsi": 55.345,
"ret": 0.0006605 
},
{
 "date":  -5132,
"name": "GSPC.Close",
"price":  45.07,
"rsi": 55.761,
"ret": -0.0083608 
},
{
 "date":  -5131,
"name": "GSPC.Close",
"price":  45.06,
"rsi": 49.476,
"ret": -0.00022188 
},
{
 "date":  -5130,
"name": "GSPC.Close",
"price":  45.13,
"rsi": 49.318,
"ret": 0.0015535 
},
{
 "date":  -5127,
"name": "GSPC.Close",
"price":  45.02,
"rsi": 50.506,
"ret": -0.0024374 
},
{
 "date":  -5126,
"name": "GSPC.Close",
"price":  44.95,
"rsi": 48.579,
"ret": -0.0015549 
},
{
 "date":  -5125,
"name": "GSPC.Close",
"price":  45.84,
"rsi": 47.341,
"ret": 0.0198 
},
{
 "date":  -5124,
"name": "GSPC.Close",
"price":  45.41,
"rsi": 60.962,
"ret": -0.0093805 
},
{
 "date":  -5123,
"name": "GSPC.Close",
"price":   45.5,
"rsi": 53.731,
"ret": 0.0019819 
},
{
 "date":  -5119,
"name": "GSPC.Close",
"price":  45.22,
"rsi": 54.936,
"ret": -0.0061538 
},
{
 "date":  -5118,
"name": "GSPC.Close",
"price":  45.05,
"rsi": 50.527,
"ret": -0.0037594 
},
{
 "date":  -5117,
"name": "GSPC.Close",
"price":  45.15,
"rsi": 48.008,
"ret": 0.0022198 
},
{
 "date":  -5116,
"name": "GSPC.Close",
"price":  45.48,
"rsi":   49.6,
"ret": 0.007309 
},
{
 "date":  -5112,
"name": "GSPC.Close",
"price":  45.16,
"rsi": 54.545,
"ret": -0.0070361 
},
{
 "date":  -5111,
"name": "GSPC.Close",
"price":     45,
"rsi": 49.476,
"ret": -0.003543 
},
{
 "date":  -5110,
"name": "GSPC.Close",
"price":  44.95,
"rsi": 47.118,
"ret": -0.0011111 
},
{
 "date":  -5109,
"name": "GSPC.Close",
"price":  45.14,
"rsi": 46.374,
"ret": 0.0042269 
},
{
 "date":  -5106,
"name": "GSPC.Close",
"price":  44.51,
"rsi": 49.628,
"ret": -0.013957 
},
{
 "date":  -5105,
"name": "GSPC.Close",
"price":  44.16,
"rsi": 40.789,
"ret": -0.0078634 
},
{
 "date":  -5104,
"name": "GSPC.Close",
"price":  44.38,
"rsi": 36.861,
"ret": 0.0049819 
},
{
 "date":  -5103,
"name": "GSPC.Close",
"price":  44.75,
"rsi": 40.725,
"ret": 0.0083371 
},
{
 "date":  -5102,
"name": "GSPC.Close",
"price":  44.67,
"rsi": 46.639,
"ret": -0.0017877 
},
{
 "date":  -5099,
"name": "GSPC.Close",
"price":  44.14,
"rsi": 45.581,
"ret": -0.011865 
},
{
 "date":  -5098,
"name": "GSPC.Close",
"price":  44.47,
"rsi": 39.226,
"ret": 0.0074762 
},
{
 "date":  -5097,
"name": "GSPC.Close",
"price":  44.17,
"rsi": 44.422,
"ret": -0.0067461 
},
{
 "date":  -5096,
"name": "GSPC.Close",
"price":  43.72,
"rsi": 40.991,
"ret": -0.010188 
},
{
 "date":  -5095,
"name": "GSPC.Close",
"price":  43.22,
"rsi": 36.444,
"ret": -0.011436 
},
{
 "date":  -5092,
"name": "GSPC.Close",
"price":  43.11,
"rsi": 32.174,
"ret": -0.0025451 
},
{
 "date":  -5091,
"name": "GSPC.Close",
"price":  43.65,
"rsi": 31.305,
"ret": 0.012526 
},
{
 "date":  -5090,
"name": "GSPC.Close",
"price":  43.72,
"rsi": 39.889,
"ret": 0.0016037 
},
{
 "date":  -5089,
"name": "GSPC.Close",
"price":  43.46,
"rsi": 40.919,
"ret": -0.0059469 
},
{
 "date":  -5088,
"name": "GSPC.Close",
"price":  43.35,
"rsi": 38.293,
"ret": -0.0025311 
},
{
 "date":  -5085,
"name": "GSPC.Close",
"price":   43.5,
"rsi": 37.205,
"ret": 0.0034602 
},
{
 "date":  -5084,
"name": "GSPC.Close",
"price":  43.82,
"rsi":  39.72,
"ret": 0.0073563 
},
{
 "date":  -5083,
"name": "GSPC.Close",
"price":  44.03,
"rsi": 44.799,
"ret": 0.0047923 
},
{
 "date":  -5082,
"name": "GSPC.Close",
"price":  44.22,
"rsi": 47.902,
"ret": 0.0043152 
},
{
 "date":  -5081,
"name": "GSPC.Close",
"price":  44.78,
"rsi": 50.607,
"ret": 0.012664 
},
{
 "date":  -5078,
"name": "GSPC.Close",
"price":  44.81,
"rsi": 57.595,
"ret": 0.00066994 
},
{
 "date":  -5077,
"name": "GSPC.Close",
"price":   44.6,
"rsi": 57.938,
"ret": -0.0046865 
},
{
 "date":  -5076,
"name": "GSPC.Close",
"price":  44.16,
"rsi": 54.605,
"ret": -0.0098655 
},
{
 "date":  -5075,
"name": "GSPC.Close",
"price":  43.66,
"rsi": 48.332,
"ret": -0.011322 
},
{
 "date":  -5074,
"name": "GSPC.Close",
"price":  43.64,
"rsi": 42.375,
"ret": -0.00045809 
},
{
 "date":  -5071,
"name": "GSPC.Close",
"price":  43.58,
"rsi": 42.151,
"ret": -0.0013749 
},
{
 "date":  -5070,
"name": "GSPC.Close",
"price":  43.42,
"rsi": 41.444,
"ret": -0.0036714 
},
{
 "date":  -5069,
"name": "GSPC.Close",
"price":  44.04,
"rsi": 39.539,
"ret": 0.014279 
},
{
 "date":  -5068,
"name": "GSPC.Close",
"price":  43.82,
"rsi":  49.27,
"ret": -0.0049955 
},
{
 "date":  -5067,
"name": "GSPC.Close",
"price":  44.52,
"rsi": 46.415,
"ret": 0.015974 
},
{
 "date":  -5064,
"name": "GSPC.Close",
"price":  44.45,
"rsi": 55.292,
"ret": -0.0015723 
},
{
 "date":  -5063,
"name": "GSPC.Close",
"price":  44.56,
"rsi": 54.322,
"ret": 0.0024747 
},
{
 "date":  -5061,
"name": "GSPC.Close",
"price":  44.95,
"rsi": 55.638,
"ret": 0.0087522 
},
{
 "date":  -5060,
"name": "GSPC.Close",
"price":  45.32,
"rsi": 60.034,
"ret": 0.0082314 
},
{
 "date":  -5057,
"name": "GSPC.Close",
"price":  45.27,
"rsi": 63.708,
"ret": -0.0011033 
},
{
 "date":  -5056,
"name": "GSPC.Close",
"price":  45.43,
"rsi": 62.867,
"ret": 0.0035343 
},
{
 "date":  -5055,
"name": "GSPC.Close",
"price":  45.34,
"rsi": 64.483,
"ret": -0.0019811 
},
{
 "date":  -5054,
"name": "GSPC.Close",
"price":  45.54,
"rsi": 62.827,
"ret": 0.0044111 
},
{
 "date":  -5053,
"name": "GSPC.Close",
"price":  45.81,
"rsi": 64.979,
"ret": 0.0059289 
},
{
 "date":  -5050,
"name": "GSPC.Close",
"price":  46.06,
"rsi": 67.699,
"ret": 0.0054573 
},
{
 "date":  -5049,
"name": "GSPC.Close",
"price":  46.04,
"rsi":  70.02,
"ret": -0.00043422 
},
{
 "date":  -5048,
"name": "GSPC.Close",
"price":  46.01,
"rsi": 69.589,
"ret": -0.00065161 
},
{
 "date":  -5047,
"name": "GSPC.Close",
"price":  46.12,
"rsi": 68.904,
"ret": 0.0023908 
},
{
 "date":  -5046,
"name": "GSPC.Close",
"price":   46.7,
"rsi": 70.068,
"ret": 0.012576 
},
{
 "date":  -5043,
"name": "GSPC.Close",
"price":  47.13,
"rsi": 75.312,
"ret": 0.0092077 
},
{
 "date":  -5042,
"name": "GSPC.Close",
"price":  47.06,
"rsi": 78.342,
"ret": -0.0014853 
},
{
 "date":  -5041,
"name": "GSPC.Close",
"price":  47.53,
"rsi": 76.692,
"ret": 0.0099873 
},
{
 "date":  -5040,
"name": "GSPC.Close",
"price":  47.99,
"rsi": 79.772,
"ret": 0.0096781 
},
{
 "date":  -5039,
"name": "GSPC.Close",
"price":  48.14,
"rsi": 82.245,
"ret": 0.0031257 
},
{
 "date":  -5036,
"name": "GSPC.Close",
"price":  48.59,
"rsi": 82.976,
"ret": 0.0093477 
},
{
 "date":  -5035,
"name": "GSPC.Close",
"price":  48.87,
"rsi": 84.975,
"ret": 0.0057625 
},
{
 "date":  -5034,
"name": "GSPC.Close",
"price":  48.23,
"rsi": 86.071,
"ret": -0.013096 
},
{
 "date":  -5033,
"name": "GSPC.Close",
"price":  48.72,
"rsi": 72.971,
"ret": 0.01016 
},
{
 "date":  -5032,
"name": "GSPC.Close",
"price":  48.83,
"rsi": 75.985,
"ret": 0.0022578 
},
{
 "date":  -5029,
"name": "GSPC.Close",
"price":  48.62,
"rsi": 76.615,
"ret": -0.0043006 
},
{
 "date":  -5028,
"name": "GSPC.Close",
"price":  48.25,
"rsi": 72.692,
"ret": -0.00761 
},
{
 "date":  -5027,
"name": "GSPC.Close",
"price":  48.51,
"rsi": 66.256,
"ret": 0.0053886 
},
{
 "date":  -5026,
"name": "GSPC.Close",
"price":  48.48,
"rsi": 68.375,
"ret": -0.00061843 
},
{
 "date":  -5022,
"name": "GSPC.Close",
"price":   48.7,
"rsi": 67.845,
"ret": 0.004538 
},
{
 "date":  -5021,
"name": "GSPC.Close",
"price":  48.53,
"rsi": 69.698,
"ret": -0.0034908 
},
{
 "date":  -5020,
"name": "GSPC.Close",
"price":   48.8,
"rsi": 66.509,
"ret": 0.0055636 
},
{
 "date":  -5019,
"name": "GSPC.Close",
"price":  48.57,
"rsi":  68.94,
"ret": -0.0047131 
},
{
 "date":  -5018,
"name": "GSPC.Close",
"price":  48.85,
"rsi": 64.636,
"ret": 0.0057649 
},
{
 "date":  -5015,
"name": "GSPC.Close",
"price":  48.61,
"rsi": 67.311,
"ret": -0.004913 
},
{
 "date":  -5014,
"name": "GSPC.Close",
"price":  47.93,
"rsi": 62.917,
"ret": -0.013989 
},
{
 "date":  -5013,
"name": "GSPC.Close",
"price":  48.31,
"rsi": 52.467,
"ret": 0.0079282 
},
{
 "date":  -5012,
"name": "GSPC.Close",
"price":  48.02,
"rsi": 56.786,
"ret": -0.0060029 
},
{
 "date":  -5011,
"name": "GSPC.Close",
"price":  47.95,
"rsi":  52.84,
"ret": -0.0014577 
},
{
 "date":  -5008,
"name": "GSPC.Close",
"price":  47.96,
"rsi": 51.902,
"ret": 0.00020855 
},
{
 "date":  -5007,
"name": "GSPC.Close",
"price":  47.93,
"rsi": 52.033,
"ret": -0.00062552 
},
{
 "date":  -5006,
"name": "GSPC.Close",
"price":  47.74,
"rsi": 51.579,
"ret": -0.0039641 
},
{
 "date":  -5005,
"name": "GSPC.Close",
"price":  47.57,
"rsi": 48.684,
"ret": -0.003561 
},
{
 "date":  -5004,
"name": "GSPC.Close",
"price":  47.76,
"rsi": 46.186,
"ret": 0.0039941 
},
{
 "date":  -5001,
"name": "GSPC.Close",
"price":  47.65,
"rsi": 49.316,
"ret": -0.0023032 
},
{
 "date":  -5000,
"name": "GSPC.Close",
"price":  47.26,
"rsi":  47.59,
"ret": -0.0081847 
},
{
 "date":  -4999,
"name": "GSPC.Close",
"price":  47.09,
"rsi": 41.981,
"ret": -0.0035971 
},
{
 "date":  -4998,
"name": "GSPC.Close",
"price":  47.49,
"rsi": 39.779,
"ret": 0.0084944 
},
{
 "date":  -4997,
"name": "GSPC.Close",
"price":  47.99,
"rsi": 46.842,
"ret": 0.010529 
},
{
 "date":  -4994,
"name": "GSPC.Close",
"price":  48.38,
"rsi":  54.09,
"ret": 0.0081267 
},
{
 "date":  -4993,
"name": "GSPC.Close",
"price":  48.16,
"rsi": 58.808,
"ret": -0.0045473 
},
{
 "date":  -4992,
"name": "GSPC.Close",
"price":  48.17,
"rsi": 55.352,
"ret": 0.00020764 
},
{
 "date":  -4991,
"name": "GSPC.Close",
"price":  48.34,
"rsi":  55.48,
"ret": 0.0035292 
},
{
 "date":  -4990,
"name": "GSPC.Close",
"price":  48.51,
"rsi": 57.701,
"ret": 0.0035168 
},
{
 "date":  -4987,
"name": "GSPC.Close",
"price":  48.22,
"rsi": 59.858,
"ret": -0.0059781 
},
{
 "date":  -4986,
"name": "GSPC.Close",
"price":  48.02,
"rsi": 54.732,
"ret": -0.0041477 
},
{
 "date":  -4985,
"name": "GSPC.Close",
"price":  47.94,
"rsi": 51.458,
"ret": -0.001666 
},
{
 "date":  -4984,
"name": "GSPC.Close",
"price":  47.16,
"rsi": 50.166,
"ret": -0.01627 
},
{
 "date":  -4983,
"name": "GSPC.Close",
"price":  47.12,
"rsi": 39.697,
"ret": -0.00084818 
},
{
 "date":  -4980,
"name": "GSPC.Close",
"price":  46.86,
"rsi": 39.245,
"ret": -0.0055178 
},
{
 "date":  -4979,
"name": "GSPC.Close",
"price":  46.37,
"rsi": 36.346,
"ret": -0.010457 
},
{
 "date":  -4978,
"name": "GSPC.Close",
"price":  46.05,
"rsi": 31.608,
"ret": -0.006901 
},
{
 "date":  -4977,
"name": "GSPC.Close",
"price":  46.61,
"rsi": 28.953,
"ret": 0.012161 
},
{
 "date":  -4976,
"name": "GSPC.Close",
"price":  46.39,
"rsi": 38.662,
"ret": -0.00472 
},
{
 "date":  -4973,
"name": "GSPC.Close",
"price":  45.99,
"rsi": 36.549,
"ret": -0.0086225 
},
{
 "date":  -4972,
"name": "GSPC.Close",
"price":  45.26,
"rsi": 33.016,
"ret": -0.015873 
},
{
 "date":  -4971,
"name": "GSPC.Close",
"price":  45.02,
"rsi": 27.744,
"ret": -0.0053027 
},
{
 "date":  -4970,
"name": "GSPC.Close",
"price":   44.6,
"rsi":  26.26,
"ret": -0.0093292 
},
{
 "date":  -4969,
"name": "GSPC.Close",
"price":  44.62,
"rsi": 23.854,
"ret": 0.00044843 
},
{
 "date":  -4966,
"name": "GSPC.Close",
"price":   44.1,
"rsi":  24.21,
"ret": -0.011654 
},
{
 "date":  -4965,
"name": "GSPC.Close",
"price":  45.11,
"rsi": 21.408,
"ret": 0.022902 
},
{
 "date":  -4963,
"name": "GSPC.Close",
"price":   45.2,
"rsi": 36.728,
"ret": 0.0019951 
},
{
 "date":  -4962,
"name": "GSPC.Close",
"price":  45.58,
"rsi":  37.89,
"ret": 0.0084071 
},
{
 "date":  -4959,
"name": "GSPC.Close",
"price":  45.85,
"rsi": 42.676,
"ret": 0.0059237 
},
{
 "date":  -4958,
"name": "GSPC.Close",
"price":  45.86,
"rsi": 45.868,
"ret": 0.0002181 
},
{
 "date":  -4957,
"name": "GSPC.Close",
"price":  45.63,
"rsi": 45.988,
"ret": -0.0050153 
},
{
 "date":  -4956,
"name": "GSPC.Close",
"price":  45.99,
"rsi": 43.595,
"ret": 0.0078895 
},
{
 "date":  -4955,
"name": "GSPC.Close",
"price":  45.14,
"rsi": 48.144,
"ret": -0.018482 
},
{
 "date":  -4952,
"name": "GSPC.Close",
"price":  45.71,
"rsi": 39.952,
"ret": 0.012627 
},
{
 "date":  -4951,
"name": "GSPC.Close",
"price":  46.36,
"rsi": 46.523,
"ret": 0.01422 
},
{
 "date":  -4950,
"name": "GSPC.Close",
"price":  46.42,
"rsi": 52.858,
"ret": 0.0012942 
},
{
 "date":  -4949,
"name": "GSPC.Close",
"price":  46.31,
"rsi": 53.407,
"ret": -0.0023697 
},
{
 "date":  -4948,
"name": "GSPC.Close",
"price":  46.37,
"rsi": 52.207,
"ret": 0.0012956 
},
{
 "date":  -4945,
"name": "GSPC.Close",
"price":  46.17,
"rsi":  52.83,
"ret": -0.0043131 
},
{
 "date":  -4944,
"name": "GSPC.Close",
"price":  46.22,
"rsi":  50.47,
"ret": 0.001083 
},
{
 "date":  -4943,
"name": "GSPC.Close",
"price":  46.41,
"rsi": 51.059,
"ret": 0.0041108 
},
{
 "date":  -4942,
"name": "GSPC.Close",
"price":  46.73,
"rsi": 53.328,
"ret": 0.0068951 
},
{
 "date":  -4941,
"name": "GSPC.Close",
"price":  46.59,
"rsi": 56.949,
"ret": -0.0029959 
},
{
 "date":  -4938,
"name": "GSPC.Close",
"price":  46.41,
"rsi": 54.941,
"ret": -0.0038635 
},
{
 "date":  -4937,
"name": "GSPC.Close",
"price":  46.72,
"rsi": 52.383,
"ret": 0.0066796 
},
{
 "date":  -4936,
"name": "GSPC.Close",
"price":  47.07,
"rsi": 56.168,
"ret": 0.0074914 
},
{
 "date":  -4935,
"name": "GSPC.Close",
"price":  47.13,
"rsi":  60.03,
"ret": 0.0012747 
},
{
 "date":  -4934,
"name": "GSPC.Close",
"price":  46.97,
"rsi":  60.67,
"ret": -0.0033949 
},
{
 "date":  -4931,
"name": "GSPC.Close",
"price":  46.93,
"rsi": 58.004,
"ret": -0.00085161 
},
{
 "date":  -4930,
"name": "GSPC.Close",
"price":  47.32,
"rsi": 57.325,
"ret": 0.0083102 
},
{
 "date":  -4928,
"name": "GSPC.Close",
"price":   47.8,
"rsi": 61.992,
"ret": 0.010144 
},
{
 "date":  -4927,
"name": "GSPC.Close",
"price":  48.04,
"rsi": 66.804,
"ret": 0.0050209 
},
{
 "date":  -4924,
"name": "GSPC.Close",
"price":  48.25,
"rsi": 68.923,
"ret": 0.0043714 
},
{
 "date":  -4923,
"name": "GSPC.Close",
"price":  48.54,
"rsi": 70.686,
"ret": 0.0060104 
},
{
 "date":  -4922,
"name": "GSPC.Close",
"price":  48.69,
"rsi": 72.967,
"ret": 0.0030902 
},
{
 "date":  -4921,
"name": "GSPC.Close",
"price":  48.58,
"rsi":  74.09,
"ret": -0.0022592 
},
{
 "date":  -4920,
"name": "GSPC.Close",
"price":  48.72,
"rsi": 71.736,
"ret": 0.0028818 
},
{
 "date":  -4917,
"name": "GSPC.Close",
"price":  49.14,
"rsi": 72.915,
"ret": 0.0086207 
},
{
 "date":  -4916,
"name": "GSPC.Close",
"price":  49.31,
"rsi": 76.132,
"ret": 0.0034595 
},
{
 "date":  -4915,
"name": "GSPC.Close",
"price":   49.3,
"rsi": 77.307,
"ret": -0.0002028 
},
{
 "date":  -4914,
"name": "GSPC.Close",
"price":  49.32,
"rsi": 77.067,
"ret": 0.00040568 
},
{
 "date":  -4913,
"name": "GSPC.Close",
"price":  49.35,
"rsi": 77.219,
"ret": 0.00060827 
},
{
 "date":  -4910,
"name": "GSPC.Close",
"price":  49.33,
"rsi": 77.462,
"ret": -0.00040527 
},
{
 "date":  -4909,
"name": "GSPC.Close",
"price":  49.33,
"rsi": 76.875,
"ret":      0 
},
{
 "date":  -4908,
"name": "GSPC.Close",
"price":  49.44,
"rsi": 76.875,
"ret": 0.0022299 
},
{
 "date":  -4907,
"name": "GSPC.Close",
"price":  49.48,
"rsi": 77.941,
"ret": 0.00080906 
},
{
 "date":  -4906,
"name": "GSPC.Close",
"price":  49.08,
"rsi": 78.332,
"ret": -0.0080841 
},
{
 "date":  -4903,
"name": "GSPC.Close",
"price":     49,
"rsi": 65.775,
"ret": -0.00163 
},
{
 "date":  -4902,
"name": "GSPC.Close",
"price":  49.39,
"rsi":  63.58,
"ret": 0.0079592 
},
{
 "date":  -4901,
"name": "GSPC.Close",
"price":  49.62,
"rsi":  69.01,
"ret": 0.0046568 
},
{
 "date":  -4900,
"name": "GSPC.Close",
"price":  49.64,
"rsi":  71.69,
"ret": 0.00040306 
},
{
 "date":  -4899,
"name": "GSPC.Close",
"price":  49.64,
"rsi": 71.918,
"ret":      0 
},
{
 "date":  -4896,
"name": "GSPC.Close",
"price":  48.96,
"rsi": 71.918,
"ret": -0.013699 
},
{
 "date":  -4895,
"name": "GSPC.Close",
"price":  49.16,
"rsi": 54.614,
"ret": 0.004085 
},
{
 "date":  -4894,
"name": "GSPC.Close",
"price":  49.36,
"rsi": 57.828,
"ret": 0.0040683 
},
{
 "date":  -4893,
"name": "GSPC.Close",
"price":  49.32,
"rsi": 60.816,
"ret": -0.00081037 
},
{
 "date":  -4892,
"name": "GSPC.Close",
"price":  49.09,
"rsi": 59.902,
"ret": -0.0046634 
},
{
 "date":  -4889,
"name": "GSPC.Close",
"price":  48.58,
"rsi": 54.801,
"ret": -0.010389 
},
{
 "date":  -4888,
"name": "GSPC.Close",
"price":     48,
"rsi":  45.54,
"ret": -0.011939 
},
{
 "date":  -4887,
"name": "GSPC.Close",
"price":  48.99,
"rsi": 37.731,
"ret": 0.020625 
},
{
 "date":  -4886,
"name": "GSPC.Close",
"price":  48.88,
"rsi": 52.655,
"ret": -0.0022454 
},
{
 "date":  -4885,
"name": "GSPC.Close",
"price":  48.82,
"rsi": 51.187,
"ret": -0.0012275 
},
{
 "date":  -4882,
"name": "GSPC.Close",
"price":  48.25,
"rsi": 50.362,
"ret": -0.011676 
},
{
 "date":  -4881,
"name": "GSPC.Close",
"price":  47.89,
"rsi": 43.235,
"ret": -0.0074611 
},
{
 "date":  -4880,
"name": "GSPC.Close",
"price":  47.42,
"rsi": 39.439,
"ret": -0.0098142 
},
{
 "date":  -4879,
"name": "GSPC.Close",
"price":     48,
"rsi": 35.105,
"ret": 0.012231 
},
{
 "date":  -4878,
"name": "GSPC.Close",
"price":  47.95,
"rsi": 43.374,
"ret": -0.0010417 
},
{
 "date":  -4875,
"name": "GSPC.Close",
"price":  47.66,
"rsi": 42.867,
"ret": -0.006048 
},
{
 "date":  -4874,
"name": "GSPC.Close",
"price":  47.57,
"rsi":  39.95,
"ret": -0.0018884 
},
{
 "date":  -4873,
"name": "GSPC.Close",
"price":  47.36,
"rsi": 39.061,
"ret": -0.0044145 
},
{
 "date":  -4872,
"name": "GSPC.Close",
"price":  46.94,
"rsi": 36.994,
"ret": -0.0088682 
},
{
 "date":  -4871,
"name": "GSPC.Close",
"price":  47.51,
"rsi": 33.208,
"ret": 0.012143 
},
{
 "date":  -4867,
"name": "GSPC.Close",
"price":  47.89,
"rsi": 41.898,
"ret": 0.0079983 
},
{
 "date":  -4866,
"name": "GSPC.Close",
"price":  48.02,
"rsi": 46.862,
"ret": 0.0027146 
},
{
 "date":  -4865,
"name": "GSPC.Close",
"price":   48.1,
"rsi": 48.483,
"ret": 0.001666 
},
{
 "date":  -4864,
"name": "GSPC.Close",
"price":  47.81,
"rsi": 49.504,
"ret": -0.0060291 
},
{
 "date":  -4861,
"name": "GSPC.Close",
"price":  47.56,
"rsi": 45.949,
"ret": -0.005229 
},
{
 "date":  -4860,
"name": "GSPC.Close",
"price":  47.38,
"rsi": 43.077,
"ret": -0.0037847 
},
{
 "date":  -4859,
"name": "GSPC.Close",
"price":  47.05,
"rsi": 41.085,
"ret": -0.006965 
},
{
 "date":  -4858,
"name": "GSPC.Close",
"price":  46.09,
"rsi": 37.649,
"ret": -0.020404 
},
{
 "date":  -4857,
"name": "GSPC.Close",
"price":  47.21,
"rsi": 29.832,
"ret": 0.0243 
},
{
 "date":  -4854,
"name": "GSPC.Close",
"price":   47.1,
"rsi": 44.349,
"ret": -0.00233 
},
{
 "date":  -4853,
"name": "GSPC.Close",
"price":  46.79,
"rsi":   43.4,
"ret": -0.0065817 
},
{
 "date":  -4852,
"name": "GSPC.Close",
"price":  46.24,
"rsi": 40.751,
"ret": -0.011755 
},
{
 "date":  -4851,
"name": "GSPC.Close",
"price":  46.21,
"rsi": 36.496,
"ret": -0.00064879 
},
{
 "date":  -4850,
"name": "GSPC.Close",
"price":  46.58,
"rsi": 36.273,
"ret": 0.0080069 
},
{
 "date":  -4847,
"name": "GSPC.Close",
"price":   46.4,
"rsi": 41.047,
"ret": -0.0038643 
},
{
 "date":  -4846,
"name": "GSPC.Close",
"price":  45.75,
"rsi": 39.497,
"ret": -0.014009 
},
{
 "date":  -4845,
"name": "GSPC.Close",
"price":  45.82,
"rsi": 34.439,
"ret": 0.0015301 
},
{
 "date":  -4844,
"name": "GSPC.Close",
"price":   45.6,
"rsi": 35.399,
"ret": -0.0048014 
},
{
 "date":  -4843,
"name": "GSPC.Close",
"price":  45.35,
"rsi": 33.728,
"ret": -0.0054825 
},
{
 "date":  -4840,
"name": "GSPC.Close",
"price":   44.7,
"rsi": 31.887,
"ret": -0.014333 
},
{
 "date":  -4839,
"name": "GSPC.Close",
"price":  45.52,
"rsi": 27.658,
"ret": 0.018345 
},
{
 "date":  -4838,
"name": "GSPC.Close",
"price":  46.28,
"rsi": 38.701,
"ret": 0.016696 
},
{
 "date":  -4837,
"name": "GSPC.Close",
"price":  46.29,
"rsi": 46.806,
"ret": 0.00021608 
},
{
 "date":  -4836,
"name": "GSPC.Close",
"price":  46.45,
"rsi": 46.906,
"ret": 0.0034565 
},
{
 "date":  -4833,
"name": "GSPC.Close",
"price":  46.43,
"rsi": 48.563,
"ret": -0.00043057 
},
{
 "date":  -4832,
"name": "GSPC.Close",
"price":   46.2,
"rsi":  48.36,
"ret": -0.0049537 
},
{
 "date":  -4831,
"name": "GSPC.Close",
"price":  46.84,
"rsi": 45.977,
"ret": 0.013853 
},
{
 "date":  -4830,
"name": "GSPC.Close",
"price":  46.81,
"rsi": 52.928,
"ret": -0.00064048 
},
{
 "date":  -4829,
"name": "GSPC.Close",
"price":     47,
"rsi": 52.586,
"ret": 0.004059 
},
{
 "date":  -4826,
"name": "GSPC.Close",
"price":  46.86,
"rsi": 54.585,
"ret": -0.0029787 
},
{
 "date":  -4825,
"name": "GSPC.Close",
"price":  46.62,
"rsi": 52.818,
"ret": -0.0051216 
},
{
 "date":  -4824,
"name": "GSPC.Close",
"price":  46.26,
"rsi":  49.84,
"ret": -0.007722 
},
{
 "date":  -4823,
"name": "GSPC.Close",
"price":  46.34,
"rsi": 45.679,
"ret": 0.0017294 
},
{
 "date":  -4822,
"name": "GSPC.Close",
"price":  46.24,
"rsi": 46.743,
"ret": -0.002158 
},
{
 "date":  -4819,
"name": "GSPC.Close",
"price":  46.23,
"rsi": 45.542,
"ret": -0.00021626 
},
{
 "date":  -4818,
"name": "GSPC.Close",
"price":  46.12,
"rsi": 45.416,
"ret": -0.0023794 
},
{
 "date":  -4817,
"name": "GSPC.Close",
"price":  45.93,
"rsi": 43.979,
"ret": -0.0041197 
},
{
 "date":  -4816,
"name": "GSPC.Close",
"price":  45.85,
"rsi": 41.534,
"ret": -0.0017418 
},
{
 "date":  -4815,
"name": "GSPC.Close",
"price":  46.27,
"rsi": 40.512,
"ret": 0.0091603 
},
{
 "date":  -4812,
"name": "GSPC.Close",
"price":   46.4,
"rsi": 47.774,
"ret": 0.0028096 
},
{
 "date":  -4811,
"name": "GSPC.Close",
"price":  46.37,
"rsi": 49.816,
"ret": -0.00064655 
},
{
 "date":  -4810,
"name": "GSPC.Close",
"price":  45.58,
"rsi": 49.336,
"ret": -0.017037 
},
{
 "date":  -4809,
"name": "GSPC.Close",
"price":  46.52,
"rsi": 38.759,
"ret": 0.020623 
},
{
 "date":  -4808,
"name": "GSPC.Close",
"price":  46.98,
"rsi": 51.957,
"ret": 0.0098882 
},
{
 "date":  -4805,
"name": "GSPC.Close",
"price":   47.6,
"rsi": 56.857,
"ret": 0.013197 
},
{
 "date":  -4803,
"name": "GSPC.Close",
"price":  47.11,
"rsi": 62.421,
"ret": -0.010294 
},
{
 "date":  -4802,
"name": "GSPC.Close",
"price":  46.73,
"rsi": 56.247,
"ret": -0.0080662 
},
{
 "date":  -4801,
"name": "GSPC.Close",
"price":  46.34,
"rsi": 51.956,
"ret": -0.0083458 
},
{
 "date":  -4798,
"name": "GSPC.Close",
"price":  46.49,
"rsi": 47.915,
"ret": 0.0032369 
},
{
 "date":  -4797,
"name": "GSPC.Close",
"price":  46.27,
"rsi": 49.541,
"ret": -0.0047322 
},
{
 "date":  -4796,
"name": "GSPC.Close",
"price":  46.01,
"rsi": 47.214,
"ret": -0.0056192 
},
{
 "date":  -4795,
"name": "GSPC.Close",
"price":  45.72,
"rsi":  44.55,
"ret": -0.006303 
},
{
 "date":  -4794,
"name": "GSPC.Close",
"price":  45.74,
"rsi": 41.723,
"ret": 0.00043745 
},
{
 "date":  -4791,
"name": "GSPC.Close",
"price":  45.29,
"rsi": 41.996,
"ret": -0.0098382 
},
{
 "date":  -4790,
"name": "GSPC.Close",
"price":  44.89,
"rsi":  37.71,
"ret": -0.008832 
},
{
 "date":  -4789,
"name": "GSPC.Close",
"price":  44.67,
"rsi": 34.353,
"ret": -0.0049009 
},
{
 "date":  -4787,
"name": "GSPC.Close",
"price":  45.14,
"rsi": 32.633,
"ret": 0.010522 
},
{
 "date":  -4784,
"name": "GSPC.Close",
"price":  44.87,
"rsi": 39.593,
"ret": -0.0059814 
},
{
 "date":  -4783,
"name": "GSPC.Close",
"price":  44.91,
"rsi": 37.214,
"ret": 0.00089146 
},
{
 "date":  -4782,
"name": "GSPC.Close",
"price":  44.43,
"rsi":  37.81,
"ret": -0.010688 
},
{
 "date":  -4781,
"name": "GSPC.Close",
"price":  44.38,
"rsi": 33.678,
"ret": -0.0011254 
},
{
 "date":  -4780,
"name": "GSPC.Close",
"price":  45.08,
"rsi":  33.27,
"ret": 0.015773 
},
{
 "date":  -4777,
"name": "GSPC.Close",
"price":  45.98,
"rsi": 43.574,
"ret": 0.019965 
},
{
 "date":  -4776,
"name": "GSPC.Close",
"price":  45.84,
"rsi": 53.512,
"ret": -0.0030448 
},
{
 "date":  -4775,
"name": "GSPC.Close",
"price":  46.39,
"rsi": 51.979,
"ret": 0.011998 
},
{
 "date":  -4774,
"name": "GSPC.Close",
"price":  46.81,
"rsi": 57.172,
"ret": 0.0090537 
},
{
 "date":  -4773,
"name": "GSPC.Close",
"price":  47.04,
"rsi":  60.67,
"ret": 0.0049135 
},
{
 "date":  -4770,
"name": "GSPC.Close",
"price":   46.8,
"rsi": 62.477,
"ret": -0.005102 
},
{
 "date":  -4769,
"name": "GSPC.Close",
"price":  46.48,
"rsi": 59.409,
"ret": -0.0068376 
},
{
 "date":  -4768,
"name": "GSPC.Close",
"price":  46.13,
"rsi": 55.496,
"ret": -0.0075301 
},
{
 "date":  -4767,
"name": "GSPC.Close",
"price":   46.5,
"rsi": 51.501,
"ret": 0.0080208 
},
{
 "date":  -4766,
"name": "GSPC.Close",
"price":  46.54,
"rsi": 55.175,
"ret": 0.00086022 
},
{
 "date":  -4763,
"name": "GSPC.Close",
"price":  46.54,
"rsi": 55.567,
"ret":      0 
},
{
 "date":  -4762,
"name": "GSPC.Close",
"price":  46.54,
"rsi": 55.567,
"ret":      0 
},
{
 "date":  -4761,
"name": "GSPC.Close",
"price":  46.43,
"rsi": 55.567,
"ret": -0.0023636 
},
{
 "date":  -4760,
"name": "GSPC.Close",
"price":  46.07,
"rsi": 53.947,
"ret": -0.0077536 
},
{
 "date":  -4759,
"name": "GSPC.Close",
"price":  46.37,
"rsi": 48.921,
"ret": 0.0065118 
},
{
 "date":  -4754,
"name": "GSPC.Close",
"price":  46.39,
"rsi": 52.862,
"ret": 0.00043131 
},
{
 "date":  -4753,
"name": "GSPC.Close",
"price":  46.35,
"rsi": 53.122,
"ret": -0.00086225 
},
{
 "date":  -4752,
"name": "GSPC.Close",
"price":  46.56,
"rsi": 52.499,
"ret": 0.0045307 
},
{
 "date":  -4749,
"name": "GSPC.Close",
"price":  46.67,
"rsi": 55.452,
"ret": 0.0023625 
},
{
 "date":  -4747,
"name": "GSPC.Close",
"price":   46.2,
"rsi": 56.962,
"ret": -0.010071 
},
{
 "date":  -4746,
"name": "GSPC.Close",
"price":   46.6,
"rsi": 49.278,
"ret": 0.008658 
},
{
 "date":  -4745,
"name": "GSPC.Close",
"price":  46.66,
"rsi": 54.859,
"ret": 0.0012876 
},
{
 "date":  -4742,
"name": "GSPC.Close",
"price":  46.42,
"rsi": 55.648,
"ret": -0.0051436 
},
{
 "date":  -4741,
"name": "GSPC.Close",
"price":  46.25,
"rsi": 51.754,
"ret": -0.0036622 
},
{
 "date":  -4740,
"name": "GSPC.Close",
"price":  46.16,
"rsi": 49.132,
"ret": -0.0019459 
},
{
 "date":  -4739,
"name": "GSPC.Close",
"price":  46.27,
"rsi": 47.752,
"ret": 0.002383 
},
{
 "date":  -4738,
"name": "GSPC.Close",
"price":  46.18,
"rsi": 49.614,
"ret": -0.0019451 
},
{
 "date":  -4735,
"name": "GSPC.Close",
"price":  45.86,
"rsi": 48.104,
"ret": -0.0069294 
},
{
 "date":  -4734,
"name": "GSPC.Close",
"price":  45.18,
"rsi": 43.081,
"ret": -0.014828 
},
{
 "date":  -4733,
"name": "GSPC.Close",
"price":  45.23,
"rsi": 34.773,
"ret": 0.0011067 
},
{
 "date":  -4732,
"name": "GSPC.Close",
"price":  45.22,
"rsi": 35.754,
"ret": -0.00022109 
},
{
 "date":  -4731,
"name": "GSPC.Close",
"price":  44.64,
"rsi": 35.639,
"ret": -0.012826 
},
{
 "date":  -4728,
"name": "GSPC.Close",
"price":   44.4,
"rsi": 29.657,
"ret": -0.0053763 
},
{
 "date":  -4727,
"name": "GSPC.Close",
"price":  44.53,
"rsi": 27.593,
"ret": 0.0029279 
},
{
 "date":  -4726,
"name": "GSPC.Close",
"price":  44.87,
"rsi": 30.418,
"ret": 0.0076353 
},
{
 "date":  -4725,
"name": "GSPC.Close",
"price":  45.03,
"rsi": 37.306,
"ret": 0.0035659 
},
{
 "date":  -4724,
"name": "GSPC.Close",
"price":  44.82,
"rsi": 40.302,
"ret": -0.0046636 
},
{
 "date":  -4721,
"name": "GSPC.Close",
"price":  44.49,
"rsi": 37.752,
"ret": -0.0073628 
},
{
 "date":  -4720,
"name": "GSPC.Close",
"price":  44.71,
"rsi": 34.102,
"ret": 0.0049449 
},
{
 "date":  -4719,
"name": "GSPC.Close",
"price":  44.91,
"rsi":  38.38,
"ret": 0.0044733 
},
{
 "date":  -4718,
"name": "GSPC.Close",
"price":  44.72,
"rsi": 42.062,
"ret": -0.0042307 
},
{
 "date":  -4717,
"name": "GSPC.Close",
"price":  44.62,
"rsi": 39.639,
"ret": -0.0022361 
},
{
 "date":  -4714,
"name": "GSPC.Close",
"price":  44.53,
"rsi": 38.385,
"ret": -0.002017 
},
{
 "date":  -4713,
"name": "GSPC.Close",
"price":  43.89,
"rsi": 37.243,
"ret": -0.014372 
},
{
 "date":  -4712,
"name": "GSPC.Close",
"price":  43.82,
"rsi": 30.335,
"ret": -0.0015949 
},
{
 "date":  -4711,
"name": "GSPC.Close",
"price":  43.62,
"rsi": 29.686,
"ret": -0.0045641 
},
{
 "date":  -4710,
"name": "GSPC.Close",
"price":  43.32,
"rsi": 27.854,
"ret": -0.0068776 
},
{
 "date":  -4707,
"name": "GSPC.Close",
"price":  42.57,
"rsi": 25.328,
"ret": -0.017313 
},
{
 "date":  -4706,
"name": "GSPC.Close",
"price":  42.39,
"rsi": 20.358,
"ret": -0.0042283 
},
{
 "date":  -4705,
"name": "GSPC.Close",
"price":  43.04,
"rsi": 19.375,
"ret": 0.015334 
},
{
 "date":  -4704,
"name": "GSPC.Close",
"price":  42.99,
"rsi": 32.118,
"ret": -0.0011617 
},
{
 "date":  -4703,
"name": "GSPC.Close",
"price":  43.51,
"rsi": 31.703,
"ret": 0.012096 
},
{
 "date":  -4700,
"name": "GSPC.Close",
"price":  43.46,
"rsi": 40.338,
"ret": -0.0011492 
},
{
 "date":  -4699,
"name": "GSPC.Close",
"price":  43.49,
"rsi": 39.817,
"ret": 0.00069029 
},
{
 "date":  -4698,
"name": "GSPC.Close",
"price":  43.63,
"rsi": 40.315,
"ret": 0.0032191 
},
{
 "date":  -4697,
"name": "GSPC.Close",
"price":  43.48,
"rsi":   42.7,
"ret": -0.003438 
},
{
 "date":  -4693,
"name": "GSPC.Close",
"price":  43.38,
"rsi": 40.818,
"ret": -0.0022999 
},
{
 "date":  -4692,
"name": "GSPC.Close",
"price":  43.45,
"rsi": 39.566,
"ret": 0.0016136 
},
{
 "date":  -4691,
"name": "GSPC.Close",
"price":  43.41,
"rsi": 40.932,
"ret": -0.0009206 
},
{
 "date":  -4690,
"name": "GSPC.Close",
"price":  43.26,
"rsi":  40.37,
"ret": -0.0034554 
},
{
 "date":  -4689,
"name": "GSPC.Close",
"price":  43.74,
"rsi": 38.252,
"ret": 0.011096 
},
{
 "date":  -4686,
"name": "GSPC.Close",
"price":  44.06,
"rsi": 47.709,
"ret": 0.007316 
},
{
 "date":  -4685,
"name": "GSPC.Close",
"price":  44.22,
"rsi":  52.89,
"ret": 0.0036314 
},
{
 "date":  -4684,
"name": "GSPC.Close",
"price":  44.23,
"rsi": 55.276,
"ret": 0.00022614 
},
{
 "date":  -4683,
"name": "GSPC.Close",
"price":  44.21,
"rsi": 55.428,
"ret": -0.00045218 
},
{
 "date":  -4682,
"name": "GSPC.Close",
"price":  44.07,
"rsi": 55.025,
"ret": -0.0031667 
},
{
 "date":  -4679,
"name": "GSPC.Close",
"price":  43.78,
"rsi": 52.168,
"ret": -0.0065804 
},
{
 "date":  -4678,
"name": "GSPC.Close",
"price":  43.75,
"rsi": 46.754,
"ret": -0.00068524 
},
{
 "date":  -4677,
"name": "GSPC.Close",
"price":  44.04,
"rsi": 46.219,
"ret": 0.0066286 
},
{
 "date":  -4676,
"name": "GSPC.Close",
"price":  44.07,
"rsi": 51.939,
"ret": 0.0006812 
},
{
 "date":  -4675,
"name": "GSPC.Close",
"price":  44.05,
"rsi": 52.501,
"ret": -0.00045382 
},
{
 "date":  -4672,
"name": "GSPC.Close",
"price":  43.85,
"rsi": 52.064,
"ret": -0.0045403 
},
{
 "date":  -4671,
"name": "GSPC.Close",
"price":  44.04,
"rsi": 47.775,
"ret": 0.004333 
},
{
 "date":  -4670,
"name": "GSPC.Close",
"price":   44.1,
"rsi": 51.834,
"ret": 0.0013624 
},
{
 "date":  -4669,
"name": "GSPC.Close",
"price":  44.11,
"rsi": 53.075,
"ret": 0.00022676 
},
{
 "date":  -4668,
"name": "GSPC.Close",
"price":  44.06,
"rsi":  53.29,
"ret": -0.0011335 
},
{
 "date":  -4665,
"name": "GSPC.Close",
"price":  43.88,
"rsi": 52.002,
"ret": -0.0040853 
},
{
 "date":  -4664,
"name": "GSPC.Close",
"price":  43.91,
"rsi": 47.546,
"ret": 0.00068368 
},
{
 "date":  -4663,
"name": "GSPC.Close",
"price":  44.09,
"rsi":  48.34,
"ret": 0.0040993 
},
{
 "date":  -4662,
"name": "GSPC.Close",
"price":  44.18,
"rsi": 52.946,
"ret": 0.0020413 
},
{
 "date":  -4661,
"name": "GSPC.Close",
"price":  44.11,
"rsi": 55.101,
"ret": -0.0015844 
},
{
 "date":  -4658,
"name": "GSPC.Close",
"price":  44.14,
"rsi": 53.065,
"ret": 0.00068012 
},
{
 "date":  -4657,
"name": "GSPC.Close",
"price":  44.42,
"rsi": 53.852,
"ret": 0.0063435 
},
{
 "date":  -4656,
"name": "GSPC.Close",
"price":  44.54,
"rsi": 60.508,
"ret": 0.0027015 
},
{
 "date":  -4655,
"name": "GSPC.Close",
"price":  44.44,
"rsi": 62.973,
"ret": -0.0022452 
},
{
 "date":  -4654,
"name": "GSPC.Close",
"price":  44.49,
"rsi": 59.633,
"ret": 0.0011251 
},
{
 "date":  -4651,
"name": "GSPC.Close",
"price":  44.39,
"rsi": 60.754,
"ret": -0.0022477 
},
{
 "date":  -4650,
"name": "GSPC.Close",
"price":  44.79,
"rsi": 57.325,
"ret": 0.009011 
},
{
 "date":  -4649,
"name": "GSPC.Close",
"price":  44.98,
"rsi": 65.671,
"ret": 0.004242 
},
{
 "date":  -4648,
"name": "GSPC.Close",
"price":  44.98,
"rsi": 68.793,
"ret":      0 
},
{
 "date":  -4647,
"name": "GSPC.Close",
"price":  44.98,
"rsi": 68.793,
"ret":      0 
},
{
 "date":  -4644,
"name": "GSPC.Close",
"price":  44.95,
"rsi": 68.793,
"ret": -0.00066696 
},
{
 "date":  -4643,
"name": "GSPC.Close",
"price":  45.02,
"rsi": 67.581,
"ret": 0.0015573 
},
{
 "date":  -4642,
"name": "GSPC.Close",
"price":  45.08,
"rsi": 68.955,
"ret": 0.0013327 
},
{
 "date":  -4641,
"name": "GSPC.Close",
"price":  45.41,
"rsi": 70.124,
"ret": 0.0073203 
},
{
 "date":  -4637,
"name": "GSPC.Close",
"price":  45.48,
"rsi": 75.573,
"ret": 0.0015415 
},
{
 "date":  -4636,
"name": "GSPC.Close",
"price":  45.65,
"rsi":  76.55,
"ret": 0.0037379 
},
{
 "date":  -4635,
"name": "GSPC.Close",
"price":  45.72,
"rsi":  78.77,
"ret": 0.0015334 
},
{
 "date":  -4634,
"name": "GSPC.Close",
"price":  45.56,
"rsi": 79.626,
"ret": -0.0034996 
},
{
 "date":  -4633,
"name": "GSPC.Close",
"price":   45.5,
"rsi":  72.44,
"ret": -0.0013169 
},
{
 "date":  -4630,
"name": "GSPC.Close",
"price":  45.73,
"rsi": 69.893,
"ret": 0.0050549 
},
{
 "date":  -4629,
"name": "GSPC.Close",
"price":  45.74,
"rsi": 73.709,
"ret": 0.00021867 
},
{
 "date":  -4628,
"name": "GSPC.Close",
"price":  46.02,
"rsi": 73.864,
"ret": 0.0061216 
},
{
 "date":  -4627,
"name": "GSPC.Close",
"price":  46.39,
"rsi": 77.812,
"ret": 0.00804 
},
{
 "date":  -4626,
"name": "GSPC.Close",
"price":  46.34,
"rsi": 81.737,
"ret": -0.0010778 
},
{
 "date":  -4623,
"name": "GSPC.Close",
"price":  46.27,
"rsi": 79.686,
"ret": -0.0015106 
},
{
 "date":  -4622,
"name": "GSPC.Close",
"price":  46.13,
"rsi":  76.78,
"ret": -0.0030257 
},
{
 "date":  -4621,
"name": "GSPC.Close",
"price":  46.31,
"rsi": 71.189,
"ret": 0.003902 
},
{
 "date":  -4620,
"name": "GSPC.Close",
"price":  46.36,
"rsi": 73.828,
"ret": 0.0010797 
},
{
 "date":  -4619,
"name": "GSPC.Close",
"price":  46.59,
"rsi": 74.526,
"ret": 0.0049612 
},
{
 "date":  -4616,
"name": "GSPC.Close",
"price":  46.88,
"rsi": 77.499,
"ret": 0.0062245 
},
{
 "date":  -4615,
"name": "GSPC.Close",
"price":  46.67,
"rsi": 80.576,
"ret": -0.0044795 
},
{
 "date":  -4614,
"name": "GSPC.Close",
"price":  46.83,
"rsi":  72.81,
"ret": 0.0034283 
},
{
 "date":  -4613,
"name": "GSPC.Close",
"price":  47.02,
"rsi": 74.803,
"ret": 0.0040572 
},
{
 "date":  -4612,
"name": "GSPC.Close",
"price":  47.15,
"rsi": 76.962,
"ret": 0.0027648 
},
{
 "date":  -4609,
"name": "GSPC.Close",
"price":  47.35,
"rsi":  78.33,
"ret": 0.0042418 
},
{
 "date":  -4608,
"name": "GSPC.Close",
"price":  47.33,
"rsi": 80.272,
"ret": -0.00042239 
},
{
 "date":  -4607,
"name": "GSPC.Close",
"price":  47.14,
"rsi": 79.505,
"ret": -0.0040144 
},
{
 "date":  -4606,
"name": "GSPC.Close",
"price":  47.15,
"rsi": 72.424,
"ret": 0.00021213 
},
{
 "date":  -4605,
"name": "GSPC.Close",
"price":  47.21,
"rsi": 72.563,
"ret": 0.0012725 
},
{
 "date":  -4602,
"name": "GSPC.Close",
"price":  46.78,
"rsi": 73.425,
"ret": -0.0091082 
},
{
 "date":  -4601,
"name": "GSPC.Close",
"price":  46.69,
"rsi":  59.09,
"ret": -0.0019239 
},
{
 "date":  -4600,
"name": "GSPC.Close",
"price":  47.11,
"rsi":   56.6,
"ret": 0.0089955 
},
{
 "date":  -4598,
"name": "GSPC.Close",
"price":  47.43,
"rsi": 64.186,
"ret": 0.0067926 
},
{
 "date":  -4595,
"name": "GSPC.Close",
"price":  47.37,
"rsi": 68.679,
"ret": -0.001265 
},
{
 "date":  -4594,
"name": "GSPC.Close",
"price":  47.28,
"rsi": 66.982,
"ret": -0.0018999 
},
{
 "date":  -4593,
"name": "GSPC.Close",
"price":  47.27,
"rsi": 64.412,
"ret": -0.00021151 
},
{
 "date":  -4592,
"name": "GSPC.Close",
"price":   47.8,
"rsi": 64.117,
"ret": 0.011212 
},
{
 "date":  -4591,
"name": "GSPC.Close",
"price":  47.85,
"rsi": 71.542,
"ret": 0.001046 
},
{
 "date":  -4588,
"name": "GSPC.Close",
"price":   47.9,
"rsi": 72.127,
"ret": 0.0010449 
},
{
 "date":  -4587,
"name": "GSPC.Close",
"price":  47.94,
"rsi": 72.732,
"ret": 0.00083507 
},
{
 "date":  -4586,
"name": "GSPC.Close",
"price":  48.05,
"rsi": 73.232,
"ret": 0.0022945 
},
{
 "date":  -4585,
"name": "GSPC.Close",
"price":  48.14,
"rsi": 74.612,
"ret": 0.001873 
},
{
 "date":  -4584,
"name": "GSPC.Close",
"price":  48.15,
"rsi": 75.714,
"ret": 0.00020773 
},
{
 "date":  -4581,
"name": "GSPC.Close",
"price":  48.24,
"rsi":  75.84,
"ret": 0.0018692 
},
{
 "date":  -4580,
"name": "GSPC.Close",
"price":  48.04,
"rsi": 76.993,
"ret": -0.0041459 
},
{
 "date":  -4579,
"name": "GSPC.Close",
"price":  47.72,
"rsi": 69.101,
"ret": -0.0066611 
},
{
 "date":  -4578,
"name": "GSPC.Close",
"price":  47.43,
"rsi":  58.73,
"ret": -0.0060771 
},
{
 "date":  -4577,
"name": "GSPC.Close",
"price":  47.15,
"rsi": 51.226,
"ret": -0.0059034 
},
{
 "date":  -4574,
"name": "GSPC.Close",
"price":  46.78,
"rsi": 45.218,
"ret": -0.0078473 
},
{
 "date":  -4573,
"name": "GSPC.Close",
"price":  47.15,
"rsi": 38.751,
"ret": 0.0079094 
},
{
 "date":  -4572,
"name": "GSPC.Close",
"price":  47.09,
"rsi": 46.926,
"ret": -0.0012725 
},
{
 "date":  -4571,
"name": "GSPC.Close",
"price":  47.26,
"rsi": 45.857,
"ret": 0.0036101 
},
{
 "date":  -4570,
"name": "GSPC.Close",
"price":  47.37,
"rsi": 49.375,
"ret": 0.0023275 
},
{
 "date":  -4567,
"name": "GSPC.Close",
"price":  47.43,
"rsi": 51.568,
"ret": 0.0012666 
},
{
 "date":  -4566,
"name": "GSPC.Close",
"price":   47.9,
"rsi":  52.77,
"ret": 0.0099093 
},
{
 "date":  -4565,
"name": "GSPC.Close",
"price":  48.46,
"rsi": 60.946,
"ret": 0.011691 
},
{
 "date":  -4563,
"name": "GSPC.Close",
"price":  48.69,
"rsi": 68.044,
"ret": 0.0047462 
},
{
 "date":  -4560,
"name": "GSPC.Close",
"price":   48.9,
"rsi": 70.422,
"ret": 0.004313 
},
{
 "date":  -4559,
"name": "GSPC.Close",
"price":   48.9,
"rsi": 72.438,
"ret":      0 
},
{
 "date":  -4558,
"name": "GSPC.Close",
"price":     49,
"rsi": 72.438,
"ret": 0.002045 
},
{
 "date":  -4557,
"name": "GSPC.Close",
"price":  48.86,
"rsi": 73.438,
"ret": -0.0028571 
},
{
 "date":  -4556,
"name": "GSPC.Close",
"price":  49.08,
"rsi": 69.629,
"ret": 0.0045027 
},
{
 "date":  -4553,
"name": "GSPC.Close",
"price":  49.13,
"rsi":  72.08,
"ret": 0.0010187 
},
{
 "date":  -4552,
"name": "GSPC.Close",
"price":  48.88,
"rsi": 72.621,
"ret": -0.0050885 
},
{
 "date":  -4551,
"name": "GSPC.Close",
"price":  48.58,
"rsi": 65.762,
"ret": -0.0061375 
},
{
 "date":  -4550,
"name": "GSPC.Close",
"price":  48.53,
"rsi": 58.609,
"ret": -0.0010292 
},
{
 "date":  -4549,
"name": "GSPC.Close",
"price":  48.58,
"rsi": 57.487,
"ret": 0.0010303 
},
{
 "date":  -4546,
"name": "GSPC.Close",
"price":  48.47,
"rsi": 58.346,
"ret": -0.0022643 
},
{
 "date":  -4545,
"name": "GSPC.Close",
"price":  48.56,
"rsi": 55.681,
"ret": 0.0018568 
},
{
 "date":  -4544,
"name": "GSPC.Close",
"price":  48.61,
"rsi": 57.396,
"ret": 0.0010297 
},
{
 "date":  -4543,
"name": "GSPC.Close",
"price":  48.61,
"rsi":  58.36,
"ret":      0 
},
{
 "date":  -4542,
"name": "GSPC.Close",
"price":  48.45,
"rsi":  58.36,
"ret": -0.0032915 
},
{
 "date":  -4539,
"name": "GSPC.Close",
"price":  47.92,
"rsi": 53.838,
"ret": -0.010939 
},
{
 "date":  -4538,
"name": "GSPC.Close",
"price":  47.92,
"rsi": 42.181,
"ret":      0 
},
{
 "date":  -4537,
"name": "GSPC.Close",
"price":  47.91,
"rsi": 42.181,
"ret": -0.00020868 
},
{
 "date":  -4536,
"name": "GSPC.Close",
"price":  47.79,
"rsi": 41.982,
"ret": -0.0025047 
},
{
 "date":  -4535,
"name": "GSPC.Close",
"price":  47.68,
"rsi": 39.571,
"ret": -0.0023017 
},
{
 "date":  -4532,
"name": "GSPC.Close",
"price":  47.26,
"rsi": 37.447,
"ret": -0.0088087 
},
{
 "date":  -4531,
"name": "GSPC.Close",
"price":  46.67,
"rsi": 30.678,
"ret": -0.012484 
},
{
 "date":  -4530,
"name": "GSPC.Close",
"price":  47.03,
"rsi":  24.09,
"ret": 0.0077137 
},
{
 "date":  -4529,
"name": "GSPC.Close",
"price":   46.9,
"rsi": 33.477,
"ret": -0.0027642 
},
{
 "date":  -4528,
"name": "GSPC.Close",
"price":  46.92,
"rsi": 31.941,
"ret": 0.00042644 
},
{
 "date":  -4525,
"name": "GSPC.Close",
"price":  46.33,
"rsi": 32.455,
"ret": -0.012575 
},
{
 "date":  -4524,
"name": "GSPC.Close",
"price":   46.3,
"rsi":  26.18,
"ret": -0.00064753 
},
{
 "date":  -4523,
"name": "GSPC.Close",
"price":  45.73,
"rsi": 25.906,
"ret": -0.012311 
},
{
 "date":  -4522,
"name": "GSPC.Close",
"price":  45.75,
"rsi": 21.333,
"ret": 0.00043735 
},
{
 "date":  -4521,
"name": "GSPC.Close",
"price":  45.83,
"rsi": 21.854,
"ret": 0.0017486 
},
{
 "date":  -4518,
"name": "GSPC.Close",
"price":  44.91,
"rsi": 24.023,
"ret": -0.020074 
},
{
 "date":  -4517,
"name": "GSPC.Close",
"price":  45.29,
"rsi": 17.878,
"ret": 0.0084614 
},
{
 "date":  -4516,
"name": "GSPC.Close",
"price":  45.49,
"rsi": 26.267,
"ret": 0.004416 
},
{
 "date":  -4515,
"name": "GSPC.Close",
"price":  45.16,
"rsi": 30.302,
"ret": -0.0072543 
},
{
 "date":  -4514,
"name": "GSPC.Close",
"price":  44.51,
"rsi": 27.617,
"ret": -0.014393 
},
{
 "date":  -4511,
"name": "GSPC.Close",
"price":  43.89,
"rsi": 23.246,
"ret": -0.013929 
},
{
 "date":  -4510,
"name": "GSPC.Close",
"price":  44.61,
"rsi": 19.996,
"ret": 0.016405 
},
{
 "date":  -4509,
"name": "GSPC.Close",
"price":  44.64,
"rsi": 31.904,
"ret": 0.00067249 
},
{
 "date":  -4508,
"name": "GSPC.Close",
"price":  44.46,
"rsi": 32.356,
"ret": -0.0040323 
},
{
 "date":  -4507,
"name": "GSPC.Close",
"price":  45.22,
"rsi": 31.026,
"ret": 0.017094 
},
{
 "date":  -4503,
"name": "GSPC.Close",
"price":  45.44,
"rsi": 41.888,
"ret": 0.0048651 
},
{
 "date":  -4502,
"name": "GSPC.Close",
"price":  45.05,
"rsi": 44.607,
"ret": -0.0085827 
},
{
 "date":  -4501,
"name": "GSPC.Close",
"price":  44.82,
"rsi": 40.949,
"ret": -0.0051054 
},
{
 "date":  -4500,
"name": "GSPC.Close",
"price":  44.68,
"rsi": 38.922,
"ret": -0.0031236 
},
{
 "date":  -4497,
"name": "GSPC.Close",
"price":  44.28,
"rsi": 37.698,
"ret": -0.0089526 
},
{
 "date":  -4496,
"name": "GSPC.Close",
"price":  43.87,
"rsi": 34.374,
"ret": -0.0092593 
},
{
 "date":  -4495,
"name": "GSPC.Close",
"price":  44.26,
"rsi": 31.324,
"ret": 0.0088899 
},
{
 "date":  -4494,
"name": "GSPC.Close",
"price":  44.82,
"rsi": 37.045,
"ret": 0.012653 
},
{
 "date":  -4493,
"name": "GSPC.Close",
"price":   44.8,
"rsi":  44.23,
"ret": -0.00044623 
},
{
 "date":  -4490,
"name": "GSPC.Close",
"price":  44.58,
"rsi": 44.036,
"ret": -0.0049107 
},
{
 "date":  -4489,
"name": "GSPC.Close",
"price":  44.64,
"rsi": 41.869,
"ret": 0.0013459 
},
{
 "date":  -4488,
"name": "GSPC.Close",
"price":  44.69,
"rsi": 42.697,
"ret": 0.0011201 
},
{
 "date":  -4487,
"name": "GSPC.Close",
"price":   44.4,
"rsi": 43.421,
"ret": -0.0064891 
},
{
 "date":  -4486,
"name": "GSPC.Close",
"price":  43.69,
"rsi": 40.247,
"ret": -0.015991 
},
{
 "date":  -4483,
"name": "GSPC.Close",
"price":  42.69,
"rsi": 33.743,
"ret": -0.022889 
},
{
 "date":  -4482,
"name": "GSPC.Close",
"price":  42.98,
"rsi":   27.1,
"ret": 0.0067932 
},
{
 "date":  -4481,
"name": "GSPC.Close",
"price":  42.98,
"rsi": 31.323,
"ret":      0 
},
{
 "date":  -4480,
"name": "GSPC.Close",
"price":  42.57,
"rsi": 31.323,
"ret": -0.0095393 
},
{
 "date":  -4479,
"name": "GSPC.Close",
"price":  42.55,
"rsi": 28.606,
"ret": -0.00046981 
},
{
 "date":  -4476,
"name": "GSPC.Close",
"price":  42.42,
"rsi": 28.476,
"ret": -0.0030552 
},
{
 "date":  -4475,
"name": "GSPC.Close",
"price":  42.76,
"rsi":   27.6,
"ret": 0.0080151 
},
{
 "date":  -4474,
"name": "GSPC.Close",
"price":   43.1,
"rsi": 33.374,
"ret": 0.0079514 
},
{
 "date":  -4473,
"name": "GSPC.Close",
"price":  43.14,
"rsi": 38.645,
"ret": 0.00092807 
},
{
 "date":  -4472,
"name": "GSPC.Close",
"price":  42.79,
"rsi": 39.253,
"ret": -0.0081131 
},
{
 "date":  -4469,
"name": "GSPC.Close",
"price":  42.22,
"rsi": 35.897,
"ret": -0.013321 
},
{
 "date":  -4468,
"name": "GSPC.Close",
"price":  41.95,
"rsi": 31.216,
"ret": -0.0063951 
},
{
 "date":  -4467,
"name": "GSPC.Close",
"price":  41.99,
"rsi": 29.269,
"ret": 0.00095352 
},
{
 "date":  -4466,
"name": "GSPC.Close",
"price":  40.96,
"rsi": 29.966,
"ret": -0.02453 
},
{
 "date":  -4465,
"name": "GSPC.Close",
"price":  40.94,
"rsi": 23.535,
"ret": -0.00048828 
},
{
 "date":  -4462,
"name": "GSPC.Close",
"price":  41.24,
"rsi":  23.43,
"ret": 0.0073278 
},
{
 "date":  -4461,
"name": "GSPC.Close",
"price":  41.67,
"rsi": 28.584,
"ret": 0.010427 
},
{
 "date":  -4460,
"name": "GSPC.Close",
"price":  41.33,
"rsi": 35.306,
"ret": -0.0081593 
},
{
 "date":  -4459,
"name": "GSPC.Close",
"price":  40.65,
"rsi": 32.686,
"ret": -0.016453 
},
{
 "date":  -4458,
"name": "GSPC.Close",
"price":  40.33,
"rsi": 28.182,
"ret": -0.0078721 
},
{
 "date":  -4455,
"name": "GSPC.Close",
"price":  39.15,
"rsi": 26.343,
"ret": -0.029259 
},
{
 "date":  -4454,
"name": "GSPC.Close",
"price":  38.98,
"rsi":  20.92,
"ret": -0.0043423 
},
{
 "date":  -4453,
"name": "GSPC.Close",
"price":  40.73,
"rsi": 20.272,
"ret": 0.044895 
},
{
 "date":  -4452,
"name": "GSPC.Close",
"price":  40.71,
"rsi": 40.639,
"ret": -0.00049104 
},
{
 "date":  -4451,
"name": "GSPC.Close",
"price":  40.59,
"rsi": 40.512,
"ret": -0.0029477 
},
{
 "date":  -4448,
"name": "GSPC.Close",
"price":  40.42,
"rsi": 39.708,
"ret": -0.0041882 
},
{
 "date":  -4447,
"name": "GSPC.Close",
"price":  40.69,
"rsi": 38.541,
"ret": 0.0066799 
},
{
 "date":  -4446,
"name": "GSPC.Close",
"price":  41.02,
"rsi": 41.483,
"ret": 0.0081101 
},
{
 "date":  -4445,
"name": "GSPC.Close",
"price":  41.06,
"rsi": 44.951,
"ret": 0.00097513 
},
{
 "date":  -4444,
"name": "GSPC.Close",
"price":  40.44,
"rsi": 45.374,
"ret": -0.0151 
},
{
 "date":  -4441,
"name": "GSPC.Close",
"price":  40.37,
"rsi": 40.219,
"ret": -0.001731 
},
{
 "date":  -4439,
"name": "GSPC.Close",
"price":  40.43,
"rsi": 39.671,
"ret": 0.0014863 
},
{
 "date":  -4438,
"name": "GSPC.Close",
"price":  40.67,
"rsi": 40.421,
"ret": 0.0059362 
},
{
 "date":  -4437,
"name": "GSPC.Close",
"price":  40.19,
"rsi": 43.446,
"ret": -0.011802 
},
{
 "date":  -4434,
"name": "GSPC.Close",
"price":  40.18,
"rsi": 39.163,
"ret": -0.00024882 
},
{
 "date":  -4433,
"name": "GSPC.Close",
"price":   39.6,
"rsi": 39.076,
"ret": -0.014435 
},
{
 "date":  -4432,
"name": "GSPC.Close",
"price":  39.55,
"rsi": 34.342,
"ret": -0.0012626 
},
{
 "date":  -4431,
"name": "GSPC.Close",
"price":  39.44,
"rsi":  33.96,
"ret": -0.0027813 
},
{
 "date":  -4430,
"name": "GSPC.Close",
"price":  40.37,
"rsi": 33.088,
"ret": 0.02358 
},
{
 "date":  -4427,
"name": "GSPC.Close",
"price":  40.04,
"rsi": 45.767,
"ret": -0.0081744 
},
{
 "date":  -4426,
"name": "GSPC.Close",
"price":  39.81,
"rsi": 42.676,
"ret": -0.0057443 
},
{
 "date":  -4425,
"name": "GSPC.Close",
"price":  39.92,
"rsi": 40.618,
"ret": 0.0027631 
},
{
 "date":  -4424,
"name": "GSPC.Close",
"price":  40.48,
"rsi": 42.057,
"ret": 0.014028 
},
{
 "date":  -4423,
"name": "GSPC.Close",
"price":  40.87,
"rsi": 48.855,
"ret": 0.0096344 
},
{
 "date":  -4420,
"name": "GSPC.Close",
"price":  41.18,
"rsi": 52.991,
"ret": 0.007585 
},
{
 "date":  -4419,
"name": "GSPC.Close",
"price":  40.09,
"rsi": 56.034,
"ret": -0.026469 
},
{
 "date":  -4418,
"name": "GSPC.Close",
"price":  41.25,
"rsi": 45.002,
"ret": 0.028935 
},
{
 "date":  -4416,
"name": "GSPC.Close",
"price":  41.72,
"rsi": 55.127,
"ret": 0.011394 
},
{
 "date":  -4413,
"name": "GSPC.Close",
"price":  41.36,
"rsi": 58.464,
"ret": -0.008629 
},
{
 "date":  -4412,
"name": "GSPC.Close",
"price":  41.37,
"rsi": 55.085,
"ret": 0.00024178 
},
{
 "date":  -4411,
"name": "GSPC.Close",
"price":  41.54,
"rsi": 55.163,
"ret": 0.0041093 
},
{
 "date":  -4410,
"name": "GSPC.Close",
"price":  41.52,
"rsi": 56.536,
"ret": -0.00048146 
},
{
 "date":  -4409,
"name": "GSPC.Close",
"price":  41.31,
"rsi": 56.318,
"ret": -0.0050578 
},
{
 "date":  -4406,
"name": "GSPC.Close",
"price":  40.92,
"rsi": 53.959,
"ret": -0.0094408 
},
{
 "date":  -4405,
"name": "GSPC.Close",
"price":  40.56,
"rsi": 49.789,
"ret": -0.0087977 
},
{
 "date":  -4404,
"name": "GSPC.Close",
"price":  40.51,
"rsi": 46.236,
"ret": -0.0012327 
},
{
 "date":  -4403,
"name": "GSPC.Close",
"price":  40.55,
"rsi": 45.748,
"ret": 0.00098741 
},
{
 "date":  -4402,
"name": "GSPC.Close",
"price":  40.73,
"rsi": 46.237,
"ret": 0.004439 
},
{
 "date":  -4399,
"name": "GSPC.Close",
"price":  40.12,
"rsi": 48.488,
"ret": -0.014977 
},
{
 "date":  -4398,
"name": "GSPC.Close",
"price":  39.42,
"rsi": 42.062,
"ret": -0.017448 
},
{
 "date":  -4397,
"name": "GSPC.Close",
"price":  39.38,
"rsi": 36.143,
"ret": -0.0010147 
},
{
 "date":  -4396,
"name": "GSPC.Close",
"price":   39.8,
"rsi": 35.833,
"ret": 0.010665 
},
{
 "date":  -4395,
"name": "GSPC.Close",
"price":  39.48,
"rsi": 41.511,
"ret": -0.0080402 
},
{
 "date":  -4392,
"name": "GSPC.Close",
"price":  39.48,
"rsi": 38.701,
"ret":      0 
},
{
 "date":  -4391,
"name": "GSPC.Close",
"price":  39.52,
"rsi": 38.701,
"ret": 0.0010132 
},
{
 "date":  -4389,
"name": "GSPC.Close",
"price":  39.92,
"rsi": 39.297,
"ret": 0.010121 
},
{
 "date":  -4388,
"name": "GSPC.Close",
"price":  39.78,
"rsi": 45.048,
"ret": -0.003507 
},
{
 "date":  -4385,
"name": "GSPC.Close",
"price":  39.58,
"rsi": 43.495,
"ret": -0.0050277 
},
{
 "date":  -4384,
"name": "GSPC.Close",
"price":  39.99,
"rsi": 41.304,
"ret": 0.010359 
},
{
 "date":  -4382,
"name": "GSPC.Close",
"price":  40.33,
"rsi": 47.178,
"ret": 0.0085021 
},
{
 "date":  -4381,
"name": "GSPC.Close",
"price":  40.87,
"rsi": 51.512,
"ret": 0.01339 
},
{
 "date":  -4378,
"name": "GSPC.Close",
"price":  40.68,
"rsi": 57.479,
"ret": -0.0046489 
},
{
 "date":  -4377,
"name": "GSPC.Close",
"price":     41,
"rsi": 54.918,
"ret": 0.0078663 
},
{
 "date":  -4376,
"name": "GSPC.Close",
"price":  40.99,
"rsi": 58.288,
"ret": -0.0002439 
},
{
 "date":  -4375,
"name": "GSPC.Close",
"price":  40.75,
"rsi": 58.142,
"ret": -0.0058551 
},
{
 "date":  -4374,
"name": "GSPC.Close",
"price":  40.37,
"rsi":   54.6,
"ret": -0.0093252 
},
{
 "date":  -4371,
"name": "GSPC.Close",
"price":  40.49,
"rsi": 49.462,
"ret": 0.0029725 
},
{
 "date":  -4370,
"name": "GSPC.Close",
"price":  40.67,
"rsi":  51.03,
"ret": 0.0044455 
},
{
 "date":  -4369,
"name": "GSPC.Close",
"price":  40.99,
"rsi": 53.366,
"ret": 0.0078682 
},
{
 "date":  -4368,
"name": "GSPC.Close",
"price":  41.06,
"rsi": 57.268,
"ret": 0.0017077 
},
{
 "date":  -4367,
"name": "GSPC.Close",
"price":   41.1,
"rsi": 58.094,
"ret": 0.00097418 
},
{
 "date":  -4364,
"name": "GSPC.Close",
"price":  41.35,
"rsi": 58.587,
"ret": 0.0060827 
},
{
 "date":  -4363,
"name": "GSPC.Close",
"price":   41.3,
"rsi": 61.624,
"ret": -0.0012092 
},
{
 "date":  -4362,
"name": "GSPC.Close",
"price":   41.2,
"rsi": 60.666,
"ret": -0.0024213 
},
{
 "date":  -4361,
"name": "GSPC.Close",
"price":  41.36,
"rsi":   58.7,
"ret": 0.0038835 
},
{
 "date":  -4360,
"name": "GSPC.Close",
"price":  41.71,
"rsi": 60.884,
"ret": 0.0084623 
},
{
 "date":  -4357,
"name": "GSPC.Close",
"price":  41.59,
"rsi": 65.217,
"ret": -0.002877 
},
{
 "date":  -4356,
"name": "GSPC.Close",
"price":  41.63,
"rsi": 62.654,
"ret": 0.00096177 
},
{
 "date":  -4355,
"name": "GSPC.Close",
"price":  41.88,
"rsi": 63.174,
"ret": 0.0060053 
},
{
 "date":  -4354,
"name": "GSPC.Close",
"price":  41.68,
"rsi": 66.327,
"ret": -0.0047755 
},
{
 "date":  -4353,
"name": "GSPC.Close",
"price":   41.7,
"rsi": 61.771,
"ret": 0.00047985 
},
{
 "date":  -4350,
"name": "GSPC.Close",
"price":  42.04,
"rsi": 62.051,
"ret": 0.0081535 
},
{
 "date":  -4349,
"name": "GSPC.Close",
"price":  42.46,
"rsi": 66.548,
"ret": 0.0099905 
},
{
 "date":  -4348,
"name": "GSPC.Close",
"price":  42.19,
"rsi": 71.104,
"ret": -0.0063589 
},
{
 "date":  -4347,
"name": "GSPC.Close",
"price":   42.1,
"rsi": 64.978,
"ret": -0.0021332 
},
{
 "date":  -4346,
"name": "GSPC.Close",
"price":  41.73,
"rsi": 63.028,
"ret": -0.0087886 
},
{
 "date":  -4343,
"name": "GSPC.Close",
"price":  41.48,
"rsi": 55.639,
"ret": -0.0059909 
},
{
 "date":  -4342,
"name": "GSPC.Close",
"price":  41.11,
"rsi": 51.265,
"ret": -0.00892 
},
{
 "date":  -4341,
"name": "GSPC.Close",
"price":  40.93,
"rsi": 45.557,
"ret": -0.0043785 
},
{
 "date":  -4340,
"name": "GSPC.Close",
"price":  40.94,
"rsi": 43.046,
"ret": 0.00024432 
},
{
 "date":  -4339,
"name": "GSPC.Close",
"price":  41.33,
"rsi": 43.233,
"ret": 0.0095261 
},
{
 "date":  -4336,
"name": "GSPC.Close",
"price":  41.11,
"rsi": 50.119,
"ret": -0.005323 
},
{
 "date":  -4335,
"name": "GSPC.Close",
"price":  41.17,
"rsi": 46.679,
"ret": 0.0014595 
},
{
 "date":  -4334,
"name": "GSPC.Close",
"price":  41.15,
"rsi": 47.733,
"ret": -0.00048579 
},
{
 "date":  -4333,
"name": "GSPC.Close",
"price":  40.91,
"rsi": 47.397,
"ret": -0.0058323 
},
{
 "date":  -4332,
"name": "GSPC.Close",
"price":  40.88,
"rsi": 43.443,
"ret": -0.00073332 
},
{
 "date":  -4329,
"name": "GSPC.Close",
"price":  40.65,
"rsi":  42.96,
"ret": -0.0056262 
},
{
 "date":  -4328,
"name": "GSPC.Close",
"price":  40.61,
"rsi": 39.352,
"ret": -0.00098401 
},
{
 "date":  -4327,
"name": "GSPC.Close",
"price":  40.92,
"rsi": 38.743,
"ret": 0.0076336 
},
{
 "date":  -4326,
"name": "GSPC.Close",
"price":  40.68,
"rsi": 45.754,
"ret": -0.0058651 
},
{
 "date":  -4325,
"name": "GSPC.Close",
"price":  40.84,
"rsi": 41.768,
"ret": 0.0039331 
},
{
 "date":  -4322,
"name": "GSPC.Close",
"price":  41.13,
"rsi": 45.196,
"ret": 0.0071009 
},
{
 "date":  -4321,
"name": "GSPC.Close",
"price":  41.35,
"rsi": 50.844,
"ret": 0.0053489 
},
{
 "date":  -4320,
"name": "GSPC.Close",
"price":  41.47,
"rsi": 54.661,
"ret": 0.0029021 
},
{
 "date":  -4319,
"name": "GSPC.Close",
"price":     42,
"rsi": 56.639,
"ret": 0.01278 
},
{
 "date":  -4318,
"name": "GSPC.Close",
"price":  42.07,
"rsi": 64.091,
"ret": 0.0016667 
},
{
 "date":  -4315,
"name": "GSPC.Close",
"price":  42.21,
"rsi": 64.948,
"ret": 0.0033278 
},
{
 "date":  -4314,
"name": "GSPC.Close",
"price":  42.51,
"rsi": 66.661,
"ret": 0.0071073 
},
{
 "date":  -4313,
"name": "GSPC.Close",
"price":  42.41,
"rsi":  70.04,
"ret": -0.0023524 
},
{
 "date":  -4312,
"name": "GSPC.Close",
"price":  42.46,
"rsi": 67.581,
"ret": 0.001179 
},
{
 "date":  -4311,
"name": "GSPC.Close",
"price":  42.33,
"rsi": 68.183,
"ret": -0.0030617 
},
{
 "date":  -4308,
"name": "GSPC.Close",
"price":  42.04,
"rsi": 64.815,
"ret": -0.0068509 
},
{
 "date":  -4307,
"name": "GSPC.Close",
"price":  41.89,
"rsi": 57.941,
"ret": -0.003568 
},
{
 "date":  -4306,
"name": "GSPC.Close",
"price":  42.09,
"rsi": 54.709,
"ret": 0.0047744 
},
{
 "date":  -4305,
"name": "GSPC.Close",
"price":  42.11,
"rsi": 58.068,
"ret": 0.00047517 
},
{
 "date":  -4304,
"name": "GSPC.Close",
"price":  42.42,
"rsi":   58.4,
"ret": 0.0073617 
},
{
 "date":  -4301,
"name": "GSPC.Close",
"price":  42.58,
"rsi": 63.259,
"ret": 0.0037718 
},
{
 "date":  -4300,
"name": "GSPC.Close",
"price":  42.44,
"rsi": 65.499,
"ret": -0.0032879 
},
{
 "date":  -4299,
"name": "GSPC.Close",
"price":   42.3,
"rsi": 61.941,
"ret": -0.0032988 
},
{
 "date":  -4298,
"name": "GSPC.Close",
"price":  42.17,
"rsi": 58.517,
"ret": -0.0030733 
},
{
 "date":  -4297,
"name": "GSPC.Close",
"price":   42.2,
"rsi": 55.452,
"ret": 0.00071141 
},
{
 "date":  -4294,
"name": "GSPC.Close",
"price":   42.1,
"rsi": 56.024,
"ret": -0.0023697 
},
{
 "date":  -4293,
"name": "GSPC.Close",
"price":  41.93,
"rsi": 53.554,
"ret": -0.004038 
},
{
 "date":  -4292,
"name": "GSPC.Close",
"price":   41.6,
"rsi": 49.554,
"ret": -0.0078703 
},
{
 "date":  -4291,
"name": "GSPC.Close",
"price":  41.48,
"rsi": 42.861,
"ret": -0.0028846 
},
{
 "date":  -4287,
"name": "GSPC.Close",
"price":  41.33,
"rsi": 40.708,
"ret": -0.0036162 
},
{
 "date":  -4286,
"name": "GSPC.Close",
"price":  41.43,
"rsi":  38.13,
"ret": 0.0024195 
},
{
 "date":  -4285,
"name": "GSPC.Close",
"price":  41.65,
"rsi": 40.821,
"ret": 0.0053102 
},
{
 "date":  -4284,
"name": "GSPC.Close",
"price":   41.7,
"rsi":  46.35,
"ret": 0.0012005 
},
{
 "date":  -4283,
"name": "GSPC.Close",
"price":  41.74,
"rsi": 47.549,
"ret": 0.00095923 
},
{
 "date":  -4280,
"name": "GSPC.Close",
"price":     42,
"rsi":  48.54,
"ret": 0.006229 
},
{
 "date":  -4279,
"name": "GSPC.Close",
"price":  42.43,
"rsi": 54.552,
"ret": 0.010238 
},
{
 "date":  -4278,
"name": "GSPC.Close",
"price":   42.1,
"rsi": 62.379,
"ret": -0.0077775 
},
{
 "date":  -4277,
"name": "GSPC.Close",
"price":  42.25,
"rsi": 54.606,
"ret": 0.0035629 
},
{
 "date":  -4276,
"name": "GSPC.Close",
"price":  42.71,
"rsi": 57.216,
"ret": 0.010888 
},
{
 "date":  -4273,
"name": "GSPC.Close",
"price":  42.93,
"rsi": 64.043,
"ret": 0.005151 
},
{
 "date":  -4272,
"name": "GSPC.Close",
"price":   42.8,
"rsi": 66.774,
"ret": -0.0030282 
},
{
 "date":  -4271,
"name": "GSPC.Close",
"price":   42.8,
"rsi": 63.695,
"ret":      0 
},
{
 "date":  -4270,
"name": "GSPC.Close",
"price":  43.14,
"rsi": 63.695,
"ret": 0.0079439 
},
{
 "date":  -4269,
"name": "GSPC.Close",
"price":  43.36,
"rsi": 68.149,
"ret": 0.0050997 
},
{
 "date":  -4266,
"name": "GSPC.Close",
"price":  43.22,
"rsi": 70.657,
"ret": -0.0032288 
},
{
 "date":  -4265,
"name": "GSPC.Close",
"price":     43,
"rsi": 67.039,
"ret": -0.0050902 
},
{
 "date":  -4264,
"name": "GSPC.Close",
"price":  43.44,
"rsi": 61.693,
"ret": 0.010233 
},
{
 "date":  -4263,
"name": "GSPC.Close",
"price":  43.54,
"rsi": 67.308,
"ret": 0.002302 
},
{
 "date":  -4262,
"name": "GSPC.Close",
"price":  43.69,
"rsi": 68.441,
"ret": 0.0034451 
},
{
 "date":  -4259,
"name": "GSPC.Close",
"price":  43.79,
"rsi": 70.113,
"ret": 0.0022889 
},
{
 "date":  -4258,
"name": "GSPC.Close",
"price":  44.01,
"rsi": 71.208,
"ret": 0.005024 
},
{
 "date":  -4257,
"name": "GSPC.Close",
"price":  43.93,
"rsi": 73.508,
"ret": -0.0018178 
},
{
 "date":  -4256,
"name": "GSPC.Close",
"price":  43.99,
"rsi": 71.278,
"ret": 0.0013658 
},
{
 "date":  -4255,
"name": "GSPC.Close",
"price":  44.09,
"rsi": 71.965,
"ret": 0.0022732 
},
{
 "date":  -4252,
"name": "GSPC.Close",
"price":  43.75,
"rsi": 73.119,
"ret": -0.0077115 
},
{
 "date":  -4251,
"name": "GSPC.Close",
"price":  43.62,
"rsi": 63.543,
"ret": -0.0029714 
},
{
 "date":  -4250,
"name": "GSPC.Close",
"price":  43.12,
"rsi": 60.291,
"ret": -0.011463 
},
{
 "date":  -4249,
"name": "GSPC.Close",
"price":  43.34,
"rsi": 49.748,
"ret": 0.005102 
},
{
 "date":  -4248,
"name": "GSPC.Close",
"price":  43.36,
"rsi": 53.593,
"ret": 0.00046147 
},
{
 "date":  -4245,
"name": "GSPC.Close",
"price":  43.24,
"rsi": 53.938,
"ret": -0.0027675 
},
{
 "date":  -4244,
"name": "GSPC.Close",
"price":  43.61,
"rsi": 51.466,
"ret": 0.0085569 
},
{
 "date":  -4243,
"name": "GSPC.Close",
"price":  43.55,
"rsi": 57.878,
"ret": -0.0013758 
},
{
 "date":  -4242,
"name": "GSPC.Close",
"price":  43.78,
"rsi": 56.573,
"ret": 0.0052813 
},
{
 "date":  -4241,
"name": "GSPC.Close",
"price":  43.87,
"rsi": 60.271,
"ret": 0.0020557 
},
{
 "date":  -4238,
"name": "GSPC.Close",
"price":  43.85,
"rsi": 61.648,
"ret": -0.00045589 
},
{
 "date":  -4237,
"name": "GSPC.Close",
"price":  43.79,
"rsi": 61.141,
"ret": -0.0013683 
},
{
 "date":  -4236,
"name": "GSPC.Close",
"price":  43.85,
"rsi": 59.559,
"ret": 0.0013702 
},
{
 "date":  -4235,
"name": "GSPC.Close",
"price":  44.09,
"rsi": 60.655,
"ret": 0.0054732 
},
{
 "date":  -4231,
"name": "GSPC.Close",
"price":  44.31,
"rsi":  64.77,
"ret": 0.0049898 
},
{
 "date":  -4230,
"name": "GSPC.Close",
"price":  44.46,
"rsi": 68.067,
"ret": 0.0033852 
},
{
 "date":  -4229,
"name": "GSPC.Close",
"price":   44.5,
"rsi": 70.121,
"ret": 0.00089969 
},
{
 "date":  -4228,
"name": "GSPC.Close",
"price":  44.55,
"rsi": 70.662,
"ret": 0.0011236 
},
{
 "date":  -4227,
"name": "GSPC.Close",
"price":  44.64,
"rsi": 71.361,
"ret": 0.0020202 
},
{
 "date":  -4224,
"name": "GSPC.Close",
"price":  44.57,
"rsi": 72.626,
"ret": -0.0015681 
},
{
 "date":  -4223,
"name": "GSPC.Close",
"price":  44.48,
"rsi": 70.036,
"ret": -0.0020193 
},
{
 "date":  -4222,
"name": "GSPC.Close",
"price":  44.49,
"rsi": 66.741,
"ret": 0.00022482 
},
{
 "date":  -4221,
"name": "GSPC.Close",
"price":  44.75,
"rsi": 66.927,
"ret": 0.005844 
},
{
 "date":  -4220,
"name": "GSPC.Close",
"price":  45.02,
"rsi": 71.409,
"ret": 0.0060335 
},
{
 "date":  -4217,
"name": "GSPC.Close",
"price":  45.18,
"rsi": 75.171,
"ret": 0.003554 
},
{
 "date":  -4216,
"name": "GSPC.Close",
"price":  44.94,
"rsi": 77.095,
"ret": -0.0053121 
},
{
 "date":  -4215,
"name": "GSPC.Close",
"price":  45.34,
"rsi": 68.519,
"ret": 0.0089008 
},
{
 "date":  -4214,
"name": "GSPC.Close",
"price":  44.61,
"rsi": 73.759,
"ret": -0.016101 
},
{
 "date":  -4213,
"name": "GSPC.Close",
"price":  44.85,
"rsi": 55.579,
"ret": 0.00538 
},
{
 "date":  -4210,
"name": "GSPC.Close",
"price":  44.69,
"rsi": 59.144,
"ret": -0.0035674 
},
{
 "date":  -4209,
"name": "GSPC.Close",
"price":  44.52,
"rsi": 55.922,
"ret": -0.003804 
},
{
 "date":  -4208,
"name": "GSPC.Close",
"price":  44.63,
"rsi":  52.64,
"ret": 0.0024708 
},
{
 "date":  -4207,
"name": "GSPC.Close",
"price":  44.84,
"rsi": 54.501,
"ret": 0.0047054 
},
{
 "date":  -4206,
"name": "GSPC.Close",
"price":   44.9,
"rsi": 57.901,
"ret": 0.0013381 
},
{
 "date":  -4203,
"name": "GSPC.Close",
"price":  45.24,
"rsi": 58.847,
"ret": 0.0075724 
},
{
 "date":  -4202,
"name": "GSPC.Close",
"price":  45.28,
"rsi": 63.812,
"ret": 0.00088417 
},
{
 "date":  -4201,
"name": "GSPC.Close",
"price":  45.32,
"rsi": 64.356,
"ret": 0.00088339 
},
{
 "date":  -4200,
"name": "GSPC.Close",
"price":  45.47,
"rsi": 64.925,
"ret": 0.0033098 
},
{
 "date":  -4196,
"name": "GSPC.Close",
"price":  45.62,
"rsi": 67.048,
"ret": 0.0032989 
},
{
 "date":  -4195,
"name": "GSPC.Close",
"price":   45.4,
"rsi": 69.064,
"ret": -0.0048224 
},
{
 "date":  -4194,
"name": "GSPC.Close",
"price":  45.25,
"rsi": 62.977,
"ret": -0.003304 
},
{
 "date":  -4193,
"name": "GSPC.Close",
"price":  45.42,
"rsi":  59.15,
"ret": 0.0037569 
},
{
 "date":  -4192,
"name": "GSPC.Close",
"price":  45.72,
"rsi": 61.971,
"ret": 0.006605 
},
{
 "date":  -4189,
"name": "GSPC.Close",
"price":  45.14,
"rsi": 66.383,
"ret": -0.012686 
},
{
 "date":  -4188,
"name": "GSPC.Close",
"price":  45.11,
"rsi": 53.467,
"ret": -0.0006646 
},
{
 "date":  -4187,
"name": "GSPC.Close",
"price":  45.25,
"rsi": 52.894,
"ret": 0.0031035 
},
{
 "date":  -4186,
"name": "GSPC.Close",
"price":  45.55,
"rsi": 55.303,
"ret": 0.0066298 
},
{
 "date":  -4185,
"name": "GSPC.Close",
"price":  45.77,
"rsi":  60.02,
"ret": 0.0048299 
},
{
 "date":  -4182,
"name": "GSPC.Close",
"price":  46.33,
"rsi": 63.095,
"ret": 0.012235 
},
{
 "date":  -4181,
"name": "GSPC.Close",
"price":  46.41,
"rsi": 69.523,
"ret": 0.0017267 
},
{
 "date":  -4180,
"name": "GSPC.Close",
"price":   46.4,
"rsi": 70.318,
"ret": -0.00021547 
},
{
 "date":  -4179,
"name": "GSPC.Close",
"price":  46.65,
"rsi": 70.072,
"ret": 0.0053879 
},
{
 "date":  -4178,
"name": "GSPC.Close",
"price":  46.97,
"rsi":  72.65,
"ret": 0.0068596 
},
{
 "date":  -4175,
"name": "GSPC.Close",
"price":  47.15,
"rsi": 75.552,
"ret": 0.0038322 
},
{
 "date":  -4174,
"name": "GSPC.Close",
"price":  46.96,
"rsi": 77.029,
"ret": -0.0040297 
},
{
 "date":  -4173,
"name": "GSPC.Close",
"price":  47.09,
"rsi":  72.08,
"ret": 0.0027683 
},
{
 "date":  -4172,
"name": "GSPC.Close",
"price":  47.19,
"rsi": 73.342,
"ret": 0.0021236 
},
{
 "date":  -4171,
"name": "GSPC.Close",
"price":  47.49,
"rsi": 74.304,
"ret": 0.0063573 
},
{
 "date":  -4168,
"name": "GSPC.Close",
"price":  47.94,
"rsi": 76.987,
"ret": 0.0094757 
},
{
 "date":  -4167,
"name": "GSPC.Close",
"price":  47.75,
"rsi": 80.309,
"ret": -0.0039633 
},
{
 "date":  -4166,
"name": "GSPC.Close",
"price":  47.46,
"rsi": 75.363,
"ret": -0.0060733 
},
{
 "date":  -4165,
"name": "GSPC.Close",
"price":  47.77,
"rsi": 68.434,
"ret": 0.0065318 
},
{
 "date":  -4164,
"name": "GSPC.Close",
"price":  48.05,
"rsi": 71.455,
"ret": 0.0058614 
},
{
 "date":  -4161,
"name": "GSPC.Close",
"price":  48.16,
"rsi": 73.886,
"ret": 0.0022893 
},
{
 "date":  -4160,
"name": "GSPC.Close",
"price":  47.73,
"rsi": 74.795,
"ret": -0.0089286 
},
{
 "date":  -4159,
"name": "GSPC.Close",
"price":  47.81,
"rsi": 65.242,
"ret": 0.0016761 
},
{
 "date":  -4158,
"name": "GSPC.Close",
"price":  47.91,
"rsi":  66.11,
"ret": 0.0020916 
},
{
 "date":  -4157,
"name": "GSPC.Close",
"price":   47.5,
"rsi": 67.211,
"ret": -0.0085577 
},
{
 "date":  -4154,
"name": "GSPC.Close",
"price":  47.22,
"rsi": 58.778,
"ret": -0.0058947 
},
{
 "date":  -4153,
"name": "GSPC.Close",
"price":   47.3,
"rsi": 53.812,
"ret": 0.0016942 
},
{
 "date":  -4152,
"name": "GSPC.Close",
"price":  47.32,
"rsi": 54.982,
"ret": 0.00042283 
},
{
 "date":  -4151,
"name": "GSPC.Close",
"price":  47.63,
"rsi": 55.287,
"ret": 0.0065511 
},
{
 "date":  -4150,
"name": "GSPC.Close",
"price":  47.73,
"rsi":  59.83,
"ret": 0.0020995 
},
{
 "date":  -4147,
"name": "GSPC.Close",
"price":  47.74,
"rsi":   61.2,
"ret": 0.00020951 
},
{
 "date":  -4146,
"name": "GSPC.Close",
"price":   47.9,
"rsi": 61.342,
"ret": 0.0033515 
},
{
 "date":  -4145,
"name": "GSPC.Close",
"price":  47.91,
"rsi": 63.634,
"ret": 0.00020877 
},
{
 "date":  -4144,
"name": "GSPC.Close",
"price":  47.66,
"rsi": 63.778,
"ret": -0.0052181 
},
{
 "date":  -4143,
"name": "GSPC.Close",
"price":  47.75,
"rsi": 57.612,
"ret": 0.0018884 
},
{
 "date":  -4139,
"name": "GSPC.Close",
"price":     48,
"rsi": 59.144,
"ret": 0.0052356 
},
{
 "date":  -4138,
"name": "GSPC.Close",
"price":  48.18,
"rsi": 63.129,
"ret": 0.00375 
},
{
 "date":  -4137,
"name": "GSPC.Close",
"price":   48.1,
"rsi": 65.721,
"ret": -0.0016604 
},
{
 "date":  -4136,
"name": "GSPC.Close",
"price":  47.97,
"rsi": 63.581,
"ret": -0.0027027 
},
{
 "date":  -4133,
"name": "GSPC.Close",
"price":  48.13,
"rsi": 60.154,
"ret": 0.0033354 
},
{
 "date":  -4132,
"name": "GSPC.Close",
"price":  48.46,
"rsi": 62.811,
"ret": 0.0068564 
},
{
 "date":  -4131,
"name": "GSPC.Close",
"price":  48.31,
"rsi": 67.608,
"ret": -0.0030953 
},
{
 "date":  -4130,
"name": "GSPC.Close",
"price":  48.64,
"rsi": 63.593,
"ret": 0.0068309 
},
{
 "date":  -4129,
"name": "GSPC.Close",
"price":  48.53,
"rsi": 68.084,
"ret": -0.0022615 
},
{
 "date":  -4126,
"name": "GSPC.Close",
"price":  48.96,
"rsi": 65.197,
"ret": 0.0088605 
},
{
 "date":  -4125,
"name": "GSPC.Close",
"price":  49.35,
"rsi": 70.469,
"ret": 0.0079657 
},
{
 "date":  -4124,
"name": "GSPC.Close",
"price":  49.35,
"rsi": 74.275,
"ret":      0 
},
{
 "date":  -4123,
"name": "GSPC.Close",
"price":  49.38,
"rsi": 74.275,
"ret": 0.0006079 
},
{
 "date":  -4122,
"name": "GSPC.Close",
"price":   49.4,
"rsi": 74.567,
"ret": 0.00040502 
},
{
 "date":  -4119,
"name": "GSPC.Close",
"price":   49.2,
"rsi": 74.773,
"ret": -0.0040486 
},
{
 "date":  -4118,
"name": "GSPC.Close",
"price":  49.56,
"rsi": 68.777,
"ret": 0.0073171 
},
{
 "date":  -4117,
"name": "GSPC.Close",
"price":  49.78,
"rsi": 72.978,
"ret": 0.0044391 
},
{
 "date":  -4116,
"name": "GSPC.Close",
"price":  49.57,
"rsi": 75.176,
"ret": -0.0042186 
},
{
 "date":  -4115,
"name": "GSPC.Close",
"price":  49.66,
"rsi": 69.375,
"ret": 0.0018156 
},
{
 "date":  -4112,
"name": "GSPC.Close",
"price":  49.87,
"rsi": 70.428,
"ret": 0.0042288 
},
{
 "date":  -4111,
"name": "GSPC.Close",
"price":  50.06,
"rsi":  72.78,
"ret": 0.0038099 
},
{
 "date":  -4110,
"name": "GSPC.Close",
"price":  49.98,
"rsi": 74.738,
"ret": -0.0015981 
},
{
 "date":  -4109,
"name": "GSPC.Close",
"price":  50.17,
"rsi": 72.378,
"ret": 0.0038015 
},
{
 "date":  -4108,
"name": "GSPC.Close",
"price":  50.37,
"rsi": 74.442,
"ret": 0.0039864 
},
{
 "date":  -4105,
"name": "GSPC.Close",
"price":  51.07,
"rsi": 76.438,
"ret": 0.013897 
},
{
 "date":  -4104,
"name": "GSPC.Close",
"price":  51.07,
"rsi": 81.798,
"ret":      0 
},
{
 "date":  -4103,
"name": "GSPC.Close",
"price":  51.06,
"rsi": 81.798,
"ret": -0.00019581 
},
{
 "date":  -4102,
"name": "GSPC.Close",
"price":  51.05,
"rsi":  81.49,
"ret": -0.00019585 
},
{
 "date":  -4101,
"name": "GSPC.Close",
"price":  51.39,
"rsi": 81.162,
"ret": 0.0066601 
},
{
 "date":  -4098,
"name": "GSPC.Close",
"price":  51.62,
"rsi": 83.583,
"ret": 0.0044756 
},
{
 "date":  -4097,
"name": "GSPC.Close",
"price":  51.26,
"rsi": 84.988,
"ret": -0.006974 
},
{
 "date":  -4096,
"name": "GSPC.Close",
"price":  50.58,
"rsi": 74.272,
"ret": -0.013266 
},
{
 "date":  -4095,
"name": "GSPC.Close",
"price":  50.94,
"rsi":  59.11,
"ret": 0.0071174 
},
{
 "date":  -4094,
"name": "GSPC.Close",
"price":  51.46,
"rsi": 63.373,
"ret": 0.010208 
},
{
 "date":  -4091,
"name": "GSPC.Close",
"price":  51.27,
"rsi": 68.484,
"ret": -0.0036922 
},
{
 "date":  -4090,
"name": "GSPC.Close",
"price":  51.27,
"rsi": 64.919,
"ret":      0 
},
{
 "date":  -4089,
"name": "GSPC.Close",
"price":  51.07,
"rsi": 64.919,
"ret": -0.0039009 
},
{
 "date":  -4088,
"name": "GSPC.Close",
"price":  50.97,
"rsi": 61.041,
"ret": -0.0019581 
},
{
 "date":  -4087,
"name": "GSPC.Close",
"price":  50.81,
"rsi": 59.138,
"ret": -0.0031391 
},
{
 "date":  -4084,
"name": "GSPC.Close",
"price":  50.42,
"rsi": 56.124,
"ret": -0.0076757 
},
{
 "date":  -4083,
"name": "GSPC.Close",
"price":  50.58,
"rsi": 49.501,
"ret": 0.0031733 
},
{
 "date":  -4082,
"name": "GSPC.Close",
"price":  51.07,
"rsi": 52.004,
"ret": 0.0096876 
},
{
 "date":  -4081,
"name": "GSPC.Close",
"price":  51.27,
"rsi": 58.746,
"ret": 0.0039162 
},
{
 "date":  -4080,
"name": "GSPC.Close",
"price":  51.33,
"rsi": 61.145,
"ret": 0.0011703 
},
{
 "date":  -4077,
"name": "GSPC.Close",
"price":  51.56,
"rsi": 61.861,
"ret": 0.0044808 
},
{
 "date":  -4075,
"name": "GSPC.Close",
"price":  52.03,
"rsi": 64.559,
"ret": 0.0091156 
},
{
 "date":  -4074,
"name": "GSPC.Close",
"price":  52.45,
"rsi": 69.334,
"ret": 0.0080723 
},
{
 "date":  -4073,
"name": "GSPC.Close",
"price":  52.26,
"rsi": 72.853,
"ret": -0.0036225 
},
{
 "date":  -4070,
"name": "GSPC.Close",
"price":  52.57,
"rsi": 68.996,
"ret": 0.0059319 
},
{
 "date":  -4069,
"name": "GSPC.Close",
"price":  52.98,
"rsi": 71.635,
"ret": 0.0077991 
},
{
 "date":  -4068,
"name": "GSPC.Close",
"price":  53.05,
"rsi": 74.702,
"ret": 0.0013213 
},
{
 "date":  -4067,
"name": "GSPC.Close",
"price":  52.83,
"rsi": 75.195,
"ret": -0.004147 
},
{
 "date":  -4066,
"name": "GSPC.Close",
"price":  53.09,
"rsi": 70.541,
"ret": 0.0049214 
},
{
 "date":  -4063,
"name": "GSPC.Close",
"price":  53.24,
"rsi": 72.692,
"ret": 0.0028254 
},
{
 "date":  -4062,
"name": "GSPC.Close",
"price":  53.13,
"rsi": 73.877,
"ret": -0.0020661 
},
{
 "date":  -4061,
"name": "GSPC.Close",
"price":   53.2,
"rsi": 71.429,
"ret": 0.0013175 
},
{
 "date":  -4060,
"name": "GSPC.Close",
"price":  53.21,
"rsi": 72.063,
"ret": 0.00018797 
},
{
 "date":  -4059,
"name": "GSPC.Close",
"price":   52.7,
"rsi": 72.159,
"ret": -0.0095847 
},
{
 "date":  -4056,
"name": "GSPC.Close",
"price":  52.03,
"rsi": 60.791,
"ret": -0.012713 
},
{
 "date":  -4055,
"name": "GSPC.Close",
"price":  51.02,
"rsi": 49.711,
"ret": -0.019412 
},
{
 "date":  -4054,
"name": "GSPC.Close",
"price":   51.9,
"rsi": 38.361,
"ret": 0.017248 
},
{
 "date":  -4052,
"name": "GSPC.Close",
"price":  52.48,
"rsi": 49.236,
"ret": 0.011175 
},
{
 "date":  -4049,
"name": "GSPC.Close",
"price":  52.69,
"rsi": 54.886,
"ret": 0.0040015 
},
{
 "date":  -4048,
"name": "GSPC.Close",
"price":  52.46,
"rsi": 56.763,
"ret": -0.0043652 
},
{
 "date":  -4047,
"name": "GSPC.Close",
"price":  52.53,
"rsi": 54.108,
"ret": 0.0013343 
},
{
 "date":  -4046,
"name": "GSPC.Close",
"price":  52.55,
"rsi": 54.801,
"ret": 0.00038073 
},
{
 "date":  -4045,
"name": "GSPC.Close",
"price":  52.46,
"rsi":  55.01,
"ret": -0.0017127 
},
{
 "date":  -4042,
"name": "GSPC.Close",
"price":  52.46,
"rsi": 53.804,
"ret":      0 
},
{
 "date":  -4041,
"name": "GSPC.Close",
"price":  52.82,
"rsi": 53.804,
"ret": 0.0068624 
},
{
 "date":  -4040,
"name": "GSPC.Close",
"price":  53.46,
"rsi": 58.067,
"ret": 0.012117 
},
{
 "date":  -4039,
"name": "GSPC.Close",
"price":  53.35,
"rsi": 64.363,
"ret": -0.0020576 
},
{
 "date":  -4038,
"name": "GSPC.Close",
"price":  53.22,
"rsi": 62.623,
"ret": -0.0024367 
},
{
 "date":  -4035,
"name": "GSPC.Close",
"price":  53.37,
"rsi":  60.54,
"ret": 0.0028185 
},
{
 "date":  -4034,
"name": "GSPC.Close",
"price":  53.57,
"rsi": 62.106,
"ret": 0.0037474 
},
{
 "date":  -4033,
"name": "GSPC.Close",
"price":  53.92,
"rsi":  64.15,
"ret": 0.0065335 
},
{
 "date":  -4032,
"name": "GSPC.Close",
"price":  54.15,
"rsi": 67.457,
"ret": 0.0042656 
},
{
 "date":  -4031,
"name": "GSPC.Close",
"price":  54.07,
"rsi": 69.452,
"ret": -0.0014774 
},
{
 "date":  -4028,
"name": "GSPC.Close",
"price":  53.71,
"rsi": 67.893,
"ret": -0.006658 
},
{
 "date":  -4027,
"name": "GSPC.Close",
"price":  53.42,
"rsi": 61.233,
"ret": -0.0053994 
},
{
 "date":  -4026,
"name": "GSPC.Close",
"price":  54.11,
"rsi": 56.431,
"ret": 0.012917 
},
{
 "date":  -4021,
"name": "GSPC.Close",
"price":  54.74,
"rsi": 63.721,
"ret": 0.011643 
},
{
 "date":  -4020,
"name": "GSPC.Close",
"price":  54.93,
"rsi": 68.847,
"ret": 0.003471 
},
{
 "date":  -4019,
"name": "GSPC.Close",
"price":  55.21,
"rsi": 70.214,
"ret": 0.0050974 
},
{
 "date":  -4017,
"name": "GSPC.Close",
"price":  55.44,
"rsi": 72.153,
"ret": 0.0041659 
},
{
 "date":  -4014,
"name": "GSPC.Close",
"price":  55.66,
"rsi": 73.669,
"ret": 0.0039683 
},
{
 "date":  -4013,
"name": "GSPC.Close",
"price":  55.59,
"rsi": 75.067,
"ret": -0.0012576 
},
{
 "date":  -4012,
"name": "GSPC.Close",
"price":  54.89,
"rsi": 73.726,
"ret": -0.012592 
},
{
 "date":  -4011,
"name": "GSPC.Close",
"price":   55.4,
"rsi": 61.825,
"ret": 0.0092913 
},
{
 "date":  -4010,
"name": "GSPC.Close",
"price":  55.77,
"rsi": 66.117,
"ret": 0.0066787 
},
{
 "date":  -4007,
"name": "GSPC.Close",
"price":  55.78,
"rsi": 68.852,
"ret": 0.00017931 
},
{
 "date":  -4006,
"name": "GSPC.Close",
"price":  55.47,
"rsi": 68.925,
"ret": -0.0055575 
},
{
 "date":  -4005,
"name": "GSPC.Close",
"price":  55.62,
"rsi": 63.922,
"ret": 0.0027042 
},
{
 "date":  -4004,
"name": "GSPC.Close",
"price":  55.83,
"rsi": 65.237,
"ret": 0.0037756 
},
{
 "date":  -4003,
"name": "GSPC.Close",
"price":  55.81,
"rsi": 67.048,
"ret": -0.00035823 
},
{
 "date":  -4000,
"name": "GSPC.Close",
"price":  55.68,
"rsi": 66.692,
"ret": -0.0023293 
},
{
 "date":  -3999,
"name": "GSPC.Close",
"price":  55.72,
"rsi":   64.3,
"ret": 0.00071839 
},
{
 "date":  -3998,
"name": "GSPC.Close",
"price":  56.04,
"rsi": 64.719,
"ret": 0.005743 
},
{
 "date":  -3997,
"name": "GSPC.Close",
"price":  55.97,
"rsi": 67.961,
"ret": -0.0012491 
},
{
 "date":  -3996,
"name": "GSPC.Close",
"price":     56,
"rsi": 66.521,
"ret": 0.000536 
},
{
 "date":  -3993,
"name": "GSPC.Close",
"price":  55.77,
"rsi": 66.845,
"ret": -0.0041071 
},
{
 "date":  -3992,
"name": "GSPC.Close",
"price":  55.78,
"rsi": 61.896,
"ret": 0.00017931 
},
{
 "date":  -3991,
"name": "GSPC.Close",
"price":  55.16,
"rsi": 62.028,
"ret": -0.011115 
},
{
 "date":  -3990,
"name": "GSPC.Close",
"price":   55.2,
"rsi": 50.402,
"ret": 0.00072516 
},
{
 "date":  -3989,
"name": "GSPC.Close",
"price":  55.45,
"rsi":  51.04,
"ret": 0.004529 
},
{
 "date":  -3986,
"name": "GSPC.Close",
"price":  55.21,
"rsi": 54.939,
"ret": -0.0043282 
},
{
 "date":  -3985,
"name": "GSPC.Close",
"price":  55.28,
"rsi":  50.76,
"ret": 0.0012679 
},
{
 "date":  -3984,
"name": "GSPC.Close",
"price":  55.06,
"rsi": 51.909,
"ret": -0.0039797 
},
{
 "date":  -3983,
"name": "GSPC.Close",
"price":  54.81,
"rsi": 48.109,
"ret": -0.0045405 
},
{
 "date":  -3982,
"name": "GSPC.Close",
"price":  54.37,
"rsi": 44.154,
"ret": -0.0080277 
},
{
 "date":  -3979,
"name": "GSPC.Close",
"price":  53.58,
"rsi": 38.201,
"ret": -0.01453 
},
{
 "date":  -3978,
"name": "GSPC.Close",
"price":  54.32,
"rsi": 30.302,
"ret": 0.013811 
},
{
 "date":  -3977,
"name": "GSPC.Close",
"price":  54.35,
"rsi": 42.331,
"ret": 0.00055228 
},
{
 "date":  -3976,
"name": "GSPC.Close",
"price":     54,
"rsi": 42.763,
"ret": -0.0064397 
},
{
 "date":  -3975,
"name": "GSPC.Close",
"price":  54.42,
"rsi":  39.09,
"ret": 0.0077778 
},
{
 "date":  -3972,
"name": "GSPC.Close",
"price":   54.5,
"rsi": 45.175,
"ret": 0.00147 
},
{
 "date":  -3971,
"name": "GSPC.Close",
"price":  54.29,
"rsi": 46.276,
"ret": -0.0038532 
},
{
 "date":  -3970,
"name": "GSPC.Close",
"price":   54.3,
"rsi":  43.79,
"ret": 0.0001842 
},
{
 "date":  -3969,
"name": "GSPC.Close",
"price":   55.5,
"rsi": 43.945,
"ret": 0.022099 
},
{
 "date":  -3968,
"name": "GSPC.Close",
"price":  55.52,
"rsi": 58.632,
"ret": 0.00036036 
},
{
 "date":  -3964,
"name": "GSPC.Close",
"price":  55.48,
"rsi": 58.826,
"ret": -0.00072046 
},
{
 "date":  -3963,
"name": "GSPC.Close",
"price":  55.24,
"rsi": 58.239,
"ret": -0.0043259 
},
{
 "date":  -3962,
"name": "GSPC.Close",
"price":  55.34,
"rsi":  54.71,
"ret": 0.0018103 
},
{
 "date":  -3961,
"name": "GSPC.Close",
"price":  55.41,
"rsi": 55.909,
"ret": 0.0012649 
},
{
 "date":  -3958,
"name": "GSPC.Close",
"price":  55.73,
"rsi": 56.771,
"ret": 0.0057751 
},
{
 "date":  -3957,
"name": "GSPC.Close",
"price":  56.25,
"rsi": 60.569,
"ret": 0.0093307 
},
{
 "date":  -3956,
"name": "GSPC.Close",
"price":  56.35,
"rsi": 65.823,
"ret": 0.0017778 
},
{
 "date":  -3955,
"name": "GSPC.Close",
"price":  56.43,
"rsi":  66.74,
"ret": 0.0014197 
},
{
 "date":  -3954,
"name": "GSPC.Close",
"price":  56.21,
"rsi": 67.493,
"ret": -0.0038986 
},
{
 "date":  -3951,
"name": "GSPC.Close",
"price":  56.15,
"rsi": 63.256,
"ret": -0.0010674 
},
{
 "date":  -3950,
"name": "GSPC.Close",
"price":  56.31,
"rsi": 62.111,
"ret": 0.0028495 
},
{
 "date":  -3949,
"name": "GSPC.Close",
"price":  56.35,
"rsi": 63.984,
"ret": 0.00071035 
},
{
 "date":  -3948,
"name": "GSPC.Close",
"price":   56.6,
"rsi": 64.456,
"ret": 0.0044366 
},
{
 "date":  -3947,
"name": "GSPC.Close",
"price":  56.67,
"rsi": 67.342,
"ret": 0.0012367 
},
{
 "date":  -3944,
"name": "GSPC.Close",
"price":  56.06,
"rsi": 68.123,
"ret": -0.010764 
},
{
 "date":  -3943,
"name": "GSPC.Close",
"price":  56.52,
"rsi": 55.644,
"ret": 0.0082055 
},
{
 "date":  -3942,
"name": "GSPC.Close",
"price":  56.39,
"rsi": 61.388,
"ret": -0.0023001 
},
{
 "date":  -3941,
"name": "GSPC.Close",
"price":  56.34,
"rsi":  59.06,
"ret": -0.00088668 
},
{
 "date":  -3940,
"name": "GSPC.Close",
"price":  56.39,
"rsi": 58.147,
"ret": 0.00088747 
},
{
 "date":  -3937,
"name": "GSPC.Close",
"price":  55.87,
"rsi": 58.832,
"ret": -0.0092215 
},
{
 "date":  -3936,
"name": "GSPC.Close",
"price":  55.96,
"rsi": 49.712,
"ret": 0.0016109 
},
{
 "date":  -3935,
"name": "GSPC.Close",
"price":  55.88,
"rsi": 51.125,
"ret": -0.0014296 
},
{
 "date":  -3934,
"name": "GSPC.Close",
"price":  55.76,
"rsi": 49.786,
"ret": -0.0021475 
},
{
 "date":  -3930,
"name": "GSPC.Close",
"price":  55.45,
"rsi": 47.766,
"ret": -0.0055595 
},
{
 "date":  -3929,
"name": "GSPC.Close",
"price":  55.44,
"rsi": 42.922,
"ret": -0.00018034 
},
{
 "date":  -3928,
"name": "GSPC.Close",
"price":  55.69,
"rsi": 42.771,
"ret": 0.0045094 
},
{
 "date":  -3927,
"name": "GSPC.Close",
"price":     56,
"rsi": 47.713,
"ret": 0.0055665 
},
{
 "date":  -3926,
"name": "GSPC.Close",
"price":  56.44,
"rsi":  53.12,
"ret": 0.0078571 
},
{
 "date":  -3923,
"name": "GSPC.Close",
"price":   56.6,
"rsi": 59.519,
"ret": 0.0028349 
},
{
 "date":  -3922,
"name": "GSPC.Close",
"price":  56.48,
"rsi": 61.573,
"ret": -0.0021201 
},
{
 "date":  -3921,
"name": "GSPC.Close",
"price":  56.21,
"rsi": 59.149,
"ret": -0.0047805 
},
{
 "date":  -3920,
"name": "GSPC.Close",
"price":  56.17,
"rsi": 53.998,
"ret": -0.00071162 
},
{
 "date":  -3919,
"name": "GSPC.Close",
"price":  56.22,
"rsi": 53.258,
"ret": 0.00089015 
},
{
 "date":  -3916,
"name": "GSPC.Close",
"price":  56.43,
"rsi": 54.105,
"ret": 0.0037353 
},
{
 "date":  -3915,
"name": "GSPC.Close",
"price":  56.71,
"rsi":  57.58,
"ret": 0.0049619 
},
{
 "date":  -3914,
"name": "GSPC.Close",
"price":  56.96,
"rsi":  61.74,
"ret": 0.0044084 
},
{
 "date":  -3913,
"name": "GSPC.Close",
"price":  57.43,
"rsi": 65.036,
"ret": 0.0082514 
},
{
 "date":  -3912,
"name": "GSPC.Close",
"price":  57.92,
"rsi":  70.23,
"ret": 0.0085321 
},
{
 "date":  -3909,
"name": "GSPC.Close",
"price":  58.17,
"rsi": 74.485,
"ret": 0.0043163 
},
{
 "date":  -3908,
"name": "GSPC.Close",
"price":  58.11,
"rsi": 76.343,
"ret": -0.0010315 
},
{
 "date":  -3907,
"name": "GSPC.Close",
"price":  57.73,
"rsi": 74.933,
"ret": -0.0065393 
},
{
 "date":  -3906,
"name": "GSPC.Close",
"price":   57.6,
"rsi": 66.548,
"ret": -0.0022519 
},
{
 "date":  -3905,
"name": "GSPC.Close",
"price":  57.96,
"rsi": 63.913,
"ret": 0.00625 
},
{
 "date":  -3902,
"name": "GSPC.Close",
"price":  58.14,
"rsi": 67.724,
"ret": 0.0031056 
},
{
 "date":  -3901,
"name": "GSPC.Close",
"price":  57.92,
"rsi": 69.461,
"ret": -0.003784 
},
{
 "date":  -3900,
"name": "GSPC.Close",
"price":  57.69,
"rsi": 64.867,
"ret": -0.003971 
},
{
 "date":  -3899,
"name": "GSPC.Close",
"price":  57.59,
"rsi": 60.372,
"ret": -0.0017334 
},
{
 "date":  -3898,
"name": "GSPC.Close",
"price":  57.65,
"rsi": 58.474,
"ret": 0.0010418 
},
{
 "date":  -3895,
"name": "GSPC.Close",
"price":  57.65,
"rsi": 59.301,
"ret":      0 
},
{
 "date":  -3894,
"name": "GSPC.Close",
"price":  57.75,
"rsi": 59.301,
"ret": 0.0017346 
},
{
 "date":  -3893,
"name": "GSPC.Close",
"price":  57.61,
"rsi": 60.809,
"ret": -0.0024242 
},
{
 "date":  -3892,
"name": "GSPC.Close",
"price":  56.88,
"rsi": 57.592,
"ret": -0.012671 
},
{
 "date":  -3891,
"name": "GSPC.Close",
"price":  57.32,
"rsi": 44.402,
"ret": 0.0077356 
},
{
 "date":  -3888,
"name": "GSPC.Close",
"price":  57.96,
"rsi": 51.597,
"ret": 0.011165 
},
{
 "date":  -3887,
"name": "GSPC.Close",
"price":  57.96,
"rsi": 59.756,
"ret":      0 
},
{
 "date":  -3886,
"name": "GSPC.Close",
"price":  57.97,
"rsi": 59.756,
"ret": 0.00017253 
},
{
 "date":  -3885,
"name": "GSPC.Close",
"price":  58.37,
"rsi": 59.879,
"ret": 0.0069001 
},
{
 "date":  -3884,
"name": "GSPC.Close",
"price":  58.16,
"rsi": 64.531,
"ret": -0.0035977 
},
{
 "date":  -3881,
"name": "GSPC.Close",
"price":  58.15,
"rsi": 60.561,
"ret": -0.00017194 
},
{
 "date":  -3880,
"name": "GSPC.Close",
"price":  58.32,
"rsi":  60.37,
"ret": 0.0029235 
},
{
 "date":  -3879,
"name": "GSPC.Close",
"price":  58.09,
"rsi": 62.528,
"ret": -0.0039438 
},
{
 "date":  -3878,
"name": "GSPC.Close",
"price":  58.14,
"rsi": 57.932,
"ret": 0.00086073 
},
{
 "date":  -3877,
"name": "GSPC.Close",
"price":  58.33,
"rsi": 58.644,
"ret": 0.003268 
},
{
 "date":  -3874,
"name": "GSPC.Close",
"price":  58.18,
"rsi": 61.321,
"ret": -0.0025716 
},
{
 "date":  -3873,
"name": "GSPC.Close",
"price":  58.09,
"rsi": 58.122,
"ret": -0.0015469 
},
{
 "date":  -3872,
"name": "GSPC.Close",
"price":  58.19,
"rsi": 56.226,
"ret": 0.0017215 
},
{
 "date":  -3871,
"name": "GSPC.Close",
"price":  58.39,
"rsi":  57.87,
"ret": 0.003437 
},
{
 "date":  -3870,
"name": "GSPC.Close",
"price":  58.68,
"rsi": 61.023,
"ret": 0.0049666 
},
{
 "date":  -3867,
"name": "GSPC.Close",
"price":  58.63,
"rsi": 65.102,
"ret": -0.00085208 
},
{
 "date":  -3866,
"name": "GSPC.Close",
"price":  58.23,
"rsi": 63.861,
"ret": -0.0068224 
},
{
 "date":  -3865,
"name": "GSPC.Close",
"price":  58.25,
"rsi": 54.854,
"ret": 0.00034347 
},
{
 "date":  -3864,
"name": "GSPC.Close",
"price":  57.63,
"rsi": 55.194,
"ret": -0.010644 
},
{
 "date":  -3863,
"name": "GSPC.Close",
"price":  57.51,
"rsi": 44.098,
"ret": -0.0020822 
},
{
 "date":  -3860,
"name": "GSPC.Close",
"price":  56.76,
"rsi": 42.324,
"ret": -0.013041 
},
{
 "date":  -3859,
"name": "GSPC.Close",
"price":  56.36,
"rsi": 33.308,
"ret": -0.0070472 
},
{
 "date":  -3858,
"name": "GSPC.Close",
"price":  57.19,
"rsi": 29.676,
"ret": 0.014727 
},
{
 "date":  -3857,
"name": "GSPC.Close",
"price":  57.25,
"rsi": 43.452,
"ret": 0.0010491 
},
{
 "date":  -3856,
"name": "GSPC.Close",
"price":  57.29,
"rsi": 44.302,
"ret": 0.00069869 
},
{
 "date":  -3853,
"name": "GSPC.Close",
"price":  56.99,
"rsi": 44.896,
"ret": -0.0052365 
},
{
 "date":  -3852,
"name": "GSPC.Close",
"price":  56.56,
"rsi": 41.334,
"ret": -0.0075452 
},
{
 "date":  -3851,
"name": "GSPC.Close",
"price":  57.09,
"rsi": 36.824,
"ret": 0.0093706 
},
{
 "date":  -3850,
"name": "GSPC.Close",
"price":  57.05,
"rsi": 44.816,
"ret": -0.00070065 
},
{
 "date":  -3849,
"name": "GSPC.Close",
"price":  57.13,
"rsi":  44.36,
"ret": 0.0014023 
},
{
 "date":  -3846,
"name": "GSPC.Close",
"price":  57.13,
"rsi": 45.554,
"ret":      0 
},
{
 "date":  -3845,
"name": "GSPC.Close",
"price":  57.12,
"rsi": 45.554,
"ret": -0.00017504 
},
{
 "date":  -3844,
"name": "GSPC.Close",
"price":  57.41,
"rsi": 45.412,
"ret": 0.005077 
},
{
 "date":  -3843,
"name": "GSPC.Close",
"price":  57.73,
"rsi": 50.231,
"ret": 0.0055739 
},
{
 "date":  -3842,
"name": "GSPC.Close",
"price":  57.98,
"rsi": 54.956,
"ret": 0.0043305 
},
{
 "date":  -3839,
"name": "GSPC.Close",
"price":  58.37,
"rsi": 58.287,
"ret": 0.0067265 
},
{
 "date":  -3838,
"name": "GSPC.Close",
"price":  58.47,
"rsi": 62.898,
"ret": 0.0017132 
},
{
 "date":  -3837,
"name": "GSPC.Close",
"price":  58.97,
"rsi": 63.996,
"ret": 0.0085514 
},
{
 "date":  -3836,
"name": "GSPC.Close",
"price":  59.28,
"rsi": 68.948,
"ret": 0.0052569 
},
{
 "date":  -3832,
"name": "GSPC.Close",
"price":  59.65,
"rsi":  71.56,
"ret": 0.0062416 
},
{
 "date":  -3831,
"name": "GSPC.Close",
"price":  60.01,
"rsi": 74.335,
"ret": 0.0060352 
},
{
 "date":  -3830,
"name": "GSPC.Close",
"price":  60.03,
"rsi": 76.715,
"ret": 0.00033328 
},
{
 "date":  -3829,
"name": "GSPC.Close",
"price":  59.97,
"rsi": 76.844,
"ret": -0.0009995 
},
{
 "date":  -3828,
"name": "GSPC.Close",
"price":  59.91,
"rsi": 75.498,
"ret": -0.0010005 
},
{
 "date":  -3825,
"name": "GSPC.Close",
"price":  59.41,
"rsi":   74.1,
"ret": -0.0083459 
},
{
 "date":  -3824,
"name": "GSPC.Close",
"price":  59.55,
"rsi": 63.542,
"ret": 0.0023565 
},
{
 "date":  -3823,
"name": "GSPC.Close",
"price":  59.59,
"rsi": 65.044,
"ret": 0.0006717 
},
{
 "date":  -3822,
"name": "GSPC.Close",
"price":  59.41,
"rsi": 65.481,
"ret": -0.0030206 
},
{
 "date":  -3821,
"name": "GSPC.Close",
"price":  59.19,
"rsi": 61.737,
"ret": -0.0037031 
},
{
 "date":  -3818,
"name": "GSPC.Close",
"price":  58.91,
"rsi": 57.415,
"ret": -0.0047305 
},
{
 "date":  -3817,
"name": "GSPC.Close",
"price":  59.41,
"rsi": 52.388,
"ret": 0.0084875 
},
{
 "date":  -3816,
"name": "GSPC.Close",
"price":  59.61,
"rsi": 59.249,
"ret": 0.0033664 
},
{
 "date":  -3815,
"name": "GSPC.Close",
"price":  59.67,
"rsi": 61.631,
"ret": 0.0010065 
},
{
 "date":  -3814,
"name": "GSPC.Close",
"price":  59.65,
"rsi": 62.342,
"ret": -0.00033518 
},
{
 "date":  -3811,
"name": "GSPC.Close",
"price":  60.02,
"rsi":  61.93,
"ret": 0.0062028 
},
{
 "date":  -3810,
"name": "GSPC.Close",
"price":  60.32,
"rsi": 66.359,
"ret": 0.0049983 
},
{
 "date":  -3809,
"name": "GSPC.Close",
"price":  60.62,
"rsi": 69.462,
"ret": 0.0049735 
},
{
 "date":  -3808,
"name": "GSPC.Close",
"price":   60.5,
"rsi": 72.221,
"ret": -0.0019795 
},
{
 "date":  -3807,
"name": "GSPC.Close",
"price":  60.51,
"rsi": 69.515,
"ret": 0.00016529 
},
{
 "date":  -3804,
"name": "GSPC.Close",
"price":  60.71,
"rsi": 69.618,
"ret": 0.0033052 
},
{
 "date":  -3803,
"name": "GSPC.Close",
"price":  60.61,
"rsi": 71.663,
"ret": -0.0016472 
},
{
 "date":  -3802,
"name": "GSPC.Close",
"price":   60.3,
"rsi": 69.156,
"ret": -0.0051147 
},
{
 "date":  -3801,
"name": "GSPC.Close",
"price":  60.24,
"rsi": 61.926,
"ret": -0.00099502 
},
{
 "date":  -3800,
"name": "GSPC.Close",
"price":  59.87,
"rsi": 60.605,
"ret": -0.0061421 
},
{
 "date":  -3797,
"name": "GSPC.Close",
"price":  58.62,
"rsi": 53.086,
"ret": -0.020879 
},
{
 "date":  -3796,
"name": "GSPC.Close",
"price":  59.39,
"rsi": 36.576,
"ret": 0.013135 
},
{
 "date":  -3795,
"name": "GSPC.Close",
"price":  59.25,
"rsi": 47.423,
"ret": -0.0023573 
},
{
 "date":  -3794,
"name": "GSPC.Close",
"price":  59.15,
"rsi": 45.886,
"ret": -0.0016878 
},
{
 "date":  -3793,
"name": "GSPC.Close",
"price":  59.29,
"rsi": 44.771,
"ret": 0.0023669 
},
{
 "date":  -3790,
"name": "GSPC.Close",
"price":  59.17,
"rsi": 46.724,
"ret": -0.002024 
},
{
 "date":  -3789,
"name": "GSPC.Close",
"price":  58.62,
"rsi": 45.247,
"ret": -0.0092953 
},
{
 "date":  -3788,
"name": "GSPC.Close",
"price":  58.27,
"rsi": 39.139,
"ret": -0.0059707 
},
{
 "date":  -3787,
"name": "GSPC.Close",
"price":  59.14,
"rsi": 35.825,
"ret": 0.01493 
},
{
 "date":  -3786,
"name": "GSPC.Close",
"price":  59.08,
"rsi": 47.684,
"ret": -0.0010145 
},
{
 "date":  -3783,
"name": "GSPC.Close",
"price":  58.87,
"rsi": 47.038,
"ret": -0.0035545 
},
{
 "date":  -3782,
"name": "GSPC.Close",
"price":  58.99,
"rsi": 44.754,
"ret": 0.0020384 
},
{
 "date":  -3781,
"name": "GSPC.Close",
"price":  59.07,
"rsi": 46.357,
"ret": 0.0013562 
},
{
 "date":  -3780,
"name": "GSPC.Close",
"price":  59.58,
"rsi": 47.451,
"ret": 0.0086338 
},
{
 "date":  -3779,
"name": "GSPC.Close",
"price":   59.6,
"rsi": 53.908,
"ret": 0.00033568 
},
{
 "date":  -3776,
"name": "GSPC.Close",
"price":   59.6,
"rsi": 54.146,
"ret":      0 
},
{
 "date":  -3775,
"name": "GSPC.Close",
"price":  58.87,
"rsi": 54.146,
"ret": -0.012248 
},
{
 "date":  -3774,
"name": "GSPC.Close",
"price":  58.92,
"rsi": 44.436,
"ret": 0.00084933 
},
{
 "date":  -3773,
"name": "GSPC.Close",
"price":  58.26,
"rsi": 45.161,
"ret": -0.011202 
},
{
 "date":  -3772,
"name": "GSPC.Close",
"price":  58.54,
"rsi": 38.092,
"ret": 0.004806 
},
{
 "date":  -3768,
"name": "GSPC.Close",
"price":   57.7,
"rsi": 42.224,
"ret": -0.014349 
},
{
 "date":  -3767,
"name": "GSPC.Close",
"price":  57.29,
"rsi": 34.734,
"ret": -0.0071057 
},
{
 "date":  -3766,
"name": "GSPC.Close",
"price":  56.99,
"rsi": 31.772,
"ret": -0.0052365 
},
{
 "date":  -3765,
"name": "GSPC.Close",
"price":  57.41,
"rsi": 29.771,
"ret": 0.0073697 
},
{
 "date":  -3762,
"name": "GSPC.Close",
"price":  56.99,
"rsi": 35.861,
"ret": -0.0073158 
},
{
 "date":  -3761,
"name": "GSPC.Close",
"price":  56.68,
"rsi": 32.798,
"ret": -0.0054396 
},
{
 "date":  -3760,
"name": "GSPC.Close",
"price":  56.72,
"rsi": 30.713,
"ret": 0.00070572 
},
{
 "date":  -3759,
"name": "GSPC.Close",
"price":  56.41,
"rsi": 31.319,
"ret": -0.0054654 
},
{
 "date":  -3758,
"name": "GSPC.Close",
"price":  56.19,
"rsi": 29.186,
"ret": -0.0039 
},
{
 "date":  -3755,
"name": "GSPC.Close",
"price":  55.27,
"rsi": 27.742,
"ret": -0.016373 
},
{
 "date":  -3754,
"name": "GSPC.Close",
"price":  55.14,
"rsi": 22.687,
"ret": -0.0023521 
},
{
 "date":  -3753,
"name": "GSPC.Close",
"price":  55.82,
"rsi": 22.075,
"ret": 0.012332 
},
{
 "date":  -3752,
"name": "GSPC.Close",
"price":  56.78,
"rsi": 32.356,
"ret": 0.017198 
},
{
 "date":  -3751,
"name": "GSPC.Close",
"price":  56.73,
"rsi": 43.657,
"ret": -0.00088059 
},
{
 "date":  -3748,
"name": "GSPC.Close",
"price":  57.15,
"rsi": 43.252,
"ret": 0.0074035 
},
{
 "date":  -3747,
"name": "GSPC.Close",
"price":  57.51,
"rsi": 47.649,
"ret": 0.0062992 
},
{
 "date":  -3746,
"name": "GSPC.Close",
"price":  56.88,
"rsi": 51.143,
"ret": -0.010955 
},
{
 "date":  -3745,
"name": "GSPC.Close",
"price":  56.94,
"rsi": 45.429,
"ret": 0.0010549 
},
{
 "date":  -3744,
"name": "GSPC.Close",
"price":   57.2,
"rsi": 46.047,
"ret": 0.0045662 
},
{
 "date":  -3741,
"name": "GSPC.Close",
"price":  57.14,
"rsi": 48.756,
"ret": -0.001049 
},
{
 "date":  -3740,
"name": "GSPC.Close",
"price":  57.09,
"rsi": 48.155,
"ret": -0.00087504 
},
{
 "date":  -3739,
"name": "GSPC.Close",
"price":  56.94,
"rsi": 47.628,
"ret": -0.0026274 
},
{
 "date":  -3738,
"name": "GSPC.Close",
"price":  56.81,
"rsi": 46.002,
"ret": -0.0022831 
},
{
 "date":  -3737,
"name": "GSPC.Close",
"price":     57,
"rsi": 44.582,
"ret": 0.0033445 
},
{
 "date":  -3734,
"name": "GSPC.Close",
"price":  57.32,
"rsi":  47.15,
"ret": 0.005614 
},
{
 "date":  -3733,
"name": "GSPC.Close",
"price":  57.16,
"rsi": 51.249,
"ret": -0.0027913 
},
{
 "date":  -3732,
"name": "GSPC.Close",
"price":  56.71,
"rsi": 49.195,
"ret": -0.0078726 
},
{
 "date":  -3731,
"name": "GSPC.Close",
"price":  56.87,
"rsi": 43.869,
"ret": 0.0028214 
},
{
 "date":  -3730,
"name": "GSPC.Close",
"price":  57.33,
"rsi": 46.103,
"ret": 0.0080886 
},
{
 "date":  -3727,
"name": "GSPC.Close",
"price":  57.01,
"rsi": 52.017,
"ret": -0.0055817 
},
{
 "date":  -3726,
"name": "GSPC.Close",
"price":  56.66,
"rsi": 48.066,
"ret": -0.0061393 
},
{
 "date":  -3725,
"name": "GSPC.Close",
"price":  56.55,
"rsi": 44.118,
"ret": -0.0019414 
},
{
 "date":  -3724,
"name": "GSPC.Close",
"price":     56,
"rsi": 42.925,
"ret": -0.0097259 
},
{
 "date":  -3723,
"name": "GSPC.Close",
"price":  56.56,
"rsi": 37.469,
"ret":   0.01 
},
{
 "date":  -3720,
"name": "GSPC.Close",
"price":  56.94,
"rsi": 45.118,
"ret": 0.0067185 
},
{
 "date":  -3719,
"name": "GSPC.Close",
"price":  57.42,
"rsi": 49.622,
"ret": 0.0084299 
},
{
 "date":  -3718,
"name": "GSPC.Close",
"price":  57.46,
"rsi":  54.68,
"ret": 0.00069662 
},
{
 "date":  -3717,
"name": "GSPC.Close",
"price":  57.41,
"rsi": 55.085,
"ret": -0.00087017 
},
{
 "date":  -3716,
"name": "GSPC.Close",
"price":  57.52,
"rsi": 54.431,
"ret": 0.001916 
},
{
 "date":  -3713,
"name": "GSPC.Close",
"price":  57.41,
"rsi": 55.678,
"ret": -0.0019124 
},
{
 "date":  -3711,
"name": "GSPC.Close",
"price":  57.26,
"rsi": 54.084,
"ret": -0.0026128 
},
{
 "date":  -3710,
"name": "GSPC.Close",
"price":  57.32,
"rsi": 51.901,
"ret": 0.0010479 
},
{
 "date":  -3709,
"name": "GSPC.Close",
"price":   57.6,
"rsi": 52.723,
"ret": 0.0048849 
},
{
 "date":  -3706,
"name": "GSPC.Close",
"price":   57.5,
"rsi": 56.462,
"ret": -0.0017361 
},
{
 "date":  -3705,
"name": "GSPC.Close",
"price":  57.48,
"rsi": 54.795,
"ret": -0.00034783 
},
{
 "date":  -3704,
"name": "GSPC.Close",
"price":  57.49,
"rsi": 54.449,
"ret": 0.00017397 
},
{
 "date":  -3703,
"name": "GSPC.Close",
"price":  57.17,
"rsi": 54.603,
"ret": -0.0055662 
},
{
 "date":  -3702,
"name": "GSPC.Close",
"price":  56.85,
"rsi": 48.891,
"ret": -0.0055973 
},
{
 "date":  -3699,
"name": "GSPC.Close",
"price":  56.22,
"rsi": 43.941,
"ret": -0.011082 
},
{
 "date":  -3698,
"name": "GSPC.Close",
"price":  56.38,
"rsi": 36.175,
"ret": 0.002846 
},
{
 "date":  -3697,
"name": "GSPC.Close",
"price":  56.99,
"rsi": 39.118,
"ret": 0.010819 
},
{
 "date":  -3696,
"name": "GSPC.Close",
"price":  56.94,
"rsi": 48.809,
"ret": -0.00087735 
},
{
 "date":  -3695,
"name": "GSPC.Close",
"price":  56.97,
"rsi": 48.133,
"ret": 0.00052687 
},
{
 "date":  -3692,
"name": "GSPC.Close",
"price":  57.08,
"rsi": 48.593,
"ret": 0.0019308 
},
{
 "date":  -3691,
"name": "GSPC.Close",
"price":  57.35,
"rsi": 50.333,
"ret": 0.0047302 
},
{
 "date":  -3690,
"name": "GSPC.Close",
"price":  57.44,
"rsi": 54.413,
"ret": 0.0015693 
},
{
 "date":  -3688,
"name": "GSPC.Close",
"price":   57.7,
"rsi": 55.718,
"ret": 0.0045265 
},
{
 "date":  -3685,
"name": "GSPC.Close",
"price":  58.28,
"rsi": 59.341,
"ret": 0.010052 
},
{
 "date":  -3684,
"name": "GSPC.Close",
"price":   58.7,
"rsi":  66.02,
"ret": 0.0072066 
},
{
 "date":  -3683,
"name": "GSPC.Close",
"price":   58.6,
"rsi": 69.879,
"ret": -0.0017036 
},
{
 "date":  -3682,
"name": "GSPC.Close",
"price":  58.73,
"rsi": 67.902,
"ret": 0.0022184 
},
{
 "date":  -3681,
"name": "GSPC.Close",
"price":  58.85,
"rsi": 69.125,
"ret": 0.0020432 
},
{
 "date":  -3678,
"name": "GSPC.Close",
"price":  58.96,
"rsi": 70.251,
"ret": 0.0018692 
},
{
 "date":  -3677,
"name": "GSPC.Close",
"price":  59.34,
"rsi": 71.286,
"ret": 0.006445 
},
{
 "date":  -3676,
"name": "GSPC.Close",
"price":  58.97,
"rsi": 74.575,
"ret": -0.0062353 
},
{
 "date":  -3675,
"name": "GSPC.Close",
"price":  59.02,
"rsi": 66.578,
"ret": 0.00084789 
},
{
 "date":  -3674,
"name": "GSPC.Close",
"price":  58.88,
"rsi": 67.092,
"ret": -0.0023721 
},
{
 "date":  -3671,
"name": "GSPC.Close",
"price":  59.04,
"rsi": 64.121,
"ret": 0.0027174 
},
{
 "date":  -3670,
"name": "GSPC.Close",
"price":   58.9,
"rsi": 65.975,
"ret": -0.0023713 
},
{
 "date":  -3669,
"name": "GSPC.Close",
"price":  58.97,
"rsi": 62.911,
"ret": 0.0011885 
},
{
 "date":  -3668,
"name": "GSPC.Close",
"price":  58.86,
"rsi": 63.816,
"ret": -0.0018654 
},
{
 "date":  -3667,
"name": "GSPC.Close",
"price":  59.14,
"rsi": 61.286,
"ret": 0.0047571 
},
{
 "date":  -3664,
"name": "GSPC.Close",
"price":  59.21,
"rsi": 65.081,
"ret": 0.0011836 
},
{
 "date":  -3663,
"name": "GSPC.Close",
"price":  59.14,
"rsi": 65.979,
"ret": -0.0011822 
},
{
 "date":  -3662,
"name": "GSPC.Close",
"price":  58.96,
"rsi": 64.201,
"ret": -0.0030436 
},
{
 "date":  -3661,
"name": "GSPC.Close",
"price":     59,
"rsi": 59.743,
"ret": 0.00067843 
},
{
 "date":  -3657,
"name": "GSPC.Close",
"price":  58.98,
"rsi": 60.401,
"ret": -0.00033898 
},
{
 "date":  -3656,
"name": "GSPC.Close",
"price":   59.3,
"rsi": 59.874,
"ret": 0.0054256 
},
{
 "date":  -3655,
"name": "GSPC.Close",
"price":  59.77,
"rsi": 65.118,
"ret": 0.0079258 
},
{
 "date":  -3654,
"name": "GSPC.Close",
"price":  59.89,
"rsi": 71.094,
"ret": 0.0020077 
},
{
 "date":  -3650,
"name": "GSPC.Close",
"price":  59.91,
"rsi": 72.394,
"ret": 0.00033395 
},
{
 "date":  -3649,
"name": "GSPC.Close",
"price":  60.39,
"rsi": 72.615,
"ret": 0.008012 
},
{
 "date":  -3648,
"name": "GSPC.Close",
"price":  60.13,
"rsi": 77.312,
"ret": -0.0043053 
},
{
 "date":  -3647,
"name": "GSPC.Close",
"price":  59.69,
"rsi": 70.281,
"ret": -0.0073175 
},
{
 "date":  -3646,
"name": "GSPC.Close",
"price":   59.5,
"rsi": 60.288,
"ret": -0.0031831 
},
{
 "date":  -3643,
"name": "GSPC.Close",
"price":  58.77,
"rsi": 56.549,
"ret": -0.012269 
},
{
 "date":  -3642,
"name": "GSPC.Close",
"price":  58.41,
"rsi": 45.001,
"ret": -0.0061256 
},
{
 "date":  -3641,
"name": "GSPC.Close",
"price":  58.08,
"rsi": 40.598,
"ret": -0.0056497 
},
{
 "date":  -3640,
"name": "GSPC.Close",
"price":   58.4,
"rsi": 37.022,
"ret": 0.0055096 
},
{
 "date":  -3639,
"name": "GSPC.Close",
"price":  58.38,
"rsi": 42.327,
"ret": -0.00034247 
},
{
 "date":  -3636,
"name": "GSPC.Close",
"price":  57.89,
"rsi": 42.088,
"ret": -0.0083933 
},
{
 "date":  -3635,
"name": "GSPC.Close",
"price":  57.27,
"rsi": 36.639,
"ret": -0.01071 
},
{
 "date":  -3634,
"name": "GSPC.Close",
"price":  57.07,
"rsi": 31.144,
"ret": -0.0034922 
},
{
 "date":  -3633,
"name": "GSPC.Close",
"price":  57.21,
"rsi": 29.601,
"ret": 0.0024531 
},
{
 "date":  -3632,
"name": "GSPC.Close",
"price":  57.38,
"rsi": 32.135,
"ret": 0.0029715 
},
{
 "date":  -3629,
"name": "GSPC.Close",
"price":  56.78,
"rsi": 35.185,
"ret": -0.010457 
},
{
 "date":  -3628,
"name": "GSPC.Close",
"price":  56.86,
"rsi": 30.051,
"ret": 0.0014089 
},
{
 "date":  -3627,
"name": "GSPC.Close",
"price":  56.72,
"rsi": 31.487,
"ret": -0.0024622 
},
{
 "date":  -3626,
"name": "GSPC.Close",
"price":  56.13,
"rsi": 30.314,
"ret": -0.010402 
},
{
 "date":  -3625,
"name": "GSPC.Close",
"price":  55.61,
"rsi": 25.932,
"ret": -0.0092642 
},
{
 "date":  -3622,
"name": "GSPC.Close",
"price":  55.96,
"rsi": 22.803,
"ret": 0.0062938 
},
{
 "date":  -3621,
"name": "GSPC.Close",
"price":  56.82,
"rsi": 29.012,
"ret": 0.015368 
},
{
 "date":  -3620,
"name": "GSPC.Close",
"price":  56.32,
"rsi": 41.468,
"ret": -0.0087997 
},
{
 "date":  -3619,
"name": "GSPC.Close",
"price":  56.27,
"rsi": 37.363,
"ret": -0.00088778 
},
{
 "date":  -3618,
"name": "GSPC.Close",
"price":  55.98,
"rsi": 36.969,
"ret": -0.0051537 
},
{
 "date":  -3615,
"name": "GSPC.Close",
"price":  55.32,
"rsi": 34.684,
"ret": -0.01179 
},
{
 "date":  -3614,
"name": "GSPC.Close",
"price":  55.84,
"rsi": 30.121,
"ret": 0.0093999 
},
{
 "date":  -3613,
"name": "GSPC.Close",
"price":  55.49,
"rsi": 37.138,
"ret": -0.0062679 
},
{
 "date":  -3612,
"name": "GSPC.Close",
"price":  55.18,
"rsi": 34.618,
"ret": -0.0055866 
},
{
 "date":  -3611,
"name": "GSPC.Close",
"price":  55.46,
"rsi": 32.514,
"ret": 0.0050743 
},
{
 "date":  -3608,
"name": "GSPC.Close",
"price":  55.17,
"rsi": 36.281,
"ret": -0.005229 
},
{
 "date":  -3607,
"name": "GSPC.Close",
"price":  54.73,
"rsi": 34.155,
"ret": -0.0079753 
},
{
 "date":  -3606,
"name": "GSPC.Close",
"price":  55.03,
"rsi": 31.169,
"ret": 0.0054815 
},
{
 "date":  -3605,
"name": "GSPC.Close",
"price":   55.8,
"rsi":  35.32,
"ret": 0.013992 
},
{
 "date":  -3604,
"name": "GSPC.Close",
"price":  56.24,
"rsi": 44.562,
"ret": 0.0078853 
},
{
 "date":  -3600,
"name": "GSPC.Close",
"price":  55.94,
"rsi": 49.042,
"ret": -0.0053343 
},
{
 "date":  -3599,
"name": "GSPC.Close",
"price":  55.74,
"rsi": 46.295,
"ret": -0.0035753 
},
{
 "date":  -3598,
"name": "GSPC.Close",
"price":  55.93,
"rsi": 44.505,
"ret": 0.0034087 
},
{
 "date":  -3597,
"name": "GSPC.Close",
"price":  56.16,
"rsi": 46.617,
"ret": 0.0041123 
},
{
 "date":  -3594,
"name": "GSPC.Close",
"price":  56.12,
"rsi":  49.14,
"ret": -0.00071225 
},
{
 "date":  -3593,
"name": "GSPC.Close",
"price":  56.01,
"rsi": 48.709,
"ret": -0.0019601 
},
{
 "date":  -3592,
"name": "GSPC.Close",
"price":  55.62,
"rsi": 47.475,
"ret": -0.006963 
},
{
 "date":  -3591,
"name": "GSPC.Close",
"price":  54.78,
"rsi": 43.289,
"ret": -0.015102 
},
{
 "date":  -3590,
"name": "GSPC.Close",
"price":  54.57,
"rsi": 35.939,
"ret": -0.0038335 
},
{
 "date":  -3587,
"name": "GSPC.Close",
"price":  54.02,
"rsi": 34.368,
"ret": -0.010079 
},
{
 "date":  -3586,
"name": "GSPC.Close",
"price":  53.47,
"rsi": 30.595,
"ret": -0.010181 
},
{
 "date":  -3585,
"name": "GSPC.Close",
"price":  54.04,
"rsi": 27.361,
"ret": 0.01066 
},
{
 "date":  -3584,
"name": "GSPC.Close",
"price":  53.83,
"rsi": 35.027,
"ret": -0.003886 
},
{
 "date":  -3583,
"name": "GSPC.Close",
"price":  54.24,
"rsi": 33.619,
"ret": 0.0076166 
},
{
 "date":  -3580,
"name": "GSPC.Close",
"price":  54.32,
"rsi": 38.791,
"ret": 0.0014749 
},
{
 "date":  -3579,
"name": "GSPC.Close",
"price":  54.74,
"rsi": 39.777,
"ret": 0.007732 
},
{
 "date":  -3578,
"name": "GSPC.Close",
"price":  55.04,
"rsi": 44.804,
"ret": 0.0054805 
},
{
 "date":  -3577,
"name": "GSPC.Close",
"price":  54.96,
"rsi": 48.135,
"ret": -0.0014535 
},
{
 "date":  -3576,
"name": "GSPC.Close",
"price":  55.01,
"rsi": 47.315,
"ret": 0.00090975 
},
{
 "date":  -3573,
"name": "GSPC.Close",
"price":  55.07,
"rsi": 47.912,
"ret": 0.0010907 
},
{
 "date":  -3572,
"name": "GSPC.Close",
"price":  55.29,
"rsi": 48.664,
"ret": 0.0039949 
},
{
 "date":  -3571,
"name": "GSPC.Close",
"price":  55.74,
"rsi": 51.432,
"ret": 0.0081389 
},
{
 "date":  -3570,
"name": "GSPC.Close",
"price":  55.98,
"rsi": 56.589,
"ret": 0.0043057 
},
{
 "date":  -3569,
"name": "GSPC.Close",
"price":  55.98,
"rsi": 59.084,
"ret":      0 
},
{
 "date":  -3566,
"name": "GSPC.Close",
"price":  55.86,
"rsi": 59.084,
"ret": -0.0021436 
},
{
 "date":  -3565,
"name": "GSPC.Close",
"price":  55.78,
"rsi": 57.179,
"ret": -0.0014322 
},
{
 "date":  -3564,
"name": "GSPC.Close",
"price":  55.66,
"rsi": 55.884,
"ret": -0.0021513 
},
{
 "date":  -3563,
"name": "GSPC.Close",
"price":  55.34,
"rsi": 53.913,
"ret": -0.0057492 
},
{
 "date":  -3562,
"name": "GSPC.Close",
"price":  55.43,
"rsi": 48.954,
"ret": 0.0016263 
},
{
 "date":  -3559,
"name": "GSPC.Close",
"price":  55.54,
"rsi": 50.338,
"ret": 0.0019845 
},
{
 "date":  -3558,
"name": "GSPC.Close",
"price":  55.37,
"rsi": 52.048,
"ret": -0.0030609 
},
{
 "date":  -3557,
"name": "GSPC.Close",
"price":  56.51,
"rsi": 49.226,
"ret": 0.020589 
},
{
 "date":  -3556,
"name": "GSPC.Close",
"price":  56.52,
"rsi": 63.514,
"ret": 0.00017696 
},
{
 "date":  -3555,
"name": "GSPC.Close",
"price":  56.39,
"rsi":  63.61,
"ret": -0.0023001 
},
{
 "date":  -3552,
"name": "GSPC.Close",
"price":  56.17,
"rsi": 61.334,
"ret": -0.0039014 
},
{
 "date":  -3551,
"name": "GSPC.Close",
"price":   56.3,
"rsi": 57.578,
"ret": 0.0023144 
},
{
 "date":  -3550,
"name": "GSPC.Close",
"price":   56.3,
"rsi": 59.169,
"ret":      0 
},
{
 "date":  -3549,
"name": "GSPC.Close",
"price":  56.43,
"rsi": 59.169,
"ret": 0.0023091 
},
{
 "date":  -3545,
"name": "GSPC.Close",
"price":  56.59,
"rsi": 60.871,
"ret": 0.0028354 
},
{
 "date":  -3544,
"name": "GSPC.Close",
"price":  56.13,
"rsi":  62.92,
"ret": -0.0081286 
},
{
 "date":  -3543,
"name": "GSPC.Close",
"price":  55.44,
"rsi": 54.143,
"ret": -0.012293 
},
{
 "date":  -3542,
"name": "GSPC.Close",
"price":  55.59,
"rsi": 44.187,
"ret": 0.0027056 
},
{
 "date":  -3541,
"name": "GSPC.Close",
"price":  55.42,
"rsi": 46.491,
"ret": -0.0030581 
},
{
 "date":  -3538,
"name": "GSPC.Close",
"price":  54.86,
"rsi": 44.261,
"ret": -0.010105 
},
{
 "date":  -3537,
"name": "GSPC.Close",
"price":  55.04,
"rsi": 37.825,
"ret": 0.0032811 
},
{
 "date":  -3536,
"name": "GSPC.Close",
"price":  55.04,
"rsi": 40.805,
"ret":      0 
},
{
 "date":  -3535,
"name": "GSPC.Close",
"price":  54.56,
"rsi": 40.805,
"ret": -0.0087209 
},
{
 "date":  -3534,
"name": "GSPC.Close",
"price":  54.37,
"rsi": 35.538,
"ret": -0.0034824 
},
{
 "date":  -3531,
"name": "GSPC.Close",
"price":  54.13,
"rsi": 33.685,
"ret": -0.0044142 
},
{
 "date":  -3530,
"name": "GSPC.Close",
"price":  54.83,
"rsi": 31.453,
"ret": 0.012932 
},
{
 "date":  -3529,
"name": "GSPC.Close",
"price":  55.04,
"rsi": 43.259,
"ret": 0.00383 
},
{
 "date":  -3528,
"name": "GSPC.Close",
"price":  54.86,
"rsi":  46.25,
"ret": -0.0032703 
},
{
 "date":  -3527,
"name": "GSPC.Close",
"price":  54.75,
"rsi": 44.104,
"ret": -0.0020051 
},
{
 "date":  -3524,
"name": "GSPC.Close",
"price":   54.8,
"rsi": 42.797,
"ret": 0.00091324 
},
{
 "date":  -3523,
"name": "GSPC.Close",
"price":  54.42,
"rsi": 43.615,
"ret": -0.0069343 
},
{
 "date":  -3522,
"name": "GSPC.Close",
"price":  54.57,
"rsi": 39.046,
"ret": 0.0027563 
},
{
 "date":  -3521,
"name": "GSPC.Close",
"price":  54.85,
"rsi": 41.645,
"ret": 0.005131 
},
{
 "date":  -3520,
"name": "GSPC.Close",
"price":   55.3,
"rsi": 46.252,
"ret": 0.0082042 
},
{
 "date":  -3517,
"name": "GSPC.Close",
"price":  55.25,
"rsi": 52.712,
"ret": -0.00090416 
},
{
 "date":  -3516,
"name": "GSPC.Close",
"price":  55.46,
"rsi": 51.965,
"ret": 0.0038009 
},
{
 "date":  -3515,
"name": "GSPC.Close",
"price":  55.44,
"rsi":  54.86,
"ret": -0.00036062 
},
{
 "date":  -3514,
"name": "GSPC.Close",
"price":  55.68,
"rsi": 54.523,
"ret": 0.004329 
},
{
 "date":  -3513,
"name": "GSPC.Close",
"price":  55.73,
"rsi": 57.868,
"ret": 0.00089799 
},
{
 "date":  -3510,
"name": "GSPC.Close",
"price":  55.76,
"rsi": 58.552,
"ret": 0.00053831 
},
{
 "date":  -3509,
"name": "GSPC.Close",
"price":   55.7,
"rsi": 58.982,
"ret": -0.001076 
},
{
 "date":  -3508,
"name": "GSPC.Close",
"price":  55.67,
"rsi": 57.692,
"ret": -0.0005386 
},
{
 "date":  -3507,
"name": "GSPC.Close",
"price":  55.71,
"rsi": 57.021,
"ret": 0.00071852 
},
{
 "date":  -3506,
"name": "GSPC.Close",
"price":  55.74,
"rsi": 57.727,
"ret": 0.0005385 
},
{
 "date":  -3502,
"name": "GSPC.Close",
"price":  55.83,
"rsi": 58.281,
"ret": 0.0016146 
},
{
 "date":  -3501,
"name": "GSPC.Close",
"price":  55.89,
"rsi": 59.976,
"ret": 0.0010747 
},
{
 "date":  -3500,
"name": "GSPC.Close",
"price":  56.13,
"rsi":  61.11,
"ret": 0.0042941 
},
{
 "date":  -3499,
"name": "GSPC.Close",
"price":  56.23,
"rsi":  65.34,
"ret": 0.0017816 
},
{
 "date":  -3496,
"name": "GSPC.Close",
"price":  56.89,
"rsi": 66.953,
"ret": 0.011738 
},
{
 "date":  -3495,
"name": "GSPC.Close",
"price":  57.43,
"rsi": 75.167,
"ret": 0.009492 
},
{
 "date":  -3494,
"name": "GSPC.Close",
"price":  57.89,
"rsi": 79.628,
"ret": 0.0080098 
},
{
 "date":  -3493,
"name": "GSPC.Close",
"price":     58,
"rsi": 82.511,
"ret": 0.0019002 
},
{
 "date":  -3492,
"name": "GSPC.Close",
"price":  57.97,
"rsi": 83.126,
"ret": -0.00051724 
},
{
 "date":  -3489,
"name": "GSPC.Close",
"price":  57.99,
"rsi": 82.276,
"ret": 0.00034501 
},
{
 "date":  -3488,
"name": "GSPC.Close",
"price":  57.91,
"rsi": 82.405,
"ret": -0.0013795 
},
{
 "date":  -3487,
"name": "GSPC.Close",
"price":  57.57,
"rsi": 79.898,
"ret": -0.0058712 
},
{
 "date":  -3486,
"name": "GSPC.Close",
"price":   57.5,
"rsi": 70.132,
"ret": -0.0012159 
},
{
 "date":  -3485,
"name": "GSPC.Close",
"price":  57.44,
"rsi": 68.282,
"ret": -0.0010435 
},
{
 "date":  -3482,
"name": "GSPC.Close",
"price":  57.16,
"rsi": 66.658,
"ret": -0.0048747 
},
{
 "date":  -3481,
"name": "GSPC.Close",
"price":  57.11,
"rsi": 59.543,
"ret": -0.00087474 
},
{
 "date":  -3480,
"name": "GSPC.Close",
"price":  57.28,
"rsi": 58.346,
"ret": 0.0029767 
},
{
 "date":  -3479,
"name": "GSPC.Close",
"price":  57.59,
"rsi": 61.203,
"ret": 0.005412 
},
{
 "date":  -3478,
"name": "GSPC.Close",
"price":  57.68,
"rsi": 65.809,
"ret": 0.0015628 
},
{
 "date":  -3475,
"name": "GSPC.Close",
"price":  57.33,
"rsi": 67.032,
"ret": -0.006068 
},
{
 "date":  -3474,
"name": "GSPC.Close",
"price":  56.94,
"rsi": 58.295,
"ret": -0.0068027 
},
{
 "date":  -3473,
"name": "GSPC.Close",
"price":  56.94,
"rsi":  50.41,
"ret":      0 
},
{
 "date":  -3472,
"name": "GSPC.Close",
"price":  56.92,
"rsi":  50.41,
"ret": -0.00035125 
},
{
 "date":  -3471,
"name": "GSPC.Close",
"price":  57.06,
"rsi": 50.008,
"ret": 0.0024596 
},
{
 "date":  -3467,
"name": "GSPC.Close",
"price":  57.02,
"rsi": 52.845,
"ret": -0.00070102 
},
{
 "date":  -3466,
"name": "GSPC.Close",
"price":  56.94,
"rsi": 51.938,
"ret": -0.001403 
},
{
 "date":  -3465,
"name": "GSPC.Close",
"price":  57.24,
"rsi": 50.087,
"ret": 0.0052687 
},
{
 "date":  -3464,
"name": "GSPC.Close",
"price":  57.38,
"rsi": 56.367,
"ret": 0.0024458 
},
{
 "date":  -3461,
"name": "GSPC.Close",
"price":  56.87,
"rsi": 58.962,
"ret": -0.0088881 
},
{
 "date":  -3460,
"name": "GSPC.Close",
"price":  56.25,
"rsi": 47.807,
"ret": -0.010902 
},
{
 "date":  -3459,
"name": "GSPC.Close",
"price":   56.1,
"rsi": 38.317,
"ret": -0.0026667 
},
{
 "date":  -3458,
"name": "GSPC.Close",
"price":  56.12,
"rsi": 36.432,
"ret": 0.00035651 
},
{
 "date":  -3457,
"name": "GSPC.Close",
"price":  56.05,
"rsi": 36.878,
"ret": -0.0012473 
},
{
 "date":  -3454,
"name": "GSPC.Close",
"price":   55.7,
"rsi": 35.928,
"ret": -0.0062444 
},
{
 "date":  -3453,
"name": "GSPC.Close",
"price":   55.7,
"rsi": 31.553,
"ret":      0 
},
{
 "date":  -3452,
"name": "GSPC.Close",
"price":  55.61,
"rsi": 31.553,
"ret": -0.0016158 
},
{
 "date":  -3451,
"name": "GSPC.Close",
"price":   55.1,
"rsi": 30.448,
"ret": -0.009171 
},
{
 "date":  -3450,
"name": "GSPC.Close",
"price":  54.72,
"rsi": 25.084,
"ret": -0.0068966 
},
{
 "date":  -3447,
"name": "GSPC.Close",
"price":  54.18,
"rsi": 21.977,
"ret": -0.0098684 
},
{
 "date":  -3446,
"name": "GSPC.Close",
"price":  54.51,
"rsi": 18.475,
"ret": 0.0060908 
},
{
 "date":  -3445,
"name": "GSPC.Close",
"price":  54.17,
"rsi": 26.213,
"ret": -0.0062374 
},
{
 "date":  -3444,
"name": "GSPC.Close",
"price":  54.57,
"rsi": 23.715,
"ret": 0.0073842 
},
{
 "date":  -3443,
"name": "GSPC.Close",
"price":  55.51,
"rsi": 31.932,
"ret": 0.017226 
},
{
 "date":  -3440,
"name": "GSPC.Close",
"price":  55.53,
"rsi": 46.512,
"ret": 0.0003603 
},
{
 "date":  -3439,
"name": "GSPC.Close",
"price":  55.04,
"rsi": 46.774,
"ret": -0.0088241 
},
{
 "date":  -3438,
"name": "GSPC.Close",
"price":  54.72,
"rsi": 41.434,
"ret": -0.005814 
},
{
 "date":  -3437,
"name": "GSPC.Close",
"price":  54.89,
"rsi": 38.355,
"ret": 0.0031067 
},
{
 "date":  -3436,
"name": "GSPC.Close",
"price":  55.44,
"rsi": 40.869,
"ret": 0.01002 
},
{
 "date":  -3433,
"name": "GSPC.Close",
"price":  55.52,
"rsi": 48.226,
"ret": 0.001443 
},
{
 "date":  -3432,
"name": "GSPC.Close",
"price":  55.84,
"rsi": 49.216,
"ret": 0.0057637 
},
{
 "date":  -3431,
"name": "GSPC.Close",
"price":  56.07,
"rsi":  53.08,
"ret": 0.0041189 
},
{
 "date":  -3430,
"name": "GSPC.Close",
"price":  56.28,
"rsi": 55.689,
"ret": 0.0037453 
},
{
 "date":  -3429,
"name": "GSPC.Close",
"price":  56.66,
"rsi": 57.987,
"ret": 0.006752 
},
{
 "date":  -3426,
"name": "GSPC.Close",
"price":  56.61,
"rsi": 61.842,
"ret": -0.00088246 
},
{
 "date":  -3425,
"name": "GSPC.Close",
"price":  56.72,
"rsi": 61.048,
"ret": 0.0019431 
},
{
 "date":  -3424,
"name": "GSPC.Close",
"price":  56.84,
"rsi": 62.198,
"ret": 0.0021157 
},
{
 "date":  -3423,
"name": "GSPC.Close",
"price":  56.81,
"rsi": 63.465,
"ret": -0.0005278 
},
{
 "date":  -3422,
"name": "GSPC.Close",
"price":  57.01,
"rsi": 62.898,
"ret": 0.0035205 
},
{
 "date":  -3419,
"name": "GSPC.Close",
"price":  57.19,
"rsi": 65.136,
"ret": 0.0031573 
},
{
 "date":  -3418,
"name": "GSPC.Close",
"price":  57.75,
"rsi": 67.062,
"ret": 0.0097919 
},
{
 "date":  -3417,
"name": "GSPC.Close",
"price":  58.07,
"rsi": 72.206,
"ret": 0.0055411 
},
{
 "date":  -3416,
"name": "GSPC.Close",
"price":  57.79,
"rsi": 74.643,
"ret": -0.0048218 
},
{
 "date":  -3415,
"name": "GSPC.Close",
"price":   57.6,
"rsi": 68.946,
"ret": -0.0032878 
},
{
 "date":  -3412,
"name": "GSPC.Close",
"price":  57.44,
"rsi": 65.304,
"ret": -0.0027778 
},
{
 "date":  -3411,
"name": "GSPC.Close",
"price":  56.84,
"rsi": 62.319,
"ret": -0.010446 
},
{
 "date":  -3410,
"name": "GSPC.Close",
"price":  56.96,
"rsi": 52.607,
"ret": 0.0021112 
},
{
 "date":  -3409,
"name": "GSPC.Close",
"price":  57.09,
"rsi": 54.146,
"ret": 0.0022823 
},
{
 "date":  -3408,
"name": "GSPC.Close",
"price":     57,
"rsi":  55.82,
"ret": -0.0015765 
},
{
 "date":  -3404,
"name": "GSPC.Close",
"price":  56.49,
"rsi": 54.341,
"ret": -0.0089474 
},
{
 "date":  -3403,
"name": "GSPC.Close",
"price":  55.79,
"rsi": 46.777,
"ret": -0.012392 
},
{
 "date":  -3402,
"name": "GSPC.Close",
"price":  55.74,
"rsi": 38.795,
"ret": -0.00089622 
},
{
 "date":  -3401,
"name": "GSPC.Close",
"price":  56.11,
"rsi": 38.292,
"ret": 0.006638 
},
{
 "date":  -3398,
"name": "GSPC.Close",
"price":  55.72,
"rsi": 44.067,
"ret": -0.0069506 
},
{
 "date":  -3397,
"name": "GSPC.Close",
"price":  55.83,
"rsi": 39.836,
"ret": 0.0019742 
},
{
 "date":  -3396,
"name": "GSPC.Close",
"price":  55.44,
"rsi": 41.541,
"ret": -0.0069855 
},
{
 "date":  -3395,
"name": "GSPC.Close",
"price":  55.22,
"rsi": 37.484,
"ret": -0.0039683 
},
{
 "date":  -3394,
"name": "GSPC.Close",
"price":  55.11,
"rsi": 35.385,
"ret": -0.001992 
},
{
 "date":  -3391,
"name": "GSPC.Close",
"price":  53.86,
"rsi":  34.35,
"ret": -0.022682 
},
{
 "date":  -3390,
"name": "GSPC.Close",
"price":  54.01,
"rsi":  25.29,
"ret": 0.002785 
},
{
 "date":  -3389,
"name": "GSPC.Close",
"price":  54.57,
"rsi": 27.753,
"ret": 0.010368 
},
{
 "date":  -3388,
"name": "GSPC.Close",
"price":  54.36,
"rsi": 36.206,
"ret": -0.0038483 
},
{
 "date":  -3387,
"name": "GSPC.Close",
"price":   53.9,
"rsi": 34.573,
"ret": -0.0084621 
},
{
 "date":  -3384,
"name": "GSPC.Close",
"price":  53.06,
"rsi": 31.247,
"ret": -0.015584 
},
{
 "date":  -3383,
"name": "GSPC.Close",
"price":  52.94,
"rsi": 26.276,
"ret": -0.0022616 
},
{
 "date":  -3382,
"name": "GSPC.Close",
"price":  52.48,
"rsi": 25.648,
"ret": -0.0086891 
},
{
 "date":  -3381,
"name": "GSPC.Close",
"price":  52.62,
"rsi": 23.346,
"ret": 0.0026677 
},
{
 "date":  -3380,
"name": "GSPC.Close",
"price":  53.52,
"rsi": 25.537,
"ret": 0.017104 
},
{
 "date":  -3377,
"name": "GSPC.Close",
"price":  53.36,
"rsi": 37.837,
"ret": -0.0029895 
},
{
 "date":  -3376,
"name": "GSPC.Close",
"price":  52.99,
"rsi": 36.677,
"ret": -0.006934 
},
{
 "date":  -3375,
"name": "GSPC.Close",
"price":  53.39,
"rsi": 34.076,
"ret": 0.0075486 
},
{
 "date":  -3374,
"name": "GSPC.Close",
"price":  53.72,
"rsi": 39.104,
"ret": 0.0061809 
},
{
 "date":  -3373,
"name": "GSPC.Close",
"price":  54.03,
"rsi":  42.97,
"ret": 0.0057707 
},
{
 "date":  -3370,
"name": "GSPC.Close",
"price":  54.14,
"rsi": 46.411,
"ret": 0.0020359 
},
{
 "date":  -3369,
"name": "GSPC.Close",
"price":  54.22,
"rsi": 47.618,
"ret": 0.0014777 
},
{
 "date":  -3368,
"name": "GSPC.Close",
"price":  54.15,
"rsi": 48.527,
"ret": -0.001291 
},
{
 "date":  -3367,
"name": "GSPC.Close",
"price":  54.57,
"rsi": 47.746,
"ret": 0.0077562 
},
{
 "date":  -3366,
"name": "GSPC.Close",
"price":  54.86,
"rsi": 52.665,
"ret": 0.0053143 
},
{
 "date":  -3363,
"name": "GSPC.Close",
"price":  54.63,
"rsi": 55.762,
"ret": -0.0041925 
},
{
 "date":  -3362,
"name": "GSPC.Close",
"price":  54.35,
"rsi": 52.811,
"ret": -0.0051254 
},
{
 "date":  -3361,
"name": "GSPC.Close",
"price":  54.25,
"rsi": 49.385,
"ret": -0.0018399 
},
{
 "date":  -3360,
"name": "GSPC.Close",
"price":  53.86,
"rsi": 48.183,
"ret": -0.0071889 
},
{
 "date":  -3359,
"name": "GSPC.Close",
"price":  53.72,
"rsi": 43.713,
"ret": -0.0025993 
},
{
 "date":  -3356,
"name": "GSPC.Close",
"price":   52.7,
"rsi":   42.2,
"ret": -0.018987 
},
{
 "date":  -3355,
"name": "GSPC.Close",
"price":   52.2,
"rsi": 33.186,
"ret": -0.0094877 
},
{
 "date":  -3354,
"name": "GSPC.Close",
"price":  53.05,
"rsi": 29.823,
"ret": 0.016284 
},
{
 "date":  -3353,
"name": "GSPC.Close",
"price":  53.62,
"rsi": 40.805,
"ret": 0.010745 
},
{
 "date":  -3352,
"name": "GSPC.Close",
"price":  53.41,
"rsi": 46.815,
"ret": -0.0039164 
},
{
 "date":  -3349,
"name": "GSPC.Close",
"price":  53.39,
"rsi": 45.002,
"ret": -0.00037446 
},
{
 "date":  -3348,
"name": "GSPC.Close",
"price":  53.94,
"rsi": 44.824,
"ret": 0.010302 
},
{
 "date":  -3347,
"name": "GSPC.Close",
"price":  54.22,
"rsi": 50.611,
"ret": 0.005191 
},
{
 "date":  -3346,
"name": "GSPC.Close",
"price":  54.43,
"rsi": 53.296,
"ret": 0.0038731 
},
{
 "date":  -3345,
"name": "GSPC.Close",
"price":   54.9,
"rsi": 55.261,
"ret": 0.0086349 
},
{
 "date":  -3342,
"name": "GSPC.Close",
"price":  55.11,
"rsi":  59.38,
"ret": 0.0038251 
},
{
 "date":  -3340,
"name": "GSPC.Close",
"price":  55.35,
"rsi": 61.103,
"ret": 0.0043549 
},
{
 "date":  -3339,
"name": "GSPC.Close",
"price":  56.43,
"rsi": 63.033,
"ret": 0.019512 
},
{
 "date":  -3338,
"name": "GSPC.Close",
"price":  55.87,
"rsi": 70.199,
"ret": -0.0099238 
},
{
 "date":  -3335,
"name": "GSPC.Close",
"price":  55.59,
"rsi": 63.342,
"ret": -0.0050116 
},
{
 "date":  -3334,
"name": "GSPC.Close",
"price":  55.81,
"rsi": 60.178,
"ret": 0.0039575 
},
{
 "date":  -3333,
"name": "GSPC.Close",
"price":   55.7,
"rsi": 61.793,
"ret": -0.001971 
},
{
 "date":  -3332,
"name": "GSPC.Close",
"price":  55.55,
"rsi": 60.472,
"ret": -0.002693 
},
{
 "date":  -3331,
"name": "GSPC.Close",
"price":  55.82,
"rsi": 58.632,
"ret": 0.0048605 
},
{
 "date":  -3328,
"name": "GSPC.Close",
"price":  55.93,
"rsi": 60.936,
"ret": 0.0019706 
},
{
 "date":  -3327,
"name": "GSPC.Close",
"price":  55.72,
"rsi": 61.868,
"ret": -0.0037547 
},
{
 "date":  -3326,
"name": "GSPC.Close",
"price":   55.8,
"rsi": 58.975,
"ret": 0.0014358 
},
{
 "date":  -3324,
"name": "GSPC.Close",
"price":  56.13,
"rsi": 59.748,
"ret": 0.005914 
},
{
 "date":  -3321,
"name": "GSPC.Close",
"price":  56.03,
"rsi": 62.853,
"ret": -0.0017816 
},
{
 "date":  -3320,
"name": "GSPC.Close",
"price":  55.83,
"rsi":  61.31,
"ret": -0.0035695 
},
{
 "date":  -3319,
"name": "GSPC.Close",
"price":  55.54,
"rsi": 58.229,
"ret": -0.0051943 
},
{
 "date":  -3318,
"name": "GSPC.Close",
"price":   55.3,
"rsi": 53.993,
"ret": -0.0043212 
},
{
 "date":  -3317,
"name": "GSPC.Close",
"price":  55.39,
"rsi": 50.705,
"ret": 0.0016275 
},
{
 "date":  -3314,
"name": "GSPC.Close",
"price":  55.31,
"rsi": 51.888,
"ret": -0.0014443 
},
{
 "date":  -3313,
"name": "GSPC.Close",
"price":  55.47,
"rsi": 50.723,
"ret": 0.0028928 
},
{
 "date":  -3312,
"name": "GSPC.Close",
"price":  56.02,
"rsi": 52.997,
"ret": 0.0099153 
},
{
 "date":  -3311,
"name": "GSPC.Close",
"price":  56.15,
"rsi": 59.854,
"ret": 0.0023206 
},
{
 "date":  -3310,
"name": "GSPC.Close",
"price":  56.65,
"rsi": 61.291,
"ret": 0.0089047 
},
{
 "date":  -3307,
"name": "GSPC.Close",
"price":  56.85,
"rsi": 66.291,
"ret": 0.0035305 
},
{
 "date":  -3306,
"name": "GSPC.Close",
"price":  56.88,
"rsi": 68.067,
"ret": 0.0005277 
},
{
 "date":  -3305,
"name": "GSPC.Close",
"price":  56.84,
"rsi": 68.337,
"ret": -0.00070323 
},
{
 "date":  -3304,
"name": "GSPC.Close",
"price":  56.68,
"rsi": 67.519,
"ret": -0.0028149 
},
{
 "date":  -3303,
"name": "GSPC.Close",
"price":   57.2,
"rsi": 64.206,
"ret": 0.0091743 
},
{
 "date":  -3300,
"name": "GSPC.Close",
"price":  57.13,
"rsi": 69.452,
"ret": -0.0012238 
},
{
 "date":  -3299,
"name": "GSPC.Close",
"price":  57.09,
"rsi": 68.007,
"ret": -0.00070016 
},
{
 "date":  -3298,
"name": "GSPC.Close",
"price":  57.55,
"rsi": 67.147,
"ret": 0.0080575 
},
{
 "date":  -3297,
"name": "GSPC.Close",
"price":  57.39,
"rsi": 71.594,
"ret": -0.0027802 
},
{
 "date":  -3296,
"name": "GSPC.Close",
"price":  57.44,
"rsi": 68.139,
"ret": 0.00087123 
},
{
 "date":  -3292,
"name": "GSPC.Close",
"price":  57.52,
"rsi": 68.648,
"ret": 0.0013928 
},
{
 "date":  -3291,
"name": "GSPC.Close",
"price":  57.78,
"rsi": 69.488,
"ret": 0.0045202 
},
{
 "date":  -3290,
"name": "GSPC.Close",
"price":  58.05,
"rsi": 72.105,
"ret": 0.0046729 
},
{
 "date":  -3289,
"name": "GSPC.Close",
"price":  58.11,
"rsi": 74.546,
"ret": 0.0010336 
},
{
 "date":  -3285,
"name": "GSPC.Close",
"price":  57.57,
"rsi": 75.068,
"ret": -0.0092927 
},
{
 "date":  -3284,
"name": "GSPC.Close",
"price":  58.36,
"rsi": 62.619,
"ret": 0.013722 
},
{
 "date":  -3283,
"name": "GSPC.Close",
"price":  58.57,
"rsi": 70.362,
"ret": 0.0035984 
},
{
 "date":  -3282,
"name": "GSPC.Close",
"price":   58.4,
"rsi": 72.022,
"ret": -0.0029025 
},
{
 "date":  -3279,
"name": "GSPC.Close",
"price":  58.81,
"rsi":  68.67,
"ret": 0.0070205 
},
{
 "date":  -3278,
"name": "GSPC.Close",
"price":  58.97,
"rsi": 72.048,
"ret": 0.0027206 
},
{
 "date":  -3277,
"name": "GSPC.Close",
"price":  59.14,
"rsi":  73.26,
"ret": 0.0028828 
},
{
 "date":  -3276,
"name": "GSPC.Close",
"price":  59.32,
"rsi": 74.524,
"ret": 0.0030436 
},
{
 "date":  -3275,
"name": "GSPC.Close",
"price":   59.6,
"rsi": 75.827,
"ret": 0.0047202 
},
{
 "date":  -3272,
"name": "GSPC.Close",
"price":  59.58,
"rsi": 77.734,
"ret": -0.00033557 
},
{
 "date":  -3271,
"name": "GSPC.Close",
"price":  59.64,
"rsi": 77.265,
"ret": 0.001007 
},
{
 "date":  -3270,
"name": "GSPC.Close",
"price":  59.68,
"rsi":   77.7,
"ret": 0.00067069 
},
{
 "date":  -3269,
"name": "GSPC.Close",
"price":  59.77,
"rsi": 78.001,
"ret": 0.001508 
},
{
 "date":  -3268,
"name": "GSPC.Close",
"price":  59.96,
"rsi":   78.7,
"ret": 0.0031789 
},
{
 "date":  -3265,
"name": "GSPC.Close",
"price":  60.29,
"rsi": 80.135,
"ret": 0.0055037 
},
{
 "date":  -3264,
"name": "GSPC.Close",
"price":  60.45,
"rsi": 82.358,
"ret": 0.0026538 
},
{
 "date":  -3263,
"name": "GSPC.Close",
"price":  60.53,
"rsi": 83.331,
"ret": 0.0013234 
},
{
 "date":  -3262,
"name": "GSPC.Close",
"price":  60.62,
"rsi": 83.812,
"ret": 0.0014869 
},
{
 "date":  -3261,
"name": "GSPC.Close",
"price":  61.24,
"rsi": 84.359,
"ret": 0.010228 
},
{
 "date":  -3258,
"name": "GSPC.Close",
"price":  61.97,
"rsi": 87.494,
"ret": 0.01192 
},
{
 "date":  -3257,
"name": "GSPC.Close",
"price":  61.78,
"rsi": 90.028,
"ret": -0.003066 
},
{
 "date":  -3256,
"name": "GSPC.Close",
"price":   61.9,
"rsi":  85.19,
"ret": 0.0019424 
},
{
 "date":  -3255,
"name": "GSPC.Close",
"price":   62.3,
"rsi": 85.712,
"ret": 0.006462 
},
{
 "date":  -3254,
"name": "GSPC.Close",
"price":  62.22,
"rsi": 87.318,
"ret": -0.0012841 
},
{
 "date":  -3251,
"name": "GSPC.Close",
"price":  61.76,
"rsi": 85.254,
"ret": -0.0073931 
},
{
 "date":  -3250,
"name": "GSPC.Close",
"price":  61.65,
"rsi": 74.371,
"ret": -0.0017811 
},
{
 "date":  -3249,
"name": "GSPC.Close",
"price":  62.21,
"rsi": 72.004,
"ret": 0.0090835 
},
{
 "date":  -3248,
"name": "GSPC.Close",
"price":  62.02,
"rsi": 76.164,
"ret": -0.0030542 
},
{
 "date":  -3247,
"name": "GSPC.Close",
"price":   61.5,
"rsi": 72.242,
"ret": -0.0083844 
},
{
 "date":  -3244,
"name": "GSPC.Close",
"price":  61.14,
"rsi": 62.723,
"ret": -0.0058537 
},
{
 "date":  -3243,
"name": "GSPC.Close",
"price":  61.41,
"rsi": 57.112,
"ret": 0.0044161 
},
{
 "date":  -3242,
"name": "GSPC.Close",
"price":  61.92,
"rsi": 60.002,
"ret": 0.0083048 
},
{
 "date":  -3241,
"name": "GSPC.Close",
"price":   62.3,
"rsi": 64.824,
"ret": 0.006137 
},
{
 "date":  -3240,
"name": "GSPC.Close",
"price":   62.1,
"rsi": 67.926,
"ret": -0.0032103 
},
{
 "date":  -3237,
"name": "GSPC.Close",
"price":  62.32,
"rsi": 64.692,
"ret": 0.0035427 
},
{
 "date":  -3236,
"name": "GSPC.Close",
"price":  62.36,
"rsi": 66.577,
"ret": 0.00064185 
},
{
 "date":  -3234,
"name": "GSPC.Close",
"price":  62.59,
"rsi": 66.923,
"ret": 0.0036883 
},
{
 "date":  -3233,
"name": "GSPC.Close",
"price":  62.84,
"rsi": 68.914,
"ret": 0.0039942 
},
{
 "date":  -3230,
"name": "GSPC.Close",
"price":   63.3,
"rsi": 70.961,
"ret": 0.0073202 
},
{
 "date":  -3229,
"name": "GSPC.Close",
"price":  63.44,
"rsi": 74.312,
"ret": 0.0022117 
},
{
 "date":  -3228,
"name": "GSPC.Close",
"price":  63.43,
"rsi": 75.248,
"ret": -0.00015763 
},
{
 "date":  -3227,
"name": "GSPC.Close",
"price":  63.85,
"rsi": 75.038,
"ret": 0.0066215 
},
{
 "date":  -3226,
"name": "GSPC.Close",
"price":  63.95,
"rsi":  77.84,
"ret": 0.0015662 
},
{
 "date":  -3223,
"name": "GSPC.Close",
"price":  64.05,
"rsi":  78.46,
"ret": 0.0015637 
},
{
 "date":  -3222,
"name": "GSPC.Close",
"price":  63.47,
"rsi":  79.09,
"ret": -0.0090554 
},
{
 "date":  -3221,
"name": "GSPC.Close",
"price":  63.44,
"rsi": 66.873,
"ret": -0.00047266 
},
{
 "date":  -3220,
"name": "GSPC.Close",
"price":   63.5,
"rsi": 66.302,
"ret": 0.00094578 
},
{
 "date":  -3219,
"name": "GSPC.Close",
"price":  63.48,
"rsi":  66.91,
"ret": -0.00031496 
},
{
 "date":  -3216,
"name": "GSPC.Close",
"price":  63.66,
"rsi":  66.48,
"ret": 0.0028355 
},
{
 "date":  -3215,
"name": "GSPC.Close",
"price":  63.38,
"rsi": 68.448,
"ret": -0.0043984 
},
{
 "date":  -3214,
"name": "GSPC.Close",
"price":  63.57,
"rsi": 62.319,
"ret": 0.0029978 
},
{
 "date":  -3213,
"name": "GSPC.Close",
"price":  64.21,
"rsi": 64.633,
"ret": 0.010068 
},
{
 "date":  -3212,
"name": "GSPC.Close",
"price":     64,
"rsi": 71.077,
"ret": -0.0032705 
},
{
 "date":  -3209,
"name": "GSPC.Close",
"price":  64.86,
"rsi": 66.777,
"ret": 0.013437 
},
{
 "date":  -3208,
"name": "GSPC.Close",
"price":  64.74,
"rsi": 73.774,
"ret": -0.0018501 
},
{
 "date":  -3207,
"name": "GSPC.Close",
"price":   64.7,
"rsi": 71.511,
"ret": -0.00061786 
},
{
 "date":  -3206,
"name": "GSPC.Close",
"price":  64.53,
"rsi": 70.732,
"ret": -0.0026275 
},
{
 "date":  -3205,
"name": "GSPC.Close",
"price":  64.42,
"rsi": 67.373,
"ret": -0.0017046 
},
{
 "date":  -3202,
"name": "GSPC.Close",
"price":  64.35,
"rsi": 65.216,
"ret": -0.0010866 
},
{
 "date":  -3201,
"name": "GSPC.Close",
"price":  64.38,
"rsi": 63.815,
"ret": 0.0004662 
},
{
 "date":  -3200,
"name": "GSPC.Close",
"price":  64.93,
"rsi":  64.17,
"ret": 0.008543 
},
{
 "date":  -3199,
"name": "GSPC.Close",
"price":  65.06,
"rsi": 69.987,
"ret": 0.0020022 
},
{
 "date":  -3195,
"name": "GSPC.Close",
"price":   65.6,
"rsi": 71.178,
"ret": 0.0083 
},
{
 "date":  -3194,
"name": "GSPC.Close",
"price":  65.66,
"rsi": 75.523,
"ret": 0.00091463 
},
{
 "date":  -3193,
"name": "GSPC.Close",
"price":  65.46,
"rsi": 75.956,
"ret": -0.003046 
},
{
 "date":  -3192,
"name": "GSPC.Close",
"price":  65.61,
"rsi": 71.414,
"ret": 0.0022915 
},
{
 "date":  -3191,
"name": "GSPC.Close",
"price":  65.96,
"rsi": 72.731,
"ret": 0.0053346 
},
{
 "date":  -3188,
"name": "GSPC.Close",
"price":  66.53,
"rsi": 75.561,
"ret": 0.0086416 
},
{
 "date":  -3187,
"name": "GSPC.Close",
"price":  66.62,
"rsi": 79.324,
"ret": 0.0013528 
},
{
 "date":  -3186,
"name": "GSPC.Close",
"price":  66.31,
"rsi": 79.851,
"ret": -0.0046533 
},
{
 "date":  -3185,
"name": "GSPC.Close",
"price":  66.26,
"rsi": 72.947,
"ret": -0.00075403 
},
{
 "date":  -3184,
"name": "GSPC.Close",
"price":  66.37,
"rsi": 71.868,
"ret": 0.0016601 
},
{
 "date":  -3181,
"name": "GSPC.Close",
"price":  68.68,
"rsi": 72.821,
"ret": 0.034805 
},
{
 "date":  -3180,
"name": "GSPC.Close",
"price":   66.2,
"rsi": 84.609,
"ret": -0.036109 
},
{
 "date":  -3179,
"name": "GSPC.Close",
"price":  65.81,
"rsi": 56.351,
"ret": -0.0058912 
},
{
 "date":  -3178,
"name": "GSPC.Close",
"price":  65.82,
"rsi": 53.335,
"ret": 0.00015195 
},
{
 "date":  -3177,
"name": "GSPC.Close",
"price":  65.77,
"rsi": 53.404,
"ret": -0.00075965 
},
{
 "date":  -3174,
"name": "GSPC.Close",
"price":   64.4,
"rsi": 52.983,
"ret": -0.02083 
},
{
 "date":  -3173,
"name": "GSPC.Close",
"price":   65.3,
"rsi": 42.982,
"ret": 0.013975 
},
{
 "date":  -3172,
"name": "GSPC.Close",
"price":  65.55,
"rsi": 49.699,
"ret": 0.0038285 
},
{
 "date":  -3171,
"name": "GSPC.Close",
"price":  65.46,
"rsi": 51.411,
"ret": -0.001373 
},
{
 "date":  -3170,
"name": "GSPC.Close",
"price":  65.31,
"rsi": 50.742,
"ret": -0.0022915 
},
{
 "date":  -3167,
"name": "GSPC.Close",
"price":  65.17,
"rsi": 49.582,
"ret": -0.0021436 
},
{
 "date":  -3166,
"name": "GSPC.Close",
"price":  65.64,
"rsi": 48.469,
"ret": 0.0072119 
},
{
 "date":  -3165,
"name": "GSPC.Close",
"price":  66.18,
"rsi": 52.337,
"ret": 0.0082267 
},
{
 "date":  -3164,
"name": "GSPC.Close",
"price":  66.44,
"rsi": 56.388,
"ret": 0.0039287 
},
{
 "date":  -3163,
"name": "GSPC.Close",
"price":  66.52,
"rsi": 58.229,
"ret": 0.0012041 
},
{
 "date":  -3160,
"name": "GSPC.Close",
"price":  66.41,
"rsi": 58.805,
"ret": -0.0016536 
},
{
 "date":  -3159,
"name": "GSPC.Close",
"price":  66.47,
"rsi": 57.628,
"ret": 0.00090348 
},
{
 "date":  -3158,
"name": "GSPC.Close",
"price":  66.41,
"rsi":  58.12,
"ret": -0.00090266 
},
{
 "date":  -3157,
"name": "GSPC.Close",
"price":  66.39,
"rsi": 57.402,
"ret": -0.00030116 
},
{
 "date":  -3156,
"name": "GSPC.Close",
"price":   66.5,
"rsi": 57.148,
"ret": 0.0016569 
},
{
 "date":  -3153,
"name": "GSPC.Close",
"price":  66.83,
"rsi": 58.241,
"ret": 0.0049624 
},
{
 "date":  -3152,
"name": "GSPC.Close",
"price":  67.08,
"rsi": 61.419,
"ret": 0.0037408 
},
{
 "date":  -3151,
"name": "GSPC.Close",
"price":  67.39,
"rsi": 63.674,
"ret": 0.0046213 
},
{
 "date":  -3150,
"name": "GSPC.Close",
"price":  66.99,
"rsi": 66.305,
"ret": -0.0059356 
},
{
 "date":  -3149,
"name": "GSPC.Close",
"price":  67.27,
"rsi": 60.243,
"ret": 0.0041797 
},
{
 "date":  -3146,
"name": "GSPC.Close",
"price":  66.85,
"rsi": 62.806,
"ret": -0.0062435 
},
{
 "date":  -3145,
"name": "GSPC.Close",
"price":  66.68,
"rsi": 56.882,
"ret": -0.002543 
},
{
 "date":  -3144,
"name": "GSPC.Close",
"price":  66.26,
"rsi": 54.635,
"ret": -0.0062987 
},
{
 "date":  -3143,
"name": "GSPC.Close",
"price":  66.01,
"rsi":  49.44,
"ret": -0.003773 
},
{
 "date":  -3142,
"name": "GSPC.Close",
"price":  66.43,
"rsi":   46.6,
"ret": 0.0063627 
},
{
 "date":  -3137,
"name": "GSPC.Close",
"price":  66.56,
"rsi": 51.628,
"ret": 0.0019569 
},
{
 "date":  -3136,
"name": "GSPC.Close",
"price":  66.56,
"rsi":   53.1,
"ret":      0 
},
{
 "date":  -3135,
"name": "GSPC.Close",
"price":  66.73,
"rsi":   53.1,
"ret": 0.0025541 
},
{
 "date":  -3132,
"name": "GSPC.Close",
"price":  67.08,
"rsi": 55.169,
"ret": 0.005245 
},
{
 "date":  -3131,
"name": "GSPC.Close",
"price":  66.89,
"rsi": 59.163,
"ret": -0.0028324 
},
{
 "date":  -3130,
"name": "GSPC.Close",
"price":  65.64,
"rsi": 56.234,
"ret": -0.018687 
},
{
 "date":  -3129,
"name": "GSPC.Close",
"price":  66.67,
"rsi": 41.631,
"ret": 0.015692 
},
{
 "date":  -3128,
"name": "GSPC.Close",
"price":  66.66,
"rsi": 52.562,
"ret": -0.00014999 
},
{
 "date":  -3125,
"name": "GSPC.Close",
"price":  66.15,
"rsi":  52.46,
"ret": -0.0076508 
},
{
 "date":  -3124,
"name": "GSPC.Close",
"price":   65.8,
"rsi": 47.375,
"ret": -0.005291 
},
{
 "date":  -3123,
"name": "GSPC.Close",
"price":  65.98,
"rsi": 44.208,
"ret": 0.0027356 
},
{
 "date":  -3122,
"name": "GSPC.Close",
"price":  65.69,
"rsi":   46.2,
"ret": -0.0043953 
},
{
 "date":  -3121,
"name": "GSPC.Close",
"price":  65.18,
"rsi": 43.505,
"ret": -0.0077637 
},
{
 "date":  -3118,
"name": "GSPC.Close",
"price":  64.58,
"rsi": 39.177,
"ret": -0.0092053 
},
{
 "date":  -3117,
"name": "GSPC.Close",
"price":  65.15,
"rsi": 34.791,
"ret": 0.0088263 
},
{
 "date":  -3116,
"name": "GSPC.Close",
"price":  65.14,
"rsi": 41.492,
"ret": -0.00015349 
},
{
 "date":  -3115,
"name": "GSPC.Close",
"price":   64.9,
"rsi": 41.411,
"ret": -0.0036844 
},
{
 "date":  -3114,
"name": "GSPC.Close",
"price":  65.16,
"rsi": 39.436,
"ret": 0.0040062 
},
{
 "date":  -3111,
"name": "GSPC.Close",
"price":  64.47,
"rsi": 42.628,
"ret": -0.010589 
},
{
 "date":  -3110,
"name": "GSPC.Close",
"price":  64.47,
"rsi": 37.048,
"ret":      0 
},
{
 "date":  -3109,
"name": "GSPC.Close",
"price":  64.59,
"rsi": 37.048,
"ret": 0.0018613 
},
{
 "date":  -3108,
"name": "GSPC.Close",
"price":  64.52,
"rsi": 38.667,
"ret": -0.0010838 
},
{
 "date":  -3107,
"name": "GSPC.Close",
"price":  64.64,
"rsi": 38.052,
"ret": 0.0018599 
},
{
 "date":  -3104,
"name": "GSPC.Close",
"price":  65.21,
"rsi": 39.819,
"ret": 0.0088181 
},
{
 "date":  -3102,
"name": "GSPC.Close",
"price":  65.63,
"rsi": 47.482,
"ret": 0.0064407 
},
{
 "date":  -3101,
"name": "GSPC.Close",
"price":  65.81,
"rsi": 52.302,
"ret": 0.0027426 
},
{
 "date":  -3100,
"name": "GSPC.Close",
"price":  65.77,
"rsi":  54.24,
"ret": -0.00060781 
},
{
 "date":  -3097,
"name": "GSPC.Close",
"price":  65.71,
"rsi": 53.717,
"ret": -0.00091227 
},
{
 "date":  -3096,
"name": "GSPC.Close",
"price":  65.69,
"rsi": 52.895,
"ret": -0.00030437 
},
{
 "date":  -3095,
"name": "GSPC.Close",
"price":  65.32,
"rsi": 52.605,
"ret": -0.0056325 
},
{
 "date":  -3094,
"name": "GSPC.Close",
"price":  64.86,
"rsi": 47.437,
"ret": -0.0070423 
},
{
 "date":  -3093,
"name": "GSPC.Close",
"price":  65.28,
"rsi": 41.922,
"ret": 0.0064755 
},
{
 "date":  -3090,
"name": "GSPC.Close",
"price":  64.79,
"rsi":  47.88,
"ret": -0.0075061 
},
{
 "date":  -3089,
"name": "GSPC.Close",
"price":  64.41,
"rsi": 42.413,
"ret": -0.0058651 
},
{
 "date":  -3088,
"name": "GSPC.Close",
"price":   64.7,
"rsi": 38.721,
"ret": 0.0045024 
},
{
 "date":  -3087,
"name": "GSPC.Close",
"price":  64.71,
"rsi": 42.813,
"ret": 0.00015456 
},
{
 "date":  -3086,
"name": "GSPC.Close",
"price":  64.86,
"rsi": 42.954,
"ret": 0.002318 
},
{
 "date":  -3083,
"name": "GSPC.Close",
"price":  64.87,
"rsi": 45.146,
"ret": 0.00015418 
},
{
 "date":  -3082,
"name": "GSPC.Close",
"price":  65.23,
"rsi": 45.296,
"ret": 0.0055496 
},
{
 "date":  -3081,
"name": "GSPC.Close",
"price":  65.84,
"rsi": 50.568,
"ret": 0.0093515 
},
{
 "date":  -3080,
"name": "GSPC.Close",
"price":  66.61,
"rsi":  57.96,
"ret": 0.011695 
},
{
 "date":  -3079,
"name": "GSPC.Close",
"price":  66.71,
"rsi": 65.063,
"ret": 0.0015013 
},
{
 "date":  -3076,
"name": "GSPC.Close",
"price":  66.76,
"rsi": 65.869,
"ret": 0.00074951 
},
{
 "date":  -3075,
"name": "GSPC.Close",
"price":  67.37,
"rsi": 66.289,
"ret": 0.0091372 
},
{
 "date":  -3074,
"name": "GSPC.Close",
"price":  66.94,
"rsi": 70.971,
"ret": -0.0063827 
},
{
 "date":  -3073,
"name": "GSPC.Close",
"price":  67.29,
"rsi": 64.201,
"ret": 0.0052286 
},
{
 "date":  -3072,
"name": "GSPC.Close",
"price":  67.68,
"rsi": 66.964,
"ret": 0.0057958 
},
{
 "date":  -3069,
"name": "GSPC.Close",
"price":  67.67,
"rsi": 69.763,
"ret": -0.00014775 
},
{
 "date":  -3068,
"name": "GSPC.Close",
"price":  67.82,
"rsi":   69.6,
"ret": 0.0022166 
},
{
 "date":  -3067,
"name": "GSPC.Close",
"price":  67.74,
"rsi": 70.705,
"ret": -0.0011796 
},
{
 "date":  -3066,
"name": "GSPC.Close",
"price":  67.95,
"rsi":  69.26,
"ret": 0.0031001 
},
{
 "date":  -3065,
"name": "GSPC.Close",
"price":  68.06,
"rsi": 70.939,
"ret": 0.0016188 
},
{
 "date":  -3062,
"name": "GSPC.Close",
"price":  67.72,
"rsi": 71.808,
"ret": -0.0049956 
},
{
 "date":  -3061,
"name": "GSPC.Close",
"price":  67.55,
"rsi": 65.308,
"ret": -0.0025103 
},
{
 "date":  -3060,
"name": "GSPC.Close",
"price":  67.73,
"rsi": 62.272,
"ret": 0.0026647 
},
{
 "date":  -3059,
"name": "GSPC.Close",
"price":  68.11,
"rsi": 64.171,
"ret": 0.0056105 
},
{
 "date":  -3058,
"name": "GSPC.Close",
"price":  68.29,
"rsi":  67.85,
"ret": 0.0026428 
},
{
 "date":  -3055,
"name": "GSPC.Close",
"price":  68.43,
"rsi":  69.45,
"ret": 0.0020501 
},
{
 "date":  -3054,
"name": "GSPC.Close",
"price":  68.44,
"rsi": 70.673,
"ret": 0.00014613 
},
{
 "date":  -3053,
"name": "GSPC.Close",
"price":  67.98,
"rsi": 70.763,
"ret": -0.0067212 
},
{
 "date":  -3052,
"name": "GSPC.Close",
"price":  67.59,
"rsi": 61.424,
"ret": -0.005737 
},
{
 "date":  -3051,
"name": "GSPC.Close",
"price":  67.67,
"rsi": 54.819,
"ret": 0.0011836 
},
{
 "date":  -3048,
"name": "GSPC.Close",
"price":   67.7,
"rsi": 55.867,
"ret": 0.00044333 
},
{
 "date":  -3047,
"name": "GSPC.Close",
"price":  67.55,
"rsi": 56.277,
"ret": -0.0022157 
},
{
 "date":  -3046,
"name": "GSPC.Close",
"price":  67.81,
"rsi": 53.597,
"ret": 0.003849 
},
{
 "date":  -3045,
"name": "GSPC.Close",
"price":  68.07,
"rsi": 57.385,
"ret": 0.0038342 
},
{
 "date":  -3044,
"name": "GSPC.Close",
"price":  68.19,
"rsi": 60.828,
"ret": 0.0017629 
},
{
 "date":  -3040,
"name": "GSPC.Close",
"price":  67.96,
"rsi":  62.34,
"ret": -0.0033729 
},
{
 "date":  -3039,
"name": "GSPC.Close",
"price":  68.46,
"rsi": 57.739,
"ret": 0.0073573 
},
{
 "date":  -3038,
"name": "GSPC.Close",
"price":  68.35,
"rsi": 63.966,
"ret": -0.0016068 
},
{
 "date":  -3037,
"name": "GSPC.Close",
"price":  67.88,
"rsi": 61.808,
"ret": -0.0068764 
},
{
 "date":  -3034,
"name": "GSPC.Close",
"price":  67.28,
"rsi": 53.504,
"ret": -0.0088391 
},
{
 "date":  -3033,
"name": "GSPC.Close",
"price":  67.96,
"rsi": 45.162,
"ret": 0.010107 
},
{
 "date":  -3032,
"name": "GSPC.Close",
"price":  68.01,
"rsi": 53.929,
"ret": 0.00073573 
},
{
 "date":  -3031,
"name": "GSPC.Close",
"price":  67.53,
"rsi": 54.505,
"ret": -0.0070578 
},
{
 "date":  -3030,
"name": "GSPC.Close",
"price":  67.65,
"rsi": 48.267,
"ret": 0.001777 
},
{
 "date":  -3027,
"name": "GSPC.Close",
"price":  67.21,
"rsi": 49.813,
"ret": -0.0065041 
},
{
 "date":  -3026,
"name": "GSPC.Close",
"price":  66.08,
"rsi": 44.554,
"ret": -0.016813 
},
{
 "date":  -3025,
"name": "GSPC.Close",
"price":  66.96,
"rsi": 34.485,
"ret": 0.013317 
},
{
 "date":  -3024,
"name": "GSPC.Close",
"price":  66.99,
"rsi": 44.924,
"ret": 0.00044803 
},
{
 "date":  -3023,
"name": "GSPC.Close",
"price":  66.72,
"rsi": 45.244,
"ret": -0.0040305 
},
{
 "date":  -3020,
"name": "GSPC.Close",
"price":  65.77,
"rsi":  42.83,
"ret": -0.014239 
},
{
 "date":  -3019,
"name": "GSPC.Close",
"price":  65.78,
"rsi": 35.626,
"ret": 0.00015205 
},
{
 "date":  -3018,
"name": "GSPC.Close",
"price":  66.47,
"rsi": 35.749,
"ret": 0.01049 
},
{
 "date":  -3017,
"name": "GSPC.Close",
"price":  66.58,
"rsi": 43.709,
"ret": 0.0016549 
},
{
 "date":  -3016,
"name": "GSPC.Close",
"price":  66.73,
"rsi": 44.881,
"ret": 0.0022529 
},
{
 "date":  -3013,
"name": "GSPC.Close",
"price":  66.77,
"rsi": 46.517,
"ret": 0.00059943 
},
{
 "date":  -3012,
"name": "GSPC.Close",
"price":  66.73,
"rsi": 46.969,
"ret": -0.00059907 
},
{
 "date":  -3011,
"name": "GSPC.Close",
"price":  67.18,
"rsi": 46.545,
"ret": 0.0067436 
},
{
 "date":  -3010,
"name": "GSPC.Close",
"price":  67.77,
"rsi":  51.81,
"ret": 0.0087824 
},
{
 "date":  -3009,
"name": "GSPC.Close",
"price":  66.97,
"rsi": 57.694,
"ret": -0.011805 
},
{
 "date":  -3006,
"name": "GSPC.Close",
"price":  67.94,
"rsi": 48.964,
"ret": 0.014484 
},
{
 "date":  -3005,
"name": "GSPC.Close",
"price":  68.11,
"rsi": 57.384,
"ret": 0.0025022 
},
{
 "date":  -3004,
"name": "GSPC.Close",
"price":  68.17,
"rsi": 58.671,
"ret": 0.00088093 
},
{
 "date":  -3003,
"name": "GSPC.Close",
"price":  68.16,
"rsi":  59.14,
"ret": -0.00014669 
},
{
 "date":  -3002,
"name": "GSPC.Close",
"price":  68.04,
"rsi":  59.02,
"ret": -0.0017606 
},
{
 "date":  -2999,
"name": "GSPC.Close",
"price":  67.85,
"rsi": 57.509,
"ret": -0.0027925 
},
{
 "date":  -2998,
"name": "GSPC.Close",
"price":  67.87,
"rsi": 55.104,
"ret": 0.00029477 
},
{
 "date":  -2997,
"name": "GSPC.Close",
"price":  68.21,
"rsi": 55.316,
"ret": 0.0050096 
},
{
 "date":  -2996,
"name": "GSPC.Close",
"price":  68.45,
"rsi": 58.869,
"ret": 0.0035185 
},
{
 "date":  -2995,
"name": "GSPC.Close",
"price":     68,
"rsi": 61.214,
"ret": -0.0065741 
},
{
 "date":  -2992,
"name": "GSPC.Close",
"price":  68.06,
"rsi": 54.895,
"ret": 0.00088235 
},
{
 "date":  -2991,
"name": "GSPC.Close",
"price":  67.98,
"rsi": 55.554,
"ret": -0.0011754 
},
{
 "date":  -2990,
"name": "GSPC.Close",
"price":  68.34,
"rsi": 54.413,
"ret": 0.0052957 
},
{
 "date":  -2989,
"name": "GSPC.Close",
"price":  68.46,
"rsi":  58.54,
"ret": 0.0017559 
},
{
 "date":  -2988,
"name": "GSPC.Close",
"price":  68.34,
"rsi": 59.845,
"ret": -0.0017528 
},
{
 "date":  -2985,
"name": "GSPC.Close",
"price":  68.42,
"rsi": 57.883,
"ret": 0.0011706 
},
{
 "date":  -2984,
"name": "GSPC.Close",
"price":  68.62,
"rsi": 58.851,
"ret": 0.0029231 
},
{
 "date":  -2983,
"name": "GSPC.Close",
"price":  68.73,
"rsi":  61.25,
"ret": 0.001603 
},
{
 "date":  -2982,
"name": "GSPC.Close",
"price":  69.11,
"rsi": 62.544,
"ret": 0.0055289 
},
{
 "date":  -2981,
"name": "GSPC.Close",
"price":  69.47,
"rsi": 66.681,
"ret": 0.0052091 
},
{
 "date":  -2978,
"name": "GSPC.Close",
"price":  70.01,
"rsi": 70.056,
"ret": 0.0077731 
},
{
 "date":  -2976,
"name": "GSPC.Close",
"price":  70.87,
"rsi": 74.266,
"ret": 0.012284 
},
{
 "date":  -2975,
"name": "GSPC.Close",
"price":  70.77,
"rsi": 79.267,
"ret": -0.001411 
},
{
 "date":  -2974,
"name": "GSPC.Close",
"price":  71.07,
"rsi": 77.384,
"ret": 0.0042391 
},
{
 "date":  -2971,
"name": "GSPC.Close",
"price":  71.27,
"rsi": 78.996,
"ret": 0.0028141 
},
{
 "date":  -2970,
"name": "GSPC.Close",
"price":  71.66,
"rsi": 80.018,
"ret": 0.0054721 
},
{
 "date":  -2969,
"name": "GSPC.Close",
"price":  71.67,
"rsi": 81.871,
"ret": 0.00013955 
},
{
 "date":  -2968,
"name": "GSPC.Close",
"price":  71.62,
"rsi": 81.918,
"ret": -0.00069764 
},
{
 "date":  -2967,
"name": "GSPC.Close",
"price":  71.62,
"rsi": 80.806,
"ret":      0 
},
{
 "date":  -2964,
"name": "GSPC.Close",
"price":  71.72,
"rsi": 80.806,
"ret": 0.0013963 
},
{
 "date":  -2963,
"name": "GSPC.Close",
"price":  71.78,
"rsi": 81.392,
"ret": 0.00083659 
},
{
 "date":  -2962,
"name": "GSPC.Close",
"price":   71.7,
"rsi": 81.751,
"ret": -0.0011145 
},
{
 "date":  -2960,
"name": "GSPC.Close",
"price":  71.84,
"rsi": 79.543,
"ret": 0.0019526 
},
{
 "date":  -2957,
"name": "GSPC.Close",
"price":  71.85,
"rsi": 80.534,
"ret": 0.0001392 
},
{
 "date":  -2956,
"name": "GSPC.Close",
"price":  71.75,
"rsi": 80.606,
"ret": -0.0013918 
},
{
 "date":  -2955,
"name": "GSPC.Close",
"price":   71.7,
"rsi": 77.508,
"ret": -0.00069686 
},
{
 "date":  -2954,
"name": "GSPC.Close",
"price":  71.32,
"rsi": 75.936,
"ret": -0.0052999 
},
{
 "date":  -2953,
"name": "GSPC.Close",
"price":  71.78,
"rsi": 65.126,
"ret": 0.0064498 
},
{
 "date":  -2950,
"name": "GSPC.Close",
"price":  72.01,
"rsi": 70.585,
"ret": 0.0032042 
},
{
 "date":  -2949,
"name": "GSPC.Close",
"price":  71.93,
"rsi": 72.871,
"ret": -0.001111 
},
{
 "date":  -2948,
"name": "GSPC.Close",
"price":  71.99,
"rsi":  70.81,
"ret": 0.00083414 
},
{
 "date":  -2947,
"name": "GSPC.Close",
"price":   71.7,
"rsi": 71.462,
"ret": -0.0040283 
},
{
 "date":  -2946,
"name": "GSPC.Close",
"price":  72.04,
"rsi": 64.017,
"ret": 0.004742 
},
{
 "date":  -2943,
"name": "GSPC.Close",
"price":  72.39,
"rsi":   68.2,
"ret": 0.0048584 
},
{
 "date":  -2942,
"name": "GSPC.Close",
"price":  72.64,
"rsi":  71.83,
"ret": 0.0034535 
},
{
 "date":  -2941,
"name": "GSPC.Close",
"price":  72.53,
"rsi": 74.104,
"ret": -0.0015143 
},
{
 "date":  -2940,
"name": "GSPC.Close",
"price":  71.98,
"rsi": 71.374,
"ret": -0.0075831 
},
{
 "date":  -2939,
"name": "GSPC.Close",
"price":  72.01,
"rsi": 59.559,
"ret": 0.00041678 
},
{
 "date":  -2936,
"name": "GSPC.Close",
"price":  71.76,
"rsi": 59.948,
"ret": -0.0034717 
},
{
 "date":  -2935,
"name": "GSPC.Close",
"price":  71.26,
"rsi": 55.179,
"ret": -0.0069677 
},
{
 "date":  -2934,
"name": "GSPC.Close",
"price":  71.12,
"rsi": 47.108,
"ret": -0.0019646 
},
{
 "date":  -2933,
"name": "GSPC.Close",
"price":  70.86,
"rsi": 45.118,
"ret": -0.0036558 
},
{
 "date":  -2932,
"name": "GSPC.Close",
"price":  70.91,
"rsi": 41.603,
"ret": 0.00070562 
},
{
 "date":  -2928,
"name": "GSPC.Close",
"price":  71.02,
"rsi":  42.53,
"ret": 0.0015513 
},
{
 "date":  -2927,
"name": "GSPC.Close",
"price":  71.65,
"rsi": 44.614,
"ret": 0.0088707 
},
{
 "date":  -2926,
"name": "GSPC.Close",
"price":  71.69,
"rsi": 54.736,
"ret": 0.00055827 
},
{
 "date":  -2925,
"name": "GSPC.Close",
"price":  71.55,
"rsi": 55.294,
"ret": -0.0019529 
},
{
 "date":  -2921,
"name": "GSPC.Close",
"price":  70.96,
"rsi": 52.836,
"ret": -0.008246 
},
{
 "date":  -2920,
"name": "GSPC.Close",
"price":  71.13,
"rsi": 43.967,
"ret": 0.0023957 
},
{
 "date":  -2919,
"name": "GSPC.Close",
"price":  70.64,
"rsi": 46.741,
"ret": -0.0068888 
},
{
 "date":  -2918,
"name": "GSPC.Close",
"price":  69.66,
"rsi": 40.514,
"ret": -0.013873 
},
{
 "date":  -2915,
"name": "GSPC.Close",
"price":  69.12,
"rsi": 31.482,
"ret": -0.0077519 
},
{
 "date":  -2914,
"name": "GSPC.Close",
"price":  69.15,
"rsi": 27.803,
"ret": 0.00043403 
},
{
 "date":  -2913,
"name": "GSPC.Close",
"price":  68.96,
"rsi": 28.304,
"ret": -0.0027477 
},
{
 "date":  -2912,
"name": "GSPC.Close",
"price":  69.37,
"rsi": 27.025,
"ret": 0.0059455 
},
{
 "date":  -2911,
"name": "GSPC.Close",
"price":  69.61,
"rsi": 33.963,
"ret": 0.0034597 
},
{
 "date":  -2908,
"name": "GSPC.Close",
"price":  69.47,
"rsi": 37.697,
"ret": -0.0020112 
},
{
 "date":  -2907,
"name": "GSPC.Close",
"price":  69.07,
"rsi": 36.403,
"ret": -0.0057579 
},
{
 "date":  -2906,
"name": "GSPC.Close",
"price":  68.32,
"rsi": 32.928,
"ret": -0.010859 
},
{
 "date":  -2905,
"name": "GSPC.Close",
"price":  68.39,
"rsi": 27.606,
"ret": 0.0010246 
},
{
 "date":  -2904,
"name": "GSPC.Close",
"price":  68.75,
"rsi": 28.763,
"ret": 0.0052639 
},
{
 "date":  -2901,
"name": "GSPC.Close",
"price":  68.81,
"rsi": 34.557,
"ret": 0.00087273 
},
{
 "date":  -2900,
"name": "GSPC.Close",
"price":  68.29,
"rsi": 35.499,
"ret": -0.007557 
},
{
 "date":  -2899,
"name": "GSPC.Close",
"price":   68.4,
"rsi": 31.296,
"ret": 0.0016108 
},
{
 "date":  -2898,
"name": "GSPC.Close",
"price":  68.35,
"rsi":   33.1,
"ret": -0.00073099 
},
{
 "date":  -2897,
"name": "GSPC.Close",
"price":  68.13,
"rsi":  32.68,
"ret": -0.0032187 
},
{
 "date":  -2894,
"name": "GSPC.Close",
"price":   67.9,
"rsi": 30.826,
"ret": -0.0033759 
},
{
 "date":  -2893,
"name": "GSPC.Close",
"price":  68.17,
"rsi": 28.976,
"ret": 0.0039764 
},
{
 "date":  -2892,
"name": "GSPC.Close",
"price":  68.84,
"rsi": 33.986,
"ret": 0.0098284 
},
{
 "date":  -2891,
"name": "GSPC.Close",
"price":  69.26,
"rsi": 44.457,
"ret": 0.0061011 
},
{
 "date":  -2890,
"name": "GSPC.Close",
"price":  69.81,
"rsi": 49.829,
"ret": 0.0079411 
},
{
 "date":  -2887,
"name": "GSPC.Close",
"price":  69.88,
"rsi": 55.852,
"ret": 0.0010027 
},
{
 "date":  -2886,
"name": "GSPC.Close",
"price":  69.96,
"rsi": 56.566,
"ret": 0.0011448 
},
{
 "date":  -2885,
"name": "GSPC.Close",
"price":  70.42,
"rsi": 57.415,
"ret": 0.0065752 
},
{
 "date":  -2884,
"name": "GSPC.Close",
"price":  70.58,
"rsi": 62.009,
"ret": 0.0022721 
},
{
 "date":  -2883,
"name": "GSPC.Close",
"price":  70.48,
"rsi": 63.485,
"ret": -0.0014168 
},
{
 "date":  -2880,
"name": "GSPC.Close",
"price":  70.46,
"rsi": 61.868,
"ret": -0.00028377 
},
{
 "date":  -2879,
"name": "GSPC.Close",
"price":  70.45,
"rsi":  61.53,
"ret": -0.00014192 
},
{
 "date":  -2878,
"name": "GSPC.Close",
"price":  70.42,
"rsi":  61.35,
"ret": -0.00042583 
},
{
 "date":  -2877,
"name": "GSPC.Close",
"price":  70.74,
"rsi": 60.774,
"ret": 0.0045442 
},
{
 "date":  -2876,
"name": "GSPC.Close",
"price":  70.59,
"rsi": 64.589,
"ret": -0.0021204 
},
{
 "date":  -2873,
"name": "GSPC.Close",
"price":  70.41,
"rsi": 61.566,
"ret": -0.0025499 
},
{
 "date":  -2872,
"name": "GSPC.Close",
"price":  70.66,
"rsi": 58.055,
"ret": 0.0035506 
},
{
 "date":  -2871,
"name": "GSPC.Close",
"price":  70.32,
"rsi": 61.352,
"ret": -0.0048118 
},
{
 "date":  -2869,
"name": "GSPC.Close",
"price":  70.16,
"rsi": 55.019,
"ret": -0.0022753 
},
{
 "date":  -2866,
"name": "GSPC.Close",
"price":  69.76,
"rsi": 52.284,
"ret": -0.0057013 
},
{
 "date":  -2865,
"name": "GSPC.Close",
"price":  69.89,
"rsi": 46.112,
"ret": 0.0018635 
},
{
 "date":  -2864,
"name": "GSPC.Close",
"price":  69.96,
"rsi":  48.25,
"ret": 0.0010016 
},
{
 "date":  -2863,
"name": "GSPC.Close",
"price":   70.2,
"rsi": 49.414,
"ret": 0.0034305 
},
{
 "date":  -2862,
"name": "GSPC.Close",
"price":  70.16,
"rsi": 53.292,
"ret": -0.0005698 
},
{
 "date":  -2859,
"name": "GSPC.Close",
"price":  70.01,
"rsi": 52.569,
"ret": -0.002138 
},
{
 "date":  -2858,
"name": "GSPC.Close",
"price":  69.78,
"rsi": 49.837,
"ret": -0.0032852 
},
{
 "date":  -2857,
"name": "GSPC.Close",
"price":  69.69,
"rsi": 45.898,
"ret": -0.0012898 
},
{
 "date":  -2856,
"name": "GSPC.Close",
"price":  70.19,
"rsi": 44.418,
"ret": 0.0071746 
},
{
 "date":  -2855,
"name": "GSPC.Close",
"price":  70.42,
"rsi": 53.404,
"ret": 0.0032768 
},
{
 "date":  -2852,
"name": "GSPC.Close",
"price":   70.4,
"rsi": 56.859,
"ret": -0.00028401 
},
{
 "date":  -2851,
"name": "GSPC.Close",
"price":   70.6,
"rsi": 56.467,
"ret": 0.0028409 
},
{
 "date":  -2850,
"name": "GSPC.Close",
"price":  70.91,
"rsi": 59.477,
"ret": 0.0043909 
},
{
 "date":  -2849,
"name": "GSPC.Close",
"price":  71.06,
"rsi": 63.669,
"ret": 0.0021154 
},
{
 "date":  -2848,
"name": "GSPC.Close",
"price":  70.94,
"rsi": 65.528,
"ret": -0.0016887 
},
{
 "date":  -2845,
"name": "GSPC.Close",
"price":  70.85,
"rsi": 62.762,
"ret": -0.0012687 
},
{
 "date":  -2844,
"name": "GSPC.Close",
"price":  70.66,
"rsi": 60.693,
"ret": -0.0026817 
},
{
 "date":  -2843,
"name": "GSPC.Close",
"price":  70.51,
"rsi": 56.461,
"ret": -0.0021228 
},
{
 "date":  -2842,
"name": "GSPC.Close",
"price":   70.4,
"rsi": 53.301,
"ret": -0.0015601 
},
{
 "date":  -2841,
"name": "GSPC.Close",
"price":  70.45,
"rsi": 51.045,
"ret": 0.00071023 
},
{
 "date":  -2838,
"name": "GSPC.Close",
"price":  69.89,
"rsi": 52.038,
"ret": -0.0079489 
},
{
 "date":  -2837,
"name": "GSPC.Close",
"price":   69.7,
"rsi": 41.803,
"ret": -0.0027186 
},
{
 "date":  -2836,
"name": "GSPC.Close",
"price":  70.04,
"rsi": 39.001,
"ret": 0.004878 
},
{
 "date":  -2835,
"name": "GSPC.Close",
"price":  70.01,
"rsi":  45.98,
"ret": -0.00042833 
},
{
 "date":  -2834,
"name": "GSPC.Close",
"price":  69.55,
"rsi": 45.486,
"ret": -0.0065705 
},
{
 "date":  -2831,
"name": "GSPC.Close",
"price":  69.37,
"rsi": 38.625,
"ret": -0.0025881 
},
{
 "date":  -2830,
"name": "GSPC.Close",
"price":  68.81,
"rsi": 36.317,
"ret": -0.0080727 
},
{
 "date":  -2829,
"name": "GSPC.Close",
"price":  68.49,
"rsi": 30.259,
"ret": -0.0046505 
},
{
 "date":  -2828,
"name": "GSPC.Close",
"price":  68.91,
"rsi": 27.442,
"ret": 0.0061323 
},
{
 "date":  -2827,
"name": "GSPC.Close",
"price":  68.84,
"rsi":  35.88,
"ret": -0.0010158 
},
{
 "date":  -2824,
"name": "GSPC.Close",
"price":  68.31,
"rsi": 35.146,
"ret": -0.007699 
},
{
 "date":  -2823,
"name": "GSPC.Close",
"price":  68.56,
"rsi": 30.124,
"ret": 0.0036598 
},
{
 "date":  -2822,
"name": "GSPC.Close",
"price":  68.41,
"rsi": 34.853,
"ret": -0.0021879 
},
{
 "date":  -2821,
"name": "GSPC.Close",
"price":   67.9,
"rsi": 33.393,
"ret": -0.0074551 
},
{
 "date":  -2820,
"name": "GSPC.Close",
"price":   67.9,
"rsi": 28.951,
"ret":      0 
},
{
 "date":  -2817,
"name": "GSPC.Close",
"price":   67.6,
"rsi": 28.951,
"ret": -0.0044183 
},
{
 "date":  -2816,
"name": "GSPC.Close",
"price":   67.9,
"rsi": 26.543,
"ret": 0.0044379 
},
{
 "date":  -2815,
"name": "GSPC.Close",
"price":  68.27,
"rsi": 32.583,
"ret": 0.0054492 
},
{
 "date":  -2814,
"name": "GSPC.Close",
"price":  68.59,
"rsi":  39.22,
"ret": 0.0046873 
},
{
 "date":  -2810,
"name": "GSPC.Close",
"price":  68.53,
"rsi": 44.325,
"ret": -0.00087476 
},
{
 "date":  -2809,
"name": "GSPC.Close",
"price":  68.46,
"rsi": 43.586,
"ret": -0.0010215 
},
{
 "date":  -2808,
"name": "GSPC.Close",
"price":  67.71,
"rsi": 42.692,
"ret": -0.010955 
},
{
 "date":  -2807,
"name": "GSPC.Close",
"price":  67.05,
"rsi": 34.517,
"ret": -0.0097475 
},
{
 "date":  -2806,
"name": "GSPC.Close",
"price":   66.3,
"rsi": 29.216,
"ret": -0.011186 
},
{
 "date":  -2803,
"name": "GSPC.Close",
"price":  65.24,
"rsi": 24.593,
"ret": -0.015988 
},
{
 "date":  -2802,
"name": "GSPC.Close",
"price":   65.7,
"rsi":  19.82,
"ret": 0.0070509 
},
{
 "date":  -2801,
"name": "GSPC.Close",
"price":  65.99,
"rsi": 26.488,
"ret": 0.004414 
},
{
 "date":  -2800,
"name": "GSPC.Close",
"price":  66.53,
"rsi": 30.417,
"ret": 0.0081831 
},
{
 "date":  -2799,
"name": "GSPC.Close",
"price":  66.24,
"rsi": 37.152,
"ret": -0.0043589 
},
{
 "date":  -2796,
"name": "GSPC.Close",
"price":  66.02,
"rsi": 35.182,
"ret": -0.0033213 
},
{
 "date":  -2795,
"name": "GSPC.Close",
"price":  65.17,
"rsi": 33.722,
"ret": -0.012875 
},
{
 "date":  -2794,
"name": "GSPC.Close",
"price":  64.26,
"rsi": 28.755,
"ret": -0.013963 
},
{
 "date":  -2793,
"name": "GSPC.Close",
"price":  63.57,
"rsi": 24.581,
"ret": -0.010738 
},
{
 "date":  -2792,
"name": "GSPC.Close",
"price":  62.65,
"rsi": 21.976,
"ret": -0.014472 
},
{
 "date":  -2789,
"name": "GSPC.Close",
"price":   63.1,
"rsi": 19.074,
"ret": 0.0071828 
},
{
 "date":  -2788,
"name": "GSPC.Close",
"price":  64.29,
"rsi": 24.337,
"ret": 0.018859 
},
{
 "date":  -2787,
"name": "GSPC.Close",
"price":  64.27,
"rsi": 36.162,
"ret": -0.00031109 
},
{
 "date":  -2786,
"name": "GSPC.Close",
"price":  63.93,
"rsi":  36.06,
"ret": -0.0052902 
},
{
 "date":  -2785,
"name": "GSPC.Close",
"price":  63.82,
"rsi":  34.29,
"ret": -0.0017206 
},
{
 "date":  -2782,
"name": "GSPC.Close",
"price":  63.59,
"rsi": 33.713,
"ret": -0.0036039 
},
{
 "date":  -2781,
"name": "GSPC.Close",
"price":  62.34,
"rsi": 32.482,
"ret": -0.019657 
},
{
 "date":  -2780,
"name": "GSPC.Close",
"price":  61.11,
"rsi": 26.765,
"ret": -0.019731 
},
{
 "date":  -2779,
"name": "GSPC.Close",
"price":  60.62,
"rsi": 22.558,
"ret": -0.0080183 
},
{
 "date":  -2778,
"name": "GSPC.Close",
"price":  59.47,
"rsi": 21.133,
"ret": -0.018971 
},
{
 "date":  -2775,
"name": "GSPC.Close",
"price":   55.5,
"rsi": 18.223,
"ret": -0.066756 
},
{
 "date":  -2774,
"name": "GSPC.Close",
"price":  58.08,
"rsi": 12.053,
"ret": 0.046486 
},
{
 "date":  -2772,
"name": "GSPC.Close",
"price":  59.63,
"rsi": 28.901,
"ret": 0.026687 
},
{
 "date":  -2771,
"name": "GSPC.Close",
"price":  59.38,
"rsi": 36.741,
"ret": -0.0041925 
},
{
 "date":  -2768,
"name": "GSPC.Close",
"price":  57.27,
"rsi": 36.051,
"ret": -0.035534 
},
{
 "date":  -2767,
"name": "GSPC.Close",
"price":  57.57,
"rsi": 30.791,
"ret": 0.0052383 
},
{
 "date":  -2766,
"name": "GSPC.Close",
"price":  58.39,
"rsi": 32.303,
"ret": 0.014244 
},
{
 "date":  -2765,
"name": "GSPC.Close",
"price":   58.4,
"rsi": 36.395,
"ret": 0.00017126 
},
{
 "date":  -2764,
"name": "GSPC.Close",
"price":  58.45,
"rsi": 36.445,
"ret": 0.00085616 
},
{
 "date":  -2761,
"name": "GSPC.Close",
"price":  57.82,
"rsi": 36.715,
"ret": -0.010778 
},
{
 "date":  -2760,
"name": "GSPC.Close",
"price":  56.34,
"rsi": 34.712,
"ret": -0.025597 
},
{
 "date":  -2759,
"name": "GSPC.Close",
"price":   55.5,
"rsi": 30.503,
"ret": -0.014909 
},
{
 "date":  -2758,
"name": "GSPC.Close",
"price":  54.33,
"rsi": 28.397,
"ret": -0.021081 
},
{
 "date":  -2757,
"name": "GSPC.Close",
"price":  55.89,
"rsi": 25.734,
"ret": 0.028713 
},
{
 "date":  -2754,
"name": "GSPC.Close",
"price":  55.74,
"rsi":  34.55,
"ret": -0.0026838 
},
{
 "date":  -2753,
"name": "GSPC.Close",
"price":  55.54,
"rsi":  34.13,
"ret": -0.0035881 
},
{
 "date":  -2752,
"name": "GSPC.Close",
"price":  54.78,
"rsi": 33.545,
"ret": -0.013684 
},
{
 "date":  -2751,
"name": "GSPC.Close",
"price":  53.59,
"rsi": 31.347,
"ret": -0.021723 
},
{
 "date":  -2750,
"name": "GSPC.Close",
"price":  52.68,
"rsi": 28.227,
"ret": -0.016981 
},
{
 "date":  -2747,
"name": "GSPC.Close",
"price":  52.45,
"rsi": 26.089,
"ret": -0.004366 
},
{
 "date":  -2746,
"name": "GSPC.Close",
"price":  52.32,
"rsi": 25.562,
"ret": -0.0024786 
},
{
 "date":  -2745,
"name": "GSPC.Close",
"price":   52.6,
"rsi": 25.252,
"ret": 0.0053517 
},
{
 "date":  -2744,
"name": "GSPC.Close",
"price":  54.41,
"rsi":   27.3,
"ret": 0.034411 
},
{
 "date":  -2743,
"name": "GSPC.Close",
"price":  54.75,
"rsi": 38.947,
"ret": 0.0062489 
},
{
 "date":  -2740,
"name": "GSPC.Close",
"price":  55.86,
"rsi": 40.863,
"ret": 0.020274 
},
{
 "date":  -2739,
"name": "GSPC.Close",
"price":  56.49,
"rsi": 46.741,
"ret": 0.011278 
},
{
 "date":  -2737,
"name": "GSPC.Close",
"price":  56.81,
"rsi": 49.791,
"ret": 0.0056647 
},
{
 "date":  -2736,
"name": "GSPC.Close",
"price":  56.17,
"rsi": 51.316,
"ret": -0.011266 
},
{
 "date":  -2733,
"name": "GSPC.Close",
"price":  56.55,
"rsi": 48.165,
"ret": 0.0067652 
},
{
 "date":  -2732,
"name": "GSPC.Close",
"price":   57.2,
"rsi": 50.123,
"ret": 0.011494 
},
{
 "date":  -2731,
"name": "GSPC.Close",
"price":  57.73,
"rsi": 53.369,
"ret": 0.0092657 
},
{
 "date":  -2730,
"name": "GSPC.Close",
"price":  58.03,
"rsi": 55.889,
"ret": 0.0051966 
},
{
 "date":  -2729,
"name": "GSPC.Close",
"price":  57.83,
"rsi": 57.296,
"ret": -0.0034465 
},
{
 "date":  -2726,
"name": "GSPC.Close",
"price":  57.83,
"rsi": 56.014,
"ret":      0 
},
{
 "date":  -2725,
"name": "GSPC.Close",
"price":  56.78,
"rsi": 56.014,
"ret": -0.018157 
},
{
 "date":  -2724,
"name": "GSPC.Close",
"price":   56.2,
"rsi": 49.294,
"ret": -0.010215 
},
{
 "date":  -2723,
"name": "GSPC.Close",
"price":  56.42,
"rsi": 46.011,
"ret": 0.0039146 
},
{
 "date":  -2722,
"name": "GSPC.Close",
"price":  56.81,
"rsi": 47.441,
"ret": 0.0069124 
},
{
 "date":  -2719,
"name": "GSPC.Close",
"price":   56.8,
"rsi": 49.971,
"ret": -0.00017603 
},
{
 "date":  -2718,
"name": "GSPC.Close",
"price":  56.36,
"rsi": 49.904,
"ret": -0.0077465 
},
{
 "date":  -2717,
"name": "GSPC.Close",
"price":  56.46,
"rsi": 46.951,
"ret": 0.0017743 
},
{
 "date":  -2716,
"name": "GSPC.Close",
"price":  56.77,
"rsi": 47.709,
"ret": 0.0054906 
},
{
 "date":  -2715,
"name": "GSPC.Close",
"price":   57.2,
"rsi": 50.088,
"ret": 0.0075744 
},
{
 "date":  -2712,
"name": "GSPC.Close",
"price":  57.83,
"rsi": 53.264,
"ret": 0.011014 
},
{
 "date":  -2711,
"name": "GSPC.Close",
"price":  58.23,
"rsi": 57.528,
"ret": 0.0069168 
},
{
 "date":  -2710,
"name": "GSPC.Close",
"price":  57.75,
"rsi": 60.022,
"ret": -0.0082432 
},
{
 "date":  -2709,
"name": "GSPC.Close",
"price":  57.98,
"rsi": 55.788,
"ret": 0.0039827 
},
{
 "date":  -2708,
"name": "GSPC.Close",
"price":  58.12,
"rsi": 57.341,
"ret": 0.0024146 
},
{
 "date":  -2705,
"name": "GSPC.Close",
"price":  57.75,
"rsi": 58.301,
"ret": -0.0063661 
},
{
 "date":  -2704,
"name": "GSPC.Close",
"price":  57.36,
"rsi": 54.792,
"ret": -0.0067532 
},
{
 "date":  -2703,
"name": "GSPC.Close",
"price":  57.51,
"rsi": 51.287,
"ret": 0.0026151 
},
{
 "date":  -2702,
"name": "GSPC.Close",
"price":  57.57,
"rsi": 52.544,
"ret": 0.0010433 
},
{
 "date":  -2701,
"name": "GSPC.Close",
"price":  57.55,
"rsi": 53.066,
"ret": -0.0003474 
},
{
 "date":  -2698,
"name": "GSPC.Close",
"price":  57.63,
"rsi": 52.858,
"ret": 0.0013901 
},
{
 "date":  -2697,
"name": "GSPC.Close",
"price":  58.25,
"rsi": 53.643,
"ret": 0.010758 
},
{
 "date":  -2696,
"name": "GSPC.Close",
"price":  58.66,
"rsi":   59.3,
"ret": 0.0070386 
},
{
 "date":  -2695,
"name": "GSPC.Close",
"price":  58.64,
"rsi": 62.554,
"ret": -0.00034095 
},
{
 "date":  -2694,
"name": "GSPC.Close",
"price":  59.01,
"rsi": 62.292,
"ret": 0.0063097 
},
{
 "date":  -2691,
"name": "GSPC.Close",
"price":  59.37,
"rsi": 65.193,
"ret": 0.0061007 
},
{
 "date":  -2690,
"name": "GSPC.Close",
"price":  59.12,
"rsi": 67.789,
"ret": -0.0042109 
},
{
 "date":  -2689,
"name": "GSPC.Close",
"price":  59.78,
"rsi": 64.207,
"ret": 0.011164 
},
{
 "date":  -2688,
"name": "GSPC.Close",
"price":   59.7,
"rsi": 68.882,
"ret": -0.0013382 
},
{
 "date":  -2687,
"name": "GSPC.Close",
"price":  59.58,
"rsi": 67.727,
"ret": -0.0020101 
},
{
 "date":  -2684,
"name": "GSPC.Close",
"price":  59.55,
"rsi": 65.942,
"ret": -0.00050352 
},
{
 "date":  -2683,
"name": "GSPC.Close",
"price":  58.79,
"rsi": 65.477,
"ret": -0.012762 
},
{
 "date":  -2682,
"name": "GSPC.Close",
"price":  58.66,
"rsi": 54.918,
"ret": -0.0022113 
},
{
 "date":  -2681,
"name": "GSPC.Close",
"price":  58.68,
"rsi": 53.333,
"ret": 0.00034095 
},
{
 "date":  -2680,
"name": "GSPC.Close",
"price":  59.12,
"rsi": 53.555,
"ret": 0.0074983 
},
{
 "date":  -2676,
"name": "GSPC.Close",
"price":  58.56,
"rsi":  58.26,
"ret": -0.0094723 
},
{
 "date":  -2675,
"name": "GSPC.Close",
"price":  58.12,
"rsi": 51.157,
"ret": -0.0075137 
},
{
 "date":  -2674,
"name": "GSPC.Close",
"price":  58.36,
"rsi": 46.374,
"ret": 0.0041294 
},
{
 "date":  -2673,
"name": "GSPC.Close",
"price":  58.38,
"rsi": 49.166,
"ret": 0.0003427 
},
{
 "date":  -2670,
"name": "GSPC.Close",
"price":  58.45,
"rsi": 49.402,
"ret": 0.001199 
},
{
 "date":  -2669,
"name": "GSPC.Close",
"price":  58.59,
"rsi": 50.274,
"ret": 0.0023952 
},
{
 "date":  -2668,
"name": "GSPC.Close",
"price":  58.84,
"rsi": 52.053,
"ret": 0.0042669 
},
{
 "date":  -2667,
"name": "GSPC.Close",
"price":   58.7,
"rsi":  55.14,
"ret": -0.0023793 
},
{
 "date":  -2666,
"name": "GSPC.Close",
"price":  58.89,
"rsi": 53.079,
"ret": 0.0032368 
},
{
 "date":  -2663,
"name": "GSPC.Close",
"price":  59.08,
"rsi": 55.509,
"ret": 0.0032264 
},
{
 "date":  -2662,
"name": "GSPC.Close",
"price":  59.03,
"rsi":  57.86,
"ret": -0.00084631 
},
{
 "date":  -2661,
"name": "GSPC.Close",
"price":  58.95,
"rsi": 57.006,
"ret": -0.0013552 
},
{
 "date":  -2660,
"name": "GSPC.Close",
"price":  58.54,
"rsi": 55.593,
"ret": -0.006955 
},
{
 "date":  -2659,
"name": "GSPC.Close",
"price":  57.69,
"rsi": 48.903,
"ret": -0.01452 
},
{
 "date":  -2656,
"name": "GSPC.Close",
"price":  56.63,
"rsi": 38.546,
"ret": -0.018374 
},
{
 "date":  -2655,
"name": "GSPC.Close",
"price":  56.96,
"rsi":  30.01,
"ret": 0.0058273 
},
{
 "date":  -2654,
"name": "GSPC.Close",
"price":  56.15,
"rsi": 34.847,
"ret": -0.014221 
},
{
 "date":  -2653,
"name": "GSPC.Close",
"price":  55.77,
"rsi": 29.465,
"ret": -0.0067676 
},
{
 "date":  -2652,
"name": "GSPC.Close",
"price":  56.27,
"rsi": 27.332,
"ret": 0.0089654 
},
{
 "date":  -2649,
"name": "GSPC.Close",
"price":  55.49,
"rsi": 34.092,
"ret": -0.013862 
},
{
 "date":  -2648,
"name": "GSPC.Close",
"price":   56.1,
"rsi": 29.484,
"ret": 0.010993 
},
{
 "date":  -2647,
"name": "GSPC.Close",
"price":  56.16,
"rsi": 36.691,
"ret": 0.0010695 
},
{
 "date":  -2646,
"name": "GSPC.Close",
"price":   56.7,
"rsi": 37.369,
"ret": 0.0096154 
},
{
 "date":  -2645,
"name": "GSPC.Close",
"price":  57.07,
"rsi":  43.26,
"ret": 0.0065256 
},
{
 "date":  -2642,
"name": "GSPC.Close",
"price":  57.07,
"rsi": 46.942,
"ret":      0 
},
{
 "date":  -2641,
"name": "GSPC.Close",
"price":   57.2,
"rsi": 46.942,
"ret": 0.0022779 
},
{
 "date":  -2640,
"name": "GSPC.Close",
"price":  57.24,
"rsi": 48.308,
"ret": 0.0006993 
},
{
 "date":  -2639,
"name": "GSPC.Close",
"price":  57.05,
"rsi": 48.746,
"ret": -0.0033194 
},
{
 "date":  -2638,
"name": "GSPC.Close",
"price":  56.95,
"rsi": 46.723,
"ret": -0.0017528 
},
{
 "date":  -2635,
"name": "GSPC.Close",
"price":  57.27,
"rsi": 45.649,
"ret": 0.005619 
},
{
 "date":  -2634,
"name": "GSPC.Close",
"price":  57.08,
"rsi": 49.638,
"ret": -0.0033176 
},
{
 "date":  -2633,
"name": "GSPC.Close",
"price":  56.89,
"rsi": 47.413,
"ret": -0.0033287 
},
{
 "date":  -2632,
"name": "GSPC.Close",
"price":  56.34,
"rsi":  45.23,
"ret": -0.0096678 
},
{
 "date":  -2631,
"name": "GSPC.Close",
"price":  55.59,
"rsi": 39.552,
"ret": -0.013312 
},
{
 "date":  -2628,
"name": "GSPC.Close",
"price":  54.96,
"rsi": 33.396,
"ret": -0.011333 
},
{
 "date":  -2627,
"name": "GSPC.Close",
"price":  53.49,
"rsi": 29.274,
"ret": -0.026747 
},
{
 "date":  -2626,
"name": "GSPC.Close",
"price":  55.21,
"rsi": 22.344,
"ret": 0.032156 
},
{
 "date":  -2625,
"name": "GSPC.Close",
"price":  54.69,
"rsi": 40.186,
"ret": -0.0094186 
},
{
 "date":  -2624,
"name": "GSPC.Close",
"price":  54.54,
"rsi": 37.389,
"ret": -0.0027427 
},
{
 "date":  -2621,
"name": "GSPC.Close",
"price":  55.72,
"rsi": 36.598,
"ret": 0.021635 
},
{
 "date":  -2620,
"name": "GSPC.Close",
"price":  56.54,
"rsi": 46.237,
"ret": 0.014716 
},
{
 "date":  -2619,
"name": "GSPC.Close",
"price":  56.52,
"rsi": 51.729,
"ret": -0.00035373 
},
{
 "date":  -2618,
"name": "GSPC.Close",
"price":  57.12,
"rsi": 51.591,
"ret": 0.010616 
},
{
 "date":  -2617,
"name": "GSPC.Close",
"price":  57.75,
"rsi": 55.443,
"ret": 0.011029 
},
{
 "date":  -2614,
"name": "GSPC.Close",
"price":  58.35,
"rsi": 59.121,
"ret": 0.01039 
},
{
 "date":  -2612,
"name": "GSPC.Close",
"price":  58.71,
"rsi": 62.312,
"ret": 0.0061697 
},
{
 "date":  -2611,
"name": "GSPC.Close",
"price":  58.32,
"rsi": 64.122,
"ret": -0.0066428 
},
{
 "date":  -2610,
"name": "GSPC.Close",
"price":  58.78,
"rsi":  60.72,
"ret": 0.0078875 
},
{
 "date":  -2607,
"name": "GSPC.Close",
"price":  59.59,
"rsi":   63.2,
"ret": 0.01378 
},
{
 "date":  -2606,
"name": "GSPC.Close",
"price":  59.46,
"rsi": 67.135,
"ret": -0.0021816 
},
{
 "date":  -2605,
"name": "GSPC.Close",
"price":  60.16,
"rsi": 65.917,
"ret": 0.011773 
},
{
 "date":  -2604,
"name": "GSPC.Close",
"price":  59.97,
"rsi": 69.161,
"ret": -0.0031582 
},
{
 "date":  -2603,
"name": "GSPC.Close",
"price":  60.16,
"rsi": 67.289,
"ret": 0.0031683 
},
{
 "date":  -2600,
"name": "GSPC.Close",
"price":  59.82,
"rsi": 68.215,
"ret": -0.0056516 
},
{
 "date":  -2599,
"name": "GSPC.Close",
"price":  60.45,
"rsi": 64.684,
"ret": 0.010532 
},
{
 "date":  -2598,
"name": "GSPC.Close",
"price":  60.81,
"rsi": 67.991,
"ret": 0.0059553 
},
{
 "date":  -2596,
"name": "GSPC.Close",
"price":  61.54,
"rsi": 69.735,
"ret": 0.012005 
},
{
 "date":  -2593,
"name": "GSPC.Close",
"price":  61.36,
"rsi": 72.952,
"ret": -0.0029249 
},
{
 "date":  -2592,
"name": "GSPC.Close",
"price":  61.73,
"rsi": 70.949,
"ret": 0.00603 
},
{
 "date":  -2591,
"name": "GSPC.Close",
"price":  62.12,
"rsi": 72.614,
"ret": 0.0063178 
},
{
 "date":  -2590,
"name": "GSPC.Close",
"price":  62.41,
"rsi": 74.286,
"ret": 0.0046684 
},
{
 "date":  -2589,
"name": "GSPC.Close",
"price":  62.26,
"rsi": 75.485,
"ret": -0.0024035 
},
{
 "date":  -2586,
"name": "GSPC.Close",
"price":  61.94,
"rsi": 73.574,
"ret": -0.0051397 
},
{
 "date":  -2585,
"name": "GSPC.Close",
"price":  62.64,
"rsi": 69.531,
"ret": 0.011301 
},
{
 "date":  -2584,
"name": "GSPC.Close",
"price":  62.39,
"rsi": 73.024,
"ret": -0.0039911 
},
{
 "date":  -2583,
"name": "GSPC.Close",
"price":  62.93,
"rsi":  69.94,
"ret": 0.0086552 
},
{
 "date":  -2582,
"name": "GSPC.Close",
"price":  63.06,
"rsi": 72.629,
"ret": 0.0020658 
},
{
 "date":  -2579,
"name": "GSPC.Close",
"price":  62.27,
"rsi": 73.249,
"ret": -0.012528 
},
{
 "date":  -2578,
"name": "GSPC.Close",
"price":  62.32,
"rsi": 63.788,
"ret": 0.00080295 
},
{
 "date":  -2577,
"name": "GSPC.Close",
"price":  62.63,
"rsi": 64.104,
"ret": 0.0049743 
},
{
 "date":  -2576,
"name": "GSPC.Close",
"price":  62.42,
"rsi":  66.08,
"ret": -0.003353 
},
{
 "date":  -2575,
"name": "GSPC.Close",
"price":  62.57,
"rsi": 63.529,
"ret": 0.0024031 
},
{
 "date":  -2572,
"name": "GSPC.Close",
"price":  62.37,
"rsi": 64.581,
"ret": -0.0031964 
},
{
 "date":  -2571,
"name": "GSPC.Close",
"price":  62.07,
"rsi": 62.012,
"ret": -0.00481 
},
{
 "date":  -2570,
"name": "GSPC.Close",
"price":  62.58,
"rsi": 58.268,
"ret": 0.0082165 
},
{
 "date":  -2569,
"name": "GSPC.Close",
"price":  62.82,
"rsi": 62.422,
"ret": 0.0038351 
},
{
 "date":  -2568,
"name": "GSPC.Close",
"price":  62.64,
"rsi": 64.226,
"ret": -0.0028653 
},
{
 "date":  -2565,
"name": "GSPC.Close",
"price":  62.63,
"rsi": 61.828,
"ret": -0.00015964 
},
{
 "date":  -2563,
"name": "GSPC.Close",
"price":  63.02,
"rsi":  61.69,
"ret": 0.006227 
},
{
 "date":  -2562,
"name": "GSPC.Close",
"price":  62.93,
"rsi":  64.97,
"ret": -0.0014281 
},
{
 "date":  -2561,
"name": "GSPC.Close",
"price":  62.96,
"rsi": 63.616,
"ret": 0.00047672 
},
{
 "date":  -2558,
"name": "GSPC.Close",
"price":   63.1,
"rsi": 63.886,
"ret": 0.0022236 
},
{
 "date":  -2556,
"name": "GSPC.Close",
"price":  62.69,
"rsi": 65.185,
"ret": -0.0064976 
},
{
 "date":  -2555,
"name": "GSPC.Close",
"price":  63.72,
"rsi": 58.546,
"ret": 0.01643 
},
{
 "date":  -2554,
"name": "GSPC.Close",
"price":  64.13,
"rsi": 67.501,
"ret": 0.0064344 
},
{
 "date":  -2551,
"name": "GSPC.Close",
"price":  64.12,
"rsi": 70.256,
"ret": -0.00015593 
},
{
 "date":  -2550,
"name": "GSPC.Close",
"price":  64.74,
"rsi": 70.099,
"ret": 0.0096694 
},
{
 "date":  -2549,
"name": "GSPC.Close",
"price":  64.59,
"rsi": 73.961,
"ret": -0.002317 
},
{
 "date":  -2548,
"name": "GSPC.Close",
"price":  64.71,
"rsi": 71.554,
"ret": 0.0018579 
},
{
 "date":  -2547,
"name": "GSPC.Close",
"price":  64.85,
"rsi":  72.33,
"ret": 0.0021635 
},
{
 "date":  -2544,
"name": "GSPC.Close",
"price":   65.2,
"rsi": 73.247,
"ret": 0.0053971 
},
{
 "date":  -2543,
"name": "GSPC.Close",
"price":  65.11,
"rsi": 75.438,
"ret": -0.0013804 
},
{
 "date":  -2542,
"name": "GSPC.Close",
"price":  64.67,
"rsi": 73.765,
"ret": -0.0067578 
},
{
 "date":  -2541,
"name": "GSPC.Close",
"price":  65.13,
"rsi": 66.051,
"ret": 0.007113 
},
{
 "date":  -2540,
"name": "GSPC.Close",
"price":  65.18,
"rsi": 69.627,
"ret": 0.0007677 
},
{
 "date":  -2537,
"name": "GSPC.Close",
"price":  65.28,
"rsi": 69.997,
"ret": 0.0015342 
},
{
 "date":  -2536,
"name": "GSPC.Close",
"price":  65.44,
"rsi": 70.764,
"ret": 0.002451 
},
{
 "date":  -2535,
"name": "GSPC.Close",
"price":  65.62,
"rsi": 71.997,
"ret": 0.0027506 
},
{
 "date":  -2534,
"name": "GSPC.Close",
"price":  65.75,
"rsi": 73.359,
"ret": 0.0019811 
},
{
 "date":  -2533,
"name": "GSPC.Close",
"price":  65.92,
"rsi":  74.33,
"ret": 0.0025856 
},
{
 "date":  -2530,
"name": "GSPC.Close",
"price":  66.24,
"rsi": 75.583,
"ret": 0.0048544 
},
{
 "date":  -2529,
"name": "GSPC.Close",
"price":  66.23,
"rsi": 77.782,
"ret": -0.00015097 
},
{
 "date":  -2528,
"name": "GSPC.Close",
"price":  65.85,
"rsi": 77.547,
"ret": -0.0057376 
},
{
 "date":  -2527,
"name": "GSPC.Close",
"price":   66.2,
"rsi": 69.014,
"ret": 0.0053151 
},
{
 "date":  -2526,
"name": "GSPC.Close",
"price":  66.31,
"rsi": 72.063,
"ret": 0.0016616 
},
{
 "date":  -2523,
"name": "GSPC.Close",
"price":  66.17,
"rsi": 72.964,
"ret": -0.0021113 
},
{
 "date":  -2522,
"name": "GSPC.Close",
"price":  66.11,
"rsi": 69.876,
"ret": -0.00090676 
},
{
 "date":  -2521,
"name": "GSPC.Close",
"price":   66.4,
"rsi": 68.538,
"ret": 0.0043866 
},
{
 "date":  -2520,
"name": "GSPC.Close",
"price":  66.17,
"rsi":  71.39,
"ret": -0.0034639 
},
{
 "date":  -2519,
"name": "GSPC.Close",
"price":  66.17,
"rsi":  66.26,
"ret":      0 
},
{
 "date":  -2516,
"name": "GSPC.Close",
"price":  65.76,
"rsi":  66.26,
"ret": -0.0061962 
},
{
 "date":  -2515,
"name": "GSPC.Close",
"price":  65.83,
"rsi": 57.688,
"ret": 0.0010645 
},
{
 "date":  -2514,
"name": "GSPC.Close",
"price":  66.15,
"rsi": 58.671,
"ret": 0.004861 
},
{
 "date":  -2513,
"name": "GSPC.Close",
"price":  66.35,
"rsi": 62.913,
"ret": 0.0030234 
},
{
 "date":  -2512,
"name": "GSPC.Close",
"price":  66.41,
"rsi": 65.309,
"ret": 0.0009043 
},
{
 "date":  -2509,
"name": "GSPC.Close",
"price":  66.52,
"rsi": 66.019,
"ret": 0.0016564 
},
{
 "date":  -2508,
"name": "GSPC.Close",
"price":   66.2,
"rsi": 67.338,
"ret": -0.0048106 
},
{
 "date":  -2507,
"name": "GSPC.Close",
"price":  65.83,
"rsi": 60.038,
"ret": -0.0055891 
},
{
 "date":  -2506,
"name": "GSPC.Close",
"price":  65.92,
"rsi": 52.898,
"ret": 0.0013672 
},
{
 "date":  -2502,
"name": "GSPC.Close",
"price":  65.46,
"rsi": 54.321,
"ret": -0.0069782 
},
{
 "date":  -2501,
"name": "GSPC.Close",
"price":  65.47,
"rsi": 46.576,
"ret": 0.00015277 
},
{
 "date":  -2500,
"name": "GSPC.Close",
"price":  65.01,
"rsi": 46.753,
"ret": -0.0070261 
},
{
 "date":  -2499,
"name": "GSPC.Close",
"price":  64.29,
"rsi": 40.138,
"ret": -0.011075 
},
{
 "date":  -2498,
"name": "GSPC.Close",
"price":   64.1,
"rsi": 32.408,
"ret": -0.0029554 
},
{
 "date":  -2495,
"name": "GSPC.Close",
"price":  64.72,
"rsi": 30.727,
"ret": 0.0096724 
},
{
 "date":  -2494,
"name": "GSPC.Close",
"price":  64.74,
"rsi":  41.41,
"ret": 0.00030902 
},
{
 "date":  -2493,
"name": "GSPC.Close",
"price":  64.85,
"rsi": 41.722,
"ret": 0.0016991 
},
{
 "date":  -2492,
"name": "GSPC.Close",
"price":  65.26,
"rsi": 43.506,
"ret": 0.0063223 
},
{
 "date":  -2491,
"name": "GSPC.Close",
"price":  65.33,
"rsi": 49.685,
"ret": 0.0010726 
},
{
 "date":  -2488,
"name": "GSPC.Close",
"price":  65.51,
"rsi": 50.677,
"ret": 0.0027552 
},
{
 "date":  -2487,
"name": "GSPC.Close",
"price":  65.67,
"rsi": 53.231,
"ret": 0.0024424 
},
{
 "date":  -2486,
"name": "GSPC.Close",
"price":  65.91,
"rsi": 55.439,
"ret": 0.0036546 
},
{
 "date":  -2485,
"name": "GSPC.Close",
"price":   65.6,
"rsi": 58.597,
"ret": -0.0047034 
},
{
 "date":  -2484,
"name": "GSPC.Close",
"price":  65.93,
"rsi": 53.339,
"ret": 0.0050305 
},
{
 "date":  -2481,
"name": "GSPC.Close",
"price":  65.61,
"rsi": 57.691,
"ret": -0.0048536 
},
{
 "date":  -2480,
"name": "GSPC.Close",
"price":  65.47,
"rsi": 52.571,
"ret": -0.0021338 
},
{
 "date":  -2479,
"name": "GSPC.Close",
"price":  65.95,
"rsi":  50.46,
"ret": 0.0073316 
},
{
 "date":  -2478,
"name": "GSPC.Close",
"price":  65.85,
"rsi": 56.855,
"ret": -0.0015163 
},
{
 "date":  -2477,
"name": "GSPC.Close",
"price":  66.19,
"rsi": 55.255,
"ret": 0.0051632 
},
{
 "date":  -2474,
"name": "GSPC.Close",
"price":  66.21,
"rsi": 59.435,
"ret": 0.00030216 
},
{
 "date":  -2473,
"name": "GSPC.Close",
"price":   66.4,
"rsi": 59.674,
"ret": 0.0028697 
},
{
 "date":  -2472,
"name": "GSPC.Close",
"price":  66.68,
"rsi": 61.964,
"ret": 0.0042169 
},
{
 "date":  -2471,
"name": "GSPC.Close",
"price":  66.58,
"rsi": 65.108,
"ret": -0.0014997 
},
{
 "date":  -2470,
"name": "GSPC.Close",
"price":  66.57,
"rsi": 63.102,
"ret": -0.0001502 
},
{
 "date":  -2467,
"name": "GSPC.Close",
"price":  66.85,
"rsi": 62.893,
"ret": 0.0042061 
},
{
 "date":  -2466,
"name": "GSPC.Close",
"price":  66.84,
"rsi": 66.258,
"ret": -0.00014959 
},
{
 "date":  -2465,
"name": "GSPC.Close",
"price":  67.36,
"rsi": 66.028,
"ret": 0.0077798 
},
{
 "date":  -2464,
"name": "GSPC.Close",
"price":  67.85,
"rsi": 71.563,
"ret": 0.0072743 
},
{
 "date":  -2463,
"name": "GSPC.Close",
"price":  68.28,
"rsi": 75.597,
"ret": 0.0063375 
},
{
 "date":  -2460,
"name": "GSPC.Close",
"price":  68.52,
"rsi": 78.483,
"ret": 0.0035149 
},
{
 "date":  -2459,
"name": "GSPC.Close",
"price":  68.45,
"rsi":  79.91,
"ret": -0.0010216 
},
{
 "date":  -2458,
"name": "GSPC.Close",
"price":  68.29,
"rsi": 78.279,
"ret": -0.0023375 
},
{
 "date":  -2457,
"name": "GSPC.Close",
"price":  68.77,
"rsi": 74.533,
"ret": 0.0070288 
},
{
 "date":  -2453,
"name": "GSPC.Close",
"price":  69.09,
"rsi": 77.943,
"ret": 0.0046532 
},
{
 "date":  -2452,
"name": "GSPC.Close",
"price":  69.14,
"rsi": 79.877,
"ret": 0.00072369 
},
{
 "date":  -2451,
"name": "GSPC.Close",
"price":  68.92,
"rsi":  80.17,
"ret": -0.0031819 
},
{
 "date":  -2450,
"name": "GSPC.Close",
"price":  68.89,
"rsi": 75.002,
"ret": -0.00043529 
},
{
 "date":  -2449,
"name": "GSPC.Close",
"price":  69.23,
"rsi": 74.299,
"ret": 0.0049354 
},
{
 "date":  -2446,
"name": "GSPC.Close",
"price":   69.3,
"rsi": 76.938,
"ret": 0.0010111 
},
{
 "date":  -2445,
"name": "GSPC.Close",
"price":  69.53,
"rsi": 77.452,
"ret": 0.0033189 
},
{
 "date":  -2444,
"name": "GSPC.Close",
"price":  69.72,
"rsi": 79.098,
"ret": 0.0027326 
},
{
 "date":  -2443,
"name": "GSPC.Close",
"price":  69.76,
"rsi": 80.373,
"ret": 0.00057372 
},
{
 "date":  -2442,
"name": "GSPC.Close",
"price":   69.7,
"rsi": 80.641,
"ret": -0.00086009 
},
{
 "date":  -2439,
"name": "GSPC.Close",
"price":  69.65,
"rsi": 78.902,
"ret": -0.00071736 
},
{
 "date":  -2438,
"name": "GSPC.Close",
"price":   69.8,
"rsi": 77.405,
"ret": 0.0021536 
},
{
 "date":  -2437,
"name": "GSPC.Close",
"price":  69.97,
"rsi":  78.71,
"ret": 0.0024355 
},
{
 "date":  -2436,
"name": "GSPC.Close",
"price":  70.17,
"rsi": 80.113,
"ret": 0.0028584 
},
{
 "date":  -2435,
"name": "GSPC.Close",
"price":  70.03,
"rsi": 81.645,
"ret": -0.0019952 
},
{
 "date":  -2432,
"name": "GSPC.Close",
"price":  69.53,
"rsi": 77.164,
"ret": -0.0071398 
},
{
 "date":  -2431,
"name": "GSPC.Close",
"price":  69.44,
"rsi": 63.713,
"ret": -0.0012944 
},
{
 "date":  -2430,
"name": "GSPC.Close",
"price":  70.01,
"rsi":  61.63,
"ret": 0.0082085 
},
{
 "date":  -2429,
"name": "GSPC.Close",
"price":  70.35,
"rsi": 68.625,
"ret": 0.0048564 
},
{
 "date":  -2428,
"name": "GSPC.Close",
"price":  70.52,
"rsi": 71.914,
"ret": 0.0024165 
},
{
 "date":  -2425,
"name": "GSPC.Close",
"price":  70.48,
"rsi": 73.414,
"ret": -0.00056721 
},
{
 "date":  -2424,
"name": "GSPC.Close",
"price":  70.21,
"rsi": 72.434,
"ret": -0.0038309 
},
{
 "date":  -2423,
"name": "GSPC.Close",
"price":  70.43,
"rsi": 66.023,
"ret": 0.0031335 
},
{
 "date":  -2422,
"name": "GSPC.Close",
"price":  70.25,
"rsi": 68.472,
"ret": -0.0025557 
},
{
 "date":  -2421,
"name": "GSPC.Close",
"price":  70.29,
"rsi": 64.383,
"ret": 0.0005694 
},
{
 "date":  -2418,
"name": "GSPC.Close",
"price":  69.96,
"rsi": 64.885,
"ret": -0.0046948 
},
{
 "date":  -2417,
"name": "GSPC.Close",
"price":  70.14,
"rsi": 57.667,
"ret": 0.0025729 
},
{
 "date":  -2416,
"name": "GSPC.Close",
"price":  70.14,
"rsi": 60.264,
"ret":      0 
},
{
 "date":  -2415,
"name": "GSPC.Close",
"price":   70.1,
"rsi": 60.264,
"ret": -0.00057029 
},
{
 "date":  -2414,
"name": "GSPC.Close",
"price":  70.02,
"rsi": 59.326,
"ret": -0.0011412 
},
{
 "date":  -2411,
"name": "GSPC.Close",
"price":  69.87,
"rsi": 57.402,
"ret": -0.0021422 
},
{
 "date":  -2410,
"name": "GSPC.Close",
"price":  70.01,
"rsi": 53.874,
"ret": 0.0020037 
},
{
 "date":  -2409,
"name": "GSPC.Close",
"price":  70.33,
"rsi": 56.558,
"ret": 0.0045708 
},
{
 "date":  -2407,
"name": "GSPC.Close",
"price":   70.8,
"rsi":     62,
"ret": 0.0066828 
},
{
 "date":  -2404,
"name": "GSPC.Close",
"price":  70.69,
"rsi": 68.284,
"ret": -0.0015537 
},
{
 "date":  -2403,
"name": "GSPC.Close",
"price":   70.7,
"rsi": 65.552,
"ret": 0.00014146 
},
{
 "date":  -2402,
"name": "GSPC.Close",
"price":  70.53,
"rsi": 65.686,
"ret": -0.0024045 
},
{
 "date":  -2401,
"name": "GSPC.Close",
"price":  70.58,
"rsi": 61.306,
"ret": 0.00070892 
},
{
 "date":  -2400,
"name": "GSPC.Close",
"price":  70.41,
"rsi": 62.107,
"ret": -0.0024086 
},
{
 "date":  -2397,
"name": "GSPC.Close",
"price":  69.94,
"rsi": 57.734,
"ret": -0.0066752 
},
{
 "date":  -2396,
"name": "GSPC.Close",
"price":  70.03,
"rsi":  47.73,
"ret": 0.0012868 
},
{
 "date":  -2395,
"name": "GSPC.Close",
"price":  70.41,
"rsi": 49.533,
"ret": 0.0054262 
},
{
 "date":  -2394,
"name": "GSPC.Close",
"price":  70.23,
"rsi": 56.377,
"ret": -0.0025565 
},
{
 "date":  -2393,
"name": "GSPC.Close",
"price":  70.25,
"rsi": 52.729,
"ret": 0.00028478 
},
{
 "date":  -2390,
"name": "GSPC.Close",
"price":  69.95,
"rsi": 53.092,
"ret": -0.0042705 
},
{
 "date":  -2389,
"name": "GSPC.Close",
"price":  70.02,
"rsi": 47.231,
"ret": 0.0010007 
},
{
 "date":  -2388,
"name": "GSPC.Close",
"price":  70.09,
"rsi": 48.655,
"ret": 0.00099971 
},
{
 "date":  -2387,
"name": "GSPC.Close",
"price":  70.01,
"rsi": 50.106,
"ret": -0.0011414 
},
{
 "date":  -2386,
"name": "GSPC.Close",
"price":  70.25,
"rsi": 48.422,
"ret": 0.0034281 
},
{
 "date":  -2383,
"name": "GSPC.Close",
"price":   70.2,
"rsi": 53.473,
"ret": -0.00071174 
},
{
 "date":  -2382,
"name": "GSPC.Close",
"price":  70.04,
"rsi": 52.323,
"ret": -0.0022792 
},
{
 "date":  -2381,
"name": "GSPC.Close",
"price":  69.41,
"rsi": 48.714,
"ret": -0.0089949 
},
{
 "date":  -2380,
"name": "GSPC.Close",
"price":  69.07,
"rsi": 37.691,
"ret": -0.0048984 
},
{
 "date":  -2379,
"name": "GSPC.Close",
"price":  69.37,
"rsi":  33.31,
"ret": 0.0043434 
},
{
 "date":  -2376,
"name": "GSPC.Close",
"price":  68.86,
"rsi": 39.943,
"ret": -0.0073519 
},
{
 "date":  -2375,
"name": "GSPC.Close",
"price":  69.46,
"rsi":  33.79,
"ret": 0.0087133 
},
{
 "date":  -2374,
"name": "GSPC.Close",
"price":  69.94,
"rsi": 44.602,
"ret": 0.0069105 
},
{
 "date":  -2372,
"name": "GSPC.Close",
"price":  70.22,
"rsi": 51.434,
"ret": 0.0040034 
},
{
 "date":  -2369,
"name": "GSPC.Close",
"price":  69.74,
"rsi": 54.927,
"ret": -0.0068357 
},
{
 "date":  -2368,
"name": "GSPC.Close",
"price":  70.04,
"rsi":  48.49,
"ret": 0.0043017 
},
{
 "date":  -2367,
"name": "GSPC.Close",
"price":  69.89,
"rsi": 52.256,
"ret": -0.0021416 
},
{
 "date":  -2366,
"name": "GSPC.Close",
"price":  69.76,
"rsi": 50.276,
"ret": -0.0018601 
},
{
 "date":  -2365,
"name": "GSPC.Close",
"price":  69.64,
"rsi":  48.56,
"ret": -0.0017202 
},
{
 "date":  -2362,
"name": "GSPC.Close",
"price":   69.2,
"rsi": 46.965,
"ret": -0.0063182 
},
{
 "date":  -2361,
"name": "GSPC.Close",
"price":  69.14,
"rsi": 41.576,
"ret": -0.00086705 
},
{
 "date":  -2360,
"name": "GSPC.Close",
"price":  68.93,
"rsi": 40.887,
"ret": -0.0030373 
},
{
 "date":  -2359,
"name": "GSPC.Close",
"price":  68.49,
"rsi": 38.483,
"ret": -0.0063833 
},
{
 "date":  -2358,
"name": "GSPC.Close",
"price":  68.35,
"rsi": 33.976,
"ret": -0.0020441 
},
{
 "date":  -2355,
"name": "GSPC.Close",
"price":   67.9,
"rsi": 32.665,
"ret": -0.0065838 
},
{
 "date":  -2354,
"name": "GSPC.Close",
"price":  67.91,
"rsi": 28.816,
"ret": 0.00014728 
},
{
 "date":  -2353,
"name": "GSPC.Close",
"price":  68.28,
"rsi": 29.016,
"ret": 0.0054484 
},
{
 "date":  -2352,
"name": "GSPC.Close",
"price":  68.26,
"rsi": 36.168,
"ret": -0.00029291 
},
{
 "date":  -2351,
"name": "GSPC.Close",
"price":  68.54,
"rsi": 35.957,
"ret": 0.004102 
},
{
 "date":  -2348,
"name": "GSPC.Close",
"price":  68.67,
"rsi": 41.132,
"ret": 0.0018967 
},
{
 "date":  -2347,
"name": "GSPC.Close",
"price":  69.24,
"rsi": 43.418,
"ret": 0.0083006 
},
{
 "date":  -2346,
"name": "GSPC.Close",
"price":  69.13,
"rsi": 52.186,
"ret": -0.0015887 
},
{
 "date":  -2345,
"name": "GSPC.Close",
"price":  69.07,
"rsi": 50.558,
"ret": -0.00086793 
},
{
 "date":  -2344,
"name": "GSPC.Close",
"price":   69.3,
"rsi": 49.648,
"ret": 0.00333 
},
{
 "date":  -2341,
"name": "GSPC.Close",
"price":  69.71,
"rsi":  53.13,
"ret": 0.0059163 
},
{
 "date":  -2340,
"name": "GSPC.Close",
"price":  70.17,
"rsi": 58.624,
"ret": 0.0065988 
},
{
 "date":  -2339,
"name": "GSPC.Close",
"price":  69.96,
"rsi": 63.756,
"ret": -0.0029927 
},
{
 "date":  -2338,
"name": "GSPC.Close",
"price":  70.02,
"rsi": 60.092,
"ret": 0.00085763 
},
{
 "date":  -2337,
"name": "GSPC.Close",
"price":  70.48,
"rsi": 60.785,
"ret": 0.0065696 
},
{
 "date":  -2334,
"name": "GSPC.Close",
"price":  70.59,
"rsi": 65.706,
"ret": 0.0015607 
},
{
 "date":  -2333,
"name": "GSPC.Close",
"price":  70.79,
"rsi": 66.779,
"ret": 0.0028333 
},
{
 "date":  -2332,
"name": "GSPC.Close",
"price":  71.07,
"rsi": 68.698,
"ret": 0.0039554 
},
{
 "date":  -2331,
"name": "GSPC.Close",
"price":  71.38,
"rsi": 71.205,
"ret": 0.0043619 
},
{
 "date":  -2330,
"name": "GSPC.Close",
"price":  71.49,
"rsi": 73.716,
"ret": 0.001541 
},
{
 "date":  -2327,
"name": "GSPC.Close",
"price":  71.44,
"rsi": 74.563,
"ret": -0.0006994 
},
{
 "date":  -2326,
"name": "GSPC.Close",
"price":  71.38,
"rsi": 73.405,
"ret": -0.00083987 
},
{
 "date":  -2325,
"name": "GSPC.Close",
"price":  71.29,
"rsi":  71.96,
"ret": -0.0012609 
},
{
 "date":  -2324,
"name": "GSPC.Close",
"price":  71.54,
"rsi": 69.742,
"ret": 0.0035068 
},
{
 "date":  -2323,
"name": "GSPC.Close",
"price":  71.76,
"rsi": 72.296,
"ret": 0.0030752 
},
{
 "date":  -2320,
"name": "GSPC.Close",
"price":  71.91,
"rsi": 74.348,
"ret": 0.0020903 
},
{
 "date":  -2319,
"name": "GSPC.Close",
"price":  71.52,
"rsi": 75.671,
"ret": -0.0054234 
},
{
 "date":  -2318,
"name": "GSPC.Close",
"price":  72.04,
"rsi": 66.122,
"ret": 0.0072707 
},
{
 "date":  -2317,
"name": "GSPC.Close",
"price":  72.16,
"rsi": 71.319,
"ret": 0.0016657 
},
{
 "date":  -2316,
"name": "GSPC.Close",
"price":   72.5,
"rsi": 72.372,
"ret": 0.0047118 
},
{
 "date":  -2312,
"name": "GSPC.Close",
"price":  72.66,
"rsi": 75.156,
"ret": 0.0022069 
},
{
 "date":  -2311,
"name": "GSPC.Close",
"price":  72.64,
"rsi": 76.363,
"ret": -0.00027525 
},
{
 "date":  -2310,
"name": "GSPC.Close",
"price":     73,
"rsi": 75.867,
"ret": 0.0049559 
},
{
 "date":  -2309,
"name": "GSPC.Close",
"price":  72.84,
"rsi": 78.567,
"ret": -0.0021918 
},
{
 "date":  -2306,
"name": "GSPC.Close",
"price":  72.58,
"rsi": 74.574,
"ret": -0.0035695 
},
{
 "date":  -2305,
"name": "GSPC.Close",
"price":  72.99,
"rsi": 68.483,
"ret": 0.0056489 
},
{
 "date":  -2304,
"name": "GSPC.Close",
"price":   73.2,
"rsi": 72.322,
"ret": 0.0028771 
},
{
 "date":  -2303,
"name": "GSPC.Close",
"price":  73.15,
"rsi": 74.064,
"ret": -0.00068306 
},
{
 "date":  -2302,
"name": "GSPC.Close",
"price":  73.17,
"rsi": 72.888,
"ret": 0.00027341 
},
{
 "date":  -2299,
"name": "GSPC.Close",
"price":  73.07,
"rsi": 73.072,
"ret": -0.0013667 
},
{
 "date":  -2298,
"name": "GSPC.Close",
"price":  73.12,
"rsi": 70.492,
"ret": 0.00068428 
},
{
 "date":  -2297,
"name": "GSPC.Close",
"price":   72.8,
"rsi": 71.043,
"ret": -0.0043764 
},
{
 "date":  -2296,
"name": "GSPC.Close",
"price":  73.22,
"rsi": 62.948,
"ret": 0.0057692 
},
{
 "date":  -2295,
"name": "GSPC.Close",
"price":   73.3,
"rsi": 68.088,
"ret": 0.0010926 
},
{
 "date":  -2292,
"name": "GSPC.Close",
"price":  72.96,
"rsi": 68.971,
"ret": -0.0046385 
},
{
 "date":  -2291,
"name": "GSPC.Close",
"price":   73.3,
"rsi": 61.219,
"ret": 0.0046601 
},
{
 "date":  -2290,
"name": "GSPC.Close",
"price":  72.89,
"rsi": 65.406,
"ret": -0.0055935 
},
{
 "date":  -2289,
"name": "GSPC.Close",
"price":  72.27,
"rsi": 57.363,
"ret": -0.008506 
},
{
 "date":  -2288,
"name": "GSPC.Close",
"price":  72.13,
"rsi": 47.792,
"ret": -0.0019372 
},
{
 "date":  -2285,
"name": "GSPC.Close",
"price":   71.7,
"rsi": 45.929,
"ret": -0.0059615 
},
{
 "date":  -2284,
"name": "GSPC.Close",
"price":  72.22,
"rsi": 40.682,
"ret": 0.0072524 
},
{
 "date":  -2283,
"name": "GSPC.Close",
"price":   72.3,
"rsi": 48.364,
"ret": 0.0011077 
},
{
 "date":  -2282,
"name": "GSPC.Close",
"price":  72.83,
"rsi": 49.449,
"ret": 0.0073306 
},
{
 "date":  -2281,
"name": "GSPC.Close",
"price":  72.85,
"rsi": 56.037,
"ret": 0.00027461 
},
{
 "date":  -2278,
"name": "GSPC.Close",
"price":   72.7,
"rsi": 56.269,
"ret": -0.002059 
},
{
 "date":  -2277,
"name": "GSPC.Close",
"price":   72.6,
"rsi": 53.972,
"ret": -0.0013755 
},
{
 "date":  -2276,
"name": "GSPC.Close",
"price":  71.87,
"rsi": 52.436,
"ret": -0.010055 
},
{
 "date":  -2275,
"name": "GSPC.Close",
"price":   72.2,
"rsi": 42.846,
"ret": 0.0045916 
},
{
 "date":  -2274,
"name": "GSPC.Close",
"price":  72.27,
"rsi": 47.518,
"ret": 0.00096953 
},
{
 "date":  -2271,
"name": "GSPC.Close",
"price":   72.3,
"rsi": 48.481,
"ret": 0.00041511 
},
{
 "date":  -2270,
"name": "GSPC.Close",
"price":   72.4,
"rsi": 48.913,
"ret": 0.0013831 
},
{
 "date":  -2269,
"name": "GSPC.Close",
"price":  72.97,
"rsi": 50.407,
"ret": 0.0078729 
},
{
 "date":  -2268,
"name": "GSPC.Close",
"price":  73.26,
"rsi": 57.954,
"ret": 0.0039742 
},
{
 "date":  -2267,
"name": "GSPC.Close",
"price":  73.32,
"rsi":  61.19,
"ret": 0.000819 
},
{
 "date":  -2264,
"name": "GSPC.Close",
"price":  73.38,
"rsi": 61.844,
"ret": 0.00081833 
},
{
 "date":  -2263,
"name": "GSPC.Close",
"price":  72.96,
"rsi": 62.524,
"ret": -0.0057236 
},
{
 "date":  -2262,
"name": "GSPC.Close",
"price":     73,
"rsi": 55.115,
"ret": 0.00054825 
},
{
 "date":  -2261,
"name": "GSPC.Close",
"price":  73.28,
"rsi": 55.654,
"ret": 0.0038356 
},
{
 "date":  -2260,
"name": "GSPC.Close",
"price":  74.01,
"rsi": 59.335,
"ret": 0.0099618 
},
{
 "date":  -2257,
"name": "GSPC.Close",
"price":  74.48,
"rsi": 67.021,
"ret": 0.0063505 
},
{
 "date":  -2256,
"name": "GSPC.Close",
"price":  74.46,
"rsi": 70.842,
"ret": -0.00026853 
},
{
 "date":  -2255,
"name": "GSPC.Close",
"price":   73.8,
"rsi": 70.468,
"ret": -0.0088638 
},
{
 "date":  -2254,
"name": "GSPC.Close",
"price":  74.01,
"rsi": 59.331,
"ret": 0.0028455 
},
{
 "date":  -2253,
"name": "GSPC.Close",
"price":  73.83,
"rsi": 61.421,
"ret": -0.0024321 
},
{
 "date":  -2250,
"name": "GSPC.Close",
"price":  73.45,
"rsi":  58.64,
"ret": -0.005147 
},
{
 "date":  -2248,
"name": "GSPC.Close",
"price":  72.81,
"rsi": 53.168,
"ret": -0.0087134 
},
{
 "date":  -2247,
"name": "GSPC.Close",
"price":  73.06,
"rsi": 45.471,
"ret": 0.0034336 
},
{
 "date":  -2246,
"name": "GSPC.Close",
"price":  73.36,
"rsi": 48.601,
"ret": 0.0041062 
},
{
 "date":  -2243,
"name": "GSPC.Close",
"price":  73.52,
"rsi": 52.151,
"ret": 0.002181 
},
{
 "date":  -2242,
"name": "GSPC.Close",
"price":  73.23,
"rsi": 53.976,
"ret": -0.0039445 
},
{
 "date":  -2241,
"name": "GSPC.Close",
"price":  73.29,
"rsi": 50.235,
"ret": 0.00081934 
},
{
 "date":  -2240,
"name": "GSPC.Close",
"price":  72.95,
"rsi": 50.992,
"ret": -0.0046391 
},
{
 "date":  -2239,
"name": "GSPC.Close",
"price":  72.35,
"rsi": 46.662,
"ret": -0.0082248 
},
{
 "date":  -2236,
"name": "GSPC.Close",
"price":  71.83,
"rsi": 40.177,
"ret": -0.0071873 
},
{
 "date":  -2235,
"name": "GSPC.Close",
"price":   71.9,
"rsi": 35.565,
"ret": 0.00097452 
},
{
 "date":  -2234,
"name": "GSPC.Close",
"price":  72.56,
"rsi": 36.619,
"ret": 0.0091794 
},
{
 "date":  -2233,
"name": "GSPC.Close",
"price":  71.62,
"rsi": 45.654,
"ret": -0.012955 
},
{
 "date":  -2232,
"name": "GSPC.Close",
"price":  69.61,
"rsi": 37.463,
"ret": -0.028065 
},
{
 "date":  -2228,
"name": "GSPC.Close",
"price":  72.38,
"rsi": 26.511,
"ret": 0.039793 
},
{
 "date":  -2227,
"name": "GSPC.Close",
"price":  72.25,
"rsi": 48.748,
"ret": -0.0017961 
},
{
 "date":  -2225,
"name": "GSPC.Close",
"price":  73.23,
"rsi": 48.014,
"ret": 0.013564 
},
{
 "date":  -2222,
"name": "GSPC.Close",
"price":  73.66,
"rsi": 53.678,
"ret": 0.0058719 
},
{
 "date":  -2221,
"name": "GSPC.Close",
"price":  73.62,
"rsi": 55.947,
"ret": -0.00054304 
},
{
 "date":  -2220,
"name": "GSPC.Close",
"price":   73.8,
"rsi": 55.673,
"ret": 0.002445 
},
{
 "date":  -2219,
"name": "GSPC.Close",
"price":  74.28,
"rsi": 56.698,
"ret": 0.0065041 
},
{
 "date":  -2218,
"name": "GSPC.Close",
"price":     74,
"rsi": 59.393,
"ret": -0.0037695 
},
{
 "date":  -2215,
"name": "GSPC.Close",
"price":  73.96,
"rsi": 57.158,
"ret": -0.00054054 
},
{
 "date":  -2214,
"name": "GSPC.Close",
"price":  73.99,
"rsi": 56.829,
"ret": 0.00040562 
},
{
 "date":  -2213,
"name": "GSPC.Close",
"price":   73.9,
"rsi": 57.029,
"ret": -0.0012164 
},
{
 "date":  -2212,
"name": "GSPC.Close",
"price":  73.91,
"rsi": 56.189,
"ret": 0.00013532 
},
{
 "date":  -2211,
"name": "GSPC.Close",
"price":  74.06,
"rsi": 56.266,
"ret": 0.0020295 
},
{
 "date":  -2208,
"name": "GSPC.Close",
"price":   74.3,
"rsi": 57.475,
"ret": 0.0032406 
},
{
 "date":  -2207,
"name": "GSPC.Close",
"price":  74.74,
"rsi": 59.407,
"ret": 0.0059219 
},
{
 "date":  -2206,
"name": "GSPC.Close",
"price":  74.63,
"rsi":  62.75,
"ret": -0.0014718 
},
{
 "date":  -2205,
"name": "GSPC.Close",
"price":   74.4,
"rsi": 61.389,
"ret": -0.0030819 
},
{
 "date":  -2204,
"name": "GSPC.Close",
"price":  74.28,
"rsi":  58.53,
"ret": -0.0016129 
},
{
 "date":  -2201,
"name": "GSPC.Close",
"price":  73.81,
"rsi": 57.038,
"ret": -0.0063274 
},
{
 "date":  -2200,
"name": "GSPC.Close",
"price":  73.97,
"rsi":   51.5,
"ret": 0.0021677 
},
{
 "date":  -2198,
"name": "GSPC.Close",
"price":  74.32,
"rsi": 53.167,
"ret": 0.0047316 
},
{
 "date":  -2197,
"name": "GSPC.Close",
"price":  74.44,
"rsi": 56.675,
"ret": 0.0016146 
},
{
 "date":  -2194,
"name": "GSPC.Close",
"price":  74.56,
"rsi": 57.841,
"ret": 0.001612 
},
{
 "date":  -2193,
"name": "GSPC.Close",
"price":  75.02,
"rsi": 59.029,
"ret": 0.0061695 
},
{
 "date":  -2191,
"name": "GSPC.Close",
"price":  75.43,
"rsi": 63.297,
"ret": 0.0054652 
},
{
 "date":  -2190,
"name": "GSPC.Close",
"price":   75.5,
"rsi": 66.634,
"ret": 0.00092801 
},
{
 "date":  -2187,
"name": "GSPC.Close",
"price":  75.67,
"rsi": 67.182,
"ret": 0.0022517 
},
{
 "date":  -2186,
"name": "GSPC.Close",
"price":  75.69,
"rsi": 68.535,
"ret": 0.00026431 
},
{
 "date":  -2185,
"name": "GSPC.Close",
"price":     76,
"rsi": 68.698,
"ret": 0.0040957 
},
{
 "date":  -2184,
"name": "GSPC.Close",
"price":  76.28,
"rsi": 71.196,
"ret": 0.0036842 
},
{
 "date":  -2183,
"name": "GSPC.Close",
"price":  76.24,
"rsi": 73.271,
"ret": -0.00052438 
},
{
 "date":  -2180,
"name": "GSPC.Close",
"price":  76.22,
"rsi": 72.468,
"ret": -0.00026233 
},
{
 "date":  -2179,
"name": "GSPC.Close",
"price":  76.36,
"rsi": 72.043,
"ret": 0.0018368 
},
{
 "date":  -2178,
"name": "GSPC.Close",
"price":  76.64,
"rsi": 73.227,
"ret": 0.0036668 
},
{
 "date":  -2177,
"name": "GSPC.Close",
"price":  76.55,
"rsi": 75.466,
"ret": -0.0011743 
},
{
 "date":  -2176,
"name": "GSPC.Close",
"price":  76.56,
"rsi": 73.343,
"ret": 0.00013063 
},
{
 "date":  -2173,
"name": "GSPC.Close",
"price":  76.41,
"rsi": 73.432,
"ret": -0.0019592 
},
{
 "date":  -2172,
"name": "GSPC.Close",
"price":  76.62,
"rsi": 69.658,
"ret": 0.0027483 
},
{
 "date":  -2171,
"name": "GSPC.Close",
"price":  77.03,
"rsi":  71.84,
"ret": 0.0053511 
},
{
 "date":  -2170,
"name": "GSPC.Close",
"price":  77.09,
"rsi": 75.539,
"ret": 0.00077892 
},
{
 "date":  -2169,
"name": "GSPC.Close",
"price":  77.11,
"rsi": 76.035,
"ret": 0.00025944 
},
{
 "date":  -2166,
"name": "GSPC.Close",
"price":  77.08,
"rsi": 76.208,
"ret": -0.00038905 
},
{
 "date":  -2165,
"name": "GSPC.Close",
"price":   77.1,
"rsi": 75.329,
"ret": 0.00025947 
},
{
 "date":  -2164,
"name": "GSPC.Close",
"price":  76.63,
"rsi": 75.532,
"ret": -0.006096 
},
{
 "date":  -2163,
"name": "GSPC.Close",
"price":   76.7,
"rsi": 62.528,
"ret": 0.00091348 
},
{
 "date":  -2162,
"name": "GSPC.Close",
"price":  77.04,
"rsi": 63.535,
"ret": 0.0044329 
},
{
 "date":  -2159,
"name": "GSPC.Close",
"price":  76.97,
"rsi": 68.029,
"ret": -0.00090862 
},
{
 "date":  -2158,
"name": "GSPC.Close",
"price":  76.88,
"rsi": 66.219,
"ret": -0.0011693 
},
{
 "date":  -2157,
"name": "GSPC.Close",
"price":  76.75,
"rsi": 63.867,
"ret": -0.0016909 
},
{
 "date":  -2156,
"name": "GSPC.Close",
"price":  76.93,
"rsi": 60.523,
"ret": 0.0023453 
},
{
 "date":  -2155,
"name": "GSPC.Close",
"price":  77.18,
"rsi": 63.382,
"ret": 0.0032497 
},
{
 "date":  -2152,
"name": "GSPC.Close",
"price":  77.05,
"rsi": 66.961,
"ret": -0.0016844 
},
{
 "date":  -2151,
"name": "GSPC.Close",
"price":  77.33,
"rsi": 63.486,
"ret": 0.003634 
},
{
 "date":  -2150,
"name": "GSPC.Close",
"price":  77.57,
"rsi": 67.409,
"ret": 0.0031036 
},
{
 "date":  -2149,
"name": "GSPC.Close",
"price":  77.52,
"rsi": 70.349,
"ret": -0.00064458 
},
{
 "date":  -2148,
"name": "GSPC.Close",
"price":  77.48,
"rsi": 68.954,
"ret": -0.000516 
},
{
 "date":  -2145,
"name": "GSPC.Close",
"price":  77.46,
"rsi": 67.795,
"ret": -0.00025813 
},
{
 "date":  -2144,
"name": "GSPC.Close",
"price":  77.47,
"rsi": 67.187,
"ret": 0.0001291 
},
{
 "date":  -2143,
"name": "GSPC.Close",
"price":  77.55,
"rsi": 67.344,
"ret": 0.0010327 
},
{
 "date":  -2142,
"name": "GSPC.Close",
"price":  77.62,
"rsi": 68.643,
"ret": 0.00090264 
},
{
 "date":  -2138,
"name": "GSPC.Close",
"price":  77.68,
"rsi": 69.775,
"ret": 0.000773 
},
{
 "date":  -2137,
"name": "GSPC.Close",
"price":  77.68,
"rsi":  70.75,
"ret":      0 
},
{
 "date":  -2136,
"name": "GSPC.Close",
"price":  77.87,
"rsi":  70.75,
"ret": 0.0024459 
},
{
 "date":  -2135,
"name": "GSPC.Close",
"price":  77.62,
"rsi": 73.848,
"ret": -0.0032105 
},
{
 "date":  -2134,
"name": "GSPC.Close",
"price":   77.8,
"rsi": 64.211,
"ret": 0.002319 
},
{
 "date":  -2131,
"name": "GSPC.Close",
"price":  77.97,
"rsi":   67.5,
"ret": 0.0021851 
},
{
 "date":  -2130,
"name": "GSPC.Close",
"price":  78.22,
"rsi": 70.278,
"ret": 0.0032064 
},
{
 "date":  -2129,
"name": "GSPC.Close",
"price":  78.07,
"rsi": 73.821,
"ret": -0.0019177 
},
{
 "date":  -2128,
"name": "GSPC.Close",
"price":  78.06,
"rsi": 68.541,
"ret": -0.00012809 
},
{
 "date":  -2127,
"name": "GSPC.Close",
"price":  78.31,
"rsi": 68.191,
"ret": 0.0032027 
},
{
 "date":  -2124,
"name": "GSPC.Close",
"price":  78.33,
"rsi": 72.037,
"ret": 0.0002554 
},
{
 "date":  -2123,
"name": "GSPC.Close",
"price":  78.59,
"rsi": 72.325,
"ret": 0.0033193 
},
{
 "date":  -2122,
"name": "GSPC.Close",
"price":  78.95,
"rsi": 75.816,
"ret": 0.0045807 
},
{
 "date":  -2121,
"name": "GSPC.Close",
"price":  79.08,
"rsi": 79.645,
"ret": 0.0016466 
},
{
 "date":  -2120,
"name": "GSPC.Close",
"price":  79.14,
"rsi": 80.825,
"ret": 0.00075873 
},
{
 "date":  -2117,
"name": "GSPC.Close",
"price":  79.14,
"rsi": 81.363,
"ret":      0 
},
{
 "date":  -2116,
"name": "GSPC.Close",
"price":  79.32,
"rsi": 81.363,
"ret": 0.0022745 
},
{
 "date":  -2115,
"name": "GSPC.Close",
"price":  79.38,
"rsi": 83.018,
"ret": 0.00075643 
},
{
 "date":  -2114,
"name": "GSPC.Close",
"price":   79.3,
"rsi": 83.543,
"ret": -0.0010078 
},
{
 "date":  -2113,
"name": "GSPC.Close",
"price":  78.92,
"rsi": 79.993,
"ret": -0.0047919 
},
{
 "date":  -2110,
"name": "GSPC.Close",
"price":  78.93,
"rsi": 65.712,
"ret": 0.00012671 
},
{
 "date":  -2109,
"name": "GSPC.Close",
"price":  78.79,
"rsi": 65.885,
"ret": -0.0017737 
},
{
 "date":  -2108,
"name": "GSPC.Close",
"price":  78.98,
"rsi": 61.237,
"ret": 0.0024115 
},
{
 "date":  -2107,
"name": "GSPC.Close",
"price":  79.19,
"rsi":  64.86,
"ret": 0.0026589 
},
{
 "date":  -2103,
"name": "GSPC.Close",
"price":  79.14,
"rsi": 68.378,
"ret": -0.00063139 
},
{
 "date":  -2102,
"name": "GSPC.Close",
"price":  78.98,
"rsi": 66.667,
"ret": -0.0020217 
},
{
 "date":  -2101,
"name": "GSPC.Close",
"price":  79.24,
"rsi": 61.373,
"ret": 0.003292 
},
{
 "date":  -2100,
"name": "GSPC.Close",
"price":   79.7,
"rsi": 66.086,
"ret": 0.0058051 
},
{
 "date":  -2099,
"name": "GSPC.Close",
"price":  79.94,
"rsi": 72.482,
"ret": 0.0030113 
},
{
 "date":  -2096,
"name": "GSPC.Close",
"price":  80.02,
"rsi": 75.119,
"ret": 0.0010008 
},
{
 "date":  -2095,
"name": "GSPC.Close",
"price":  79.74,
"rsi": 75.946,
"ret": -0.0034991 
},
{
 "date":  -2094,
"name": "GSPC.Close",
"price":  79.75,
"rsi": 67.488,
"ret": 0.00012541 
},
{
 "date":  -2093,
"name": "GSPC.Close",
"price":   79.7,
"rsi": 67.626,
"ret": -0.00062696 
},
{
 "date":  -2092,
"name": "GSPC.Close",
"price":  79.85,
"rsi": 66.108,
"ret": 0.0018821 
},
{
 "date":  -2089,
"name": "GSPC.Close",
"price":  79.77,
"rsi":   68.4,
"ret": -0.0010019 
},
{
 "date":  -2088,
"name": "GSPC.Close",
"price":  79.99,
"rsi": 65.843,
"ret": 0.0027579 
},
{
 "date":  -2087,
"name": "GSPC.Close",
"price":  80.09,
"rsi": 69.248,
"ret": 0.0012502 
},
{
 "date":  -2086,
"name": "GSPC.Close",
"price":   80.2,
"rsi": 70.679,
"ret": 0.0013735 
},
{
 "date":  -2085,
"name": "GSPC.Close",
"price":  80.55,
"rsi": 72.211,
"ret": 0.0043641 
},
{
 "date":  -2082,
"name": "GSPC.Close",
"price":   80.5,
"rsi":  76.43,
"ret": -0.00062073 
},
{
 "date":  -2081,
"name": "GSPC.Close",
"price":  80.54,
"rsi": 74.686,
"ret": 0.00049689 
},
{
 "date":  -2080,
"name": "GSPC.Close",
"price":  80.49,
"rsi": 75.174,
"ret": -0.00062081 
},
{
 "date":  -2079,
"name": "GSPC.Close",
"price":  80.38,
"rsi": 73.271,
"ret": -0.0013666 
},
{
 "date":  -2078,
"name": "GSPC.Close",
"price":  79.75,
"rsi": 69.127,
"ret": -0.0078378 
},
{
 "date":  -2075,
"name": "GSPC.Close",
"price":  79.35,
"rsi": 51.248,
"ret": -0.0050157 
},
{
 "date":  -2074,
"name": "GSPC.Close",
"price":   79.9,
"rsi": 43.547,
"ret": 0.0069313 
},
{
 "date":  -2073,
"name": "GSPC.Close",
"price":   79.7,
"rsi": 53.822,
"ret": -0.0025031 
},
{
 "date":  -2072,
"name": "GSPC.Close",
"price":  79.46,
"rsi": 50.241,
"ret": -0.0030113 
},
{
 "date":  -2071,
"name": "GSPC.Close",
"price":  80.17,
"rsi": 46.263,
"ret": 0.0089353 
},
{
 "date":  -2068,
"name": "GSPC.Close",
"price":  80.47,
"rsi": 57.088,
"ret": 0.003742 
},
{
 "date":  -2067,
"name": "GSPC.Close",
"price":  80.88,
"rsi": 60.691,
"ret": 0.0050951 
},
{
 "date":  -2066,
"name": "GSPC.Close",
"price":  81.06,
"rsi": 65.014,
"ret": 0.0022255 
},
{
 "date":  -2065,
"name": "GSPC.Close",
"price":  81.15,
"rsi": 66.744,
"ret": 0.0011103 
},
{
 "date":  -2064,
"name": "GSPC.Close",
"price":     81,
"rsi": 67.606,
"ret": -0.0018484 
},
{
 "date":  -2061,
"name": "GSPC.Close",
"price":   80.9,
"rsi":   64.6,
"ret": -0.0012346 
},
{
 "date":  -2060,
"name": "GSPC.Close",
"price":  81.16,
"rsi": 62.601,
"ret": 0.0032138 
},
{
 "date":  -2059,
"name": "GSPC.Close",
"price":  80.97,
"rsi": 65.583,
"ret": -0.0023411 
},
{
 "date":  -2058,
"name": "GSPC.Close",
"price":  80.86,
"rsi": 61.711,
"ret": -0.0013585 
},
{
 "date":  -2057,
"name": "GSPC.Close",
"price":   81.1,
"rsi": 59.521,
"ret": 0.0029681 
},
{
 "date":  -2054,
"name": "GSPC.Close",
"price":  80.72,
"rsi": 62.637,
"ret": -0.0046856 
},
{
 "date":  -2053,
"name": "GSPC.Close",
"price":   80.3,
"rsi": 55.368,
"ret": -0.0052032 
},
{
 "date":  -2052,
"name": "GSPC.Close",
"price":  80.66,
"rsi": 48.649,
"ret": 0.0044832 
},
{
 "date":  -2051,
"name": "GSPC.Close",
"price":  80.94,
"rsi": 53.822,
"ret": 0.0034714 
},
{
 "date":  -2050,
"name": "GSPC.Close",
"price":  80.73,
"rsi": 57.415,
"ret": -0.0025945 
},
{
 "date":  -2047,
"name": "GSPC.Close",
"price":  80.56,
"rsi":  54.02,
"ret": -0.0021058 
},
{
 "date":  -2046,
"name": "GSPC.Close",
"price":  80.39,
"rsi": 51.372,
"ret": -0.0021102 
},
{
 "date":  -2045,
"name": "GSPC.Close",
"price":  80.26,
"rsi": 48.796,
"ret": -0.0016171 
},
{
 "date":  -2044,
"name": "GSPC.Close",
"price":  80.37,
"rsi":  46.86,
"ret": 0.0013705 
},
{
 "date":  -2040,
"name": "GSPC.Close",
"price":  80.11,
"rsi": 48.714,
"ret": -0.003235 
},
{
 "date":  -2039,
"name": "GSPC.Close",
"price":   79.7,
"rsi": 44.741,
"ret": -0.005118 
},
{
 "date":  -2038,
"name": "GSPC.Close",
"price":  79.49,
"rsi": 39.299,
"ret": -0.0026349 
},
{
 "date":  -2037,
"name": "GSPC.Close",
"price":  78.67,
"rsi": 36.828,
"ret": -0.010316 
},
{
 "date":  -2036,
"name": "GSPC.Close",
"price":  79.02,
"rsi": 29.127,
"ret": 0.004449 
},
{
 "date":  -2033,
"name": "GSPC.Close",
"price":  78.64,
"rsi": 35.342,
"ret": -0.0048089 
},
{
 "date":  -2032,
"name": "GSPC.Close",
"price":  79.14,
"rsi": 32.055,
"ret": 0.0063581 
},
{
 "date":  -2031,
"name": "GSPC.Close",
"price":  79.44,
"rsi": 39.966,
"ret": 0.0037908 
},
{
 "date":  -2030,
"name": "GSPC.Close",
"price":  79.73,
"rsi": 44.167,
"ret": 0.0036506 
},
{
 "date":  -2029,
"name": "GSPC.Close",
"price":   79.6,
"rsi": 47.958,
"ret": -0.0016305 
},
{
 "date":  -2026,
"name": "GSPC.Close",
"price":  79.97,
"rsi": 46.436,
"ret": 0.0046482 
},
{
 "date":  -2025,
"name": "GSPC.Close",
"price":   80.4,
"rsi": 51.184,
"ret": 0.005377 
},
{
 "date":  -2024,
"name": "GSPC.Close",
"price":  80.81,
"rsi":  56.06,
"ret": 0.0050995 
},
{
 "date":  -2023,
"name": "GSPC.Close",
"price":  80.79,
"rsi": 60.147,
"ret": -0.00024749 
},
{
 "date":  -2022,
"name": "GSPC.Close",
"price":  80.89,
"rsi": 59.854,
"ret": 0.0012378 
},
{
 "date":  -2019,
"name": "GSPC.Close",
"price":  81.11,
"rsi": 60.878,
"ret": 0.0027197 
},
{
 "date":  -2018,
"name": "GSPC.Close",
"price":  80.77,
"rsi": 63.109,
"ret": -0.0041918 
},
{
 "date":  -2017,
"name": "GSPC.Close",
"price":  81.06,
"rsi":  57.64,
"ret": 0.0035904 
},
{
 "date":  -2016,
"name": "GSPC.Close",
"price":  81.21,
"rsi": 60.763,
"ret": 0.0018505 
},
{
 "date":  -2015,
"name": "GSPC.Close",
"price":  81.46,
"rsi": 62.311,
"ret": 0.0030784 
},
{
 "date":  -2012,
"name": "GSPC.Close",
"price":  81.64,
"rsi": 64.803,
"ret": 0.0022097 
},
{
 "date":  -2011,
"name": "GSPC.Close",
"price":  81.69,
"rsi":  66.52,
"ret": 0.00061244 
},
{
 "date":  -2010,
"name": "GSPC.Close",
"price":  82.27,
"rsi": 67.001,
"ret": 0.0071 
},
{
 "date":  -2009,
"name": "GSPC.Close",
"price":   82.6,
"rsi": 72.026,
"ret": 0.0040112 
},
{
 "date":  -2005,
"name": "GSPC.Close",
"price":  82.98,
"rsi": 74.413,
"ret": 0.0046005 
},
{
 "date":  -2004,
"name": "GSPC.Close",
"price":  83.12,
"rsi": 76.862,
"ret": 0.0016872 
},
{
 "date":  -2003,
"name": "GSPC.Close",
"price":  83.12,
"rsi": 77.709,
"ret":      0 
},
{
 "date":  -2002,
"name": "GSPC.Close",
"price":  83.22,
"rsi": 77.709,
"ret": 0.0012031 
},
{
 "date":  -2001,
"name": "GSPC.Close",
"price":  83.36,
"rsi": 78.364,
"ret": 0.0016823 
},
{
 "date":  -1998,
"name": "GSPC.Close",
"price":  83.31,
"rsi": 79.283,
"ret": -0.00059981 
},
{
 "date":  -1997,
"name": "GSPC.Close",
"price":  83.06,
"rsi": 78.009,
"ret": -0.0030008 
},
{
 "date":  -1996,
"name": "GSPC.Close",
"price":  83.34,
"rsi": 71.796,
"ret": 0.0033711 
},
{
 "date":  -1995,
"name": "GSPC.Close",
"price":  83.64,
"rsi": 74.268,
"ret": 0.0035997 
},
{
 "date":  -1994,
"name": "GSPC.Close",
"price":  84.01,
"rsi": 76.631,
"ret": 0.0044237 
},
{
 "date":  -1991,
"name": "GSPC.Close",
"price":  83.74,
"rsi": 79.172,
"ret": -0.0032139 
},
{
 "date":  -1990,
"name": "GSPC.Close",
"price":  83.54,
"rsi":  72.94,
"ret": -0.0023883 
},
{
 "date":  -1989,
"name": "GSPC.Close",
"price":  83.52,
"rsi": 68.631,
"ret": -0.00023941 
},
{
 "date":  -1988,
"name": "GSPC.Close",
"price":  83.48,
"rsi": 68.197,
"ret": -0.00047893 
},
{
 "date":  -1987,
"name": "GSPC.Close",
"price":  83.46,
"rsi": 67.281,
"ret": -0.00023958 
},
{
 "date":  -1984,
"name": "GSPC.Close",
"price":  83.08,
"rsi": 66.798,
"ret": -0.0045531 
},
{
 "date":  -1983,
"name": "GSPC.Close",
"price":  82.85,
"rsi": 58.239,
"ret": -0.0027684 
},
{
 "date":  -1982,
"name": "GSPC.Close",
"price":  82.92,
"rsi": 53.751,
"ret": 0.0008449 
},
{
 "date":  -1981,
"name": "GSPC.Close",
"price":  83.09,
"rsi":  54.89,
"ret": 0.0020502 
},
{
 "date":  -1980,
"name": "GSPC.Close",
"price":  83.18,
"rsi": 57.621,
"ret": 0.0010832 
},
{
 "date":  -1977,
"name": "GSPC.Close",
"price":     83,
"rsi": 59.035,
"ret": -0.002164 
},
{
 "date":  -1976,
"name": "GSPC.Close",
"price":  81.96,
"rsi": 55.077,
"ret": -0.01253 
},
{
 "date":  -1975,
"name": "GSPC.Close",
"price":  82.09,
"rsi": 38.864,
"ret": 0.0015861 
},
{
 "date":  -1974,
"name": "GSPC.Close",
"price":  81.34,
"rsi": 41.194,
"ret": -0.0091363 
},
{
 "date":  -1973,
"name": "GSPC.Close",
"price":  81.86,
"rsi": 33.307,
"ret": 0.0063929 
},
{
 "date":  -1970,
"name": "GSPC.Close",
"price":  81.78,
"rsi": 41.649,
"ret": -0.00097728 
},
{
 "date":  -1969,
"name": "GSPC.Close",
"price":  81.76,
"rsi": 40.803,
"ret": -0.00024456 
},
{
 "date":  -1968,
"name": "GSPC.Close",
"price":  82.17,
"rsi": 40.582,
"ret": 0.0050147 
},
{
 "date":  -1967,
"name": "GSPC.Close",
"price":  82.41,
"rsi": 46.949,
"ret": 0.0029208 
},
{
 "date":  -1966,
"name": "GSPC.Close",
"price":  82.35,
"rsi": 50.306,
"ret": -0.00072807 
},
{
 "date":  -1963,
"name": "GSPC.Close",
"price":  82.36,
"rsi": 49.463,
"ret": 0.00012143 
},
{
 "date":  -1962,
"name": "GSPC.Close",
"price":   82.4,
"rsi": 49.615,
"ret": 0.00048567 
},
{
 "date":  -1961,
"name": "GSPC.Close",
"price":  82.32,
"rsi": 50.257,
"ret": -0.00097087 
},
{
 "date":  -1960,
"name": "GSPC.Close",
"price":  81.94,
"rsi": 48.914,
"ret": -0.0046161 
},
{
 "date":  -1959,
"name": "GSPC.Close",
"price":  82.07,
"rsi": 43.031,
"ret": 0.0015865 
},
{
 "date":  -1956,
"name": "GSPC.Close",
"price":  81.91,
"rsi": 45.448,
"ret": -0.0019496 
},
{
 "date":  -1955,
"name": "GSPC.Close",
"price":  81.44,
"rsi": 43.029,
"ret": -0.005738 
},
{
 "date":  -1954,
"name": "GSPC.Close",
"price":  81.32,
"rsi": 36.826,
"ret": -0.0014735 
},
{
 "date":  -1953,
"name": "GSPC.Close",
"price":   81.7,
"rsi": 35.422,
"ret": 0.0046729 
},
{
 "date":  -1952,
"name": "GSPC.Close",
"price":  81.99,
"rsi": 42.852,
"ret": 0.0035496 
},
{
 "date":  -1949,
"name": "GSPC.Close",
"price":  81.83,
"rsi": 47.789,
"ret": -0.0019515 
},
{
 "date":  -1948,
"name": "GSPC.Close",
"price":  82.18,
"rsi": 45.456,
"ret": 0.0042772 
},
{
 "date":  -1947,
"name": "GSPC.Close",
"price":  82.31,
"rsi": 51.082,
"ret": 0.0015819 
},
{
 "date":  -1946,
"name": "GSPC.Close",
"price":  82.56,
"rsi": 53.021,
"ret": 0.0030373 
},
{
 "date":  -1945,
"name": "GSPC.Close",
"price":  82.76,
"rsi": 56.584,
"ret": 0.0024225 
},
{
 "date":  -1941,
"name": "GSPC.Close",
"price":  82.87,
"rsi": 59.246,
"ret": 0.0013291 
},
{
 "date":  -1940,
"name": "GSPC.Close",
"price":  83.05,
"rsi": 60.675,
"ret": 0.0021721 
},
{
 "date":  -1939,
"name": "GSPC.Close",
"price":   83.1,
"rsi": 62.963,
"ret": 0.00060205 
},
{
 "date":  -1938,
"name": "GSPC.Close",
"price":  83.45,
"rsi": 63.597,
"ret": 0.0042118 
},
{
 "date":  -1935,
"name": "GSPC.Close",
"price":  83.22,
"rsi": 67.755,
"ret": -0.0027561 
},
{
 "date":  -1934,
"name": "GSPC.Close",
"price":     83,
"rsi": 62.687,
"ret": -0.0026436 
},
{
 "date":  -1933,
"name": "GSPC.Close",
"price":  83.24,
"rsi": 58.203,
"ret": 0.0028916 
},
{
 "date":  -1932,
"name": "GSPC.Close",
"price":  83.79,
"rsi": 61.443,
"ret": 0.0066074 
},
{
 "date":  -1931,
"name": "GSPC.Close",
"price":  83.48,
"rsi": 67.635,
"ret": -0.0036997 
},
{
 "date":  -1928,
"name": "GSPC.Close",
"price":  83.86,
"rsi": 61.628,
"ret": 0.004552 
},
{
 "date":  -1927,
"name": "GSPC.Close",
"price":  83.89,
"rsi": 65.655,
"ret": 0.00035774 
},
{
 "date":  -1926,
"name": "GSPC.Close",
"price":  83.91,
"rsi": 65.959,
"ret": 0.00023841 
},
{
 "date":  -1925,
"name": "GSPC.Close",
"price":     84,
"rsi": 66.174,
"ret": 0.0010726 
},
{
 "date":  -1924,
"name": "GSPC.Close",
"price":  84.21,
"rsi": 67.177,
"ret": 0.0025 
},
{
 "date":  -1921,
"name": "GSPC.Close",
"price":  84.28,
"rsi": 69.454,
"ret": 0.00083126 
},
{
 "date":  -1920,
"name": "GSPC.Close",
"price":  84.24,
"rsi": 70.197,
"ret": -0.00047461 
},
{
 "date":  -1919,
"name": "GSPC.Close",
"price":  84.18,
"rsi": 69.162,
"ret": -0.00071225 
},
{
 "date":  -1918,
"name": "GSPC.Close",
"price":  84.08,
"rsi": 67.555,
"ret": -0.0011879 
},
{
 "date":  -1917,
"name": "GSPC.Close",
"price":  84.36,
"rsi": 64.849,
"ret": 0.0033302 
},
{
 "date":  -1914,
"name": "GSPC.Close",
"price":  84.74,
"rsi": 68.637,
"ret": 0.0045045 
},
{
 "date":  -1913,
"name": "GSPC.Close",
"price":  84.79,
"rsi": 72.904,
"ret": 0.00059004 
},
{
 "date":  -1912,
"name": "GSPC.Close",
"price":   84.8,
"rsi": 73.417,
"ret": 0.00011794 
},
{
 "date":  -1911,
"name": "GSPC.Close",
"price":  85.04,
"rsi": 73.525,
"ret": 0.0028302 
},
{
 "date":  -1910,
"name": "GSPC.Close",
"price":  85.22,
"rsi": 76.038,
"ret": 0.0021167 
},
{
 "date":  -1907,
"name": "GSPC.Close",
"price":  85.24,
"rsi": 77.744,
"ret": 0.00023469 
},
{
 "date":  -1906,
"name": "GSPC.Close",
"price":  84.96,
"rsi": 77.932,
"ret": -0.0032848 
},
{
 "date":  -1905,
"name": "GSPC.Close",
"price":  84.79,
"rsi": 69.127,
"ret": -0.0020009 
},
{
 "date":  -1904,
"name": "GSPC.Close",
"price":  84.25,
"rsi": 64.371,
"ret": -0.0063687 
},
{
 "date":  -1903,
"name": "GSPC.Close",
"price":  84.83,
"rsi": 52.108,
"ret": 0.0068843 
},
{
 "date":  -1900,
"name": "GSPC.Close",
"price":  84.93,
"rsi": 60.756,
"ret": 0.0011788 
},
{
 "date":  -1899,
"name": "GSPC.Close",
"price":  85.18,
"rsi": 62.029,
"ret": 0.0029436 
},
{
 "date":  -1898,
"name": "GSPC.Close",
"price":   85.1,
"rsi": 65.079,
"ret": -0.00093919 
},
{
 "date":  -1897,
"name": "GSPC.Close",
"price":  84.94,
"rsi": 63.326,
"ret": -0.0018801 
},
{
 "date":  -1896,
"name": "GSPC.Close",
"price":  85.14,
"rsi": 59.854,
"ret": 0.0023546 
},
{
 "date":  -1893,
"name": "GSPC.Close",
"price":     85,
"rsi": 62.613,
"ret": -0.0016444 
},
{
 "date":  -1892,
"name": "GSPC.Close",
"price":     85,
"rsi": 59.529,
"ret":      0 
},
{
 "date":  -1891,
"name": "GSPC.Close",
"price":  84.69,
"rsi": 59.529,
"ret": -0.0036471 
},
{
 "date":  -1890,
"name": "GSPC.Close",
"price":  84.73,
"rsi": 52.843,
"ret": 0.00047231 
},
{
 "date":  -1889,
"name": "GSPC.Close",
"price":  84.86,
"rsi": 53.568,
"ret": 0.0015343 
},
{
 "date":  -1886,
"name": "GSPC.Close",
"price":  85.18,
"rsi": 55.938,
"ret": 0.0037709 
},
{
 "date":  -1884,
"name": "GSPC.Close",
"price":  85.14,
"rsi": 61.188,
"ret": -0.00046959 
},
{
 "date":  -1883,
"name": "GSPC.Close",
"price":  85.16,
"rsi": 60.222,
"ret": 0.00023491 
},
{
 "date":  -1882,
"name": "GSPC.Close",
"price":  85.23,
"rsi": 60.558,
"ret": 0.00082198 
},
{
 "date":  -1879,
"name": "GSPC.Close",
"price":  85.19,
"rsi": 61.772,
"ret": -0.00046932 
},
{
 "date":  -1878,
"name": "GSPC.Close",
"price":  84.84,
"rsi": 60.623,
"ret": -0.0041085 
},
{
 "date":  -1877,
"name": "GSPC.Close",
"price":  85.08,
"rsi": 51.583,
"ret": 0.0028289 
},
{
 "date":  -1876,
"name": "GSPC.Close",
"price":  85.19,
"rsi": 56.386,
"ret": 0.0012929 
},
{
 "date":  -1875,
"name": "GSPC.Close",
"price":  85.21,
"rsi": 58.422,
"ret": 0.00023477 
},
{
 "date":  -1872,
"name": "GSPC.Close",
"price":  85.65,
"rsi": 58.798,
"ret": 0.0051637 
},
{
 "date":  -1871,
"name": "GSPC.Close",
"price":  86.03,
"rsi": 66.077,
"ret": 0.0044367 
},
{
 "date":  -1870,
"name": "GSPC.Close",
"price":  86.22,
"rsi": 70.865,
"ret": 0.0022085 
},
{
 "date":  -1869,
"name": "GSPC.Close",
"price":  86.18,
"rsi": 72.922,
"ret": -0.00046393 
},
{
 "date":  -1868,
"name": "GSPC.Close",
"price":  86.28,
"rsi": 71.773,
"ret": 0.0011604 
},
{
 "date":  -1865,
"name": "GSPC.Close",
"price":     86,
"rsi": 72.922,
"ret": -0.0032452 
},
{
 "date":  -1864,
"name": "GSPC.Close",
"price":  85.73,
"rsi":  64.95,
"ret": -0.0031395 
},
{
 "date":  -1863,
"name": "GSPC.Close",
"price":  85.44,
"rsi": 58.329,
"ret": -0.0033827 
},
{
 "date":  -1861,
"name": "GSPC.Close",
"price":  85.16,
"rsi": 52.176,
"ret": -0.0032772 
},
{
 "date":  -1858,
"name": "GSPC.Close",
"price":  84.42,
"rsi": 47.019,
"ret": -0.0086895 
},
{
 "date":  -1857,
"name": "GSPC.Close",
"price":  83.55,
"rsi": 36.696,
"ret": -0.010306 
},
{
 "date":  -1856,
"name": "GSPC.Close",
"price":  83.79,
"rsi": 28.714,
"ret": 0.0028725 
},
{
 "date":  -1855,
"name": "GSPC.Close",
"price":  84.18,
"rsi": 33.041,
"ret": 0.0046545 
},
{
 "date":  -1854,
"name": "GSPC.Close",
"price":  84.35,
"rsi":  39.47,
"ret": 0.0020195 
},
{
 "date":  -1851,
"name": "GSPC.Close",
"price":  84.33,
"rsi": 42.081,
"ret": -0.00023711 
},
{
 "date":  -1850,
"name": "GSPC.Close",
"price":     84,
"rsi": 41.852,
"ret": -0.0039132 
},
{
 "date":  -1849,
"name": "GSPC.Close",
"price":  83.46,
"rsi": 38.166,
"ret": -0.0064286 
},
{
 "date":  -1848,
"name": "GSPC.Close",
"price":  83.45,
"rsi": 33.039,
"ret": -0.00011982 
},
{
 "date":  -1847,
"name": "GSPC.Close",
"price":  83.66,
"rsi": 32.951,
"ret": 0.0025165 
},
{
 "date":  -1844,
"name": "GSPC.Close",
"price":  83.45,
"rsi": 36.772,
"ret": -0.0025102 
},
{
 "date":  -1843,
"name": "GSPC.Close",
"price":  83.22,
"rsi": 34.645,
"ret": -0.0027561 
},
{
 "date":  -1842,
"name": "GSPC.Close",
"price":  83.55,
"rsi": 32.433,
"ret": 0.0039654 
},
{
 "date":  -1841,
"name": "GSPC.Close",
"price":   83.9,
"rsi":   38.5,
"ret": 0.0041891 
},
{
 "date":  -1840,
"name": "GSPC.Close",
"price":  84.29,
"rsi": 44.221,
"ret": 0.0046484 
},
{
 "date":  -1837,
"name": "GSPC.Close",
"price":  84.38,
"rsi": 49.822,
"ret": 0.0010677 
},
{
 "date":  -1836,
"name": "GSPC.Close",
"price":  84.33,
"rsi": 51.044,
"ret": -0.00059256 
},
{
 "date":  -1835,
"name": "GSPC.Close",
"price":  84.15,
"rsi": 50.311,
"ret": -0.0021345 
},
{
 "date":  -1834,
"name": "GSPC.Close",
"price":  84.15,
"rsi": 47.658,
"ret":      0 
},
{
 "date":  -1830,
"name": "GSPC.Close",
"price":  84.07,
"rsi": 47.658,
"ret": -0.00095068 
},
{
 "date":  -1829,
"name": "GSPC.Close",
"price":  83.81,
"rsi": 46.397,
"ret": -0.0030927 
},
{
 "date":  -1828,
"name": "GSPC.Close",
"price":   84.3,
"rsi": 42.465,
"ret": 0.0058466 
},
{
 "date":  -1827,
"name": "GSPC.Close",
"price":  84.75,
"rsi":  50.91,
"ret": 0.0053381 
},
{
 "date":  -1823,
"name": "GSPC.Close",
"price":  84.23,
"rsi": 57.132,
"ret": -0.0061357 
},
{
 "date":  -1822,
"name": "GSPC.Close",
"price":  84.63,
"rsi": 49.348,
"ret": 0.0047489 
},
{
 "date":  -1821,
"name": "GSPC.Close",
"price":  84.89,
"rsi": 54.485,
"ret": 0.0030722 
},
{
 "date":  -1820,
"name": "GSPC.Close",
"price":  85.26,
"rsi": 57.503,
"ret": 0.0043586 
},
{
 "date":  -1819,
"name": "GSPC.Close",
"price":  85.37,
"rsi": 61.422,
"ret": 0.0012902 
},
{
 "date":  -1816,
"name": "GSPC.Close",
"price":   85.4,
"rsi": 62.528,
"ret": 0.00035141 
},
{
 "date":  -1815,
"name": "GSPC.Close",
"price":  85.61,
"rsi": 62.841,
"ret": 0.002459 
},
{
 "date":  -1814,
"name": "GSPC.Close",
"price":  85.84,
"rsi": 65.043,
"ret": 0.0026866 
},
{
 "date":  -1813,
"name": "GSPC.Close",
"price":  85.84,
"rsi": 67.326,
"ret":      0 
},
{
 "date":  -1812,
"name": "GSPC.Close",
"price":  86.21,
"rsi": 67.326,
"ret": 0.0043103 
},
{
 "date":  -1809,
"name": "GSPC.Close",
"price":  86.49,
"rsi": 70.875,
"ret": 0.0032479 
},
{
 "date":  -1808,
"name": "GSPC.Close",
"price":  86.63,
"rsi": 73.243,
"ret": 0.0016187 
},
{
 "date":  -1807,
"name": "GSPC.Close",
"price":   86.6,
"rsi": 74.366,
"ret": -0.0003463 
},
{
 "date":  -1806,
"name": "GSPC.Close",
"price":  86.52,
"rsi": 73.653,
"ret": -0.00092379 
},
{
 "date":  -1805,
"name": "GSPC.Close",
"price":  86.74,
"rsi": 71.679,
"ret": 0.0025428 
},
{
 "date":  -1802,
"name": "GSPC.Close",
"price":  86.86,
"rsi": 73.761,
"ret": 0.0013834 
},
{
 "date":  -1801,
"name": "GSPC.Close",
"price":  86.94,
"rsi": 74.848,
"ret": 0.00092102 
},
{
 "date":  -1800,
"name": "GSPC.Close",
"price":  87.23,
"rsi": 75.574,
"ret": 0.0033356 
},
{
 "date":  -1799,
"name": "GSPC.Close",
"price":  87.48,
"rsi": 78.047,
"ret": 0.002866 
},
{
 "date":  -1798,
"name": "GSPC.Close",
"price":  87.56,
"rsi": 79.934,
"ret": 0.00091449 
},
{
 "date":  -1795,
"name": "GSPC.Close",
"price":  87.58,
"rsi": 80.511,
"ret": 0.00022841 
},
{
 "date":  -1794,
"name": "GSPC.Close",
"price":  87.55,
"rsi": 80.661,
"ret": -0.00034254 
},
{
 "date":  -1793,
"name": "GSPC.Close",
"price":  87.63,
"rsi": 79.672,
"ret": 0.00091376 
},
{
 "date":  -1792,
"name": "GSPC.Close",
"price":  87.57,
"rsi": 80.364,
"ret": -0.0006847 
},
{
 "date":  -1791,
"name": "GSPC.Close",
"price":  87.29,
"rsi": 78.215,
"ret": -0.0031974 
},
{
 "date":  -1788,
"name": "GSPC.Close",
"price":  86.95,
"rsi": 68.949,
"ret": -0.0038951 
},
{
 "date":  -1787,
"name": "GSPC.Close",
"price":  87.24,
"rsi":   59.7,
"ret": 0.0033353 
},
{
 "date":  -1786,
"name": "GSPC.Close",
"price":  86.46,
"rsi": 64.121,
"ret": -0.0089409 
},
{
 "date":  -1785,
"name": "GSPC.Close",
"price":  85.54,
"rsi":  48.66,
"ret": -0.010641 
},
{
 "date":  -1784,
"name": "GSPC.Close",
"price":  86.17,
"rsi": 37.251,
"ret": 0.007365 
},
{
 "date":  -1781,
"name": "GSPC.Close",
"price":  86.07,
"rsi": 46.501,
"ret": -0.0011605 
},
{
 "date":  -1780,
"name": "GSPC.Close",
"price":  85.67,
"rsi": 45.358,
"ret": -0.0046474 
},
{
 "date":  -1779,
"name": "GSPC.Close",
"price":  85.77,
"rsi": 41.015,
"ret": 0.0011673 
},
{
 "date":  -1778,
"name": "GSPC.Close",
"price":  86.05,
"rsi": 42.498,
"ret": 0.0032645 
},
{
 "date":  -1777,
"name": "GSPC.Close",
"price":  86.21,
"rsi": 46.548,
"ret": 0.0018594 
},
{
 "date":  -1773,
"name": "GSPC.Close",
"price":  86.64,
"rsi": 48.769,
"ret": 0.0049878 
},
{
 "date":  -1772,
"name": "GSPC.Close",
"price":  87.17,
"rsi": 54.268,
"ret": 0.0061173 
},
{
 "date":  -1771,
"name": "GSPC.Close",
"price":   87.2,
"rsi": 59.971,
"ret": 0.00034416 
},
{
 "date":  -1770,
"name": "GSPC.Close",
"price":  87.43,
"rsi": 60.273,
"ret": 0.0026376 
},
{
 "date":  -1767,
"name": "GSPC.Close",
"price":  87.25,
"rsi": 62.603,
"ret": -0.0020588 
},
{
 "date":  -1766,
"name": "GSPC.Close",
"price":   87.4,
"rsi": 59.654,
"ret": 0.0017192 
},
{
 "date":  -1765,
"name": "GSPC.Close",
"price":  87.26,
"rsi":  61.29,
"ret": -0.0016018 
},
{
 "date":  -1764,
"name": "GSPC.Close",
"price":  86.98,
"rsi":  58.89,
"ret": -0.0032088 
},
{
 "date":  -1763,
"name": "GSPC.Close",
"price":   86.8,
"rsi": 54.309,
"ret": -0.0020694 
},
{
 "date":  -1760,
"name": "GSPC.Close",
"price":  86.83,
"rsi": 51.534,
"ret": 0.00034562 
},
{
 "date":  -1759,
"name": "GSPC.Close",
"price":  86.69,
"rsi": 51.974,
"ret": -0.0016123 
},
{
 "date":  -1758,
"name": "GSPC.Close",
"price":  86.54,
"rsi": 49.704,
"ret": -0.0017303 
},
{
 "date":  -1757,
"name": "GSPC.Close",
"price":   86.9,
"rsi": 47.319,
"ret": 0.0041599 
},
{
 "date":  -1756,
"name": "GSPC.Close",
"price":  87.21,
"rsi": 53.132,
"ret": 0.0035673 
},
{
 "date":  -1753,
"name": "GSPC.Close",
"price":  87.24,
"rsi": 57.482,
"ret": 0.000344 
},
{
 "date":  -1752,
"name": "GSPC.Close",
"price":  87.13,
"rsi": 57.889,
"ret": -0.0012609 
},
{
 "date":  -1751,
"name": "GSPC.Close",
"price":  87.02,
"rsi": 55.779,
"ret": -0.0012625 
},
{
 "date":  -1750,
"name": "GSPC.Close",
"price":  86.81,
"rsi": 53.672,
"ret": -0.0024132 
},
{
 "date":  -1749,
"name": "GSPC.Close",
"price":  86.84,
"rsi": 49.804,
"ret": 0.00034558 
},
{
 "date":  -1746,
"name": "GSPC.Close",
"price":  86.83,
"rsi": 50.355,
"ret": -0.00011515 
},
{
 "date":  -1745,
"name": "GSPC.Close",
"price":  86.93,
"rsi": 50.157,
"ret": 0.0011517 
},
{
 "date":  -1744,
"name": "GSPC.Close",
"price":  87.09,
"rsi": 52.177,
"ret": 0.0018406 
},
{
 "date":  -1743,
"name": "GSPC.Close",
"price":  86.84,
"rsi": 55.297,
"ret": -0.0028706 
},
{
 "date":  -1742,
"name": "GSPC.Close",
"price":   86.2,
"rsi": 49.826,
"ret": -0.0073699 
},
{
 "date":  -1739,
"name": "GSPC.Close",
"price":  86.03,
"rsi": 39.148,
"ret": -0.0019722 
},
{
 "date":  -1738,
"name": "GSPC.Close",
"price":   86.2,
"rsi": 36.887,
"ret": 0.0019761 
},
{
 "date":  -1737,
"name": "GSPC.Close",
"price":  86.16,
"rsi": 40.583,
"ret": -0.00046404 
},
{
 "date":  -1736,
"name": "GSPC.Close",
"price":  86.32,
"rsi": 39.989,
"ret": 0.001857 
},
{
 "date":  -1735,
"name": "GSPC.Close",
"price":  86.53,
"rsi": 43.545,
"ret": 0.0024328 
},
{
 "date":  -1732,
"name": "GSPC.Close",
"price":  86.53,
"rsi": 47.909,
"ret":      0 
},
{
 "date":  -1731,
"name": "GSPC.Close",
"price":   86.5,
"rsi": 47.909,
"ret": -0.0003467 
},
{
 "date":  -1730,
"name": "GSPC.Close",
"price":  86.55,
"rsi": 47.303,
"ret": 0.00057803 
},
{
 "date":  -1729,
"name": "GSPC.Close",
"price":  87.04,
"rsi": 48.472,
"ret": 0.0056615 
},
{
 "date":  -1728,
"name": "GSPC.Close",
"price":  87.56,
"rsi": 58.249,
"ret": 0.0059743 
},
{
 "date":  -1725,
"name": "GSPC.Close",
"price":  87.94,
"rsi": 65.689,
"ret": 0.0043399 
},
{
 "date":  -1724,
"name": "GSPC.Close",
"price":  88.04,
"rsi": 69.909,
"ret": 0.0011371 
},
{
 "date":  -1723,
"name": "GSPC.Close",
"price":  88.24,
"rsi": 70.923,
"ret": 0.0022717 
},
{
 "date":  -1722,
"name": "GSPC.Close",
"price":  88.15,
"rsi":  72.89,
"ret": -0.0010199 
},
{
 "date":  -1718,
"name": "GSPC.Close",
"price":  88.51,
"rsi": 70.576,
"ret": 0.0040839 
},
{
 "date":  -1717,
"name": "GSPC.Close",
"price":  88.46,
"rsi": 74.115,
"ret": -0.00056491 
},
{
 "date":  -1716,
"name": "GSPC.Close",
"price":   88.3,
"rsi": 72.805,
"ret": -0.0018087 
},
{
 "date":  -1715,
"name": "GSPC.Close",
"price":  88.78,
"rsi": 68.626,
"ret": 0.005436 
},
{
 "date":  -1714,
"name": "GSPC.Close",
"price":  88.88,
"rsi": 73.534,
"ret": 0.0011264 
},
{
 "date":  -1711,
"name": "GSPC.Close",
"price":  88.89,
"rsi": 74.432,
"ret": 0.00011251 
},
{
 "date":  -1710,
"name": "GSPC.Close",
"price":  89.04,
"rsi": 74.525,
"ret": 0.0016875 
},
{
 "date":  -1709,
"name": "GSPC.Close",
"price":     89,
"rsi": 75.939,
"ret": -0.00044924 
},
{
 "date":  -1708,
"name": "GSPC.Close",
"price":  88.93,
"rsi": 74.747,
"ret": -0.00078652 
},
{
 "date":  -1707,
"name": "GSPC.Close",
"price":  89.11,
"rsi":   72.6,
"ret": 0.0020241 
},
{
 "date":  -1704,
"name": "GSPC.Close",
"price":  89.23,
"rsi": 74.619,
"ret": 0.0013467 
},
{
 "date":  -1703,
"name": "GSPC.Close",
"price":  89.51,
"rsi": 75.895,
"ret": 0.003138 
},
{
 "date":  -1702,
"name": "GSPC.Close",
"price":  89.71,
"rsi": 78.597,
"ret": 0.0022344 
},
{
 "date":  -1701,
"name": "GSPC.Close",
"price":  89.92,
"rsi": 80.296,
"ret": 0.0023409 
},
{
 "date":  -1700,
"name": "GSPC.Close",
"price":  89.85,
"rsi": 81.919,
"ret": -0.00077847 
},
{
 "date":  -1697,
"name": "GSPC.Close",
"price":  89.66,
"rsi": 79.566,
"ret": -0.0021146 
},
{
 "date":  -1696,
"name": "GSPC.Close",
"price":  89.55,
"rsi": 73.404,
"ret": -0.0012269 
},
{
 "date":  -1695,
"name": "GSPC.Close",
"price":  89.94,
"rsi": 70.023,
"ret": 0.0043551 
},
{
 "date":  -1694,
"name": "GSPC.Close",
"price":  90.27,
"rsi": 74.506,
"ret": 0.0036691 
},
{
 "date":  -1693,
"name": "GSPC.Close",
"price":   90.1,
"rsi": 77.564,
"ret": -0.0018832 
},
{
 "date":  -1690,
"name": "GSPC.Close",
"price":  89.54,
"rsi": 72.725,
"ret": -0.0062153 
},
{
 "date":  -1689,
"name": "GSPC.Close",
"price":  89.46,
"rsi": 59.545,
"ret": -0.00089346 
},
{
 "date":  -1688,
"name": "GSPC.Close",
"price":  89.67,
"rsi":  57.93,
"ret": 0.0023474 
},
{
 "date":  -1687,
"name": "GSPC.Close",
"price":  89.18,
"rsi": 60.926,
"ret": -0.0054645 
},
{
 "date":  -1686,
"name": "GSPC.Close",
"price":  88.75,
"rsi": 51.678,
"ret": -0.0048217 
},
{
 "date":  -1683,
"name": "GSPC.Close",
"price":  88.09,
"rsi": 45.195,
"ret": -0.0074366 
},
{
 "date":  -1682,
"name": "GSPC.Close",
"price":   88.6,
"rsi": 37.432,
"ret": 0.0057895 
},
{
 "date":  -1681,
"name": "GSPC.Close",
"price":   88.3,
"rsi": 45.257,
"ret": -0.003386 
},
{
 "date":  -1680,
"name": "GSPC.Close",
"price":  87.84,
"rsi": 41.934,
"ret": -0.0052095 
},
{
 "date":  -1679,
"name": "GSPC.Close",
"price":  88.42,
"rsi": 37.401,
"ret": 0.0066029 
},
{
 "date":  -1675,
"name": "GSPC.Close",
"price":  88.72,
"rsi": 45.414,
"ret": 0.0033929 
},
{
 "date":  -1674,
"name": "GSPC.Close",
"price":  87.09,
"rsi": 49.047,
"ret": -0.018372 
},
{
 "date":  -1673,
"name": "GSPC.Close",
"price":   86.9,
"rsi":   35.3,
"ret": -0.0021817 
},
{
 "date":  -1672,
"name": "GSPC.Close",
"price":  87.11,
"rsi":   34.1,
"ret": 0.0024166 
},
{
 "date":  -1669,
"name": "GSPC.Close",
"price":  86.88,
"rsi": 36.662,
"ret": -0.0026403 
},
{
 "date":  -1668,
"name": "GSPC.Close",
"price":  85.93,
"rsi": 35.055,
"ret": -0.010935 
},
{
 "date":  -1667,
"name": "GSPC.Close",
"price":  85.04,
"rsi": 29.333,
"ret": -0.010357 
},
{
 "date":  -1666,
"name": "GSPC.Close",
"price":  84.73,
"rsi": 25.186,
"ret": -0.0036453 
},
{
 "date":  -1665,
"name": "GSPC.Close",
"price":  85.12,
"rsi": 23.917,
"ret": 0.0046029 
},
{
 "date":  -1662,
"name": "GSPC.Close",
"price":  84.01,
"rsi": 28.777,
"ret": -0.01304 
},
{
 "date":  -1661,
"name": "GSPC.Close",
"price":  84.49,
"rsi": 24.065,
"ret": 0.0057136 
},
{
 "date":  -1660,
"name": "GSPC.Close",
"price":   85.2,
"rsi": 29.445,
"ret": 0.0084034 
},
{
 "date":  -1659,
"name": "GSPC.Close",
"price":  85.74,
"rsi":   36.6,
"ret": 0.006338 
},
{
 "date":  -1658,
"name": "GSPC.Close",
"price":  85.34,
"rsi": 41.463,
"ret": -0.0046653 
},
{
 "date":  -1655,
"name": "GSPC.Close",
"price":  85.05,
"rsi": 39.072,
"ret": -0.0033982 
},
{
 "date":  -1654,
"name": "GSPC.Close",
"price":  85.21,
"rsi": 37.389,
"ret": 0.0018812 
},
{
 "date":  -1653,
"name": "GSPC.Close",
"price":  84.67,
"rsi": 38.952,
"ret": -0.0063373 
},
{
 "date":  -1652,
"name": "GSPC.Close",
"price":  83.56,
"rsi": 35.713,
"ret": -0.01311 
},
{
 "date":  -1651,
"name": "GSPC.Close",
"price":  83.06,
"rsi":  30.16,
"ret": -0.0059837 
},
{
 "date":  -1648,
"name": "GSPC.Close",
"price":   81.6,
"rsi": 28.045,
"ret": -0.017578 
},
{
 "date":  -1647,
"name": "GSPC.Close",
"price":  82.41,
"rsi": 22.978,
"ret": 0.0099265 
},
{
 "date":  -1646,
"name": "GSPC.Close",
"price":  84.12,
"rsi": 30.483,
"ret": 0.02075 
},
{
 "date":  -1645,
"name": "GSPC.Close",
"price":  84.48,
"rsi": 43.089,
"ret": 0.0042796 
},
{
 "date":  -1644,
"name": "GSPC.Close",
"price":  85.16,
"rsi": 45.337,
"ret": 0.0080492 
},
{
 "date":  -1640,
"name": "GSPC.Close",
"price":  84.99,
"rsi": 49.401,
"ret": -0.0019962 
},
{
 "date":  -1639,
"name": "GSPC.Close",
"price":  84.67,
"rsi": 48.432,
"ret": -0.0037651 
},
{
 "date":  -1638,
"name": "GSPC.Close",
"price":  85.39,
"rsi": 46.579,
"ret": 0.0085036 
},
{
 "date":  -1637,
"name": "GSPC.Close",
"price":  85.71,
"rsi": 51.111,
"ret": 0.0037475 
},
{
 "date":  -1634,
"name": "GSPC.Close",
"price":  85.69,
"rsi": 53.019,
"ret": -0.00023335 
},
{
 "date":  -1633,
"name": "GSPC.Close",
"price":  85.59,
"rsi":  52.88,
"ret": -0.001167 
},
{
 "date":  -1632,
"name": "GSPC.Close",
"price":  85.87,
"rsi": 52.145,
"ret": 0.0032714 
},
{
 "date":  -1631,
"name": "GSPC.Close",
"price":  85.72,
"rsi": 54.071,
"ret": -0.0017468 
},
{
 "date":  -1630,
"name": "GSPC.Close",
"price":  85.69,
"rsi": 52.844,
"ret": -0.00034998 
},
{
 "date":  -1627,
"name": "GSPC.Close",
"price":  85.63,
"rsi": 52.587,
"ret": -0.0007002 
},
{
 "date":  -1626,
"name": "GSPC.Close",
"price":  84.55,
"rsi": 52.042,
"ret": -0.012612 
},
{
 "date":  -1625,
"name": "GSPC.Close",
"price":  84.07,
"rsi": 43.331,
"ret": -0.0056771 
},
{
 "date":  -1624,
"name": "GSPC.Close",
"price":  83.85,
"rsi": 40.117,
"ret": -0.0026169 
},
{
 "date":  -1623,
"name": "GSPC.Close",
"price":  84.07,
"rsi":   38.7,
"ret": 0.0026237 
},
{
 "date":  -1620,
"name": "GSPC.Close",
"price":  84.05,
"rsi": 40.946,
"ret": -0.0002379 
},
{
 "date":  -1619,
"name": "GSPC.Close",
"price":  83.87,
"rsi":   40.8,
"ret": -0.0021416 
},
{
 "date":  -1618,
"name": "GSPC.Close",
"price":  84.03,
"rsi": 39.434,
"ret": 0.0019077 
},
{
 "date":  -1617,
"name": "GSPC.Close",
"price":  84.68,
"rsi": 41.315,
"ret": 0.0077353 
},
{
 "date":  -1616,
"name": "GSPC.Close",
"price":  85.25,
"rsi": 48.335,
"ret": 0.0067312 
},
{
 "date":  -1613,
"name": "GSPC.Close",
"price":  85.42,
"rsi": 53.579,
"ret": 0.0019941 
},
{
 "date":  -1612,
"name": "GSPC.Close",
"price":  85.46,
"rsi": 55.044,
"ret": 0.00046827 
},
{
 "date":  -1611,
"name": "GSPC.Close",
"price":  85.79,
"rsi": 55.401,
"ret": 0.0038615 
},
{
 "date":  -1610,
"name": "GSPC.Close",
"price":  85.79,
"rsi": 58.339,
"ret":      0 
},
{
 "date":  -1609,
"name": "GSPC.Close",
"price":  86.07,
"rsi": 58.339,
"ret": 0.0032638 
},
{
 "date":  -1606,
"name": "GSPC.Close",
"price":  85.86,
"rsi": 60.875,
"ret": -0.0024399 
},
{
 "date":  -1605,
"name": "GSPC.Close",
"price":  85.87,
"rsi": 58.022,
"ret": 0.00011647 
},
{
 "date":  -1604,
"name": "GSPC.Close",
"price":  86.13,
"rsi": 58.123,
"ret": 0.0030278 
},
{
 "date":  -1603,
"name": "GSPC.Close",
"price":  86.38,
"rsi": 60.757,
"ret": 0.0029026 
},
{
 "date":  -1602,
"name": "GSPC.Close",
"price":  86.77,
"rsi": 63.157,
"ret": 0.0045149 
},
{
 "date":  -1599,
"name": "GSPC.Close",
"price":  86.87,
"rsi": 66.589,
"ret": 0.0011525 
},
{
 "date":  -1598,
"name": "GSPC.Close",
"price":  87.04,
"rsi": 67.427,
"ret": 0.0019569 
},
{
 "date":  -1597,
"name": "GSPC.Close",
"price":  86.99,
"rsi": 68.857,
"ret": -0.00057445 
},
{
 "date":  -1596,
"name": "GSPC.Close",
"price":  86.79,
"rsi": 67.913,
"ret": -0.0022991 
},
{
 "date":  -1595,
"name": "GSPC.Close",
"price":  86.69,
"rsi": 64.125,
"ret": -0.0011522 
},
{
 "date":  -1592,
"name": "GSPC.Close",
"price":  86.56,
"rsi": 62.255,
"ret": -0.0014996 
},
{
 "date":  -1591,
"name": "GSPC.Close",
"price":  86.71,
"rsi": 59.813,
"ret": 0.0017329 
},
{
 "date":  -1590,
"name": "GSPC.Close",
"price":  86.81,
"rsi":  61.68,
"ret": 0.0011533 
},
{
 "date":  -1589,
"name": "GSPC.Close",
"price":  87.14,
"rsi": 62.918,
"ret": 0.0038014 
},
{
 "date":  -1588,
"name": "GSPC.Close",
"price":   87.2,
"rsi": 66.735,
"ret": 0.00068855 
},
{
 "date":  -1585,
"name": "GSPC.Close",
"price":  87.21,
"rsi": 67.392,
"ret": 0.00011468 
},
{
 "date":  -1584,
"name": "GSPC.Close",
"price":  87.17,
"rsi": 67.508,
"ret": -0.00045866 
},
{
 "date":  -1583,
"name": "GSPC.Close",
"price":  87.17,
"rsi": 66.495,
"ret":      0 
},
{
 "date":  -1582,
"name": "GSPC.Close",
"price":  87.65,
"rsi": 66.495,
"ret": 0.0055065 
},
{
 "date":  -1581,
"name": "GSPC.Close",
"price":  88.06,
"rsi":  72.28,
"ret": 0.0046777 
},
{
 "date":  -1577,
"name": "GSPC.Close",
"price":  88.36,
"rsi": 76.079,
"ret": 0.0034068 
},
{
 "date":  -1576,
"name": "GSPC.Close",
"price":  88.66,
"rsi":  78.41,
"ret": 0.0033952 
},
{
 "date":  -1575,
"name": "GSPC.Close",
"price":  88.89,
"rsi": 80.461,
"ret": 0.0025942 
},
{
 "date":  -1574,
"name": "GSPC.Close",
"price":  89.12,
"rsi": 81.882,
"ret": 0.0025875 
},
{
 "date":  -1571,
"name": "GSPC.Close",
"price":  89.38,
"rsi": 83.198,
"ret": 0.0029174 
},
{
 "date":  -1570,
"name": "GSPC.Close",
"price":  89.03,
"rsi": 84.563,
"ret": -0.0039159 
},
{
 "date":  -1569,
"name": "GSPC.Close",
"price":  89.52,
"rsi": 75.653,
"ret": 0.0055038 
},
{
 "date":  -1568,
"name": "GSPC.Close",
"price":  90.02,
"rsi": 78.991,
"ret": 0.0055853 
},
{
 "date":  -1567,
"name": "GSPC.Close",
"price":  90.05,
"rsi": 81.741,
"ret": 0.00033326 
},
{
 "date":  -1564,
"name": "GSPC.Close",
"price":  90.08,
"rsi": 81.894,
"ret": 0.00033315 
},
{
 "date":  -1563,
"name": "GSPC.Close",
"price":  89.81,
"rsi": 82.056,
"ret": -0.0029973 
},
{
 "date":  -1562,
"name": "GSPC.Close",
"price":  90.22,
"rsi": 75.505,
"ret": 0.0045652 
},
{
 "date":  -1561,
"name": "GSPC.Close",
"price":  89.86,
"rsi": 78.334,
"ret": -0.0039902 
},
{
 "date":  -1560,
"name": "GSPC.Close",
"price":  90.02,
"rsi": 70.621,
"ret": 0.0017805 
},
{
 "date":  -1557,
"name": "GSPC.Close",
"price":  90.65,
"rsi": 71.944,
"ret": 0.0069984 
},
{
 "date":  -1556,
"name": "GSPC.Close",
"price":  90.43,
"rsi":  76.44,
"ret": -0.0024269 
},
{
 "date":  -1555,
"name": "GSPC.Close",
"price":  90.02,
"rsi": 72.095,
"ret": -0.0045339 
},
{
 "date":  -1554,
"name": "GSPC.Close",
"price":  89.96,
"rsi": 64.713,
"ret": -0.00066652 
},
{
 "date":  -1553,
"name": "GSPC.Close",
"price":   89.9,
"rsi": 63.685,
"ret": -0.00066696 
},
{
 "date":  -1550,
"name": "GSPC.Close",
"price":  90.08,
"rsi": 62.614,
"ret": 0.0020022 
},
{
 "date":  -1549,
"name": "GSPC.Close",
"price":  90.63,
"rsi":  64.54,
"ret": 0.0061057 
},
{
 "date":  -1548,
"name": "GSPC.Close",
"price":  90.54,
"rsi": 69.681,
"ret": -0.00099305 
},
{
 "date":  -1547,
"name": "GSPC.Close",
"price":  90.47,
"rsi": 67.945,
"ret": -0.00077314 
},
{
 "date":  -1546,
"name": "GSPC.Close",
"price":  90.85,
"rsi": 66.556,
"ret": 0.0042003 
},
{
 "date":  -1543,
"name": "GSPC.Close",
"price":  91.37,
"rsi": 70.126,
"ret": 0.0057237 
},
{
 "date":  -1542,
"name": "GSPC.Close",
"price":  91.35,
"rsi": 74.187,
"ret": -0.00021889 
},
{
 "date":  -1541,
"name": "GSPC.Close",
"price":  91.34,
"rsi": 73.771,
"ret": -0.00010947 
},
{
 "date":  -1540,
"name": "GSPC.Close",
"price":  91.19,
"rsi":  73.55,
"ret": -0.0016422 
},
{
 "date":  -1539,
"name": "GSPC.Close",
"price":  91.38,
"rsi": 70.144,
"ret": 0.0020836 
},
{
 "date":  -1536,
"name": "GSPC.Close",
"price":  91.68,
"rsi": 71.918,
"ret": 0.003283 
},
{
 "date":  -1535,
"name": "GSPC.Close",
"price":   91.8,
"rsi": 74.494,
"ret": 0.0013089 
},
{
 "date":  -1534,
"name": "GSPC.Close",
"price":  91.78,
"rsi": 75.464,
"ret": -0.00021786 
},
{
 "date":  -1533,
"name": "GSPC.Close",
"price":  91.94,
"rsi": 74.952,
"ret": 0.0017433 
},
{
 "date":  -1532,
"name": "GSPC.Close",
"price":  91.98,
"rsi": 76.334,
"ret": 0.00043507 
},
{
 "date":  -1529,
"name": "GSPC.Close",
"price":  91.67,
"rsi": 76.681,
"ret": -0.0033703 
},
{
 "date":  -1528,
"name": "GSPC.Close",
"price":   92.2,
"rsi": 68.333,
"ret": 0.0057816 
},
{
 "date":  -1527,
"name": "GSPC.Close",
"price":  92.51,
"rsi": 73.621,
"ret": 0.0033623 
},
{
 "date":  -1526,
"name": "GSPC.Close",
"price":  92.21,
"rsi": 76.131,
"ret": -0.0032429 
},
{
 "date":  -1525,
"name": "GSPC.Close",
"price":  92.42,
"rsi": 69.262,
"ret": 0.0022774 
},
{
 "date":  -1522,
"name": "GSPC.Close",
"price":  92.23,
"rsi": 71.219,
"ret": -0.0020558 
},
{
 "date":  -1520,
"name": "GSPC.Close",
"price":  92.31,
"rsi": 67.058,
"ret": 0.0008674 
},
{
 "date":  -1519,
"name": "GSPC.Close",
"price":  92.46,
"rsi": 67.908,
"ret": 0.001625 
},
{
 "date":  -1518,
"name": "GSPC.Close",
"price":  92.37,
"rsi": 69.498,
"ret": -0.00097339 
},
{
 "date":  -1515,
"name": "GSPC.Close",
"price":  92.23,
"rsi": 67.343,
"ret": -0.0015156 
},
{
 "date":  -1514,
"name": "GSPC.Close",
"price":  91.93,
"rsi": 64.017,
"ret": -0.0032527 
},
{
 "date":  -1513,
"name": "GSPC.Close",
"price":  91.83,
"rsi": 57.467,
"ret": -0.0010878 
},
{
 "date":  -1512,
"name": "GSPC.Close",
"price":  92.11,
"rsi": 55.431,
"ret": 0.0030491 
},
{
 "date":  -1511,
"name": "GSPC.Close",
"price":  92.55,
"rsi": 59.733,
"ret": 0.0047769 
},
{
 "date":  -1508,
"name": "GSPC.Close",
"price":  92.63,
"rsi": 65.386,
"ret": 0.0008644 
},
{
 "date":  -1507,
"name": "GSPC.Close",
"price":  92.41,
"rsi": 66.312,
"ret": -0.002375 
},
{
 "date":  -1506,
"name": "GSPC.Close",
"price":   92.6,
"rsi": 61.444,
"ret": 0.0020561 
},
{
 "date":  -1505,
"name": "GSPC.Close",
"price":  92.22,
"rsi": 63.908,
"ret": -0.0041037 
},
{
 "date":  -1504,
"name": "GSPC.Close",
"price":  92.24,
"rsi": 56.174,
"ret": 0.00021687 
},
{
 "date":  -1501,
"name": "GSPC.Close",
"price":  91.64,
"rsi": 56.473,
"ret": -0.0065048 
},
{
 "date":  -1500,
"name": "GSPC.Close",
"price":  91.78,
"rsi": 46.286,
"ret": 0.0015277 
},
{
 "date":  -1499,
"name": "GSPC.Close",
"price":  91.94,
"rsi": 48.615,
"ret": 0.0017433 
},
{
 "date":  -1497,
"name": "GSPC.Close",
"price":  92.03,
"rsi": 51.218,
"ret": 0.0009789 
},
{
 "date":  -1494,
"name": "GSPC.Close",
"price":   91.8,
"rsi": 52.671,
"ret": -0.0024992 
},
{
 "date":  -1493,
"name": "GSPC.Close",
"price":  91.61,
"rsi": 48.681,
"ret": -0.0020697 
},
{
 "date":  -1492,
"name": "GSPC.Close",
"price":   91.5,
"rsi": 45.608,
"ret": -0.0012007 
},
{
 "date":  -1491,
"name": "GSPC.Close",
"price":  91.21,
"rsi": 43.881,
"ret": -0.0031694 
},
{
 "date":  -1490,
"name": "GSPC.Close",
"price":  91.27,
"rsi": 39.621,
"ret": 0.00065782 
},
{
 "date":  -1487,
"name": "GSPC.Close",
"price":  90.59,
"rsi": 40.899,
"ret": -0.0074504 
},
{
 "date":  -1486,
"name": "GSPC.Close",
"price":  91.39,
"rsi":   32.5,
"ret": 0.008831 
},
{
 "date":  -1485,
"name": "GSPC.Close",
"price":  91.28,
"rsi": 46.436,
"ret": -0.0012036 
},
{
 "date":  -1484,
"name": "GSPC.Close",
"price":  91.56,
"rsi": 45.059,
"ret": 0.0030675 
},
{
 "date":  -1483,
"name": "GSPC.Close",
"price":   91.8,
"rsi": 49.191,
"ret": 0.0026212 
},
{
 "date":  -1480,
"name": "GSPC.Close",
"price":  91.83,
"rsi": 52.489,
"ret": 0.0003268 
},
{
 "date":  -1479,
"name": "GSPC.Close",
"price":  91.88,
"rsi":   52.9,
"ret": 0.00054448 
},
{
 "date":  -1478,
"name": "GSPC.Close",
"price":  92.02,
"rsi": 53.622,
"ret": 0.0015237 
},
{
 "date":  -1477,
"name": "GSPC.Close",
"price":  92.12,
"rsi": 55.668,
"ret": 0.0010867 
},
{
 "date":  -1476,
"name": "GSPC.Close",
"price":  92.08,
"rsi": 57.124,
"ret": -0.00043422 
},
{
 "date":  -1473,
"name": "GSPC.Close",
"price":  91.65,
"rsi": 56.327,
"ret": -0.0046699 
},
{
 "date":  -1472,
"name": "GSPC.Close",
"price":  92.01,
"rsi": 48.497,
"ret": 0.003928 
},
{
 "date":  -1471,
"name": "GSPC.Close",
"price":  92.29,
"rsi": 54.233,
"ret": 0.0030431 
},
{
 "date":  -1470,
"name": "GSPC.Close",
"price":  92.19,
"rsi": 58.138,
"ret": -0.0010835 
},
{
 "date":  -1466,
"name": "GSPC.Close",
"price":  91.52,
"rsi": 56.291,
"ret": -0.0072676 
},
{
 "date":  -1465,
"name": "GSPC.Close",
"price":  91.53,
"rsi": 45.792,
"ret": 0.00010927 
},
{
 "date":  -1464,
"name": "GSPC.Close",
"price":  91.81,
"rsi": 45.954,
"ret": 0.0030591 
},
{
 "date":  -1463,
"name": "GSPC.Close",
"price":   92.2,
"rsi": 50.423,
"ret": 0.0042479 
},
{
 "date":  -1462,
"name": "GSPC.Close",
"price":  92.43,
"rsi": 55.892,
"ret": 0.0024946 
},
{
 "date":  -1459,
"name": "GSPC.Close",
"price":  92.18,
"rsi": 58.781,
"ret": -0.0027047 
},
{
 "date":  -1458,
"name": "GSPC.Close",
"price":  92.26,
"rsi": 54.596,
"ret": 0.00086787 
},
{
 "date":  -1457,
"name": "GSPC.Close",
"price":  92.85,
"rsi": 55.683,
"ret": 0.006395 
},
{
 "date":  -1456,
"name": "GSPC.Close",
"price":  93.06,
"rsi": 62.765,
"ret": 0.0022617 
},
{
 "date":  -1455,
"name": "GSPC.Close",
"price":  93.14,
"rsi": 64.914,
"ret": 0.00085966 
},
{
 "date":  -1452,
"name": "GSPC.Close",
"price":  93.33,
"rsi": 65.726,
"ret": 0.0020399 
},
{
 "date":  -1451,
"name": "GSPC.Close",
"price":  93.41,
"rsi":  67.64,
"ret": 0.00085717 
},
{
 "date":  -1450,
"name": "GSPC.Close",
"price":  93.19,
"rsi":  68.44,
"ret": -0.0023552 
},
{
 "date":  -1449,
"name": "GSPC.Close",
"price":  93.36,
"rsi": 63.774,
"ret": 0.0018242 
},
{
 "date":  -1448,
"name": "GSPC.Close",
"price":   93.5,
"rsi": 65.719,
"ret": 0.0014996 
},
{
 "date":  -1445,
"name": "GSPC.Close",
"price":  93.77,
"rsi": 67.277,
"ret": 0.0028877 
},
{
 "date":  -1444,
"name": "GSPC.Close",
"price":  93.95,
"rsi": 70.099,
"ret": 0.0019196 
},
{
 "date":  -1443,
"name": "GSPC.Close",
"price":  93.69,
"rsi": 71.843,
"ret": -0.0027674 
},
{
 "date":  -1442,
"name": "GSPC.Close",
"price":  93.36,
"rsi": 65.868,
"ret": -0.0035223 
},
{
 "date":  -1441,
"name": "GSPC.Close",
"price":  93.47,
"rsi": 59.145,
"ret": 0.0011782 
},
{
 "date":  -1438,
"name": "GSPC.Close",
"price":  93.71,
"rsi": 60.589,
"ret": 0.0025677 
},
{
 "date":  -1437,
"name": "GSPC.Close",
"price":  93.85,
"rsi": 63.611,
"ret": 0.001494 
},
{
 "date":  -1436,
"name": "GSPC.Close",
"price":   93.7,
"rsi": 65.283,
"ret": -0.0015983 
},
{
 "date":  -1435,
"name": "GSPC.Close",
"price":  93.67,
"rsi": 61.996,
"ret": -0.00032017 
},
{
 "date":  -1434,
"name": "GSPC.Close",
"price":  93.31,
"rsi": 61.331,
"ret": -0.0038433 
},
{
 "date":  -1431,
"name": "GSPC.Close",
"price":  92.88,
"rsi": 53.862,
"ret": -0.0046083 
},
{
 "date":  -1430,
"name": "GSPC.Close",
"price":  92.16,
"rsi": 46.567,
"ret": -0.0077519 
},
{
 "date":  -1429,
"name": "GSPC.Close",
"price":  92.53,
"rsi": 37.427,
"ret": 0.0040148 
},
{
 "date":  -1428,
"name": "GSPC.Close",
"price":  92.65,
"rsi": 43.558,
"ret": 0.0012969 
},
{
 "date":  -1427,
"name": "GSPC.Close",
"price":  93.26,
"rsi": 45.426,
"ret": 0.0065839 
},
{
 "date":  -1424,
"name": "GSPC.Close",
"price":  93.59,
"rsi": 53.795,
"ret": 0.0035385 
},
{
 "date":  -1423,
"name": "GSPC.Close",
"price":  93.55,
"rsi": 57.585,
"ret": -0.0004274 
},
{
 "date":  -1422,
"name": "GSPC.Close",
"price":  94.06,
"rsi": 56.975,
"ret": 0.0054516 
},
{
 "date":  -1421,
"name": "GSPC.Close",
"price":  93.83,
"rsi": 62.439,
"ret": -0.0024452 
},
{
 "date":  -1420,
"name": "GSPC.Close",
"price":  93.81,
"rsi": 58.812,
"ret": -0.00021315 
},
{
 "date":  -1417,
"name": "GSPC.Close",
"price":  93.53,
"rsi": 58.493,
"ret": -0.0029848 
},
{
 "date":  -1416,
"name": "GSPC.Close",
"price":  93.17,
"rsi": 54.082,
"ret": -0.003849 
},
{
 "date":  -1415,
"name": "GSPC.Close",
"price":  93.16,
"rsi": 48.968,
"ret": -0.00010733 
},
{
 "date":  -1414,
"name": "GSPC.Close",
"price":  92.66,
"rsi":  48.83,
"ret": -0.0053671 
},
{
 "date":  -1413,
"name": "GSPC.Close",
"price":  92.41,
"rsi": 42.392,
"ret": -0.002698 
},
{
 "date":  -1410,
"name": "GSPC.Close",
"price":  91.87,
"rsi": 39.582,
"ret": -0.0058435 
},
{
 "date":  -1408,
"name": "GSPC.Close",
"price":  91.48,
"rsi": 34.293,
"ret": -0.0042451 
},
{
 "date":  -1407,
"name": "GSPC.Close",
"price":  90.89,
"rsi": 31.065,
"ret": -0.0064495 
},
{
 "date":  -1406,
"name": "GSPC.Close",
"price":  91.14,
"rsi": 26.935,
"ret": 0.0027506 
},
{
 "date":  -1403,
"name": "GSPC.Close",
"price":  91.22,
"rsi": 31.114,
"ret": 0.00087777 
},
{
 "date":  -1402,
"name": "GSPC.Close",
"price":  90.06,
"rsi": 32.446,
"ret": -0.012717 
},
{
 "date":  -1401,
"name": "GSPC.Close",
"price":  89.15,
"rsi": 24.923,
"ret": -0.010104 
},
{
 "date":  -1400,
"name": "GSPC.Close",
"price":  89.47,
"rsi":  20.84,
"ret": 0.0035895 
},
{
 "date":  -1399,
"name": "GSPC.Close",
"price":  89.24,
"rsi": 25.464,
"ret": -0.0025707 
},
{
 "date":  -1396,
"name": "GSPC.Close",
"price":  88.04,
"rsi": 24.362,
"ret": -0.013447 
},
{
 "date":  -1395,
"name": "GSPC.Close",
"price":  88.18,
"rsi": 19.599,
"ret": 0.0015902 
},
{
 "date":  -1394,
"name": "GSPC.Close",
"price":  88.96,
"rsi": 21.527,
"ret": 0.0088455 
},
{
 "date":  -1393,
"name": "GSPC.Close",
"price":  88.96,
"rsi": 31.396,
"ret":      0 
},
{
 "date":  -1392,
"name": "GSPC.Close",
"price":  88.85,
"rsi": 31.396,
"ret": -0.0012365 
},
{
 "date":  -1389,
"name": "GSPC.Close",
"price":  87.85,
"rsi": 30.763,
"ret": -0.011255 
},
{
 "date":  -1388,
"name": "GSPC.Close",
"price":  87.35,
"rsi": 25.693,
"ret": -0.0056915 
},
{
 "date":  -1387,
"name": "GSPC.Close",
"price":  87.86,
"rsi": 23.599,
"ret": 0.0058386 
},
{
 "date":  -1386,
"name": "GSPC.Close",
"price":  88.17,
"rsi": 29.877,
"ret": 0.0035283 
},
{
 "date":  -1385,
"name": "GSPC.Close",
"price":  88.53,
"rsi": 33.457,
"ret": 0.004083 
},
{
 "date":  -1382,
"name": "GSPC.Close",
"price":   89.2,
"rsi":  37.45,
"ret": 0.0075681 
},
{
 "date":  -1381,
"name": "GSPC.Close",
"price":  89.46,
"rsi": 44.166,
"ret": 0.0029148 
},
{
 "date":  -1380,
"name": "GSPC.Close",
"price":  89.13,
"rsi": 46.563,
"ret": -0.0036888 
},
{
 "date":  -1379,
"name": "GSPC.Close",
"price":  89.29,
"rsi": 43.982,
"ret": 0.0017951 
},
{
 "date":  -1378,
"name": "GSPC.Close",
"price":  89.54,
"rsi": 45.558,
"ret": 0.0027999 
},
{
 "date":  -1375,
"name": "GSPC.Close",
"price":  89.62,
"rsi": 48.019,
"ret": 0.00089346 
},
{
 "date":  -1374,
"name": "GSPC.Close",
"price":  89.27,
"rsi": 48.816,
"ret": -0.0039054 
},
{
 "date":  -1373,
"name": "GSPC.Close",
"price":  88.78,
"rsi": 45.526,
"ret": -0.005489 
},
{
 "date":  -1372,
"name": "GSPC.Close",
"price":  89.23,
"rsi": 41.327,
"ret": 0.0050687 
},
{
 "date":  -1371,
"name": "GSPC.Close",
"price":  89.94,
"rsi": 46.232,
"ret": 0.007957 
},
{
 "date":  -1368,
"name": "GSPC.Close",
"price":  90.76,
"rsi": 52.919,
"ret": 0.0091172 
},
{
 "date":  -1367,
"name": "GSPC.Close",
"price":  91.31,
"rsi": 59.227,
"ret": 0.0060599 
},
{
 "date":  -1366,
"name": "GSPC.Close",
"price":  91.56,
"rsi": 62.824,
"ret": 0.0027379 
},
{
 "date":  -1365,
"name": "GSPC.Close",
"price":  91.76,
"rsi": 64.364,
"ret": 0.0021844 
},
{
 "date":  -1361,
"name": "GSPC.Close",
"price":  91.79,
"rsi": 65.591,
"ret": 0.00032694 
},
{
 "date":  -1360,
"name": "GSPC.Close",
"price":  91.45,
"rsi": 65.781,
"ret": -0.0037041 
},
{
 "date":  -1359,
"name": "GSPC.Close",
"price":  91.54,
"rsi":  61.62,
"ret": 0.00098414 
},
{
 "date":  -1358,
"name": "GSPC.Close",
"price":  91.87,
"rsi":   62.3,
"ret": 0.003605 
},
{
 "date":  -1357,
"name": "GSPC.Close",
"price":  91.99,
"rsi": 64.764,
"ret": 0.0013062 
},
{
 "date":  -1354,
"name": "GSPC.Close",
"price":  91.58,
"rsi": 65.644,
"ret": -0.004457 
},
{
 "date":  -1353,
"name": "GSPC.Close",
"price":  91.57,
"rsi": 60.122,
"ret": -0.00010919 
},
{
 "date":  -1352,
"name": "GSPC.Close",
"price":  92.08,
"rsi":  59.99,
"ret": 0.0055695 
},
{
 "date":  -1351,
"name": "GSPC.Close",
"price":  92.42,
"rsi": 64.311,
"ret": 0.0036924 
},
{
 "date":  -1350,
"name": "GSPC.Close",
"price":  92.27,
"rsi": 66.879,
"ret": -0.001623 
},
{
 "date":  -1347,
"name": "GSPC.Close",
"price":  92.08,
"rsi": 64.668,
"ret": -0.0020592 
},
{
 "date":  -1346,
"name": "GSPC.Close",
"price":  91.99,
"rsi": 61.878,
"ret": -0.00097741 
},
{
 "date":  -1345,
"name": "GSPC.Close",
"price":  91.76,
"rsi": 60.545,
"ret": -0.0025003 
},
{
 "date":  -1344,
"name": "GSPC.Close",
"price":  91.13,
"rsi": 57.157,
"ret": -0.0068657 
},
{
 "date":  -1343,
"name": "GSPC.Close",
"price":  91.06,
"rsi": 49.059,
"ret": -0.00076813 
},
{
 "date":  -1340,
"name": "GSPC.Close",
"price":   90.9,
"rsi": 48.241,
"ret": -0.0017571 
},
{
 "date":  -1339,
"name": "GSPC.Close",
"price":  89.85,
"rsi": 46.339,
"ret": -0.011551 
},
{
 "date":  -1338,
"name": "GSPC.Close",
"price":  89.39,
"rsi": 36.243,
"ret": -0.0051196 
},
{
 "date":  -1337,
"name": "GSPC.Close",
"price":  87.93,
"rsi": 32.864,
"ret": -0.016333 
},
{
 "date":  -1336,
"name": "GSPC.Close",
"price":  87.84,
"rsi": 24.923,
"ret": -0.0010235 
},
{
 "date":  -1333,
"name": "GSPC.Close",
"price":  86.32,
"rsi":  24.53,
"ret": -0.017304 
},
{
 "date":  -1332,
"name": "GSPC.Close",
"price":  87.08,
"rsi": 19.058,
"ret": 0.0088044 
},
{
 "date":  -1331,
"name": "GSPC.Close",
"price":  87.23,
"rsi": 27.738,
"ret": 0.0017226 
},
{
 "date":  -1330,
"name": "GSPC.Close",
"price":  86.23,
"rsi": 29.348,
"ret": -0.011464 
},
{
 "date":  -1329,
"name": "GSPC.Close",
"price":  85.47,
"rsi":   25.3,
"ret": -0.0088136 
},
{
 "date":  -1326,
"name": "GSPC.Close",
"price":  84.41,
"rsi": 22.734,
"ret": -0.012402 
},
{
 "date":  -1325,
"name": "GSPC.Close",
"price":  83.63,
"rsi": 19.728,
"ret": -0.0092406 
},
{
 "date":  -1324,
"name": "GSPC.Close",
"price":  85.12,
"rsi": 17.857,
"ret": 0.017817 
},
{
 "date":  -1323,
"name": "GSPC.Close",
"price":  85.02,
"rsi": 31.267,
"ret": -0.0011748 
},
{
 "date":  -1322,
"name": "GSPC.Close",
"price":  85.43,
"rsi": 30.903,
"ret": 0.0048224 
},
{
 "date":  -1319,
"name": "GSPC.Close",
"price":   86.2,
"rsi": 34.286,
"ret": 0.0090132 
},
{
 "date":  -1318,
"name": "GSPC.Close",
"price":  86.77,
"rsi": 40.208,
"ret": 0.0066125 
},
{
 "date":  -1317,
"name": "GSPC.Close",
"price":  87.07,
"rsi": 44.216,
"ret": 0.0034574 
},
{
 "date":  -1316,
"name": "GSPC.Close",
"price":  87.07,
"rsi": 46.258,
"ret":      0 
},
{
 "date":  -1315,
"name": "GSPC.Close",
"price":  87.33,
"rsi": 46.258,
"ret": 0.0029861 
},
{
 "date":  -1311,
"name": "GSPC.Close",
"price":  86.13,
"rsi": 48.165,
"ret": -0.013741 
},
{
 "date":  -1310,
"name": "GSPC.Close",
"price":   86.1,
"rsi": 40.944,
"ret": -0.00034831 
},
{
 "date":  -1309,
"name": "GSPC.Close",
"price":  85.96,
"rsi": 40.779,
"ret": -0.001626 
},
{
 "date":  -1308,
"name": "GSPC.Close",
"price":  86.06,
"rsi": 39.971,
"ret": 0.0011633 
},
{
 "date":  -1305,
"name": "GSPC.Close",
"price":  85.42,
"rsi": 40.872,
"ret": -0.0074367 
},
{
 "date":  -1304,
"name": "GSPC.Close",
"price":  84.83,
"rsi": 37.041,
"ret": -0.006907 
},
{
 "date":  -1303,
"name": "GSPC.Close",
"price":  84.93,
"rsi": 33.888,
"ret": 0.0011788 
},
{
 "date":  -1302,
"name": "GSPC.Close",
"price":   85.5,
"rsi":   34.9,
"ret": 0.0067114 
},
{
 "date":  -1301,
"name": "GSPC.Close",
"price":  86.44,
"rsi": 40.489,
"ret": 0.010994 
},
{
 "date":  -1298,
"name": "GSPC.Close",
"price":  86.83,
"rsi": 48.363,
"ret": 0.0045118 
},
{
 "date":  -1297,
"name": "GSPC.Close",
"price":  87.07,
"rsi": 51.245,
"ret": 0.002764 
},
{
 "date":  -1296,
"name": "GSPC.Close",
"price":  86.73,
"rsi": 52.984,
"ret": -0.0039049 
},
{
 "date":  -1295,
"name": "GSPC.Close",
"price":  86.47,
"rsi":  50.25,
"ret": -0.0029978 
},
{
 "date":  -1294,
"name": "GSPC.Close",
"price":  86.51,
"rsi": 48.201,
"ret": 0.00046259 
},
{
 "date":  -1291,
"name": "GSPC.Close",
"price":  86.48,
"rsi": 48.548,
"ret": -0.00034678 
},
{
 "date":  -1290,
"name": "GSPC.Close",
"price":  86.71,
"rsi": 48.287,
"ret": 0.0026596 
},
{
 "date":  -1289,
"name": "GSPC.Close",
"price":  86.85,
"rsi":  50.49,
"ret": 0.0016146 
},
{
 "date":  -1288,
"name": "GSPC.Close",
"price":   86.5,
"rsi": 51.835,
"ret": -0.0040299 
},
{
 "date":  -1287,
"name": "GSPC.Close",
"price":  86.58,
"rsi": 48.302,
"ret": 0.00092486 
},
{
 "date":  -1284,
"name": "GSPC.Close",
"price":  86.08,
"rsi": 49.155,
"ret": -0.005775 
},
{
 "date":  -1283,
"name": "GSPC.Close",
"price":  85.67,
"rsi": 44.241,
"ret": -0.004763 
},
{
 "date":  -1282,
"name": "GSPC.Close",
"price":  84.86,
"rsi": 40.652,
"ret": -0.0094549 
},
{
 "date":  -1281,
"name": "GSPC.Close",
"price":  84.74,
"rsi": 34.669,
"ret": -0.0014141 
},
{
 "date":  -1280,
"name": "GSPC.Close",
"price":  85.61,
"rsi": 33.873,
"ret": 0.010267 
},
{
 "date":  -1276,
"name": "GSPC.Close",
"price":  85.82,
"rsi": 43.919,
"ret": 0.002453 
},
{
 "date":  -1275,
"name": "GSPC.Close",
"price":  87.06,
"rsi":  46.05,
"ret": 0.014449 
},
{
 "date":  -1274,
"name": "GSPC.Close",
"price":  87.38,
"rsi": 56.548,
"ret": 0.0036756 
},
{
 "date":  -1273,
"name": "GSPC.Close",
"price":  87.61,
"rsi": 58.777,
"ret": 0.0026322 
},
{
 "date":  -1270,
"name": "GSPC.Close",
"price":  87.45,
"rsi": 60.351,
"ret": -0.0018263 
},
{
 "date":  -1269,
"name": "GSPC.Close",
"price":  86.88,
"rsi": 58.673,
"ret": -0.006518 
},
{
 "date":  -1268,
"name": "GSPC.Close",
"price":   86.3,
"rsi": 53.015,
"ret": -0.0066759 
},
{
 "date":  -1267,
"name": "GSPC.Close",
"price":  86.82,
"rsi": 47.948,
"ret": 0.0060255 
},
{
 "date":  -1266,
"name": "GSPC.Close",
"price":  87.08,
"rsi": 52.345,
"ret": 0.0029947 
},
{
 "date":  -1263,
"name": "GSPC.Close",
"price":  86.99,
"rsi": 54.419,
"ret": -0.0010335 
},
{
 "date":  -1262,
"name": "GSPC.Close",
"price":  86.33,
"rsi":  53.55,
"ret": -0.0075871 
},
{
 "date":  -1261,
"name": "GSPC.Close",
"price":  85.51,
"rsi": 47.556,
"ret": -0.0094984 
},
{
 "date":  -1260,
"name": "GSPC.Close",
"price":  85.52,
"rsi": 41.361,
"ret": 0.00011695 
},
{
 "date":  -1259,
"name": "GSPC.Close",
"price":  85.41,
"rsi": 41.461,
"ret": -0.0012862 
},
{
 "date":  -1256,
"name": "GSPC.Close",
"price":  83.83,
"rsi": 40.639,
"ret": -0.018499 
},
{
 "date":  -1255,
"name": "GSPC.Close",
"price":   83.7,
"rsi": 31.099,
"ret": -0.0015508 
},
{
 "date":  -1254,
"name": "GSPC.Close",
"price":   84.1,
"rsi": 30.466,
"ret": 0.004779 
},
{
 "date":  -1253,
"name": "GSPC.Close",
"price":  83.77,
"rsi": 34.864,
"ret": -0.0039239 
},
{
 "date":  -1252,
"name": "GSPC.Close",
"price":   83.6,
"rsi": 33.009,
"ret": -0.0020294 
},
{
 "date":  -1249,
"name": "GSPC.Close",
"price":  82.31,
"rsi": 32.062,
"ret": -0.015431 
},
{
 "date":  -1248,
"name": "GSPC.Close",
"price":  82.33,
"rsi": 25.976,
"ret": 0.00024298 
},
{
 "date":  -1247,
"name": "GSPC.Close",
"price":  83.15,
"rsi":  26.21,
"ret": 0.0099599 
},
{
 "date":  -1246,
"name": "GSPC.Close",
"price":  83.93,
"rsi": 35.243,
"ret": 0.0093806 
},
{
 "date":  -1245,
"name": "GSPC.Close",
"price":     84,
"rsi": 42.459,
"ret": 0.00083403 
},
{
 "date":  -1242,
"name": "GSPC.Close",
"price":  83.75,
"rsi": 43.072,
"ret": -0.0029762 
},
{
 "date":  -1241,
"name": "GSPC.Close",
"price":  83.49,
"rsi": 41.377,
"ret": -0.0031045 
},
{
 "date":  -1240,
"name": "GSPC.Close",
"price":  83.11,
"rsi": 39.629,
"ret": -0.0045514 
},
{
 "date":  -1239,
"name": "GSPC.Close",
"price":  83.02,
"rsi":  37.16,
"ret": -0.0010829 
},
{
 "date":  -1238,
"name": "GSPC.Close",
"price":  83.17,
"rsi": 36.578,
"ret": 0.0018068 
},
{
 "date":  -1235,
"name": "GSPC.Close",
"price":  82.74,
"rsi": 38.311,
"ret": -0.0051701 
},
{
 "date":  -1234,
"name": "GSPC.Close",
"price":  81.63,
"rsi": 35.331,
"ret": -0.013416 
},
{
 "date":  -1233,
"name": "GSPC.Close",
"price":  81.18,
"rsi":  29.05,
"ret": -0.0055127 
},
{
 "date":  -1232,
"name": "GSPC.Close",
"price":  80.16,
"rsi": 26.958,
"ret": -0.012565 
},
{
 "date":  -1231,
"name": "GSPC.Close",
"price":  79.62,
"rsi": 22.927,
"ret": -0.0067365 
},
{
 "date":  -1228,
"name": "GSPC.Close",
"price":  78.24,
"rsi": 21.126,
"ret": -0.017332 
},
{
 "date":  -1227,
"name": "GSPC.Close",
"price":  78.11,
"rsi":  17.37,
"ret": -0.0016616 
},
{
 "date":  -1226,
"name": "GSPC.Close",
"price":  79.07,
"rsi": 17.063,
"ret": 0.01229 
},
{
 "date":  -1225,
"name": "GSPC.Close",
"price":  78.06,
"rsi": 27.304,
"ret": -0.012773 
},
{
 "date":  -1224,
"name": "GSPC.Close",
"price":  76.41,
"rsi": 23.953,
"ret": -0.021138 
},
{
 "date":  -1221,
"name": "GSPC.Close",
"price":  74.53,
"rsi": 19.699,
"ret": -0.024604 
},
{
 "date":  -1220,
"name": "GSPC.Close",
"price":  75.86,
"rsi": 16.175,
"ret": 0.017845 
},
{
 "date":  -1219,
"name": "GSPC.Close",
"price":   77.1,
"rsi":  26.23,
"ret": 0.016346 
},
{
 "date":  -1218,
"name": "GSPC.Close",
"price":   77.7,
"rsi":  34.16,
"ret": 0.0077821 
},
{
 "date":  -1217,
"name": "GSPC.Close",
"price":  77.42,
"rsi": 37.653,
"ret": -0.0036036 
},
{
 "date":  -1213,
"name": "GSPC.Close",
"price":  76.96,
"rsi": 36.675,
"ret": -0.0059416 
},
{
 "date":  -1212,
"name": "GSPC.Close",
"price":  76.37,
"rsi": 35.064,
"ret": -0.0076663 
},
{
 "date":  -1211,
"name": "GSPC.Close",
"price":  76.05,
"rsi": 33.058,
"ret": -0.0041901 
},
{
 "date":  -1210,
"name": "GSPC.Close",
"price":  76.29,
"rsi":  31.99,
"ret": 0.0031558 
},
{
 "date":  -1207,
"name": "GSPC.Close",
"price":  77.91,
"rsi":  33.72,
"ret": 0.021235 
},
{
 "date":  -1206,
"name": "GSPC.Close",
"price":  78.32,
"rsi": 44.067,
"ret": 0.0052625 
},
{
 "date":  -1205,
"name": "GSPC.Close",
"price":  79.13,
"rsi":  46.35,
"ret": 0.010342 
},
{
 "date":  -1204,
"name": "GSPC.Close",
"price":  80.08,
"rsi": 50.636,
"ret": 0.012006 
},
{
 "date":  -1203,
"name": "GSPC.Close",
"price":  79.99,
"rsi": 55.161,
"ret": -0.0011239 
},
{
 "date":  -1200,
"name": "GSPC.Close",
"price":  79.59,
"rsi":  54.65,
"ret": -0.0050006 
},
{
 "date":  -1199,
"name": "GSPC.Close",
"price":  79.04,
"rsi": 52.329,
"ret": -0.0069104 
},
{
 "date":  -1198,
"name": "GSPC.Close",
"price":  77.71,
"rsi": 49.233,
"ret": -0.016827 
},
{
 "date":  -1197,
"name": "GSPC.Close",
"price":  77.94,
"rsi": 42.661,
"ret": 0.0029597 
},
{
 "date":  -1196,
"name": "GSPC.Close",
"price":  77.67,
"rsi": 44.052,
"ret": -0.0034642 
},
{
 "date":  -1193,
"name": "GSPC.Close",
"price":  77.86,
"rsi": 42.741,
"ret": 0.0024462 
},
{
 "date":  -1192,
"name": "GSPC.Close",
"price":   78.1,
"rsi": 44.004,
"ret": 0.0030825 
},
{
 "date":  -1191,
"name": "GSPC.Close",
"price":  77.11,
"rsi": 45.635,
"ret": -0.012676 
},
{
 "date":  -1190,
"name": "GSPC.Close",
"price":  76.31,
"rsi": 40.407,
"ret": -0.010375 
},
{
 "date":  -1189,
"name": "GSPC.Close",
"price":  76.56,
"rsi": 36.744,
"ret": 0.0032761 
},
{
 "date":  -1186,
"name": "GSPC.Close",
"price":   74.9,
"rsi": 38.617,
"ret": -0.021682 
},
{
 "date":  -1185,
"name": "GSPC.Close",
"price":   75.1,
"rsi":  31.87,
"ret": 0.0026702 
},
{
 "date":  -1184,
"name": "GSPC.Close",
"price":  74.69,
"rsi":  33.38,
"ret": -0.0054594 
},
{
 "date":  -1183,
"name": "GSPC.Close",
"price":  74.05,
"rsi": 31.823,
"ret": -0.0085688 
},
{
 "date":  -1182,
"name": "GSPC.Close",
"price":   73.2,
"rsi": 29.509,
"ret": -0.011479 
},
{
 "date":  -1179,
"name": "GSPC.Close",
"price":  74.53,
"rsi": 26.728,
"ret": 0.018169 
},
{
 "date":  -1178,
"name": "GSPC.Close",
"price":  74.91,
"rsi": 36.767,
"ret": 0.0050986 
},
{
 "date":  -1177,
"name": "GSPC.Close",
"price":  77.04,
"rsi": 39.325,
"ret": 0.028434 
},
{
 "date":  -1176,
"name": "GSPC.Close",
"price":  76.89,
"rsi": 51.233,
"ret": -0.001947 
},
{
 "date":  -1175,
"name": "GSPC.Close",
"price":   76.6,
"rsi": 50.482,
"ret": -0.0037716 
},
{
 "date":  -1172,
"name": "GSPC.Close",
"price":  77.47,
"rsi": 48.986,
"ret": 0.011358 
},
{
 "date":  -1171,
"name": "GSPC.Close",
"price":  78.68,
"rsi": 53.443,
"ret": 0.015619 
},
{
 "date":  -1170,
"name": "GSPC.Close",
"price":  78.05,
"rsi":  58.83,
"ret": -0.0080071 
},
{
 "date":  -1169,
"name": "GSPC.Close",
"price":  77.84,
"rsi": 55.246,
"ret": -0.0026906 
},
{
 "date":  -1168,
"name": "GSPC.Close",
"price":  78.19,
"rsi": 54.063,
"ret": 0.0044964 
},
{
 "date":  -1165,
"name": "GSPC.Close",
"price":  78.42,
"rsi": 55.763,
"ret": 0.0029416 
},
{
 "date":  -1164,
"name": "GSPC.Close",
"price":   78.9,
"rsi": 56.891,
"ret": 0.0061209 
},
{
 "date":  -1163,
"name": "GSPC.Close",
"price":  79.58,
"rsi": 59.229,
"ret": 0.0086185 
},
{
 "date":  -1162,
"name": "GSPC.Close",
"price":  80.23,
"rsi": 62.345,
"ret": 0.0081679 
},
{
 "date":  -1161,
"name": "GSPC.Close",
"price":  80.24,
"rsi": 65.091,
"ret": 0.00012464 
},
{
 "date":  -1158,
"name": "GSPC.Close",
"price":   80.2,
"rsi": 65.133,
"ret": -0.0004985 
},
{
 "date":  -1157,
"name": "GSPC.Close",
"price":  80.81,
"rsi": 64.796,
"ret": 0.007606 
},
{
 "date":  -1156,
"name": "GSPC.Close",
"price":  80.88,
"rsi": 67.552,
"ret": 0.00086623 
},
{
 "date":  -1155,
"name": "GSPC.Close",
"price":  80.56,
"rsi": 67.863,
"ret": -0.0039565 
},
{
 "date":  -1154,
"name": "GSPC.Close",
"price":  80.81,
"rsi": 64.806,
"ret": 0.0031033 
},
{
 "date":  -1151,
"name": "GSPC.Close",
"price":  80.73,
"rsi": 66.091,
"ret": -0.00098998 
},
{
 "date":  -1149,
"name": "GSPC.Close",
"price":  81.38,
"rsi":  65.27,
"ret": 0.0080515 
},
{
 "date":  -1148,
"name": "GSPC.Close",
"price":  81.89,
"rsi": 68.676,
"ret": 0.0062669 
},
{
 "date":  -1147,
"name": "GSPC.Close",
"price":  81.94,
"rsi": 71.073,
"ret": 0.00061058 
},
{
 "date":  -1144,
"name": "GSPC.Close",
"price":  81.37,
"rsi": 71.305,
"ret": -0.0069563 
},
{
 "date":  -1143,
"name": "GSPC.Close",
"price":  81.69,
"rsi": 64.917,
"ret": 0.0039327 
},
{
 "date":  -1142,
"name": "GSPC.Close",
"price":  82.37,
"rsi":  66.72,
"ret": 0.0083242 
},
{
 "date":  -1141,
"name": "GSPC.Close",
"price":   81.8,
"rsi": 70.221,
"ret": -0.00692 
},
{
 "date":  -1140,
"name": "GSPC.Close",
"price":  81.26,
"rsi":  64.13,
"ret": -0.0066015 
},
{
 "date":  -1137,
"name": "GSPC.Close",
"price":  80.09,
"rsi": 58.916,
"ret": -0.014398 
},
{
 "date":  -1136,
"name": "GSPC.Close",
"price":  79.67,
"rsi": 49.522,
"ret": -0.0052441 
},
{
 "date":  -1135,
"name": "GSPC.Close",
"price":  80.21,
"rsi": 46.647,
"ret": 0.006778 
},
{
 "date":  -1133,
"name": "GSPC.Close",
"price":  80.85,
"rsi": 50.617,
"ret": 0.0079791 
},
{
 "date":  -1130,
"name": "GSPC.Close",
"price":  80.71,
"rsi":   54.9,
"ret": -0.0017316 
},
{
 "date":  -1129,
"name": "GSPC.Close",
"price":  80.42,
"rsi": 53.801,
"ret": -0.0035931 
},
{
 "date":  -1128,
"name": "GSPC.Close",
"price":  80.45,
"rsi":   51.5,
"ret": 0.00037304 
},
{
 "date":  -1127,
"name": "GSPC.Close",
"price":  80.08,
"rsi":  51.73,
"ret": -0.0045991 
},
{
 "date":  -1126,
"name": "GSPC.Close",
"price":  80.13,
"rsi": 48.666,
"ret": 0.00062438 
},
{
 "date":  -1123,
"name": "GSPC.Close",
"price":  80.24,
"rsi": 49.105,
"ret": 0.0013728 
},
{
 "date":  -1122,
"name": "GSPC.Close",
"price":  80.84,
"rsi": 50.115,
"ret": 0.0074776 
},
{
 "date":  -1121,
"name": "GSPC.Close",
"price":  81.72,
"rsi": 55.324,
"ret": 0.010886 
},
{
 "date":  -1120,
"name": "GSPC.Close",
"price":  82.05,
"rsi": 61.649,
"ret": 0.0040382 
},
{
 "date":  -1119,
"name": "GSPC.Close",
"price":  82.14,
"rsi": 63.723,
"ret": 0.0010969 
},
{
 "date":  -1116,
"name": "GSPC.Close",
"price":     83,
"rsi": 64.291,
"ret": 0.01047 
},
{
 "date":  -1115,
"name": "GSPC.Close",
"price":  82.73,
"rsi":  69.24,
"ret": -0.003253 
},
{
 "date":  -1114,
"name": "GSPC.Close",
"price":  82.64,
"rsi": 66.141,
"ret": -0.0010879 
},
{
 "date":  -1113,
"name": "GSPC.Close",
"price":  81.64,
"rsi": 65.095,
"ret": -0.012101 
},
{
 "date":  -1112,
"name": "GSPC.Close",
"price":  81.58,
"rsi": 54.736,
"ret": -0.00073493 
},
{
 "date":  -1109,
"name": "GSPC.Close",
"price":  81.27,
"rsi": 54.179,
"ret": -0.0038 
},
{
 "date":  -1108,
"name": "GSPC.Close",
"price":  80.96,
"rsi": 51.275,
"ret": -0.0038144 
},
{
 "date":  -1107,
"name": "GSPC.Close",
"price":  81.38,
"rsi": 48.477,
"ret": 0.0051877 
},
{
 "date":  -1106,
"name": "GSPC.Close",
"price":  81.69,
"rsi": 52.277,
"ret": 0.0038093 
},
{
 "date":  -1105,
"name": "GSPC.Close",
"price":  81.47,
"rsi": 54.919,
"ret": -0.0026931 
},
{
 "date":  -1101,
"name": "GSPC.Close",
"price":     81,
"rsi":  52.69,
"ret": -0.005769 
},
{
 "date":  -1100,
"name": "GSPC.Close",
"price":  80.61,
"rsi": 48.188,
"ret": -0.0048148 
},
{
 "date":  -1099,
"name": "GSPC.Close",
"price":  80.37,
"rsi":  44.77,
"ret": -0.0029773 
},
{
 "date":  -1098,
"name": "GSPC.Close",
"price":  80.33,
"rsi":  42.76,
"ret": -0.0004977 
},
{
 "date":  -1094,
"name": "GSPC.Close",
"price":  80.38,
"rsi": 42.419,
"ret": 0.00062243 
},
{
 "date":  -1093,
"name": "GSPC.Close",
"price":  80.55,
"rsi": 43.032,
"ret": 0.002115 
},
{
 "date":  -1092,
"name": "GSPC.Close",
"price":   81.6,
"rsi": 45.169,
"ret": 0.013035 
},
{
 "date":  -1091,
"name": "GSPC.Close",
"price":  82.18,
"rsi":  56.12,
"ret": 0.0071078 
},
{
 "date":  -1088,
"name": "GSPC.Close",
"price":  82.81,
"rsi": 60.779,
"ret": 0.0076661 
},
{
 "date":  -1087,
"name": "GSPC.Close",
"price":  82.81,
"rsi": 65.113,
"ret":      0 
},
{
 "date":  -1086,
"name": "GSPC.Close",
"price":  83.47,
"rsi": 65.113,
"ret": 0.0079701 
},
{
 "date":  -1085,
"name": "GSPC.Close",
"price":  83.91,
"rsi": 69.242,
"ret": 0.0052714 
},
{
 "date":  -1084,
"name": "GSPC.Close",
"price":  84.53,
"rsi": 71.651,
"ret": 0.0073889 
},
{
 "date":  -1081,
"name": "GSPC.Close",
"price":  84.31,
"rsi": 74.662,
"ret": -0.0026026 
},
{
 "date":  -1080,
"name": "GSPC.Close",
"price":  85.24,
"rsi":  71.75,
"ret": 0.011031 
},
{
 "date":  -1079,
"name": "GSPC.Close",
"price":  85.79,
"rsi":  76.01,
"ret": 0.0064524 
},
{
 "date":  -1078,
"name": "GSPC.Close",
"price":  85.82,
"rsi": 78.112,
"ret": 0.00034969 
},
{
 "date":  -1077,
"name": "GSPC.Close",
"price":  86.07,
"rsi": 78.225,
"ret": 0.0029131 
},
{
 "date":  -1074,
"name": "GSPC.Close",
"price":  86.39,
"rsi": 79.181,
"ret": 0.0037179 
},
{
 "date":  -1073,
"name": "GSPC.Close",
"price":  86.51,
"rsi":  80.37,
"ret": 0.001389 
},
{
 "date":  -1072,
"name": "GSPC.Close",
"price":  85.85,
"rsi": 80.813,
"ret": -0.0076292 
},
{
 "date":  -1071,
"name": "GSPC.Close",
"price":  85.81,
"rsi": 71.293,
"ret": -0.00046593 
},
{
 "date":  -1070,
"name": "GSPC.Close",
"price":  86.16,
"rsi": 70.749,
"ret": 0.0040788 
},
{
 "date":  -1067,
"name": "GSPC.Close",
"price":  86.66,
"rsi": 72.711,
"ret": 0.0058032 
},
{
 "date":  -1066,
"name": "GSPC.Close",
"price":  86.61,
"rsi": 75.264,
"ret": -0.00057697 
},
{
 "date":  -1065,
"name": "GSPC.Close",
"price":  86.43,
"rsi": 74.513,
"ret": -0.0020783 
},
{
 "date":  -1064,
"name": "GSPC.Close",
"price":  86.73,
"rsi": 71.739,
"ret": 0.003471 
},
{
 "date":  -1063,
"name": "GSPC.Close",
"price":  87.36,
"rsi": 73.509,
"ret": 0.0072639 
},
{
 "date":  -1060,
"name": "GSPC.Close",
"price":  87.18,
"rsi": 76.796,
"ret": -0.0020604 
},
{
 "date":  -1059,
"name": "GSPC.Close",
"price":  86.95,
"rsi": 73.972,
"ret": -0.0026382 
},
{
 "date":  -1058,
"name": "GSPC.Close",
"price":  87.72,
"rsi":  70.41,
"ret": 0.0088557 
},
{
 "date":  -1057,
"name": "GSPC.Close",
"price":  87.36,
"rsi": 74.787,
"ret": -0.004104 
},
{
 "date":  -1056,
"name": "GSPC.Close",
"price":  87.63,
"rsi": 69.603,
"ret": 0.0030907 
},
{
 "date":  -1053,
"name": "GSPC.Close",
"price":  87.58,
"rsi": 71.214,
"ret": -0.00057058 
},
{
 "date":  -1052,
"name": "GSPC.Close",
"price":  88.17,
"rsi": 70.469,
"ret": 0.0067367 
},
{
 "date":  -1051,
"name": "GSPC.Close",
"price":  88.27,
"rsi": 73.935,
"ret": 0.0011342 
},
{
 "date":  -1050,
"name": "GSPC.Close",
"price":  87.86,
"rsi": 74.482,
"ret": -0.0046448 
},
{
 "date":  -1049,
"name": "GSPC.Close",
"price":  87.89,
"rsi": 68.169,
"ret": 0.00034145 
},
{
 "date":  -1046,
"name": "GSPC.Close",
"price":   87.4,
"rsi":  68.38,
"ret": -0.0055752 
},
{
 "date":  -1045,
"name": "GSPC.Close",
"price":  87.34,
"rsi": 61.234,
"ret": -0.0006865 
},
{
 "date":  -1043,
"name": "GSPC.Close",
"price":  87.45,
"rsi": 60.402,
"ret": 0.0012594 
},
{
 "date":  -1042,
"name": "GSPC.Close",
"price":  87.41,
"rsi": 61.437,
"ret": -0.0004574 
},
{
 "date":  -1039,
"name": "GSPC.Close",
"price":  86.46,
"rsi": 60.814,
"ret": -0.010868 
},
{
 "date":  -1038,
"name": "GSPC.Close",
"price":  86.78,
"rsi": 48.298,
"ret": 0.0037011 
},
{
 "date":  -1037,
"name": "GSPC.Close",
"price":  87.68,
"rsi":  51.89,
"ret": 0.010371 
},
{
 "date":  -1036,
"name": "GSPC.Close",
"price":  88.16,
"rsi": 60.253,
"ret": 0.0054745 
},
{
 "date":  -1035,
"name": "GSPC.Close",
"price":  88.29,
"rsi": 63.861,
"ret": 0.0014746 
},
{
 "date":  -1032,
"name": "GSPC.Close",
"price":   88.1,
"rsi": 64.794,
"ret": -0.002152 
},
{
 "date":  -1031,
"name": "GSPC.Close",
"price":  88.16,
"rsi": 62.266,
"ret": 0.00068104 
},
{
 "date":  -1030,
"name": "GSPC.Close",
"price":  88.27,
"rsi":  62.76,
"ret": 0.0012477 
},
{
 "date":  -1029,
"name": "GSPC.Close",
"price":  88.53,
"rsi": 63.698,
"ret": 0.0029455 
},
{
 "date":  -1028,
"name": "GSPC.Close",
"price":  88.89,
"rsi": 65.887,
"ret": 0.0040664 
},
{
 "date":  -1025,
"name": "GSPC.Close",
"price":  88.43,
"rsi":   68.7,
"ret": -0.0051749 
},
{
 "date":  -1024,
"name": "GSPC.Close",
"price":  88.35,
"rsi": 61.698,
"ret": -0.00090467 
},
{
 "date":  -1023,
"name": "GSPC.Close",
"price":  89.19,
"rsi": 60.542,
"ret": 0.0095076 
},
{
 "date":  -1022,
"name": "GSPC.Close",
"price":  90.09,
"rsi": 67.439,
"ret": 0.010091 
},
{
 "date":  -1021,
"name": "GSPC.Close",
"price":  90.25,
"rsi": 72.904,
"ret": 0.001776 
},
{
 "date":  -1018,
"name": "GSPC.Close",
"price":   90.2,
"rsi": 73.748,
"ret": -0.00055402 
},
{
 "date":  -1017,
"name": "GSPC.Close",
"price":     90,
"rsi": 72.983,
"ret": -0.0022173 
},
{
 "date":  -1016,
"name": "GSPC.Close",
"price":  90.25,
"rsi": 69.863,
"ret": 0.0027778 
},
{
 "date":  -1015,
"name": "GSPC.Close",
"price":  90.94,
"rsi": 71.503,
"ret": 0.0076454 
},
{
 "date":  -1011,
"name": "GSPC.Close",
"price":  90.87,
"rsi": 75.471,
"ret": -0.00076974 
},
{
 "date":  -1010,
"name": "GSPC.Close",
"price":  90.91,
"rsi":  74.34,
"ret": 0.00044019 
},
{
 "date":  -1009,
"name": "GSPC.Close",
"price":  90.73,
"rsi": 74.574,
"ret": -0.00198 
},
{
 "date":  -1008,
"name": "GSPC.Close",
"price":   90.7,
"rsi": 71.412,
"ret": -0.00033065 
},
{
 "date":  -1007,
"name": "GSPC.Close",
"price":   90.2,
"rsi": 70.873,
"ret": -0.0055127 
},
{
 "date":  -1004,
"name": "GSPC.Close",
"price":  89.24,
"rsi": 62.412,
"ret": -0.010643 
},
{
 "date":  -1003,
"name": "GSPC.Close",
"price":  89.22,
"rsi": 50.056,
"ret": -0.00022411 
},
{
 "date":  -1002,
"name": "GSPC.Close",
"price":  89.79,
"rsi": 49.835,
"ret": 0.0063887 
},
{
 "date":  -1001,
"name": "GSPC.Close",
"price":  89.94,
"rsi":  55.83,
"ret": 0.0016706 
},
{
 "date":  -1000,
"name": "GSPC.Close",
"price":  89.36,
"rsi": 57.277,
"ret": -0.0064487 
},
{
 "date":   -997,
"name": "GSPC.Close",
"price":  88.24,
"rsi": 50.401,
"ret": -0.012534 
},
{
 "date":   -996,
"name": "GSPC.Close",
"price":  88.88,
"rsi": 40.333,
"ret": 0.0072529 
},
{
 "date":   -995,
"name": "GSPC.Close",
"price":  88.78,
"rsi": 46.865,
"ret": -0.0011251 
},
{
 "date":   -994,
"name": "GSPC.Close",
"price":  89.46,
"rsi": 46.017,
"ret": 0.0076594 
},
{
 "date":   -993,
"name": "GSPC.Close",
"price":  90.43,
"rsi": 52.331,
"ret": 0.010843 
},
{
 "date":   -990,
"name": "GSPC.Close",
"price":  91.07,
"rsi": 59.592,
"ret": 0.0070773 
},
{
 "date":   -989,
"name": "GSPC.Close",
"price":  91.86,
"rsi": 63.538,
"ret": 0.0086746 
},
{
 "date":   -988,
"name": "GSPC.Close",
"price":  91.94,
"rsi": 67.727,
"ret": 0.00087089 
},
{
 "date":   -987,
"name": "GSPC.Close",
"price":  92.11,
"rsi": 68.127,
"ret": 0.001849 
},
{
 "date":   -986,
"name": "GSPC.Close",
"price":   92.3,
"rsi": 69.005,
"ret": 0.0020628 
},
{
 "date":   -983,
"name": "GSPC.Close",
"price":  92.62,
"rsi": 69.999,
"ret": 0.003467 
},
{
 "date":   -982,
"name": "GSPC.Close",
"price":  93.11,
"rsi": 71.649,
"ret": 0.0052904 
},
{
 "date":   -981,
"name": "GSPC.Close",
"price":  93.02,
"rsi": 74.006,
"ret": -0.0009666 
},
{
 "date":   -980,
"name": "GSPC.Close",
"price":  93.81,
"rsi": 72.809,
"ret": 0.0084928 
},
{
 "date":   -979,
"name": "GSPC.Close",
"price":  94.01,
"rsi": 76.416,
"ret": 0.002132 
},
{
 "date":   -976,
"name": "GSPC.Close",
"price":  93.84,
"rsi": 77.239,
"ret": -0.0018083 
},
{
 "date":   -975,
"name": "GSPC.Close",
"price":  93.67,
"rsi": 74.848,
"ret": -0.0018116 
},
{
 "date":   -974,
"name": "GSPC.Close",
"price":  93.91,
"rsi": 72.432,
"ret": 0.0025622 
},
{
 "date":   -973,
"name": "GSPC.Close",
"price":  94.32,
"rsi": 73.722,
"ret": 0.0043659 
},
{
 "date":   -972,
"name": "GSPC.Close",
"price":  94.44,
"rsi": 75.804,
"ret": 0.0012723 
},
{
 "date":   -969,
"name": "GSPC.Close",
"price":  94.58,
"rsi": 76.393,
"ret": 0.0014824 
},
{
 "date":   -968,
"name": "GSPC.Close",
"price":   93.6,
"rsi": 77.094,
"ret": -0.010362 
},
{
 "date":   -967,
"name": "GSPC.Close",
"price":  93.35,
"rsi": 62.991,
"ret": -0.0026709 
},
{
 "date":   -966,
"name": "GSPC.Close",
"price":  93.75,
"rsi": 59.977,
"ret": 0.0042849 
},
{
 "date":   -965,
"name": "GSPC.Close",
"price":  93.48,
"rsi": 63.025,
"ret": -0.00288 
},
{
 "date":   -962,
"name": "GSPC.Close",
"price":  92.71,
"rsi": 59.719,
"ret": -0.0082371 
},
{
 "date":   -961,
"name": "GSPC.Close",
"price":  93.14,
"rsi": 51.431,
"ret": 0.0046381 
},
{
 "date":   -960,
"name": "GSPC.Close",
"price":  92.78,
"rsi": 55.172,
"ret": -0.0038651 
},
{
 "date":   -959,
"name": "GSPC.Close",
"price":  92.53,
"rsi":  51.59,
"ret": -0.0026945 
},
{
 "date":   -958,
"name": "GSPC.Close",
"price":  92.07,
"rsi":   49.2,
"ret": -0.0049714 
},
{
 "date":   -955,
"name": "GSPC.Close",
"price":  91.67,
"rsi": 45.064,
"ret": -0.0043445 
},
{
 "date":   -954,
"name": "GSPC.Close",
"price":  91.23,
"rsi": 41.775,
"ret": -0.0047998 
},
{
 "date":   -953,
"name": "GSPC.Close",
"price":  90.18,
"rsi": 38.451,
"ret": -0.011509 
},
{
 "date":   -952,
"name": "GSPC.Close",
"price":  91.19,
"rsi": 31.923,
"ret": 0.0112 
},
{
 "date":   -951,
"name": "GSPC.Close",
"price":  90.98,
"rsi": 42.105,
"ret": -0.0023029 
},
{
 "date":   -948,
"name": "GSPC.Close",
"price":  90.49,
"rsi": 40.741,
"ret": -0.0053858 
},
{
 "date":   -946,
"name": "GSPC.Close",
"price":  89.08,
"rsi": 37.673,
"ret": -0.015582 
},
{
 "date":   -945,
"name": "GSPC.Close",
"price":  90.23,
"rsi": 30.546,
"ret": 0.01291 
},
{
 "date":   -944,
"name": "GSPC.Close",
"price":  89.79,
"rsi": 40.443,
"ret": -0.0048764 
},
{
 "date":   -941,
"name": "GSPC.Close",
"price":  88.43,
"rsi":   38.2,
"ret": -0.015146 
},
{
 "date":   -940,
"name": "GSPC.Close",
"price":  90.23,
"rsi": 32.247,
"ret": 0.020355 
},
{
 "date":   -939,
"name": "GSPC.Close",
"price":  90.91,
"rsi": 44.561,
"ret": 0.0075363 
},
{
 "date":   -938,
"name": "GSPC.Close",
"price":   91.4,
"rsi": 48.378,
"ret": 0.0053899 
},
{
 "date":   -937,
"name": "GSPC.Close",
"price":  91.56,
"rsi": 50.996,
"ret": 0.0017505 
},
{
 "date":   -934,
"name": "GSPC.Close",
"price":  92.04,
"rsi": 51.855,
"ret": 0.0052425 
},
{
 "date":   -933,
"name": "GSPC.Close",
"price":  92.62,
"rsi": 54.434,
"ret": 0.0063016 
},
{
 "date":   -932,
"name": "GSPC.Close",
"price":   92.4,
"rsi": 57.404,
"ret": -0.0023753 
},
{
 "date":   -931,
"name": "GSPC.Close",
"price":  92.49,
"rsi": 55.915,
"ret": 0.00097403 
},
{
 "date":   -930,
"name": "GSPC.Close",
"price":  92.54,
"rsi": 56.413,
"ret": 0.0005406 
},
{
 "date":   -927,
"name": "GSPC.Close",
"price":  92.51,
"rsi": 56.706,
"ret": -0.00032418 
},
{
 "date":   -926,
"name": "GSPC.Close",
"price":  92.48,
"rsi": 56.461,
"ret": -0.00032429 
},
{
 "date":   -925,
"name": "GSPC.Close",
"price":   92.2,
"rsi":   56.2,
"ret": -0.0030277 
},
{
 "date":   -924,
"name": "GSPC.Close",
"price":  91.97,
"rsi": 53.701,
"ret": -0.0024946 
},
{
 "date":   -923,
"name": "GSPC.Close",
"price":     92,
"rsi": 51.669,
"ret": 0.00032619 
},
{
 "date":   -920,
"name": "GSPC.Close",
"price":  91.64,
"rsi": 51.924,
"ret": -0.003913 
},
{
 "date":   -919,
"name": "GSPC.Close",
"price":   91.3,
"rsi": 48.603,
"ret": -0.0037102 
},
{
 "date":   -918,
"name": "GSPC.Close",
"price":  91.31,
"rsi": 45.634,
"ret": 0.00010953 
},
{
 "date":   -917,
"name": "GSPC.Close",
"price":  90.85,
"rsi": 45.739,
"ret": -0.0050378 
},
{
 "date":   -916,
"name": "GSPC.Close",
"price":  90.64,
"rsi": 41.745,
"ret": -0.0023115 
},
{
 "date":   -913,
"name": "GSPC.Close",
"price":  90.91,
"rsi": 40.027,
"ret": 0.0029788 
},
{
 "date":   -911,
"name": "GSPC.Close",
"price":  91.36,
"rsi": 43.261,
"ret": 0.00495 
},
{
 "date":   -910,
"name": "GSPC.Close",
"price":  91.32,
"rsi": 48.267,
"ret": -0.00043783 
},
{
 "date":   -909,
"name": "GSPC.Close",
"price":  91.69,
"rsi": 47.863,
"ret": 0.0040517 
},
{
 "date":   -906,
"name": "GSPC.Close",
"price":  92.05,
"rsi": 51.878,
"ret": 0.0039263 
},
{
 "date":   -905,
"name": "GSPC.Close",
"price":  92.48,
"rsi": 55.471,
"ret": 0.0046714 
},
{
 "date":   -904,
"name": "GSPC.Close",
"price":   92.4,
"rsi": 59.373,
"ret": -0.00086505 
},
{
 "date":   -903,
"name": "GSPC.Close",
"price":  92.42,
"rsi": 58.348,
"ret": 0.00021645 
},
{
 "date":   -902,
"name": "GSPC.Close",
"price":  92.74,
"rsi": 58.541,
"ret": 0.0034625 
},
{
 "date":   -899,
"name": "GSPC.Close",
"price":  92.75,
"rsi":   61.6,
"ret": 0.00010783 
},
{
 "date":   -898,
"name": "GSPC.Close",
"price":   93.5,
"rsi": 61.696,
"ret": 0.0080863 
},
{
 "date":   -897,
"name": "GSPC.Close",
"price":  93.65,
"rsi": 68.082,
"ret": 0.0016043 
},
{
 "date":   -896,
"name": "GSPC.Close",
"price":  93.85,
"rsi": 69.188,
"ret": 0.0021356 
},
{
 "date":   -895,
"name": "GSPC.Close",
"price":  94.04,
"rsi": 70.649,
"ret": 0.0020245 
},
{
 "date":   -892,
"name": "GSPC.Close",
"price":  93.73,
"rsi": 72.007,
"ret": -0.0032965 
},
{
 "date":   -891,
"name": "GSPC.Close",
"price":  93.24,
"rsi": 66.594,
"ret": -0.0052278 
},
{
 "date":   -890,
"name": "GSPC.Close",
"price":  94.06,
"rsi": 59.038,
"ret": 0.0087945 
},
{
 "date":   -889,
"name": "GSPC.Close",
"price":  94.35,
"rsi": 65.992,
"ret": 0.0030831 
},
{
 "date":   -888,
"name": "GSPC.Close",
"price":  94.49,
"rsi": 68.057,
"ret": 0.0014838 
},
{
 "date":   -885,
"name": "GSPC.Close",
"price":  94.75,
"rsi": 69.035,
"ret": 0.0027516 
},
{
 "date":   -884,
"name": "GSPC.Close",
"price":  95.37,
"rsi": 70.821,
"ret": 0.0065435 
},
{
 "date":   -883,
"name": "GSPC.Close",
"price":  95.78,
"rsi": 74.586,
"ret": 0.004299 
},
{
 "date":   -882,
"name": "GSPC.Close",
"price":  95.66,
"rsi": 76.724,
"ret": -0.0012529 
},
{
 "date":   -881,
"name": "GSPC.Close",
"price":  95.83,
"rsi": 74.742,
"ret": 0.0017771 
},
{
 "date":   -878,
"name": "GSPC.Close",
"price":  95.58,
"rsi":   75.7,
"ret": -0.0026088 
},
{
 "date":   -877,
"name": "GSPC.Close",
"price":  95.69,
"rsi": 71.411,
"ret": 0.0011509 
},
{
 "date":   -876,
"name": "GSPC.Close",
"price":  95.78,
"rsi": 72.158,
"ret": 0.00094054 
},
{
 "date":   -875,
"name": "GSPC.Close",
"price":  95.53,
"rsi": 72.785,
"ret": -0.0026101 
},
{
 "date":   -874,
"name": "GSPC.Close",
"price":  95.15,
"rsi": 68.191,
"ret": -0.0039778 
},
{
 "date":   -871,
"name": "GSPC.Close",
"price":  94.64,
"rsi": 61.806,
"ret": -0.00536 
},
{
 "date":   -870,
"name": "GSPC.Close",
"price":  94.77,
"rsi": 54.439,
"ret": 0.0013736 
},
{
 "date":   -869,
"name": "GSPC.Close",
"price":  94.55,
"rsi": 55.882,
"ret": -0.0023214 
},
{
 "date":   -868,
"name": "GSPC.Close",
"price":  94.63,
"rsi": 52.831,
"ret": 0.00084611 
},
{
 "date":   -867,
"name": "GSPC.Close",
"price":  94.78,
"rsi": 53.819,
"ret": 0.0015851 
},
{
 "date":   -864,
"name": "GSPC.Close",
"price":  94.25,
"rsi": 55.692,
"ret": -0.0055919 
},
{
 "date":   -863,
"name": "GSPC.Close",
"price":  93.74,
"rsi": 48.247,
"ret": -0.0054111 
},
{
 "date":   -862,
"name": "GSPC.Close",
"price":  93.61,
"rsi": 42.376,
"ret": -0.0013868 
},
{
 "date":   -861,
"name": "GSPC.Close",
"price":  93.09,
"rsi": 41.007,
"ret": -0.005555 
},
{
 "date":   -860,
"name": "GSPC.Close",
"price":   92.7,
"rsi": 35.995,
"ret": -0.0041895 
},
{
 "date":   -857,
"name": "GSPC.Close",
"price":  92.64,
"rsi": 32.761,
"ret": -0.00064725 
},
{
 "date":   -856,
"name": "GSPC.Close",
"price":  92.88,
"rsi": 32.281,
"ret": 0.0025907 
},
{
 "date":   -855,
"name": "GSPC.Close",
"price":  93.07,
"rsi": 36.305,
"ret": 0.0020457 
},
{
 "date":   -854,
"name": "GSPC.Close",
"price":  93.64,
"rsi": 39.376,
"ret": 0.0061244 
},
{
 "date":   -853,
"name": "GSPC.Close",
"price":  93.68,
"rsi": 47.548,
"ret": 0.00042717 
},
{
 "date":   -849,
"name": "GSPC.Close",
"price":  94.21,
"rsi": 48.077,
"ret": 0.0056576 
},
{
 "date":   -848,
"name": "GSPC.Close",
"price":  94.39,
"rsi": 54.608,
"ret": 0.0019106 
},
{
 "date":   -847,
"name": "GSPC.Close",
"price":  94.33,
"rsi": 56.605,
"ret": -0.00063566 
},
{
 "date":   -846,
"name": "GSPC.Close",
"price":  94.36,
"rsi": 55.725,
"ret": 0.00031803 
},
{
 "date":   -843,
"name": "GSPC.Close",
"price":  94.54,
"rsi": 56.093,
"ret": 0.0019076 
},
{
 "date":   -842,
"name": "GSPC.Close",
"price":  94.99,
"rsi": 58.328,
"ret": 0.0047599 
},
{
 "date":   -841,
"name": "GSPC.Close",
"price":  95.99,
"rsi":  63.35,
"ret": 0.010527 
},
{
 "date":   -840,
"name": "GSPC.Close",
"price":   96.2,
"rsi": 71.555,
"ret": 0.0021877 
},
{
 "date":   -839,
"name": "GSPC.Close",
"price":  96.27,
"rsi": 72.926,
"ret": 0.00072765 
},
{
 "date":   -836,
"name": "GSPC.Close",
"price":  96.53,
"rsi": 73.386,
"ret": 0.0027007 
},
{
 "date":   -835,
"name": "GSPC.Close",
"price":  96.17,
"rsi": 75.081,
"ret": -0.0037294 
},
{
 "date":   -834,
"name": "GSPC.Close",
"price":  96.13,
"rsi": 68.569,
"ret": -0.00041593 
},
{
 "date":   -833,
"name": "GSPC.Close",
"price":  96.75,
"rsi": 67.865,
"ret": 0.0064496 
},
{
 "date":   -832,
"name": "GSPC.Close",
"price":     97,
"rsi": 72.568,
"ret": 0.002584 
},
{
 "date":   -829,
"name": "GSPC.Close",
"price":  97.59,
"rsi": 74.207,
"ret": 0.0060825 
},
{
 "date":   -828,
"name": "GSPC.Close",
"price":  96.76,
"rsi": 77.608,
"ret": -0.008505 
},
{
 "date":   -827,
"name": "GSPC.Close",
"price":  96.79,
"rsi": 64.687,
"ret": 0.00031005 
},
{
 "date":   -826,
"name": "GSPC.Close",
"price":  96.79,
"rsi": 64.914,
"ret":      0 
},
{
 "date":   -825,
"name": "GSPC.Close",
"price":  96.71,
"rsi": 64.914,
"ret": -0.00082653 
},
{
 "date":   -822,
"name": "GSPC.Close",
"price":  96.32,
"rsi": 63.647,
"ret": -0.0040327 
},
{
 "date":   -821,
"name": "GSPC.Close",
"price":  96.65,
"rsi": 57.729,
"ret": 0.0034261 
},
{
 "date":   -820,
"name": "GSPC.Close",
"price":  96.43,
"rsi": 61.031,
"ret": -0.0022763 
},
{
 "date":   -819,
"name": "GSPC.Close",
"price":  96.67,
"rsi":  57.79,
"ret": 0.0024889 
},
{
 "date":   -818,
"name": "GSPC.Close",
"price":  97.26,
"rsi": 60.269,
"ret": 0.0061032 
},
{
 "date":   -815,
"name": "GSPC.Close",
"price":  97.51,
"rsi": 65.614,
"ret": 0.0025704 
},
{
 "date":   -814,
"name": "GSPC.Close",
"price":  96.84,
"rsi": 67.603,
"ret": -0.0068711 
},
{
 "date":   -813,
"name": "GSPC.Close",
"price":  96.37,
"rsi": 57.932,
"ret": -0.0048534 
},
{
 "date":   -812,
"name": "GSPC.Close",
"price":  95.75,
"rsi": 52.282,
"ret": -0.0064335 
},
{
 "date":   -811,
"name": "GSPC.Close",
"price":     96,
"rsi": 45.919,
"ret": 0.002611 
},
{
 "date":   -808,
"name": "GSPC.Close",
"price":  95.25,
"rsi": 48.634,
"ret": -0.0078125 
},
{
 "date":   -807,
"name": "GSPC.Close",
"price":     95,
"rsi": 41.847,
"ret": -0.0026247 
},
{
 "date":   -806,
"name": "GSPC.Close",
"price":  95.25,
"rsi": 39.851,
"ret": 0.0026316 
},
{
 "date":   -805,
"name": "GSPC.Close",
"price":  95.43,
"rsi":  42.79,
"ret": 0.0018898 
},
{
 "date":   -804,
"name": "GSPC.Close",
"price":  95.38,
"rsi": 44.878,
"ret": -0.00052394 
},
{
 "date":   -801,
"name": "GSPC.Close",
"price":  94.96,
"rsi": 44.394,
"ret": -0.0044034 
},
{
 "date":   -800,
"name": "GSPC.Close",
"price":  94.42,
"rsi": 40.442,
"ret": -0.0056866 
},
{
 "date":   -799,
"name": "GSPC.Close",
"price":  94.52,
"rsi": 36.004,
"ret": 0.0010591 
},
{
 "date":   -798,
"name": "GSPC.Close",
"price":  94.94,
"rsi": 37.375,
"ret": 0.0044435 
},
{
 "date":   -797,
"name": "GSPC.Close",
"price":  94.96,
"rsi": 42.905,
"ret": 0.00021066 
},
{
 "date":   -794,
"name": "GSPC.Close",
"price":  94.79,
"rsi": 43.162,
"ret": -0.0017902 
},
{
 "date":   -793,
"name": "GSPC.Close",
"price":   93.3,
"rsi": 41.452,
"ret": -0.015719 
},
{
 "date":   -792,
"name": "GSPC.Close",
"price":  92.71,
"rsi": 30.167,
"ret": -0.0063237 
},
{
 "date":   -791,
"name": "GSPC.Close",
"price":  92.34,
"rsi": 27.029,
"ret": -0.0039909 
},
{
 "date":   -790,
"name": "GSPC.Close",
"price":  91.78,
"rsi": 25.255,
"ret": -0.0060645 
},
{
 "date":   -787,
"name": "GSPC.Close",
"price":  91.48,
"rsi": 22.814,
"ret": -0.0032687 
},
{
 "date":   -785,
"name": "GSPC.Close",
"price":  91.14,
"rsi":  21.61,
"ret": -0.0037167 
},
{
 "date":   -784,
"name": "GSPC.Close",
"price":  91.59,
"rsi": 20.301,
"ret": 0.0049375 
},
{
 "date":   -783,
"name": "GSPC.Close",
"price":  92.21,
"rsi": 26.633,
"ret": 0.0067693 
},
{
 "date":   -780,
"name": "GSPC.Close",
"price":  91.97,
"rsi":  34.37,
"ret": -0.0026028 
},
{
 "date":   -779,
"name": "GSPC.Close",
"price":  91.39,
"rsi": 32.923,
"ret": -0.0063064 
},
{
 "date":   -778,
"name": "GSPC.Close",
"price":  91.76,
"rsi": 29.671,
"ret": 0.0040486 
},
{
 "date":   -777,
"name": "GSPC.Close",
"price":   92.6,
"rsi":  34.14,
"ret": 0.0091543 
},
{
 "date":   -776,
"name": "GSPC.Close",
"price":  92.82,
"rsi": 42.996,
"ret": 0.0023758 
},
{
 "date":   -773,
"name": "GSPC.Close",
"price":  91.65,
"rsi": 45.079,
"ret": -0.012605 
},
{
 "date":   -772,
"name": "GSPC.Close",
"price":   93.1,
"rsi": 37.278,
"ret": 0.015821 
},
{
 "date":   -771,
"name": "GSPC.Close",
"price":  93.65,
"rsi": 49.047,
"ret": 0.0059076 
},
{
 "date":   -769,
"name": "GSPC.Close",
"price":   93.9,
"rsi": 52.674,
"ret": 0.0026695 
},
{
 "date":   -766,
"name": "GSPC.Close",
"price":  94.17,
"rsi": 54.268,
"ret": 0.0028754 
},
{
 "date":   -765,
"name": "GSPC.Close",
"price":  94.49,
"rsi": 55.992,
"ret": 0.0033981 
},
{
 "date":   -764,
"name": "GSPC.Close",
"price":  94.47,
"rsi": 58.011,
"ret": -0.00021166 
},
{
 "date":   -763,
"name": "GSPC.Close",
"price":     94,
"rsi": 57.833,
"ret": -0.0049751 
},
{
 "date":   -762,
"name": "GSPC.Close",
"price":   94.5,
"rsi": 53.651,
"ret": 0.0053191 
},
{
 "date":   -759,
"name": "GSPC.Close",
"price":   95.1,
"rsi": 57.197,
"ret": 0.0063492 
},
{
 "date":   -758,
"name": "GSPC.Close",
"price":  95.23,
"rsi": 61.048,
"ret": 0.001367 
},
{
 "date":   -757,
"name": "GSPC.Close",
"price":  95.64,
"rsi": 61.849,
"ret": 0.0043054 
},
{
 "date":   -756,
"name": "GSPC.Close",
"price":  95.53,
"rsi": 64.339,
"ret": -0.0011501 
},
{
 "date":   -755,
"name": "GSPC.Close",
"price":  95.42,
"rsi": 63.148,
"ret": -0.0011515 
},
{
 "date":   -752,
"name": "GSPC.Close",
"price":  95.12,
"rsi": 61.914,
"ret": -0.003144 
},
{
 "date":   -751,
"name": "GSPC.Close",
"price":  95.01,
"rsi": 58.553,
"ret": -0.0011564 
},
{
 "date":   -750,
"name": "GSPC.Close",
"price":  95.34,
"rsi": 57.324,
"ret": 0.0034733 
},
{
 "date":   -749,
"name": "GSPC.Close",
"price":  95.47,
"rsi": 60.034,
"ret": 0.0013635 
},
{
 "date":   -748,
"name": "GSPC.Close",
"price":  95.03,
"rsi": 61.082,
"ret": -0.0046088 
},
{
 "date":   -745,
"name": "GSPC.Close",
"price":  94.77,
"rsi": 55.751,
"ret": -0.002736 
},
{
 "date":   -744,
"name": "GSPC.Close",
"price":  94.63,
"rsi": 52.818,
"ret": -0.0014773 
},
{
 "date":   -743,
"name": "GSPC.Close",
"price":  95.15,
"rsi": 51.254,
"ret": 0.0054951 
},
{
 "date":   -742,
"name": "GSPC.Close",
"price":  95.38,
"rsi": 56.416,
"ret": 0.0024172 
},
{
 "date":   -741,
"name": "GSPC.Close",
"price":   95.2,
"rsi": 58.508,
"ret": -0.0018872 
},
{
 "date":   -737,
"name": "GSPC.Close",
"price":  95.26,
"rsi": 56.233,
"ret": 0.00063025 
},
{
 "date":   -736,
"name": "GSPC.Close",
"price":  95.91,
"rsi": 56.835,
"ret": 0.0068234 
},
{
 "date":   -735,
"name": "GSPC.Close",
"price":  95.89,
"rsi":  62.81,
"ret": -0.00020853 
},
{
 "date":   -734,
"name": "GSPC.Close",
"price":  96.47,
"rsi": 62.523,
"ret": 0.0060486 
},
{
 "date":   -730,
"name": "GSPC.Close",
"price":  96.11,
"rsi":   67.2,
"ret": -0.0037317 
},
{
 "date":   -729,
"name": "GSPC.Close",
"price":  95.67,
"rsi": 62.026,
"ret": -0.0045781 
},
{
 "date":   -728,
"name": "GSPC.Close",
"price":  95.36,
"rsi": 56.319,
"ret": -0.0032403 
},
{
 "date":   -727,
"name": "GSPC.Close",
"price":  95.94,
"rsi": 52.643,
"ret": 0.0060822 
},
{
 "date":   -724,
"name": "GSPC.Close",
"price":  96.62,
"rsi": 58.147,
"ret": 0.0070878 
},
{
 "date":   -723,
"name": "GSPC.Close",
"price":   96.5,
"rsi": 63.502,
"ret": -0.001242 
},
{
 "date":   -722,
"name": "GSPC.Close",
"price":  96.52,
"rsi": 61.994,
"ret": 0.00020725 
},
{
 "date":   -721,
"name": "GSPC.Close",
"price":  96.62,
"rsi": 62.156,
"ret": 0.0010361 
},
{
 "date":   -720,
"name": "GSPC.Close",
"price":  96.72,
"rsi": 63.001,
"ret": 0.001035 
},
{
 "date":   -717,
"name": "GSPC.Close",
"price":  96.42,
"rsi":  63.87,
"ret": -0.0031017 
},
{
 "date":   -716,
"name": "GSPC.Close",
"price":  95.82,
"rsi": 59.365,
"ret": -0.0062228 
},
{
 "date":   -715,
"name": "GSPC.Close",
"price":  95.64,
"rsi": 51.536,
"ret": -0.0018785 
},
{
 "date":   -714,
"name": "GSPC.Close",
"price":  95.56,
"rsi": 49.429,
"ret": -0.00083647 
},
{
 "date":   -713,
"name": "GSPC.Close",
"price":  95.24,
"rsi": 48.481,
"ret": -0.0033487 
},
{
 "date":   -710,
"name": "GSPC.Close",
"price":  94.03,
"rsi":  44.78,
"ret": -0.012705 
},
{
 "date":   -709,
"name": "GSPC.Close",
"price":  93.66,
"rsi": 34.161,
"ret": -0.0039349 
},
{
 "date":   -708,
"name": "GSPC.Close",
"price":  93.17,
"rsi": 31.687,
"ret": -0.0052317 
},
{
 "date":   -707,
"name": "GSPC.Close",
"price":   93.3,
"rsi":  28.72,
"ret": 0.0013953 
},
{
 "date":   -706,
"name": "GSPC.Close",
"price":  93.45,
"rsi": 30.577,
"ret": 0.0016077 
},
{
 "date":   -703,
"name": "GSPC.Close",
"price":  93.35,
"rsi": 32.754,
"ret": -0.0010701 
},
{
 "date":   -702,
"name": "GSPC.Close",
"price":  92.89,
"rsi": 32.033,
"ret": -0.0049277 
},
{
 "date":   -701,
"name": "GSPC.Close",
"price":  92.24,
"rsi": 28.882,
"ret": -0.0069975 
},
{
 "date":   -700,
"name": "GSPC.Close",
"price":  92.56,
"rsi": 25.122,
"ret": 0.0034692 
},
{
 "date":   -699,
"name": "GSPC.Close",
"price":  92.27,
"rsi": 29.957,
"ret": -0.0031331 
},
{
 "date":   -696,
"name": "GSPC.Close",
"price":  91.87,
"rsi": 28.181,
"ret": -0.0043351 
},
{
 "date":   -695,
"name": "GSPC.Close",
"price":   91.9,
"rsi": 25.901,
"ret": 0.00032655 
},
{
 "date":   -694,
"name": "GSPC.Close",
"price":  92.06,
"rsi": 26.382,
"ret": 0.001741 
},
{
 "date":   -693,
"name": "GSPC.Close",
"price":   90.9,
"rsi": 29.029,
"ret": -0.0126 
},
{
 "date":   -692,
"name": "GSPC.Close",
"price":  89.86,
"rsi": 22.666,
"ret": -0.011441 
},
{
 "date":   -688,
"name": "GSPC.Close",
"price":  89.07,
"rsi": 18.707,
"ret": -0.0087915 
},
{
 "date":   -687,
"name": "GSPC.Close",
"price":  90.14,
"rsi": 16.368,
"ret": 0.012013 
},
{
 "date":   -686,
"name": "GSPC.Close",
"price":   90.3,
"rsi": 29.267,
"ret": 0.001775 
},
{
 "date":   -685,
"name": "GSPC.Close",
"price":  89.96,
"rsi": 30.981,
"ret": -0.0037652 
},
{
 "date":   -682,
"name": "GSPC.Close",
"price":  90.31,
"rsi": 29.353,
"ret": 0.0038906 
},
{
 "date":   -681,
"name": "GSPC.Close",
"price":  91.24,
"rsi": 33.242,
"ret": 0.010298 
},
{
 "date":   -680,
"name": "GSPC.Close",
"price":  91.24,
"rsi": 42.327,
"ret":      0 
},
{
 "date":   -678,
"name": "GSPC.Close",
"price":  90.89,
"rsi": 42.327,
"ret": -0.003836 
},
{
 "date":   -675,
"name": "GSPC.Close",
"price":  90.18,
"rsi": 39.954,
"ret": -0.0078116 
},
{
 "date":   -674,
"name": "GSPC.Close",
"price":  90.53,
"rsi": 35.594,
"ret": 0.0038811 
},
{
 "date":   -673,
"name": "GSPC.Close",
"price":  90.08,
"rsi": 39.121,
"ret": -0.0049707 
},
{
 "date":   -672,
"name": "GSPC.Close",
"price":  89.36,
"rsi": 36.364,
"ret": -0.0079929 
},
{
 "date":   -671,
"name": "GSPC.Close",
"price":  89.11,
"rsi": 32.426,
"ret": -0.0027977 
},
{
 "date":   -668,
"name": "GSPC.Close",
"price":  87.92,
"rsi": 31.164,
"ret": -0.013354 
},
{
 "date":   -667,
"name": "GSPC.Close",
"price":  87.72,
"rsi": 25.981,
"ret": -0.0022748 
},
{
 "date":   -666,
"name": "GSPC.Close",
"price":  89.26,
"rsi": 25.222,
"ret": 0.017556 
},
{
 "date":   -665,
"name": "GSPC.Close",
"price":   89.1,
"rsi": 39.808,
"ret": -0.0017925 
},
{
 "date":   -664,
"name": "GSPC.Close",
"price":  89.03,
"rsi": 38.957,
"ret": -0.00078563 
},
{
 "date":   -661,
"name": "GSPC.Close",
"price":  90.13,
"rsi": 38.569,
"ret": 0.012355 
},
{
 "date":   -660,
"name": "GSPC.Close",
"price":  90.23,
"rsi": 47.432,
"ret": 0.0011095 
},
{
 "date":   -659,
"name": "GSPC.Close",
"price":  90.03,
"rsi": 48.164,
"ret": -0.0022166 
},
{
 "date":   -658,
"name": "GSPC.Close",
"price":  88.32,
"rsi": 46.761,
"ret": -0.018994 
},
{
 "date":   -657,
"name": "GSPC.Close",
"price":   89.1,
"rsi": 36.873,
"ret": 0.0088315 
},
{
 "date":   -654,
"name": "GSPC.Close",
"price":  89.59,
"rsi": 42.813,
"ret": 0.0054994 
},
{
 "date":   -653,
"name": "GSPC.Close",
"price":  88.99,
"rsi": 46.236,
"ret": -0.0066972 
},
{
 "date":   -652,
"name": "GSPC.Close",
"price":  88.98,
"rsi": 42.854,
"ret": -0.00011237 
},
{
 "date":   -651,
"name": "GSPC.Close",
"price":  88.33,
"rsi": 42.798,
"ret": -0.007305 
},
{
 "date":   -650,
"name": "GSPC.Close",
"price":  88.42,
"rsi":   39.2,
"ret": 0.0010189 
},
{
 "date":   -647,
"name": "GSPC.Close",
"price":  88.33,
"rsi": 39.952,
"ret": -0.0010179 
},
{
 "date":   -646,
"name": "GSPC.Close",
"price":  88.93,
"rsi": 39.427,
"ret": 0.0067927 
},
{
 "date":   -645,
"name": "GSPC.Close",
"price":  89.66,
"rsi": 44.655,
"ret": 0.0082087 
},
{
 "date":   -644,
"name": "GSPC.Close",
"price":  89.57,
"rsi": 50.278,
"ret": -0.0010038 
},
{
 "date":   -643,
"name": "GSPC.Close",
"price":   90.2,
"rsi": 49.609,
"ret": 0.0070336 
},
{
 "date":   -640,
"name": "GSPC.Close",
"price":  92.48,
"rsi": 54.204,
"ret": 0.025277 
},
{
 "date":   -639,
"name": "GSPC.Close",
"price":  92.64,
"rsi": 66.212,
"ret": 0.0017301 
},
{
 "date":   -638,
"name": "GSPC.Close",
"price":  93.47,
"rsi": 66.869,
"ret": 0.0089594 
},
{
 "date":   -637,
"name": "GSPC.Close",
"price":  93.84,
"rsi": 70.113,
"ret": 0.0039585 
},
{
 "date":   -636,
"name": "GSPC.Close",
"price":  93.29,
"rsi": 71.455,
"ret": -0.005861 
},
{
 "date":   -633,
"name": "GSPC.Close",
"price":  94.95,
"rsi": 66.664,
"ret": 0.017794 
},
{
 "date":   -631,
"name": "GSPC.Close",
"price":  95.67,
"rsi": 72.629,
"ret": 0.0075829 
},
{
 "date":   -630,
"name": "GSPC.Close",
"price":  96.53,
"rsi": 74.741,
"ret": 0.0089892 
},
{
 "date":   -626,
"name": "GSPC.Close",
"price":  96.59,
"rsi": 77.021,
"ret": 0.00062157 
},
{
 "date":   -625,
"name": "GSPC.Close",
"price":  96.62,
"rsi": 77.176,
"ret": 0.00031059 
},
{
 "date":   -624,
"name": "GSPC.Close",
"price":  96.81,
"rsi": 77.258,
"ret": 0.0019665 
},
{
 "date":   -623,
"name": "GSPC.Close",
"price":  97.08,
"rsi": 77.805,
"ret": 0.002789 
},
{
 "date":   -622,
"name": "GSPC.Close",
"price":  95.85,
"rsi": 78.593,
"ret": -0.01267 
},
{
 "date":   -619,
"name": "GSPC.Close",
"price":  95.32,
"rsi": 66.933,
"ret": -0.0055295 
},
{
 "date":   -618,
"name": "GSPC.Close",
"price":  96.62,
"rsi": 62.621,
"ret": 0.013638 
},
{
 "date":   -617,
"name": "GSPC.Close",
"price":  96.92,
"rsi": 68.056,
"ret": 0.0031049 
},
{
 "date":   -616,
"name": "GSPC.Close",
"price":  96.62,
"rsi": 69.171,
"ret": -0.0030953 
},
{
 "date":   -615,
"name": "GSPC.Close",
"price":  97.21,
"rsi": 66.667,
"ret": 0.0061064 
},
{
 "date":   -612,
"name": "GSPC.Close",
"price":  97.97,
"rsi":  69.04,
"ret": 0.0078181 
},
{
 "date":   -611,
"name": "GSPC.Close",
"price":  97.46,
"rsi": 71.824,
"ret": -0.0052057 
},
{
 "date":   -610,
"name": "GSPC.Close",
"price":  97.97,
"rsi": 67.442,
"ret": 0.0052329 
},
{
 "date":   -609,
"name": "GSPC.Close",
"price":  98.59,
"rsi": 69.449,
"ret": 0.0063285 
},
{
 "date":   -608,
"name": "GSPC.Close",
"price":  98.66,
"rsi": 71.731,
"ret": 0.00071001 
},
{
 "date":   -605,
"name": "GSPC.Close",
"price":  98.35,
"rsi": 71.985,
"ret": -0.0031421 
},
{
 "date":   -604,
"name": "GSPC.Close",
"price":   98.9,
"rsi": 69.023,
"ret": 0.0055923 
},
{
 "date":   -603,
"name": "GSPC.Close",
"price":  98.91,
"rsi": 71.281,
"ret": 0.00010111 
},
{
 "date":   -602,
"name": "GSPC.Close",
"price":  98.39,
"rsi": 71.322,
"ret": -0.0052573 
},
{
 "date":   -601,
"name": "GSPC.Close",
"price":   98.5,
"rsi":  66.05,
"ret": 0.001118 
},
{
 "date":   -598,
"name": "GSPC.Close",
"price":  98.19,
"rsi": 66.612,
"ret": -0.0031472 
},
{
 "date":   -597,
"name": "GSPC.Close",
"price":  98.12,
"rsi": 63.424,
"ret": -0.0007129 
},
{
 "date":   -596,
"name": "GSPC.Close",
"price":  98.07,
"rsi": 62.695,
"ret": -0.00050958 
},
{
 "date":   -595,
"name": "GSPC.Close",
"price":   97.6,
"rsi": 62.145,
"ret": -0.0047925 
},
{
 "date":   -594,
"name": "GSPC.Close",
"price":   96.9,
"rsi": 57.077,
"ret": -0.0071721 
},
{
 "date":   -591,
"name": "GSPC.Close",
"price":  96.45,
"rsi": 50.475,
"ret": -0.004644 
},
{
 "date":   -590,
"name": "GSPC.Close",
"price":  96.93,
"rsi": 46.733,
"ret": 0.0049767 
},
{
 "date":   -589,
"name": "GSPC.Close",
"price":  97.18,
"rsi": 50.913,
"ret": 0.0025792 
},
{
 "date":   -588,
"name": "GSPC.Close",
"price":  96.97,
"rsi": 52.983,
"ret": -0.0021609 
},
{
 "date":   -587,
"name": "GSPC.Close",
"price":  97.15,
"rsi": 51.036,
"ret": 0.0018562 
},
{
 "date":   -584,
"name": "GSPC.Close",
"price":  96.99,
"rsi": 52.643,
"ret": -0.0016469 
},
{
 "date":   -583,
"name": "GSPC.Close",
"price":  97.62,
"rsi":  51.04,
"ret": 0.0064955 
},
{
 "date":   -582,
"name": "GSPC.Close",
"price":  97.92,
"rsi": 56.638,
"ret": 0.0030731 
},
{
 "date":   -580,
"name": "GSPC.Close",
"price":  98.68,
"rsi":  59.04,
"ret": 0.0077614 
},
{
 "date":   -577,
"name": "GSPC.Close",
"price":  99.99,
"rsi": 64.416,
"ret": 0.013275 
},
{
 "date":   -576,
"name": "GSPC.Close",
"price": 100.38,
"rsi": 71.388,
"ret": 0.0039004 
},
{
 "date":   -575,
"name": "GSPC.Close",
"price":  99.89,
"rsi":  73.08,
"ret": -0.0048815 
},
{
 "date":   -574,
"name": "GSPC.Close",
"price": 100.65,
"rsi": 67.668,
"ret": 0.0076084 
},
{
 "date":   -573,
"name": "GSPC.Close",
"price": 101.27,
"rsi": 71.227,
"ret": 0.00616 
},
{
 "date":   -570,
"name": "GSPC.Close",
"price": 101.41,
"rsi": 73.764,
"ret": 0.0013824 
},
{
 "date":   -569,
"name": "GSPC.Close",
"price": 101.66,
"rsi": 74.315,
"ret": 0.0024652 
},
{
 "date":   -567,
"name": "GSPC.Close",
"price": 101.25,
"rsi": 75.311,
"ret": -0.0040331 
},
{
 "date":   -566,
"name": "GSPC.Close",
"price": 101.13,
"rsi": 70.481,
"ret": -0.0011852 
},
{
 "date":   -563,
"name": "GSPC.Close",
"price": 100.13,
"rsi": 69.085,
"ret": -0.0098883 
},
{
 "date":   -562,
"name": "GSPC.Close",
"price":  99.99,
"rsi": 58.654,
"ret": -0.0013982 
},
{
 "date":   -560,
"name": "GSPC.Close",
"price": 101.51,
"rsi": 57.349,
"ret": 0.015202 
},
{
 "date":   -559,
"name": "GSPC.Close",
"price": 100.66,
"rsi": 66.156,
"ret": -0.0083736 
},
{
 "date":   -556,
"name": "GSPC.Close",
"price": 100.39,
"rsi": 58.839,
"ret": -0.0026823 
},
{
 "date":   -555,
"name": "GSPC.Close",
"price": 100.08,
"rsi": 56.694,
"ret": -0.003088 
},
{
 "date":   -553,
"name": "GSPC.Close",
"price":  99.98,
"rsi": 54.249,
"ret": -0.0009992 
},
{
 "date":   -552,
"name": "GSPC.Close",
"price":  99.58,
"rsi": 53.448,
"ret": -0.0040008 
},
{
 "date":   -549,
"name": "GSPC.Close",
"price":   99.4,
"rsi": 50.252,
"ret": -0.0018076 
},
{
 "date":   -548,
"name": "GSPC.Close",
"price":  99.74,
"rsi": 48.837,
"ret": 0.0034205 
},
{
 "date":   -547,
"name": "GSPC.Close",
"price": 100.91,
"rsi": 51.609,
"ret": 0.01173 
},
{
 "date":   -542,
"name": "GSPC.Close",
"price": 101.94,
"rsi":   59.7,
"ret": 0.010207 
},
{
 "date":   -541,
"name": "GSPC.Close",
"price": 102.23,
"rsi": 65.215,
"ret": 0.0028448 
},
{
 "date":   -539,
"name": "GSPC.Close",
"price": 102.39,
"rsi":   66.6,
"ret": 0.0015651 
},
{
 "date":   -538,
"name": "GSPC.Close",
"price": 102.34,
"rsi": 67.373,
"ret": -0.00048833 
},
{
 "date":   -535,
"name": "GSPC.Close",
"price": 102.26,
"rsi": 66.852,
"ret": -0.00078171 
},
{
 "date":   -534,
"name": "GSPC.Close",
"price":  101.7,
"rsi": 65.975,
"ret": -0.0054762 
},
{
 "date":   -532,
"name": "GSPC.Close",
"price": 101.44,
"rsi": 60.033,
"ret": -0.0025565 
},
{
 "date":   -531,
"name": "GSPC.Close",
"price": 100.46,
"rsi": 57.446,
"ret": -0.0096609 
},
{
 "date":   -528,
"name": "GSPC.Close",
"price":  99.33,
"rsi": 48.893,
"ret": -0.011248 
},
{
 "date":   -527,
"name": "GSPC.Close",
"price":  99.21,
"rsi": 41.265,
"ret": -0.0012081 
},
{
 "date":   -525,
"name": "GSPC.Close",
"price":  97.94,
"rsi": 40.542,
"ret": -0.012801 
},
{
 "date":   -524,
"name": "GSPC.Close",
"price":  98.34,
"rsi":  33.79,
"ret": 0.0040841 
},
{
 "date":   -521,
"name": "GSPC.Close",
"price":  97.65,
"rsi":  37.33,
"ret": -0.0070165 
},
{
 "date":   -520,
"name": "GSPC.Close",
"price":  97.74,
"rsi": 33.957,
"ret": 0.00092166 
},
{
 "date":   -518,
"name": "GSPC.Close",
"price":  97.28,
"rsi": 34.785,
"ret": -0.0047064 
},
{
 "date":   -517,
"name": "GSPC.Close",
"price":  96.63,
"rsi":  32.54,
"ret": -0.0066817 
},
{
 "date":   -514,
"name": "GSPC.Close",
"price":  96.85,
"rsi": 29.631,
"ret": 0.0022767 
},
{
 "date":   -513,
"name": "GSPC.Close",
"price":  97.25,
"rsi": 31.852,
"ret": 0.0041301 
},
{
 "date":   -511,
"name": "GSPC.Close",
"price":  97.04,
"rsi": 35.818,
"ret": -0.0021594 
},
{
 "date":   -510,
"name": "GSPC.Close",
"price":  97.01,
"rsi": 34.677,
"ret": -0.00030915 
},
{
 "date":   -507,
"name": "GSPC.Close",
"price":  98.01,
"rsi": 34.508,
"ret": 0.010308 
},
{
 "date":   -506,
"name": "GSPC.Close",
"price":  98.53,
"rsi": 44.267,
"ret": 0.0053056 
},
{
 "date":   -504,
"name": "GSPC.Close",
"price":  98.07,
"rsi": 48.559,
"ret": -0.0046686 
},
{
 "date":   -503,
"name": "GSPC.Close",
"price":  98.68,
"rsi":  45.24,
"ret": 0.00622 
},
{
 "date":   -500,
"name": "GSPC.Close",
"price":     99,
"rsi":  50.11,
"ret": 0.0032428 
},
{
 "date":   -499,
"name": "GSPC.Close",
"price":  98.96,
"rsi": 52.496,
"ret": -0.00040404 
},
{
 "date":   -497,
"name": "GSPC.Close",
"price":   98.7,
"rsi": 52.161,
"ret": -0.0026273 
},
{
 "date":   -496,
"name": "GSPC.Close",
"price":  98.69,
"rsi": 49.924,
"ret": -0.00010132 
},
{
 "date":   -493,
"name": "GSPC.Close",
"price":  98.94,
"rsi": 49.836,
"ret": 0.0025332 
},
{
 "date":   -492,
"name": "GSPC.Close",
"price":  98.81,
"rsi": 52.121,
"ret": -0.0013139 
},
{
 "date":   -490,
"name": "GSPC.Close",
"price":  98.74,
"rsi": 50.824,
"ret": -0.00070843 
},
{
 "date":   -489,
"name": "GSPC.Close",
"price":  98.86,
"rsi": 50.102,
"ret": 0.0012153 
},
{
 "date":   -485,
"name": "GSPC.Close",
"price":  99.32,
"rsi": 51.378,
"ret": 0.004653 
},
{
 "date":   -484,
"name": "GSPC.Close",
"price": 100.02,
"rsi": 56.022,
"ret": 0.0070479 
},
{
 "date":   -483,
"name": "GSPC.Close",
"price": 100.74,
"rsi": 61.974,
"ret": 0.0071986 
},
{
 "date":   -482,
"name": "GSPC.Close",
"price":  101.2,
"rsi": 66.931,
"ret": 0.0045662 
},
{
 "date":   -479,
"name": "GSPC.Close",
"price": 101.23,
"rsi": 69.653,
"ret": 0.00029644 
},
{
 "date":   -478,
"name": "GSPC.Close",
"price": 100.73,
"rsi": 69.827,
"ret": -0.0049392 
},
{
 "date":   -476,
"name": "GSPC.Close",
"price": 100.52,
"rsi": 63.297,
"ret": -0.0020848 
},
{
 "date":   -475,
"name": "GSPC.Close",
"price": 100.86,
"rsi": 60.728,
"ret": 0.0033824 
},
{
 "date":   -472,
"name": "GSPC.Close",
"price": 101.24,
"rsi": 63.324,
"ret": 0.0037676 
},
{
 "date":   -471,
"name": "GSPC.Close",
"price":  101.5,
"rsi": 66.026,
"ret": 0.0025682 
},
{
 "date":   -469,
"name": "GSPC.Close",
"price": 101.59,
"rsi": 67.775,
"ret": 0.0008867 
},
{
 "date":   -468,
"name": "GSPC.Close",
"price": 101.66,
"rsi": 68.382,
"ret": 0.00068904 
},
{
 "date":   -465,
"name": "GSPC.Close",
"price": 102.24,
"rsi": 68.873,
"ret": 0.0057053 
},
{
 "date":   -464,
"name": "GSPC.Close",
"price": 102.59,
"rsi": 72.662,
"ret": 0.0034233 
},
{
 "date":   -462,
"name": "GSPC.Close",
"price": 102.36,
"rsi": 74.666,
"ret": -0.0022419 
},
{
 "date":   -461,
"name": "GSPC.Close",
"price": 102.31,
"rsi": 70.984,
"ret": -0.00048847 
},
{
 "date":   -458,
"name": "GSPC.Close",
"price": 102.67,
"rsi": 70.173,
"ret": 0.0035187 
},
{
 "date":   -457,
"name": "GSPC.Close",
"price": 102.86,
"rsi": 72.598,
"ret": 0.0018506 
},
{
 "date":   -455,
"name": "GSPC.Close",
"price": 103.22,
"rsi": 73.809,
"ret": 0.0034999 
},
{
 "date":   -454,
"name": "GSPC.Close",
"price": 103.71,
"rsi": 75.974,
"ret": 0.0047471 
},
{
 "date":   -451,
"name": "GSPC.Close",
"price":  103.7,
"rsi": 78.571,
"ret": -9.6423e-05 
},
{
 "date":   -450,
"name": "GSPC.Close",
"price": 103.74,
"rsi": 78.385,
"ret": 0.00038573 
},
{
 "date":   -448,
"name": "GSPC.Close",
"price": 103.29,
"rsi": 78.603,
"ret": -0.0043378 
},
{
 "date":   -447,
"name": "GSPC.Close",
"price": 103.18,
"rsi": 70.029,
"ret": -0.001065 
},
{
 "date":   -444,
"name": "GSPC.Close",
"price": 103.32,
"rsi": 68.074,
"ret": 0.0013569 
},
{
 "date":   -443,
"name": "GSPC.Close",
"price": 103.53,
"rsi": 69.251,
"ret": 0.0020325 
},
{
 "date":   -441,
"name": "GSPC.Close",
"price": 104.01,
"rsi": 70.978,
"ret": 0.0046363 
},
{
 "date":   -440,
"name": "GSPC.Close",
"price": 104.82,
"rsi": 74.504,
"ret": 0.0077877 
},
{
 "date":   -437,
"name": "GSPC.Close",
"price": 104.99,
"rsi": 79.115,
"ret": 0.0016218 
},
{
 "date":   -436,
"name": "GSPC.Close",
"price": 104.57,
"rsi": 79.936,
"ret": -0.0040004 
},
{
 "date":   -434,
"name": "GSPC.Close",
"price": 103.84,
"rsi": 72.373,
"ret": -0.006981 
},
{
 "date":   -433,
"name": "GSPC.Close",
"price":  104.2,
"rsi": 61.485,
"ret": 0.0034669 
},
{
 "date":   -430,
"name": "GSPC.Close",
"price":  103.9,
"rsi": 64.335,
"ret": -0.0028791 
},
{
 "date":   -429,
"name": "GSPC.Close",
"price":  103.3,
"rsi": 60.329,
"ret": -0.0057748 
},
{
 "date":   -427,
"name": "GSPC.Close",
"price": 103.41,
"rsi": 53.195,
"ret": 0.0010649 
},
{
 "date":   -426,
"name": "GSPC.Close",
"price": 103.06,
"rsi": 54.263,
"ret": -0.0033846 
},
{
 "date":   -423,
"name": "GSPC.Close",
"price":  103.1,
"rsi": 50.329,
"ret": 0.00038812 
},
{
 "date":   -421,
"name": "GSPC.Close",
"price": 103.27,
"rsi": 50.768,
"ret": 0.0016489 
},
{
 "date":   -420,
"name": "GSPC.Close",
"price":  103.5,
"rsi": 52.684,
"ret": 0.0022272 
},
{
 "date":   -419,
"name": "GSPC.Close",
"price": 103.95,
"rsi": 55.222,
"ret": 0.0043478 
},
{
 "date":   -415,
"name": "GSPC.Close",
"price": 104.62,
"rsi": 59.769,
"ret": 0.0064454 
},
{
 "date":   -414,
"name": "GSPC.Close",
"price": 105.13,
"rsi": 65.403,
"ret": 0.0048748 
},
{
 "date":   -413,
"name": "GSPC.Close",
"price":  105.2,
"rsi": 68.966,
"ret": 0.00066584 
},
{
 "date":   -412,
"name": "GSPC.Close",
"price": 105.78,
"rsi": 69.431,
"ret": 0.0055133 
},
{
 "date":   -409,
"name": "GSPC.Close",
"price": 105.92,
"rsi": 73.038,
"ret": 0.0013235 
},
{
 "date":   -408,
"name": "GSPC.Close",
"price": 106.14,
"rsi":  73.84,
"ret": 0.002077 
},
{
 "date":   -406,
"name": "GSPC.Close",
"price": 105.97,
"rsi": 75.094,
"ret": -0.0016017 
},
{
 "date":   -405,
"name": "GSPC.Close",
"price":  106.3,
"rsi": 72.213,
"ret": 0.0031141 
},
{
 "date":   -402,
"name": "GSPC.Close",
"price": 106.48,
"rsi": 74.276,
"ret": 0.0016933 
},
{
 "date":   -401,
"name": "GSPC.Close",
"price": 107.26,
"rsi": 75.352,
"ret": 0.0073253 
},
{
 "date":   -400,
"name": "GSPC.Close",
"price": 107.76,
"rsi": 79.374,
"ret": 0.0046616 
},
{
 "date":   -398,
"name": "GSPC.Close",
"price": 108.37,
"rsi": 81.463,
"ret": 0.0056607 
},
{
 "date":   -395,
"name": "GSPC.Close",
"price": 108.12,
"rsi":  83.64,
"ret": -0.0023069 
},
{
 "date":   -394,
"name": "GSPC.Close",
"price": 108.02,
"rsi": 79.519,
"ret": -0.0009249 
},
{
 "date":   -392,
"name": "GSPC.Close",
"price": 107.67,
"rsi": 77.866,
"ret": -0.0032401 
},
{
 "date":   -391,
"name": "GSPC.Close",
"price": 107.93,
"rsi": 72.209,
"ret": 0.0024148 
},
{
 "date":   -388,
"name": "GSPC.Close",
"price": 107.66,
"rsi": 73.736,
"ret": -0.0025016 
},
{
 "date":   -387,
"name": "GSPC.Close",
"price": 107.39,
"rsi": 69.469,
"ret": -0.0025079 
},
{
 "date":   -385,
"name": "GSPC.Close",
"price": 107.32,
"rsi": 65.393,
"ret": -0.00065183 
},
{
 "date":   -384,
"name": "GSPC.Close",
"price": 107.58,
"rsi": 64.339,
"ret": 0.0024227 
},
{
 "date":   -381,
"name": "GSPC.Close",
"price":  107.1,
"rsi": 66.499,
"ret": -0.0044618 
},
{
 "date":   -380,
"name": "GSPC.Close",
"price": 106.66,
"rsi": 59.353,
"ret": -0.0041083 
},
{
 "date":   -378,
"name": "GSPC.Close",
"price": 106.97,
"rsi":  53.66,
"ret": 0.0029064 
},
{
 "date":   -377,
"name": "GSPC.Close",
"price": 106.34,
"rsi": 56.804,
"ret": -0.0058895 
},
{
 "date":   -374,
"name": "GSPC.Close",
"price": 105.21,
"rsi": 49.461,
"ret": -0.010626 
},
{
 "date":   -373,
"name": "GSPC.Close",
"price": 105.04,
"rsi": 39.578,
"ret": -0.0016158 
},
{
 "date":   -371,
"name": "GSPC.Close",
"price": 105.15,
"rsi": 38.337,
"ret": 0.0010472 
},
{
 "date":   -370,
"name": "GSPC.Close",
"price": 104.74,
"rsi": 39.656,
"ret": -0.0038992 
},
{
 "date":   -367,
"name": "GSPC.Close",
"price":  103.8,
"rsi": 36.521,
"ret": -0.0089746 
},
{
 "date":   -366,
"name": "GSPC.Close",
"price": 103.86,
"rsi": 30.557,
"ret": 0.00057803 
},
{
 "date":   -364,
"name": "GSPC.Close",
"price": 103.93,
"rsi": 31.328,
"ret": 0.00067398 
},
{
 "date":   -363,
"name": "GSPC.Close",
"price": 103.99,
"rsi": 32.272,
"ret": 0.00057731 
},
{
 "date":   -360,
"name": "GSPC.Close",
"price": 102.47,
"rsi": 33.122,
"ret": -0.014617 
},
{
 "date":   -359,
"name": "GSPC.Close",
"price": 101.22,
"rsi":  24.68,
"ret": -0.012199 
},
{
 "date":   -358,
"name": "GSPC.Close",
"price":  100.8,
"rsi": 20.135,
"ret": -0.0041494 
},
{
 "date":   -357,
"name": "GSPC.Close",
"price": 101.22,
"rsi": 18.877,
"ret": 0.0041667 
},
{
 "date":   -356,
"name": "GSPC.Close",
"price": 100.93,
"rsi": 23.991,
"ret": -0.002865 
},
{
 "date":   -353,
"name": "GSPC.Close",
"price": 100.44,
"rsi": 22.917,
"ret": -0.0048548 
},
{
 "date":   -352,
"name": "GSPC.Close",
"price": 101.13,
"rsi":  21.19,
"ret": 0.0068698 
},
{
 "date":   -351,
"name": "GSPC.Close",
"price": 101.62,
"rsi": 29.271,
"ret": 0.0048452 
},
{
 "date":   -350,
"name": "GSPC.Close",
"price": 102.18,
"rsi": 34.414,
"ret": 0.0055107 
},
{
 "date":   -349,
"name": "GSPC.Close",
"price": 102.03,
"rsi": 39.801,
"ret": -0.001468 
},
{
 "date":   -346,
"name": "GSPC.Close",
"price": 101.69,
"rsi":  38.88,
"ret": -0.0033324 
},
{
 "date":   -345,
"name": "GSPC.Close",
"price": 101.63,
"rsi":   36.8,
"ret": -0.00059003 
},
{
 "date":   -344,
"name": "GSPC.Close",
"price": 101.98,
"rsi":  36.43,
"ret": 0.0034439 
},
{
 "date":   -343,
"name": "GSPC.Close",
"price": 102.43,
"rsi": 40.209,
"ret": 0.0044126 
},
{
 "date":   -342,
"name": "GSPC.Close",
"price": 102.38,
"rsi": 44.756,
"ret": -0.00048814 
},
{
 "date":   -339,
"name": "GSPC.Close",
"price":  102.4,
"rsi": 44.353,
"ret": 0.00019535 
},
{
 "date":   -338,
"name": "GSPC.Close",
"price": 102.41,
"rsi": 44.568,
"ret": 9.7656e-05 
},
{
 "date":   -337,
"name": "GSPC.Close",
"price": 102.51,
"rsi": 44.683,
"ret": 0.00097647 
},
{
 "date":   -336,
"name": "GSPC.Close",
"price": 102.55,
"rsi": 45.895,
"ret": 0.00039021 
},
{
 "date":   -335,
"name": "GSPC.Close",
"price": 103.01,
"rsi": 46.401,
"ret": 0.0044856 
},
{
 "date":   -332,
"name": "GSPC.Close",
"price": 102.89,
"rsi": 51.961,
"ret": -0.0011649 
},
{
 "date":   -331,
"name": "GSPC.Close",
"price": 102.92,
"rsi":  50.49,
"ret": 0.00029157 
},
{
 "date":   -330,
"name": "GSPC.Close",
"price":  103.2,
"rsi": 50.864,
"ret": 0.0027206 
},
{
 "date":   -329,
"name": "GSPC.Close",
"price": 103.54,
"rsi": 54.338,
"ret": 0.0032946 
},
{
 "date":   -328,
"name": "GSPC.Close",
"price": 103.53,
"rsi": 58.201,
"ret": -9.6581e-05 
},
{
 "date":   -324,
"name": "GSPC.Close",
"price": 103.65,
"rsi": 58.046,
"ret": 0.0011591 
},
{
 "date":   -323,
"name": "GSPC.Close",
"price": 103.63,
"rsi": 59.446,
"ret": -0.00019296 
},
{
 "date":   -322,
"name": "GSPC.Close",
"price": 103.71,
"rsi": 59.092,
"ret": 0.00077198 
},
{
 "date":   -321,
"name": "GSPC.Close",
"price": 103.61,
"rsi": 60.116,
"ret": -0.00096423 
},
{
 "date":   -318,
"name": "GSPC.Close",
"price": 102.44,
"rsi": 58.157,
"ret": -0.011292 
},
{
 "date":   -317,
"name": "GSPC.Close",
"price":  101.4,
"rsi":  41.23,
"ret": -0.010152 
},
{
 "date":   -316,
"name": "GSPC.Close",
"price": 100.65,
"rsi": 32.246,
"ret": -0.0073964 
},
{
 "date":   -315,
"name": "GSPC.Close",
"price":  99.79,
"rsi": 27.579,
"ret": -0.0085445 
},
{
 "date":   -311,
"name": "GSPC.Close",
"price":   98.6,
"rsi": 23.397,
"ret": -0.011925 
},
{
 "date":   -310,
"name": "GSPC.Close",
"price":  97.98,
"rsi": 19.085,
"ret": -0.006288 
},
{
 "date":   -309,
"name": "GSPC.Close",
"price":  98.45,
"rsi": 17.296,
"ret": 0.0047969 
},
{
 "date":   -308,
"name": "GSPC.Close",
"price":  98.14,
"rsi": 23.174,
"ret": -0.0031488 
},
{
 "date":   -307,
"name": "GSPC.Close",
"price":  98.13,
"rsi": 22.061,
"ret": -0.0001019 
},
{
 "date":   -304,
"name": "GSPC.Close",
"price":  98.38,
"rsi": 22.024,
"ret": 0.0025476 
},
{
 "date":   -303,
"name": "GSPC.Close",
"price":  99.32,
"rsi": 25.373,
"ret": 0.0095548 
},
{
 "date":   -302,
"name": "GSPC.Close",
"price":  99.71,
"rsi": 36.428,
"ret": 0.0039267 
},
{
 "date":   -301,
"name": "GSPC.Close",
"price":   98.7,
"rsi": 40.374,
"ret": -0.010129 
},
{
 "date":   -300,
"name": "GSPC.Close",
"price":  98.65,
"rsi": 34.416,
"ret": -0.00050659 
},
{
 "date":   -297,
"name": "GSPC.Close",
"price":  98.99,
"rsi": 34.147,
"ret": 0.0034465 
},
{
 "date":   -296,
"name": "GSPC.Close",
"price":  99.32,
"rsi": 37.708,
"ret": 0.0033337 
},
{
 "date":   -295,
"name": "GSPC.Close",
"price":  99.05,
"rsi": 41.041,
"ret": -0.0027185 
},
{
 "date":   -294,
"name": "GSPC.Close",
"price":  98.39,
"rsi": 39.193,
"ret": -0.0066633 
},
{
 "date":   -293,
"name": "GSPC.Close",
"price":     98,
"rsi": 35.041,
"ret": -0.0039638 
},
{
 "date":   -290,
"name": "GSPC.Close",
"price":  98.25,
"rsi": 32.827,
"ret": 0.002551 
},
{
 "date":   -289,
"name": "GSPC.Close",
"price":  98.49,
"rsi": 35.634,
"ret": 0.0024427 
},
{
 "date":   -288,
"name": "GSPC.Close",
"price":  99.21,
"rsi": 38.299,
"ret": 0.0073104 
},
{
 "date":   -287,
"name": "GSPC.Close",
"price":  99.84,
"rsi":  45.58,
"ret": 0.0063502 
},
{
 "date":   -286,
"name": "GSPC.Close",
"price":  99.63,
"rsi": 51.025,
"ret": -0.0021034 
},
{
 "date":   -283,
"name": "GSPC.Close",
"price":   99.5,
"rsi": 49.256,
"ret": -0.0013048 
},
{
 "date":   -282,
"name": "GSPC.Close",
"price":  99.66,
"rsi": 48.143,
"ret": 0.001608 
},
{
 "date":   -281,
"name": "GSPC.Close",
"price": 100.39,
"rsi": 49.651,
"ret": 0.0073249 
},
{
 "date":   -280,
"name": "GSPC.Close",
"price":  101.1,
"rsi": 55.945,
"ret": 0.0070724 
},
{
 "date":   -279,
"name": "GSPC.Close",
"price": 101.51,
"rsi": 61.046,
"ret": 0.0040554 
},
{
 "date":   -275,
"name": "GSPC.Close",
"price": 101.42,
"rsi": 63.662,
"ret": -0.00088661 
},
{
 "date":   -274,
"name": "GSPC.Close",
"price": 100.78,
"rsi": 62.667,
"ret": -0.0063104 
},
{
 "date":   -273,
"name": "GSPC.Close",
"price": 100.68,
"rsi": 55.968,
"ret": -0.00099226 
},
{
 "date":   -269,
"name": "GSPC.Close",
"price":  99.89,
"rsi": 54.979,
"ret": -0.0078466 
},
{
 "date":   -268,
"name": "GSPC.Close",
"price": 100.14,
"rsi": 47.794,
"ret": 0.0025028 
},
{
 "date":   -267,
"name": "GSPC.Close",
"price": 101.02,
"rsi":  50.02,
"ret": 0.0087877 
},
{
 "date":   -266,
"name": "GSPC.Close",
"price": 101.55,
"rsi": 56.974,
"ret": 0.0052465 
},
{
 "date":   -265,
"name": "GSPC.Close",
"price": 101.65,
"rsi": 60.536,
"ret": 0.00098474 
},
{
 "date":   -262,
"name": "GSPC.Close",
"price": 101.57,
"rsi": 61.189,
"ret": -0.00078701 
},
{
 "date":   -261,
"name": "GSPC.Close",
"price": 101.53,
"rsi": 60.329,
"ret": -0.00039382 
},
{
 "date":   -260,
"name": "GSPC.Close",
"price": 100.63,
"rsi": 59.876,
"ret": -0.0088644 
},
{
 "date":   -259,
"name": "GSPC.Close",
"price": 100.78,
"rsi": 50.659,
"ret": 0.0014906 
},
{
 "date":   -258,
"name": "GSPC.Close",
"price": 101.24,
"rsi": 51.985,
"ret": 0.0045644 
},
{
 "date":   -255,
"name": "GSPC.Close",
"price": 100.56,
"rsi": 55.901,
"ret": -0.0067167 
},
{
 "date":   -254,
"name": "GSPC.Close",
"price": 100.78,
"rsi": 49.477,
"ret": 0.0021877 
},
{
 "date":   -253,
"name": "GSPC.Close",
"price":  100.8,
"rsi": 51.422,
"ret": 0.00019845 
},
{
 "date":   -252,
"name": "GSPC.Close",
"price": 101.27,
"rsi": 51.605,
"ret": 0.0046627 
},
{
 "date":   -251,
"name": "GSPC.Close",
"price": 101.72,
"rsi": 55.804,
"ret": 0.0044436 
},
{
 "date":   -248,
"name": "GSPC.Close",
"price": 102.03,
"rsi": 59.434,
"ret": 0.0030476 
},
{
 "date":   -247,
"name": "GSPC.Close",
"price": 102.79,
"rsi": 61.764,
"ret": 0.0074488 
},
{
 "date":   -246,
"name": "GSPC.Close",
"price": 103.69,
"rsi": 66.798,
"ret": 0.0087557 
},
{
 "date":   -245,
"name": "GSPC.Close",
"price": 103.51,
"rsi": 71.571,
"ret": -0.0017359 
},
{
 "date":   -244,
"name": "GSPC.Close",
"price":    104,
"rsi": 69.422,
"ret": 0.0047338 
},
{
 "date":   -241,
"name": "GSPC.Close",
"price": 104.37,
"rsi": 71.896,
"ret": 0.0035577 
},
{
 "date":   -240,
"name": "GSPC.Close",
"price": 104.86,
"rsi": 73.632,
"ret": 0.0046948 
},
{
 "date":   -239,
"name": "GSPC.Close",
"price": 104.67,
"rsi": 75.766,
"ret": -0.0018119 
},
{
 "date":   -238,
"name": "GSPC.Close",
"price":  105.1,
"rsi": 73.289,
"ret": 0.0041081 
},
{
 "date":   -237,
"name": "GSPC.Close",
"price": 105.05,
"rsi":  75.26,
"ret": -0.00047574 
},
{
 "date":   -234,
"name": "GSPC.Close",
"price": 104.89,
"rsi": 74.571,
"ret": -0.0015231 
},
{
 "date":   -233,
"name": "GSPC.Close",
"price": 105.34,
"rsi":  72.29,
"ret": 0.0042902 
},
{
 "date":   -232,
"name": "GSPC.Close",
"price": 106.16,
"rsi": 74.639,
"ret": 0.0077843 
},
{
 "date":   -231,
"name": "GSPC.Close",
"price": 105.85,
"rsi": 78.257,
"ret": -0.0029201 
},
{
 "date":   -230,
"name": "GSPC.Close",
"price": 105.94,
"rsi": 73.962,
"ret": 0.00085026 
},
{
 "date":   -227,
"name": "GSPC.Close",
"price": 104.97,
"rsi": 74.401,
"ret": -0.0091561 
},
{
 "date":   -226,
"name": "GSPC.Close",
"price": 104.04,
"rsi": 62.216,
"ret": -0.0088597 
},
{
 "date":   -225,
"name": "GSPC.Close",
"price": 104.47,
"rsi": 53.217,
"ret": 0.004133 
},
{
 "date":   -224,
"name": "GSPC.Close",
"price":  104.6,
"rsi":  56.36,
"ret": 0.0012444 
},
{
 "date":   -223,
"name": "GSPC.Close",
"price": 104.59,
"rsi": 57.294,
"ret": -9.5602e-05 
},
{
 "date":   -220,
"name": "GSPC.Close",
"price": 104.36,
"rsi": 57.193,
"ret": -0.0021991 
},
{
 "date":   -219,
"name": "GSPC.Close",
"price": 103.57,
"rsi": 54.791,
"ret": -0.00757 
},
{
 "date":   -218,
"name": "GSPC.Close",
"price": 103.26,
"rsi": 47.423,
"ret": -0.0029931 
},
{
 "date":   -217,
"name": "GSPC.Close",
"price": 103.46,
"rsi": 44.873,
"ret": 0.0019369 
},
{
 "date":   -213,
"name": "GSPC.Close",
"price": 102.94,
"rsi": 46.858,
"ret": -0.0050261 
},
{
 "date":   -212,
"name": "GSPC.Close",
"price": 102.63,
"rsi": 42.566,
"ret": -0.0030115 
},
{
 "date":   -211,
"name": "GSPC.Close",
"price": 102.59,
"rsi": 40.202,
"ret": -0.00038975 
},
{
 "date":   -210,
"name": "GSPC.Close",
"price": 102.76,
"rsi": 39.894,
"ret": 0.0016571 
},
{
 "date":   -209,
"name": "GSPC.Close",
"price": 102.12,
"rsi":  41.93,
"ret": -0.0062281 
},
{
 "date":   -206,
"name": "GSPC.Close",
"price":  101.2,
"rsi": 36.867,
"ret": -0.009009 
},
{
 "date":   -205,
"name": "GSPC.Close",
"price": 100.42,
"rsi": 31.062,
"ret": -0.0077075 
},
{
 "date":   -204,
"name": "GSPC.Close",
"price":  99.05,
"rsi": 27.157,
"ret": -0.013643 
},
{
 "date":   -203,
"name": "GSPC.Close",
"price":  98.26,
"rsi": 21.941,
"ret": -0.0079758 
},
{
 "date":   -202,
"name": "GSPC.Close",
"price":  98.65,
"rsi": 19.602,
"ret": 0.0039691 
},
{
 "date":   -199,
"name": "GSPC.Close",
"price":  98.32,
"rsi": 23.913,
"ret": -0.0033452 
},
{
 "date":   -198,
"name": "GSPC.Close",
"price":  97.95,
"rsi": 22.799,
"ret": -0.0037632 
},
{
 "date":   -197,
"name": "GSPC.Close",
"price":  97.81,
"rsi": 21.585,
"ret": -0.0014293 
},
{
 "date":   -196,
"name": "GSPC.Close",
"price":  97.24,
"rsi": 21.127,
"ret": -0.0058276 
},
{
 "date":   -195,
"name": "GSPC.Close",
"price":  96.67,
"rsi": 19.327,
"ret": -0.0058618 
},
{
 "date":   -192,
"name": "GSPC.Close",
"price":  96.23,
"rsi": 17.702,
"ret": -0.0045516 
},
{
 "date":   -191,
"name": "GSPC.Close",
"price":  97.32,
"rsi": 16.547,
"ret": 0.011327 
},
{
 "date":   -190,
"name": "GSPC.Close",
"price":  97.01,
"rsi": 28.928,
"ret": -0.0031854 
},
{
 "date":   -189,
"name": "GSPC.Close",
"price":  97.25,
"rsi": 27.671,
"ret": 0.002474 
},
{
 "date":   -188,
"name": "GSPC.Close",
"price":  97.33,
"rsi":   30.2,
"ret": 0.00082262 
},
{
 "date":   -185,
"name": "GSPC.Close",
"price":  97.71,
"rsi": 31.066,
"ret": 0.0039042 
},
{
 "date":   -184,
"name": "GSPC.Close",
"price":  98.08,
"rsi": 35.177,
"ret": 0.0037867 
},
{
 "date":   -183,
"name": "GSPC.Close",
"price":  98.94,
"rsi": 38.992,
"ret": 0.0087684 
},
{
 "date":   -182,
"name": "GSPC.Close",
"price":  99.61,
"rsi": 46.826,
"ret": 0.0067718 
},
{
 "date":   -178,
"name": "GSPC.Close",
"price":  99.03,
"rsi": 51.998,
"ret": -0.0058227 
},
{
 "date":   -177,
"name": "GSPC.Close",
"price":  97.63,
"rsi": 47.675,
"ret": -0.014137 
},
{
 "date":   -176,
"name": "GSPC.Close",
"price":  96.88,
"rsi": 39.203,
"ret": -0.0076821 
},
{
 "date":   -175,
"name": "GSPC.Close",
"price":  95.38,
"rsi": 35.558,
"ret": -0.015483 
},
{
 "date":   -174,
"name": "GSPC.Close",
"price":  95.77,
"rsi": 29.625,
"ret": 0.0040889 
},
{
 "date":   -171,
"name": "GSPC.Close",
"price":  94.55,
"rsi": 32.766,
"ret": -0.012739 
},
{
 "date":   -170,
"name": "GSPC.Close",
"price":  94.24,
"rsi": 28.483,
"ret": -0.0032787 
},
{
 "date":   -169,
"name": "GSPC.Close",
"price":  95.18,
"rsi": 27.499,
"ret": 0.0099745 
},
{
 "date":   -168,
"name": "GSPC.Close",
"price":  95.76,
"rsi": 34.847,
"ret": 0.0060937 
},
{
 "date":   -167,
"name": "GSPC.Close",
"price":  94.95,
"rsi": 38.957,
"ret": -0.0084586 
},
{
 "date":   -163,
"name": "GSPC.Close",
"price":  93.52,
"rsi": 35.581,
"ret": -0.015061 
},
{
 "date":   -162,
"name": "GSPC.Close",
"price":  93.12,
"rsi": 30.548,
"ret": -0.0042772 
},
{
 "date":   -161,
"name": "GSPC.Close",
"price":   92.8,
"rsi": 29.299,
"ret": -0.0034364 
},
{
 "date":   -160,
"name": "GSPC.Close",
"price":  92.06,
"rsi": 28.303,
"ret": -0.0079741 
},
{
 "date":   -157,
"name": "GSPC.Close",
"price":  90.21,
"rsi": 26.092,
"ret": -0.020096 
},
{
 "date":   -156,
"name": "GSPC.Close",
"price":  89.48,
"rsi": 21.559,
"ret": -0.0080922 
},
{
 "date":   -155,
"name": "GSPC.Close",
"price":  89.93,
"rsi": 20.077,
"ret": 0.0050291 
},
{
 "date":   -154,
"name": "GSPC.Close",
"price":  91.83,
"rsi": 23.566,
"ret": 0.021128 
},
{
 "date":   -153,
"name": "GSPC.Close",
"price":  93.47,
"rsi": 36.223,
"ret": 0.017859 
},
{
 "date":   -150,
"name": "GSPC.Close",
"price":  92.99,
"rsi": 44.731,
"ret": -0.0051353 
},
{
 "date":   -149,
"name": "GSPC.Close",
"price":  93.41,
"rsi": 42.926,
"ret": 0.0045166 
},
{
 "date":   -148,
"name": "GSPC.Close",
"price":  93.92,
"rsi": 45.017,
"ret": 0.0054598 
},
{
 "date":   -147,
"name": "GSPC.Close",
"price":  93.99,
"rsi":  47.53,
"ret": 0.00074532 
},
{
 "date":   -146,
"name": "GSPC.Close",
"price":  93.94,
"rsi": 47.882,
"ret": -0.00053197 
},
{
 "date":   -143,
"name": "GSPC.Close",
"price":  93.36,
"rsi": 47.636,
"ret": -0.0061742 
},
{
 "date":   -142,
"name": "GSPC.Close",
"price":  92.63,
"rsi": 44.764,
"ret": -0.0078192 
},
{
 "date":   -141,
"name": "GSPC.Close",
"price":   92.7,
"rsi": 41.382,
"ret": 0.00075569 
},
{
 "date":   -140,
"name": "GSPC.Close",
"price":  93.34,
"rsi": 41.836,
"ret": 0.006904 
},
{
 "date":   -139,
"name": "GSPC.Close",
"price":     94,
"rsi": 45.955,
"ret": 0.0070709 
},
{
 "date":   -136,
"name": "GSPC.Close",
"price":  94.57,
"rsi": 49.896,
"ret": 0.0060638 
},
{
 "date":   -135,
"name": "GSPC.Close",
"price":  95.07,
"rsi": 53.079,
"ret": 0.0052871 
},
{
 "date":   -134,
"name": "GSPC.Close",
"price":  95.07,
"rsi": 55.734,
"ret":      0 
},
{
 "date":   -133,
"name": "GSPC.Close",
"price":  95.35,
"rsi": 55.734,
"ret": 0.0029452 
},
{
 "date":   -132,
"name": "GSPC.Close",
"price":  95.92,
"rsi": 57.304,
"ret": 0.005978 
},
{
 "date":   -129,
"name": "GSPC.Close",
"price":  94.93,
"rsi": 60.384,
"ret": -0.010321 
},
{
 "date":   -128,
"name": "GSPC.Close",
"price":   94.3,
"rsi": 53.206,
"ret": -0.0066365 
},
{
 "date":   -127,
"name": "GSPC.Close",
"price":  94.49,
"rsi": 49.198,
"ret": 0.0020148 
},
{
 "date":   -126,
"name": "GSPC.Close",
"price":  94.89,
"rsi": 50.411,
"ret": 0.0042333 
},
{
 "date":   -125,
"name": "GSPC.Close",
"price":  95.51,
"rsi": 52.958,
"ret": 0.0065339 
},
{
 "date":   -121,
"name": "GSPC.Close",
"price":  95.54,
"rsi": 56.673,
"ret": 0.0003141 
},
{
 "date":   -120,
"name": "GSPC.Close",
"price":  94.98,
"rsi":  56.85,
"ret": -0.0058614 
},
{
 "date":   -119,
"name": "GSPC.Close",
"price":   94.2,
"rsi": 52.523,
"ret": -0.0082123 
},
{
 "date":   -118,
"name": "GSPC.Close",
"price":  93.64,
"rsi": 47.141,
"ret": -0.0059448 
},
{
 "date":   -115,
"name": "GSPC.Close",
"price":   92.7,
"rsi": 43.681,
"ret": -0.010038 
},
{
 "date":   -114,
"name": "GSPC.Close",
"price":  93.38,
"rsi": 38.563,
"ret": 0.0073355 
},
{
 "date":   -113,
"name": "GSPC.Close",
"price":  94.95,
"rsi": 43.702,
"ret": 0.016813 
},
{
 "date":   -112,
"name": "GSPC.Close",
"price":  94.22,
"rsi": 53.394,
"ret": -0.0076883 
},
{
 "date":   -111,
"name": "GSPC.Close",
"price":  94.13,
"rsi": 49.156,
"ret": -0.00095521 
},
{
 "date":   -108,
"name": "GSPC.Close",
"price":  94.87,
"rsi": 48.644,
"ret": 0.0078615 
},
{
 "date":   -107,
"name": "GSPC.Close",
"price":  94.95,
"rsi": 52.985,
"ret": 0.00084326 
},
{
 "date":   -106,
"name": "GSPC.Close",
"price":  94.76,
"rsi": 53.443,
"ret": -0.0020011 
},
{
 "date":   -105,
"name": "GSPC.Close",
"price":   94.9,
"rsi": 52.143,
"ret": 0.0014774 
},
{
 "date":   -104,
"name": "GSPC.Close",
"price":  95.19,
"rsi": 53.049,
"ret": 0.0030558 
},
{
 "date":   -101,
"name": "GSPC.Close",
"price":  95.63,
"rsi": 54.952,
"ret": 0.0046223 
},
{
 "date":   -100,
"name": "GSPC.Close",
"price":  95.63,
"rsi": 57.749,
"ret":      0 
},
{
 "date":    -99,
"name": "GSPC.Close",
"price":   95.5,
"rsi": 57.749,
"ret": -0.0013594 
},
{
 "date":    -98,
"name": "GSPC.Close",
"price":  94.77,
"rsi": 56.546,
"ret": -0.007644 
},
{
 "date":    -97,
"name": "GSPC.Close",
"price":  94.16,
"rsi": 50.218,
"ret": -0.0064366 
},
{
 "date":    -94,
"name": "GSPC.Close",
"price":  93.41,
"rsi": 45.624,
"ret": -0.0079652 
},
{
 "date":    -93,
"name": "GSPC.Close",
"price":  93.12,
"rsi": 40.695,
"ret": -0.0031046 
},
{
 "date":    -92,
"name": "GSPC.Close",
"price":  92.52,
"rsi": 38.943,
"ret": -0.0064433 
},
{
 "date":    -91,
"name": "GSPC.Close",
"price":  93.24,
"rsi": 35.534,
"ret": 0.0077821 
},
{
 "date":    -90,
"name": "GSPC.Close",
"price":  93.19,
"rsi": 42.085,
"ret": -0.00053625 
},
{
 "date":    -87,
"name": "GSPC.Close",
"price":  93.38,
"rsi": 41.768,
"ret": 0.0020388 
},
{
 "date":    -86,
"name": "GSPC.Close",
"price":  93.09,
"rsi": 43.511,
"ret": -0.0031056 
},
{
 "date":    -85,
"name": "GSPC.Close",
"price":  92.67,
"rsi":  41.47,
"ret": -0.0045118 
},
{
 "date":    -84,
"name": "GSPC.Close",
"price":  93.03,
"rsi": 38.643,
"ret": 0.0038848 
},
{
 "date":    -83,
"name": "GSPC.Close",
"price":  93.56,
"rsi": 42.276,
"ret": 0.0056971 
},
{
 "date":    -80,
"name": "GSPC.Close",
"price":  94.55,
"rsi": 47.229,
"ret": 0.010581 
},
{
 "date":    -79,
"name": "GSPC.Close",
"price":   95.7,
"rsi": 54.998,
"ret": 0.012163 
},
{
 "date":    -78,
"name": "GSPC.Close",
"price":  95.72,
"rsi": 61.996,
"ret": 0.00020899 
},
{
 "date":    -77,
"name": "GSPC.Close",
"price":  96.37,
"rsi": 62.107,
"ret": 0.0067906 
},
{
 "date":    -76,
"name": "GSPC.Close",
"price":  96.26,
"rsi": 65.603,
"ret": -0.0011414 
},
{
 "date":    -73,
"name": "GSPC.Close",
"price":  96.46,
"rsi": 64.518,
"ret": 0.0020777 
},
{
 "date":    -72,
"name": "GSPC.Close",
"price":   97.2,
"rsi": 65.631,
"ret": 0.0076716 
},
{
 "date":    -71,
"name": "GSPC.Close",
"price":  97.83,
"rsi": 69.449,
"ret": 0.0064815 
},
{
 "date":    -70,
"name": "GSPC.Close",
"price":  97.46,
"rsi": 72.273,
"ret": -0.0037821 
},
{
 "date":    -69,
"name": "GSPC.Close",
"price":  98.12,
"rsi": 68.281,
"ret": 0.006772 
},
{
 "date":    -66,
"name": "GSPC.Close",
"price":  97.97,
"rsi": 71.324,
"ret": -0.0015287 
},
{
 "date":    -65,
"name": "GSPC.Close",
"price":  97.66,
"rsi": 69.688,
"ret": -0.0031642 
},
{
 "date":    -64,
"name": "GSPC.Close",
"price":  96.81,
"rsi": 66.302,
"ret": -0.0087037 
},
{
 "date":    -63,
"name": "GSPC.Close",
"price":  96.93,
"rsi": 57.985,
"ret": 0.0012395 
},
{
 "date":    -62,
"name": "GSPC.Close",
"price":  97.12,
"rsi": 58.771,
"ret": 0.0019602 
},
{
 "date":    -59,
"name": "GSPC.Close",
"price":  97.15,
"rsi": 60.046,
"ret": 0.0003089 
},
{
 "date":    -58,
"name": "GSPC.Close",
"price":  97.21,
"rsi": 60.255,
"ret": 0.0006176 
},
{
 "date":    -57,
"name": "GSPC.Close",
"price":  97.64,
"rsi": 60.698,
"ret": 0.0044234 
},
{
 "date":    -56,
"name": "GSPC.Close",
"price":  97.67,
"rsi":  63.81,
"ret": 0.00030725 
},
{
 "date":    -55,
"name": "GSPC.Close",
"price":  98.26,
"rsi": 64.024,
"ret": 0.0060407 
},
{
 "date":    -52,
"name": "GSPC.Close",
"price":  98.33,
"rsi": 68.029,
"ret": 0.0007124 
},
{
 "date":    -51,
"name": "GSPC.Close",
"price":  98.07,
"rsi": 68.477,
"ret": -0.0026442 
},
{
 "date":    -50,
"name": "GSPC.Close",
"price":  97.89,
"rsi":  64.84,
"ret": -0.0018354 
},
{
 "date":    -49,
"name": "GSPC.Close",
"price":  97.42,
"rsi":  62.37,
"ret": -0.0048013 
},
{
 "date":    -48,
"name": "GSPC.Close",
"price":  97.07,
"rsi": 56.336,
"ret": -0.0035927 
},
{
 "date":    -45,
"name": "GSPC.Close",
"price":  96.41,
"rsi":  52.28,
"ret": -0.0067992 
},
{
 "date":    -44,
"name": "GSPC.Close",
"price":  96.39,
"rsi": 45.611,
"ret": -0.00020745 
},
{
 "date":    -43,
"name": "GSPC.Close",
"price":   95.9,
"rsi": 45.421,
"ret": -0.0050835 
},
{
 "date":    -42,
"name": "GSPC.Close",
"price":  94.91,
"rsi": 40.943,
"ret": -0.010323 
},
{
 "date":    -41,
"name": "GSPC.Close",
"price":  94.32,
"rsi": 33.711,
"ret": -0.0062164 
},
{
 "date":    -38,
"name": "GSPC.Close",
"price":  93.24,
"rsi": 30.278,
"ret": -0.01145 
},
{
 "date":    -37,
"name": "GSPC.Close",
"price":  92.94,
"rsi": 25.217,
"ret": -0.0032175 
},
{
 "date":    -36,
"name": "GSPC.Close",
"price":  93.27,
"rsi": 24.016,
"ret": 0.0035507 
},
{
 "date":    -34,
"name": "GSPC.Close",
"price":  93.81,
"rsi": 28.074,
"ret": 0.0057896 
},
{
 "date":    -31,
"name": "GSPC.Close",
"price":  93.22,
"rsi": 34.261,
"ret": -0.0062893 
},
{
 "date":    -30,
"name": "GSPC.Close",
"price":  92.65,
"rsi": 31.112,
"ret": -0.0061146 
},
{
 "date":    -29,
"name": "GSPC.Close",
"price":  91.65,
"rsi": 28.396,
"ret": -0.010793 
},
{
 "date":    -28,
"name": "GSPC.Close",
"price":  91.95,
"rsi": 24.377,
"ret": 0.0032733 
},
{
 "date":    -27,
"name": "GSPC.Close",
"price":  91.73,
"rsi": 27.684,
"ret": -0.0023926 
},
{
 "date":    -24,
"name": "GSPC.Close",
"price":  90.84,
"rsi":  26.76,
"ret": -0.0097024 
},
{
 "date":    -23,
"name": "GSPC.Close",
"price":  90.55,
"rsi": 23.362,
"ret": -0.0031924 
},
{
 "date":    -22,
"name": "GSPC.Close",
"price":  90.48,
"rsi": 22.365,
"ret": -0.00077305 
},
{
 "date":    -21,
"name": "GSPC.Close",
"price":  90.52,
"rsi":  22.12,
"ret": 0.00044209 
},
{
 "date":    -20,
"name": "GSPC.Close",
"price":  90.81,
"rsi": 22.642,
"ret": 0.0032037 
},
{
 "date":    -17,
"name": "GSPC.Close",
"price":  90.54,
"rsi":  26.49,
"ret": -0.0029732 
},
{
 "date":    -16,
"name": "GSPC.Close",
"price":  89.72,
"rsi": 25.231,
"ret": -0.0090568 
},
{
 "date":    -15,
"name": "GSPC.Close",
"price":   89.2,
"rsi": 21.839,
"ret": -0.0057958 
},
{
 "date":    -14,
"name": "GSPC.Close",
"price":  90.61,
"rsi": 20.002,
"ret": 0.015807 
},
{
 "date":    -13,
"name": "GSPC.Close",
"price":  91.38,
"rsi": 35.775,
"ret": 0.008498 
},
{
 "date":    -10,
"name": "GSPC.Close",
"price":  90.58,
"rsi": 42.449,
"ret": -0.0087547 
},
{
 "date":     -9,
"name": "GSPC.Close",
"price":  90.23,
"rsi": 38.028,
"ret": -0.003864 
},
{
 "date":     -8,
"name": "GSPC.Close",
"price":  91.18,
"rsi": 36.249,
"ret": 0.010529 
},
{
 "date":     -6,
"name": "GSPC.Close",
"price":  91.89,
"rsi": 43.917,
"ret": 0.0077868 
},
{
 "date":     -3,
"name": "GSPC.Close",
"price":  91.25,
"rsi": 48.868,
"ret": -0.0069648 
},
{
 "date":     -2,
"name": "GSPC.Close",
"price":   91.6,
"rsi": 45.011,
"ret": 0.0038356 
},
{
 "date":     -1,
"name": "GSPC.Close",
"price":  92.06,
"rsi": 47.453,
"ret": 0.0050218 
},
{
 "date":      1,
"name": "GSPC.Close",
"price":     93,
"rsi": 50.561,
"ret": 0.010211 
},
{
 "date":      4,
"name": "GSPC.Close",
"price":  93.46,
"rsi": 56.255,
"ret": 0.0049462 
},
{
 "date":      5,
"name": "GSPC.Close",
"price":  92.82,
"rsi": 58.759,
"ret": -0.0068478 
},
{
 "date":      6,
"name": "GSPC.Close",
"price":  92.63,
"rsi": 54.119,
"ret": -0.002047 
},
{
 "date":      7,
"name": "GSPC.Close",
"price":  92.68,
"rsi": 52.786,
"ret": 0.00053978 
},
{
 "date":      8,
"name": "GSPC.Close",
"price":   92.4,
"rsi": 53.113,
"ret": -0.0030211 
},
{
 "date":     11,
"name": "GSPC.Close",
"price":   91.7,
"rsi": 50.982,
"ret": -0.0075758 
},
{
 "date":     12,
"name": "GSPC.Close",
"price":  91.92,
"rsi": 46.012,
"ret": 0.0023991 
},
{
 "date":     13,
"name": "GSPC.Close",
"price":  91.65,
"rsi": 47.737,
"ret": -0.0029373 
},
{
 "date":     14,
"name": "GSPC.Close",
"price":  91.68,
"rsi": 45.803,
"ret": 0.00032733 
},
{
 "date":     15,
"name": "GSPC.Close",
"price":  90.92,
"rsi": 46.064,
"ret": -0.0082897 
},
{
 "date":     18,
"name": "GSPC.Close",
"price":  89.65,
"rsi": 40.708,
"ret": -0.013968 
},
{
 "date":     19,
"name": "GSPC.Close",
"price":  89.83,
"rsi": 33.663,
"ret": 0.0020078 
},
{
 "date":     20,
"name": "GSPC.Close",
"price":  89.95,
"rsi":  35.37,
"ret": 0.0013359 
},
{
 "date":     21,
"name": "GSPC.Close",
"price":  90.04,
"rsi": 36.542,
"ret": 0.0010006 
},
{
 "date":     22,
"name": "GSPC.Close",
"price":  89.37,
"rsi": 37.459,
"ret": -0.0074411 
},
{
 "date":     25,
"name": "GSPC.Close",
"price":  88.17,
"rsi": 33.572,
"ret": -0.013427 
},
{
 "date":     26,
"name": "GSPC.Close",
"price":  87.62,
"rsi": 27.973,
"ret": -0.0062379 
},
{
 "date":     27,
"name": "GSPC.Close",
"price":  86.79,
"rsi": 25.846,
"ret": -0.0094727 
},
{
 "date":     28,
"name": "GSPC.Close",
"price":  85.69,
"rsi": 23.003,
"ret": -0.012674 
},
{
 "date":     29,
"name": "GSPC.Close",
"price":  85.02,
"rsi": 19.882,
"ret": -0.0078189 
},
{
 "date":     32,
"name": "GSPC.Close",
"price":  85.75,
"rsi": 18.257,
"ret": 0.0085862 
},
{
 "date":     33,
"name": "GSPC.Close",
"price":  86.77,
"rsi":  25.41,
"ret": 0.011895 
},
{
 "date":     34,
"name": "GSPC.Close",
"price":  86.24,
"rsi": 34.089,
"ret": -0.0061081 
},
{
 "date":     35,
"name": "GSPC.Close",
"price":   85.9,
"rsi": 32.005,
"ret": -0.0039425 
},
{
 "date":     36,
"name": "GSPC.Close",
"price":  86.33,
"rsi": 30.708,
"ret": 0.0050058 
},
{
 "date":     39,
"name": "GSPC.Close",
"price":  87.01,
"rsi": 34.333,
"ret": 0.0078768 
},
{
 "date":     40,
"name": "GSPC.Close",
"price":   86.1,
"rsi": 39.703,
"ret": -0.010459 
},
{
 "date":     41,
"name": "GSPC.Close",
"price":  86.94,
"rsi": 35.517,
"ret": 0.0097561 
},
{
 "date":     42,
"name": "GSPC.Close",
"price":  86.73,
"rsi": 41.635,
"ret": -0.0024155 
},
{
 "date":     43,
"name": "GSPC.Close",
"price":  86.54,
"rsi": 40.598,
"ret": -0.0021907 
},
{
 "date":     46,
"name": "GSPC.Close",
"price":  86.47,
"rsi": 39.636,
"ret": -0.00080887 
},
{
 "date":     47,
"name": "GSPC.Close",
"price":  86.37,
"rsi": 39.267,
"ret": -0.0011565 
},
{
 "date":     48,
"name": "GSPC.Close",
"price":  87.44,
"rsi": 38.712,
"ret": 0.012389 
},
{
 "date":     49,
"name": "GSPC.Close",
"price":  87.76,
"rsi": 47.291,
"ret": 0.0036597 
},
{
 "date":     50,
"name": "GSPC.Close",
"price":  88.03,
"rsi": 49.565,
"ret": 0.0030766 
},
{
 "date":     54,
"name": "GSPC.Close",
"price":  87.99,
"rsi": 51.468,
"ret": -0.00045439 
},
{
 "date":     55,
"name": "GSPC.Close",
"price":  89.35,
"rsi":  51.16,
"ret": 0.015456 
},
{
 "date":     56,
"name": "GSPC.Close",
"price":   88.9,
"rsi": 59.935,
"ret": -0.0050364 
},
{
 "date":     57,
"name": "GSPC.Close",
"price":   89.5,
"rsi": 56.329,
"ret": 0.0067492 
},
{
 "date":     60,
"name": "GSPC.Close",
"price":  89.71,
"rsi": 59.802,
"ret": 0.0023464 
},
{
 "date":     61,
"name": "GSPC.Close",
"price":  90.23,
"rsi": 60.972,
"ret": 0.0057965 
},
{
 "date":     62,
"name": "GSPC.Close",
"price":  90.04,
"rsi": 63.783,
"ret": -0.0021057 
},
{
 "date":     63,
"name": "GSPC.Close",
"price":     90,
"rsi": 62.025,
"ret": -0.00044425 
},
{
 "date":     64,
"name": "GSPC.Close",
"price":  89.44,
"rsi":  61.64,
"ret": -0.0062222 
},
{
 "date":     67,
"name": "GSPC.Close",
"price":  88.51,
"rsi": 56.363,
"ret": -0.010398 
},
{
 "date":     68,
"name": "GSPC.Close",
"price":  88.75,
"rsi":  48.88,
"ret": 0.0027116 
},
{
 "date":     69,
"name": "GSPC.Close",
"price":  88.69,
"rsi": 50.699,
"ret": -0.00067606 
},
{
 "date":     70,
"name": "GSPC.Close",
"price":  88.33,
"rsi": 50.218,
"ret": -0.0040591 
},
{
 "date":     71,
"name": "GSPC.Close",
"price":  87.86,
"rsi": 47.316,
"ret": -0.005321 
},
{
 "date":     74,
"name": "GSPC.Close",
"price":  86.91,
"rsi": 43.761,
"ret": -0.010813 
},
{
 "date":     75,
"name": "GSPC.Close",
"price":  87.29,
"rsi":  37.61,
"ret": 0.0043723 
},
{
 "date":     76,
"name": "GSPC.Close",
"price":  87.54,
"rsi": 41.172,
"ret": 0.002864 
},
{
 "date":     77,
"name": "GSPC.Close",
"price":  87.42,
"rsi": 43.459,
"ret": -0.0013708 
},
{
 "date":     78,
"name": "GSPC.Close",
"price":  87.06,
"rsi": 42.603,
"ret": -0.0041181 
},
{
 "date":     81,
"name": "GSPC.Close",
"price":  86.99,
"rsi": 40.054,
"ret": -0.00080404 
},
{
 "date":     82,
"name": "GSPC.Close",
"price":  87.98,
"rsi": 39.558,
"ret": 0.011381 
},
{
 "date":     83,
"name": "GSPC.Close",
"price":  89.77,
"rsi": 49.144,
"ret": 0.020346 
},
{
 "date":     84,
"name": "GSPC.Close",
"price":  89.92,
"rsi": 61.143,
"ret": 0.0016709 
},
{
 "date":     88,
"name": "GSPC.Close",
"price":  89.63,
"rsi": 61.953,
"ret": -0.0032251 
},
{
 "date":     89,
"name": "GSPC.Close",
"price":  89.63,
"rsi": 59.376,
"ret":      0 
},
{
 "date":     90,
"name": "GSPC.Close",
"price":  90.07,
"rsi": 59.376,
"ret": 0.0049091 
},
{
 "date":     91,
"name": "GSPC.Close",
"price":  89.79,
"rsi": 62.147,
"ret": -0.0031087 
},
{
 "date":     92,
"name": "GSPC.Close",
"price":  89.39,
"rsi": 59.371,
"ret": -0.0044548 
},
{
 "date":     95,
"name": "GSPC.Close",
"price":  88.76,
"rsi": 55.554,
"ret": -0.0070478 
},
{
 "date":     96,
"name": "GSPC.Close",
"price":  88.52,
"rsi": 50.092,
"ret": -0.0027039 
},
{
 "date":     97,
"name": "GSPC.Close",
"price":  88.49,
"rsi":  48.15,
"ret": -0.00033891 
},
{
 "date":     98,
"name": "GSPC.Close",
"price":  88.53,
"rsi":   47.9,
"ret": 0.00045203 
},
{
 "date":     99,
"name": "GSPC.Close",
"price":  88.24,
"rsi": 48.285,
"ret": -0.0032757 
},
{
 "date":    102,
"name": "GSPC.Close",
"price":  87.64,
"rsi": 45.648,
"ret": -0.0067996 
},
{
 "date":    103,
"name": "GSPC.Close",
"price":  86.89,
"rsi": 40.695,
"ret": -0.0085577 
},
{
 "date":    104,
"name": "GSPC.Close",
"price":  86.73,
"rsi": 35.508,
"ret": -0.0018414 
},
{
 "date":    105,
"name": "GSPC.Close",
"price":  85.88,
"rsi": 34.498,
"ret": -0.0098005 
},
{
 "date":    106,
"name": "GSPC.Close",
"price":  85.67,
"rsi": 29.669,
"ret": -0.0024453 
},
{
 "date":    109,
"name": "GSPC.Close",
"price":  85.83,
"rsi": 28.604,
"ret": 0.0018676 
},
{
 "date":    110,
"name": "GSPC.Close",
"price":  85.38,
"rsi": 30.647,
"ret": -0.0052429 
},
{
 "date":    111,
"name": "GSPC.Close",
"price":  84.27,
"rsi": 28.203,
"ret": -0.013001 
},
{
 "date":    112,
"name": "GSPC.Close",
"price":  83.04,
"rsi": 23.272,
"ret": -0.014596 
},
{
 "date":    113,
"name": "GSPC.Close",
"price":  82.77,
"rsi": 19.255,
"ret": -0.0032514 
},
{
 "date":    116,
"name": "GSPC.Close",
"price":  81.46,
"rsi":   18.5,
"ret": -0.015827 
},
{
 "date":    117,
"name": "GSPC.Close",
"price":  80.27,
"rsi": 15.354,
"ret": -0.014608 
},
{
 "date":    118,
"name": "GSPC.Close",
"price":  81.81,
"rsi": 13.164,
"ret": 0.019185 
},
{
 "date":    119,
"name": "GSPC.Close",
"price":  81.52,
"rsi": 27.562,
"ret": -0.0035448 
},
{
 "date":    120,
"name": "GSPC.Close",
"price":  81.44,
"rsi": 26.665,
"ret": -0.00098135 
},
{
 "date":    123,
"name": "GSPC.Close",
"price":  79.37,
"rsi":  26.41,
"ret": -0.025417 
},
{
 "date":    124,
"name": "GSPC.Close",
"price":   78.6,
"rsi": 20.849,
"ret": -0.0097014 
},
{
 "date":    125,
"name": "GSPC.Close",
"price":  79.47,
"rsi": 19.227,
"ret": 0.011069 
},
{
 "date":    126,
"name": "GSPC.Close",
"price":  79.83,
"rsi": 26.212,
"ret": 0.00453 
},
{
 "date":    127,
"name": "GSPC.Close",
"price":  79.44,
"rsi": 28.949,
"ret": -0.0048854 
},
{
 "date":    130,
"name": "GSPC.Close",
"price":   78.6,
"rsi": 27.748,
"ret": -0.010574 
},
{
 "date":    131,
"name": "GSPC.Close",
"price":  77.85,
"rsi": 25.312,
"ret": -0.009542 
},
{
 "date":    132,
"name": "GSPC.Close",
"price":  76.53,
"rsi": 23.342,
"ret": -0.016956 
},
{
 "date":    133,
"name": "GSPC.Close",
"price":  75.44,
"rsi": 20.341,
"ret": -0.014243 
},
{
 "date":    134,
"name": "GSPC.Close",
"price":   76.9,
"rsi": 18.254,
"ret": 0.019353 
},
{
 "date":    137,
"name": "GSPC.Close",
"price":  76.96,
"rsi": 28.793,
"ret": 0.00078023 
},
{
 "date":    138,
"name": "GSPC.Close",
"price":  75.46,
"rsi": 29.197,
"ret": -0.019491 
},
{
 "date":    139,
"name": "GSPC.Close",
"price":  73.52,
"rsi": 25.328,
"ret": -0.025709 
},
{
 "date":    140,
"name": "GSPC.Close",
"price":  72.16,
"rsi": 21.382,
"ret": -0.018498 
},
{
 "date":    141,
"name": "GSPC.Close",
"price":  72.25,
"rsi": 19.132,
"ret": 0.0012472 
},
{
 "date":    144,
"name": "GSPC.Close",
"price":  70.25,
"rsi": 19.734,
"ret": -0.027682 
},
{
 "date":    145,
"name": "GSPC.Close",
"price":  69.29,
"rsi": 16.749,
"ret": -0.013665 
},
{
 "date":    146,
"name": "GSPC.Close",
"price":  72.77,
"rsi": 15.535,
"ret": 0.050224 
},
{
 "date":    147,
"name": "GSPC.Close",
"price":  74.61,
"rsi": 34.168,
"ret": 0.025285 
},
{
 "date":    148,
"name": "GSPC.Close",
"price":  76.55,
"rsi": 41.514,
"ret": 0.026002 
},
{
 "date":    151,
"name": "GSPC.Close",
"price":  77.84,
"rsi": 48.092,
"ret": 0.016852 
},
{
 "date":    152,
"name": "GSPC.Close",
"price":  77.84,
"rsi":  51.96,
"ret":      0 
},
{
 "date":    153,
"name": "GSPC.Close",
"price":  78.52,
"rsi":  51.96,
"ret": 0.0087359 
},
{
 "date":    154,
"name": "GSPC.Close",
"price":  77.36,
"rsi": 54.054,
"ret": -0.014773 
},
{
 "date":    155,
"name": "GSPC.Close",
"price":  76.17,
"rsi": 50.047,
"ret": -0.015383 
},
{
 "date":    158,
"name": "GSPC.Close",
"price":  76.29,
"rsi": 46.259,
"ret": 0.0015754 
},
{
 "date":    159,
"name": "GSPC.Close",
"price":  76.25,
"rsi": 46.697,
"ret": -0.00052432 
},
{
 "date":    160,
"name": "GSPC.Close",
"price":  75.48,
"rsi": 46.561,
"ret": -0.010098 
},
{
 "date":    161,
"name": "GSPC.Close",
"price":  74.45,
"rsi": 43.905,
"ret": -0.013646 
},
{
 "date":    162,
"name": "GSPC.Close",
"price":  73.88,
"rsi": 40.571,
"ret": -0.0076561 
},
{
 "date":    165,
"name": "GSPC.Close",
"price":  74.58,
"rsi": 38.814,
"ret": 0.0094748 
},
{
 "date":    166,
"name": "GSPC.Close",
"price":  76.15,
"rsi": 42.128,
"ret": 0.021051 
},
{
 "date":    167,
"name": "GSPC.Close",
"price":     76,
"rsi": 48.823,
"ret": -0.0019698 
},
{
 "date":    168,
"name": "GSPC.Close",
"price":  76.51,
"rsi": 48.249,
"ret": 0.0067105 
},
{
 "date":    169,
"name": "GSPC.Close",
"price":  77.05,
"rsi": 50.385,
"ret": 0.0070579 
},
{
 "date":    172,
"name": "GSPC.Close",
"price":  76.64,
"rsi": 52.616,
"ret": -0.0053212 
},
{
 "date":    173,
"name": "GSPC.Close",
"price":  74.76,
"rsi":  50.75,
"ret": -0.02453 
},
{
 "date":    174,
"name": "GSPC.Close",
"price":  73.97,
"rsi": 43.187,
"ret": -0.010567 
},
{
 "date":    175,
"name": "GSPC.Close",
"price":  74.02,
"rsi": 40.459,
"ret": 0.00067595 
},
{
 "date":    176,
"name": "GSPC.Close",
"price":  73.47,
"rsi": 40.714,
"ret": -0.0074304 
},
{
 "date":    179,
"name": "GSPC.Close",
"price":  72.89,
"rsi": 38.746,
"ret": -0.0078944 
},
{
 "date":    180,
"name": "GSPC.Close",
"price":  72.72,
"rsi":  36.73,
"ret": -0.0023323 
},
{
 "date":    181,
"name": "GSPC.Close",
"price":  72.94,
"rsi": 36.136,
"ret": 0.0030253 
},
{
 "date":    182,
"name": "GSPC.Close",
"price":  72.92,
"rsi": 37.543,
"ret": -0.0002742 
},
{
 "date":    186,
"name": "GSPC.Close",
"price":  71.78,
"rsi": 37.462,
"ret": -0.015634 
},
{
 "date":    187,
"name": "GSPC.Close",
"price":  71.23,
"rsi": 33.091,
"ret": -0.0076623 
},
{
 "date":    188,
"name": "GSPC.Close",
"price":     73,
"rsi":   31.2,
"ret": 0.024849 
},
{
 "date":    189,
"name": "GSPC.Close",
"price":  74.06,
"rsi": 42.575,
"ret": 0.014521 
},
{
 "date":    190,
"name": "GSPC.Close",
"price":  74.45,
"rsi": 48.108,
"ret": 0.005266 
},
{
 "date":    193,
"name": "GSPC.Close",
"price":  74.55,
"rsi": 50.017,
"ret": 0.0013432 
},
{
 "date":    194,
"name": "GSPC.Close",
"price":  74.42,
"rsi": 50.519,
"ret": -0.0017438 
},
{
 "date":    195,
"name": "GSPC.Close",
"price":  75.23,
"rsi": 49.818,
"ret": 0.010884 
},
{
 "date":    196,
"name": "GSPC.Close",
"price":  76.34,
"rsi": 54.093,
"ret": 0.014755 
},
{
 "date":    197,
"name": "GSPC.Close",
"price":  77.69,
"rsi":  59.22,
"ret": 0.017684 
},
{
 "date":    200,
"name": "GSPC.Close",
"price":  77.79,
"rsi": 64.424,
"ret": 0.0012872 
},
{
 "date":    201,
"name": "GSPC.Close",
"price":  76.98,
"rsi": 64.783,
"ret": -0.010413 
},
{
 "date":    202,
"name": "GSPC.Close",
"price":  77.03,
"rsi": 59.548,
"ret": 0.00064952 
},
{
 "date":    203,
"name": "GSPC.Close",
"price":     78,
"rsi": 59.764,
"ret": 0.012592 
},
{
 "date":    204,
"name": "GSPC.Close",
"price":  77.82,
"rsi": 63.804,
"ret": -0.0023077 
},
{
 "date":    207,
"name": "GSPC.Close",
"price":  77.65,
"rsi": 62.549,
"ret": -0.0021845 
},
{
 "date":    208,
"name": "GSPC.Close",
"price":  77.77,
"rsi": 61.322,
"ret": 0.0015454 
},
{
 "date":    209,
"name": "GSPC.Close",
"price":  78.04,
"rsi": 61.891,
"ret": 0.0034718 
},
{
 "date":    210,
"name": "GSPC.Close",
"price":  78.07,
"rsi": 63.201,
"ret": 0.00038442 
},
{
 "date":    211,
"name": "GSPC.Close",
"price":  78.05,
"rsi": 63.351,
"ret": -0.00025618 
},
{
 "date":    214,
"name": "GSPC.Close",
"price":  77.02,
"rsi": 63.166,
"ret": -0.013197 
},
{
 "date":    215,
"name": "GSPC.Close",
"price":  77.19,
"rsi": 54.329,
"ret": 0.0022072 
},
{
 "date":    216,
"name": "GSPC.Close",
"price":  77.18,
"rsi": 55.437,
"ret": -0.00012955 
},
{
 "date":    217,
"name": "GSPC.Close",
"price":  77.08,
"rsi": 55.352,
"ret": -0.0012957 
},
{
 "date":    218,
"name": "GSPC.Close",
"price":  77.28,
"rsi": 54.452,
"ret": 0.0025947 
},
{
 "date":    221,
"name": "GSPC.Close",
"price":   76.2,
"rsi": 55.993,
"ret": -0.013975 
},
{
 "date":    222,
"name": "GSPC.Close",
"price":  75.82,
"rsi": 46.788,
"ret": -0.0049869 
},
{
 "date":    223,
"name": "GSPC.Close",
"price":  75.42,
"rsi": 44.044,
"ret": -0.0052757 
},
{
 "date":    224,
"name": "GSPC.Close",
"price":  74.76,
"rsi": 41.299,
"ret": -0.008751 
},
{
 "date":    225,
"name": "GSPC.Close",
"price":  75.18,
"rsi": 37.181,
"ret": 0.005618 
},
{
 "date":    228,
"name": "GSPC.Close",
"price":  75.33,
"rsi": 41.199,
"ret": 0.0019952 
},
{
 "date":    229,
"name": "GSPC.Close",
"price":   76.2,
"rsi": 42.611,
"ret": 0.011549 
},
{
 "date":    230,
"name": "GSPC.Close",
"price":  76.96,
"rsi": 50.095,
"ret": 0.0099738 
},
{
 "date":    231,
"name": "GSPC.Close",
"price":  77.84,
"rsi": 55.549,
"ret": 0.011435 
},
{
 "date":    232,
"name": "GSPC.Close",
"price":  79.24,
"rsi":  60.88,
"ret": 0.017986 
},
{
 "date":    235,
"name": "GSPC.Close",
"price":  80.99,
"rsi": 67.548,
"ret": 0.022085 
},
{
 "date":    236,
"name": "GSPC.Close",
"price":  81.12,
"rsi": 73.605,
"ret": 0.0016051 
},
{
 "date":    237,
"name": "GSPC.Close",
"price":  81.21,
"rsi": 73.993,
"ret": 0.0011095 
},
{
 "date":    238,
"name": "GSPC.Close",
"price":  81.08,
"rsi": 74.275,
"ret": -0.0016008 
},
{
 "date":    239,
"name": "GSPC.Close",
"price":  81.86,
"rsi": 73.042,
"ret": 0.0096201 
},
{
 "date":    242,
"name": "GSPC.Close",
"price":  81.52,
"rsi": 75.653,
"ret": -0.0041534 
},
{
 "date":    243,
"name": "GSPC.Close",
"price":  80.95,
"rsi": 72.363,
"ret": -0.0069921 
},
{
 "date":    244,
"name": "GSPC.Close",
"price":  80.96,
"rsi": 67.096,
"ret": 0.00012353 
},
{
 "date":    245,
"name": "GSPC.Close",
"price":  82.09,
"rsi": 67.141,
"ret": 0.013958 
},
{
 "date":    246,
"name": "GSPC.Close",
"price":  82.83,
"rsi": 71.846,
"ret": 0.0090145 
},
{
 "date":    250,
"name": "GSPC.Close",
"price":  83.04,
"rsi": 74.429,
"ret": 0.0025353 
},
{
 "date":    251,
"name": "GSPC.Close",
"price":  82.79,
"rsi": 75.126,
"ret": -0.0030106 
},
{
 "date":    252,
"name": "GSPC.Close",
"price":   82.3,
"rsi": 72.589,
"ret": -0.0059186 
},
{
 "date":    253,
"name": "GSPC.Close",
"price":  82.52,
"rsi": 67.757,
"ret": 0.0026731 
},
{
 "date":    256,
"name": "GSPC.Close",
"price":  82.07,
"rsi": 68.763,
"ret": -0.0054532 
},
{
 "date":    257,
"name": "GSPC.Close",
"price":  81.36,
"rsi": 64.344,
"ret": -0.0086512 
},
{
 "date":    258,
"name": "GSPC.Close",
"price":  81.79,
"rsi": 58.009,
"ret": 0.0052852 
},
{
 "date":    259,
"name": "GSPC.Close",
"price":  82.29,
"rsi": 60.543,
"ret": 0.0061132 
},
{
 "date":    260,
"name": "GSPC.Close",
"price":  82.62,
"rsi": 63.314,
"ret": 0.0040102 
},
{
 "date":    263,
"name": "GSPC.Close",
"price":  81.91,
"rsi": 65.059,
"ret": -0.0085936 
},
{
 "date":    264,
"name": "GSPC.Close",
"price":  81.86,
"rsi": 58.602,
"ret": -0.00061043 
},
{
 "date":    265,
"name": "GSPC.Close",
"price":  81.91,
"rsi": 58.164,
"ret": 0.0006108 
},
{
 "date":    266,
"name": "GSPC.Close",
"price":  81.66,
"rsi": 58.498,
"ret": -0.0030521 
},
{
 "date":    267,
"name": "GSPC.Close",
"price":  82.83,
"rsi": 56.088,
"ret": 0.014328 
},
{
 "date":    270,
"name": "GSPC.Close",
"price":  83.91,
"rsi": 63.639,
"ret": 0.013039 
},
{
 "date":    271,
"name": "GSPC.Close",
"price":  83.86,
"rsi": 68.947,
"ret": -0.00059588 
},
{
 "date":    272,
"name": "GSPC.Close",
"price":   84.3,
"rsi": 68.449,
"ret": 0.0052468 
},
{
 "date":    273,
"name": "GSPC.Close",
"price":  84.32,
"rsi": 70.471,
"ret": 0.00023725 
},
{
 "date":    274,
"name": "GSPC.Close",
"price":  85.16,
"rsi": 70.563,
"ret": 0.009962 
},
{
 "date":    277,
"name": "GSPC.Close",
"price":  86.47,
"rsi": 74.211,
"ret": 0.015383 
},
{
 "date":    278,
"name": "GSPC.Close",
"price":  86.85,
"rsi": 78.654,
"ret": 0.0043946 
},
{
 "date":    279,
"name": "GSPC.Close",
"price":  86.89,
"rsi": 79.744,
"ret": 0.00046056 
},
{
 "date":    280,
"name": "GSPC.Close",
"price":  85.95,
"rsi": 79.861,
"ret": -0.010818 
},
{
 "date":    281,
"name": "GSPC.Close",
"price":  85.08,
"rsi": 69.707,
"ret": -0.010122 
},
{
 "date":    284,
"name": "GSPC.Close",
"price":  84.17,
"rsi": 61.866,
"ret": -0.010696 
},
{
 "date":    285,
"name": "GSPC.Close",
"price":  84.06,
"rsi": 54.909,
"ret": -0.0013069 
},
{
 "date":    286,
"name": "GSPC.Close",
"price":  84.19,
"rsi": 54.117,
"ret": 0.0015465 
},
{
 "date":    287,
"name": "GSPC.Close",
"price":  84.65,
"rsi": 54.944,
"ret": 0.0054638 
},
{
 "date":    288,
"name": "GSPC.Close",
"price":  84.28,
"rsi": 57.841,
"ret": -0.0043709 
},
{
 "date":    291,
"name": "GSPC.Close",
"price":  83.15,
"rsi":  54.79,
"ret": -0.013408 
},
{
 "date":    292,
"name": "GSPC.Close",
"price":  83.64,
"rsi": 46.689,
"ret": 0.005893 
},
{
 "date":    293,
"name": "GSPC.Close",
"price":  83.66,
"rsi": 50.132,
"ret": 0.00023912 
},
{
 "date":    294,
"name": "GSPC.Close",
"price":  83.38,
"rsi": 50.273,
"ret": -0.0033469 
},
{
 "date":    295,
"name": "GSPC.Close",
"price":  83.77,
"rsi": 48.215,
"ret": 0.0046774 
},
{
 "date":    298,
"name": "GSPC.Close",
"price":  83.31,
"rsi": 51.211,
"ret": -0.0054912 
},
{
 "date":    299,
"name": "GSPC.Close",
"price":  83.12,
"rsi": 47.706,
"ret": -0.0022806 
},
{
 "date":    300,
"name": "GSPC.Close",
"price":  83.43,
"rsi": 46.296,
"ret": 0.0037295 
},
{
 "date":    301,
"name": "GSPC.Close",
"price":  83.36,
"rsi": 48.947,
"ret": -0.00083903 
},
{
 "date":    302,
"name": "GSPC.Close",
"price":  83.25,
"rsi": 48.366,
"ret": -0.0013196 
},
{
 "date":    305,
"name": "GSPC.Close",
"price":  83.51,
"rsi": 47.415,
"ret": 0.0031231 
},
{
 "date":    306,
"name": "GSPC.Close",
"price":  84.22,
"rsi": 49.923,
"ret": 0.008502 
},
{
 "date":    307,
"name": "GSPC.Close",
"price":  84.39,
"rsi": 56.083,
"ret": 0.0020185 
},
{
 "date":    308,
"name": "GSPC.Close",
"price":   84.1,
"rsi": 57.433,
"ret": -0.0034364 
},
{
 "date":    309,
"name": "GSPC.Close",
"price":  84.22,
"rsi": 54.362,
"ret": 0.0014269 
},
{
 "date":    312,
"name": "GSPC.Close",
"price":  84.67,
"rsi": 55.424,
"ret": 0.0053431 
},
{
 "date":    313,
"name": "GSPC.Close",
"price":  84.79,
"rsi": 59.253,
"ret": 0.0014173 
},
{
 "date":    314,
"name": "GSPC.Close",
"price":  85.03,
"rsi": 60.234,
"ret": 0.0028305 
},
{
 "date":    315,
"name": "GSPC.Close",
"price":  84.15,
"rsi": 62.195,
"ret": -0.010349 
},
{
 "date":    316,
"name": "GSPC.Close",
"price":  83.37,
"rsi": 52.061,
"ret": -0.0092692 
},
{
 "date":    319,
"name": "GSPC.Close",
"price":  83.24,
"rsi": 45.053,
"ret": -0.0015593 
},
{
 "date":    320,
"name": "GSPC.Close",
"price":  83.47,
"rsi": 43.991,
"ret": 0.0027631 
},
{
 "date":    321,
"name": "GSPC.Close",
"price":  82.79,
"rsi":   46.4,
"ret": -0.0081466 
},
{
 "date":    322,
"name": "GSPC.Close",
"price":  82.91,
"rsi": 40.811,
"ret": 0.0014495 
},
{
 "date":    323,
"name": "GSPC.Close",
"price":  83.72,
"rsi": 42.135,
"ret": 0.0097696 
},
{
 "date":    326,
"name": "GSPC.Close",
"price":  84.24,
"rsi": 50.232,
"ret": 0.0062112 
},
{
 "date":    327,
"name": "GSPC.Close",
"price":  84.78,
"rsi": 54.621,
"ret": 0.0064103 
},
{
 "date":    328,
"name": "GSPC.Close",
"price":  85.09,
"rsi": 58.695,
"ret": 0.0036565 
},
{
 "date":    330,
"name": "GSPC.Close",
"price":  85.93,
"rsi": 60.867,
"ret": 0.0098719 
},
{
 "date":    333,
"name": "GSPC.Close",
"price":   87.2,
"rsi": 66.074,
"ret": 0.014779 
},
{
 "date":    334,
"name": "GSPC.Close",
"price":  87.47,
"rsi": 72.114,
"ret": 0.0030963 
},
{
 "date":    335,
"name": "GSPC.Close",
"price":  88.48,
"rsi": 73.206,
"ret": 0.011547 
},
{
 "date":    336,
"name": "GSPC.Close",
"price":   88.9,
"rsi": 76.858,
"ret": 0.0047468 
},
{
 "date":    337,
"name": "GSPC.Close",
"price":  89.46,
"rsi": 78.189,
"ret": 0.0062992 
},
{
 "date":    340,
"name": "GSPC.Close",
"price":  89.94,
"rsi": 79.853,
"ret": 0.0053655 
},
{
 "date":    341,
"name": "GSPC.Close",
"price":  89.47,
"rsi": 81.179,
"ret": -0.0052257 
},
{
 "date":    342,
"name": "GSPC.Close",
"price":  89.54,
"rsi": 75.912,
"ret": 0.00078239 
},
{
 "date":    343,
"name": "GSPC.Close",
"price":  89.92,
"rsi":  76.16,
"ret": 0.0042439 
},
{
 "date":    344,
"name": "GSPC.Close",
"price":  90.26,
"rsi": 77.514,
"ret": 0.0037811 
},
{
 "date":    347,
"name": "GSPC.Close",
"price":   89.8,
"rsi":  78.68,
"ret": -0.0050964 
},
{
 "date":    348,
"name": "GSPC.Close",
"price":  89.66,
"rsi": 73.151,
"ret": -0.001559 
},
{
 "date":    349,
"name": "GSPC.Close",
"price":  89.72,
"rsi": 71.504,
"ret": 0.00066919 
},
{
 "date":    350,
"name": "GSPC.Close",
"price":  90.04,
"rsi": 71.797,
"ret": 0.0035667 
},
{
 "date":    351,
"name": "GSPC.Close",
"price":  90.22,
"rsi":  73.37,
"ret": 0.0019991 
},
{
 "date":    354,
"name": "GSPC.Close",
"price":  89.94,
"rsi": 74.241,
"ret": -0.0031035 
},
{
 "date":    355,
"name": "GSPC.Close",
"price":  90.04,
"rsi": 70.387,
"ret": 0.0011119 
},
{
 "date":    356,
"name": "GSPC.Close",
"price":   90.1,
"rsi": 70.966,
"ret": 0.00066637 
},
{
 "date":    357,
"name": "GSPC.Close",
"price":  90.61,
"rsi": 71.329,
"ret": 0.0056604 
},
{
 "date":    361,
"name": "GSPC.Close",
"price":  91.09,
"rsi": 74.271,
"ret": 0.0052974 
},
{
 "date":    362,
"name": "GSPC.Close",
"price":  92.08,
"rsi": 76.694,
"ret": 0.010868 
},
{
 "date":    363,
"name": "GSPC.Close",
"price":  92.27,
"rsi": 80.727,
"ret": 0.0020634 
},
{
 "date":    364,
"name": "GSPC.Close",
"price":  92.15,
"rsi": 81.392,
"ret": -0.0013005 
},
{
 "date":    368,
"name": "GSPC.Close",
"price":  91.15,
"rsi": 79.525,
"ret": -0.010852 
},
{
 "date":    369,
"name": "GSPC.Close",
"price":   91.8,
"rsi": 65.946,
"ret": 0.0071311 
},
{
 "date":    370,
"name": "GSPC.Close",
"price":  92.35,
"rsi": 69.581,
"ret": 0.0059913 
},
{
 "date":    371,
"name": "GSPC.Close",
"price":  92.38,
"rsi": 72.278,
"ret": 0.00032485 
},
{
 "date":    372,
"name": "GSPC.Close",
"price":  92.19,
"rsi": 72.422,
"ret": -0.0020567 
},
{
 "date":    375,
"name": "GSPC.Close",
"price":  91.98,
"rsi":  69.95,
"ret": -0.0022779 
},
{
 "date":    376,
"name": "GSPC.Close",
"price":  92.72,
"rsi": 67.219,
"ret": 0.0080452 
},
{
 "date":    377,
"name": "GSPC.Close",
"price":  92.56,
"rsi": 71.449,
"ret": -0.0017256 
},
{
 "date":    378,
"name": "GSPC.Close",
"price":   92.8,
"rsi": 69.365,
"ret": 0.0025929 
},
{
 "date":    379,
"name": "GSPC.Close",
"price":  93.03,
"rsi": 70.744,
"ret": 0.0024784 
},
{
 "date":    382,
"name": "GSPC.Close",
"price":  93.41,
"rsi": 72.042,
"ret": 0.0040847 
},
{
 "date":    383,
"name": "GSPC.Close",
"price":  93.76,
"rsi": 74.088,
"ret": 0.0037469 
},
{
 "date":    384,
"name": "GSPC.Close",
"price":  93.78,
"rsi": 75.842,
"ret": 0.00021331 
},
{
 "date":    385,
"name": "GSPC.Close",
"price":  94.19,
"rsi": 75.942,
"ret": 0.0043719 
},
{
 "date":    386,
"name": "GSPC.Close",
"price":  94.88,
"rsi":  77.96,
"ret": 0.0073256 
},
{
 "date":    389,
"name": "GSPC.Close",
"price":  95.28,
"rsi": 80.869,
"ret": 0.0042159 
},
{
 "date":    390,
"name": "GSPC.Close",
"price":  95.59,
"rsi": 82.325,
"ret": 0.0032536 
},
{
 "date":    391,
"name": "GSPC.Close",
"price":  94.89,
"rsi": 83.381,
"ret": -0.0073229 
},
{
 "date":    392,
"name": "GSPC.Close",
"price":  95.21,
"rsi": 72.805,
"ret": 0.0033723 
},
{
 "date":    393,
"name": "GSPC.Close",
"price":  95.88,
"rsi": 74.403,
"ret": 0.0070371 
},
{
 "date":    396,
"name": "GSPC.Close",
"price":  96.42,
"rsi": 77.399,
"ret": 0.005632 
},
{
 "date":    397,
"name": "GSPC.Close",
"price":  96.43,
"rsi": 79.483,
"ret": 0.00010371 
},
{
 "date":    398,
"name": "GSPC.Close",
"price":  96.63,
"rsi":  79.52,
"ret": 0.002074 
},
{
 "date":    399,
"name": "GSPC.Close",
"price":  96.62,
"rsi": 80.299,
"ret": -0.00010349 
},
{
 "date":    400,
"name": "GSPC.Close",
"price":  96.93,
"rsi": 80.135,
"ret": 0.0032084 
},
{
 "date":    403,
"name": "GSPC.Close",
"price":  97.45,
"rsi": 81.404,
"ret": 0.0053647 
},
{
 "date":    404,
"name": "GSPC.Close",
"price":  97.51,
"rsi": 83.327,
"ret": 0.0006157 
},
{
 "date":    405,
"name": "GSPC.Close",
"price":  97.39,
"rsi": 83.539,
"ret": -0.0012306 
},
{
 "date":    406,
"name": "GSPC.Close",
"price":  97.91,
"rsi": 81.316,
"ret": 0.0053394 
},
{
 "date":    407,
"name": "GSPC.Close",
"price":  98.43,
"rsi":  83.38,
"ret": 0.005311 
},
{
 "date":    411,
"name": "GSPC.Close",
"price":  98.66,
"rsi": 85.146,
"ret": 0.0023367 
},
{
 "date":    412,
"name": "GSPC.Close",
"price":   98.2,
"rsi": 85.862,
"ret": -0.0046625 
},
{
 "date":    413,
"name": "GSPC.Close",
"price":  97.56,
"rsi": 77.788,
"ret": -0.0065173 
},
{
 "date":    414,
"name": "GSPC.Close",
"price":  96.74,
"rsi": 68.181,
"ret": -0.0084051 
},
{
 "date":    417,
"name": "GSPC.Close",
"price":  95.72,
"rsi": 58.255,
"ret": -0.010544 
},
{
 "date":    418,
"name": "GSPC.Close",
"price":  96.09,
"rsi": 48.747,
"ret": 0.0038654 
},
{
 "date":    419,
"name": "GSPC.Close",
"price":  96.73,
"rsi": 51.819,
"ret": 0.0066604 
},
{
 "date":    420,
"name": "GSPC.Close",
"price":  96.96,
"rsi": 56.658,
"ret": 0.0023778 
},
{
 "date":    421,
"name": "GSPC.Close",
"price":  96.75,
"rsi":  58.28,
"ret": -0.0021658 
},
{
 "date":    424,
"name": "GSPC.Close",
"price":     97,
"rsi": 56.212,
"ret": 0.002584 
},
{
 "date":    425,
"name": "GSPC.Close",
"price":  96.98,
"rsi": 58.117,
"ret": -0.00020619 
},
{
 "date":    426,
"name": "GSPC.Close",
"price":  96.95,
"rsi":   57.9,
"ret": -0.00030934 
},
{
 "date":    427,
"name": "GSPC.Close",
"price":  97.92,
"rsi": 57.553,
"ret": 0.010005 
},
{
 "date":    428,
"name": "GSPC.Close",
"price":  98.96,
"rsi": 64.885,
"ret": 0.010621 
},
{
 "date":    431,
"name": "GSPC.Close",
"price":  99.38,
"rsi": 70.724,
"ret": 0.0042441 
},
{
 "date":    432,
"name": "GSPC.Close",
"price":  99.46,
"rsi": 72.699,
"ret": 0.00080499 
},
{
 "date":    433,
"name": "GSPC.Close",
"price":   99.3,
"rsi": 73.071,
"ret": -0.0016087 
},
{
 "date":    434,
"name": "GSPC.Close",
"price":  99.39,
"rsi": 70.985,
"ret": 0.00090634 
},
{
 "date":    435,
"name": "GSPC.Close",
"price":  99.57,
"rsi": 71.478,
"ret": 0.001811 
},
{
 "date":    438,
"name": "GSPC.Close",
"price": 100.71,
"rsi": 72.486,
"ret": 0.011449 
},
{
 "date":    439,
"name": "GSPC.Close",
"price": 101.21,
"rsi": 77.828,
"ret": 0.0049648 
},
{
 "date":    440,
"name": "GSPC.Close",
"price": 101.12,
"rsi": 79.691,
"ret": -0.00088924 
},
{
 "date":    441,
"name": "GSPC.Close",
"price": 101.19,
"rsi": 78.414,
"ret": 0.00069225 
},
{
 "date":    442,
"name": "GSPC.Close",
"price": 101.01,
"rsi":   78.7,
"ret": -0.0017788 
},
{
 "date":    445,
"name": "GSPC.Close",
"price": 100.62,
"rsi": 75.915,
"ret": -0.003861 
},
{
 "date":    446,
"name": "GSPC.Close",
"price": 100.28,
"rsi": 70.127,
"ret": -0.003379 
},
{
 "date":    447,
"name": "GSPC.Close",
"price":  99.62,
"rsi": 65.442,
"ret": -0.0065816 
},
{
 "date":    448,
"name": "GSPC.Close",
"price":  99.61,
"rsi": 57.423,
"ret": -0.00010038 
},
{
 "date":    449,
"name": "GSPC.Close",
"price":  99.95,
"rsi": 57.308,
"ret": 0.0034133 
},
{
 "date":    452,
"name": "GSPC.Close",
"price": 100.03,
"rsi": 60.215,
"ret": 0.0008004 
},
{
 "date":    453,
"name": "GSPC.Close",
"price": 100.26,
"rsi":  60.89,
"ret": 0.0022993 
},
{
 "date":    454,
"name": "GSPC.Close",
"price": 100.31,
"rsi": 62.841,
"ret": 0.0004987 
},
{
 "date":    455,
"name": "GSPC.Close",
"price": 100.39,
"rsi":  63.27,
"ret": 0.00079753 
},
{
 "date":    456,
"name": "GSPC.Close",
"price": 100.56,
"rsi": 63.987,
"ret": 0.0016934 
},
{
 "date":    459,
"name": "GSPC.Close",
"price": 100.79,
"rsi": 65.526,
"ret": 0.0022872 
},
{
 "date":    460,
"name": "GSPC.Close",
"price": 101.51,
"rsi": 67.546,
"ret": 0.0071436 
},
{
 "date":    461,
"name": "GSPC.Close",
"price": 101.98,
"rsi": 72.901,
"ret": 0.0046301 
},
{
 "date":    462,
"name": "GSPC.Close",
"price":  102.1,
"rsi": 75.718,
"ret": 0.0011767 
},
{
 "date":    466,
"name": "GSPC.Close",
"price": 102.88,
"rsi": 76.392,
"ret": 0.0076396 
},
{
 "date":    467,
"name": "GSPC.Close",
"price": 102.98,
"rsi": 80.236,
"ret": 0.00097201 
},
{
 "date":    468,
"name": "GSPC.Close",
"price": 103.37,
"rsi": 80.671,
"ret": 0.0037871 
},
{
 "date":    469,
"name": "GSPC.Close",
"price": 103.52,
"rsi": 82.305,
"ret": 0.0014511 
},
{
 "date":    470,
"name": "GSPC.Close",
"price": 103.49,
"rsi": 82.903,
"ret": -0.0002898 
},
{
 "date":    473,
"name": "GSPC.Close",
"price": 104.01,
"rsi": 82.304,
"ret": 0.0050246 
},
{
 "date":    474,
"name": "GSPC.Close",
"price": 103.61,
"rsi": 84.409,
"ret": -0.0038458 
},
{
 "date":    475,
"name": "GSPC.Close",
"price": 103.36,
"rsi": 76.837,
"ret": -0.0024129 
},
{
 "date":    476,
"name": "GSPC.Close",
"price": 103.56,
"rsi": 72.461,
"ret": 0.001935 
},
{
 "date":    477,
"name": "GSPC.Close",
"price": 104.05,
"rsi": 73.749,
"ret": 0.0047316 
},
{
 "date":    480,
"name": "GSPC.Close",
"price": 103.94,
"rsi": 76.632,
"ret": -0.0010572 
},
{
 "date":    481,
"name": "GSPC.Close",
"price": 104.59,
"rsi":  74.65,
"ret": 0.0062536 
},
{
 "date":    482,
"name": "GSPC.Close",
"price": 104.77,
"rsi": 78.233,
"ret": 0.001721 
},
{
 "date":    483,
"name": "GSPC.Close",
"price": 104.63,
"rsi": 79.113,
"ret": -0.0013363 
},
{
 "date":    484,
"name": "GSPC.Close",
"price": 103.95,
"rsi": 76.521,
"ret": -0.0064991 
},
{
 "date":    487,
"name": "GSPC.Close",
"price": 103.29,
"rsi": 65.324,
"ret": -0.0063492 
},
{
 "date":    488,
"name": "GSPC.Close",
"price": 103.79,
"rsi": 56.659,
"ret": 0.0048407 
},
{
 "date":    489,
"name": "GSPC.Close",
"price": 103.78,
"rsi": 60.891,
"ret": -9.6348e-05 
},
{
 "date":    490,
"name": "GSPC.Close",
"price": 103.23,
"rsi": 60.763,
"ret": -0.0052997 
},
{
 "date":    491,
"name": "GSPC.Close",
"price": 102.87,
"rsi": 54.044,
"ret": -0.0034874 
},
{
 "date":    494,
"name": "GSPC.Close",
"price": 102.36,
"rsi": 50.137,
"ret": -0.0049577 
},
{
 "date":    495,
"name": "GSPC.Close",
"price": 102.62,
"rsi": 45.155,
"ret": 0.0025401 
},
{
 "date":    496,
"name": "GSPC.Close",
"price":  102.9,
"rsi": 47.992,
"ret": 0.0027285 
},
{
 "date":    497,
"name": "GSPC.Close",
"price": 102.69,
"rsi": 50.936,
"ret": -0.0020408 
},
{
 "date":    498,
"name": "GSPC.Close",
"price": 102.21,
"rsi": 48.709,
"ret": -0.0046743 
},
{
 "date":    501,
"name": "GSPC.Close",
"price": 100.69,
"rsi": 43.977,
"ret": -0.014871 
},
{
 "date":    502,
"name": "GSPC.Close",
"price": 100.83,
"rsi": 33.033,
"ret": 0.0013904 
},
{
 "date":    503,
"name": "GSPC.Close",
"price": 101.07,
"rsi": 34.646,
"ret": 0.0023802 
},
{
 "date":    504,
"name": "GSPC.Close",
"price": 101.31,
"rsi": 37.429,
"ret": 0.0023746 
},
{
 "date":    505,
"name": "GSPC.Close",
"price": 100.99,
"rsi": 40.172,
"ret": -0.0031586 
},
{
 "date":    508,
"name": "GSPC.Close",
"price": 100.13,
"rsi": 37.793,
"ret": -0.0085157 
},
{
 "date":    509,
"name": "GSPC.Close",
"price":  99.47,
"rsi": 32.263,
"ret": -0.0065914 
},
{
 "date":    510,
"name": "GSPC.Close",
"price":  99.59,
"rsi": 28.782,
"ret": 0.0012064 
},
{
 "date":    511,
"name": "GSPC.Close",
"price":   99.4,
"rsi": 30.255,
"ret": -0.0019078 
},
{
 "date":    512,
"name": "GSPC.Close",
"price":  99.63,
"rsi": 29.224,
"ret": 0.0023139 
},
{
 "date":    516,
"name": "GSPC.Close",
"price":  100.2,
"rsi": 32.234,
"ret": 0.0057212 
},
{
 "date":    517,
"name": "GSPC.Close",
"price": 100.96,
"rsi": 39.143,
"ret": 0.0075848 
},
{
 "date":    518,
"name": "GSPC.Close",
"price": 101.01,
"rsi": 46.913,
"ret": 0.00049525 
},
{
 "date":    519,
"name": "GSPC.Close",
"price":  101.3,
"rsi": 47.389,
"ret": 0.002871 
},
{
 "date":    522,
"name": "GSPC.Close",
"price": 101.09,
"rsi": 50.179,
"ret": -0.0020731 
},
{
 "date":    523,
"name": "GSPC.Close",
"price": 100.32,
"rsi": 48.186,
"ret": -0.007617 
},
{
 "date":    524,
"name": "GSPC.Close",
"price": 100.29,
"rsi": 41.654,
"ret": -0.00029904 
},
{
 "date":    525,
"name": "GSPC.Close",
"price": 100.64,
"rsi": 41.419,
"ret": 0.0034899 
},
{
 "date":    526,
"name": "GSPC.Close",
"price": 101.07,
"rsi": 45.305,
"ret": 0.0042727 
},
{
 "date":    529,
"name": "GSPC.Close",
"price": 100.22,
"rsi": 49.719,
"ret": -0.00841 
},
{
 "date":    530,
"name": "GSPC.Close",
"price": 100.32,
"rsi":  42.43,
"ret": 0.0009978 
},
{
 "date":    531,
"name": "GSPC.Close",
"price": 100.52,
"rsi":  43.48,
"ret": 0.0019936 
},
{
 "date":    532,
"name": "GSPC.Close",
"price":  100.5,
"rsi": 45.616,
"ret": -0.00019897 
},
{
 "date":    533,
"name": "GSPC.Close",
"price":  98.97,
"rsi": 45.431,
"ret": -0.015224 
},
{
 "date":    536,
"name": "GSPC.Close",
"price":  97.87,
"rsi": 34.058,
"ret": -0.011114 
},
{
 "date":    537,
"name": "GSPC.Close",
"price":  97.59,
"rsi": 28.528,
"ret": -0.0028609 
},
{
 "date":    538,
"name": "GSPC.Close",
"price":  98.41,
"rsi": 27.313,
"ret": 0.0084025 
},
{
 "date":    539,
"name": "GSPC.Close",
"price":  98.13,
"rsi": 35.924,
"ret": -0.0028452 
},
{
 "date":    540,
"name": "GSPC.Close",
"price":  97.99,
"rsi": 34.424,
"ret": -0.0014267 
},
{
 "date":    543,
"name": "GSPC.Close",
"price":  97.74,
"rsi": 33.667,
"ret": -0.0025513 
},
{
 "date":    544,
"name": "GSPC.Close",
"price":  98.82,
"rsi": 32.302,
"ret": 0.01105 
},
{
 "date":    545,
"name": "GSPC.Close",
"price":   98.7,
"rsi": 43.049,
"ret": -0.0012143 
},
{
 "date":    546,
"name": "GSPC.Close",
"price":  99.78,
"rsi": 42.246,
"ret": 0.010942 
},
{
 "date":    547,
"name": "GSPC.Close",
"price":  99.78,
"rsi": 51.084,
"ret":      0 
},
{
 "date":    551,
"name": "GSPC.Close",
"price":  99.76,
"rsi": 51.084,
"ret": -0.00020044 
},
{
 "date":    552,
"name": "GSPC.Close",
"price": 100.04,
"rsi": 50.917,
"ret": 0.0028067 
},
{
 "date":    553,
"name": "GSPC.Close",
"price": 100.34,
"rsi": 53.227,
"ret": 0.0029988 
},
{
 "date":    554,
"name": "GSPC.Close",
"price": 100.69,
"rsi": 55.636,
"ret": 0.0034881 
},
{
 "date":    557,
"name": "GSPC.Close",
"price": 100.82,
"rsi": 58.333,
"ret": 0.0012911 
},
{
 "date":    558,
"name": "GSPC.Close",
"price":   99.5,
"rsi": 59.322,
"ret": -0.013093 
},
{
 "date":    559,
"name": "GSPC.Close",
"price":  99.22,
"rsi": 47.098,
"ret": -0.0028141 
},
{
 "date":    560,
"name": "GSPC.Close",
"price":  99.28,
"rsi":  44.98,
"ret": 0.00060472 
},
{
 "date":    561,
"name": "GSPC.Close",
"price":  99.11,
"rsi": 45.545,
"ret": -0.0017123 
},
{
 "date":    564,
"name": "GSPC.Close",
"price":  98.93,
"rsi": 44.162,
"ret": -0.0018162 
},
{
 "date":    565,
"name": "GSPC.Close",
"price":  99.32,
"rsi": 42.683,
"ret": 0.0039422 
},
{
 "date":    566,
"name": "GSPC.Close",
"price":  99.28,
"rsi": 46.836,
"ret": -0.00040274 
},
{
 "date":    567,
"name": "GSPC.Close",
"price":  99.11,
"rsi": 46.464,
"ret": -0.0017123 
},
{
 "date":    568,
"name": "GSPC.Close",
"price":  98.94,
"rsi": 44.835,
"ret": -0.0017153 
},
{
 "date":    571,
"name": "GSPC.Close",
"price":  98.14,
"rsi": 43.203,
"ret": -0.0080857 
},
{
 "date":    572,
"name": "GSPC.Close",
"price":  97.78,
"rsi": 36.476,
"ret": -0.0036682 
},
{
 "date":    573,
"name": "GSPC.Close",
"price":  97.07,
"rsi": 33.917,
"ret": -0.0072612 
},
{
 "date":    574,
"name": "GSPC.Close",
"price":  96.02,
"rsi": 29.518,
"ret": -0.010817 
},
{
 "date":    575,
"name": "GSPC.Close",
"price":  95.58,
"rsi": 24.465,
"ret": -0.0045824 
},
{
 "date":    578,
"name": "GSPC.Close",
"price":  95.96,
"rsi": 22.711,
"ret": 0.0039757 
},
{
 "date":    579,
"name": "GSPC.Close",
"price":  94.51,
"rsi": 27.543,
"ret": -0.01511 
},
{
 "date":    580,
"name": "GSPC.Close",
"price":  93.89,
"rsi": 21.913,
"ret": -0.0065602 
},
{
 "date":    581,
"name": "GSPC.Close",
"price":  94.09,
"rsi": 20.028,
"ret": 0.0021302 
},
{
 "date":    582,
"name": "GSPC.Close",
"price":  94.25,
"rsi": 22.348,
"ret": 0.0017005 
},
{
 "date":    585,
"name": "GSPC.Close",
"price":  93.53,
"rsi": 24.243,
"ret": -0.0076393 
},
{
 "date":    586,
"name": "GSPC.Close",
"price":  93.54,
"rsi":  21.68,
"ret": 0.00010692 
},
{
 "date":    587,
"name": "GSPC.Close",
"price":  94.66,
"rsi": 21.803,
"ret": 0.011973 
},
{
 "date":    588,
"name": "GSPC.Close",
"price":     96,
"rsi": 34.311,
"ret": 0.014156 
},
{
 "date":    589,
"name": "GSPC.Close",
"price":  95.69,
"rsi": 45.536,
"ret": -0.0032292 
},
{
 "date":    592,
"name": "GSPC.Close",
"price":  98.76,
"rsi": 43.677,
"ret": 0.032083 
},
{
 "date":    593,
"name": "GSPC.Close",
"price":  99.99,
"rsi": 60.764,
"ret": 0.012454 
},
{
 "date":    594,
"name": "GSPC.Close",
"price":   98.6,
"rsi": 65.306,
"ret": -0.013901 
},
{
 "date":    595,
"name": "GSPC.Close",
"price":  98.16,
"rsi": 57.242,
"ret": -0.0044625 
},
{
 "date":    596,
"name": "GSPC.Close",
"price":  98.33,
"rsi":  54.93,
"ret": 0.0017319 
},
{
 "date":    599,
"name": "GSPC.Close",
"price":  99.25,
"rsi": 55.675,
"ret": 0.0093562 
},
{
 "date":    600,
"name": "GSPC.Close",
"price":  100.4,
"rsi":  59.57,
"ret": 0.011587 
},
{
 "date":    601,
"name": "GSPC.Close",
"price": 100.41,
"rsi": 63.846,
"ret": 9.9602e-05 
},
{
 "date":    602,
"name": "GSPC.Close",
"price": 100.24,
"rsi": 63.882,
"ret": -0.0016931 
},
{
 "date":    603,
"name": "GSPC.Close",
"price": 100.48,
"rsi": 62.745,
"ret": 0.0023943 
},
{
 "date":    606,
"name": "GSPC.Close",
"price":  99.52,
"rsi": 63.726,
"ret": -0.0095541 
},
{
 "date":    607,
"name": "GSPC.Close",
"price":  99.03,
"rsi": 57.233,
"ret": -0.0049236 
},
{
 "date":    608,
"name": "GSPC.Close",
"price":  99.07,
"rsi": 54.197,
"ret": 0.00040392 
},
{
 "date":    609,
"name": "GSPC.Close",
"price":  99.29,
"rsi": 54.409,
"ret": 0.0022207 
},
{
 "date":    610,
"name": "GSPC.Close",
"price": 100.69,
"rsi": 55.629,
"ret": 0.0141 
},
{
 "date":    614,
"name": "GSPC.Close",
"price": 101.15,
"rsi": 62.504,
"ret": 0.0045685 
},
{
 "date":    615,
"name": "GSPC.Close",
"price": 101.34,
"rsi": 64.453,
"ret": 0.0018784 
},
{
 "date":    616,
"name": "GSPC.Close",
"price":  100.8,
"rsi": 65.257,
"ret": -0.0053286 
},
{
 "date":    617,
"name": "GSPC.Close",
"price": 100.42,
"rsi": 61.035,
"ret": -0.0037698 
},
{
 "date":    620,
"name": "GSPC.Close",
"price": 100.07,
"rsi": 58.183,
"ret": -0.0034854 
},
{
 "date":    621,
"name": "GSPC.Close",
"price":  99.34,
"rsi": 55.605,
"ret": -0.0072949 
},
{
 "date":    622,
"name": "GSPC.Close",
"price":  99.77,
"rsi": 50.572,
"ret": 0.0043286 
},
{
 "date":    623,
"name": "GSPC.Close",
"price":  99.66,
"rsi": 53.256,
"ret": -0.0011025 
},
{
 "date":    624,
"name": "GSPC.Close",
"price":  99.96,
"rsi": 52.471,
"ret": 0.0030102 
},
{
 "date":    627,
"name": "GSPC.Close",
"price":  99.68,
"rsi": 54.443,
"ret": -0.0028011 
},
{
 "date":    628,
"name": "GSPC.Close",
"price":  99.34,
"rsi": 52.264,
"ret": -0.0034109 
},
{
 "date":    629,
"name": "GSPC.Close",
"price":  98.47,
"rsi": 49.664,
"ret": -0.0087578 
},
{
 "date":    630,
"name": "GSPC.Close",
"price":  98.38,
"rsi": 43.677,
"ret": -0.00091398 
},
{
 "date":    631,
"name": "GSPC.Close",
"price":  98.15,
"rsi": 43.098,
"ret": -0.0023379 
},
{
 "date":    634,
"name": "GSPC.Close",
"price":  97.62,
"rsi": 41.581,
"ret": -0.0053999 
},
{
 "date":    635,
"name": "GSPC.Close",
"price":  97.88,
"rsi": 38.242,
"ret": 0.0026634 
},
{
 "date":    636,
"name": "GSPC.Close",
"price":   97.9,
"rsi": 40.755,
"ret": 0.00020433 
},
{
 "date":    637,
"name": "GSPC.Close",
"price":  98.34,
"rsi": 40.954,
"ret": 0.0044944 
},
{
 "date":    638,
"name": "GSPC.Close",
"price":  98.93,
"rsi": 45.309,
"ret": 0.0059996 
},
{
 "date":    641,
"name": "GSPC.Close",
"price":  99.21,
"rsi": 50.572,
"ret": 0.0028303 
},
{
 "date":    642,
"name": "GSPC.Close",
"price":  99.11,
"rsi":  52.89,
"ret": -0.001008 
},
{
 "date":    643,
"name": "GSPC.Close",
"price":  99.82,
"rsi": 51.953,
"ret": 0.0071638 
},
{
 "date":    644,
"name": "GSPC.Close",
"price": 100.02,
"rsi": 57.684,
"ret": 0.0020036 
},
{
 "date":    645,
"name": "GSPC.Close",
"price":  99.36,
"rsi": 59.162,
"ret": -0.0065987 
},
{
 "date":    648,
"name": "GSPC.Close",
"price":  99.21,
"rsi":  52.63,
"ret": -0.0015097 
},
{
 "date":    649,
"name": "GSPC.Close",
"price":  99.57,
"rsi": 51.245,
"ret": 0.0036287 
},
{
 "date":    650,
"name": "GSPC.Close",
"price":  99.03,
"rsi":  54.35,
"ret": -0.0054233 
},
{
 "date":    651,
"name": "GSPC.Close",
"price":  98.13,
"rsi": 49.281,
"ret": -0.0090882 
},
{
 "date":    652,
"name": "GSPC.Close",
"price":  97.79,
"rsi": 42.215,
"ret": -0.0034648 
},
{
 "date":    655,
"name": "GSPC.Close",
"price":  97.35,
"rsi": 39.888,
"ret": -0.0044994 
},
{
 "date":    656,
"name": "GSPC.Close",
"price":     97,
"rsi": 37.042,
"ret": -0.0035953 
},
{
 "date":    657,
"name": "GSPC.Close",
"price":  95.65,
"rsi": 34.909,
"ret": -0.013918 
},
{
 "date":    658,
"name": "GSPC.Close",
"price":   95.6,
"rsi":  28.17,
"ret": -0.00052274 
},
{
 "date":    659,
"name": "GSPC.Close",
"price":  95.57,
"rsi": 27.954,
"ret": -0.00031381 
},
{
 "date":    662,
"name": "GSPC.Close",
"price":   95.1,
"rsi": 27.817,
"ret": -0.0049179 
},
{
 "date":    663,
"name": "GSPC.Close",
"price":  94.74,
"rsi": 25.688,
"ret": -0.0037855 
},
{
 "date":    664,
"name": "GSPC.Close",
"price":  93.79,
"rsi": 24.162,
"ret": -0.010027 
},
{
 "date":    665,
"name": "GSPC.Close",
"price":  93.96,
"rsi": 20.673,
"ret": 0.0018126 
},
{
 "date":    666,
"name": "GSPC.Close",
"price":  94.23,
"rsi": 22.821,
"ret": 0.0028736 
},
{
 "date":    669,
"name": "GSPC.Close",
"price":   92.8,
"rsi": 26.237,
"ret": -0.015176 
},
{
 "date":    670,
"name": "GSPC.Close",
"price":  93.18,
"rsi": 20.948,
"ret": 0.0040948 
},
{
 "date":    671,
"name": "GSPC.Close",
"price":  94.91,
"rsi":  25.26,
"ret": 0.018566 
},
{
 "date":    672,
"name": "GSPC.Close",
"price":  94.79,
"rsi": 41.028,
"ret": -0.0012644 
},
{
 "date":    673,
"name": "GSPC.Close",
"price":  94.46,
"rsi": 40.392,
"ret": -0.0034814 
},
{
 "date":    676,
"name": "GSPC.Close",
"price":  94.39,
"rsi": 38.617,
"ret": -0.00074105 
},
{
 "date":    677,
"name": "GSPC.Close",
"price":  94.46,
"rsi": 38.233,
"ret": 0.0007416 
},
{
 "date":    678,
"name": "GSPC.Close",
"price":  93.41,
"rsi": 38.887,
"ret": -0.011116 
},
{
 "date":    679,
"name": "GSPC.Close",
"price":  92.12,
"rsi": 33.208,
"ret": -0.01381 
},
{
 "date":    680,
"name": "GSPC.Close",
"price":  92.12,
"rsi": 27.831,
"ret":      0 
},
{
 "date":    683,
"name": "GSPC.Close",
"price":  91.81,
"rsi": 27.831,
"ret": -0.0033652 
},
{
 "date":    684,
"name": "GSPC.Close",
"price":  92.71,
"rsi": 26.629,
"ret": 0.0098029 
},
{
 "date":    685,
"name": "GSPC.Close",
"price":  92.85,
"rsi": 35.356,
"ret": 0.0015101 
},
{
 "date":    686,
"name": "GSPC.Close",
"price":  92.13,
"rsi": 36.619,
"ret": -0.0077544 
},
{
 "date":    687,
"name": "GSPC.Close",
"price":  91.61,
"rsi": 33.044,
"ret": -0.0056442 
},
{
 "date":    690,
"name": "GSPC.Close",
"price":  90.79,
"rsi": 30.711,
"ret": -0.008951 
},
{
 "date":    691,
"name": "GSPC.Close",
"price":  90.16,
"rsi": 27.424,
"ret": -0.0069391 
},
{
 "date":    692,
"name": "GSPC.Close",
"price":  90.33,
"rsi": 25.193,
"ret": 0.0018855 
},
{
 "date":    694,
"name": "GSPC.Close",
"price":  91.94,
"rsi": 26.921,
"ret": 0.017824 
},
{
 "date":    697,
"name": "GSPC.Close",
"price":  93.41,
"rsi": 40.853,
"ret": 0.015989 
},
{
 "date":    698,
"name": "GSPC.Close",
"price":  93.99,
"rsi": 50.191,
"ret": 0.0062092 
},
{
 "date":    699,
"name": "GSPC.Close",
"price":  95.44,
"rsi": 53.322,
"ret": 0.015427 
},
{
 "date":    700,
"name": "GSPC.Close",
"price":  95.84,
"rsi": 60.078,
"ret": 0.0041911 
},
{
 "date":    701,
"name": "GSPC.Close",
"price":  97.06,
"rsi": 61.724,
"ret": 0.01273 
},
{
 "date":    704,
"name": "GSPC.Close",
"price":  96.51,
"rsi": 66.289,
"ret": -0.0056666 
},
{
 "date":    705,
"name": "GSPC.Close",
"price":  96.87,
"rsi": 62.661,
"ret": 0.0037302 
},
{
 "date":    706,
"name": "GSPC.Close",
"price":  96.92,
"rsi": 64.048,
"ret": 0.00051616 
},
{
 "date":    707,
"name": "GSPC.Close",
"price":  96.96,
"rsi": 64.247,
"ret": 0.00041271 
},
{
 "date":    708,
"name": "GSPC.Close",
"price":  97.69,
"rsi": 64.416,
"ret": 0.0075289 
},
{
 "date":    711,
"name": "GSPC.Close",
"price":  97.97,
"rsi": 67.448,
"ret": 0.0028662 
},
{
 "date":    712,
"name": "GSPC.Close",
"price":  97.67,
"rsi": 68.554,
"ret": -0.0030622 
},
{
 "date":    713,
"name": "GSPC.Close",
"price":  98.54,
"rsi": 65.967,
"ret": 0.0089075 
},
{
 "date":    714,
"name": "GSPC.Close",
"price":  99.74,
"rsi": 69.555,
"ret": 0.012178 
},
{
 "date":    715,
"name": "GSPC.Close",
"price": 100.26,
"rsi": 73.678,
"ret": 0.0052136 
},
{
 "date":    718,
"name": "GSPC.Close",
"price": 101.55,
"rsi": 75.243,
"ret": 0.012867 
},
{
 "date":    719,
"name": "GSPC.Close",
"price":  101.8,
"rsi": 78.635,
"ret": 0.0024618 
},
{
 "date":    720,
"name": "GSPC.Close",
"price": 101.18,
"rsi": 79.229,
"ret": -0.0060904 
},
{
 "date":    721,
"name": "GSPC.Close",
"price": 100.74,
"rsi": 73.752,
"ret": -0.0043487 
},
{
 "date":    725,
"name": "GSPC.Close",
"price": 100.95,
"rsi": 70.052,
"ret": 0.0020846 
},
{
 "date":    726,
"name": "GSPC.Close",
"price": 101.95,
"rsi": 70.805,
"ret": 0.0099059 
},
{
 "date":    727,
"name": "GSPC.Close",
"price": 102.21,
"rsi": 74.139,
"ret": 0.0025503 
},
{
 "date":    728,
"name": "GSPC.Close",
"price": 101.78,
"rsi":  74.94,
"ret": -0.004207 
},
{
 "date":    729,
"name": "GSPC.Close",
"price": 102.09,
"rsi": 71.021,
"ret": 0.0030458 
},
{
 "date":    732,
"name": "GSPC.Close",
"price": 101.67,
"rsi": 72.152,
"ret": -0.004114 
},
{
 "date":    733,
"name": "GSPC.Close",
"price": 102.09,
"rsi": 68.265,
"ret": 0.004131 
},
{
 "date":    734,
"name": "GSPC.Close",
"price": 103.06,
"rsi": 70.005,
"ret": 0.0095014 
},
{
 "date":    735,
"name": "GSPC.Close",
"price": 103.51,
"rsi": 73.605,
"ret": 0.0043664 
},
{
 "date":    736,
"name": "GSPC.Close",
"price": 103.47,
"rsi": 75.098,
"ret": -0.00038644 
},
{
 "date":    739,
"name": "GSPC.Close",
"price": 103.32,
"rsi": 74.693,
"ret": -0.0014497 
},
{
 "date":    740,
"name": "GSPC.Close",
"price": 103.65,
"rsi": 73.103,
"ret": 0.003194 
},
{
 "date":    741,
"name": "GSPC.Close",
"price": 103.59,
"rsi": 74.395,
"ret": -0.00057887 
},
{
 "date":    742,
"name": "GSPC.Close",
"price": 102.99,
"rsi": 73.702,
"ret": -0.0057921 
},
{
 "date":    743,
"name": "GSPC.Close",
"price": 103.39,
"rsi": 66.983,
"ret": 0.0038839 
},
{
 "date":    746,
"name": "GSPC.Close",
"price":  103.7,
"rsi": 69.011,
"ret": 0.0029984 
},
{
 "date":    747,
"name": "GSPC.Close",
"price": 104.05,
"rsi": 70.523,
"ret": 0.0033751 
},
{
 "date":    748,
"name": "GSPC.Close",
"price": 103.88,
"rsi": 72.173,
"ret": -0.0016338 
},
{
 "date":    749,
"name": "GSPC.Close",
"price": 103.88,
"rsi":  70.12,
"ret":      0 
},
{
 "date":    750,
"name": "GSPC.Close",
"price": 103.65,
"rsi":  70.12,
"ret": -0.0022141 
},
{
 "date":    753,
"name": "GSPC.Close",
"price": 102.57,
"rsi": 67.123,
"ret": -0.01042 
},
{
 "date":    754,
"name": "GSPC.Close",
"price":  102.7,
"rsi": 55.197,
"ret": 0.0012674 
},
{
 "date":    755,
"name": "GSPC.Close",
"price":  102.5,
"rsi": 56.205,
"ret": -0.0019474 
},
{
 "date":    756,
"name": "GSPC.Close",
"price":  103.5,
"rsi": 54.184,
"ret": 0.0097561 
},
{
 "date":    757,
"name": "GSPC.Close",
"price": 104.16,
"rsi": 61.617,
"ret": 0.0063768 
},
{
 "date":    760,
"name": "GSPC.Close",
"price": 103.94,
"rsi": 65.585,
"ret": -0.0021121 
},
{
 "date":    761,
"name": "GSPC.Close",
"price": 104.01,
"rsi": 63.238,
"ret": 0.00067347 
},
{
 "date":    762,
"name": "GSPC.Close",
"price": 104.68,
"rsi": 63.683,
"ret": 0.0064417 
},
{
 "date":    763,
"name": "GSPC.Close",
"price": 104.64,
"rsi": 67.714,
"ret": -0.00038212 
},
{
 "date":    764,
"name": "GSPC.Close",
"price": 104.86,
"rsi": 67.234,
"ret": 0.0021024 
},
{
 "date":    767,
"name": "GSPC.Close",
"price": 104.54,
"rsi": 68.554,
"ret": -0.0030517 
},
{
 "date":    768,
"name": "GSPC.Close",
"price": 104.74,
"rsi": 64.485,
"ret": 0.0019131 
},
{
 "date":    769,
"name": "GSPC.Close",
"price": 105.55,
"rsi":  65.85,
"ret": 0.0077334 
},
{
 "date":    770,
"name": "GSPC.Close",
"price": 105.59,
"rsi":  70.75,
"ret": 0.00037897 
},
{
 "date":    771,
"name": "GSPC.Close",
"price": 105.08,
"rsi": 70.972,
"ret": -0.00483 
},
{
 "date":    774,
"name": "GSPC.Close",
"price": 104.59,
"rsi": 64.286,
"ret": -0.0046631 
},
{
 "date":    775,
"name": "GSPC.Close",
"price": 105.03,
"rsi": 58.577,
"ret": 0.0042069 
},
{
 "date":    776,
"name": "GSPC.Close",
"price": 105.62,
"rsi": 61.853,
"ret": 0.0056174 
},
{
 "date":    777,
"name": "GSPC.Close",
"price": 105.59,
"rsi": 65.763,
"ret": -0.00028404 
},
{
 "date":    778,
"name": "GSPC.Close",
"price": 105.28,
"rsi": 65.396,
"ret": -0.0029359 
},
{
 "date":    782,
"name": "GSPC.Close",
"price": 105.29,
"rsi": 61.572,
"ret": 9.4985e-05 
},
{
 "date":    783,
"name": "GSPC.Close",
"price": 105.38,
"rsi":  61.65,
"ret": 0.00085478 
},
{
 "date":    784,
"name": "GSPC.Close",
"price": 105.45,
"rsi": 62.389,
"ret": 0.00066426 
},
{
 "date":    785,
"name": "GSPC.Close",
"price": 106.18,
"rsi": 62.986,
"ret": 0.0069227 
},
{
 "date":    788,
"name": "GSPC.Close",
"price": 106.19,
"rsi":  68.59,
"ret": 9.418e-05 
},
{
 "date":    789,
"name": "GSPC.Close",
"price": 106.57,
"rsi":  68.66,
"ret": 0.0035785 
},
{
 "date":    790,
"name": "GSPC.Close",
"price": 107.35,
"rsi":  71.28,
"ret": 0.0073191 
},
{
 "date":    791,
"name": "GSPC.Close",
"price": 107.32,
"rsi": 75.758,
"ret": -0.00027946 
},
{
 "date":    792,
"name": "GSPC.Close",
"price": 107.94,
"rsi": 75.272,
"ret": 0.0057771 
},
{
 "date":    795,
"name": "GSPC.Close",
"price": 108.77,
"rsi": 78.363,
"ret": 0.0076895 
},
{
 "date":    796,
"name": "GSPC.Close",
"price": 108.87,
"rsi": 81.666,
"ret": 0.00091937 
},
{
 "date":    797,
"name": "GSPC.Close",
"price": 108.96,
"rsi": 82.022,
"ret": 0.00082667 
},
{
 "date":    798,
"name": "GSPC.Close",
"price": 108.94,
"rsi": 82.354,
"ret": -0.00018355 
},
{
 "date":    799,
"name": "GSPC.Close",
"price": 108.38,
"rsi": 81.992,
"ret": -0.0051404 
},
{
 "date":    802,
"name": "GSPC.Close",
"price": 107.33,
"rsi": 72.382,
"ret": -0.0096881 
},
{
 "date":    803,
"name": "GSPC.Close",
"price": 107.61,
"rsi":  58.53,
"ret": 0.0026088 
},
{
 "date":    804,
"name": "GSPC.Close",
"price": 107.75,
"rsi": 60.691,
"ret": 0.001301 
},
{
 "date":    805,
"name": "GSPC.Close",
"price":  107.5,
"rsi": 61.763,
"ret": -0.0023202 
},
{
 "date":    806,
"name": "GSPC.Close",
"price": 107.92,
"rsi": 58.684,
"ret": 0.003907 
},
{
 "date":    809,
"name": "GSPC.Close",
"price": 107.59,
"rsi": 62.102,
"ret": -0.0030578 
},
{
 "date":    810,
"name": "GSPC.Close",
"price": 106.69,
"rsi": 58.039,
"ret": -0.0083651 
},
{
 "date":    811,
"name": "GSPC.Close",
"price": 106.84,
"rsi": 48.684,
"ret": 0.0014059 
},
{
 "date":    812,
"name": "GSPC.Close",
"price": 107.75,
"rsi": 50.127,
"ret": 0.0085174 
},
{
 "date":    813,
"name": "GSPC.Close",
"price": 107.52,
"rsi": 57.867,
"ret": -0.0021346 
},
{
 "date":    816,
"name": "GSPC.Close",
"price":  107.3,
"rsi": 55.521,
"ret": -0.0020461 
},
{
 "date":    817,
"name": "GSPC.Close",
"price": 107.17,
"rsi": 53.296,
"ret": -0.0012116 
},
{
 "date":    818,
"name": "GSPC.Close",
"price": 106.49,
"rsi": 51.971,
"ret": -0.0063451 
},
{
 "date":    819,
"name": "GSPC.Close",
"price":  107.2,
"rsi": 45.585,
"ret": 0.0066673 
},
{
 "date":    823,
"name": "GSPC.Close",
"price": 107.48,
"rsi":  52.19,
"ret": 0.0026119 
},
{
 "date":    824,
"name": "GSPC.Close",
"price": 108.12,
"rsi": 54.535,
"ret": 0.0059546 
},
{
 "date":    825,
"name": "GSPC.Close",
"price":    109,
"rsi": 59.431,
"ret": 0.0081391 
},
{
 "date":    826,
"name": "GSPC.Close",
"price": 109.53,
"rsi":  65.01,
"ret": 0.0048624 
},
{
 "date":    827,
"name": "GSPC.Close",
"price": 109.62,
"rsi": 67.876,
"ret": 0.00082169 
},
{
 "date":    830,
"name": "GSPC.Close",
"price": 109.45,
"rsi":  68.35,
"ret": -0.0015508 
},
{
 "date":    831,
"name": "GSPC.Close",
"price": 109.76,
"rsi": 66.358,
"ret": 0.0028323 
},
{
 "date":    832,
"name": "GSPC.Close",
"price": 110.18,
"rsi": 68.179,
"ret": 0.0038265 
},
{
 "date":    833,
"name": "GSPC.Close",
"price": 109.91,
"rsi": 70.508,
"ret": -0.0024505 
},
{
 "date":    834,
"name": "GSPC.Close",
"price": 109.84,
"rsi": 67.108,
"ret": -0.00063688 
},
{
 "date":    837,
"name": "GSPC.Close",
"price": 109.51,
"rsi": 66.216,
"ret": -0.0030044 
},
{
 "date":    838,
"name": "GSPC.Close",
"price": 109.77,
"rsi": 62.031,
"ret": 0.0023742 
},
{
 "date":    839,
"name": "GSPC.Close",
"price":  109.2,
"rsi": 63.964,
"ret": -0.0051927 
},
{
 "date":    840,
"name": "GSPC.Close",
"price": 109.04,
"rsi": 57.103,
"ret": -0.0014652 
},
{
 "date":    841,
"name": "GSPC.Close",
"price": 108.89,
"rsi": 55.309,
"ret": -0.0013756 
},
{
 "date":    844,
"name": "GSPC.Close",
"price": 108.19,
"rsi": 53.609,
"ret": -0.0064285 
},
{
 "date":    845,
"name": "GSPC.Close",
"price": 107.12,
"rsi": 46.437,
"ret": -0.00989 
},
{
 "date":    846,
"name": "GSPC.Close",
"price": 106.89,
"rsi": 38.055,
"ret": -0.0021471 
},
{
 "date":    847,
"name": "GSPC.Close",
"price": 107.05,
"rsi": 36.529,
"ret": 0.0014969 
},
{
 "date":    848,
"name": "GSPC.Close",
"price": 107.67,
"rsi":  38.38,
"ret": 0.0057917 
},
{
 "date":    851,
"name": "GSPC.Close",
"price": 106.69,
"rsi": 45.067,
"ret": -0.0091019 
},
{
 "date":    852,
"name": "GSPC.Close",
"price": 106.08,
"rsi":  38.04,
"ret": -0.0057175 
},
{
 "date":    853,
"name": "GSPC.Close",
"price": 105.99,
"rsi":  34.44,
"ret": -0.00084842 
},
{
 "date":    854,
"name": "GSPC.Close",
"price": 106.25,
"rsi":  33.93,
"ret": 0.0024531 
},
{
 "date":    855,
"name": "GSPC.Close",
"price": 106.63,
"rsi": 36.841,
"ret": 0.0035765 
},
{
 "date":    858,
"name": "GSPC.Close",
"price": 106.14,
"rsi": 40.936,
"ret": -0.0045953 
},
{
 "date":    859,
"name": "GSPC.Close",
"price": 104.74,
"rsi": 37.555,
"ret": -0.01319 
},
{
 "date":    860,
"name": "GSPC.Close",
"price": 105.42,
"rsi": 29.944,
"ret": 0.0064923 
},
{
 "date":    861,
"name": "GSPC.Close",
"price": 105.77,
"rsi": 36.659,
"ret": 0.0033201 
},
{
 "date":    862,
"name": "GSPC.Close",
"price": 106.38,
"rsi": 39.854,
"ret": 0.0057672 
},
{
 "date":    865,
"name": "GSPC.Close",
"price": 106.86,
"rsi": 45.056,
"ret": 0.0045121 
},
{
 "date":    866,
"name": "GSPC.Close",
"price": 106.66,
"rsi": 48.809,
"ret": -0.0018716 
},
{
 "date":    867,
"name": "GSPC.Close",
"price": 106.89,
"rsi": 47.357,
"ret": 0.0021564 
},
{
 "date":    868,
"name": "GSPC.Close",
"price": 107.94,
"rsi": 49.227,
"ret": 0.0098232 
},
{
 "date":    869,
"name": "GSPC.Close",
"price": 108.98,
"rsi": 56.775,
"ret": 0.009635 
},
{
 "date":    872,
"name": "GSPC.Close",
"price": 109.69,
"rsi": 62.691,
"ret": 0.006515 
},
{
 "date":    873,
"name": "GSPC.Close",
"price": 109.78,
"rsi": 66.101,
"ret": 0.00082049 
},
{
 "date":    874,
"name": "GSPC.Close",
"price": 110.31,
"rsi": 66.519,
"ret": 0.0048278 
},
{
 "date":    875,
"name": "GSPC.Close",
"price": 110.46,
"rsi": 68.947,
"ret": 0.0013598 
},
{
 "date":    876,
"name": "GSPC.Close",
"price": 110.66,
"rsi": 69.618,
"ret": 0.0018106 
},
{
 "date":    880,
"name": "GSPC.Close",
"price": 110.35,
"rsi": 70.533,
"ret": -0.0028014 
},
{
 "date":    881,
"name": "GSPC.Close",
"price": 109.53,
"rsi": 67.158,
"ret": -0.0074309 
},
{
 "date":    882,
"name": "GSPC.Close",
"price": 109.69,
"rsi": 59.101,
"ret": 0.0014608 
},
{
 "date":    883,
"name": "GSPC.Close",
"price": 109.73,
"rsi": 60.106,
"ret": 0.00036466 
},
{
 "date":    886,
"name": "GSPC.Close",
"price": 108.82,
"rsi": 60.369,
"ret": -0.0082931 
},
{
 "date":    887,
"name": "GSPC.Close",
"price": 108.21,
"rsi": 51.991,
"ret": -0.0056056 
},
{
 "date":    888,
"name": "GSPC.Close",
"price": 107.65,
"rsi": 47.257,
"ret": -0.0051751 
},
{
 "date":    889,
"name": "GSPC.Close",
"price": 107.28,
"rsi": 43.354,
"ret": -0.0034371 
},
{
 "date":    890,
"name": "GSPC.Close",
"price": 106.86,
"rsi": 40.948,
"ret": -0.003915 
},
{
 "date":    893,
"name": "GSPC.Close",
"price": 107.01,
"rsi": 38.346,
"ret": 0.0014037 
},
{
 "date":    894,
"name": "GSPC.Close",
"price": 107.55,
"rsi": 39.817,
"ret": 0.0050463 
},
{
 "date":    895,
"name": "GSPC.Close",
"price": 108.39,
"rsi": 44.912,
"ret": 0.0078103 
},
{
 "date":    896,
"name": "GSPC.Close",
"price": 108.44,
"rsi": 51.754,
"ret": 0.0004613 
},
{
 "date":    897,
"name": "GSPC.Close",
"price": 108.36,
"rsi": 52.135,
"ret": -0.00073774 
},
{
 "date":    900,
"name": "GSPC.Close",
"price": 108.11,
"rsi": 51.435,
"ret": -0.0023071 
},
{
 "date":    901,
"name": "GSPC.Close",
"price": 108.56,
"rsi": 49.211,
"ret": 0.0041624 
},
{
 "date":    902,
"name": "GSPC.Close",
"price": 108.79,
"rsi": 53.139,
"ret": 0.0021186 
},
{
 "date":    903,
"name": "GSPC.Close",
"price": 108.68,
"rsi": 55.052,
"ret": -0.0010111 
},
{
 "date":    904,
"name": "GSPC.Close",
"price": 108.27,
"rsi": 53.918,
"ret": -0.0037725 
},
{
 "date":    907,
"name": "GSPC.Close",
"price": 107.48,
"rsi": 49.801,
"ret": -0.0072966 
},
{
 "date":    908,
"name": "GSPC.Close",
"price": 107.37,
"rsi":  42.99,
"ret": -0.0010234 
},
{
 "date":    909,
"name": "GSPC.Close",
"price": 107.02,
"rsi": 42.126,
"ret": -0.0032598 
},
{
 "date":    910,
"name": "GSPC.Close",
"price": 106.82,
"rsi": 39.412,
"ret": -0.0018688 
},
{
 "date":    911,
"name": "GSPC.Close",
"price": 107.14,
"rsi": 37.909,
"ret": 0.0029957 
},
{
 "date":    914,
"name": "GSPC.Close",
"price": 107.49,
"rsi": 41.737,
"ret": 0.0032668 
},
{
 "date":    916,
"name": "GSPC.Close",
"price":  108.1,
"rsi": 45.682,
"ret": 0.0056749 
},
{
 "date":    917,
"name": "GSPC.Close",
"price": 109.04,
"rsi": 51.807,
"ret": 0.0086957 
},
{
 "date":    918,
"name": "GSPC.Close",
"price": 108.69,
"rsi": 59.403,
"ret": -0.0032098 
},
{
 "date":    921,
"name": "GSPC.Close",
"price": 108.11,
"rsi": 55.872,
"ret": -0.0053363 
},
{
 "date":    922,
"name": "GSPC.Close",
"price": 107.32,
"rsi": 50.513,
"ret": -0.0073074 
},
{
 "date":    923,
"name": "GSPC.Close",
"price": 106.89,
"rsi": 44.283,
"ret": -0.0040067 
},
{
 "date":    924,
"name": "GSPC.Close",
"price": 106.28,
"rsi": 41.297,
"ret": -0.0057068 
},
{
 "date":    925,
"name": "GSPC.Close",
"price":  106.8,
"rsi": 37.441,
"ret": 0.0048927 
},
{
 "date":    928,
"name": "GSPC.Close",
"price": 105.88,
"rsi":  42.38,
"ret": -0.0086142 
},
{
 "date":    929,
"name": "GSPC.Close",
"price": 105.83,
"rsi": 36.838,
"ret": -0.00047223 
},
{
 "date":    930,
"name": "GSPC.Close",
"price": 106.14,
"rsi": 36.558,
"ret": 0.0029292 
},
{
 "date":    931,
"name": "GSPC.Close",
"price": 105.81,
"rsi": 39.621,
"ret": -0.0031091 
},
{
 "date":    932,
"name": "GSPC.Close",
"price": 106.66,
"rsi": 37.543,
"ret": 0.0080333 
},
{
 "date":    935,
"name": "GSPC.Close",
"price": 107.92,
"rsi": 45.474,
"ret": 0.011813 
},
{
 "date":    936,
"name": "GSPC.Close",
"price":  107.6,
"rsi": 54.664,
"ret": -0.0029652 
},
{
 "date":    937,
"name": "GSPC.Close",
"price": 107.53,
"rsi": 52.255,
"ret": -0.00065056 
},
{
 "date":    938,
"name": "GSPC.Close",
"price": 107.28,
"rsi": 51.718,
"ret": -0.0023249 
},
{
 "date":    939,
"name": "GSPC.Close",
"price": 107.38,
"rsi": 49.752,
"ret": 0.00093214 
},
{
 "date":    942,
"name": "GSPC.Close",
"price": 107.39,
"rsi": 50.561,
"ret": 9.3127e-05 
},
{
 "date":    943,
"name": "GSPC.Close",
"price":  108.4,
"rsi": 50.647,
"ret": 0.009405 
},
{
 "date":    944,
"name": "GSPC.Close",
"price": 109.29,
"rsi": 58.471,
"ret": 0.0082103 
},
{
 "date":    945,
"name": "GSPC.Close",
"price": 110.14,
"rsi": 63.902,
"ret": 0.0077775 
},
{
 "date":    946,
"name": "GSPC.Close",
"price": 110.43,
"rsi": 68.181,
"ret": 0.002633 
},
{
 "date":    949,
"name": "GSPC.Close",
"price": 110.61,
"rsi": 69.509,
"ret": 0.00163 
},
{
 "date":    950,
"name": "GSPC.Close",
"price": 110.69,
"rsi": 70.337,
"ret": 0.00072326 
},
{
 "date":    951,
"name": "GSPC.Close",
"price": 110.86,
"rsi": 70.717,
"ret": 0.0015358 
},
{
 "date":    952,
"name": "GSPC.Close",
"price": 111.05,
"rsi": 71.552,
"ret": 0.0017139 
},
{
 "date":    953,
"name": "GSPC.Close",
"price": 111.95,
"rsi": 72.496,
"ret": 0.0081045 
},
{
 "date":    956,
"name": "GSPC.Close",
"price": 112.55,
"rsi": 76.477,
"ret": 0.0053595 
},
{
 "date":    957,
"name": "GSPC.Close",
"price": 112.06,
"rsi": 78.692,
"ret": -0.0043536 
},
{
 "date":    958,
"name": "GSPC.Close",
"price": 111.66,
"rsi": 72.675,
"ret": -0.0035695 
},
{
 "date":    959,
"name": "GSPC.Close",
"price": 111.34,
"rsi": 68.097,
"ret": -0.0028658 
},
{
 "date":    960,
"name": "GSPC.Close",
"price": 111.76,
"rsi": 64.592,
"ret": 0.0037722 
},
{
 "date":    963,
"name": "GSPC.Close",
"price": 111.72,
"rsi": 66.993,
"ret": -0.00035791 
},
{
 "date":    964,
"name": "GSPC.Close",
"price": 112.41,
"rsi":  66.53,
"ret": 0.0061762 
},
{
 "date":    965,
"name": "GSPC.Close",
"price": 112.26,
"rsi": 70.337,
"ret": -0.0013344 
},
{
 "date":    966,
"name": "GSPC.Close",
"price": 111.02,
"rsi": 68.513,
"ret": -0.011046 
},
{
 "date":    967,
"name": "GSPC.Close",
"price": 110.67,
"rsi": 55.661,
"ret": -0.0031526 
},
{
 "date":    970,
"name": "GSPC.Close",
"price": 110.23,
"rsi": 52.658,
"ret": -0.0039758 
},
{
 "date":    971,
"name": "GSPC.Close",
"price": 110.41,
"rsi": 49.074,
"ret": 0.0016329 
},
{
 "date":    972,
"name": "GSPC.Close",
"price": 110.57,
"rsi": 50.557,
"ret": 0.0014491 
},
{
 "date":    973,
"name": "GSPC.Close",
"price": 111.09,
"rsi": 51.897,
"ret": 0.0047029 
},
{
 "date":    974,
"name": "GSPC.Close",
"price": 111.51,
"rsi": 56.066,
"ret": 0.0037807 
},
{
 "date":    978,
"name": "GSPC.Close",
"price": 111.23,
"rsi": 59.146,
"ret": -0.002511 
},
{
 "date":    979,
"name": "GSPC.Close",
"price": 110.55,
"rsi": 56.312,
"ret": -0.0061135 
},
{
 "date":    980,
"name": "GSPC.Close",
"price": 110.29,
"rsi": 50.041,
"ret": -0.0023519 
},
{
 "date":    981,
"name": "GSPC.Close",
"price": 110.15,
"rsi": 47.847,
"ret": -0.0012694 
},
{
 "date":    984,
"name": "GSPC.Close",
"price": 109.51,
"rsi":  46.66,
"ret": -0.0058103 
},
{
 "date":    985,
"name": "GSPC.Close",
"price": 108.47,
"rsi": 41.584,
"ret": -0.0094968 
},
{
 "date":    986,
"name": "GSPC.Close",
"price":  108.9,
"rsi": 34.933,
"ret": 0.0039642 
},
{
 "date":    987,
"name": "GSPC.Close",
"price": 108.93,
"rsi": 39.259,
"ret": 0.00027548 
},
{
 "date":    988,
"name": "GSPC.Close",
"price": 108.81,
"rsi": 39.561,
"ret": -0.0011016 
},
{
 "date":    991,
"name": "GSPC.Close",
"price": 108.61,
"rsi": 38.732,
"ret": -0.0018381 
},
{
 "date":    992,
"name": "GSPC.Close",
"price": 108.55,
"rsi": 37.327,
"ret": -0.00055244 
},
{
 "date":    993,
"name": "GSPC.Close",
"price":  108.6,
"rsi": 36.895,
"ret": 0.00046062 
},
{
 "date":    994,
"name": "GSPC.Close",
"price": 108.43,
"rsi": 37.544,
"ret": -0.0015654 
},
{
 "date":    995,
"name": "GSPC.Close",
"price": 108.52,
"rsi": 36.182,
"ret": 0.00083003 
},
{
 "date":    998,
"name": "GSPC.Close",
"price": 108.05,
"rsi": 37.475,
"ret": -0.004331 
},
{
 "date":    999,
"name": "GSPC.Close",
"price": 108.12,
"rsi":  33.64,
"ret": 0.00064785 
},
{
 "date":   1000,
"name": "GSPC.Close",
"price": 109.66,
"rsi": 34.712,
"ret": 0.014243 
},
{
 "date":   1001,
"name": "GSPC.Close",
"price": 110.35,
"rsi": 52.778,
"ret": 0.0062922 
},
{
 "date":   1002,
"name": "GSPC.Close",
"price": 110.55,
"rsi": 58.341,
"ret": 0.0018124 
},
{
 "date":   1005,
"name": "GSPC.Close",
"price": 110.16,
"rsi": 59.818,
"ret": -0.0035278 
},
{
 "date":   1006,
"name": "GSPC.Close",
"price":  110.3,
"rsi": 55.672,
"ret": 0.0012709 
},
{
 "date":   1007,
"name": "GSPC.Close",
"price": 110.09,
"rsi": 56.829,
"ret": -0.0019039 
},
{
 "date":   1008,
"name": "GSPC.Close",
"price": 108.89,
"rsi":  54.53,
"ret": -0.0109 
},
{
 "date":   1009,
"name": "GSPC.Close",
"price": 109.62,
"rsi": 43.661,
"ret": 0.006704 
},
{
 "date":   1012,
"name": "GSPC.Close",
"price":  109.9,
"rsi": 50.168,
"ret": 0.0025543 
},
{
 "date":   1013,
"name": "GSPC.Close",
"price": 109.99,
"rsi": 52.437,
"ret": 0.00081893 
},
{
 "date":   1014,
"name": "GSPC.Close",
"price":  109.5,
"rsi": 53.175,
"ret": -0.004455 
},
{
 "date":   1015,
"name": "GSPC.Close",
"price":  108.6,
"rsi": 48.741,
"ret": -0.0082192 
},
{
 "date":   1016,
"name": "GSPC.Close",
"price": 107.92,
"rsi": 41.839,
"ret": -0.0062615 
},
{
 "date":   1019,
"name": "GSPC.Close",
"price": 106.77,
"rsi": 37.516,
"ret": -0.010656 
},
{
 "date":   1020,
"name": "GSPC.Close",
"price":  107.5,
"rsi": 31.575,
"ret": 0.0068371 
},
{
 "date":   1021,
"name": "GSPC.Close",
"price": 108.19,
"rsi": 38.259,
"ret": 0.0064186 
},
{
 "date":   1022,
"name": "GSPC.Close",
"price": 108.05,
"rsi": 43.843,
"ret": -0.001294 
},
{
 "date":   1023,
"name": "GSPC.Close",
"price": 109.24,
"rsi": 42.994,
"ret": 0.011013 
},
{
 "date":   1026,
"name": "GSPC.Close",
"price": 110.35,
"rsi": 51.582,
"ret": 0.010161 
},
{
 "date":   1027,
"name": "GSPC.Close",
"price": 110.81,
"rsi": 57.947,
"ret": 0.0041686 
},
{
 "date":   1028,
"name": "GSPC.Close",
"price": 110.72,
"rsi": 60.277,
"ret": -0.0008122 
},
{
 "date":   1029,
"name": "GSPC.Close",
"price": 110.99,
"rsi": 59.582,
"ret": 0.0024386 
},
{
 "date":   1030,
"name": "GSPC.Close",
"price": 110.62,
"rsi": 61.035,
"ret": -0.0033336 
},
{
 "date":   1033,
"name": "GSPC.Close",
"price": 110.59,
"rsi":  57.96,
"ret": -0.0002712 
},
{
 "date":   1034,
"name": "GSPC.Close",
"price": 111.58,
"rsi": 57.706,
"ret": 0.008952 
},
{
 "date":   1035,
"name": "GSPC.Close",
"price": 112.67,
"rsi": 63.402,
"ret": 0.0097688 
},
{
 "date":   1036,
"name": "GSPC.Close",
"price": 113.23,
"rsi": 68.442,
"ret": 0.0049703 
},
{
 "date":   1037,
"name": "GSPC.Close",
"price": 114.22,
"rsi": 70.676,
"ret": 0.0087433 
},
{
 "date":   1040,
"name": "GSPC.Close",
"price": 113.98,
"rsi": 74.159,
"ret": -0.0021012 
},
{
 "date":   1042,
"name": "GSPC.Close",
"price": 113.35,
"rsi": 71.928,
"ret": -0.0055273 
},
{
 "date":   1043,
"name": "GSPC.Close",
"price":  113.5,
"rsi": 66.292,
"ret": 0.0013233 
},
{
 "date":   1044,
"name": "GSPC.Close",
"price": 113.73,
"rsi": 66.956,
"ret": 0.0020264 
},
{
 "date":   1047,
"name": "GSPC.Close",
"price":  113.9,
"rsi": 67.997,
"ret": 0.0014948 
},
{
 "date":   1048,
"name": "GSPC.Close",
"price": 114.95,
"rsi":  68.78,
"ret": 0.0092186 
},
{
 "date":   1049,
"name": "GSPC.Close",
"price":  114.5,
"rsi": 73.149,
"ret": -0.0039147 
},
{
 "date":   1050,
"name": "GSPC.Close",
"price": 115.13,
"rsi": 68.711,
"ret": 0.0055022 
},
{
 "date":   1051,
"name": "GSPC.Close",
"price": 115.49,
"rsi": 71.333,
"ret": 0.0031269 
},
{
 "date":   1054,
"name": "GSPC.Close",
"price": 115.53,
"rsi": 72.739,
"ret": 0.00034635 
},
{
 "date":   1055,
"name": "GSPC.Close",
"price": 116.21,
"rsi": 72.898,
"ret": 0.0058859 
},
{
 "date":   1056,
"name": "GSPC.Close",
"price":  116.9,
"rsi": 75.513,
"ret": 0.0059375 
},
{
 "date":   1058,
"name": "GSPC.Close",
"price": 117.27,
"rsi": 77.849,
"ret": 0.0031651 
},
{
 "date":   1061,
"name": "GSPC.Close",
"price": 116.72,
"rsi": 79.005,
"ret": -0.00469 
},
{
 "date":   1062,
"name": "GSPC.Close",
"price": 116.47,
"rsi": 72.912,
"ret": -0.0021419 
},
{
 "date":   1063,
"name": "GSPC.Close",
"price": 116.52,
"rsi": 70.259,
"ret": 0.0004293 
},
{
 "date":   1064,
"name": "GSPC.Close",
"price": 116.67,
"rsi":  70.49,
"ret": 0.0012873 
},
{
 "date":   1065,
"name": "GSPC.Close",
"price": 117.38,
"rsi": 71.213,
"ret": 0.0060855 
},
{
 "date":   1068,
"name": "GSPC.Close",
"price": 117.77,
"rsi":  74.41,
"ret": 0.0033225 
},
{
 "date":   1069,
"name": "GSPC.Close",
"price": 117.58,
"rsi": 75.987,
"ret": -0.0016133 
},
{
 "date":   1070,
"name": "GSPC.Close",
"price": 118.01,
"rsi": 73.607,
"ret": 0.0036571 
},
{
 "date":   1071,
"name": "GSPC.Close",
"price":  118.6,
"rsi": 75.479,
"ret": 0.0049996 
},
{
 "date":   1072,
"name": "GSPC.Close",
"price": 118.86,
"rsi": 77.805,
"ret": 0.0021922 
},
{
 "date":   1075,
"name": "GSPC.Close",
"price": 119.12,
"rsi": 78.761,
"ret": 0.0021874 
},
{
 "date":   1076,
"name": "GSPC.Close",
"price": 118.66,
"rsi": 79.703,
"ret": -0.0038617 
},
{
 "date":   1077,
"name": "GSPC.Close",
"price": 118.56,
"rsi": 73.494,
"ret": -0.00084274 
},
{
 "date":   1078,
"name": "GSPC.Close",
"price": 118.24,
"rsi": 72.178,
"ret": -0.0026991 
},
{
 "date":   1079,
"name": "GSPC.Close",
"price": 118.26,
"rsi": 67.982,
"ret": 0.00016915 
},
{
 "date":   1082,
"name": "GSPC.Close",
"price":  116.9,
"rsi": 68.106,
"ret": -0.0115 
},
{
 "date":   1083,
"name": "GSPC.Close",
"price": 116.34,
"rsi": 52.983,
"ret": -0.0047904 
},
{
 "date":   1084,
"name": "GSPC.Close",
"price": 115.95,
"rsi": 48.234,
"ret": -0.0033522 
},
{
 "date":   1085,
"name": "GSPC.Close",
"price": 115.11,
"rsi": 45.195,
"ret": -0.0072445 
},
{
 "date":   1086,
"name": "GSPC.Close",
"price": 115.83,
"rsi": 39.433,
"ret": 0.0062549 
},
{
 "date":   1090,
"name": "GSPC.Close",
"price":  116.3,
"rsi":  45.81,
"ret": 0.0040577 
},
{
 "date":   1091,
"name": "GSPC.Close",
"price": 116.93,
"rsi": 49.545,
"ret": 0.005417 
},
{
 "date":   1093,
"name": "GSPC.Close",
"price": 118.05,
"rsi":  54.11,
"ret": 0.0095784 
},
{
 "date":   1097,
"name": "GSPC.Close",
"price":  119.1,
"rsi": 60.886,
"ret": 0.0088945 
},
{
 "date":   1098,
"name": "GSPC.Close",
"price": 119.57,
"rsi": 65.961,
"ret": 0.0039463 
},
{
 "date":   1099,
"name": "GSPC.Close",
"price":  119.4,
"rsi": 67.964,
"ret": -0.0014218 
},
{
 "date":   1100,
"name": "GSPC.Close",
"price": 119.87,
"rsi": 66.441,
"ret": 0.0039363 
},
{
 "date":   1103,
"name": "GSPC.Close",
"price": 119.85,
"rsi":  68.54,
"ret": -0.00016685 
},
{
 "date":   1104,
"name": "GSPC.Close",
"price": 119.73,
"rsi": 68.344,
"ret": -0.0010013 
},
{
 "date":   1105,
"name": "GSPC.Close",
"price": 119.43,
"rsi": 67.105,
"ret": -0.0025056 
},
{
 "date":   1106,
"name": "GSPC.Close",
"price": 120.24,
"rsi": 63.981,
"ret": 0.0067822 
},
{
 "date":   1107,
"name": "GSPC.Close",
"price":  119.3,
"rsi": 68.275,
"ret": -0.0078177 
},
{
 "date":   1110,
"name": "GSPC.Close",
"price": 118.44,
"rsi": 59.421,
"ret": -0.0072087 
},
{
 "date":   1111,
"name": "GSPC.Close",
"price": 118.14,
"rsi": 52.689,
"ret": -0.0025329 
},
{
 "date":   1112,
"name": "GSPC.Close",
"price": 118.68,
"rsi": 50.538,
"ret": 0.0045708 
},
{
 "date":   1113,
"name": "GSPC.Close",
"price": 118.85,
"rsi": 54.165,
"ret": 0.0014324 
},
{
 "date":   1114,
"name": "GSPC.Close",
"price": 118.78,
"rsi": 55.277,
"ret": -0.00058898 
},
{
 "date":   1117,
"name": "GSPC.Close",
"price": 118.21,
"rsi": 54.689,
"ret": -0.0047988 
},
{
 "date":   1118,
"name": "GSPC.Close",
"price": 118.22,
"rsi": 50.021,
"ret": 8.4595e-05 
},
{
 "date":   1119,
"name": "GSPC.Close",
"price": 116.73,
"rsi": 50.101,
"ret": -0.012604 
},
{
 "date":   1121,
"name": "GSPC.Close",
"price": 116.45,
"rsi": 39.814,
"ret": -0.0023987 
},
{
 "date":   1124,
"name": "GSPC.Close",
"price": 116.01,
"rsi": 38.226,
"ret": -0.0037784 
},
{
 "date":   1125,
"name": "GSPC.Close",
"price": 115.83,
"rsi": 35.808,
"ret": -0.0015516 
},
{
 "date":   1126,
"name": "GSPC.Close",
"price": 116.03,
"rsi": 34.837,
"ret": 0.0017267 
},
{
 "date":   1127,
"name": "GSPC.Close",
"price": 114.76,
"rsi": 36.885,
"ret": -0.010945 
},
{
 "date":   1128,
"name": "GSPC.Close",
"price": 114.35,
"rsi": 30.362,
"ret": -0.0035727 
},
{
 "date":   1131,
"name": "GSPC.Close",
"price": 114.23,
"rsi": 28.603,
"ret": -0.0010494 
},
{
 "date":   1132,
"name": "GSPC.Close",
"price": 114.45,
"rsi":  28.09,
"ret": 0.0019259 
},
{
 "date":   1133,
"name": "GSPC.Close",
"price": 113.66,
"rsi": 30.549,
"ret": -0.0069026 
},
{
 "date":   1134,
"name": "GSPC.Close",
"price": 113.16,
"rsi": 26.981,
"ret": -0.0043991 
},
{
 "date":   1135,
"name": "GSPC.Close",
"price": 114.68,
"rsi": 24.992,
"ret": 0.013432 
},
{
 "date":   1138,
"name": "GSPC.Close",
"price": 116.06,
"rsi": 39.576,
"ret": 0.012033 
},
{
 "date":   1139,
"name": "GSPC.Close",
"price": 116.78,
"rsi": 49.229,
"ret": 0.0062037 
},
{
 "date":   1140,
"name": "GSPC.Close",
"price":  115.1,
"rsi":  53.41,
"ret": -0.014386 
},
{
 "date":   1141,
"name": "GSPC.Close",
"price": 114.45,
"rsi": 44.252,
"ret": -0.0056473 
},
{
 "date":   1142,
"name": "GSPC.Close",
"price": 114.98,
"rsi": 41.301,
"ret": 0.0046308 
},
{
 "date":   1146,
"name": "GSPC.Close",
"price":  115.4,
"rsi": 44.548,
"ret": 0.0036528 
},
{
 "date":   1147,
"name": "GSPC.Close",
"price": 114.69,
"rsi": 47.048,
"ret": -0.0061525 
},
{
 "date":   1148,
"name": "GSPC.Close",
"price": 114.44,
"rsi": 43.479,
"ret": -0.0021798 
},
{
 "date":   1149,
"name": "GSPC.Close",
"price": 113.16,
"rsi": 42.264,
"ret": -0.011185 
},
{
 "date":   1152,
"name": "GSPC.Close",
"price": 112.19,
"rsi": 36.619,
"ret": -0.0085719 
},
{
 "date":   1153,
"name": "GSPC.Close",
"price":  110.9,
"rsi":  33.02,
"ret": -0.011498 
},
{
 "date":   1154,
"name": "GSPC.Close",
"price": 111.68,
"rsi": 28.946,
"ret": 0.0070334 
},
{
 "date":   1155,
"name": "GSPC.Close",
"price": 111.05,
"rsi":  34.23,
"ret": -0.0056411 
},
{
 "date":   1156,
"name": "GSPC.Close",
"price": 112.28,
"rsi": 32.151,
"ret": 0.011076 
},
{
 "date":   1159,
"name": "GSPC.Close",
"price": 112.68,
"rsi": 39.837,
"ret": 0.0035625 
},
{
 "date":   1160,
"name": "GSPC.Close",
"price":  114.1,
"rsi": 42.132,
"ret": 0.012602 
},
{
 "date":   1161,
"name": "GSPC.Close",
"price": 114.45,
"rsi":   49.5,
"ret": 0.0030675 
},
{
 "date":   1162,
"name": "GSPC.Close",
"price": 114.23,
"rsi":  51.15,
"ret": -0.0019222 
},
{
 "date":   1163,
"name": "GSPC.Close",
"price": 113.79,
"rsi": 50.043,
"ret": -0.0038519 
},
{
 "date":   1166,
"name": "GSPC.Close",
"price": 113.86,
"rsi": 47.814,
"ret": 0.00061517 
},
{
 "date":   1167,
"name": "GSPC.Close",
"price": 114.48,
"rsi": 48.209,
"ret": 0.0054453 
},
{
 "date":   1168,
"name": "GSPC.Close",
"price": 114.98,
"rsi": 51.699,
"ret": 0.0043676 
},
{
 "date":   1169,
"name": "GSPC.Close",
"price": 114.12,
"rsi": 54.369,
"ret": -0.0074796 
},
{
 "date":   1170,
"name": "GSPC.Close",
"price": 113.54,
"rsi": 49.319,
"ret": -0.0050824 
},
{
 "date":   1173,
"name": "GSPC.Close",
"price": 112.17,
"rsi": 46.201,
"ret": -0.012066 
},
{
 "date":   1174,
"name": "GSPC.Close",
"price": 111.95,
"rsi": 39.802,
"ret": -0.0019613 
},
{
 "date":   1175,
"name": "GSPC.Close",
"price": 110.49,
"rsi": 38.871,
"ret": -0.013042 
},
{
 "date":   1176,
"name": "GSPC.Close",
"price": 108.84,
"rsi": 33.303,
"ret": -0.014933 
},
{
 "date":   1177,
"name": "GSPC.Close",
"price": 108.88,
"rsi": 28.359,
"ret": 0.00036751 
},
{
 "date":   1180,
"name": "GSPC.Close",
"price": 109.84,
"rsi": 28.636,
"ret": 0.008817 
},
{
 "date":   1181,
"name": "GSPC.Close",
"price": 111.56,
"rsi": 35.111,
"ret": 0.015659 
},
{
 "date":   1182,
"name": "GSPC.Close",
"price": 111.62,
"rsi": 44.778,
"ret": 0.00053783 
},
{
 "date":   1183,
"name": "GSPC.Close",
"price": 112.71,
"rsi": 45.085,
"ret": 0.0097653 
},
{
 "date":   1184,
"name": "GSPC.Close",
"price": 111.52,
"rsi": 50.478,
"ret": -0.010558 
},
{
 "date":   1187,
"name": "GSPC.Close",
"price": 110.18,
"rsi": 45.253,
"ret": -0.012016 
},
{
 "date":   1188,
"name": "GSPC.Close",
"price": 109.24,
"rsi": 40.207,
"ret": -0.0085315 
},
{
 "date":   1189,
"name": "GSPC.Close",
"price": 108.77,
"rsi": 37.083,
"ret": -0.0043025 
},
{
 "date":   1190,
"name": "GSPC.Close",
"price": 108.52,
"rsi": 35.594,
"ret": -0.0022984 
},
{
 "date":   1191,
"name": "GSPC.Close",
"price": 109.28,
"rsi": 34.793,
"ret": 0.0070033 
},
{
 "date":   1194,
"name": "GSPC.Close",
"price": 110.86,
"rsi": 39.264,
"ret": 0.014458 
},
{
 "date":   1195,
"name": "GSPC.Close",
"price": 112.21,
"rsi": 47.348,
"ret": 0.012178 
},
{
 "date":   1196,
"name": "GSPC.Close",
"price": 112.68,
"rsi": 53.092,
"ret": 0.0041886 
},
{
 "date":   1197,
"name": "GSPC.Close",
"price": 112.58,
"rsi": 54.935,
"ret": -0.00088747 
},
{
 "date":   1198,
"name": "GSPC.Close",
"price": 112.08,
"rsi": 54.445,
"ret": -0.0044413 
},
{
 "date":   1201,
"name": "GSPC.Close",
"price": 111.44,
"rsi": 51.949,
"ret": -0.0057102 
},
{
 "date":   1202,
"name": "GSPC.Close",
"price": 110.94,
"rsi": 48.861,
"ret": -0.0044867 
},
{
 "date":   1203,
"name": "GSPC.Close",
"price": 111.54,
"rsi": 46.533,
"ret": 0.0054083 
},
{
 "date":   1204,
"name": "GSPC.Close",
"price": 112.17,
"rsi": 49.634,
"ret": 0.0056482 
},
{
 "date":   1208,
"name": "GSPC.Close",
"price": 111.57,
"rsi": 52.733,
"ret": -0.005349 
},
{
 "date":   1209,
"name": "GSPC.Close",
"price": 109.99,
"rsi": 49.602,
"ret": -0.014162 
},
{
 "date":   1210,
"name": "GSPC.Close",
"price": 108.34,
"rsi": 42.455,
"ret": -0.015001 
},
{
 "date":   1211,
"name": "GSPC.Close",
"price": 108.89,
"rsi": 36.535,
"ret": 0.0050766 
},
{
 "date":   1212,
"name": "GSPC.Close",
"price": 107.23,
"rsi":  39.56,
"ret": -0.015245 
},
{
 "date":   1215,
"name": "GSPC.Close",
"price": 106.97,
"rsi": 34.253,
"ret": -0.0024247 
},
{
 "date":   1216,
"name": "GSPC.Close",
"price":  107.1,
"rsi": 33.495,
"ret": 0.0012153 
},
{
 "date":   1217,
"name": "GSPC.Close",
"price": 108.43,
"rsi": 34.278,
"ret": 0.012418 
},
{
 "date":   1218,
"name": "GSPC.Close",
"price": 110.22,
"rsi": 41.825,
"ret": 0.016508 
},
{
 "date":   1219,
"name": "GSPC.Close",
"price":    111,
"rsi": 50.127,
"ret": 0.0070768 
},
{
 "date":   1222,
"name": "GSPC.Close",
"price": 110.53,
"rsi": 53.257,
"ret": -0.0042342 
},
{
 "date":   1223,
"name": "GSPC.Close",
"price": 111.25,
"rsi": 51.173,
"ret": 0.0065141 
},
{
 "date":   1224,
"name": "GSPC.Close",
"price": 110.44,
"rsi": 54.134,
"ret": -0.0072809 
},
{
 "date":   1225,
"name": "GSPC.Close",
"price": 109.54,
"rsi": 50.429,
"ret": -0.0081492 
},
{
 "date":   1226,
"name": "GSPC.Close",
"price": 108.17,
"rsi": 46.611,
"ret": -0.012507 
},
{
 "date":   1229,
"name": "GSPC.Close",
"price":  105.9,
"rsi": 41.466,
"ret": -0.020985 
},
{
 "date":   1230,
"name": "GSPC.Close",
"price": 106.57,
"rsi": 34.642,
"ret": 0.0063267 
},
{
 "date":   1231,
"name": "GSPC.Close",
"price": 106.43,
"rsi":  37.89,
"ret": -0.0013137 
},
{
 "date":   1232,
"name": "GSPC.Close",
"price": 105.56,
"rsi": 37.471,
"ret": -0.0081744 
},
{
 "date":   1233,
"name": "GSPC.Close",
"price": 103.86,
"rsi": 34.888,
"ret": -0.016105 
},
{
 "date":   1236,
"name": "GSPC.Close",
"price": 102.73,
"rsi": 30.469,
"ret": -0.01088 
},
{
 "date":   1237,
"name": "GSPC.Close",
"price": 103.58,
"rsi": 27.936,
"ret": 0.0082741 
},
{
 "date":   1238,
"name": "GSPC.Close",
"price": 104.07,
"rsi": 32.483,
"ret": 0.0047306 
},
{
 "date":   1239,
"name": "GSPC.Close",
"price": 107.14,
"rsi": 35.028,
"ret": 0.029499 
},
{
 "date":   1240,
"name": "GSPC.Close",
"price": 107.94,
"rsi": 48.203,
"ret": 0.0074669 
},
{
 "date":   1244,
"name": "GSPC.Close",
"price": 107.51,
"rsi": 50.992,
"ret": -0.0039837 
},
{
 "date":   1245,
"name": "GSPC.Close",
"price": 105.91,
"rsi":  49.45,
"ret": -0.014882 
},
{
 "date":   1246,
"name": "GSPC.Close",
"price": 104.95,
"rsi": 44.108,
"ret": -0.0090643 
},
{
 "date":   1247,
"name": "GSPC.Close",
"price": 103.93,
"rsi":  41.23,
"ret": -0.0097189 
},
{
 "date":   1250,
"name": "GSPC.Close",
"price": 102.97,
"rsi": 38.366,
"ret": -0.009237 
},
{
 "date":   1251,
"name": "GSPC.Close",
"price": 104.62,
"rsi": 35.842,
"ret": 0.016024 
},
{
 "date":   1252,
"name": "GSPC.Close",
"price": 104.31,
"rsi": 42.806,
"ret": -0.0029631 
},
{
 "date":   1253,
"name": "GSPC.Close",
"price": 105.84,
"rsi": 41.886,
"ret": 0.014668 
},
{
 "date":   1254,
"name": "GSPC.Close",
"price": 107.03,
"rsi": 47.844,
"ret": 0.011243 
},
{
 "date":   1257,
"name": "GSPC.Close",
"price":  106.7,
"rsi": 51.968,
"ret": -0.0030832 
},
{
 "date":   1258,
"name": "GSPC.Close",
"price": 108.29,
"rsi": 50.769,
"ret": 0.014902 
},
{
 "date":   1259,
"name": "GSPC.Close",
"price":  107.6,
"rsi": 56.032,
"ret": -0.0063718 
},
{
 "date":   1260,
"name": "GSPC.Close",
"price":  106.4,
"rsi": 53.366,
"ret": -0.011152 
},
{
 "date":   1261,
"name": "GSPC.Close",
"price":  105.1,
"rsi": 48.999,
"ret": -0.012218 
},
{
 "date":   1264,
"name": "GSPC.Close",
"price":  103.6,
"rsi": 44.729,
"ret": -0.014272 
},
{
 "date":   1265,
"name": "GSPC.Close",
"price": 103.99,
"rsi": 40.358,
"ret": 0.0037645 
},
{
 "date":   1266,
"name": "GSPC.Close",
"price": 104.44,
"rsi": 41.947,
"ret": 0.0043273 
},
{
 "date":   1267,
"name": "GSPC.Close",
"price": 103.21,
"rsi": 43.806,
"ret": -0.011777 
},
{
 "date":   1268,
"name": "GSPC.Close",
"price":  103.7,
"rsi": 40.032,
"ret": 0.0047476 
},
{
 "date":   1271,
"name": "GSPC.Close",
"price": 102.25,
"rsi": 42.169,
"ret": -0.013983 
},
{
 "date":   1272,
"name": "GSPC.Close",
"price":  103.3,
"rsi": 37.867,
"ret": 0.010269 
},
{
 "date":   1273,
"name": "GSPC.Close",
"price": 103.62,
"rsi": 42.446,
"ret": 0.0030978 
},
{
 "date":   1274,
"name": "GSPC.Close",
"price": 104.69,
"rsi": 43.805,
"ret": 0.010326 
},
{
 "date":   1275,
"name": "GSPC.Close",
"price": 104.26,
"rsi": 48.209,
"ret": -0.0041074 
},
{
 "date":   1278,
"name": "GSPC.Close",
"price":  102.9,
"rsi": 46.628,
"ret": -0.013044 
},
{
 "date":   1279,
"name": "GSPC.Close",
"price": 101.87,
"rsi": 41.941,
"ret": -0.01001 
},
{
 "date":   1281,
"name": "GSPC.Close",
"price": 101.78,
"rsi": 38.764,
"ret": -0.00088348 
},
{
 "date":   1282,
"name": "GSPC.Close",
"price": 101.28,
"rsi": 38.489,
"ret": -0.0049126 
},
{
 "date":   1285,
"name": "GSPC.Close",
"price": 102.14,
"rsi": 36.925,
"ret": 0.0084913 
},
{
 "date":   1286,
"name": "GSPC.Close",
"price": 103.52,
"rsi":  41.34,
"ret": 0.013511 
},
{
 "date":   1287,
"name": "GSPC.Close",
"price":  105.8,
"rsi":  47.67,
"ret": 0.022025 
},
{
 "date":   1288,
"name": "GSPC.Close",
"price":  105.5,
"rsi": 56.099,
"ret": -0.0028355 
},
{
 "date":   1289,
"name": "GSPC.Close",
"price": 104.09,
"rsi": 54.847,
"ret": -0.013365 
},
{
 "date":   1292,
"name": "GSPC.Close",
"price": 105.67,
"rsi": 49.281,
"ret": 0.015179 
},
{
 "date":   1293,
"name": "GSPC.Close",
"price": 105.72,
"rsi": 54.815,
"ret": 0.00047317 
},
{
 "date":   1294,
"name": "GSPC.Close",
"price": 106.35,
"rsi": 54.982,
"ret": 0.0059591 
},
{
 "date":   1295,
"name": "GSPC.Close",
"price": 106.55,
"rsi": 57.137,
"ret": 0.0018806 
},
{
 "date":   1296,
"name": "GSPC.Close",
"price": 107.14,
"rsi": 57.827,
"ret": 0.0055373 
},
{
 "date":   1299,
"name": "GSPC.Close",
"price": 107.52,
"rsi": 59.879,
"ret": 0.0035468 
},
{
 "date":   1300,
"name": "GSPC.Close",
"price": 108.14,
"rsi": 61.189,
"ret": 0.0057664 
},
{
 "date":   1301,
"name": "GSPC.Close",
"price": 109.64,
"rsi": 63.294,
"ret": 0.013871 
},
{
 "date":   1302,
"name": "GSPC.Close",
"price": 109.85,
"rsi":  67.84,
"ret": 0.0019154 
},
{
 "date":   1303,
"name": "GSPC.Close",
"price": 109.59,
"rsi": 68.429,
"ret": -0.0023669 
},
{
 "date":   1306,
"name": "GSPC.Close",
"price": 109.25,
"rsi": 66.797,
"ret": -0.0031025 
},
{
 "date":   1307,
"name": "GSPC.Close",
"price": 108.22,
"rsi": 64.626,
"ret": -0.0094279 
},
{
 "date":   1308,
"name": "GSPC.Close",
"price": 106.83,
"rsi":  58.43,
"ret": -0.012844 
},
{
 "date":   1309,
"name": "GSPC.Close",
"price": 106.67,
"rsi": 51.284,
"ret": -0.0014977 
},
{
 "date":   1310,
"name": "GSPC.Close",
"price": 106.49,
"rsi": 50.518,
"ret": -0.0016874 
},
{
 "date":   1313,
"name": "GSPC.Close",
"price": 106.73,
"rsi":  49.62,
"ret": 0.0022537 
},
{
 "date":   1314,
"name": "GSPC.Close",
"price": 106.55,
"rsi": 50.873,
"ret": -0.0016865 
},
{
 "date":   1315,
"name": "GSPC.Close",
"price": 105.55,
"rsi": 49.871,
"ret": -0.0093853 
},
{
 "date":   1316,
"name": "GSPC.Close",
"price": 105.61,
"rsi": 44.612,
"ret": 0.00056845 
},
{
 "date":   1317,
"name": "GSPC.Close",
"price": 104.77,
"rsi": 44.987,
"ret": -0.0079538 
},
{
 "date":   1320,
"name": "GSPC.Close",
"price": 103.71,
"rsi": 40.822,
"ret": -0.010117 
},
{
 "date":   1321,
"name": "GSPC.Close",
"price": 102.71,
"rsi":  36.26,
"ret": -0.0096423 
},
{
 "date":   1322,
"name": "GSPC.Close",
"price": 103.01,
"rsi": 32.563,
"ret": 0.0029208 
},
{
 "date":   1323,
"name": "GSPC.Close",
"price": 102.29,
"rsi": 34.713,
"ret": -0.0069896 
},
{
 "date":   1324,
"name": "GSPC.Close",
"price": 102.31,
"rsi":  32.07,
"ret": 0.00019552 
},
{
 "date":   1327,
"name": "GSPC.Close",
"price": 101.61,
"rsi": 32.224,
"ret": -0.006842 
},
{
 "date":   1328,
"name": "GSPC.Close",
"price": 100.89,
"rsi": 29.681,
"ret": -0.0070859 
},
{
 "date":   1329,
"name": "GSPC.Close",
"price": 100.53,
"rsi": 27.296,
"ret": -0.0035682 
},
{
 "date":   1330,
"name": "GSPC.Close",
"price": 101.91,
"rsi": 26.163,
"ret": 0.013727 
},
{
 "date":   1331,
"name": "GSPC.Close",
"price": 101.62,
"rsi":  36.96,
"ret": -0.0028456 
},
{
 "date":   1334,
"name": "GSPC.Close",
"price": 102.42,
"rsi": 35.776,
"ret": 0.0078725 
},
{
 "date":   1335,
"name": "GSPC.Close",
"price": 103.02,
"rsi": 41.356,
"ret": 0.0058582 
},
{
 "date":   1336,
"name": "GSPC.Close",
"price": 104.03,
"rsi": 45.202,
"ret": 0.0098039 
},
{
 "date":   1337,
"name": "GSPC.Close",
"price": 103.88,
"rsi": 51.025,
"ret": -0.0014419 
},
{
 "date":   1338,
"name": "GSPC.Close",
"price": 104.25,
"rsi": 50.172,
"ret": 0.0035618 
},
{
 "date":   1342,
"name": "GSPC.Close",
"price": 104.51,
"rsi":  52.29,
"ret": 0.002494 
},
{
 "date":   1343,
"name": "GSPC.Close",
"price": 104.64,
"rsi": 53.777,
"ret": 0.0012439 
},
{
 "date":   1344,
"name": "GSPC.Close",
"price": 105.15,
"rsi": 54.539,
"ret": 0.0048739 
},
{
 "date":   1345,
"name": "GSPC.Close",
"price": 104.76,
"rsi": 57.502,
"ret": -0.003709 
},
{
 "date":   1348,
"name": "GSPC.Close",
"price": 103.85,
"rsi": 54.573,
"ret": -0.0086865 
},
{
 "date":   1349,
"name": "GSPC.Close",
"price": 103.22,
"rsi":  48.38,
"ret": -0.0060664 
},
{
 "date":   1350,
"name": "GSPC.Close",
"price": 103.06,
"rsi": 44.606,
"ret": -0.0015501 
},
{
 "date":   1351,
"name": "GSPC.Close",
"price": 103.36,
"rsi": 43.675,
"ret": 0.0029109 
},
{
 "date":   1352,
"name": "GSPC.Close",
"price": 104.44,
"rsi": 45.954,
"ret": 0.010449 
},
{
 "date":   1355,
"name": "GSPC.Close",
"price": 104.15,
"rsi": 53.284,
"ret": -0.0027767 
},
{
 "date":   1356,
"name": "GSPC.Close",
"price": 103.77,
"rsi": 51.273,
"ret": -0.0036486 
},
{
 "date":   1357,
"name": "GSPC.Close",
"price": 105.88,
"rsi": 48.681,
"ret": 0.020333 
},
{
 "date":   1358,
"name": "GSPC.Close",
"price": 106.76,
"rsi": 60.595,
"ret": 0.0083113 
},
{
 "date":   1359,
"name": "GSPC.Close",
"price":  107.2,
"rsi": 64.316,
"ret": 0.0041214 
},
{
 "date":   1362,
"name": "GSPC.Close",
"price": 107.36,
"rsi": 66.043,
"ret": 0.0014925 
},
{
 "date":   1363,
"name": "GSPC.Close",
"price": 108.05,
"rsi": 66.674,
"ret": 0.006427 
},
{
 "date":   1364,
"name": "GSPC.Close",
"price": 108.83,
"rsi": 69.323,
"ret": 0.0072189 
},
{
 "date":   1365,
"name": "GSPC.Close",
"price": 109.08,
"rsi":  72.03,
"ret": 0.0022972 
},
{
 "date":   1366,
"name": "GSPC.Close",
"price": 108.43,
"rsi": 72.857,
"ret": -0.0059589 
},
{
 "date":   1369,
"name": "GSPC.Close",
"price": 108.21,
"rsi": 67.288,
"ret": -0.002029 
},
{
 "date":   1370,
"name": "GSPC.Close",
"price": 108.79,
"rsi": 65.464,
"ret": 0.0053599 
},
{
 "date":   1371,
"name": "GSPC.Close",
"price": 108.78,
"rsi": 67.932,
"ret": -9.192e-05 
},
{
 "date":   1372,
"name": "GSPC.Close",
"price": 108.41,
"rsi": 67.842,
"ret": -0.0034014 
},
{
 "date":   1373,
"name": "GSPC.Close",
"price": 109.85,
"rsi":  64.44,
"ret": 0.013283 
},
{
 "date":   1376,
"name": "GSPC.Close",
"price": 110.23,
"rsi": 70.616,
"ret": 0.0034593 
},
{
 "date":   1377,
"name": "GSPC.Close",
"price": 110.13,
"rsi": 71.998,
"ret": -0.00090719 
},
{
 "date":   1378,
"name": "GSPC.Close",
"price": 109.22,
"rsi": 71.051,
"ret": -0.008263 
},
{
 "date":   1379,
"name": "GSPC.Close",
"price": 111.09,
"rsi": 62.937,
"ret": 0.017121 
},
{
 "date":   1380,
"name": "GSPC.Close",
"price": 111.44,
"rsi": 70.414,
"ret": 0.0031506 
},
{
 "date":   1383,
"name": "GSPC.Close",
"price": 110.05,
"rsi":  71.57,
"ret": -0.012473 
},
{
 "date":   1384,
"name": "GSPC.Close",
"price": 110.19,
"rsi": 61.322,
"ret": 0.0012721 
},
{
 "date":   1385,
"name": "GSPC.Close",
"price": 109.97,
"rsi": 61.914,
"ret": -0.0019966 
},
{
 "date":   1386,
"name": "GSPC.Close",
"price": 110.01,
"rsi": 60.352,
"ret": 0.00036374 
},
{
 "date":   1387,
"name": "GSPC.Close",
"price": 110.22,
"rsi": 60.547,
"ret": 0.0019089 
},
{
 "date":   1390,
"name": "GSPC.Close",
"price": 109.16,
"rsi": 61.614,
"ret": -0.0096171 
},
{
 "date":   1391,
"name": "GSPC.Close",
"price": 109.75,
"rsi": 53.718,
"ret": 0.0054049 
},
{
 "date":   1392,
"name": "GSPC.Close",
"price": 110.27,
"rsi": 57.019,
"ret": 0.004738 
},
{
 "date":   1393,
"name": "GSPC.Close",
"price":  110.5,
"rsi": 59.745,
"ret": 0.0020858 
},
{
 "date":   1394,
"name": "GSPC.Close",
"price": 111.38,
"rsi": 60.925,
"ret": 0.0079638 
},
{
 "date":   1397,
"name": "GSPC.Close",
"price": 111.15,
"rsi": 65.137,
"ret": -0.002065 
},
{
 "date":   1398,
"name": "GSPC.Close",
"price": 109.33,
"rsi": 63.219,
"ret": -0.016374 
},
{
 "date":   1399,
"name": "GSPC.Close",
"price": 108.29,
"rsi": 50.537,
"ret": -0.0095125 
},
{
 "date":   1400,
"name": "GSPC.Close",
"price": 107.69,
"rsi": 44.984,
"ret": -0.0055407 
},
{
 "date":   1401,
"name": "GSPC.Close",
"price": 107.07,
"rsi":  42.11,
"ret": -0.0057573 
},
{
 "date":   1404,
"name": "GSPC.Close",
"price": 105.52,
"rsi": 39.314,
"ret": -0.014477 
},
{
 "date":   1405,
"name": "GSPC.Close",
"price": 104.96,
"rsi": 33.352,
"ret": -0.0053071 
},
{
 "date":   1406,
"name": "GSPC.Close",
"price":  105.8,
"rsi": 31.494,
"ret": 0.008003 
},
{
 "date":   1407,
"name": "GSPC.Close",
"price": 107.02,
"rsi":  37.15,
"ret": 0.011531 
},
{
 "date":   1408,
"name": "GSPC.Close",
"price":  105.3,
"rsi": 44.339,
"ret": -0.016072 
},
{
 "date":   1411,
"name": "GSPC.Close",
"price": 104.44,
"rsi": 37.778,
"ret": -0.0081671 
},
{
 "date":   1412,
"name": "GSPC.Close",
"price": 104.36,
"rsi": 34.991,
"ret": -0.00076599 
},
{
 "date":   1413,
"name": "GSPC.Close",
"price": 102.45,
"rsi": 34.734,
"ret": -0.018302 
},
{
 "date":   1414,
"name": "GSPC.Close",
"price": 102.43,
"rsi": 29.221,
"ret": -0.00019522 
},
{
 "date":   1415,
"name": "GSPC.Close",
"price": 103.88,
"rsi": 29.168,
"ret": 0.014156 
},
{
 "date":   1418,
"name": "GSPC.Close",
"price": 100.71,
"rsi":  37.84,
"ret": -0.030516 
},
{
 "date":   1419,
"name": "GSPC.Close",
"price":  98.66,
"rsi": 29.373,
"ret": -0.020355 
},
{
 "date":   1420,
"name": "GSPC.Close",
"price":  99.76,
"rsi": 25.413,
"ret": 0.011149 
},
{
 "date":   1422,
"name": "GSPC.Close",
"price":  99.44,
"rsi": 30.804,
"ret": -0.0032077 
},
{
 "date":   1425,
"name": "GSPC.Close",
"price":  96.58,
"rsi": 30.122,
"ret": -0.028761 
},
{
 "date":   1426,
"name": "GSPC.Close",
"price":   95.7,
"rsi": 24.831,
"ret": -0.0091116 
},
{
 "date":   1427,
"name": "GSPC.Close",
"price":  97.65,
"rsi": 23.465,
"ret": 0.020376 
},
{
 "date":   1428,
"name": "GSPC.Close",
"price":  97.31,
"rsi": 32.346,
"ret": -0.0034818 
},
{
 "date":   1429,
"name": "GSPC.Close",
"price":  95.96,
"rsi": 31.656,
"ret": -0.013873 
},
{
 "date":   1432,
"name": "GSPC.Close",
"price":   93.9,
"rsi": 29.011,
"ret": -0.021467 
},
{
 "date":   1433,
"name": "GSPC.Close",
"price":  93.59,
"rsi": 25.508,
"ret": -0.0033014 
},
{
 "date":   1434,
"name": "GSPC.Close",
"price":  92.16,
"rsi": 25.018,
"ret": -0.015279 
},
{
 "date":   1435,
"name": "GSPC.Close",
"price":  94.42,
"rsi": 22.841,
"ret": 0.024523 
},
{
 "date":   1436,
"name": "GSPC.Close",
"price":  96.51,
"rsi": 32.796,
"ret": 0.022135 
},
{
 "date":   1439,
"name": "GSPC.Close",
"price":  97.95,
"rsi": 40.449,
"ret": 0.014921 
},
{
 "date":   1440,
"name": "GSPC.Close",
"price":  96.04,
"rsi": 45.088,
"ret": -0.0195 
},
{
 "date":   1441,
"name": "GSPC.Close",
"price":  93.57,
"rsi": 40.573,
"ret": -0.025718 
},
{
 "date":   1442,
"name": "GSPC.Close",
"price":  92.38,
"rsi": 35.607,
"ret": -0.012718 
},
{
 "date":   1443,
"name": "GSPC.Close",
"price":  93.29,
"rsi": 33.481,
"ret": 0.0098506 
},
{
 "date":   1446,
"name": "GSPC.Close",
"price":  92.75,
"rsi": 36.599,
"ret": -0.0057884 
},
{
 "date":   1447,
"name": "GSPC.Close",
"price":  94.74,
"rsi": 35.534,
"ret": 0.021456 
},
{
 "date":   1448,
"name": "GSPC.Close",
"price":  94.82,
"rsi": 42.205,
"ret": 0.00084442 
},
{
 "date":   1449,
"name": "GSPC.Close",
"price":  94.55,
"rsi": 42.462,
"ret": -0.0028475 
},
{
 "date":   1450,
"name": "GSPC.Close",
"price":  93.54,
"rsi": 41.785,
"ret": -0.010682 
},
{
 "date":   1453,
"name": "GSPC.Close",
"price":   92.9,
"rsi": 39.262,
"ret": -0.006842 
},
{
 "date":   1455,
"name": "GSPC.Close",
"price":  95.74,
"rsi": 37.709,
"ret": 0.030571 
},
{
 "date":   1456,
"name": "GSPC.Close",
"price":  97.74,
"rsi": 47.615,
"ret": 0.02089 
},
{
 "date":   1457,
"name": "GSPC.Close",
"price":  97.54,
"rsi": 53.253,
"ret": -0.0020462 
},
{
 "date":   1460,
"name": "GSPC.Close",
"price":  97.55,
"rsi": 52.643,
"ret": 0.00010252 
},
{
 "date":   1462,
"name": "GSPC.Close",
"price":  97.68,
"rsi": 52.672,
"ret": 0.0013326 
},
{
 "date":   1463,
"name": "GSPC.Close",
"price":   99.8,
"rsi": 53.077,
"ret": 0.021704 
},
{
 "date":   1464,
"name": "GSPC.Close",
"price":   98.9,
"rsi": 59.208,
"ret": -0.009018 
},
{
 "date":   1467,
"name": "GSPC.Close",
"price":  98.07,
"rsi": 55.871,
"ret": -0.0083923 
},
{
 "date":   1468,
"name": "GSPC.Close",
"price":  96.12,
"rsi": 52.909,
"ret": -0.019884 
},
{
 "date":   1469,
"name": "GSPC.Close",
"price":  93.42,
"rsi": 46.651,
"ret": -0.02809 
},
{
 "date":   1470,
"name": "GSPC.Close",
"price":  92.39,
"rsi": 39.657,
"ret": -0.011025 
},
{
 "date":   1471,
"name": "GSPC.Close",
"price":  93.66,
"rsi": 37.356,
"ret": 0.013746 
},
{
 "date":   1474,
"name": "GSPC.Close",
"price":  93.42,
"rsi": 41.837,
"ret": -0.0025625 
},
{
 "date":   1475,
"name": "GSPC.Close",
"price":  94.23,
"rsi": 41.237,
"ret": 0.0086705 
},
{
 "date":   1476,
"name": "GSPC.Close",
"price":  95.67,
"rsi": 44.149,
"ret": 0.015282 
},
{
 "date":   1477,
"name": "GSPC.Close",
"price":   97.3,
"rsi":  48.99,
"ret": 0.017038 
},
{
 "date":   1478,
"name": "GSPC.Close",
"price":  95.56,
"rsi": 53.864,
"ret": -0.017883 
},
{
 "date":   1481,
"name": "GSPC.Close",
"price":   95.4,
"rsi": 48.533,
"ret": -0.0016743 
},
{
 "date":   1482,
"name": "GSPC.Close",
"price":  96.55,
"rsi": 48.062,
"ret": 0.012055 
},
{
 "date":   1483,
"name": "GSPC.Close",
"price":  97.07,
"rsi": 51.691,
"ret": 0.0053858 
},
{
 "date":   1484,
"name": "GSPC.Close",
"price":  96.82,
"rsi": 53.281,
"ret": -0.0025755 
},
{
 "date":   1485,
"name": "GSPC.Close",
"price":  96.63,
"rsi": 52.388,
"ret": -0.0019624 
},
{
 "date":   1488,
"name": "GSPC.Close",
"price":  96.09,
"rsi":  51.68,
"ret": -0.0055883 
},
{
 "date":   1489,
"name": "GSPC.Close",
"price":  96.01,
"rsi": 49.625,
"ret": -0.00083255 
},
{
 "date":   1490,
"name": "GSPC.Close",
"price":  97.06,
"rsi": 49.312,
"ret": 0.010936 
},
{
 "date":   1491,
"name": "GSPC.Close",
"price":  96.57,
"rsi": 53.459,
"ret": -0.0050484 
},
{
 "date":   1492,
"name": "GSPC.Close",
"price":  95.32,
"rsi": 51.348,
"ret": -0.012944 
},
{
 "date":   1495,
"name": "GSPC.Close",
"price":  93.29,
"rsi": 46.323,
"ret": -0.021297 
},
{
 "date":   1496,
"name": "GSPC.Close",
"price":     93,
"rsi": 39.553,
"ret": -0.0031086 
},
{
 "date":   1497,
"name": "GSPC.Close",
"price":  93.26,
"rsi": 38.683,
"ret": 0.0027957 
},
{
 "date":   1498,
"name": "GSPC.Close",
"price":   93.3,
"rsi": 39.958,
"ret": 0.00042891 
},
{
 "date":   1499,
"name": "GSPC.Close",
"price":  92.33,
"rsi": 40.164,
"ret": -0.010397 
},
{
 "date":   1502,
"name": "GSPC.Close",
"price":  90.66,
"rsi":  36.86,
"ret": -0.018087 
},
{
 "date":   1503,
"name": "GSPC.Close",
"price":  90.94,
"rsi": 31.982,
"ret": 0.0030885 
},
{
 "date":   1504,
"name": "GSPC.Close",
"price":  90.98,
"rsi": 33.569,
"ret": 0.00043985 
},
{
 "date":   1505,
"name": "GSPC.Close",
"price":  90.95,
"rsi": 33.807,
"ret": -0.00032974 
},
{
 "date":   1506,
"name": "GSPC.Close",
"price":  92.27,
"rsi":  33.71,
"ret": 0.014513 
},
{
 "date":   1510,
"name": "GSPC.Close",
"price":  92.12,
"rsi": 41.673,
"ret": -0.0016257 
},
{
 "date":   1511,
"name": "GSPC.Close",
"price":  93.44,
"rsi": 41.069,
"ret": 0.014329 
},
{
 "date":   1512,
"name": "GSPC.Close",
"price":  94.71,
"rsi": 48.184,
"ret": 0.013592 
},
{
 "date":   1513,
"name": "GSPC.Close",
"price":  95.39,
"rsi": 53.945,
"ret": 0.0071798 
},
{
 "date":   1516,
"name": "GSPC.Close",
"price":  95.03,
"rsi":  56.72,
"ret": -0.003774 
},
{
 "date":   1517,
"name": "GSPC.Close",
"price":     96,
"rsi": 54.836,
"ret": 0.010207 
},
{
 "date":   1518,
"name": "GSPC.Close",
"price":   96.4,
"rsi": 58.806,
"ret": 0.0041667 
},
{
 "date":   1519,
"name": "GSPC.Close",
"price":  96.22,
"rsi": 60.353,
"ret": -0.0018672 
},
{
 "date":   1520,
"name": "GSPC.Close",
"price":  95.53,
"rsi": 59.274,
"ret": -0.0071711 
},
{
 "date":   1523,
"name": "GSPC.Close",
"price":  95.53,
"rsi":   55.2,
"ret":      0 
},
{
 "date":   1524,
"name": "GSPC.Close",
"price":  97.32,
"rsi":   55.2,
"ret": 0.018738 
},
{
 "date":   1525,
"name": "GSPC.Close",
"price":  97.98,
"rsi": 62.877,
"ret": 0.0067818 
},
{
 "date":   1526,
"name": "GSPC.Close",
"price":  96.94,
"rsi": 65.242,
"ret": -0.010614 
},
{
 "date":   1527,
"name": "GSPC.Close",
"price":  97.78,
"rsi": 58.877,
"ret": 0.0086652 
},
{
 "date":   1530,
"name": "GSPC.Close",
"price":  98.88,
"rsi": 62.094,
"ret": 0.01125 
},
{
 "date":   1531,
"name": "GSPC.Close",
"price":  99.15,
"rsi":  65.86,
"ret": 0.0027306 
},
{
 "date":   1532,
"name": "GSPC.Close",
"price":  99.74,
"rsi": 66.734,
"ret": 0.0059506 
},
{
 "date":   1533,
"name": "GSPC.Close",
"price":  99.65,
"rsi": 68.623,
"ret": -0.00090235 
},
{
 "date":   1534,
"name": "GSPC.Close",
"price":  99.28,
"rsi": 67.989,
"ret": -0.003713 
},
{
 "date":   1537,
"name": "GSPC.Close",
"price":  98.05,
"rsi": 65.315,
"ret": -0.012389 
},
{
 "date":   1538,
"name": "GSPC.Close",
"price":  97.23,
"rsi": 57.255,
"ret": -0.0083631 
},
{
 "date":   1539,
"name": "GSPC.Close",
"price":  97.57,
"rsi": 52.595,
"ret": 0.0034969 
},
{
 "date":   1540,
"name": "GSPC.Close",
"price":  97.34,
"rsi": 54.258,
"ret": -0.0023573 
},
{
 "date":   1541,
"name": "GSPC.Close",
"price":  97.27,
"rsi": 52.906,
"ret": -0.00071913 
},
{
 "date":   1544,
"name": "GSPC.Close",
"price":  97.64,
"rsi": 52.478,
"ret": 0.0038038 
},
{
 "date":   1545,
"name": "GSPC.Close",
"price":  97.95,
"rsi": 54.572,
"ret": 0.0031749 
},
{
 "date":   1546,
"name": "GSPC.Close",
"price":  96.59,
"rsi": 56.309,
"ret": -0.013885 
},
{
 "date":   1547,
"name": "GSPC.Close",
"price":  94.82,
"rsi": 47.692,
"ret": -0.018325 
},
{
 "date":   1548,
"name": "GSPC.Close",
"price":  93.98,
"rsi":  39.27,
"ret": -0.0088589 
},
{
 "date":   1551,
"name": "GSPC.Close",
"price":  93.25,
"rsi": 36.019,
"ret": -0.0077676 
},
{
 "date":   1552,
"name": "GSPC.Close",
"price":  93.35,
"rsi": 33.429,
"ret": 0.0010724 
},
{
 "date":   1553,
"name": "GSPC.Close",
"price":  94.33,
"rsi": 34.128,
"ret": 0.010498 
},
{
 "date":   1554,
"name": "GSPC.Close",
"price":  94.33,
"rsi": 40.697,
"ret":      0 
},
{
 "date":   1555,
"name": "GSPC.Close",
"price":  93.01,
"rsi": 40.697,
"ret": -0.013993 
},
{
 "date":   1558,
"name": "GSPC.Close",
"price":  92.03,
"rsi": 35.212,
"ret": -0.010537 
},
{
 "date":   1559,
"name": "GSPC.Close",
"price":  92.61,
"rsi": 31.786,
"ret": 0.0063023 
},
{
 "date":   1560,
"name": "GSPC.Close",
"price":   92.4,
"rsi": 35.769,
"ret": -0.0022676 
},
{
 "date":   1561,
"name": "GSPC.Close",
"price":  92.12,
"rsi": 34.973,
"ret": -0.0030303 
},
{
 "date":   1565,
"name": "GSPC.Close",
"price":  92.05,
"rsi": 33.889,
"ret": -0.00075988 
},
{
 "date":   1566,
"name": "GSPC.Close",
"price":  93.66,
"rsi": 33.609,
"ret": 0.01749 
},
{
 "date":   1567,
"name": "GSPC.Close",
"price":  94.36,
"rsi": 44.896,
"ret": 0.0074738 
},
{
 "date":   1568,
"name": "GSPC.Close",
"price":  94.78,
"rsi": 48.959,
"ret": 0.004451 
},
{
 "date":   1569,
"name": "GSPC.Close",
"price":  93.75,
"rsi": 51.281,
"ret": -0.010867 
},
{
 "date":   1572,
"name": "GSPC.Close",
"price":  93.38,
"rsi": 45.782,
"ret": -0.0039467 
},
{
 "date":   1573,
"name": "GSPC.Close",
"price":  91.81,
"rsi": 43.958,
"ret": -0.016813 
},
{
 "date":   1574,
"name": "GSPC.Close",
"price":   90.3,
"rsi":  37.19,
"ret": -0.016447 
},
{
 "date":   1575,
"name": "GSPC.Close",
"price":  89.57,
"rsi": 32.074,
"ret": -0.0080842 
},
{
 "date":   1576,
"name": "GSPC.Close",
"price":  90.18,
"rsi": 29.931,
"ret": 0.0068103 
},
{
 "date":   1579,
"name": "GSPC.Close",
"price":     90,
"rsi": 33.906,
"ret": -0.001996 
},
{
 "date":   1580,
"name": "GSPC.Close",
"price":  90.31,
"rsi": 33.305,
"ret": 0.0034444 
},
{
 "date":   1581,
"name": "GSPC.Close",
"price":  92.22,
"rsi": 35.426,
"ret": 0.021149 
},
{
 "date":   1582,
"name": "GSPC.Close",
"price":  92.09,
"rsi": 46.676,
"ret": -0.0014097 
},
{
 "date":   1583,
"name": "GSPC.Close",
"price":  91.29,
"rsi": 46.088,
"ret": -0.0086872 
},
{
 "date":   1586,
"name": "GSPC.Close",
"price":  91.12,
"rsi": 42.533,
"ret": -0.0018622 
},
{
 "date":   1587,
"name": "GSPC.Close",
"price":  91.46,
"rsi": 41.796,
"ret": 0.0037313 
},
{
 "date":   1588,
"name": "GSPC.Close",
"price":  91.64,
"rsi": 43.892,
"ret": 0.0019681 
},
{
 "date":   1589,
"name": "GSPC.Close",
"price":  92.96,
"rsi":  45.02,
"ret": 0.014404 
},
{
 "date":   1590,
"name": "GSPC.Close",
"price":  91.47,
"rsi": 52.558,
"ret": -0.016028 
},
{
 "date":   1593,
"name": "GSPC.Close",
"price":  90.66,
"rsi":  45.05,
"ret": -0.0088554 
},
{
 "date":   1594,
"name": "GSPC.Close",
"price":  90.69,
"rsi": 41.573,
"ret": 0.00033091 
},
{
 "date":   1595,
"name": "GSPC.Close",
"price":  90.45,
"rsi": 41.753,
"ret": -0.0026464 
},
{
 "date":   1596,
"name": "GSPC.Close",
"price":  89.72,
"rsi": 40.677,
"ret": -0.0080708 
},
{
 "date":   1597,
"name": "GSPC.Close",
"price":  88.21,
"rsi": 37.512,
"ret": -0.01683 
},
{
 "date":   1600,
"name": "GSPC.Close",
"price":  87.86,
"rsi": 31.971,
"ret": -0.0039678 
},
{
 "date":   1601,
"name": "GSPC.Close",
"price":  87.91,
"rsi": 30.834,
"ret": 0.00056909 
},
{
 "date":   1602,
"name": "GSPC.Close",
"price":  87.09,
"rsi":  31.21,
"ret": -0.0093277 
},
{
 "date":   1603,
"name": "GSPC.Close",
"price":  87.29,
"rsi": 28.474,
"ret": 0.0022965 
},
{
 "date":   1604,
"name": "GSPC.Close",
"price":  88.58,
"rsi": 30.084,
"ret": 0.014778 
},
{
 "date":   1608,
"name": "GSPC.Close",
"price":  88.37,
"rsi": 39.538,
"ret": -0.0023707 
},
{
 "date":   1609,
"name": "GSPC.Close",
"price":  86.89,
"rsi": 38.623,
"ret": -0.016748 
},
{
 "date":   1610,
"name": "GSPC.Close",
"price":  87.43,
"rsi": 32.849,
"ret": 0.0062148 
},
{
 "date":   1611,
"name": "GSPC.Close",
"price":  87.28,
"rsi": 36.575,
"ret": -0.0017157 
},
{
 "date":   1614,
"name": "GSPC.Close",
"price":   89.1,
"rsi": 35.977,
"ret": 0.020852 
},
{
 "date":   1615,
"name": "GSPC.Close",
"price":  90.14,
"rsi": 47.233,
"ret": 0.011672 
},
{
 "date":   1616,
"name": "GSPC.Close",
"price":  90.31,
"rsi": 52.385,
"ret": 0.001886 
},
{
 "date":   1617,
"name": "GSPC.Close",
"price":  91.96,
"rsi": 53.189,
"ret": 0.01827 
},
{
 "date":   1618,
"name": "GSPC.Close",
"price":  92.55,
"rsi": 60.215,
"ret": 0.0064158 
},
{
 "date":   1621,
"name": "GSPC.Close",
"price":   93.1,
"rsi": 62.389,
"ret": 0.0059427 
},
{
 "date":   1622,
"name": "GSPC.Close",
"price":  92.28,
"rsi": 64.345,
"ret": -0.0088077 
},
{
 "date":   1623,
"name": "GSPC.Close",
"price":  92.06,
"rsi": 59.387,
"ret": -0.002384 
},
{
 "date":   1624,
"name": "GSPC.Close",
"price":  92.34,
"rsi": 58.093,
"ret": 0.0030415 
},
{
 "date":   1625,
"name": "GSPC.Close",
"price":   91.3,
"rsi": 59.308,
"ret": -0.011263 
},
{
 "date":   1628,
"name": "GSPC.Close",
"price":  90.04,
"rsi": 53.146,
"ret": -0.013801 
},
{
 "date":   1629,
"name": "GSPC.Close",
"price":  89.45,
"rsi": 46.801,
"ret": -0.0065526 
},
{
 "date":   1630,
"name": "GSPC.Close",
"price":  88.84,
"rsi": 44.144,
"ret": -0.0068195 
},
{
 "date":   1631,
"name": "GSPC.Close",
"price":  88.21,
"rsi": 41.519,
"ret": -0.0070914 
},
{
 "date":   1632,
"name": "GSPC.Close",
"price":  87.46,
"rsi": 38.943,
"ret": -0.0085024 
},
{
 "date":   1635,
"name": "GSPC.Close",
"price":  87.69,
"rsi": 36.074,
"ret": 0.0026298 
},
{
 "date":   1636,
"name": "GSPC.Close",
"price":  88.98,
"rsi": 37.593,
"ret": 0.014711 
},
{
 "date":   1637,
"name": "GSPC.Close",
"price":  87.61,
"rsi": 45.423,
"ret": -0.015397 
},
{
 "date":   1638,
"name": "GSPC.Close",
"price":  86.31,
"rsi": 39.723,
"ret": -0.014838 
},
{
 "date":   1639,
"name": "GSPC.Close",
"price":     86,
"rsi": 35.208,
"ret": -0.0035917 
},
{
 "date":   1642,
"name": "GSPC.Close",
"price":  86.02,
"rsi": 34.209,
"ret": 0.00023256 
},
{
 "date":   1643,
"name": "GSPC.Close",
"price":   84.3,
"rsi": 34.339,
"ret": -0.019995 
},
{
 "date":   1644,
"name": "GSPC.Close",
"price":  84.25,
"rsi": 29.048,
"ret": -0.00059312 
},
{
 "date":   1646,
"name": "GSPC.Close",
"price":  83.66,
"rsi": 28.908,
"ret": -0.007003 
},
{
 "date":   1649,
"name": "GSPC.Close",
"price":  81.09,
"rsi": 27.246,
"ret": -0.03072 
},
{
 "date":   1650,
"name": "GSPC.Close",
"price":  81.48,
"rsi": 21.459,
"ret": 0.0048095 
},
{
 "date":   1651,
"name": "GSPC.Close",
"price":  79.99,
"rsi": 24.094,
"ret": -0.018287 
},
{
 "date":   1652,
"name": "GSPC.Close",
"price":  79.89,
"rsi": 21.171,
"ret": -0.0012502 
},
{
 "date":   1653,
"name": "GSPC.Close",
"price":  83.15,
"rsi": 20.987,
"ret": 0.040806 
},
{
 "date":   1656,
"name": "GSPC.Close",
"price":  83.78,
"rsi": 39.459,
"ret": 0.0075767 
},
{
 "date":   1657,
"name": "GSPC.Close",
"price":  82.81,
"rsi": 42.267,
"ret": -0.011578 
},
{
 "date":   1658,
"name": "GSPC.Close",
"price":   83.7,
"rsi": 39.248,
"ret": 0.010747 
},
{
 "date":   1659,
"name": "GSPC.Close",
"price":  83.78,
"rsi": 43.254,
"ret": 0.00095579 
},
{
 "date":   1660,
"name": "GSPC.Close",
"price":  83.54,
"rsi": 43.613,
"ret": -0.0028646 
},
{
 "date":   1663,
"name": "GSPC.Close",
"price":  83.81,
"rsi": 42.738,
"ret": 0.003232 
},
{
 "date":   1664,
"name": "GSPC.Close",
"price":  84.65,
"rsi": 44.098,
"ret": 0.010023 
},
{
 "date":   1665,
"name": "GSPC.Close",
"price":  84.99,
"rsi": 48.217,
"ret": 0.0040165 
},
{
 "date":   1666,
"name": "GSPC.Close",
"price":  83.98,
"rsi": 49.829,
"ret": -0.011884 
},
{
 "date":   1667,
"name": "GSPC.Close",
"price":   82.4,
"rsi": 45.317,
"ret": -0.018814 
},
{
 "date":   1670,
"name": "GSPC.Close",
"price":  80.94,
"rsi": 39.319,
"ret": -0.017718 
},
{
 "date":   1671,
"name": "GSPC.Close",
"price":   80.5,
"rsi": 34.742,
"ret": -0.0054361 
},
{
 "date":   1672,
"name": "GSPC.Close",
"price":  79.31,
"rsi": 33.478,
"ret": -0.014783 
},
{
 "date":   1673,
"name": "GSPC.Close",
"price":  78.75,
"rsi": 30.269,
"ret": -0.0070609 
},
{
 "date":   1674,
"name": "GSPC.Close",
"price":  78.59,
"rsi": 28.866,
"ret": -0.0020317 
},
{
 "date":   1677,
"name": "GSPC.Close",
"price":  79.29,
"rsi": 28.461,
"ret": 0.008907 
},
{
 "date":   1678,
"name": "GSPC.Close",
"price":  80.52,
"rsi": 32.904,
"ret": 0.015513 
},
{
 "date":   1679,
"name": "GSPC.Close",
"price":  82.65,
"rsi":  39.96,
"ret": 0.026453 
},
{
 "date":   1680,
"name": "GSPC.Close",
"price":  81.57,
"rsi": 49.804,
"ret": -0.013067 
},
{
 "date":   1681,
"name": "GSPC.Close",
"price":  80.86,
"rsi": 45.711,
"ret": -0.0087042 
},
{
 "date":   1684,
"name": "GSPC.Close",
"price":  79.75,
"rsi": 43.198,
"ret": -0.013727 
},
{
 "date":   1685,
"name": "GSPC.Close",
"price":  78.49,
"rsi": 39.538,
"ret": -0.015799 
},
{
 "date":   1686,
"name": "GSPC.Close",
"price":  76.73,
"rsi": 35.828,
"ret": -0.022423 
},
{
 "date":   1687,
"name": "GSPC.Close",
"price":   76.3,
"rsi": 31.396,
"ret": -0.0056041 
},
{
 "date":   1688,
"name": "GSPC.Close",
"price":  75.67,
"rsi": 30.406,
"ret": -0.0082569 
},
{
 "date":   1691,
"name": "GSPC.Close",
"price":  74.57,
"rsi": 28.965,
"ret": -0.014537 
},
{
 "date":   1692,
"name": "GSPC.Close",
"price":  74.95,
"rsi": 26.596,
"ret": 0.0050959 
},
{
 "date":   1693,
"name": "GSPC.Close",
"price":  73.51,
"rsi": 28.764,
"ret": -0.019213 
},
{
 "date":   1694,
"name": "GSPC.Close",
"price":   72.8,
"rsi":  25.67,
"ret": -0.0096585 
},
{
 "date":   1695,
"name": "GSPC.Close",
"price":  71.55,
"rsi": 24.283,
"ret": -0.01717 
},
{
 "date":   1698,
"name": "GSPC.Close",
"price":  72.16,
"rsi": 22.026,
"ret": 0.0085255 
},
{
 "date":   1699,
"name": "GSPC.Close",
"price":  70.94,
"rsi": 25.657,
"ret": -0.016907 
},
{
 "date":   1700,
"name": "GSPC.Close",
"price":  70.76,
"rsi": 23.318,
"ret": -0.0025374 
},
{
 "date":   1701,
"name": "GSPC.Close",
"price":  69.99,
"rsi": 22.985,
"ret": -0.010882 
},
{
 "date":   1702,
"name": "GSPC.Close",
"price":  72.15,
"rsi": 21.567,
"ret": 0.030862 
},
{
 "date":   1706,
"name": "GSPC.Close",
"price":  70.52,
"rsi": 33.891,
"ret": -0.022592 
},
{
 "date":   1707,
"name": "GSPC.Close",
"price":  68.69,
"rsi": 30.053,
"ret": -0.02595 
},
{
 "date":   1708,
"name": "GSPC.Close",
"price":  70.87,
"rsi": 26.434,
"ret": 0.031737 
},
{
 "date":   1709,
"name": "GSPC.Close",
"price":  71.42,
"rsi": 36.278,
"ret": 0.0077607 
},
{
 "date":   1712,
"name": "GSPC.Close",
"price":  69.72,
"rsi": 38.514,
"ret": -0.023803 
},
{
 "date":   1713,
"name": "GSPC.Close",
"price":  69.24,
"rsi": 34.486,
"ret": -0.0068847 
},
{
 "date":   1714,
"name": "GSPC.Close",
"price":  68.55,
"rsi": 33.424,
"ret": -0.0099653 
},
{
 "date":   1715,
"name": "GSPC.Close",
"price":  66.71,
"rsi": 31.902,
"ret": -0.026842 
},
{
 "date":   1716,
"name": "GSPC.Close",
"price":   65.2,
"rsi": 28.213,
"ret": -0.022635 
},
{
 "date":   1719,
"name": "GSPC.Close",
"price":  66.26,
"rsi": 25.597,
"ret": 0.016258 
},
{
 "date":   1720,
"name": "GSPC.Close",
"price":  67.38,
"rsi": 30.471,
"ret": 0.016903 
},
{
 "date":   1721,
"name": "GSPC.Close",
"price":  67.72,
"rsi": 35.294,
"ret": 0.005046 
},
{
 "date":   1722,
"name": "GSPC.Close",
"price":  70.09,
"rsi": 36.728,
"ret": 0.034997 
},
{
 "date":   1723,
"name": "GSPC.Close",
"price":  70.14,
"rsi": 45.758,
"ret": 0.00071337 
},
{
 "date":   1726,
"name": "GSPC.Close",
"price":  69.42,
"rsi": 45.933,
"ret": -0.010265 
},
{
 "date":   1727,
"name": "GSPC.Close",
"price":  68.02,
"rsi": 43.741,
"ret": -0.020167 
},
{
 "date":   1728,
"name": "GSPC.Close",
"price":  67.57,
"rsi": 39.767,
"ret": -0.0066157 
},
{
 "date":   1729,
"name": "GSPC.Close",
"price":  66.46,
"rsi": 38.554,
"ret": -0.016427 
},
{
 "date":   1730,
"name": "GSPC.Close",
"price":  64.94,
"rsi": 35.665,
"ret": -0.022871 
},
{
 "date":   1733,
"name": "GSPC.Close",
"price":  63.54,
"rsi": 32.116,
"ret": -0.021558 
},
{
 "date":   1734,
"name": "GSPC.Close",
"price":  63.39,
"rsi": 29.231,
"ret": -0.0023607 
},
{
 "date":   1735,
"name": "GSPC.Close",
"price":  63.38,
"rsi": 28.931,
"ret": -0.00015775 
},
{
 "date":   1736,
"name": "GSPC.Close",
"price":  62.28,
"rsi":  28.91,
"ret": -0.017356 
},
{
 "date":   1737,
"name": "GSPC.Close",
"price":  62.34,
"rsi": 26.592,
"ret": 0.00096339 
},
{
 "date":   1740,
"name": "GSPC.Close",
"price":  64.95,
"rsi": 26.936,
"ret": 0.041867 
},
{
 "date":   1741,
"name": "GSPC.Close",
"price":  64.84,
"rsi": 40.094,
"ret": -0.0016936 
},
{
 "date":   1742,
"name": "GSPC.Close",
"price":  67.82,
"rsi": 39.769,
"ret": 0.045959 
},
{
 "date":   1743,
"name": "GSPC.Close",
"price":  69.79,
"rsi": 51.291,
"ret": 0.029047 
},
{
 "date":   1744,
"name": "GSPC.Close",
"price":  71.14,
"rsi": 57.129,
"ret": 0.019344 
},
{
 "date":   1747,
"name": "GSPC.Close",
"price":  72.74,
"rsi": 60.613,
"ret": 0.022491 
},
{
 "date":   1748,
"name": "GSPC.Close",
"price":  71.44,
"rsi": 64.314,
"ret": -0.017872 
},
{
 "date":   1749,
"name": "GSPC.Close",
"price":  70.33,
"rsi": 59.428,
"ret": -0.015538 
},
{
 "date":   1750,
"name": "GSPC.Close",
"price":  71.17,
"rsi": 55.547,
"ret": 0.011944 
},
{
 "date":   1751,
"name": "GSPC.Close",
"price":  72.28,
"rsi": 57.793,
"ret": 0.015596 
},
{
 "date":   1754,
"name": "GSPC.Close",
"price":   73.5,
"rsi": 60.625,
"ret": 0.016879 
},
{
 "date":   1755,
"name": "GSPC.Close",
"price":  73.13,
"rsi": 63.521,
"ret": -0.005034 
},
{
 "date":   1756,
"name": "GSPC.Close",
"price":  71.03,
"rsi": 62.031,
"ret": -0.028716 
},
{
 "date":   1757,
"name": "GSPC.Close",
"price":  70.22,
"rsi": 54.251,
"ret": -0.011404 
},
{
 "date":   1758,
"name": "GSPC.Close",
"price":  70.12,
"rsi": 51.564,
"ret": -0.0014241 
},
{
 "date":   1761,
"name": "GSPC.Close",
"price":  70.09,
"rsi": 51.227,
"ret": -0.00042784 
},
{
 "date":   1762,
"name": "GSPC.Close",
"price":  72.83,
"rsi": 51.119,
"ret": 0.039093 
},
{
 "date":   1763,
"name": "GSPC.Close",
"price":  74.31,
"rsi": 59.516,
"ret": 0.020321 
},
{
 "date":   1764,
"name": "GSPC.Close",
"price":   73.9,
"rsi": 63.194,
"ret": -0.0055174 
},
{
 "date":   1765,
"name": "GSPC.Close",
"price":  73.88,
"rsi": 61.526,
"ret": -0.00027064 
},
{
 "date":   1768,
"name": "GSPC.Close",
"price":  73.08,
"rsi": 61.441,
"ret": -0.010828 
},
{
 "date":   1769,
"name": "GSPC.Close",
"price":  75.11,
"rsi": 57.983,
"ret": 0.027778 
},
{
 "date":   1770,
"name": "GSPC.Close",
"price":  74.75,
"rsi": 63.584,
"ret": -0.004793 
},
{
 "date":   1771,
"name": "GSPC.Close",
"price":  75.21,
"rsi": 62.005,
"ret": 0.0061538 
},
{
 "date":   1772,
"name": "GSPC.Close",
"price":  74.91,
"rsi":  63.26,
"ret": -0.0039888 
},
{
 "date":   1775,
"name": "GSPC.Close",
"price":  75.15,
"rsi": 61.826,
"ret": 0.0032038 
},
{
 "date":   1776,
"name": "GSPC.Close",
"price":  73.67,
"rsi": 62.557,
"ret": -0.019694 
},
{
 "date":   1777,
"name": "GSPC.Close",
"price":  73.35,
"rsi": 55.496,
"ret": -0.0043437 
},
{
 "date":   1778,
"name": "GSPC.Close",
"price":  73.06,
"rsi": 54.075,
"ret": -0.0039536 
},
{
 "date":   1779,
"name": "GSPC.Close",
"price":  71.91,
"rsi": 52.756,
"ret": -0.01574 
},
{
 "date":   1782,
"name": "GSPC.Close",
"price":  69.27,
"rsi": 47.781,
"ret": -0.036713 
},
{
 "date":   1783,
"name": "GSPC.Close",
"price":   68.2,
"rsi": 38.746,
"ret": -0.015447 
},
{
 "date":   1784,
"name": "GSPC.Close",
"price":   67.9,
"rsi": 35.792,
"ret": -0.0043988 
},
{
 "date":   1785,
"name": "GSPC.Close",
"price":  68.18,
"rsi": 34.987,
"ret": 0.0041237 
},
{
 "date":   1786,
"name": "GSPC.Close",
"price":   68.9,
"rsi": 36.425,
"ret": 0.01056 
},
{
 "date":   1789,
"name": "GSPC.Close",
"price":  68.83,
"rsi": 40.094,
"ret": -0.001016 
},
{
 "date":   1790,
"name": "GSPC.Close",
"price":  69.47,
"rsi": 39.853,
"ret": 0.0092983 
},
{
 "date":   1791,
"name": "GSPC.Close",
"price":  69.94,
"rsi": 43.211,
"ret": 0.0067655 
},
{
 "date":   1793,
"name": "GSPC.Close",
"price":  69.97,
"rsi": 45.613,
"ret": 0.00042894 
},
{
 "date":   1796,
"name": "GSPC.Close",
"price":  68.11,
"rsi": 45.771,
"ret": -0.026583 
},
{
 "date":   1797,
"name": "GSPC.Close",
"price":  67.17,
"rsi": 38.349,
"ret": -0.013801 
},
{
 "date":   1798,
"name": "GSPC.Close",
"price":  67.41,
"rsi": 35.239,
"ret": 0.003573 
},
{
 "date":   1799,
"name": "GSPC.Close",
"price":  66.13,
"rsi": 36.651,
"ret": -0.018988 
},
{
 "date":   1800,
"name": "GSPC.Close",
"price":  65.01,
"rsi": 32.571,
"ret": -0.016936 
},
{
 "date":   1803,
"name": "GSPC.Close",
"price":   65.6,
"rsi": 29.478,
"ret": 0.0090755 
},
{
 "date":   1804,
"name": "GSPC.Close",
"price":  67.28,
"rsi": 33.083,
"ret": 0.02561 
},
{
 "date":   1805,
"name": "GSPC.Close",
"price":  67.67,
"rsi":  42.15,
"ret": 0.0057967 
},
{
 "date":   1806,
"name": "GSPC.Close",
"price":  67.45,
"rsi": 44.045,
"ret": -0.0032511 
},
{
 "date":   1807,
"name": "GSPC.Close",
"price":  67.07,
"rsi": 43.186,
"ret": -0.0056338 
},
{
 "date":   1810,
"name": "GSPC.Close",
"price":  66.46,
"rsi": 41.673,
"ret": -0.009095 
},
{
 "date":   1811,
"name": "GSPC.Close",
"price":  67.58,
"rsi": 39.293,
"ret": 0.016852 
},
{
 "date":   1812,
"name": "GSPC.Close",
"price":   67.9,
"rsi": 45.452,
"ret": 0.0047351 
},
{
 "date":   1813,
"name": "GSPC.Close",
"price":  67.65,
"rsi": 47.103,
"ret": -0.0036819 
},
{
 "date":   1814,
"name": "GSPC.Close",
"price":  66.91,
"rsi": 45.933,
"ret": -0.010939 
},
{
 "date":   1817,
"name": "GSPC.Close",
"price":  65.96,
"rsi": 42.564,
"ret": -0.014198 
},
{
 "date":   1818,
"name": "GSPC.Close",
"price":  66.88,
"rsi": 38.644,
"ret": 0.013948 
},
{
 "date":   1820,
"name": "GSPC.Close",
"price":  67.44,
"rsi":  44.02,
"ret": 0.0083732 
},
{
 "date":   1821,
"name": "GSPC.Close",
"price":  67.14,
"rsi": 47.061,
"ret": -0.0044484 
},
{
 "date":   1824,
"name": "GSPC.Close",
"price":  67.16,
"rsi": 45.631,
"ret": 0.00029789 
},
{
 "date":   1825,
"name": "GSPC.Close",
"price":  68.56,
"rsi": 45.749,
"ret": 0.020846 
},
{
 "date":   1827,
"name": "GSPC.Close",
"price":  70.23,
"rsi": 53.397,
"ret": 0.024358 
},
{
 "date":   1828,
"name": "GSPC.Close",
"price":  70.71,
"rsi": 60.542,
"ret": 0.0068347 
},
{
 "date":   1831,
"name": "GSPC.Close",
"price":  71.07,
"rsi": 62.329,
"ret": 0.0050912 
},
{
 "date":   1832,
"name": "GSPC.Close",
"price":  71.02,
"rsi": 63.659,
"ret": -0.00070353 
},
{
 "date":   1833,
"name": "GSPC.Close",
"price":  70.04,
"rsi": 63.325,
"ret": -0.013799 
},
{
 "date":   1834,
"name": "GSPC.Close",
"price":  71.17,
"rsi": 57.005,
"ret": 0.016134 
},
{
 "date":   1835,
"name": "GSPC.Close",
"price":  72.61,
"rsi": 61.746,
"ret": 0.020233 
},
{
 "date":   1838,
"name": "GSPC.Close",
"price":  72.31,
"rsi": 66.774,
"ret": -0.0041317 
},
{
 "date":   1839,
"name": "GSPC.Close",
"price":  71.68,
"rsi": 64.861,
"ret": -0.0087125 
},
{
 "date":   1840,
"name": "GSPC.Close",
"price":  72.14,
"rsi": 60.915,
"ret": 0.0064174 
},
{
 "date":   1841,
"name": "GSPC.Close",
"price":  72.05,
"rsi": 62.699,
"ret": -0.0012476 
},
{
 "date":   1842,
"name": "GSPC.Close",
"price":  70.96,
"rsi": 62.102,
"ret": -0.015128 
},
{
 "date":   1845,
"name": "GSPC.Close",
"price":  71.08,
"rsi": 55.238,
"ret": 0.0016911 
},
{
 "date":   1846,
"name": "GSPC.Close",
"price":   70.7,
"rsi": 55.817,
"ret": -0.0053461 
},
{
 "date":   1847,
"name": "GSPC.Close",
"price":  71.74,
"rsi": 53.458,
"ret": 0.01471 
},
{
 "date":   1848,
"name": "GSPC.Close",
"price":  72.07,
"rsi": 58.612,
"ret": 0.0045999 
},
{
 "date":   1849,
"name": "GSPC.Close",
"price":  72.98,
"rsi": 60.121,
"ret": 0.012627 
},
{
 "date":   1852,
"name": "GSPC.Close",
"price":  75.37,
"rsi": 64.017,
"ret": 0.032749 
},
{
 "date":   1853,
"name": "GSPC.Close",
"price":  76.03,
"rsi": 71.808,
"ret": 0.0087568 
},
{
 "date":   1854,
"name": "GSPC.Close",
"price":  77.26,
"rsi": 73.513,
"ret": 0.016178 
},
{
 "date":   1855,
"name": "GSPC.Close",
"price":  76.21,
"rsi": 76.381,
"ret": -0.01359 
},
{
 "date":   1856,
"name": "GSPC.Close",
"price":  76.98,
"rsi": 69.467,
"ret": 0.010104 
},
{
 "date":   1859,
"name": "GSPC.Close",
"price":  77.82,
"rsi": 71.504,
"ret": 0.010912 
},
{
 "date":   1860,
"name": "GSPC.Close",
"price":  77.61,
"rsi": 73.575,
"ret": -0.0026985 
},
{
 "date":   1861,
"name": "GSPC.Close",
"price":  78.95,
"rsi": 72.163,
"ret": 0.017266 
},
{
 "date":   1862,
"name": "GSPC.Close",
"price":  78.56,
"rsi": 75.407,
"ret": -0.0049398 
},
{
 "date":   1863,
"name": "GSPC.Close",
"price":  78.63,
"rsi":  72.75,
"ret": 0.00089104 
},
{
 "date":   1866,
"name": "GSPC.Close",
"price":  78.36,
"rsi": 72.934,
"ret": -0.0034338 
},
{
 "date":   1867,
"name": "GSPC.Close",
"price":  78.58,
"rsi": 70.941,
"ret": 0.0028076 
},
{
 "date":   1868,
"name": "GSPC.Close",
"price":  79.92,
"rsi": 71.621,
"ret": 0.017053 
},
{
 "date":   1869,
"name": "GSPC.Close",
"price":  81.01,
"rsi":   75.4,
"ret": 0.013639 
},
{
 "date":   1870,
"name": "GSPC.Close",
"price":   81.5,
"rsi":  77.97,
"ret": 0.0060486 
},
{
 "date":   1874,
"name": "GSPC.Close",
"price":  80.93,
"rsi": 79.031,
"ret": -0.0069939 
},
{
 "date":   1875,
"name": "GSPC.Close",
"price":  81.44,
"rsi": 74.536,
"ret": 0.0063017 
},
{
 "date":   1876,
"name": "GSPC.Close",
"price":  82.21,
"rsi": 75.859,
"ret": 0.0094548 
},
{
 "date":   1877,
"name": "GSPC.Close",
"price":  82.62,
"rsi": 77.739,
"ret": 0.0049872 
},
{
 "date":   1880,
"name": "GSPC.Close",
"price":  81.44,
"rsi": 78.691,
"ret": -0.014282 
},
{
 "date":   1881,
"name": "GSPC.Close",
"price":  79.53,
"rsi": 69.483,
"ret": -0.023453 
},
{
 "date":   1882,
"name": "GSPC.Close",
"price":  80.37,
"rsi":  57.71,
"ret": 0.010562 
},
{
 "date":   1883,
"name": "GSPC.Close",
"price":  80.77,
"rsi": 60.852,
"ret": 0.004977 
},
{
 "date":   1884,
"name": "GSPC.Close",
"price":  81.59,
"rsi": 62.288,
"ret": 0.010152 
},
{
 "date":   1887,
"name": "GSPC.Close",
"price":  83.03,
"rsi": 65.114,
"ret": 0.017649 
},
{
 "date":   1888,
"name": "GSPC.Close",
"price":  83.56,
"rsi": 69.445,
"ret": 0.0063832 
},
{
 "date":   1889,
"name": "GSPC.Close",
"price":   83.9,
"rsi": 70.878,
"ret": 0.0040689 
},
{
 "date":   1890,
"name": "GSPC.Close",
"price":  83.69,
"rsi": 71.792,
"ret": -0.002503 
},
{
 "date":   1891,
"name": "GSPC.Close",
"price":   84.3,
"rsi": 70.324,
"ret": 0.0072888 
},
{
 "date":   1894,
"name": "GSPC.Close",
"price":  84.95,
"rsi": 72.108,
"ret": 0.0077106 
},
{
 "date":   1895,
"name": "GSPC.Close",
"price":  84.36,
"rsi": 73.908,
"ret": -0.0069453 
},
{
 "date":   1896,
"name": "GSPC.Close",
"price":  83.59,
"rsi": 69.522,
"ret": -0.0091275 
},
{
 "date":   1897,
"name": "GSPC.Close",
"price":  83.74,
"rsi":  64.17,
"ret": 0.0017945 
},
{
 "date":   1898,
"name": "GSPC.Close",
"price":  84.76,
"rsi":  64.74,
"ret": 0.012181 
},
{
 "date":   1901,
"name": "GSPC.Close",
"price":  86.01,
"rsi": 68.416,
"ret": 0.014748 
},
{
 "date":   1902,
"name": "GSPC.Close",
"price":  85.13,
"rsi": 72.236,
"ret": -0.010231 
},
{
 "date":   1903,
"name": "GSPC.Close",
"price":  84.34,
"rsi": 66.168,
"ret": -0.0092799 
},
{
 "date":   1904,
"name": "GSPC.Close",
"price":  83.61,
"rsi": 61.199,
"ret": -0.0086554 
},
{
 "date":   1905,
"name": "GSPC.Close",
"price":  83.39,
"rsi": 56.943,
"ret": -0.0026313 
},
{
 "date":   1908,
"name": "GSPC.Close",
"price":  81.42,
"rsi": 55.686,
"ret": -0.023624 
},
{
 "date":   1909,
"name": "GSPC.Close",
"price":  82.06,
"rsi": 45.913,
"ret": 0.0078605 
},
{
 "date":   1910,
"name": "GSPC.Close",
"price":  83.59,
"rsi": 49.042,
"ret": 0.018645 
},
{
 "date":   1911,
"name": "GSPC.Close",
"price":  83.85,
"rsi": 55.647,
"ret": 0.0031104 
},
{
 "date":   1915,
"name": "GSPC.Close",
"price":  83.36,
"rsi": 56.675,
"ret": -0.0058438 
},
{
 "date":   1916,
"name": "GSPC.Close",
"price":  82.64,
"rsi": 54.129,
"ret": -0.0086372 
},
{
 "date":   1917,
"name": "GSPC.Close",
"price":  82.43,
"rsi": 50.537,
"ret": -0.0025411 
},
{
 "date":   1918,
"name": "GSPC.Close",
"price":  81.51,
"rsi": 49.505,
"ret": -0.011161 
},
{
 "date":   1919,
"name": "GSPC.Close",
"price":  80.88,
"rsi": 45.155,
"ret": -0.0077291 
},
{
 "date":   1922,
"name": "GSPC.Close",
"price":  80.35,
"rsi": 42.407,
"ret": -0.0065529 
},
{
 "date":   1923,
"name": "GSPC.Close",
"price":  80.99,
"rsi": 40.191,
"ret": 0.0079652 
},
{
 "date":   1924,
"name": "GSPC.Close",
"price":  82.84,
"rsi": 43.997,
"ret": 0.022842 
},
{
 "date":   1925,
"name": "GSPC.Close",
"price":  83.77,
"rsi": 53.256,
"ret": 0.011226 
},
{
 "date":   1926,
"name": "GSPC.Close",
"price":  84.18,
"rsi": 57.096,
"ret": 0.0048944 
},
{
 "date":   1929,
"name": "GSPC.Close",
"price":   85.6,
"rsi": 58.707,
"ret": 0.016869 
},
{
 "date":   1930,
"name": "GSPC.Close",
"price":   86.3,
"rsi": 63.778,
"ret": 0.0081776 
},
{
 "date":   1931,
"name": "GSPC.Close",
"price":   86.6,
"rsi": 65.995,
"ret": 0.0034762 
},
{
 "date":   1932,
"name": "GSPC.Close",
"price":  87.25,
"rsi":  66.93,
"ret": 0.0075058 
},
{
 "date":   1933,
"name": "GSPC.Close",
"price":   86.3,
"rsi": 68.922,
"ret": -0.010888 
},
{
 "date":   1936,
"name": "GSPC.Close",
"price":  87.23,
"rsi": 62.953,
"ret": 0.010776 
},
{
 "date":   1937,
"name": "GSPC.Close",
"price":  87.09,
"rsi": 66.052,
"ret": -0.001605 
},
{
 "date":   1938,
"name": "GSPC.Close",
"price":  86.12,
"rsi": 65.168,
"ret": -0.011138 
},
{
 "date":   1939,
"name": "GSPC.Close",
"price":  86.04,
"rsi": 59.252,
"ret": -0.00092894 
},
{
 "date":   1940,
"name": "GSPC.Close",
"price":  86.62,
"rsi": 58.778,
"ret": 0.0067411 
},
{
 "date":   1943,
"name": "GSPC.Close",
"price":  86.23,
"rsi": 61.201,
"ret": -0.0045024 
},
{
 "date":   1944,
"name": "GSPC.Close",
"price":  85.64,
"rsi": 58.702,
"ret": -0.0068422 
},
{
 "date":   1945,
"name": "GSPC.Close",
"price":   87.3,
"rsi": 55.041,
"ret": 0.019383 
},
{
 "date":   1946,
"name": "GSPC.Close",
"price":   88.1,
"rsi": 62.187,
"ret": 0.0091638 
},
{
 "date":   1947,
"name": "GSPC.Close",
"price":  89.22,
"rsi": 65.068,
"ret": 0.012713 
},
{
 "date":   1950,
"name": "GSPC.Close",
"price":  90.08,
"rsi": 68.668,
"ret": 0.0096391 
},
{
 "date":   1951,
"name": "GSPC.Close",
"price":  88.64,
"rsi": 71.129,
"ret": -0.015986 
},
{
 "date":   1952,
"name": "GSPC.Close",
"price":  89.08,
"rsi": 62.306,
"ret": 0.0049639 
},
{
 "date":   1953,
"name": "GSPC.Close",
"price":  89.56,
"rsi": 63.784,
"ret": 0.0053884 
},
{
 "date":   1954,
"name": "GSPC.Close",
"price":  90.53,
"rsi": 65.379,
"ret": 0.010831 
},
{
 "date":   1957,
"name": "GSPC.Close",
"price":  90.61,
"rsi": 68.407,
"ret": 0.00088368 
},
{
 "date":   1958,
"name": "GSPC.Close",
"price":  91.58,
"rsi": 68.651,
"ret": 0.010705 
},
{
 "date":   1959,
"name": "GSPC.Close",
"price":  92.27,
"rsi": 71.518,
"ret": 0.0075344 
},
{
 "date":   1960,
"name": "GSPC.Close",
"price":  91.41,
"rsi": 73.383,
"ret": -0.0093205 
},
{
 "date":   1961,
"name": "GSPC.Close",
"price":  90.43,
"rsi": 67.455,
"ret": -0.010721 
},
{
 "date":   1964,
"name": "GSPC.Close",
"price":  90.53,
"rsi": 61.371,
"ret": 0.0011058 
},
{
 "date":   1965,
"name": "GSPC.Close",
"price":  90.07,
"rsi":  61.75,
"ret": -0.0050812 
},
{
 "date":   1966,
"name": "GSPC.Close",
"price":  89.06,
"rsi": 58.887,
"ret": -0.011214 
},
{
 "date":   1967,
"name": "GSPC.Close",
"price":  89.39,
"rsi": 53.069,
"ret": 0.0037054 
},
{
 "date":   1968,
"name": "GSPC.Close",
"price":  90.58,
"rsi": 54.646,
"ret": 0.013312 
},
{
 "date":   1972,
"name": "GSPC.Close",
"price":  90.34,
"rsi":  59.88,
"ret": -0.0026496 
},
{
 "date":   1973,
"name": "GSPC.Close",
"price":  89.71,
"rsi": 58.416,
"ret": -0.0069737 
},
{
 "date":   1974,
"name": "GSPC.Close",
"price":  89.68,
"rsi": 54.639,
"ret": -0.00033441 
},
{
 "date":   1975,
"name": "GSPC.Close",
"price":  91.15,
"rsi": 54.458,
"ret": 0.016392 
},
{
 "date":   1978,
"name": "GSPC.Close",
"price":  92.58,
"rsi": 61.221,
"ret": 0.015688 
},
{
 "date":   1979,
"name": "GSPC.Close",
"price":  92.89,
"rsi": 66.442,
"ret": 0.0033485 
},
{
 "date":   1980,
"name": "GSPC.Close",
"price":   92.6,
"rsi": 67.464,
"ret": -0.003122 
},
{
 "date":   1981,
"name": "GSPC.Close",
"price":  92.69,
"rsi": 65.455,
"ret": 0.00097192 
},
{
 "date":   1982,
"name": "GSPC.Close",
"price":  92.48,
"rsi": 65.795,
"ret": -0.0022656 
},
{
 "date":   1985,
"name": "GSPC.Close",
"price":  91.21,
"rsi": 64.205,
"ret": -0.013733 
},
{
 "date":   1986,
"name": "GSPC.Close",
"price":  90.44,
"rsi": 55.474,
"ret": -0.0084421 
},
{
 "date":   1987,
"name": "GSPC.Close",
"price":  90.55,
"rsi": 50.949,
"ret": 0.0012163 
},
{
 "date":   1988,
"name": "GSPC.Close",
"price":  90.08,
"rsi": 51.557,
"ret": -0.0051905 
},
{
 "date":   1989,
"name": "GSPC.Close",
"price":  90.52,
"rsi": 48.776,
"ret": 0.0048845 
},
{
 "date":   1992,
"name": "GSPC.Close",
"price":  91.46,
"rsi": 51.418,
"ret": 0.010384 
},
{
 "date":   1993,
"name": "GSPC.Close",
"price":  90.58,
"rsi": 56.572,
"ret": -0.0096217 
},
{
 "date":   1994,
"name": "GSPC.Close",
"price":  90.39,
"rsi": 51.106,
"ret": -0.0020976 
},
{
 "date":   1995,
"name": "GSPC.Close",
"price":  92.02,
"rsi": 49.983,
"ret": 0.018033 
},
{
 "date":   1996,
"name": "GSPC.Close",
"price":  92.61,
"rsi": 58.423,
"ret": 0.0064116 
},
{
 "date":   1999,
"name": "GSPC.Close",
"price":  93.62,
"rsi": 60.989,
"ret": 0.010906 
},
{
 "date":   2000,
"name": "GSPC.Close",
"price":  94.19,
"rsi": 64.974,
"ret": 0.0060884 
},
{
 "date":   2001,
"name": "GSPC.Close",
"price":  94.62,
"rsi": 67.021,
"ret": 0.0045652 
},
{
 "date":   2002,
"name": "GSPC.Close",
"price":  94.81,
"rsi": 68.516,
"ret": 0.002008 
},
{
 "date":   2003,
"name": "GSPC.Close",
"price":  94.81,
"rsi": 69.181,
"ret":      0 
},
{
 "date":   2006,
"name": "GSPC.Close",
"price":  95.19,
"rsi": 69.181,
"ret": 0.004008 
},
{
 "date":   2007,
"name": "GSPC.Close",
"price":  94.85,
"rsi":  70.62,
"ret": -0.0035718 
},
{
 "date":   2008,
"name": "GSPC.Close",
"price":  94.18,
"rsi":  67.58,
"ret": -0.0070638 
},
{
 "date":   2009,
"name": "GSPC.Close",
"price":  94.36,
"rsi": 61.922,
"ret": 0.0019112 
},
{
 "date":   2013,
"name": "GSPC.Close",
"price":  93.54,
"rsi": 62.822,
"ret": -0.0086901 
},
{
 "date":   2014,
"name": "GSPC.Close",
"price":  93.39,
"rsi": 56.291,
"ret": -0.0016036 
},
{
 "date":   2015,
"name": "GSPC.Close",
"price":   94.8,
"rsi": 55.161,
"ret": 0.015098 
},
{
 "date":   2016,
"name": "GSPC.Close",
"price":  94.81,
"rsi": 62.733,
"ret": 0.00010549 
},
{
 "date":   2017,
"name": "GSPC.Close",
"price":  94.66,
"rsi": 62.781,
"ret": -0.0015821 
},
{
 "date":   2020,
"name": "GSPC.Close",
"price":  95.19,
"rsi": 61.501,
"ret": 0.005599 
},
{
 "date":   2021,
"name": "GSPC.Close",
"price":  95.61,
"rsi": 64.272,
"ret": 0.0044122 
},
{
 "date":   2022,
"name": "GSPC.Close",
"price":  94.61,
"rsi":  66.34,
"ret": -0.010459 
},
{
 "date":   2023,
"name": "GSPC.Close",
"price":  93.63,
"rsi": 57.768,
"ret": -0.010358 
},
{
 "date":   2024,
"name": "GSPC.Close",
"price":   93.2,
"rsi": 50.835,
"ret": -0.0045925 
},
{
 "date":   2027,
"name": "GSPC.Close",
"price":  92.44,
"rsi": 48.107,
"ret": -0.0081545 
},
{
 "date":   2028,
"name": "GSPC.Close",
"price":  91.45,
"rsi": 43.649,
"ret": -0.01071 
},
{
 "date":   2029,
"name": "GSPC.Close",
"price":  90.18,
"rsi": 38.627,
"ret": -0.013887 
},
{
 "date":   2030,
"name": "GSPC.Close",
"price":  90.07,
"rsi": 33.329,
"ret": -0.0012198 
},
{
 "date":   2031,
"name": "GSPC.Close",
"price":  89.29,
"rsi": 32.908,
"ret": -0.0086599 
},
{
 "date":   2034,
"name": "GSPC.Close",
"price":  88.69,
"rsi": 30.013,
"ret": -0.0067197 
},
{
 "date":   2035,
"name": "GSPC.Close",
"price":  88.19,
"rsi": 27.975,
"ret": -0.0056376 
},
{
 "date":   2036,
"name": "GSPC.Close",
"price":  88.83,
"rsi": 26.367,
"ret": 0.0072571 
},
{
 "date":   2037,
"name": "GSPC.Close",
"price":  88.75,
"rsi": 31.771,
"ret": -0.0009006 
},
{
 "date":   2038,
"name": "GSPC.Close",
"price":  87.99,
"rsi":  31.46,
"ret": -0.0085634 
},
{
 "date":   2041,
"name": "GSPC.Close",
"price":  87.15,
"rsi": 28.598,
"ret": -0.0095465 
},
{
 "date":   2042,
"name": "GSPC.Close",
"price":  86.23,
"rsi": 25.804,
"ret": -0.010557 
},
{
 "date":   2043,
"name": "GSPC.Close",
"price":  86.25,
"rsi": 23.137,
"ret": 0.00023194 
},
{
 "date":   2044,
"name": "GSPC.Close",
"price":   86.3,
"rsi": 23.323,
"ret": 0.00057971 
},
{
 "date":   2045,
"name": "GSPC.Close",
"price":  86.02,
"rsi": 23.818,
"ret": -0.0032445 
},
{
 "date":   2048,
"name": "GSPC.Close",
"price":  86.55,
"rsi": 22.925,
"ret": 0.0061614 
},
{
 "date":   2049,
"name": "GSPC.Close",
"price":  87.12,
"rsi": 28.395,
"ret": 0.0065858 
},
{
 "date":   2050,
"name": "GSPC.Close",
"price":  85.97,
"rsi": 33.834,
"ret": -0.0132 
},
{
 "date":   2051,
"name": "GSPC.Close",
"price":   85.6,
"rsi": 29.041,
"ret": -0.0043038 
},
{
 "date":   2052,
"name": "GSPC.Close",
"price":  86.36,
"rsi": 27.683,
"ret": 0.0088785 
},
{
 "date":   2055,
"name": "GSPC.Close",
"price":   86.2,
"rsi": 34.465,
"ret": -0.0018527 
},
{
 "date":   2056,
"name": "GSPC.Close",
"price":  84.95,
"rsi": 33.747,
"ret": -0.014501 
},
{
 "date":   2057,
"name": "GSPC.Close",
"price":  83.22,
"rsi": 28.717,
"ret": -0.020365 
},
{
 "date":   2058,
"name": "GSPC.Close",
"price":  83.07,
"rsi": 23.497,
"ret": -0.0018025 
},
{
 "date":   2059,
"name": "GSPC.Close",
"price":  84.28,
"rsi": 23.105,
"ret": 0.014566 
},
{
 "date":   2062,
"name": "GSPC.Close",
"price":  85.06,
"rsi": 32.842,
"ret": 0.0092549 
},
{
 "date":   2063,
"name": "GSPC.Close",
"price":  83.96,
"rsi": 38.269,
"ret": -0.012932 
},
{
 "date":   2064,
"name": "GSPC.Close",
"price":  84.43,
"rsi": 34.086,
"ret": 0.0055979 
},
{
 "date":   2065,
"name": "GSPC.Close",
"price":   86.4,
"rsi": 37.242,
"ret": 0.023333 
},
{
 "date":   2066,
"name": "GSPC.Close",
"price":  86.88,
"rsi": 48.397,
"ret": 0.0055556 
},
{
 "date":   2070,
"name": "GSPC.Close",
"price":  85.48,
"rsi": 50.696,
"ret": -0.016114 
},
{
 "date":   2071,
"name": "GSPC.Close",
"price":  86.03,
"rsi": 44.472,
"ret": 0.0064343 
},
{
 "date":   2072,
"name": "GSPC.Close",
"price":   86.2,
"rsi": 47.214,
"ret": 0.0019761 
},
{
 "date":   2073,
"name": "GSPC.Close",
"price":  85.62,
"rsi": 48.067,
"ret": -0.0067285 
},
{
 "date":   2076,
"name": "GSPC.Close",
"price":  85.89,
"rsi": 45.372,
"ret": 0.0031535 
},
{
 "date":   2077,
"name": "GSPC.Close",
"price":   84.6,
"rsi": 46.866,
"ret": -0.015019 
},
{
 "date":   2078,
"name": "GSPC.Close",
"price":  83.79,
"rsi": 41.084,
"ret": -0.0095745 
},
{
 "date":   2079,
"name": "GSPC.Close",
"price":  83.45,
"rsi": 37.921,
"ret": -0.0040578 
},
{
 "date":   2080,
"name": "GSPC.Close",
"price":   83.3,
"rsi": 36.646,
"ret": -0.0017975 
},
{
 "date":   2083,
"name": "GSPC.Close",
"price":  82.88,
"rsi":  36.07,
"ret": -0.005042 
},
{
 "date":   2084,
"name": "GSPC.Close",
"price":  82.09,
"rsi": 34.436,
"ret": -0.0095319 
},
{
 "date":   2085,
"name": "GSPC.Close",
"price":  82.37,
"rsi": 31.543,
"ret": 0.0034109 
},
{
 "date":   2086,
"name": "GSPC.Close",
"price":  84.06,
"rsi":  33.67,
"ret": 0.020517 
},
{
 "date":   2087,
"name": "GSPC.Close",
"price":  85.88,
"rsi": 44.815,
"ret": 0.021651 
},
{
 "date":   2090,
"name": "GSPC.Close",
"price":  85.07,
"rsi": 53.815,
"ret": -0.0094318 
},
{
 "date":   2091,
"name": "GSPC.Close",
"price":  84.94,
"rsi": 49.914,
"ret": -0.0015282 
},
{
 "date":   2092,
"name": "GSPC.Close",
"price":  85.74,
"rsi": 49.296,
"ret": 0.0094184 
},
{
 "date":   2093,
"name": "GSPC.Close",
"price":  85.64,
"rsi": 53.139,
"ret": -0.0011663 
},
{
 "date":   2094,
"name": "GSPC.Close",
"price":  86.19,
"rsi": 52.603,
"ret": 0.0064222 
},
{
 "date":   2097,
"name": "GSPC.Close",
"price":  85.03,
"rsi": 55.278,
"ret": -0.013459 
},
{
 "date":   2098,
"name": "GSPC.Close",
"price":  83.87,
"rsi": 48.996,
"ret": -0.013642 
},
{
 "date":   2099,
"name": "GSPC.Close",
"price":  82.93,
"rsi": 43.653,
"ret": -0.011208 
},
{
 "date":   2100,
"name": "GSPC.Close",
"price":  83.82,
"rsi":  39.86,
"ret": 0.010732 
},
{
 "date":   2101,
"name": "GSPC.Close",
"price":  85.95,
"rsi": 44.755,
"ret": 0.025412 
},
{
 "date":   2104,
"name": "GSPC.Close",
"price":  86.88,
"rsi": 54.334,
"ret": 0.01082 
},
{
 "date":   2105,
"name": "GSPC.Close",
"price":  86.77,
"rsi": 57.776,
"ret": -0.0012661 
},
{
 "date":   2106,
"name": "GSPC.Close",
"price":  87.94,
"rsi": 57.227,
"ret": 0.013484 
},
{
 "date":   2107,
"name": "GSPC.Close",
"price":  88.37,
"rsi": 61.429,
"ret": 0.0048897 
},
{
 "date":   2108,
"name": "GSPC.Close",
"price":  88.21,
"rsi": 62.873,
"ret": -0.0018106 
},
{
 "date":   2111,
"name": "GSPC.Close",
"price":  89.46,
"rsi": 61.944,
"ret": 0.014171 
},
{
 "date":   2112,
"name": "GSPC.Close",
"price":  89.28,
"rsi": 66.152,
"ret": -0.0020121 
},
{
 "date":   2113,
"name": "GSPC.Close",
"price":  89.23,
"rsi": 65.036,
"ret": -0.00056004 
},
{
 "date":   2114,
"name": "GSPC.Close",
"price":  89.37,
"rsi":  64.71,
"ret": 0.001569 
},
{
 "date":   2115,
"name": "GSPC.Close",
"price":  88.86,
"rsi": 65.236,
"ret": -0.0057066 
},
{
 "date":   2118,
"name": "GSPC.Close",
"price":  89.82,
"rsi": 61.632,
"ret": 0.010804 
},
{
 "date":   2119,
"name": "GSPC.Close",
"price":  90.56,
"rsi": 65.496,
"ret": 0.0082387 
},
{
 "date":   2120,
"name": "GSPC.Close",
"price":  90.71,
"rsi": 68.158,
"ret": 0.0016564 
},
{
 "date":   2121,
"name": "GSPC.Close",
"price":  91.24,
"rsi": 68.686,
"ret": 0.0058428 
},
{
 "date":   2122,
"name": "GSPC.Close",
"price":  89.83,
"rsi": 70.542,
"ret": -0.015454 
},
{
 "date":   2125,
"name": "GSPC.Close",
"price":  89.73,
"rsi":   60.3,
"ret": -0.0011132 
},
{
 "date":   2126,
"name": "GSPC.Close",
"price":  90.51,
"rsi": 59.638,
"ret": 0.0086927 
},
{
 "date":   2127,
"name": "GSPC.Close",
"price":  89.39,
"rsi": 63.043,
"ret": -0.012374 
},
{
 "date":   2128,
"name": "GSPC.Close",
"price":  89.31,
"rsi": 55.768,
"ret": -0.00089495 
},
{
 "date":   2129,
"name": "GSPC.Close",
"price":  89.04,
"rsi": 55.278,
"ret": -0.0030232 
},
{
 "date":   2132,
"name": "GSPC.Close",
"price":  88.09,
"rsi": 53.565,
"ret": -0.010669 
},
{
 "date":   2133,
"name": "GSPC.Close",
"price":  88.51,
"rsi": 47.936,
"ret": 0.0047679 
},
{
 "date":   2134,
"name": "GSPC.Close",
"price":  89.15,
"rsi": 50.417,
"ret": 0.0072308 
},
{
 "date":   2135,
"name": "GSPC.Close",
"price":  89.55,
"rsi": 54.012,
"ret": 0.0044868 
},
{
 "date":   2136,
"name": "GSPC.Close",
"price":  89.33,
"rsi": 56.153,
"ret": -0.0024567 
},
{
 "date":   2139,
"name": "GSPC.Close",
"price":  89.34,
"rsi": 54.646,
"ret": 0.00011194 
},
{
 "date":   2140,
"name": "GSPC.Close",
"price":  89.87,
"rsi": 54.706,
"ret": 0.0059324 
},
{
 "date":   2141,
"name": "GSPC.Close",
"price":  91.19,
"rsi":  57.86,
"ret": 0.014688 
},
{
 "date":   2142,
"name": "GSPC.Close",
"price":  91.04,
"rsi": 64.492,
"ret": -0.0016449 
},
{
 "date":   2143,
"name": "GSPC.Close",
"price":  90.97,
"rsi": 63.274,
"ret": -0.00076889 
},
{
 "date":   2146,
"name": "GSPC.Close",
"price":  91.46,
"rsi": 62.678,
"ret": 0.0053864 
},
{
 "date":   2147,
"name": "GSPC.Close",
"price":     91,
"rsi":  65.15,
"ret": -0.0050295 
},
{
 "date":   2148,
"name": "GSPC.Close",
"price":  89.98,
"rsi": 61.062,
"ret": -0.011209 
},
{
 "date":   2149,
"name": "GSPC.Close",
"price":  89.64,
"rsi": 53.105,
"ret": -0.0037786 
},
{
 "date":   2150,
"name": "GSPC.Close",
"price":  89.53,
"rsi": 50.731,
"ret": -0.0012271 
},
{
 "date":   2153,
"name": "GSPC.Close",
"price":   89.7,
"rsi": 49.954,
"ret": 0.0018988 
},
{
 "date":   2154,
"name": "GSPC.Close",
"price":  90.71,
"rsi": 51.199,
"ret": 0.01126 
},
{
 "date":   2155,
"name": "GSPC.Close",
"price":  90.94,
"rsi": 57.901,
"ret": 0.0025356 
},
{
 "date":   2157,
"name": "GSPC.Close",
"price":  91.24,
"rsi": 59.273,
"ret": 0.0032989 
},
{
 "date":   2160,
"name": "GSPC.Close",
"price":  90.67,
"rsi": 61.055,
"ret": -0.0062473 
},
{
 "date":   2161,
"name": "GSPC.Close",
"price":  89.33,
"rsi": 56.037,
"ret": -0.014779 
},
{
 "date":   2162,
"name": "GSPC.Close",
"price":   87.6,
"rsi": 46.385,
"ret": -0.019366 
},
{
 "date":   2163,
"name": "GSPC.Close",
"price":  87.84,
"rsi": 37.423,
"ret": 0.0027397 
},
{
 "date":   2164,
"name": "GSPC.Close",
"price":  86.82,
"rsi": 39.179,
"ret": -0.011612 
},
{
 "date":   2167,
"name": "GSPC.Close",
"price":  87.07,
"rsi":  34.72,
"ret": 0.0028795 
},
{
 "date":   2168,
"name": "GSPC.Close",
"price":   87.3,
"rsi": 36.624,
"ret": 0.0026416 
},
{
 "date":   2169,
"name": "GSPC.Close",
"price":  88.08,
"rsi": 38.404,
"ret": 0.0089347 
},
{
 "date":   2170,
"name": "GSPC.Close",
"price":   87.8,
"rsi": 44.133,
"ret": -0.0031789 
},
{
 "date":   2171,
"name": "GSPC.Close",
"price":  87.83,
"rsi": 42.601,
"ret": 0.00034169 
},
{
 "date":   2174,
"name": "GSPC.Close",
"price":  88.09,
"rsi":  42.83,
"ret": 0.0029603 
},
{
 "date":   2175,
"name": "GSPC.Close",
"price":  88.93,
"rsi": 44.882,
"ret": 0.0095357 
},
{
 "date":   2176,
"name": "GSPC.Close",
"price":  89.15,
"rsi": 51.001,
"ret": 0.0024739 
},
{
 "date":   2177,
"name": "GSPC.Close",
"price":  89.43,
"rsi": 52.489,
"ret": 0.0031408 
},
{
 "date":   2178,
"name": "GSPC.Close",
"price":   88.8,
"rsi": 54.387,
"ret": -0.0070446 
},
{
 "date":   2181,
"name": "GSPC.Close",
"price":  88.14,
"rsi": 49.587,
"ret": -0.0074324 
},
{
 "date":   2182,
"name": "GSPC.Close",
"price":  88.73,
"rsi": 45.096,
"ret": 0.0066939 
},
{
 "date":   2183,
"name": "GSPC.Close",
"price":  89.46,
"rsi": 49.499,
"ret": 0.0082272 
},
{
 "date":   2185,
"name": "GSPC.Close",
"price":  90.25,
"rsi": 54.374,
"ret": 0.0088308 
},
{
 "date":   2188,
"name": "GSPC.Close",
"price":  90.13,
"rsi": 58.989,
"ret": -0.0013296 
},
{
 "date":   2189,
"name": "GSPC.Close",
"price":  89.77,
"rsi": 58.029,
"ret": -0.0039942 
},
{
 "date":   2190,
"name": "GSPC.Close",
"price":  90.19,
"rsi":  55.13,
"ret": 0.0046786 
},
{
 "date":   2192,
"name": "GSPC.Close",
"price":   90.9,
"rsi":  57.78,
"ret": 0.0078723 
},
{
 "date":   2195,
"name": "GSPC.Close",
"price":  92.58,
"rsi": 61.878,
"ret": 0.018482 
},
{
 "date":   2196,
"name": "GSPC.Close",
"price":  93.53,
"rsi": 69.438,
"ret": 0.010261 
},
{
 "date":   2197,
"name": "GSPC.Close",
"price":  93.95,
"rsi": 72.731,
"ret": 0.0044905 
},
{
 "date":   2198,
"name": "GSPC.Close",
"price":  94.58,
"rsi": 74.062,
"ret": 0.0067057 
},
{
 "date":   2199,
"name": "GSPC.Close",
"price":  94.95,
"rsi": 75.957,
"ret": 0.003912 
},
{
 "date":   2202,
"name": "GSPC.Close",
"price":  96.33,
"rsi": 77.019,
"ret": 0.014534 
},
{
 "date":   2203,
"name": "GSPC.Close",
"price":  95.57,
"rsi": 80.482,
"ret": -0.0078895 
},
{
 "date":   2204,
"name": "GSPC.Close",
"price":  97.13,
"rsi": 73.879,
"ret": 0.016323 
},
{
 "date":   2205,
"name": "GSPC.Close",
"price":  96.61,
"rsi": 77.889,
"ret": -0.0053536 
},
{
 "date":   2206,
"name": "GSPC.Close",
"price":     97,
"rsi": 73.821,
"ret": 0.0040368 
},
{
 "date":   2209,
"name": "GSPC.Close",
"price":  98.32,
"rsi": 74.881,
"ret": 0.013608 
},
{
 "date":   2210,
"name": "GSPC.Close",
"price":  98.86,
"rsi":  78.11,
"ret": 0.0054923 
},
{
 "date":   2211,
"name": "GSPC.Close",
"price":  98.24,
"rsi": 79.284,
"ret": -0.0062715 
},
{
 "date":   2212,
"name": "GSPC.Close",
"price":  98.04,
"rsi": 74.355,
"ret": -0.0020358 
},
{
 "date":   2213,
"name": "GSPC.Close",
"price":  99.21,
"rsi": 72.784,
"ret": 0.011934 
},
{
 "date":   2216,
"name": "GSPC.Close",
"price":  99.68,
"rsi": 75.982,
"ret": 0.0047374 
},
{
 "date":   2217,
"name": "GSPC.Close",
"price":  99.07,
"rsi": 77.144,
"ret": -0.0061196 
},
{
 "date":   2218,
"name": "GSPC.Close",
"price":  98.53,
"rsi": 72.258,
"ret": -0.0054507 
},
{
 "date":   2219,
"name": "GSPC.Close",
"price": 100.11,
"rsi": 68.143,
"ret": 0.016036 
},
{
 "date":   2220,
"name": "GSPC.Close",
"price": 100.86,
"rsi":  72.99,
"ret": 0.0074918 
},
{
 "date":   2223,
"name": "GSPC.Close",
"price": 100.87,
"rsi": 74.939,
"ret": 9.9147e-05 
},
{
 "date":   2224,
"name": "GSPC.Close",
"price": 101.18,
"rsi": 74.965,
"ret": 0.0030733 
},
{
 "date":   2225,
"name": "GSPC.Close",
"price": 101.91,
"rsi": 75.801,
"ret": 0.0072149 
},
{
 "date":   2226,
"name": "GSPC.Close",
"price": 100.39,
"rsi": 77.691,
"ret": -0.014915 
},
{
 "date":   2227,
"name": "GSPC.Close",
"price":  99.46,
"rsi": 66.114,
"ret": -0.0092639 
},
{
 "date":   2230,
"name": "GSPC.Close",
"price":  99.62,
"rsi": 60.203,
"ret": 0.0016087 
},
{
 "date":   2231,
"name": "GSPC.Close",
"price": 100.47,
"rsi": 60.851,
"ret": 0.0085324 
},
{
 "date":   2232,
"name": "GSPC.Close",
"price": 100.77,
"rsi":  64.19,
"ret": 0.002986 
},
{
 "date":   2233,
"name": "GSPC.Close",
"price": 100.25,
"rsi": 65.314,
"ret": -0.0051603 
},
{
 "date":   2234,
"name": "GSPC.Close",
"price":  99.67,
"rsi": 61.698,
"ret": -0.0057855 
},
{
 "date":   2238,
"name": "GSPC.Close",
"price":  99.05,
"rsi": 57.851,
"ret": -0.0062205 
},
{
 "date":   2239,
"name": "GSPC.Close",
"price":  99.85,
"rsi": 53.977,
"ret": 0.0080767 
},
{
 "date":   2240,
"name": "GSPC.Close",
"price": 101.41,
"rsi": 57.895,
"ret": 0.015623 
},
{
 "date":   2241,
"name": "GSPC.Close",
"price":  102.1,
"rsi": 64.281,
"ret": 0.0068041 
},
{
 "date":   2244,
"name": "GSPC.Close",
"price": 101.61,
"rsi": 66.688,
"ret": -0.0047992 
},
{
 "date":   2245,
"name": "GSPC.Close",
"price": 102.03,
"rsi":  63.42,
"ret": 0.0041335 
},
{
 "date":   2246,
"name": "GSPC.Close",
"price": 101.69,
"rsi": 65.003,
"ret": -0.0033324 
},
{
 "date":   2247,
"name": "GSPC.Close",
"price": 100.11,
"rsi":  62.64,
"ret": -0.015537 
},
{
 "date":   2248,
"name": "GSPC.Close",
"price":  99.71,
"rsi": 52.997,
"ret": -0.0039956 
},
{
 "date":   2251,
"name": "GSPC.Close",
"price": 100.02,
"rsi": 50.862,
"ret": 0.003109 
},
{
 "date":   2252,
"name": "GSPC.Close",
"price": 100.58,
"rsi":  52.46,
"ret": 0.0055989 
},
{
 "date":   2253,
"name": "GSPC.Close",
"price":  99.98,
"rsi": 55.289,
"ret": -0.0059654 
},
{
 "date":   2254,
"name": "GSPC.Close",
"price":  98.92,
"rsi": 51.737,
"ret": -0.010602 
},
{
 "date":   2255,
"name": "GSPC.Close",
"price":  99.11,
"rsi": 46.101,
"ret": 0.0019207 
},
{
 "date":   2258,
"name": "GSPC.Close",
"price": 100.19,
"rsi": 47.211,
"ret": 0.010897 
},
{
 "date":   2259,
"name": "GSPC.Close",
"price": 100.58,
"rsi": 53.121,
"ret": 0.0038926 
},
{
 "date":   2260,
"name": "GSPC.Close",
"price": 100.94,
"rsi": 55.077,
"ret": 0.0035792 
},
{
 "date":   2261,
"name": "GSPC.Close",
"price": 101.89,
"rsi": 56.866,
"ret": 0.0094115 
},
{
 "date":   2262,
"name": "GSPC.Close",
"price": 100.86,
"rsi": 61.251,
"ret": -0.010109 
},
{
 "date":   2265,
"name": "GSPC.Close",
"price":   99.8,
"rsi": 54.752,
"ret": -0.01051 
},
{
 "date":   2266,
"name": "GSPC.Close",
"price": 100.92,
"rsi": 48.991,
"ret": 0.011222 
},
{
 "date":   2267,
"name": "GSPC.Close",
"price": 100.86,
"rsi": 54.445,
"ret": -0.00059453 
},
{
 "date":   2268,
"name": "GSPC.Close",
"price": 100.45,
"rsi": 54.111,
"ret": -0.004065 
},
{
 "date":   2269,
"name": "GSPC.Close",
"price": 100.58,
"rsi": 51.775,
"ret": 0.0012942 
},
{
 "date":   2272,
"name": "GSPC.Close",
"price": 100.71,
"rsi": 52.476,
"ret": 0.0012925 
},
{
 "date":   2273,
"name": "GSPC.Close",
"price": 102.24,
"rsi": 53.208,
"ret": 0.015192 
},
{
 "date":   2274,
"name": "GSPC.Close",
"price": 103.42,
"rsi": 60.851,
"ret": 0.011541 
},
{
 "date":   2275,
"name": "GSPC.Close",
"price": 102.85,
"rsi": 65.528,
"ret": -0.0055115 
},
{
 "date":   2276,
"name": "GSPC.Close",
"price": 102.85,
"rsi": 61.694,
"ret":      0 
},
{
 "date":   2279,
"name": "GSPC.Close",
"price": 102.41,
"rsi": 61.694,
"ret": -0.0042781 
},
{
 "date":   2280,
"name": "GSPC.Close",
"price": 102.01,
"rsi": 58.623,
"ret": -0.0039059 
},
{
 "date":   2281,
"name": "GSPC.Close",
"price": 102.77,
"rsi": 55.899,
"ret": 0.0074502 
},
{
 "date":   2282,
"name": "GSPC.Close",
"price": 102.24,
"rsi": 59.728,
"ret": -0.0051571 
},
{
 "date":   2283,
"name": "GSPC.Close",
"price": 102.25,
"rsi": 56.072,
"ret": 9.7809e-05 
},
{
 "date":   2286,
"name": "GSPC.Close",
"price": 103.51,
"rsi": 56.127,
"ret": 0.012323 
},
{
 "date":   2287,
"name": "GSPC.Close",
"price": 103.36,
"rsi": 62.455,
"ret": -0.0014491 
},
{
 "date":   2288,
"name": "GSPC.Close",
"price": 102.21,
"rsi": 61.321,
"ret": -0.011126 
},
{
 "date":   2289,
"name": "GSPC.Close",
"price": 101.28,
"rsi": 53.327,
"ret": -0.0090989 
},
{
 "date":   2290,
"name": "GSPC.Close",
"price": 100.35,
"rsi": 47.889,
"ret": -0.0091825 
},
{
 "date":   2293,
"name": "GSPC.Close",
"price":  100.2,
"rsi": 43.151,
"ret": -0.0014948 
},
{
 "date":   2294,
"name": "GSPC.Close",
"price": 101.05,
"rsi": 42.422,
"ret": 0.008483 
},
{
 "date":   2295,
"name": "GSPC.Close",
"price": 100.31,
"rsi": 47.804,
"ret": -0.0073231 
},
{
 "date":   2296,
"name": "GSPC.Close",
"price": 100.67,
"rsi": 43.952,
"ret": 0.0035889 
},
{
 "date":   2300,
"name": "GSPC.Close",
"price": 101.44,
"rsi": 46.222,
"ret": 0.0076488 
},
{
 "date":   2301,
"name": "GSPC.Close",
"price": 102.87,
"rsi": 50.811,
"ret": 0.014097 
},
{
 "date":   2302,
"name": "GSPC.Close",
"price": 103.32,
"rsi": 57.982,
"ret": 0.0043745 
},
{
 "date":   2303,
"name": "GSPC.Close",
"price": 102.98,
"rsi":  59.96,
"ret": -0.0032907 
},
{
 "date":   2304,
"name": "GSPC.Close",
"price": 102.29,
"rsi": 57.748,
"ret": -0.0067003 
},
{
 "date":   2307,
"name": "GSPC.Close",
"price": 102.43,
"rsi": 53.439,
"ret": 0.0013687 
},
{
 "date":   2308,
"name": "GSPC.Close",
"price": 101.86,
"rsi": 54.186,
"ret": -0.0055648 
},
{
 "date":   2309,
"name": "GSPC.Close",
"price": 102.13,
"rsi": 50.625,
"ret": 0.0026507 
},
{
 "date":   2310,
"name": "GSPC.Close",
"price": 102.13,
"rsi": 52.227,
"ret":      0 
},
{
 "date":   2311,
"name": "GSPC.Close",
"price": 101.64,
"rsi": 52.227,
"ret": -0.0047978 
},
{
 "date":   2314,
"name": "GSPC.Close",
"price": 100.92,
"rsi": 48.889,
"ret": -0.0070838 
},
{
 "date":   2315,
"name": "GSPC.Close",
"price": 101.46,
"rsi": 44.399,
"ret": 0.0053508 
},
{
 "date":   2316,
"name": "GSPC.Close",
"price": 100.88,
"rsi": 48.239,
"ret": -0.0057165 
},
{
 "date":   2317,
"name": "GSPC.Close",
"price": 101.16,
"rsi":  44.67,
"ret": 0.0027756 
},
{
 "date":   2318,
"name": "GSPC.Close",
"price": 101.88,
"rsi": 46.719,
"ret": 0.0071174 
},
{
 "date":   2321,
"name": "GSPC.Close",
"price":  103.1,
"rsi": 51.675,
"ret": 0.011975 
},
{
 "date":   2322,
"name": "GSPC.Close",
"price": 102.95,
"rsi": 58.687,
"ret": -0.0014549 
},
{
 "date":   2323,
"name": "GSPC.Close",
"price": 102.77,
"rsi": 57.581,
"ret": -0.0017484 
},
{
 "date":   2324,
"name": "GSPC.Close",
"price": 102.16,
"rsi": 56.212,
"ret": -0.0059356 
},
{
 "date":   2325,
"name": "GSPC.Close",
"price": 101.34,
"rsi": 51.722,
"ret": -0.0080266 
},
{
 "date":   2328,
"name": "GSPC.Close",
"price": 101.09,
"rsi": 46.362,
"ret": -0.0024669 
},
{
 "date":   2329,
"name": "GSPC.Close",
"price": 101.26,
"rsi": 44.837,
"ret": 0.0016817 
},
{
 "date":   2330,
"name": "GSPC.Close",
"price": 101.18,
"rsi": 46.135,
"ret": -0.00079005 
},
{
 "date":   2331,
"name": "GSPC.Close",
"price":    102,
"rsi": 45.591,
"ret": 0.0081044 
},
{
 "date":   2332,
"name": "GSPC.Close",
"price": 101.26,
"rsi": 51.854,
"ret": -0.0072549 
},
{
 "date":   2335,
"name": "GSPC.Close",
"price":  99.44,
"rsi": 46.637,
"ret": -0.017974 
},
{
 "date":   2336,
"name": "GSPC.Close",
"price":  99.49,
"rsi": 36.824,
"ret": 0.00050282 
},
{
 "date":   2337,
"name": "GSPC.Close",
"price":  99.34,
"rsi": 37.215,
"ret": -0.0015077 
},
{
 "date":   2338,
"name": "GSPC.Close",
"price":  99.38,
"rsi": 36.486,
"ret": 0.00040266 
},
{
 "date":   2339,
"name": "GSPC.Close",
"price": 100.18,
"rsi": 36.841,
"ret": 0.0080499 
},
{
 "date":   2343,
"name": "GSPC.Close",
"price":  99.85,
"rsi": 43.635,
"ret": -0.0032941 
},
{
 "date":   2344,
"name": "GSPC.Close",
"price": 100.22,
"rsi": 41.645,
"ret": 0.0037056 
},
{
 "date":   2345,
"name": "GSPC.Close",
"price": 100.13,
"rsi":  44.69,
"ret": -0.00089802 
},
{
 "date":   2346,
"name": "GSPC.Close",
"price":  99.15,
"rsi": 44.088,
"ret": -0.0097873 
},
{
 "date":   2349,
"name": "GSPC.Close",
"price":  98.63,
"rsi": 38.067,
"ret": -0.0052446 
},
{
 "date":   2350,
"name": "GSPC.Close",
"price":   98.8,
"rsi": 35.311,
"ret": 0.0017236 
},
{
 "date":   2351,
"name": "GSPC.Close",
"price":  98.74,
"rsi": 36.919,
"ret": -0.00060729 
},
{
 "date":   2352,
"name": "GSPC.Close",
"price":  99.56,
"rsi": 36.574,
"ret": 0.0083046 
},
{
 "date":   2353,
"name": "GSPC.Close",
"price": 100.92,
"rsi": 44.252,
"ret": 0.01366 
},
{
 "date":   2356,
"name": "GSPC.Close",
"price": 101.95,
"rsi": 54.162,
"ret": 0.010206 
},
{
 "date":   2357,
"name": "GSPC.Close",
"price": 101.46,
"rsi": 59.967,
"ret": -0.0048063 
},
{
 "date":   2358,
"name": "GSPC.Close",
"price": 102.01,
"rsi": 56.313,
"ret": 0.0054209 
},
{
 "date":   2359,
"name": "GSPC.Close",
"price": 103.61,
"rsi":  59.31,
"ret": 0.015685 
},
{
 "date":   2360,
"name": "GSPC.Close",
"price": 103.76,
"rsi": 66.508,
"ret": 0.0014477 
},
{
 "date":   2363,
"name": "GSPC.Close",
"price": 104.28,
"rsi": 67.095,
"ret": 0.0050116 
},
{
 "date":   2364,
"name": "GSPC.Close",
"price": 103.47,
"rsi": 69.118,
"ret": -0.0077675 
},
{
 "date":   2365,
"name": "GSPC.Close",
"price": 103.25,
"rsi": 62.657,
"ret": -0.0021262 
},
{
 "date":   2366,
"name": "GSPC.Close",
"price": 103.79,
"rsi": 60.989,
"ret": 0.00523 
},
{
 "date":   2367,
"name": "GSPC.Close",
"price": 103.72,
"rsi": 63.553,
"ret": -0.00067444 
},
{
 "date":   2370,
"name": "GSPC.Close",
"price": 103.43,
"rsi": 62.975,
"ret": -0.002796 
},
{
 "date":   2371,
"name": "GSPC.Close",
"price": 103.86,
"rsi":  60.52,
"ret": 0.0041574 
},
{
 "date":   2372,
"name": "GSPC.Close",
"price": 104.28,
"rsi": 62.834,
"ret": 0.0040439 
},
{
 "date":   2373,
"name": "GSPC.Close",
"price": 103.59,
"rsi": 64.992,
"ret": -0.0066168 
},
{
 "date":   2374,
"name": "GSPC.Close",
"price": 104.11,
"rsi": 58.937,
"ret": 0.0050198 
},
{
 "date":   2378,
"name": "GSPC.Close",
"price": 103.54,
"rsi": 61.824,
"ret": -0.005475 
},
{
 "date":   2379,
"name": "GSPC.Close",
"price": 103.83,
"rsi": 57.087,
"ret": 0.0028008 
},
{
 "date":   2380,
"name": "GSPC.Close",
"price": 103.98,
"rsi": 58.816,
"ret": 0.0014447 
},
{
 "date":   2381,
"name": "GSPC.Close",
"price": 104.98,
"rsi":  59.72,
"ret": 0.0096172 
},
{
 "date":   2384,
"name": "GSPC.Close",
"price":  105.9,
"rsi": 65.203,
"ret": 0.0087636 
},
{
 "date":   2385,
"name": "GSPC.Close",
"price": 105.67,
"rsi": 69.339,
"ret": -0.0021719 
},
{
 "date":   2386,
"name": "GSPC.Close",
"price": 105.95,
"rsi": 67.189,
"ret": 0.0026498 
},
{
 "date":   2387,
"name": "GSPC.Close",
"price":  105.2,
"rsi": 68.471,
"ret": -0.0070788 
},
{
 "date":   2388,
"name": "GSPC.Close",
"price": 104.68,
"rsi": 61.537,
"ret": -0.004943 
},
{
 "date":   2391,
"name": "GSPC.Close",
"price": 104.29,
"rsi": 57.211,
"ret": -0.0037256 
},
{
 "date":   2392,
"name": "GSPC.Close",
"price": 103.72,
"rsi": 54.137,
"ret": -0.0054655 
},
{
 "date":   2393,
"name": "GSPC.Close",
"price": 103.82,
"rsi": 49.916,
"ret": 0.00096413 
},
{
 "date":   2394,
"name": "GSPC.Close",
"price": 103.93,
"rsi": 50.643,
"ret": 0.0010595 
},
{
 "date":   2395,
"name": "GSPC.Close",
"price": 104.06,
"rsi": 51.477,
"ret": 0.0012508 
},
{
 "date":   2398,
"name": "GSPC.Close",
"price": 104.07,
"rsi": 52.499,
"ret": 9.6098e-05 
},
{
 "date":   2399,
"name": "GSPC.Close",
"price": 103.48,
"rsi": 52.582,
"ret": -0.0056693 
},
{
 "date":   2400,
"name": "GSPC.Close",
"price": 103.05,
"rsi": 47.342,
"ret": -0.0041554 
},
{
 "date":   2401,
"name": "GSPC.Close",
"price": 102.93,
"rsi": 43.908,
"ret": -0.0011645 
},
{
 "date":   2402,
"name": "GSPC.Close",
"price": 103.44,
"rsi": 42.971,
"ret": 0.0049548 
},
{
 "date":   2405,
"name": "GSPC.Close",
"price": 103.19,
"rsi": 48.045,
"ret": -0.0024169 
},
{
 "date":   2406,
"name": "GSPC.Close",
"price": 104.14,
"rsi": 45.889,
"ret": 0.0092063 
},
{
 "date":   2407,
"name": "GSPC.Close",
"price": 104.43,
"rsi": 54.282,
"ret": 0.0027847 
},
{
 "date":   2408,
"name": "GSPC.Close",
"price": 103.85,
"rsi":   56.5,
"ret": -0.005554 
},
{
 "date":   2409,
"name": "GSPC.Close",
"price": 103.79,
"rsi": 51.155,
"ret": -0.00057776 
},
{
 "date":   2412,
"name": "GSPC.Close",
"price": 103.49,
"rsi": 50.621,
"ret": -0.0028905 
},
{
 "date":   2413,
"name": "GSPC.Close",
"price": 104.41,
"rsi": 47.929,
"ret": 0.0088897 
},
{
 "date":   2414,
"name": "GSPC.Close",
"price": 104.06,
"rsi": 55.708,
"ret": -0.0033522 
},
{
 "date":   2415,
"name": "GSPC.Close",
"price": 104.22,
"rsi": 52.495,
"ret": 0.0015376 
},
{
 "date":   2416,
"name": "GSPC.Close",
"price": 104.25,
"rsi": 53.807,
"ret": 0.00028785 
},
{
 "date":   2419,
"name": "GSPC.Close",
"price": 104.43,
"rsi": 54.063,
"ret": 0.0017266 
},
{
 "date":   2420,
"name": "GSPC.Close",
"price":  104.8,
"rsi": 55.651,
"ret": 0.003543 
},
{
 "date":   2421,
"name": "GSPC.Close",
"price": 104.56,
"rsi": 58.805,
"ret": -0.0022901 
},
{
 "date":   2422,
"name": "GSPC.Close",
"price": 103.39,
"rsi": 56.022,
"ret": -0.01119 
},
{
 "date":   2423,
"name": "GSPC.Close",
"price": 102.37,
"rsi": 44.873,
"ret": -0.0098656 
},
{
 "date":   2426,
"name": "GSPC.Close",
"price": 101.96,
"rsi": 37.809,
"ret": -0.0040051 
},
{
 "date":   2427,
"name": "GSPC.Close",
"price": 101.27,
"rsi": 35.397,
"ret": -0.0067674 
},
{
 "date":   2428,
"name": "GSPC.Close",
"price": 102.03,
"rsi": 31.728,
"ret": 0.0075047 
},
{
 "date":   2429,
"name": "GSPC.Close",
"price": 101.32,
"rsi": 39.203,
"ret": -0.0069587 
},
{
 "date":   2430,
"name": "GSPC.Close",
"price": 101.48,
"rsi": 35.313,
"ret": 0.0015792 
},
{
 "date":   2433,
"name": "GSPC.Close",
"price": 102.07,
"rsi": 36.834,
"ret": 0.005814 
},
{
 "date":   2434,
"name": "GSPC.Close",
"price": 102.91,
"rsi": 42.228,
"ret": 0.0082296 
},
{
 "date":   2435,
"name": "GSPC.Close",
"price": 104.06,
"rsi": 48.917,
"ret": 0.011175 
},
{
 "date":   2436,
"name": "GSPC.Close",
"price": 103.92,
"rsi": 56.365,
"ret": -0.0013454 
},
{
 "date":   2437,
"name": "GSPC.Close",
"price":  104.3,
"rsi": 55.308,
"ret": 0.0036567 
},
{
 "date":   2441,
"name": "GSPC.Close",
"price": 105.03,
"rsi": 57.631,
"ret": 0.006999 
},
{
 "date":   2442,
"name": "GSPC.Close",
"price": 104.94,
"rsi": 61.745,
"ret": -0.0008569 
},
{
 "date":   2443,
"name": "GSPC.Close",
"price":  104.4,
"rsi": 60.959,
"ret": -0.0051458 
},
{
 "date":   2444,
"name": "GSPC.Close",
"price": 104.65,
"rsi": 56.327,
"ret": 0.0023946 
},
{
 "date":   2447,
"name": "GSPC.Close",
"price": 104.29,
"rsi": 57.921,
"ret": -0.00344 
},
{
 "date":   2448,
"name": "GSPC.Close",
"price": 103.94,
"rsi": 54.818,
"ret": -0.003356 
},
{
 "date":   2449,
"name": "GSPC.Close",
"price": 104.25,
"rsi": 51.906,
"ret": 0.0029825 
},
{
 "date":   2450,
"name": "GSPC.Close",
"price": 105.34,
"rsi": 54.225,
"ret": 0.010456 
},
{
 "date":   2451,
"name": "GSPC.Close",
"price": 106.27,
"rsi": 61.293,
"ret": 0.0088286 
},
{
 "date":   2454,
"name": "GSPC.Close",
"price": 106.32,
"rsi": 66.102,
"ret": 0.0004705 
},
{
 "date":   2455,
"name": "GSPC.Close",
"price": 107.83,
"rsi": 66.344,
"ret": 0.014202 
},
{
 "date":   2456,
"name": "GSPC.Close",
"price": 107.46,
"rsi": 72.688,
"ret": -0.0034313 
},
{
 "date":   2457,
"name": "GSPC.Close",
"price": 106.92,
"rsi": 69.244,
"ret": -0.0050251 
},
{
 "date":   2458,
"name": "GSPC.Close",
"price":  106.8,
"rsi": 64.444,
"ret": -0.0011223 
},
{
 "date":   2461,
"name": "GSPC.Close",
"price": 107.27,
"rsi": 63.393,
"ret": 0.0044007 
},
{
 "date":   2462,
"name": "GSPC.Close",
"price": 105.92,
"rsi":  65.75,
"ret": -0.012585 
},
{
 "date":   2463,
"name": "GSPC.Close",
"price": 105.37,
"rsi": 54.829,
"ret": -0.0051926 
},
{
 "date":   2464,
"name": "GSPC.Close",
"price": 105.24,
"rsi": 51.105,
"ret": -0.0012337 
},
{
 "date":   2465,
"name": "GSPC.Close",
"price": 104.17,
"rsi": 50.236,
"ret": -0.010167 
},
{
 "date":   2468,
"name": "GSPC.Close",
"price": 104.03,
"rsi": 43.659,
"ret": -0.001344 
},
{
 "date":   2469,
"name": "GSPC.Close",
"price": 103.23,
"rsi": 42.868,
"ret": -0.0076901 
},
{
 "date":   2470,
"name": "GSPC.Close",
"price": 102.97,
"rsi": 38.568,
"ret": -0.0025186 
},
{
 "date":   2471,
"name": "GSPC.Close",
"price": 103.54,
"rsi":  37.26,
"ret": 0.0055356 
},
{
 "date":   2472,
"name": "GSPC.Close",
"price": 102.56,
"rsi": 41.911,
"ret": -0.0094649 
},
{
 "date":   2475,
"name": "GSPC.Close",
"price": 101.64,
"rsi": 36.853,
"ret": -0.0089704 
},
{
 "date":   2476,
"name": "GSPC.Close",
"price": 100.81,
"rsi": 32.845,
"ret": -0.0081661 
},
{
 "date":   2477,
"name": "GSPC.Close",
"price": 102.12,
"rsi": 29.707,
"ret": 0.012995 
},
{
 "date":   2478,
"name": "GSPC.Close",
"price": 100.85,
"rsi": 39.529,
"ret": -0.012436 
},
{
 "date":   2479,
"name": "GSPC.Close",
"price": 100.88,
"rsi": 34.496,
"ret": 0.00029747 
},
{
 "date":   2482,
"name": "GSPC.Close",
"price": 101.47,
"rsi": 34.708,
"ret": 0.0058485 
},
{
 "date":   2483,
"name": "GSPC.Close",
"price": 101.45,
"rsi": 38.886,
"ret": -0.0001971 
},
{
 "date":   2484,
"name": "GSPC.Close",
"price": 101.74,
"rsi": 38.796,
"ret": 0.0028586 
},
{
 "date":   2485,
"name": "GSPC.Close",
"price": 100.77,
"rsi": 40.945,
"ret": -0.0095341 
},
{
 "date":   2486,
"name": "GSPC.Close",
"price":  99.96,
"rsi": 36.347,
"ret": -0.0080381 
},
{
 "date":   2489,
"name": "GSPC.Close",
"price": 100.07,
"rsi": 33.013,
"ret": 0.0011004 
},
{
 "date":   2490,
"name": "GSPC.Close",
"price": 101.06,
"rsi":   33.9,
"ret": 0.0098931 
},
{
 "date":   2491,
"name": "GSPC.Close",
"price": 101.76,
"rsi": 41.416,
"ret": 0.0069266 
},
{
 "date":   2492,
"name": "GSPC.Close",
"price": 101.61,
"rsi": 46.084,
"ret": -0.0014741 
},
{
 "date":   2493,
"name": "GSPC.Close",
"price":  102.9,
"rsi": 45.252,
"ret": 0.012696 
},
{
 "date":   2496,
"name": "GSPC.Close",
"price":  103.1,
"rsi": 53.096,
"ret": 0.0019436 
},
{
 "date":   2498,
"name": "GSPC.Close",
"price": 101.92,
"rsi": 54.192,
"ret": -0.011445 
},
{
 "date":   2499,
"name": "GSPC.Close",
"price": 102.41,
"rsi": 47.187,
"ret": 0.0048077 
},
{
 "date":   2500,
"name": "GSPC.Close",
"price": 100.82,
"rsi": 50.073,
"ret": -0.015526 
},
{
 "date":   2503,
"name": "GSPC.Close",
"price":   99.6,
"rsi": 42.044,
"ret": -0.012101 
},
{
 "date":   2504,
"name": "GSPC.Close",
"price":  99.32,
"rsi": 37.126,
"ret": -0.0028112 
},
{
 "date":   2505,
"name": "GSPC.Close",
"price":  98.81,
"rsi": 36.082,
"ret": -0.0051349 
},
{
 "date":   2506,
"name": "GSPC.Close",
"price":  99.64,
"rsi": 34.197,
"ret": 0.0084 
},
{
 "date":   2507,
"name": "GSPC.Close",
"price":  99.24,
"rsi": 39.717,
"ret": -0.0040145 
},
{
 "date":   2510,
"name": "GSPC.Close",
"price":   99.9,
"rsi":  38.06,
"ret": 0.0066505 
},
{
 "date":   2511,
"name": "GSPC.Close",
"price": 100.04,
"rsi": 42.335,
"ret": 0.0014014 
},
{
 "date":   2512,
"name": "GSPC.Close",
"price": 100.61,
"rsi":  43.23,
"ret": 0.0056977 
},
{
 "date":   2513,
"name": "GSPC.Close",
"price": 101.89,
"rsi": 46.847,
"ret": 0.012722 
},
{
 "date":   2514,
"name": "GSPC.Close",
"price": 101.92,
"rsi": 53.944,
"ret": 0.00029444 
},
{
 "date":   2517,
"name": "GSPC.Close",
"price": 102.59,
"rsi": 54.099,
"ret": 0.0065738 
},
{
 "date":   2518,
"name": "GSPC.Close",
"price": 101.96,
"rsi":  57.53,
"ret": -0.0061409 
},
{
 "date":   2519,
"name": "GSPC.Close",
"price": 102.41,
"rsi": 53.482,
"ret": 0.0044135 
},
{
 "date":   2521,
"name": "GSPC.Close",
"price": 103.15,
"rsi":  55.87,
"ret": 0.0072259 
},
{
 "date":   2524,
"name": "GSPC.Close",
"price": 102.44,
"rsi": 59.549,
"ret": -0.0068832 
},
{
 "date":   2525,
"name": "GSPC.Close",
"price":  102.1,
"rsi": 54.827,
"ret": -0.003319 
},
{
 "date":   2526,
"name": "GSPC.Close",
"price": 102.49,
"rsi": 52.673,
"ret": 0.0038198 
},
{
 "date":   2527,
"name": "GSPC.Close",
"price": 102.12,
"rsi": 54.863,
"ret": -0.0036101 
},
{
 "date":   2528,
"name": "GSPC.Close",
"price": 102.76,
"rsi": 52.386,
"ret": 0.0062671 
},
{
 "date":   2531,
"name": "GSPC.Close",
"price": 103.56,
"rsi":  56.08,
"ret": 0.0077851 
},
{
 "date":   2532,
"name": "GSPC.Close",
"price": 103.49,
"rsi": 60.233,
"ret": -0.00067594 
},
{
 "date":   2533,
"name": "GSPC.Close",
"price": 104.08,
"rsi": 59.701,
"ret": 0.005701 
},
{
 "date":   2534,
"name": "GSPC.Close",
"price": 104.51,
"rsi": 62.692,
"ret": 0.0041314 
},
{
 "date":   2535,
"name": "GSPC.Close",
"price":  104.7,
"rsi": 64.746,
"ret": 0.001818 
},
{
 "date":   2538,
"name": "GSPC.Close",
"price": 104.63,
"rsi": 65.646,
"ret": -0.00066858 
},
{
 "date":   2539,
"name": "GSPC.Close",
"price": 105.07,
"rsi": 64.988,
"ret": 0.0042053 
},
{
 "date":   2540,
"name": "GSPC.Close",
"price": 105.14,
"rsi": 67.213,
"ret": 0.00066622 
},
{
 "date":   2541,
"name": "GSPC.Close",
"price":  104.8,
"rsi": 67.566,
"ret": -0.0032338 
},
{
 "date":   2542,
"name": "GSPC.Close",
"price": 104.26,
"rsi": 63.962,
"ret": -0.0051527 
},
{
 "date":   2545,
"name": "GSPC.Close",
"price": 103.65,
"rsi": 58.615,
"ret": -0.0058508 
},
{
 "date":   2546,
"name": "GSPC.Close",
"price": 104.22,
"rsi": 53.204,
"ret": 0.0054993 
},
{
 "date":   2547,
"name": "GSPC.Close",
"price": 104.71,
"rsi": 57.182,
"ret": 0.0047016 
},
{
 "date":   2548,
"name": "GSPC.Close",
"price": 104.84,
"rsi": 60.305,
"ret": 0.0012415 
},
{
 "date":   2552,
"name": "GSPC.Close",
"price": 106.06,
"rsi": 61.116,
"ret": 0.011637 
},
{
 "date":   2553,
"name": "GSPC.Close",
"price": 106.77,
"rsi": 67.767,
"ret": 0.0066943 
},
{
 "date":   2554,
"name": "GSPC.Close",
"price": 106.34,
"rsi": 70.888,
"ret": -0.0040273 
},
{
 "date":   2555,
"name": "GSPC.Close",
"price": 106.88,
"rsi": 66.677,
"ret": 0.0050781 
},
{
 "date":   2556,
"name": "GSPC.Close",
"price": 107.46,
"rsi": 69.155,
"ret": 0.0054266 
},
{
 "date":   2559,
"name": "GSPC.Close",
"price":    107,
"rsi": 71.598,
"ret": -0.0042807 
},
{
 "date":   2560,
"name": "GSPC.Close",
"price":  105.7,
"rsi": 67.062,
"ret": -0.01215 
},
{
 "date":   2561,
"name": "GSPC.Close",
"price": 104.76,
"rsi":  56.22,
"ret": -0.0088931 
},
{
 "date":   2562,
"name": "GSPC.Close",
"price": 105.02,
"rsi": 49.934,
"ret": 0.0024819 
},
{
 "date":   2563,
"name": "GSPC.Close",
"price": 105.01,
"rsi": 51.548,
"ret": -9.522e-05 
},
{
 "date":   2566,
"name": "GSPC.Close",
"price":  105.2,
"rsi": 51.479,
"ret": 0.0018094 
},
{
 "date":   2567,
"name": "GSPC.Close",
"price": 104.12,
"rsi": 52.768,
"ret": -0.010266 
},
{
 "date":   2568,
"name": "GSPC.Close",
"price":  103.4,
"rsi": 45.389,
"ret": -0.0069151 
},
{
 "date":   2569,
"name": "GSPC.Close",
"price":  104.2,
"rsi": 41.248,
"ret": 0.0077369 
},
{
 "date":   2570,
"name": "GSPC.Close",
"price": 104.01,
"rsi": 47.031,
"ret": -0.0018234 
},
{
 "date":   2573,
"name": "GSPC.Close",
"price": 103.73,
"rsi": 45.876,
"ret": -0.002692 
},
{
 "date":   2574,
"name": "GSPC.Close",
"price": 103.32,
"rsi": 44.155,
"ret": -0.0039526 
},
{
 "date":   2575,
"name": "GSPC.Close",
"price": 103.85,
"rsi": 41.689,
"ret": 0.0051297 
},
{
 "date":   2576,
"name": "GSPC.Close",
"price": 102.97,
"rsi": 45.896,
"ret": -0.0084738 
},
{
 "date":   2577,
"name": "GSPC.Close",
"price": 103.32,
"rsi": 40.652,
"ret": 0.003399 
},
{
 "date":   2580,
"name": "GSPC.Close",
"price": 103.25,
"rsi": 43.421,
"ret": -0.00067751 
},
{
 "date":   2581,
"name": "GSPC.Close",
"price": 103.13,
"rsi": 42.989,
"ret": -0.0011622 
},
{
 "date":   2582,
"name": "GSPC.Close",
"price": 102.34,
"rsi": 42.214,
"ret": -0.0076602 
},
{
 "date":   2583,
"name": "GSPC.Close",
"price": 101.79,
"rsi": 37.428,
"ret": -0.0053742 
},
{
 "date":   2584,
"name": "GSPC.Close",
"price": 101.93,
"rsi": 34.496,
"ret": 0.0013754 
},
{
 "date":   2587,
"name": "GSPC.Close",
"price": 102.03,
"rsi": 35.873,
"ret": 0.00098107 
},
{
 "date":   2588,
"name": "GSPC.Close",
"price": 102.54,
"rsi": 36.894,
"ret": 0.0049985 
},
{
 "date":   2589,
"name": "GSPC.Close",
"price": 102.36,
"rsi": 41.966,
"ret": -0.0017554 
},
{
 "date":   2590,
"name": "GSPC.Close",
"price": 101.85,
"rsi": 40.722,
"ret": -0.0049824 
},
{
 "date":   2591,
"name": "GSPC.Close",
"price": 101.88,
"rsi": 37.344,
"ret": 0.00029455 
},
{
 "date":   2594,
"name": "GSPC.Close",
"price": 101.89,
"rsi": 37.671,
"ret": 9.8155e-05 
},
{
 "date":   2595,
"name": "GSPC.Close",
"price":  101.6,
"rsi": 37.788,
"ret": -0.0028462 
},
{
 "date":   2596,
"name": "GSPC.Close",
"price": 100.73,
"rsi":   35.7,
"ret": -0.008563 
},
{
 "date":   2597,
"name": "GSPC.Close",
"price": 100.82,
"rsi": 30.292,
"ret": 0.00089348 
},
{
 "date":   2598,
"name": "GSPC.Close",
"price": 100.22,
"rsi": 31.449,
"ret": -0.0059512 
},
{
 "date":   2601,
"name": "GSPC.Close",
"price": 100.74,
"rsi":   28.1,
"ret": 0.0051886 
},
{
 "date":   2602,
"name": "GSPC.Close",
"price": 101.04,
"rsi": 34.599,
"ret": 0.002978 
},
{
 "date":   2603,
"name": "GSPC.Close",
"price":  101.5,
"rsi": 38.077,
"ret": 0.0045527 
},
{
 "date":   2604,
"name": "GSPC.Close",
"price": 100.92,
"rsi": 43.075,
"ret": -0.0057143 
},
{
 "date":   2605,
"name": "GSPC.Close",
"price": 100.49,
"rsi":  38.82,
"ret": -0.0042608 
},
{
 "date":   2609,
"name": "GSPC.Close",
"price": 100.49,
"rsi": 35.983,
"ret":      0 
},
{
 "date":   2610,
"name": "GSPC.Close",
"price": 100.19,
"rsi": 35.983,
"ret": -0.0029854 
},
{
 "date":   2611,
"name": "GSPC.Close",
"price":   99.6,
"rsi": 33.973,
"ret": -0.0058888 
},
{
 "date":   2612,
"name": "GSPC.Close",
"price":  99.48,
"rsi":  30.38,
"ret": -0.0012048 
},
{
 "date":   2615,
"name": "GSPC.Close",
"price":  99.82,
"rsi": 29.692,
"ret": 0.0034178 
},
{
 "date":   2616,
"name": "GSPC.Close",
"price": 100.66,
"rsi": 34.236,
"ret": 0.0084151 
},
{
 "date":   2617,
"name": "GSPC.Close",
"price": 100.39,
"rsi": 43.884,
"ret": -0.0026823 
},
{
 "date":   2618,
"name": "GSPC.Close",
"price": 100.88,
"rsi": 41.763,
"ret": 0.004881 
},
{
 "date":   2619,
"name": "GSPC.Close",
"price":  101.2,
"rsi": 46.789,
"ret": 0.0031721 
},
{
 "date":   2622,
"name": "GSPC.Close",
"price": 101.25,
"rsi": 49.834,
"ret": 0.00049407 
},
{
 "date":   2623,
"name": "GSPC.Close",
"price": 100.87,
"rsi": 50.313,
"ret": -0.0037531 
},
{
 "date":   2624,
"name": "GSPC.Close",
"price":  100.1,
"rsi":  46.67,
"ret": -0.0076336 
},
{
 "date":   2625,
"name": "GSPC.Close",
"price": 100.67,
"rsi": 40.302,
"ret": 0.0056943 
},
{
 "date":   2626,
"name": "GSPC.Close",
"price": 100.65,
"rsi": 46.158,
"ret": -0.00019867 
},
{
 "date":   2629,
"name": "GSPC.Close",
"price": 101.42,
"rsi": 45.988,
"ret": 0.0076503 
},
{
 "date":   2630,
"name": "GSPC.Close",
"price": 101.98,
"rsi": 53.161,
"ret": 0.0055216 
},
{
 "date":   2631,
"name": "GSPC.Close",
"price": 102.17,
"rsi": 57.573,
"ret": 0.0018631 
},
{
 "date":   2632,
"name": "GSPC.Close",
"price": 102.08,
"rsi": 58.985,
"ret": -0.00088088 
},
{
 "date":   2633,
"name": "GSPC.Close",
"price": 101.86,
"rsi": 58.001,
"ret": -0.0021552 
},
{
 "date":   2636,
"name": "GSPC.Close",
"price": 101.31,
"rsi": 55.559,
"ret": -0.0053996 
},
{
 "date":   2637,
"name": "GSPC.Close",
"price":    101,
"rsi": 49.904,
"ret": -0.0030599 
},
{
 "date":   2638,
"name": "GSPC.Close",
"price":  100.2,
"rsi":     47,
"ret": -0.0079208 
},
{
 "date":   2639,
"name": "GSPC.Close",
"price":   99.7,
"rsi": 40.457,
"ret": -0.00499 
},
{
 "date":   2640,
"name": "GSPC.Close",
"price":  99.06,
"rsi": 36.991,
"ret": -0.0064193 
},
{
 "date":   2643,
"name": "GSPC.Close",
"price":     99,
"rsi": 33.084,
"ret": -0.00060569 
},
{
 "date":   2644,
"name": "GSPC.Close",
"price":  99.69,
"rsi": 32.735,
"ret": 0.0069697 
},
{
 "date":   2645,
"name": "GSPC.Close",
"price":  98.54,
"rsi": 40.509,
"ret": -0.011536 
},
{
 "date":   2646,
"name": "GSPC.Close",
"price":  98.42,
"rsi":  33.55,
"ret": -0.0012178 
},
{
 "date":   2647,
"name": "GSPC.Close",
"price":  99.21,
"rsi": 32.914,
"ret": 0.0080268 
},
{
 "date":   2650,
"name": "GSPC.Close",
"price":  98.23,
"rsi": 40.856,
"ret": -0.009878 
},
{
 "date":   2651,
"name": "GSPC.Close",
"price":  98.01,
"rsi": 35.277,
"ret": -0.0022396 
},
{
 "date":   2652,
"name": "GSPC.Close",
"price":  97.91,
"rsi":  34.15,
"ret": -0.0010203 
},
{
 "date":   2653,
"name": "GSPC.Close",
"price":  98.35,
"rsi": 33.624,
"ret": 0.0044939 
},
{
 "date":   2657,
"name": "GSPC.Close",
"price":  98.88,
"rsi": 38.139,
"ret": 0.0053889 
},
{
 "date":   2658,
"name": "GSPC.Close",
"price": 100.15,
"rsi": 43.154,
"ret": 0.012844 
},
{
 "date":   2659,
"name": "GSPC.Close",
"price": 100.16,
"rsi": 52.991,
"ret": 9.985e-05 
},
{
 "date":   2660,
"name": "GSPC.Close",
"price":    101,
"rsi":  53.06,
"ret": 0.0083866 
},
{
 "date":   2661,
"name": "GSPC.Close",
"price": 101.04,
"rsi": 58.553,
"ret": 0.00039604 
},
{
 "date":   2664,
"name": "GSPC.Close",
"price": 100.54,
"rsi":   58.8,
"ret": -0.0049485 
},
{
 "date":   2665,
"name": "GSPC.Close",
"price": 100.07,
"rsi": 54.429,
"ret": -0.0046748 
},
{
 "date":   2666,
"name": "GSPC.Close",
"price":  100.4,
"rsi":  50.62,
"ret": 0.0032977 
},
{
 "date":   2667,
"name": "GSPC.Close",
"price":  99.75,
"rsi": 53.102,
"ret": -0.0064741 
},
{
 "date":   2668,
"name": "GSPC.Close",
"price":  98.44,
"rsi": 47.986,
"ret": -0.013133 
},
{
 "date":   2671,
"name": "GSPC.Close",
"price":  97.15,
"rsi": 39.688,
"ret": -0.013104 
},
{
 "date":   2672,
"name": "GSPC.Close",
"price":  97.11,
"rsi": 33.537,
"ret": -0.00041173 
},
{
 "date":   2673,
"name": "GSPC.Close",
"price":  97.96,
"rsi": 33.364,
"ret": 0.008753 
},
{
 "date":   2674,
"name": "GSPC.Close",
"price":   98.2,
"rsi": 40.388,
"ret": 0.00245 
},
{
 "date":   2675,
"name": "GSPC.Close",
"price":  98.44,
"rsi": 42.239,
"ret": 0.002444 
},
{
 "date":   2678,
"name": "GSPC.Close",
"price":  98.93,
"rsi": 44.108,
"ret": 0.0049777 
},
{
 "date":   2679,
"name": "GSPC.Close",
"price":  99.43,
"rsi": 47.821,
"ret": 0.0050541 
},
{
 "date":   2680,
"name": "GSPC.Close",
"price":  99.96,
"rsi":  51.37,
"ret": 0.0053304 
},
{
 "date":   2681,
"name": "GSPC.Close",
"price": 100.11,
"rsi": 54.875,
"ret": 0.0015006 
},
{
 "date":   2682,
"name": "GSPC.Close",
"price":  99.49,
"rsi": 55.845,
"ret": -0.0061932 
},
{
 "date":   2685,
"name": "GSPC.Close",
"price":  99.18,
"rsi": 50.969,
"ret": -0.0031159 
},
{
 "date":   2686,
"name": "GSPC.Close",
"price":  99.47,
"rsi":  48.68,
"ret": 0.002924 
},
{
 "date":   2687,
"name": "GSPC.Close",
"price":  98.78,
"rsi": 50.901,
"ret": -0.0069368 
},
{
 "date":   2688,
"name": "GSPC.Close",
"price":  98.73,
"rsi":  45.82,
"ret": -0.00050618 
},
{
 "date":   2689,
"name": "GSPC.Close",
"price":  99.03,
"rsi": 45.466,
"ret": 0.0030386 
},
{
 "date":   2692,
"name": "GSPC.Close",
"price":  99.47,
"rsi":  48.06,
"ret": 0.0044431 
},
{
 "date":   2693,
"name": "GSPC.Close",
"price":  99.77,
"rsi":  51.69,
"ret": 0.003016 
},
{
 "date":   2694,
"name": "GSPC.Close",
"price":  100.3,
"rsi": 54.048,
"ret": 0.0053122 
},
{
 "date":   2695,
"name": "GSPC.Close",
"price":  99.88,
"rsi": 57.953,
"ret": -0.0041874 
},
{
 "date":   2696,
"name": "GSPC.Close",
"price":  99.45,
"rsi": 54.034,
"ret": -0.0043052 
},
{
 "date":   2699,
"name": "GSPC.Close",
"price":  98.15,
"rsi": 50.285,
"ret": -0.013072 
},
{
 "date":   2700,
"name": "GSPC.Close",
"price":  97.67,
"rsi":  41.02,
"ret": -0.0048905 
},
{
 "date":   2701,
"name": "GSPC.Close",
"price":  96.77,
"rsi":  38.22,
"ret": -0.0092147 
},
{
 "date":   2702,
"name": "GSPC.Close",
"price":  97.01,
"rsi": 33.589,
"ret": 0.0024801 
},
{
 "date":   2703,
"name": "GSPC.Close",
"price":  96.27,
"rsi": 35.822,
"ret": -0.0076281 
},
{
 "date":   2707,
"name": "GSPC.Close",
"price":  96.12,
"rsi": 32.225,
"ret": -0.0015581 
},
{
 "date":   2708,
"name": "GSPC.Close",
"price":  96.93,
"rsi": 31.533,
"ret": 0.008427 
},
{
 "date":   2709,
"name": "GSPC.Close",
"price":  96.74,
"rsi": 39.127,
"ret": -0.0019602 
},
{
 "date":   2710,
"name": "GSPC.Close",
"price":  97.69,
"rsi": 38.061,
"ret": 0.0098201 
},
{
 "date":   2713,
"name": "GSPC.Close",
"price":  97.23,
"rsi": 45.988,
"ret": -0.0047088 
},
{
 "date":   2714,
"name": "GSPC.Close",
"price":  97.73,
"rsi": 43.111,
"ret": 0.0051424 
},
{
 "date":   2715,
"name": "GSPC.Close",
"price":   98.2,
"rsi": 46.993,
"ret": 0.0048092 
},
{
 "date":   2716,
"name": "GSPC.Close",
"price":  98.14,
"rsi": 50.417,
"ret": -0.000611 
},
{
 "date":   2717,
"name": "GSPC.Close",
"price":  98.46,
"rsi": 49.974,
"ret": 0.0032606 
},
{
 "date":   2720,
"name": "GSPC.Close",
"price":  98.74,
"rsi": 52.382,
"ret": 0.0028438 
},
{
 "date":   2721,
"name": "GSPC.Close",
"price":  99.86,
"rsi": 54.448,
"ret": 0.011343 
},
{
 "date":   2722,
"name": "GSPC.Close",
"price":  99.61,
"rsi": 61.621,
"ret": -0.0025035 
},
{
 "date":   2723,
"name": "GSPC.Close",
"price":  99.85,
"rsi": 59.374,
"ret": 0.0024094 
},
{
 "date":   2724,
"name": "GSPC.Close",
"price":  99.97,
"rsi":  60.85,
"ret": 0.0012018 
},
{
 "date":   2727,
"name": "GSPC.Close",
"price": 100.42,
"rsi": 61.601,
"ret": 0.0045014 
},
{
 "date":   2728,
"name": "GSPC.Close",
"price": 100.74,
"rsi": 64.363,
"ret": 0.0031866 
},
{
 "date":   2729,
"name": "GSPC.Close",
"price": 100.46,
"rsi": 66.224,
"ret": -0.0027794 
},
{
 "date":   2730,
"name": "GSPC.Close",
"price": 100.62,
"rsi": 63.119,
"ret": 0.0015927 
},
{
 "date":   2731,
"name": "GSPC.Close",
"price": 101.19,
"rsi": 64.153,
"ret": 0.0056649 
},
{
 "date":   2734,
"name": "GSPC.Close",
"price": 100.98,
"rsi": 67.635,
"ret": -0.0020753 
},
{
 "date":   2735,
"name": "GSPC.Close",
"price": 100.14,
"rsi": 65.125,
"ret": -0.0083185 
},
{
 "date":   2736,
"name": "GSPC.Close",
"price": 100.11,
"rsi": 56.149,
"ret": -0.00029958 
},
{
 "date":   2737,
"name": "GSPC.Close",
"price": 100.48,
"rsi": 55.852,
"ret": 0.0036959 
},
{
 "date":   2738,
"name": "GSPC.Close",
"price":  100.1,
"rsi": 58.742,
"ret": -0.0037818 
},
{
 "date":   2742,
"name": "GSPC.Close",
"price": 100.09,
"rsi": 54.777,
"ret": -9.99e-05 
},
{
 "date":   2743,
"name": "GSPC.Close",
"price":  99.58,
"rsi": 54.672,
"ret": -0.0050954 
},
{
 "date":   2744,
"name": "GSPC.Close",
"price":  99.93,
"rsi": 49.482,
"ret": 0.0035148 
},
{
 "date":   2745,
"name": "GSPC.Close",
"price":  99.79,
"rsi": 52.794,
"ret": -0.001401 
},
{
 "date":   2748,
"name": "GSPC.Close",
"price":  99.55,
"rsi": 51.344,
"ret": -0.0024051 
},
{
 "date":   2749,
"name": "GSPC.Close",
"price":  99.45,
"rsi": 48.866,
"ret": -0.0010045 
},
{
 "date":   2750,
"name": "GSPC.Close",
"price":  99.59,
"rsi": 47.831,
"ret": 0.0014077 
},
{
 "date":   2752,
"name": "GSPC.Close",
"price": 100.18,
"rsi": 49.446,
"ret": 0.0059243 
},
{
 "date":   2755,
"name": "GSPC.Close",
"price": 100.95,
"rsi": 55.675,
"ret": 0.0076862 
},
{
 "date":   2756,
"name": "GSPC.Close",
"price": 101.79,
"rsi": 62.218,
"ret": 0.008321 
},
{
 "date":   2757,
"name": "GSPC.Close",
"price": 101.73,
"rsi": 67.802,
"ret": -0.00058945 
},
{
 "date":   2758,
"name": "GSPC.Close",
"price": 101.59,
"rsi":  67.04,
"ret": -0.0013762 
},
{
 "date":   2759,
"name": "GSPC.Close",
"price": 101.67,
"rsi": 65.198,
"ret": 0.00078748 
},
{
 "date":   2762,
"name": "GSPC.Close",
"price": 100.85,
"rsi": 65.777,
"ret": -0.0080653 
},
{
 "date":   2763,
"name": "GSPC.Close",
"price": 100.27,
"rsi": 55.578,
"ret": -0.0057511 
},
{
 "date":   2764,
"name": "GSPC.Close",
"price":  98.64,
"rsi": 49.708,
"ret": -0.016256 
},
{
 "date":   2765,
"name": "GSPC.Close",
"price":  98.79,
"rsi": 37.666,
"ret": 0.0015207 
},
{
 "date":   2766,
"name": "GSPC.Close",
"price":  98.85,
"rsi": 39.127,
"ret": 0.00060735 
},
{
 "date":   2769,
"name": "GSPC.Close",
"price":  99.12,
"rsi": 39.736,
"ret": 0.0027314 
},
{
 "date":   2770,
"name": "GSPC.Close",
"price":   98.5,
"rsi": 42.521,
"ret": -0.006255 
},
{
 "date":   2771,
"name": "GSPC.Close",
"price":  98.37,
"rsi":  38.16,
"ret": -0.0013198 
},
{
 "date":   2772,
"name": "GSPC.Close",
"price":  98.74,
"rsi": 37.296,
"ret": 0.0037613 
},
{
 "date":   2773,
"name": "GSPC.Close",
"price":  98.76,
"rsi": 41.364,
"ret": 0.00020255 
},
{
 "date":   2776,
"name": "GSPC.Close",
"price":  97.99,
"rsi": 41.585,
"ret": -0.0077967 
},
{
 "date":   2777,
"name": "GSPC.Close",
"price":  98.05,
"rsi": 35.973,
"ret": 0.00061231 
},
{
 "date":   2778,
"name": "GSPC.Close",
"price":  98.92,
"rsi":  36.69,
"ret": 0.008873 
},
{
 "date":   2779,
"name": "GSPC.Close",
"price":  98.16,
"rsi": 46.112,
"ret": -0.007683 
},
{
 "date":   2780,
"name": "GSPC.Close",
"price":  97.88,
"rsi": 40.449,
"ret": -0.0028525 
},
{
 "date":   2783,
"name": "GSPC.Close",
"price":  98.18,
"rsi":  38.57,
"ret": 0.003065 
},
{
 "date":   2784,
"name": "GSPC.Close",
"price":  97.73,
"rsi": 41.696,
"ret": -0.0045834 
},
{
 "date":   2785,
"name": "GSPC.Close",
"price":  97.74,
"rsi": 38.529,
"ret": 0.00010232 
},
{
 "date":   2786,
"name": "GSPC.Close",
"price":  97.68,
"rsi":  38.64,
"ret": -0.00061387 
},
{
 "date":   2787,
"name": "GSPC.Close",
"price":  97.51,
"rsi": 38.192,
"ret": -0.0017404 
},
{
 "date":   2790,
"name": "GSPC.Close",
"price":  97.79,
"rsi": 36.888,
"ret": 0.0028715 
},
{
 "date":   2791,
"name": "GSPC.Close",
"price":  97.62,
"rsi": 40.493,
"ret": -0.0017384 
},
{
 "date":   2792,
"name": "GSPC.Close",
"price":  97.23,
"rsi": 39.035,
"ret": -0.0039951 
},
{
 "date":   2793,
"name": "GSPC.Close",
"price":  96.15,
"rsi": 35.847,
"ret": -0.011108 
},
{
 "date":   2794,
"name": "GSPC.Close",
"price":  96.06,
"rsi": 28.825,
"ret": -0.00093604 
},
{
 "date":   2797,
"name": "GSPC.Close",
"price":  96.92,
"rsi": 28.327,
"ret": 0.0089527 
},
{
 "date":   2798,
"name": "GSPC.Close",
"price":  96.38,
"rsi": 39.145,
"ret": -0.0055716 
},
{
 "date":   2799,
"name": "GSPC.Close",
"price":  96.77,
"rsi":  35.52,
"ret": 0.0040465 
},
{
 "date":   2800,
"name": "GSPC.Close",
"price":  96.83,
"rsi": 39.852,
"ret": 0.00062003 
},
{
 "date":   2801,
"name": "GSPC.Close",
"price":  97.45,
"rsi": 40.515,
"ret": 0.006403 
},
{
 "date":   2805,
"name": "GSPC.Close",
"price":  97.71,
"rsi": 47.007,
"ret": 0.002668 
},
{
 "date":   2806,
"name": "GSPC.Close",
"price":  98.01,
"rsi": 49.497,
"ret": 0.0030703 
},
{
 "date":   2807,
"name": "GSPC.Close",
"price":  97.28,
"rsi": 52.282,
"ret": -0.0074482 
},
{
 "date":   2808,
"name": "GSPC.Close",
"price":  96.37,
"rsi":  45.68,
"ret": -0.0093544 
},
{
 "date":   2811,
"name": "GSPC.Close",
"price":  96.03,
"rsi": 39.059,
"ret": -0.0035281 
},
{
 "date":   2812,
"name": "GSPC.Close",
"price":  96.09,
"rsi": 36.906,
"ret": 0.0006248 
},
{
 "date":   2813,
"name": "GSPC.Close",
"price":  96.55,
"rsi":  37.56,
"ret": 0.0047872 
},
{
 "date":   2814,
"name": "GSPC.Close",
"price":   96.8,
"rsi": 42.482,
"ret": 0.0025893 
},
{
 "date":   2815,
"name": "GSPC.Close",
"price":  96.48,
"rsi": 45.019,
"ret": -0.0033058 
},
{
 "date":   2818,
"name": "GSPC.Close",
"price":  95.85,
"rsi": 42.439,
"ret": -0.0065299 
},
{
 "date":   2819,
"name": "GSPC.Close",
"price":  95.89,
"rsi": 37.841,
"ret": 0.00041732 
},
{
 "date":   2820,
"name": "GSPC.Close",
"price":   95.1,
"rsi": 38.298,
"ret": -0.0082386 
},
{
 "date":   2821,
"name": "GSPC.Close",
"price":  95.09,
"rsi": 33.118,
"ret": -0.00010515 
},
{
 "date":   2822,
"name": "GSPC.Close",
"price":  95.04,
"rsi": 33.057,
"ret": -0.00052582 
},
{
 "date":   2825,
"name": "GSPC.Close",
"price":  95.38,
"rsi": 32.733,
"ret": 0.0035774 
},
{
 "date":   2826,
"name": "GSPC.Close",
"price":  95.24,
"rsi": 37.242,
"ret": -0.0014678 
},
{
 "date":   2827,
"name": "GSPC.Close",
"price":  95.31,
"rsi": 36.167,
"ret": 0.00073499 
},
{
 "date":   2828,
"name": "GSPC.Close",
"price":  95.85,
"rsi": 37.144,
"ret": 0.0056657 
},
{
 "date":   2829,
"name": "GSPC.Close",
"price":  96.53,
"rsi": 44.236,
"ret": 0.0070944 
},
{
 "date":   2832,
"name": "GSPC.Close",
"price":  96.74,
"rsi": 51.635,
"ret": 0.0021755 
},
{
 "date":   2833,
"name": "GSPC.Close",
"price":  96.03,
"rsi":  53.68,
"ret": -0.0073393 
},
{
 "date":   2834,
"name": "GSPC.Close",
"price":  95.68,
"rsi":  46.52,
"ret": -0.0036447 
},
{
 "date":   2835,
"name": "GSPC.Close",
"price":  96.05,
"rsi": 43.444,
"ret": 0.0038671 
},
{
 "date":   2836,
"name": "GSPC.Close",
"price":  95.97,
"rsi": 47.404,
"ret": -0.0008329 
},
{
 "date":   2839,
"name": "GSPC.Close",
"price":  95.75,
"rsi": 46.643,
"ret": -0.0022924 
},
{
 "date":   2840,
"name": "GSPC.Close",
"price":  94.93,
"rsi": 44.528,
"ret": -0.008564 
},
{
 "date":   2841,
"name": "GSPC.Close",
"price":  94.04,
"rsi": 37.671,
"ret": -0.0093753 
},
{
 "date":   2842,
"name": "GSPC.Close",
"price":  93.46,
"rsi": 31.925,
"ret": -0.0061676 
},
{
 "date":   2843,
"name": "GSPC.Close",
"price":  93.56,
"rsi": 28.838,
"ret": 0.00107 
},
{
 "date":   2846,
"name": "GSPC.Close",
"price":  93.47,
"rsi": 30.093,
"ret": -0.00096195 
},
{
 "date":   2847,
"name": "GSPC.Close",
"price":  93.46,
"rsi": 29.587,
"ret": -0.00010699 
},
{
 "date":   2848,
"name": "GSPC.Close",
"price":  92.38,
"rsi": 29.528,
"ret": -0.011556 
},
{
 "date":   2849,
"name": "GSPC.Close",
"price":  92.67,
"rsi": 23.939,
"ret": 0.0031392 
},
{
 "date":   2850,
"name": "GSPC.Close",
"price":  92.32,
"rsi": 27.886,
"ret": -0.0037768 
},
{
 "date":   2853,
"name": "GSPC.Close",
"price":  91.63,
"rsi": 26.124,
"ret": -0.007474 
},
{
 "date":   2854,
"name": "GSPC.Close",
"price":     91,
"rsi": 23.034,
"ret": -0.0068755 
},
{
 "date":   2855,
"name": "GSPC.Close",
"price":   92.1,
"rsi": 20.634,
"ret": 0.012088 
},
{
 "date":   2856,
"name": "GSPC.Close",
"price":  92.34,
"rsi": 33.635,
"ret": 0.0026059 
},
{
 "date":   2857,
"name": "GSPC.Close",
"price":  92.61,
"rsi": 36.095,
"ret": 0.002924 
},
{
 "date":   2860,
"name": "GSPC.Close",
"price":  92.34,
"rsi": 38.841,
"ret": -0.0029155 
},
{
 "date":   2861,
"name": "GSPC.Close",
"price":  91.35,
"rsi": 37.123,
"ret": -0.010721 
},
{
 "date":   2862,
"name": "GSPC.Close",
"price":  90.71,
"rsi": 31.603,
"ret": -0.007006 
},
{
 "date":   2863,
"name": "GSPC.Close",
"price":  90.76,
"rsi": 28.639,
"ret": 0.00055121 
},
{
 "date":   2864,
"name": "GSPC.Close",
"price":  91.58,
"rsi": 29.197,
"ret": 0.0090348 
},
{
 "date":   2867,
"name": "GSPC.Close",
"price":  92.29,
"rsi":   37.8,
"ret": 0.0077528 
},
{
 "date":   2868,
"name": "GSPC.Close",
"price":  92.46,
"rsi": 44.129,
"ret": 0.001842 
},
{
 "date":   2869,
"name": "GSPC.Close",
"price":  92.98,
"rsi": 45.558,
"ret": 0.0056241 
},
{
 "date":   2870,
"name": "GSPC.Close",
"price":  94.71,
"rsi": 49.787,
"ret": 0.018606 
},
{
 "date":   2871,
"name": "GSPC.Close",
"price":  95.98,
"rsi":  60.72,
"ret": 0.013409 
},
{
 "date":   2874,
"name": "GSPC.Close",
"price":  95.32,
"rsi": 66.488,
"ret": -0.0068764 
},
{
 "date":   2875,
"name": "GSPC.Close",
"price":  95.93,
"rsi": 61.439,
"ret": 0.0063995 
},
{
 "date":   2876,
"name": "GSPC.Close",
"price":  95.45,
"rsi": 64.149,
"ret": -0.0050036 
},
{
 "date":   2877,
"name": "GSPC.Close",
"price":  95.16,
"rsi": 60.543,
"ret": -0.0030382 
},
{
 "date":   2878,
"name": "GSPC.Close",
"price":  95.33,
"rsi": 58.407,
"ret": 0.0017865 
},
{
 "date":   2881,
"name": "GSPC.Close",
"price":  95.25,
"rsi": 59.313,
"ret": -0.00083919 
},
{
 "date":   2882,
"name": "GSPC.Close",
"price":  96.09,
"rsi": 58.666,
"ret": 0.0088189 
},
{
 "date":   2883,
"name": "GSPC.Close",
"price":  96.49,
"rsi": 63.209,
"ret": 0.0041628 
},
{
 "date":   2885,
"name": "GSPC.Close",
"price":  96.69,
"rsi": 65.172,
"ret": 0.0020728 
},
{
 "date":   2888,
"name": "GSPC.Close",
"price":  96.04,
"rsi": 66.145,
"ret": -0.0067225 
},
{
 "date":   2889,
"name": "GSPC.Close",
"price":  94.55,
"rsi": 60.255,
"ret": -0.015514 
},
{
 "date":   2890,
"name": "GSPC.Close",
"price":  94.83,
"rsi": 49.396,
"ret": 0.0029614 
},
{
 "date":   2891,
"name": "GSPC.Close",
"price":  94.69,
"rsi": 51.177,
"ret": -0.0014763 
},
{
 "date":   2892,
"name": "GSPC.Close",
"price":  94.67,
"rsi": 50.225,
"ret": -0.00021122 
},
{
 "date":   2895,
"name": "GSPC.Close",
"price":  94.27,
"rsi": 50.082,
"ret": -0.0042252 
},
{
 "date":   2896,
"name": "GSPC.Close",
"price":  92.83,
"rsi": 47.183,
"ret": -0.015275 
},
{
 "date":   2897,
"name": "GSPC.Close",
"price":  92.78,
"rsi": 38.535,
"ret": -0.00053862 
},
{
 "date":   2898,
"name": "GSPC.Close",
"price":  92.96,
"rsi": 38.273,
"ret": 0.0019401 
},
{
 "date":   2899,
"name": "GSPC.Close",
"price":  93.65,
"rsi":  39.86,
"ret": 0.0074225 
},
{
 "date":   2902,
"name": "GSPC.Close",
"price":  93.63,
"rsi": 45.631,
"ret": -0.00021356 
},
{
 "date":   2903,
"name": "GSPC.Close",
"price":  93.56,
"rsi": 45.494,
"ret": -0.00074762 
},
{
 "date":   2904,
"name": "GSPC.Close",
"price":  94.03,
"rsi": 44.988,
"ret": 0.0050235 
},
{
 "date":   2905,
"name": "GSPC.Close",
"price":  93.55,
"rsi": 49.086,
"ret": -0.0051048 
},
{
 "date":   2906,
"name": "GSPC.Close",
"price":   93.4,
"rsi": 45.369,
"ret": -0.0016034 
},
{
 "date":   2909,
"name": "GSPC.Close",
"price":  92.69,
"rsi": 44.241,
"ret": -0.0076017 
},
{
 "date":   2910,
"name": "GSPC.Close",
"price":   92.5,
"rsi": 39.267,
"ret": -0.0020498 
},
{
 "date":   2911,
"name": "GSPC.Close",
"price":  93.05,
"rsi": 38.035,
"ret": 0.0059459 
},
{
 "date":   2912,
"name": "GSPC.Close",
"price":   93.8,
"rsi": 43.557,
"ret": 0.0080602 
},
{
 "date":   2913,
"name": "GSPC.Close",
"price":  94.69,
"rsi": 50.089,
"ret": 0.0094883 
},
{
 "date":   2917,
"name": "GSPC.Close",
"price":  94.69,
"rsi":  56.52,
"ret":      0 
},
{
 "date":   2918,
"name": "GSPC.Close",
"price":  94.75,
"rsi":  56.52,
"ret": 0.00063365 
},
{
 "date":   2919,
"name": "GSPC.Close",
"price":  94.94,
"rsi": 56.953,
"ret": 0.0020053 
},
{
 "date":   2920,
"name": "GSPC.Close",
"price":   95.1,
"rsi": 58.369,
"ret": 0.0016853 
},
{
 "date":   2924,
"name": "GSPC.Close",
"price":  93.82,
"rsi": 59.575,
"ret": -0.01346 
},
{
 "date":   2925,
"name": "GSPC.Close",
"price":  93.52,
"rsi": 47.677,
"ret": -0.0031976 
},
{
 "date":   2926,
"name": "GSPC.Close",
"price":  92.74,
"rsi": 45.389,
"ret": -0.0083405 
},
{
 "date":   2927,
"name": "GSPC.Close",
"price":  91.62,
"rsi": 40.013,
"ret": -0.012077 
},
{
 "date":   2930,
"name": "GSPC.Close",
"price":  90.64,
"rsi": 33.818,
"ret": -0.010696 
},
{
 "date":   2931,
"name": "GSPC.Close",
"price":  90.17,
"rsi": 29.513,
"ret": -0.0051853 
},
{
 "date":   2932,
"name": "GSPC.Close",
"price":  89.74,
"rsi": 27.692,
"ret": -0.0047688 
},
{
 "date":   2933,
"name": "GSPC.Close",
"price":  89.82,
"rsi": 26.105,
"ret": 0.00089146 
},
{
 "date":   2934,
"name": "GSPC.Close",
"price":  89.69,
"rsi": 26.944,
"ret": -0.0014473 
},
{
 "date":   2937,
"name": "GSPC.Close",
"price":  89.43,
"rsi": 26.419,
"ret": -0.0028989 
},
{
 "date":   2938,
"name": "GSPC.Close",
"price":  89.88,
"rsi": 25.356,
"ret": 0.0050319 
},
{
 "date":   2939,
"name": "GSPC.Close",
"price":  90.56,
"rsi": 30.566,
"ret": 0.0075656 
},
{
 "date":   2940,
"name": "GSPC.Close",
"price":  90.09,
"rsi": 37.649,
"ret": -0.0051899 
},
{
 "date":   2941,
"name": "GSPC.Close",
"price":  89.89,
"rsi": 34.992,
"ret": -0.00222 
},
{
 "date":   2944,
"name": "GSPC.Close",
"price":  89.24,
"rsi": 33.896,
"ret": -0.0072311 
},
{
 "date":   2945,
"name": "GSPC.Close",
"price":  89.25,
"rsi": 30.547,
"ret": 0.00011206 
},
{
 "date":   2946,
"name": "GSPC.Close",
"price":  89.39,
"rsi":  30.66,
"ret": 0.0015686 
},
{
 "date":   2947,
"name": "GSPC.Close",
"price":  88.58,
"rsi": 32.328,
"ret": -0.0090614 
},
{
 "date":   2948,
"name": "GSPC.Close",
"price":  88.58,
"rsi": 28.115,
"ret":      0 
},
{
 "date":   2951,
"name": "GSPC.Close",
"price":  89.34,
"rsi": 28.115,
"ret": 0.0085798 
},
{
 "date":   2952,
"name": "GSPC.Close",
"price":  89.25,
"rsi": 37.043,
"ret": -0.0010074 
},
{
 "date":   2953,
"name": "GSPC.Close",
"price":  89.93,
"rsi": 36.465,
"ret": 0.007619 
},
{
 "date":   2954,
"name": "GSPC.Close",
"price":  90.13,
"rsi": 43.618,
"ret": 0.002224 
},
{
 "date":   2955,
"name": "GSPC.Close",
"price":  89.62,
"rsi":  45.56,
"ret": -0.0056585 
},
{
 "date":   2958,
"name": "GSPC.Close",
"price":   89.5,
"rsi": 41.624,
"ret": -0.001339 
},
{
 "date":   2959,
"name": "GSPC.Close",
"price":  90.33,
"rsi": 40.732,
"ret": 0.0092737 
},
{
 "date":   2960,
"name": "GSPC.Close",
"price":  90.83,
"rsi": 48.888,
"ret": 0.0055353 
},
{
 "date":   2961,
"name": "GSPC.Close",
"price":   90.3,
"rsi": 53.077,
"ret": -0.0058351 
},
{
 "date":   2962,
"name": "GSPC.Close",
"price":  90.08,
"rsi": 48.536,
"ret": -0.0024363 
},
{
 "date":   2965,
"name": "GSPC.Close",
"price":  89.86,
"rsi": 46.748,
"ret": -0.0024423 
},
{
 "date":   2966,
"name": "GSPC.Close",
"price":  89.04,
"rsi": 44.964,
"ret": -0.0091253 
},
{
 "date":   2967,
"name": "GSPC.Close",
"price":  88.83,
"rsi": 38.993,
"ret": -0.0023585 
},
{
 "date":   2968,
"name": "GSPC.Close",
"price":  88.08,
"rsi": 37.615,
"ret": -0.0084431 
},
{
 "date":   2969,
"name": "GSPC.Close",
"price":  87.96,
"rsi": 33.114,
"ret": -0.0013624 
},
{
 "date":   2973,
"name": "GSPC.Close",
"price":  87.59,
"rsi": 32.446,
"ret": -0.0042065 
},
{
 "date":   2974,
"name": "GSPC.Close",
"price":  87.56,
"rsi": 30.406,
"ret": -0.0003425 
},
{
 "date":   2975,
"name": "GSPC.Close",
"price":  87.64,
"rsi":  30.24,
"ret": 0.00091366 
},
{
 "date":   2976,
"name": "GSPC.Close",
"price":  88.49,
"rsi": 31.317,
"ret": 0.0096988 
},
{
 "date":   2979,
"name": "GSPC.Close",
"price":  87.72,
"rsi": 41.626,
"ret": -0.0087015 
},
{
 "date":   2980,
"name": "GSPC.Close",
"price":  87.04,
"rsi": 36.309,
"ret": -0.0077519 
},
{
 "date":   2981,
"name": "GSPC.Close",
"price":  87.19,
"rsi": 32.376,
"ret": 0.0017233 
},
{
 "date":   2982,
"name": "GSPC.Close",
"price":  87.32,
"rsi": 34.073,
"ret": 0.001491 
},
{
 "date":   2983,
"name": "GSPC.Close",
"price":  87.45,
"rsi": 35.581,
"ret": 0.0014888 
},
{
 "date":   2986,
"name": "GSPC.Close",
"price":   86.9,
"rsi":  37.13,
"ret": -0.0062893 
},
{
 "date":   2987,
"name": "GSPC.Close",
"price":  87.36,
"rsi": 33.464,
"ret": 0.0052934 
},
{
 "date":   2988,
"name": "GSPC.Close",
"price":  87.84,
"rsi": 38.898,
"ret": 0.0054945 
},
{
 "date":   2989,
"name": "GSPC.Close",
"price":  87.89,
"rsi": 44.034,
"ret": 0.00056922 
},
{
 "date":   2990,
"name": "GSPC.Close",
"price":  88.88,
"rsi": 44.557,
"ret": 0.011264 
},
{
 "date":   2993,
"name": "GSPC.Close",
"price":  88.95,
"rsi": 53.766,
"ret": 0.00078758 
},
{
 "date":   2994,
"name": "GSPC.Close",
"price":  89.35,
"rsi": 54.344,
"ret": 0.0044969 
},
{
 "date":   2995,
"name": "GSPC.Close",
"price":  89.12,
"rsi": 57.603,
"ret": -0.0025741 
},
{
 "date":   2996,
"name": "GSPC.Close",
"price":  89.51,
"rsi": 55.164,
"ret": 0.0043761 
},
{
 "date":   2997,
"name": "GSPC.Close",
"price":   90.2,
"rsi": 58.381,
"ret": 0.0077086 
},
{
 "date":   3000,
"name": "GSPC.Close",
"price":  90.82,
"rsi": 63.386,
"ret": 0.0068736 
},
{
 "date":   3001,
"name": "GSPC.Close",
"price":  89.79,
"rsi": 67.203,
"ret": -0.011341 
},
{
 "date":   3002,
"name": "GSPC.Close",
"price":  89.47,
"rsi":  56.64,
"ret": -0.0035639 
},
{
 "date":   3003,
"name": "GSPC.Close",
"price":  89.36,
"rsi":  53.81,
"ret": -0.0012295 
},
{
 "date":   3007,
"name": "GSPC.Close",
"price":  88.87,
"rsi": 52.833,
"ret": -0.0054834 
},
{
 "date":   3008,
"name": "GSPC.Close",
"price":   89.5,
"rsi": 48.599,
"ret": 0.007089 
},
{
 "date":   3009,
"name": "GSPC.Close",
"price":  89.64,
"rsi": 53.733,
"ret": 0.0015642 
},
{
 "date":   3010,
"name": "GSPC.Close",
"price":  89.41,
"rsi": 54.813,
"ret": -0.0025658 
},
{
 "date":   3011,
"name": "GSPC.Close",
"price":  89.21,
"rsi": 52.639,
"ret": -0.0022369 
},
{
 "date":   3014,
"name": "GSPC.Close",
"price":  88.46,
"rsi": 50.754,
"ret": -0.0084071 
},
{
 "date":   3015,
"name": "GSPC.Close",
"price":  88.86,
"rsi": 44.341,
"ret": 0.0045218 
},
{
 "date":   3016,
"name": "GSPC.Close",
"price":  89.64,
"rsi": 48.107,
"ret": 0.0087779 
},
{
 "date":   3017,
"name": "GSPC.Close",
"price":  89.79,
"rsi": 54.563,
"ret": 0.0016734 
},
{
 "date":   3018,
"name": "GSPC.Close",
"price":  90.17,
"rsi": 55.704,
"ret": 0.0042321 
},
{
 "date":   3021,
"name": "GSPC.Close",
"price":  90.49,
"rsi": 58.545,
"ret": 0.0035489 
},
{
 "date":   3022,
"name": "GSPC.Close",
"price":  90.25,
"rsi": 60.824,
"ret": -0.0026522 
},
{
 "date":   3023,
"name": "GSPC.Close",
"price":  90.11,
"rsi": 58.238,
"ret": -0.0015512 
},
{
 "date":   3024,
"name": "GSPC.Close",
"price":  90.98,
"rsi": 56.723,
"ret": 0.0096549 
},
{
 "date":   3025,
"name": "GSPC.Close",
"price":  92.92,
"rsi": 63.139,
"ret": 0.021323 
},
{
 "date":   3028,
"name": "GSPC.Close",
"price":  94.45,
"rsi": 72.817,
"ret": 0.016466 
},
{
 "date":   3029,
"name": "GSPC.Close",
"price":  93.43,
"rsi": 77.773,
"ret": -0.010799 
},
{
 "date":   3030,
"name": "GSPC.Close",
"price":  93.86,
"rsi": 68.771,
"ret": 0.0046024 
},
{
 "date":   3031,
"name": "GSPC.Close",
"price":  94.54,
"rsi":  70.33,
"ret": 0.0072448 
},
{
 "date":   3032,
"name": "GSPC.Close",
"price":  94.34,
"rsi": 72.655,
"ret": -0.0021155 
},
{
 "date":   3035,
"name": "GSPC.Close",
"price":  95.77,
"rsi": 70.895,
"ret": 0.015158 
},
{
 "date":   3036,
"name": "GSPC.Close",
"price":  96.64,
"rsi":  75.47,
"ret": 0.0090843 
},
{
 "date":   3037,
"name": "GSPC.Close",
"price":  96.82,
"rsi": 77.761,
"ret": 0.0018626 
},
{
 "date":   3038,
"name": "GSPC.Close",
"price":  95.86,
"rsi": 78.214,
"ret": -0.0099153 
},
{
 "date":   3039,
"name": "GSPC.Close",
"price":  96.83,
"rsi": 70.018,
"ret": 0.010119 
},
{
 "date":   3042,
"name": "GSPC.Close",
"price":  97.67,
"rsi": 73.087,
"ret": 0.008675 
},
{
 "date":   3043,
"name": "GSPC.Close",
"price":  97.25,
"rsi": 75.432,
"ret": -0.0043002 
},
{
 "date":   3044,
"name": "GSPC.Close",
"price":  96.26,
"rsi": 72.051,
"ret": -0.01018 
},
{
 "date":   3045,
"name": "GSPC.Close",
"price":  95.93,
"rsi": 64.692,
"ret": -0.0034282 
},
{
 "date":   3046,
"name": "GSPC.Close",
"price":  96.53,
"rsi": 62.403,
"ret": 0.0062546 
},
{
 "date":   3049,
"name": "GSPC.Close",
"price":  96.19,
"rsi": 64.839,
"ret": -0.0035222 
},
{
 "date":   3050,
"name": "GSPC.Close",
"price":   95.9,
"rsi": 62.373,
"ret": -0.0030149 
},
{
 "date":   3051,
"name": "GSPC.Close",
"price":  95.92,
"rsi": 60.268,
"ret": 0.00020855 
},
{
 "date":   3052,
"name": "GSPC.Close",
"price":   97.2,
"rsi": 60.368,
"ret": 0.013344 
},
{
 "date":   3053,
"name": "GSPC.Close",
"price":  98.07,
"rsi": 66.193,
"ret": 0.0089506 
},
{
 "date":   3056,
"name": "GSPC.Close",
"price":  98.76,
"rsi": 69.477,
"ret": 0.0070358 
},
{
 "date":   3057,
"name": "GSPC.Close",
"price":  99.35,
"rsi": 71.816,
"ret": 0.0059741 
},
{
 "date":   3058,
"name": "GSPC.Close",
"price":   99.6,
"rsi": 73.673,
"ret": 0.0025164 
},
{
 "date":   3059,
"name": "GSPC.Close",
"price":  98.62,
"rsi": 74.442,
"ret": -0.0098394 
},
{
 "date":   3060,
"name": "GSPC.Close",
"price":  98.12,
"rsi": 66.274,
"ret": -0.00507 
},
{
 "date":   3063,
"name": "GSPC.Close",
"price":  99.09,
"rsi": 62.506,
"ret": 0.0098859 
},
{
 "date":   3064,
"name": "GSPC.Close",
"price":  98.05,
"rsi": 66.487,
"ret": -0.010496 
},
{
 "date":   3065,
"name": "GSPC.Close",
"price":  97.08,
"rsi": 59.226,
"ret": -0.0098929 
},
{
 "date":   3066,
"name": "GSPC.Close",
"price":   96.8,
"rsi": 53.371,
"ret": -0.0028842 
},
{
 "date":   3067,
"name": "GSPC.Close",
"price":  96.58,
"rsi":  51.78,
"ret": -0.0022727 
},
{
 "date":   3071,
"name": "GSPC.Close",
"price":  96.86,
"rsi": 50.506,
"ret": 0.0028992 
},
{
 "date":   3072,
"name": "GSPC.Close",
"price":  97.24,
"rsi": 52.121,
"ret": 0.0039232 
},
{
 "date":   3073,
"name": "GSPC.Close",
"price":  97.35,
"rsi":   54.3,
"ret": 0.0011312 
},
{
 "date":   3074,
"name": "GSPC.Close",
"price":  98.14,
"rsi": 54.939,
"ret": 0.008115 
},
{
 "date":   3077,
"name": "GSPC.Close",
"price":  99.95,
"rsi": 59.339,
"ret": 0.018443 
},
{
 "date":   3078,
"name": "GSPC.Close",
"price": 100.32,
"rsi": 67.233,
"ret": 0.0037019 
},
{
 "date":   3079,
"name": "GSPC.Close",
"price": 100.12,
"rsi": 68.576,
"ret": -0.0019936 
},
{
 "date":   3080,
"name": "GSPC.Close",
"price": 100.21,
"rsi": 66.978,
"ret": 0.00089892 
},
{
 "date":   3081,
"name": "GSPC.Close",
"price":  99.93,
"rsi": 67.346,
"ret": -0.0027941 
},
{
 "date":   3084,
"name": "GSPC.Close",
"price":  99.55,
"rsi": 64.917,
"ret": -0.0038027 
},
{
 "date":   3085,
"name": "GSPC.Close",
"price":  99.57,
"rsi": 61.667,
"ret": 0.0002009 
},
{
 "date":   3086,
"name": "GSPC.Close",
"price":  99.48,
"rsi": 61.776,
"ret": -0.00090389 
},
{
 "date":   3087,
"name": "GSPC.Close",
"price":  98.34,
"rsi":  60.94,
"ret": -0.01146 
},
{
 "date":   3088,
"name": "GSPC.Close",
"price":  97.42,
"rsi": 51.446,
"ret": -0.0093553 
},
{
 "date":   3091,
"name": "GSPC.Close",
"price":  97.49,
"rsi": 45.311,
"ret": 0.00071854 
},
{
 "date":   3092,
"name": "GSPC.Close",
"price":  96.51,
"rsi":  45.84,
"ret": -0.010052 
},
{
 "date":   3093,
"name": "GSPC.Close",
"price":  96.01,
"rsi": 40.003,
"ret": -0.0051808 
},
{
 "date":   3094,
"name": "GSPC.Close",
"price":  96.24,
"rsi": 37.388,
"ret": 0.0023956 
},
{
 "date":   3095,
"name": "GSPC.Close",
"price":  95.85,
"rsi": 39.352,
"ret": -0.0040524 
},
{
 "date":   3098,
"name": "GSPC.Close",
"price":   94.6,
"rsi":  37.22,
"ret": -0.013041 
},
{
 "date":   3099,
"name": "GSPC.Close",
"price":  94.98,
"rsi": 31.355,
"ret": 0.0040169 
},
{
 "date":   3100,
"name": "GSPC.Close",
"price":   95.4,
"rsi": 34.722,
"ret": 0.004422 
},
{
 "date":   3101,
"name": "GSPC.Close",
"price":  95.57,
"rsi": 38.324,
"ret": 0.001782 
},
{
 "date":   3102,
"name": "GSPC.Close",
"price":  95.53,
"rsi": 39.772,
"ret": -0.00041854 
},
{
 "date":   3105,
"name": "GSPC.Close",
"price":  95.09,
"rsi": 39.537,
"ret": -0.0046059 
},
{
 "date":   3107,
"name": "GSPC.Close",
"price":  94.27,
"rsi": 36.948,
"ret": -0.0086234 
},
{
 "date":   3108,
"name": "GSPC.Close",
"price":  94.32,
"rsi": 32.656,
"ret": 0.00053039 
},
{
 "date":   3109,
"name": "GSPC.Close",
"price":  94.89,
"rsi": 33.166,
"ret": 0.0060433 
},
{
 "date":   3112,
"name": "GSPC.Close",
"price":  95.27,
"rsi": 38.849,
"ret": 0.0040046 
},
{
 "date":   3113,
"name": "GSPC.Close",
"price":  95.93,
"rsi": 42.367,
"ret": 0.0069277 
},
{
 "date":   3114,
"name": "GSPC.Close",
"price":  96.24,
"rsi": 47.967,
"ret": 0.0032315 
},
{
 "date":   3115,
"name": "GSPC.Close",
"price":  96.25,
"rsi": 50.404,
"ret": 0.00010391 
},
{
 "date":   3116,
"name": "GSPC.Close",
"price":  97.58,
"rsi": 50.485,
"ret": 0.013818 
},
{
 "date":   3119,
"name": "GSPC.Close",
"price":  97.78,
"rsi": 59.833,
"ret": 0.0020496 
},
{
 "date":   3120,
"name": "GSPC.Close",
"price":  96.87,
"rsi": 61.024,
"ret": -0.0093066 
},
{
 "date":   3121,
"name": "GSPC.Close",
"price":  98.12,
"rsi":  53.28,
"ret": 0.012904 
},
{
 "date":   3122,
"name": "GSPC.Close",
"price":  98.03,
"rsi": 60.664,
"ret": -0.00091724 
},
{
 "date":   3123,
"name": "GSPC.Close",
"price":  97.75,
"rsi":  59.93,
"ret": -0.0028563 
},
{
 "date":   3126,
"name": "GSPC.Close",
"price":  97.72,
"rsi": 57.593,
"ret": -0.00030691 
},
{
 "date":   3127,
"name": "GSPC.Close",
"price":  98.44,
"rsi": 57.336,
"ret": 0.007368 
},
{
 "date":   3128,
"name": "GSPC.Close",
"price":  99.08,
"rsi": 61.761,
"ret": 0.0065014 
},
{
 "date":   3129,
"name": "GSPC.Close",
"price":  99.54,
"rsi": 65.215,
"ret": 0.0046427 
},
{
 "date":   3130,
"name": "GSPC.Close",
"price":    100,
"rsi": 67.489,
"ret": 0.0046213 
},
{
 "date":   3133,
"name": "GSPC.Close",
"price": 100.68,
"rsi": 69.626,
"ret": 0.0068 
},
{
 "date":   3134,
"name": "GSPC.Close",
"price": 100.66,
"rsi": 72.504,
"ret": -0.00019865 
},
{
 "date":   3135,
"name": "GSPC.Close",
"price": 102.92,
"rsi": 72.287,
"ret": 0.022452 
},
{
 "date":   3136,
"name": "GSPC.Close",
"price": 103.51,
"rsi": 79.685,
"ret": 0.0057326 
},
{
 "date":   3137,
"name": "GSPC.Close",
"price": 103.92,
"rsi": 81.103,
"ret": 0.003961 
},
{
 "date":   3140,
"name": "GSPC.Close",
"price": 103.55,
"rsi": 82.041,
"ret": -0.0035604 
},
{
 "date":   3141,
"name": "GSPC.Close",
"price": 104.01,
"rsi": 78.265,
"ret": 0.0044423 
},
{
 "date":   3142,
"name": "GSPC.Close",
"price":  104.5,
"rsi": 79.527,
"ret": 0.0047111 
},
{
 "date":   3143,
"name": "GSPC.Close",
"price": 103.66,
"rsi": 80.805,
"ret": -0.0080383 
},
{
 "date":   3144,
"name": "GSPC.Close",
"price": 103.96,
"rsi": 72.453,
"ret": 0.0028941 
},
{
 "date":   3147,
"name": "GSPC.Close",
"price": 103.97,
"rsi": 73.507,
"ret": 9.6191e-05 
},
{
 "date":   3148,
"name": "GSPC.Close",
"price": 103.85,
"rsi": 73.543,
"ret": -0.0011542 
},
{
 "date":   3149,
"name": "GSPC.Close",
"price": 104.65,
"rsi": 72.263,
"ret": 0.0077034 
},
{
 "date":   3150,
"name": "GSPC.Close",
"price": 105.08,
"rsi": 75.344,
"ret": 0.0041089 
},
{
 "date":   3151,
"name": "GSPC.Close",
"price": 104.73,
"rsi": 76.833,
"ret": -0.0033308 
},
{
 "date":   3154,
"name": "GSPC.Close",
"price": 103.89,
"rsi": 72.969,
"ret": -0.0080206 
},
{
 "date":   3155,
"name": "GSPC.Close",
"price": 104.31,
"rsi": 64.576,
"ret": 0.0040427 
},
{
 "date":   3156,
"name": "GSPC.Close",
"price": 104.91,
"rsi": 66.642,
"ret": 0.0057521 
},
{
 "date":   3157,
"name": "GSPC.Close",
"price": 105.08,
"rsi": 69.389,
"ret": 0.0016204 
},
{
 "date":   3158,
"name": "GSPC.Close",
"price":  104.9,
"rsi": 70.139,
"ret": -0.001713 
},
{
 "date":   3161,
"name": "GSPC.Close",
"price": 103.96,
"rsi": 68.232,
"ret": -0.0089609 
},
{
 "date":   3162,
"name": "GSPC.Close",
"price": 103.39,
"rsi": 59.183,
"ret": -0.0054829 
},
{
 "date":   3163,
"name": "GSPC.Close",
"price":  103.5,
"rsi": 54.466,
"ret": 0.0010639 
},
{
 "date":   3164,
"name": "GSPC.Close",
"price": 103.29,
"rsi": 55.208,
"ret": -0.002029 
},
{
 "date":   3165,
"name": "GSPC.Close",
"price": 103.68,
"rsi": 53.418,
"ret": 0.0037758 
},
{
 "date":   3169,
"name": "GSPC.Close",
"price": 104.49,
"rsi": 56.254,
"ret": 0.0078125 
},
{
 "date":   3170,
"name": "GSPC.Close",
"price": 105.38,
"rsi": 61.497,
"ret": 0.0085176 
},
{
 "date":   3171,
"name": "GSPC.Close",
"price": 105.42,
"rsi":  66.28,
"ret": 0.00037958 
},
{
 "date":   3172,
"name": "GSPC.Close",
"price": 106.79,
"rsi": 66.481,
"ret": 0.012996 
},
{
 "date":   3175,
"name": "GSPC.Close",
"price": 106.98,
"rsi": 72.535,
"ret": 0.0017792 
},
{
 "date":   3176,
"name": "GSPC.Close",
"price": 106.99,
"rsi": 73.256,
"ret": 9.3475e-05 
},
{
 "date":   3177,
"name": "GSPC.Close",
"price": 106.34,
"rsi": 73.296,
"ret": -0.0060753 
},
{
 "date":   3178,
"name": "GSPC.Close",
"price":  105.1,
"rsi": 66.388,
"ret": -0.011661 
},
{
 "date":   3179,
"name": "GSPC.Close",
"price": 104.12,
"rsi": 55.618,
"ret": -0.0093245 
},
{
 "date":   3182,
"name": "GSPC.Close",
"price": 103.21,
"rsi": 48.871,
"ret": -0.0087399 
},
{
 "date":   3183,
"name": "GSPC.Close",
"price": 102.53,
"rsi": 43.583,
"ret": -0.0065885 
},
{
 "date":   3184,
"name": "GSPC.Close",
"price": 101.73,
"rsi": 40.093,
"ret": -0.0078026 
},
{
 "date":   3185,
"name": "GSPC.Close",
"price":  101.9,
"rsi": 36.399,
"ret": 0.0016711 
},
{
 "date":   3186,
"name": "GSPC.Close",
"price": 101.84,
"rsi": 37.712,
"ret": -0.00058881 
},
{
 "date":   3189,
"name": "GSPC.Close",
"price": 101.86,
"rsi": 37.419,
"ret": 0.00019639 
},
{
 "date":   3190,
"name": "GSPC.Close",
"price": 102.62,
"rsi": 37.593,
"ret": 0.0074612 
},
{
 "date":   3191,
"name": "GSPC.Close",
"price": 101.66,
"rsi": 43.983,
"ret": -0.0093549 
},
{
 "date":   3192,
"name": "GSPC.Close",
"price": 101.96,
"rsi": 38.606,
"ret": 0.002951 
},
{
 "date":   3193,
"name": "GSPC.Close",
"price": 102.54,
"rsi": 41.032,
"ret": 0.0056885 
},
{
 "date":   3196,
"name": "GSPC.Close",
"price": 102.96,
"rsi": 45.515,
"ret": 0.004096 
},
{
 "date":   3197,
"name": "GSPC.Close",
"price":  102.6,
"rsi": 48.564,
"ret": -0.0034965 
},
{
 "date":   3198,
"name": "GSPC.Close",
"price": 103.06,
"rsi": 46.179,
"ret": 0.0044834 
},
{
 "date":   3199,
"name": "GSPC.Close",
"price": 103.27,
"rsi": 49.587,
"ret": 0.0020376 
},
{
 "date":   3200,
"name": "GSPC.Close",
"price": 103.52,
"rsi": 51.109,
"ret": 0.0024208 
},
{
 "date":   3203,
"name": "GSPC.Close",
"price": 104.59,
"rsi":  52.93,
"ret": 0.010336 
},
{
 "date":   3204,
"name": "GSPC.Close",
"price": 104.46,
"rsi":  59.83,
"ret": -0.0012429 
},
{
 "date":   3205,
"name": "GSPC.Close",
"price": 105.39,
"rsi": 58.704,
"ret": 0.0089029 
},
{
 "date":   3206,
"name": "GSPC.Close",
"price": 104.88,
"rsi": 63.933,
"ret": -0.0048392 
},
{
 "date":   3207,
"name": "GSPC.Close",
"price": 104.66,
"rsi": 59.485,
"ret": -0.0020976 
},
{
 "date":   3210,
"name": "GSPC.Close",
"price": 102.61,
"rsi": 57.622,
"ret": -0.019587 
},
{
 "date":   3211,
"name": "GSPC.Close",
"price": 101.26,
"rsi": 43.846,
"ret": -0.013157 
},
{
 "date":   3212,
"name": "GSPC.Close",
"price": 100.49,
"rsi":  37.49,
"ret": -0.0076042 
},
{
 "date":   3213,
"name": "GSPC.Close",
"price":  99.33,
"rsi": 34.425,
"ret": -0.011543 
},
{
 "date":   3214,
"name": "GSPC.Close",
"price":  97.95,
"rsi": 30.393,
"ret": -0.013893 
},
{
 "date":   3217,
"name": "GSPC.Close",
"price":  98.18,
"rsi": 26.427,
"ret": 0.0023481 
},
{
 "date":   3218,
"name": "GSPC.Close",
"price":  97.49,
"rsi": 28.111,
"ret": -0.0070279 
},
{
 "date":   3219,
"name": "GSPC.Close",
"price":  97.31,
"rsi": 26.176,
"ret": -0.0018463 
},
{
 "date":   3220,
"name": "GSPC.Close",
"price":  96.03,
"rsi": 25.679,
"ret": -0.013154 
},
{
 "date":   3221,
"name": "GSPC.Close",
"price":  94.59,
"rsi": 22.422,
"ret": -0.014995 
},
{
 "date":   3224,
"name": "GSPC.Close",
"price":  95.06,
"rsi": 19.435,
"ret": 0.0049688 
},
{
 "date":   3225,
"name": "GSPC.Close",
"price":  93.15,
"rsi": 23.038,
"ret": -0.020093 
},
{
 "date":   3226,
"name": "GSPC.Close",
"price":  96.85,
"rsi": 19.267,
"ret": 0.039721 
},
{
 "date":   3227,
"name": "GSPC.Close",
"price":  95.61,
"rsi":  39.82,
"ret": -0.012803 
},
{
 "date":   3228,
"name": "GSPC.Close",
"price":  96.18,
"rsi": 36.469,
"ret": 0.0059617 
},
{
 "date":   3231,
"name": "GSPC.Close",
"price":  95.19,
"rsi":  39.01,
"ret": -0.010293 
},
{
 "date":   3232,
"name": "GSPC.Close",
"price":  93.85,
"rsi": 36.295,
"ret": -0.014077 
},
{
 "date":   3233,
"name": "GSPC.Close",
"price":  94.45,
"rsi": 32.952,
"ret": 0.0063932 
},
{
 "date":   3234,
"name": "GSPC.Close",
"price":  94.42,
"rsi": 35.803,
"ret": -0.00031763 
},
{
 "date":   3235,
"name": "GSPC.Close",
"price":  94.77,
"rsi": 35.722,
"ret": 0.0037068 
},
{
 "date":   3238,
"name": "GSPC.Close",
"price":  93.13,
"rsi": 37.515,
"ret": -0.017305 
},
{
 "date":   3239,
"name": "GSPC.Close",
"price":  92.49,
"rsi": 32.885,
"ret": -0.0068721 
},
{
 "date":   3240,
"name": "GSPC.Close",
"price":  92.71,
"rsi": 31.263,
"ret": 0.0023786 
},
{
 "date":   3241,
"name": "GSPC.Close",
"price":  93.71,
"rsi": 32.496,
"ret": 0.010786 
},
{
 "date":   3242,
"name": "GSPC.Close",
"price":  94.42,
"rsi": 37.942,
"ret": 0.0075766 
},
{
 "date":   3245,
"name": "GSPC.Close",
"price":  95.25,
"rsi": 41.547,
"ret": 0.0087905 
},
{
 "date":   3246,
"name": "GSPC.Close",
"price":  95.01,
"rsi": 45.532,
"ret": -0.0025197 
},
{
 "date":   3247,
"name": "GSPC.Close",
"price":  95.48,
"rsi": 44.585,
"ret": 0.0049468 
},
{
 "date":   3249,
"name": "GSPC.Close",
"price":  95.79,
"rsi": 46.912,
"ret": 0.0032468 
},
{
 "date":   3252,
"name": "GSPC.Close",
"price":  95.99,
"rsi":  48.45,
"ret": 0.0020879 
},
{
 "date":   3253,
"name": "GSPC.Close",
"price":  95.15,
"rsi": 49.467,
"ret": -0.0087509 
},
{
 "date":   3254,
"name": "GSPC.Close",
"price":  93.75,
"rsi": 45.415,
"ret": -0.014714 
},
{
 "date":   3255,
"name": "GSPC.Close",
"price":   94.7,
"rsi": 39.593,
"ret": 0.010133 
},
{
 "date":   3256,
"name": "GSPC.Close",
"price":  96.28,
"rsi": 44.767,
"ret": 0.016684 
},
{
 "date":   3259,
"name": "GSPC.Close",
"price":  96.15,
"rsi": 52.113,
"ret": -0.0013502 
},
{
 "date":   3260,
"name": "GSPC.Close",
"price":  97.44,
"rsi": 51.506,
"ret": 0.013417 
},
{
 "date":   3261,
"name": "GSPC.Close",
"price":  97.49,
"rsi": 56.874,
"ret": 0.00051314 
},
{
 "date":   3262,
"name": "GSPC.Close",
"price":  97.08,
"rsi": 57.073,
"ret": -0.0042056 
},
{
 "date":   3263,
"name": "GSPC.Close",
"price":  96.63,
"rsi": 54.845,
"ret": -0.0046354 
},
{
 "date":   3266,
"name": "GSPC.Close",
"price":  97.11,
"rsi": 52.427,
"ret": 0.0049674 
},
{
 "date":   3267,
"name": "GSPC.Close",
"price":  96.59,
"rsi":  54.72,
"ret": -0.0053548 
},
{
 "date":   3268,
"name": "GSPC.Close",
"price":  96.06,
"rsi": 51.806,
"ret": -0.0054871 
},
{
 "date":   3269,
"name": "GSPC.Close",
"price":  96.04,
"rsi": 48.945,
"ret": -0.0002082 
},
{
 "date":   3270,
"name": "GSPC.Close",
"price":  95.33,
"rsi": 48.836,
"ret": -0.0073928 
},
{
 "date":   3273,
"name": "GSPC.Close",
"price":  93.44,
"rsi": 44.984,
"ret": -0.019826 
},
{
 "date":   3274,
"name": "GSPC.Close",
"price":  94.24,
"rsi":  36.69,
"ret": 0.0085616 
},
{
 "date":   3275,
"name": "GSPC.Close",
"price":  94.68,
"rsi": 41.599,
"ret": 0.0046689 
},
{
 "date":   3276,
"name": "GSPC.Close",
"price":  94.71,
"rsi": 44.163,
"ret": 0.00031686 
},
{
 "date":   3277,
"name": "GSPC.Close",
"price":  96.31,
"rsi": 44.342,
"ret": 0.016894 
},
{
 "date":   3281,
"name": "GSPC.Close",
"price":  97.52,
"rsi": 53.015,
"ret": 0.012564 
},
{
 "date":   3282,
"name": "GSPC.Close",
"price":  96.66,
"rsi": 58.306,
"ret": -0.0088187 
},
{
 "date":   3283,
"name": "GSPC.Close",
"price":  96.28,
"rsi": 53.679,
"ret": -0.0039313 
},
{
 "date":   3284,
"name": "GSPC.Close",
"price":  96.11,
"rsi": 51.726,
"ret": -0.0017657 
},
{
 "date":   3288,
"name": "GSPC.Close",
"price":  96.73,
"rsi": 50.835,
"ret": 0.0064509 
},
{
 "date":   3289,
"name": "GSPC.Close",
"price":   97.8,
"rsi": 53.951,
"ret": 0.011062 
},
{
 "date":   3290,
"name": "GSPC.Close",
"price":  98.58,
"rsi": 58.803,
"ret": 0.0079755 
},
{
 "date":   3291,
"name": "GSPC.Close",
"price":  99.13,
"rsi": 61.951,
"ret": 0.0055792 
},
{
 "date":   3294,
"name": "GSPC.Close",
"price":   98.8,
"rsi": 64.037,
"ret": -0.003329 
},
{
 "date":   3295,
"name": "GSPC.Close",
"price":  99.33,
"rsi": 61.846,
"ret": 0.0053644 
},
{
 "date":   3296,
"name": "GSPC.Close",
"price":  98.77,
"rsi": 63.978,
"ret": -0.0056378 
},
{
 "date":   3297,
"name": "GSPC.Close",
"price":   99.1,
"rsi": 60.153,
"ret": 0.0033411 
},
{
 "date":   3298,
"name": "GSPC.Close",
"price":  99.93,
"rsi":  61.61,
"ret": 0.0083754 
},
{
 "date":   3301,
"name": "GSPC.Close",
"price": 100.69,
"rsi": 65.068,
"ret": 0.0076053 
},
{
 "date":   3302,
"name": "GSPC.Close",
"price":  99.46,
"rsi": 67.918,
"ret": -0.012216 
},
{
 "date":   3303,
"name": "GSPC.Close",
"price":  99.48,
"rsi": 59.463,
"ret": 0.00020109 
},
{
 "date":   3304,
"name": "GSPC.Close",
"price":  99.72,
"rsi": 59.551,
"ret": 0.0024125 
},
{
 "date":   3305,
"name": "GSPC.Close",
"price":  99.75,
"rsi": 60.657,
"ret": 0.00030084 
},
{
 "date":   3308,
"name": "GSPC.Close",
"price":   99.9,
"rsi": 60.801,
"ret": 0.0015038 
},
{
 "date":   3309,
"name": "GSPC.Close",
"price":  100.6,
"rsi":  61.56,
"ret": 0.007007 
},
{
 "date":   3310,
"name": "GSPC.Close",
"price": 100.16,
"rsi": 64.969,
"ret": -0.0043738 
},
{
 "date":   3311,
"name": "GSPC.Close",
"price": 101.19,
"rsi":  61.29,
"ret": 0.010284 
},
{
 "date":   3312,
"name": "GSPC.Close",
"price": 101.86,
"rsi": 66.126,
"ret": 0.0066212 
},
{
 "date":   3315,
"name": "GSPC.Close",
"price": 101.55,
"rsi": 68.852,
"ret": -0.0030434 
},
{
 "date":   3316,
"name": "GSPC.Close",
"price": 101.05,
"rsi": 66.198,
"ret": -0.0049237 
},
{
 "date":   3317,
"name": "GSPC.Close",
"price":  99.93,
"rsi": 62.043,
"ret": -0.011084 
},
{
 "date":   3318,
"name": "GSPC.Close",
"price":  99.96,
"rsi": 53.884,
"ret": 0.00030021 
},
{
 "date":   3319,
"name": "GSPC.Close",
"price":   99.5,
"rsi": 54.058,
"ret": -0.0046018 
},
{
 "date":   3322,
"name": "GSPC.Close",
"price":  98.09,
"rsi": 50.883,
"ret": -0.014171 
},
{
 "date":   3323,
"name": "GSPC.Close",
"price":  98.05,
"rsi":  42.62,
"ret": -0.00040779 
},
{
 "date":   3324,
"name": "GSPC.Close",
"price":  97.16,
"rsi": 42.409,
"ret": -0.009077 
},
{
 "date":   3325,
"name": "GSPC.Close",
"price":  97.65,
"rsi": 37.923,
"ret": 0.0050432 
},
{
 "date":   3326,
"name": "GSPC.Close",
"price":  97.87,
"rsi": 41.587,
"ret": 0.0022529 
},
{
 "date":   3329,
"name": "GSPC.Close",
"price":   98.2,
"rsi": 43.208,
"ret": 0.0033718 
},
{
 "date":   3330,
"name": "GSPC.Close",
"price":  98.93,
"rsi": 45.644,
"ret": 0.0074338 
},
{
 "date":   3331,
"name": "GSPC.Close",
"price":  98.87,
"rsi": 50.683,
"ret": -0.00060649 
},
{
 "date":   3332,
"name": "GSPC.Close",
"price":  98.73,
"rsi": 50.271,
"ret": -0.001416 
},
{
 "date":   3333,
"name": "GSPC.Close",
"price":  98.67,
"rsi": 49.263,
"ret": -0.00060772 
},
{
 "date":   3337,
"name": "GSPC.Close",
"price":  99.42,
"rsi": 48.812,
"ret": 0.0076011 
},
{
 "date":   3338,
"name": "GSPC.Close",
"price":  99.07,
"rsi": 54.434,
"ret": -0.0035204 
},
{
 "date":   3339,
"name": "GSPC.Close",
"price":  98.33,
"rsi": 51.587,
"ret": -0.0074695 
},
{
 "date":   3340,
"name": "GSPC.Close",
"price":  97.78,
"rsi": 46.096,
"ret": -0.0055934 
},
{
 "date":   3343,
"name": "GSPC.Close",
"price":  97.67,
"rsi": 42.477,
"ret": -0.001125 
},
{
 "date":   3344,
"name": "GSPC.Close",
"price":  96.13,
"rsi": 41.771,
"ret": -0.015767 
},
{
 "date":   3345,
"name": "GSPC.Close",
"price":  96.28,
"rsi": 33.398,
"ret": 0.0015604 
},
{
 "date":   3346,
"name": "GSPC.Close",
"price":   96.9,
"rsi":  34.77,
"ret": 0.0064396 
},
{
 "date":   3347,
"name": "GSPC.Close",
"price":  96.97,
"rsi": 40.247,
"ret": 0.00072239 
},
{
 "date":   3350,
"name": "GSPC.Close",
"price":  98.06,
"rsi": 40.851,
"ret": 0.011241 
},
{
 "date":   3351,
"name": "GSPC.Close",
"price":  97.87,
"rsi": 49.422,
"ret": -0.0019376 
},
{
 "date":   3352,
"name": "GSPC.Close",
"price":  98.44,
"rsi": 48.113,
"ret": 0.0058241 
},
{
 "date":   3353,
"name": "GSPC.Close",
"price":  99.58,
"rsi": 52.203,
"ret": 0.011581 
},
{
 "date":   3354,
"name": "GSPC.Close",
"price":  99.54,
"rsi": 59.139,
"ret": -0.00040169 
},
{
 "date":   3357,
"name": "GSPC.Close",
"price":  99.67,
"rsi": 58.817,
"ret": 0.001306 
},
{
 "date":   3358,
"name": "GSPC.Close",
"price":  99.84,
"rsi": 59.588,
"ret": 0.0017056 
},
{
 "date":   3359,
"name": "GSPC.Close",
"price":  99.71,
"rsi": 60.627,
"ret": -0.0013021 
},
{
 "date":   3360,
"name": "GSPC.Close",
"price":  99.86,
"rsi":  59.37,
"ret": 0.0015044 
},
{
 "date":   3361,
"name": "GSPC.Close",
"price": 100.69,
"rsi":  60.39,
"ret": 0.0083116 
},
{
 "date":   3364,
"name": "GSPC.Close",
"price": 101.06,
"rsi": 65.545,
"ret": 0.0036746 
},
{
 "date":   3365,
"name": "GSPC.Close",
"price":  100.5,
"rsi": 67.571,
"ret": -0.0055413 
},
{
 "date":   3366,
"name": "GSPC.Close",
"price": 101.25,
"rsi": 61.661,
"ret": 0.0074627 
},
{
 "date":   3367,
"name": "GSPC.Close",
"price": 101.67,
"rsi": 65.956,
"ret": 0.0041481 
},
{
 "date":   3368,
"name": "GSPC.Close",
"price":  101.6,
"rsi":  68.11,
"ret": -0.0006885 
},
{
 "date":   3371,
"name": "GSPC.Close",
"price": 101.04,
"rsi": 67.345,
"ret": -0.0055118 
},
{
 "date":   3372,
"name": "GSPC.Close",
"price": 102.48,
"rsi": 61.404,
"ret": 0.014252 
},
{
 "date":   3373,
"name": "GSPC.Close",
"price": 102.12,
"rsi": 68.982,
"ret": -0.0035129 
},
{
 "date":   3374,
"name": "GSPC.Close",
"price": 102.03,
"rsi": 65.519,
"ret": -0.00088132 
},
{
 "date":   3375,
"name": "GSPC.Close",
"price": 101.59,
"rsi": 64.645,
"ret": -0.0043125 
},
{
 "date":   3378,
"name": "GSPC.Close",
"price":  100.9,
"rsi": 60.403,
"ret": -0.006792 
},
{
 "date":   3379,
"name": "GSPC.Close",
"price":  102.4,
"rsi": 54.378,
"ret": 0.014866 
},
{
 "date":   3380,
"name": "GSPC.Close",
"price": 102.65,
"rsi": 63.015,
"ret": 0.0024414 
},
{
 "date":   3381,
"name": "GSPC.Close",
"price": 103.26,
"rsi": 64.231,
"ret": 0.0059425 
},
{
 "date":   3382,
"name": "GSPC.Close",
"price": 103.18,
"rsi": 67.074,
"ret": -0.00077474 
},
{
 "date":   3385,
"name": "GSPC.Close",
"price": 102.87,
"rsi": 66.329,
"ret": -0.0030045 
},
{
 "date":   3386,
"name": "GSPC.Close",
"price": 103.34,
"rsi": 63.392,
"ret": 0.0045689 
},
{
 "date":   3387,
"name": "GSPC.Close",
"price": 102.31,
"rsi": 65.861,
"ret": -0.0099671 
},
{
 "date":   3388,
"name": "GSPC.Close",
"price":    102,
"rsi": 56.819,
"ret": -0.00303 
},
{
 "date":   3392,
"name": "GSPC.Close",
"price": 101.12,
"rsi": 54.399,
"ret": -0.0086275 
},
{
 "date":   3393,
"name": "GSPC.Close",
"price": 101.24,
"rsi": 48.131,
"ret": 0.0011867 
},
{
 "date":   3394,
"name": "GSPC.Close",
"price":  101.7,
"rsi": 48.994,
"ret": 0.0045437 
},
{
 "date":   3395,
"name": "GSPC.Close",
"price": 101.28,
"rsi": 52.272,
"ret": -0.0041298 
},
{
 "date":   3396,
"name": "GSPC.Close",
"price": 101.23,
"rsi": 49.165,
"ret": -0.00049368 
},
{
 "date":   3399,
"name": "GSPC.Close",
"price": 101.57,
"rsi": 48.793,
"ret": 0.0033587 
},
{
 "date":   3400,
"name": "GSPC.Close",
"price":  102.2,
"rsi": 51.481,
"ret": 0.0062026 
},
{
 "date":   3401,
"name": "GSPC.Close",
"price":  102.5,
"rsi":  56.08,
"ret": 0.0029354 
},
{
 "date":   3402,
"name": "GSPC.Close",
"price": 102.01,
"rsi": 58.116,
"ret": -0.0047805 
},
{
 "date":   3403,
"name": "GSPC.Close",
"price":  101.8,
"rsi": 53.734,
"ret": -0.0020586 
},
{
 "date":   3406,
"name": "GSPC.Close",
"price": 101.76,
"rsi": 51.927,
"ret": -0.00039293 
},
{
 "date":   3407,
"name": "GSPC.Close",
"price": 101.68,
"rsi": 51.572,
"ret": -0.00078616 
},
{
 "date":   3408,
"name": "GSPC.Close",
"price": 101.72,
"rsi": 50.822,
"ret": 0.00039339 
},
{
 "date":   3409,
"name": "GSPC.Close",
"price": 101.81,
"rsi": 51.204,
"ret": 0.00088478 
},
{
 "date":   3410,
"name": "GSPC.Close",
"price": 100.69,
"rsi": 52.105,
"ret": -0.011001 
},
{
 "date":   3413,
"name": "GSPC.Close",
"price":  99.02,
"rsi": 41.764,
"ret": -0.016586 
},
{
 "date":   3414,
"name": "GSPC.Close",
"price":  99.17,
"rsi":  31.67,
"ret": 0.0015148 
},
{
 "date":   3415,
"name": "GSPC.Close",
"price":  99.46,
"rsi": 33.231,
"ret": 0.0029243 
},
{
 "date":   3416,
"name": "GSPC.Close",
"price":  98.52,
"rsi": 36.262,
"ret": -0.009451 
},
{
 "date":   3417,
"name": "GSPC.Close",
"price":  98.52,
"rsi": 31.302,
"ret":      0 
},
{
 "date":   3420,
"name": "GSPC.Close",
"price":  98.06,
"rsi": 31.302,
"ret": -0.0046691 
},
{
 "date":   3421,
"name": "GSPC.Close",
"price":  98.14,
"rsi": 29.046,
"ret": 0.00081583 
},
{
 "date":   3422,
"name": "GSPC.Close",
"price":  98.42,
"rsi": 29.991,
"ret": 0.0028531 
},
{
 "date":   3423,
"name": "GSPC.Close",
"price":  99.94,
"rsi": 33.337,
"ret": 0.015444 
},
{
 "date":   3424,
"name": "GSPC.Close",
"price":  99.93,
"rsi": 47.894,
"ret": -0.00010006 
},
{
 "date":   3427,
"name": "GSPC.Close",
"price": 100.14,
"rsi":  47.82,
"ret": 0.0021015 
},
{
 "date":   3428,
"name": "GSPC.Close",
"price": 100.51,
"rsi": 49.581,
"ret": 0.0036948 
},
{
 "date":   3429,
"name": "GSPC.Close",
"price":  99.89,
"rsi": 52.616,
"ret": -0.0061685 
},
{
 "date":   3430,
"name": "GSPC.Close",
"price":  99.93,
"rsi": 47.461,
"ret": 0.00040044 
},
{
 "date":   3431,
"name": "GSPC.Close",
"price": 100.22,
"rsi": 47.816,
"ret": 0.002902 
},
{
 "date":   3435,
"name": "GSPC.Close",
"price": 100.05,
"rsi": 50.433,
"ret": -0.0016963 
},
{
 "date":   3436,
"name": "GSPC.Close",
"price":  99.11,
"rsi": 48.885,
"ret": -0.0093953 
},
{
 "date":   3437,
"name": "GSPC.Close",
"price":  99.08,
"rsi": 41.333,
"ret": -0.00030269 
},
{
 "date":   3438,
"name": "GSPC.Close",
"price":  99.17,
"rsi": 41.114,
"ret": 0.00090836 
},
{
 "date":   3441,
"name": "GSPC.Close",
"price":  99.32,
"rsi": 42.102,
"ret": 0.0015126 
},
{
 "date":   3442,
"name": "GSPC.Close",
"price": 100.62,
"rsi": 43.795,
"ret": 0.013089 
},
{
 "date":   3443,
"name": "GSPC.Close",
"price":  101.3,
"rsi": 55.843,
"ret": 0.0067581 
},
{
 "date":   3444,
"name": "GSPC.Close",
"price": 101.79,
"rsi": 60.601,
"ret": 0.0048371 
},
{
 "date":   3445,
"name": "GSPC.Close",
"price": 101.49,
"rsi": 63.641,
"ret": -0.0029472 
},
{
 "date":   3448,
"name": "GSPC.Close",
"price": 101.91,
"rsi":  60.56,
"ret": 0.0041383 
},
{
 "date":   3449,
"name": "GSPC.Close",
"price": 102.85,
"rsi": 63.243,
"ret": 0.0092238 
},
{
 "date":   3450,
"name": "GSPC.Close",
"price": 102.31,
"rsi":  68.42,
"ret": -0.0052504 
},
{
 "date":   3451,
"name": "GSPC.Close",
"price":  102.2,
"rsi": 62.936,
"ret": -0.0010752 
},
{
 "date":   3452,
"name": "GSPC.Close",
"price": 102.09,
"rsi": 61.848,
"ret": -0.0010763 
},
{
 "date":   3455,
"name": "GSPC.Close",
"price": 101.56,
"rsi": 60.718,
"ret": -0.0051915 
},
{
 "date":   3456,
"name": "GSPC.Close",
"price": 101.58,
"rsi": 55.461,
"ret": 0.00019693 
},
{
 "date":   3457,
"name": "GSPC.Close",
"price": 101.63,
"rsi": 55.617,
"ret": 0.00049222 
},
{
 "date":   3458,
"name": "GSPC.Close",
"price": 102.09,
"rsi": 56.032,
"ret": 0.0045262 
},
{
 "date":   3459,
"name": "GSPC.Close",
"price": 102.64,
"rsi": 59.761,
"ret": 0.0053874 
},
{
 "date":   3462,
"name": "GSPC.Close",
"price": 102.09,
"rsi": 63.722,
"ret": -0.0053585 
},
{
 "date":   3463,
"name": "GSPC.Close",
"price": 101.66,
"rsi": 57.614,
"ret": -0.004212 
},
{
 "date":   3464,
"name": "GSPC.Close",
"price": 102.27,
"rsi": 53.311,
"ret": 0.0060004 
},
{
 "date":   3465,
"name": "GSPC.Close",
"price":  102.8,
"rsi": 58.093,
"ret": 0.0051824 
},
{
 "date":   3466,
"name": "GSPC.Close",
"price": 102.91,
"rsi": 61.757,
"ret": 0.00107 
},
{
 "date":   3469,
"name": "GSPC.Close",
"price": 101.99,
"rsi":  62.49,
"ret": -0.0089399 
},
{
 "date":   3470,
"name": "GSPC.Close",
"price": 102.09,
"rsi": 53.289,
"ret": 0.00098049 
},
{
 "date":   3472,
"name": "GSPC.Close",
"price": 102.43,
"rsi": 54.081,
"ret": 0.0033304 
},
{
 "date":   3473,
"name": "GSPC.Close",
"price": 103.62,
"rsi": 56.763,
"ret": 0.011618 
},
{
 "date":   3476,
"name": "GSPC.Close",
"price": 104.47,
"rsi": 64.565,
"ret": 0.008203 
},
{
 "date":   3477,
"name": "GSPC.Close",
"price":  104.2,
"rsi": 68.884,
"ret": -0.0025845 
},
{
 "date":   3478,
"name": "GSPC.Close",
"price": 103.64,
"rsi": 66.127,
"ret": -0.0053743 
},
{
 "date":   3479,
"name": "GSPC.Close",
"price": 102.69,
"rsi":   60.7,
"ret": -0.0091663 
},
{
 "date":   3480,
"name": "GSPC.Close",
"price": 102.32,
"rsi": 52.786,
"ret": -0.0036031 
},
{
 "date":   3483,
"name": "GSPC.Close",
"price": 102.74,
"rsi": 50.049,
"ret": 0.0041048 
},
{
 "date":   3484,
"name": "GSPC.Close",
"price": 101.83,
"rsi": 53.026,
"ret": -0.0088573 
},
{
 "date":   3485,
"name": "GSPC.Close",
"price": 101.69,
"rsi": 46.552,
"ret": -0.0013748 
},
{
 "date":   3486,
"name": "GSPC.Close",
"price": 101.61,
"rsi": 45.629,
"ret": -0.0007867 
},
{
 "date":   3487,
"name": "GSPC.Close",
"price": 101.82,
"rsi": 45.079,
"ret": 0.0020667 
},
{
 "date":   3490,
"name": "GSPC.Close",
"price": 101.59,
"rsi": 46.889,
"ret": -0.0022589 
},
{
 "date":   3491,
"name": "GSPC.Close",
"price": 101.97,
"rsi": 45.134,
"ret": 0.0037405 
},
{
 "date":   3492,
"name": "GSPC.Close",
"price": 103.08,
"rsi": 48.559,
"ret": 0.010886 
},
{
 "date":   3493,
"name": "GSPC.Close",
"price":  103.1,
"rsi": 57.002,
"ret": 0.00019402 
},
{
 "date":   3494,
"name": "GSPC.Close",
"price":  103.1,
"rsi": 57.138,
"ret":      0 
},
{
 "date":   3497,
"name": "GSPC.Close",
"price": 103.15,
"rsi": 57.138,
"ret": 0.00048497 
},
{
 "date":   3498,
"name": "GSPC.Close",
"price": 103.81,
"rsi": 57.529,
"ret": 0.0063984 
},
{
 "date":   3499,
"name": "GSPC.Close",
"price": 104.17,
"rsi": 62.404,
"ret": 0.0034679 
},
{
 "date":   3500,
"name": "GSPC.Close",
"price":  104.1,
"rsi": 64.778,
"ret": -0.00067198 
},
{
 "date":   3501,
"name": "GSPC.Close",
"price": 104.04,
"rsi": 63.933,
"ret": -0.00057637 
},
{
 "date":   3504,
"name": "GSPC.Close",
"price":  104.3,
"rsi": 63.171,
"ret": 0.002499 
},
{
 "date":   3505,
"name": "GSPC.Close",
"price": 105.65,
"rsi":  65.11,
"ret": 0.012943 
},
{
 "date":   3506,
"name": "GSPC.Close",
"price": 105.98,
"rsi": 73.044,
"ret": 0.0031235 
},
{
 "date":   3507,
"name": "GSPC.Close",
"price": 105.49,
"rsi": 74.566,
"ret": -0.0046235 
},
{
 "date":   3508,
"name": "GSPC.Close",
"price":  106.4,
"rsi":  68.39,
"ret": 0.0086264 
},
{
 "date":   3511,
"name": "GSPC.Close",
"price": 107.42,
"rsi": 72.882,
"ret": 0.0095865 
},
{
 "date":   3512,
"name": "GSPC.Close",
"price": 107.52,
"rsi": 76.853,
"ret": 0.00093093 
},
{
 "date":   3513,
"name": "GSPC.Close",
"price": 108.25,
"rsi": 77.206,
"ret": 0.0067894 
},
{
 "date":   3514,
"name": "GSPC.Close",
"price": 108.09,
"rsi": 79.642,
"ret": -0.0014781 
},
{
 "date":   3515,
"name": "GSPC.Close",
"price":  108.3,
"rsi": 77.682,
"ret": 0.0019428 
},
{
 "date":   3518,
"name": "GSPC.Close",
"price": 108.83,
"rsi": 78.432,
"ret": 0.0048938 
},
{
 "date":   3519,
"name": "GSPC.Close",
"price": 108.91,
"rsi": 80.238,
"ret": 0.00073509 
},
{
 "date":   3520,
"name": "GSPC.Close",
"price": 108.99,
"rsi": 80.503,
"ret": 0.00073455 
},
{
 "date":   3521,
"name": "GSPC.Close",
"price": 108.63,
"rsi": 80.781,
"ret": -0.0033031 
},
{
 "date":   3522,
"name": "GSPC.Close",
"price":  108.6,
"rsi": 75.562,
"ret": -0.00027617 
},
{
 "date":   3525,
"name": "GSPC.Close",
"price": 109.14,
"rsi": 75.126,
"ret": 0.0049724 
},
{
 "date":   3526,
"name": "GSPC.Close",
"price": 109.02,
"rsi": 77.627,
"ret": -0.0010995 
},
{
 "date":   3527,
"name": "GSPC.Close",
"price": 109.02,
"rsi": 75.803,
"ret":      0 
},
{
 "date":   3528,
"name": "GSPC.Close",
"price": 109.02,
"rsi": 75.803,
"ret":      0 
},
{
 "date":   3529,
"name": "GSPC.Close",
"price": 109.32,
"rsi": 75.803,
"ret": 0.0027518 
},
{
 "date":   3533,
"name": "GSPC.Close",
"price": 107.44,
"rsi": 77.457,
"ret": -0.017197 
},
{
 "date":   3534,
"name": "GSPC.Close",
"price":  106.4,
"rsi":  53.01,
"ret": -0.0096798 
},
{
 "date":   3535,
"name": "GSPC.Close",
"price": 106.85,
"rsi":  44.62,
"ret": 0.0042293 
},
{
 "date":   3536,
"name": "GSPC.Close",
"price": 107.66,
"rsi": 48.424,
"ret": 0.0075807 
},
{
 "date":   3539,
"name": "GSPC.Close",
"price": 108.17,
"rsi": 54.484,
"ret": 0.0047371 
},
{
 "date":   3540,
"name": "GSPC.Close",
"price": 107.51,
"rsi": 57.843,
"ret": -0.0061015 
},
{
 "date":   3541,
"name": "GSPC.Close",
"price": 107.82,
"rsi": 52.449,
"ret": 0.0028835 
},
{
 "date":   3542,
"name": "GSPC.Close",
"price": 107.85,
"rsi": 54.591,
"ret": 0.00027824 
},
{
 "date":   3543,
"name": "GSPC.Close",
"price": 108.76,
"rsi": 54.803,
"ret": 0.0084376 
},
{
 "date":   3546,
"name": "GSPC.Close",
"price": 108.84,
"rsi": 60.788,
"ret": 0.00073556 
},
{
 "date":   3547,
"name": "GSPC.Close",
"price":    108,
"rsi": 61.273,
"ret": -0.0077178 
},
{
 "date":   3548,
"name": "GSPC.Close",
"price": 108.28,
"rsi": 53.748,
"ret": 0.0025926 
},
{
 "date":   3549,
"name": "GSPC.Close",
"price": 110.51,
"rsi": 55.701,
"ret": 0.020595 
},
{
 "date":   3550,
"name": "GSPC.Close",
"price": 110.47,
"rsi": 67.479,
"ret": -0.00036196 
},
{
 "date":   3553,
"name": "GSPC.Close",
"price": 109.61,
"rsi": 67.134,
"ret": -0.0077849 
},
{
 "date":   3554,
"name": "GSPC.Close",
"price": 109.68,
"rsi": 60.032,
"ret": 0.00063863 
},
{
 "date":   3555,
"name": "GSPC.Close",
"price": 109.96,
"rsi": 60.399,
"ret": 0.0025529 
},
{
 "date":   3556,
"name": "GSPC.Close",
"price": 110.21,
"rsi": 61.907,
"ret": 0.0022736 
},
{
 "date":   3557,
"name": "GSPC.Close",
"price": 109.32,
"rsi": 63.252,
"ret": -0.0080755 
},
{
 "date":   3560,
"name": "GSPC.Close",
"price": 108.56,
"rsi": 55.709,
"ret": -0.0069521 
},
{
 "date":   3561,
"name": "GSPC.Close",
"price": 109.59,
"rsi": 50.204,
"ret": 0.0094878 
},
{
 "date":   3562,
"name": "GSPC.Close",
"price": 109.59,
"rsi": 56.481,
"ret":      0 
},
{
 "date":   3563,
"name": "GSPC.Close",
"price": 110.17,
"rsi": 56.481,
"ret": 0.0052925 
},
{
 "date":   3564,
"name": "GSPC.Close",
"price": 111.27,
"rsi": 59.791,
"ret": 0.0099846 
},
{
 "date":   3567,
"name": "GSPC.Close",
"price": 109.88,
"rsi": 65.198,
"ret": -0.012492 
},
{
 "date":   3568,
"name": "GSPC.Close",
"price": 106.63,
"rsi": 55.113,
"ret": -0.029578 
},
{
 "date":   3569,
"name": "GSPC.Close",
"price":  105.3,
"rsi": 39.665,
"ret": -0.012473 
},
{
 "date":   3570,
"name": "GSPC.Close",
"price": 105.05,
"rsi": 35.303,
"ret": -0.0023742 
},
{
 "date":   3571,
"name": "GSPC.Close",
"price": 104.49,
"rsi": 34.535,
"ret": -0.0053308 
},
{
 "date":   3574,
"name": "GSPC.Close",
"price": 103.36,
"rsi": 32.811,
"ret": -0.010814 
},
{
 "date":   3575,
"name": "GSPC.Close",
"price": 103.19,
"rsi": 29.601,
"ret": -0.0016447 
},
{
 "date":   3576,
"name": "GSPC.Close",
"price": 103.39,
"rsi":  29.14,
"ret": 0.0019382 
},
{
 "date":   3577,
"name": "GSPC.Close",
"price": 103.61,
"rsi": 30.513,
"ret": 0.0021279 
},
{
 "date":   3578,
"name": "GSPC.Close",
"price":  101.6,
"rsi": 32.073,
"ret": -0.0194 
},
{
 "date":   3581,
"name": "GSPC.Close",
"price": 100.71,
"rsi": 26.271,
"ret": -0.0087598 
},
{
 "date":   3582,
"name": "GSPC.Close",
"price": 100.28,
"rsi": 24.184,
"ret": -0.0042697 
},
{
 "date":   3583,
"name": "GSPC.Close",
"price": 100.44,
"rsi": 23.225,
"ret": 0.0015955 
},
{
 "date":   3584,
"name": "GSPC.Close",
"price":    100,
"rsi": 24.426,
"ret": -0.0043807 
},
{
 "date":   3585,
"name": "GSPC.Close",
"price": 100.57,
"rsi": 23.344,
"ret": 0.0057 
},
{
 "date":   3588,
"name": "GSPC.Close",
"price": 100.71,
"rsi": 27.806,
"ret": 0.0013921 
},
{
 "date":   3589,
"name": "GSPC.Close",
"price": 102.67,
"rsi": 28.901,
"ret": 0.019462 
},
{
 "date":   3590,
"name": "GSPC.Close",
"price": 101.82,
"rsi":  42.13,
"ret": -0.008279 
},
{
 "date":   3591,
"name": "GSPC.Close",
"price": 102.57,
"rsi": 38.762,
"ret": 0.0073659 
},
{
 "date":   3592,
"name": "GSPC.Close",
"price": 102.51,
"rsi": 43.086,
"ret": -0.00058497 
},
{
 "date":   3595,
"name": "GSPC.Close",
"price": 101.82,
"rsi": 42.825,
"ret": -0.0067311 
},
{
 "date":   3596,
"name": "GSPC.Close",
"price":  101.2,
"rsi": 39.842,
"ret": -0.0060892 
},
{
 "date":   3597,
"name": "GSPC.Close",
"price":  99.87,
"rsi": 37.326,
"ret": -0.013142 
},
{
 "date":   3598,
"name": "GSPC.Close",
"price":  100.3,
"rsi": 32.573,
"ret": 0.0043056 
},
{
 "date":   3599,
"name": "GSPC.Close",
"price": 101.51,
"rsi": 35.435,
"ret": 0.012064 
},
{
 "date":   3602,
"name": "GSPC.Close",
"price": 103.51,
"rsi": 42.794,
"ret": 0.019702 
},
{
 "date":   3603,
"name": "GSPC.Close",
"price": 102.94,
"rsi": 52.443,
"ret": -0.0055067 
},
{
 "date":   3604,
"name": "GSPC.Close",
"price": 103.39,
"rsi": 49.862,
"ret": 0.0043715 
},
{
 "date":   3605,
"name": "GSPC.Close",
"price": 104.13,
"rsi": 51.876,
"ret": 0.0071574 
},
{
 "date":   3606,
"name": "GSPC.Close",
"price": 103.79,
"rsi": 55.071,
"ret": -0.0032651 
},
{
 "date":   3609,
"name": "GSPC.Close",
"price": 104.23,
"rsi": 53.319,
"ret": 0.0042393 
},
{
 "date":   3610,
"name": "GSPC.Close",
"price": 103.69,
"rsi": 55.301,
"ret": -0.0051809 
},
{
 "date":   3611,
"name": "GSPC.Close",
"price": 103.89,
"rsi": 52.363,
"ret": 0.0019288 
},
{
 "date":   3613,
"name": "GSPC.Close",
"price": 104.67,
"rsi": 53.352,
"ret": 0.0075079 
},
{
 "date":   3616,
"name": "GSPC.Close",
"price":  106.8,
"rsi": 57.091,
"ret": 0.02035 
},
{
 "date":   3617,
"name": "GSPC.Close",
"price": 106.38,
"rsi": 65.278,
"ret": -0.0039326 
},
{
 "date":   3618,
"name": "GSPC.Close",
"price": 106.77,
"rsi": 62.736,
"ret": 0.0036661 
},
{
 "date":   3619,
"name": "GSPC.Close",
"price": 106.81,
"rsi": 64.133,
"ret": 0.00037464 
},
{
 "date":   3620,
"name": "GSPC.Close",
"price": 106.16,
"rsi": 64.281,
"ret": -0.0060856 
},
{
 "date":   3623,
"name": "GSPC.Close",
"price": 105.83,
"rsi": 59.955,
"ret": -0.0031085 
},
{
 "date":   3624,
"name": "GSPC.Close",
"price": 106.79,
"rsi": 57.828,
"ret": 0.0090712 
},
{
 "date":   3625,
"name": "GSPC.Close",
"price": 107.25,
"rsi": 62.047,
"ret": 0.0043075 
},
{
 "date":   3626,
"name": "GSPC.Close",
"price":    108,
"rsi":  63.91,
"ret": 0.006993 
},
{
 "date":   3627,
"name": "GSPC.Close",
"price": 107.52,
"rsi": 66.774,
"ret": -0.0044444 
},
{
 "date":   3630,
"name": "GSPC.Close",
"price": 107.67,
"rsi": 63.311,
"ret": 0.0013951 
},
{
 "date":   3631,
"name": "GSPC.Close",
"price": 107.49,
"rsi": 63.941,
"ret": -0.0016718 
},
{
 "date":   3632,
"name": "GSPC.Close",
"price": 107.52,
"rsi": 62.554,
"ret": 0.0002791 
},
{
 "date":   3633,
"name": "GSPC.Close",
"price": 107.67,
"rsi": 62.699,
"ret": 0.0013951 
},
{
 "date":   3634,
"name": "GSPC.Close",
"price": 108.92,
"rsi": 63.462,
"ret": 0.01161 
},
{
 "date":   3637,
"name": "GSPC.Close",
"price": 109.33,
"rsi": 69.128,
"ret": 0.0037642 
},
{
 "date":   3638,
"name": "GSPC.Close",
"price":  108.3,
"rsi": 70.731,
"ret": -0.009421 
},
{
 "date":   3639,
"name": "GSPC.Close",
"price":  108.2,
"rsi": 62.018,
"ret": -0.00092336 
},
{
 "date":   3640,
"name": "GSPC.Close",
"price": 108.26,
"rsi": 61.229,
"ret": 0.00055453 
},
{
 "date":   3641,
"name": "GSPC.Close",
"price": 107.59,
"rsi": 61.545,
"ret": -0.0061888 
},
{
 "date":   3644,
"name": "GSPC.Close",
"price": 107.66,
"rsi": 56.052,
"ret": 0.00065062 
},
{
 "date":   3646,
"name": "GSPC.Close",
"price": 107.78,
"rsi": 56.489,
"ret": 0.0011146 
},
{
 "date":   3647,
"name": "GSPC.Close",
"price": 107.96,
"rsi": 57.273,
"ret": 0.0016701 
},
{
 "date":   3648,
"name": "GSPC.Close",
"price": 107.84,
"rsi": 58.482,
"ret": -0.0011115 
},
{
 "date":   3651,
"name": "GSPC.Close",
"price": 107.94,
"rsi": 57.318,
"ret": 0.0009273 
},
{
 "date":   3653,
"name": "GSPC.Close",
"price": 105.76,
"rsi": 58.067,
"ret": -0.020196 
},
{
 "date":   3654,
"name": "GSPC.Close",
"price": 105.22,
"rsi": 41.121,
"ret": -0.0051059 
},
{
 "date":   3655,
"name": "GSPC.Close",
"price": 106.52,
"rsi": 38.151,
"ret": 0.012355 
},
{
 "date":   3658,
"name": "GSPC.Close",
"price": 106.81,
"rsi": 47.906,
"ret": 0.0027225 
},
{
 "date":   3659,
"name": "GSPC.Close",
"price": 108.95,
"rsi": 49.808,
"ret": 0.020036 
},
{
 "date":   3660,
"name": "GSPC.Close",
"price": 109.05,
"rsi": 61.095,
"ret": 0.00091785 
},
{
 "date":   3661,
"name": "GSPC.Close",
"price": 109.89,
"rsi":  61.53,
"ret": 0.0077029 
},
{
 "date":   3662,
"name": "GSPC.Close",
"price": 109.92,
"rsi": 65.066,
"ret": 0.000273 
},
{
 "date":   3665,
"name": "GSPC.Close",
"price": 110.38,
"rsi":  65.19,
"ret": 0.0041849 
},
{
 "date":   3666,
"name": "GSPC.Close",
"price": 111.14,
"rsi": 67.103,
"ret": 0.0068853 
},
{
 "date":   3667,
"name": "GSPC.Close",
"price": 111.05,
"rsi": 70.034,
"ret": -0.00080979 
},
{
 "date":   3668,
"name": "GSPC.Close",
"price":  110.7,
"rsi": 69.248,
"ret": -0.0031517 
},
{
 "date":   3669,
"name": "GSPC.Close",
"price": 111.07,
"rsi": 66.136,
"ret": 0.0033424 
},
{
 "date":   3672,
"name": "GSPC.Close",
"price":  112.1,
"rsi": 67.784,
"ret": 0.0092734 
},
{
 "date":   3673,
"name": "GSPC.Close",
"price": 111.51,
"rsi": 71.886,
"ret": -0.0052632 
},
{
 "date":   3674,
"name": "GSPC.Close",
"price": 113.44,
"rsi": 66.651,
"ret": 0.017308 
},
{
 "date":   3675,
"name": "GSPC.Close",
"price":  113.7,
"rsi":  73.46,
"ret": 0.002292 
},
{
 "date":   3676,
"name": "GSPC.Close",
"price": 113.61,
"rsi": 74.224,
"ret": -0.00079156 
},
{
 "date":   3679,
"name": "GSPC.Close",
"price": 114.85,
"rsi": 73.436,
"ret": 0.010915 
},
{
 "date":   3680,
"name": "GSPC.Close",
"price": 114.07,
"rsi": 77.049,
"ret": -0.0067915 
},
{
 "date":   3681,
"name": "GSPC.Close",
"price":  115.2,
"rsi": 70.549,
"ret": 0.0099062 
},
{
 "date":   3682,
"name": "GSPC.Close",
"price": 114.16,
"rsi": 73.974,
"ret": -0.0090278 
},
{
 "date":   3683,
"name": "GSPC.Close",
"price": 115.12,
"rsi": 66.327,
"ret": 0.0084093 
},
{
 "date":   3686,
"name": "GSPC.Close",
"price": 114.37,
"rsi": 69.465,
"ret": -0.0065149 
},
{
 "date":   3687,
"name": "GSPC.Close",
"price": 114.66,
"rsi": 64.415,
"ret": 0.0025356 
},
{
 "date":   3688,
"name": "GSPC.Close",
"price": 115.72,
"rsi": 65.461,
"ret": 0.0092447 
},
{
 "date":   3689,
"name": "GSPC.Close",
"price": 116.28,
"rsi": 69.041,
"ret": 0.0048393 
},
{
 "date":   3690,
"name": "GSPC.Close",
"price": 117.95,
"rsi": 70.766,
"ret": 0.014362 
},
{
 "date":   3693,
"name": "GSPC.Close",
"price": 117.12,
"rsi": 75.202,
"ret": -0.0070369 
},
{
 "date":   3694,
"name": "GSPC.Close",
"price":  117.9,
"rsi": 69.553,
"ret": 0.0066598 
},
{
 "date":   3695,
"name": "GSPC.Close",
"price": 118.44,
"rsi": 71.704,
"ret": 0.0045802 
},
{
 "date":   3696,
"name": "GSPC.Close",
"price": 116.72,
"rsi":  73.12,
"ret": -0.014522 
},
{
 "date":   3697,
"name": "GSPC.Close",
"price": 115.41,
"rsi": 62.408,
"ret": -0.011223 
},
{
 "date":   3701,
"name": "GSPC.Close",
"price":  114.6,
"rsi": 55.714,
"ret": -0.0070185 
},
{
 "date":   3702,
"name": "GSPC.Close",
"price": 116.47,
"rsi": 51.999,
"ret": 0.016318 
},
{
 "date":   3703,
"name": "GSPC.Close",
"price": 115.28,
"rsi": 58.824,
"ret": -0.010217 
},
{
 "date":   3704,
"name": "GSPC.Close",
"price": 115.04,
"rsi": 53.601,
"ret": -0.0020819 
},
{
 "date":   3707,
"name": "GSPC.Close",
"price": 113.33,
"rsi": 52.587,
"ret": -0.014864 
},
{
 "date":   3708,
"name": "GSPC.Close",
"price": 113.98,
"rsi": 45.921,
"ret": 0.0057355 
},
{
 "date":   3709,
"name": "GSPC.Close",
"price": 112.38,
"rsi": 48.589,
"ret": -0.014038 
},
{
 "date":   3710,
"name": "GSPC.Close",
"price": 112.35,
"rsi": 42.969,
"ret": -0.00026695 
},
{
 "date":   3711,
"name": "GSPC.Close",
"price": 113.66,
"rsi": 42.869,
"ret": 0.01166 
},
{
 "date":   3714,
"name": "GSPC.Close",
"price":  112.5,
"rsi": 48.511,
"ret": -0.010206 
},
{
 "date":   3715,
"name": "GSPC.Close",
"price": 112.78,
"rsi": 44.336,
"ret": 0.0024889 
},
{
 "date":   3716,
"name": "GSPC.Close",
"price": 111.13,
"rsi": 45.554,
"ret": -0.01463 
},
{
 "date":   3717,
"name": "GSPC.Close",
"price": 108.65,
"rsi": 39.999,
"ret": -0.022316 
},
{
 "date":   3718,
"name": "GSPC.Close",
"price":  106.9,
"rsi": 33.406,
"ret": -0.016107 
},
{
 "date":   3721,
"name": "GSPC.Close",
"price": 106.51,
"rsi": 29.688,
"ret": -0.0036483 
},
{
 "date":   3722,
"name": "GSPC.Close",
"price": 107.78,
"rsi": 28.915,
"ret": 0.011924 
},
{
 "date":   3723,
"name": "GSPC.Close",
"price": 106.87,
"rsi": 34.859,
"ret": -0.0084431 
},
{
 "date":   3724,
"name": "GSPC.Close",
"price": 105.62,
"rsi": 32.746,
"ret": -0.011696 
},
{
 "date":   3725,
"name": "GSPC.Close",
"price": 105.43,
"rsi": 30.052,
"ret": -0.0017989 
},
{
 "date":   3728,
"name": "GSPC.Close",
"price": 102.26,
"rsi": 29.652,
"ret": -0.030067 
},
{
 "date":   3729,
"name": "GSPC.Close",
"price":  104.1,
"rsi": 23.936,
"ret": 0.017993 
},
{
 "date":   3730,
"name": "GSPC.Close",
"price": 104.31,
"rsi": 32.116,
"ret": 0.0020173 
},
{
 "date":   3731,
"name": "GSPC.Close",
"price": 103.12,
"rsi": 33.002,
"ret": -0.011408 
},
{
 "date":   3732,
"name": "GSPC.Close",
"price": 102.31,
"rsi": 30.568,
"ret": -0.0078549 
},
{
 "date":   3735,
"name": "GSPC.Close",
"price":  99.28,
"rsi": 29.001,
"ret": -0.029616 
},
{
 "date":   3736,
"name": "GSPC.Close",
"price":  99.19,
"rsi": 24.035,
"ret": -0.00090653 
},
{
 "date":   3737,
"name": "GSPC.Close",
"price":  98.68,
"rsi": 23.904,
"ret": -0.0051416 
},
{
 "date":   3738,
"name": "GSPC.Close",
"price":  98.22,
"rsi": 23.135,
"ret": -0.0046615 
},
{
 "date":   3739,
"name": "GSPC.Close",
"price": 100.68,
"rsi": 22.434,
"ret": 0.025046 
},
{
 "date":   3742,
"name": "GSPC.Close",
"price": 102.09,
"rsi": 33.959,
"ret": 0.014005 
},
{
 "date":   3743,
"name": "GSPC.Close",
"price": 102.18,
"rsi": 39.508,
"ret": 0.00088158 
},
{
 "date":   3744,
"name": "GSPC.Close",
"price": 102.68,
"rsi": 39.855,
"ret": 0.0048933 
},
{
 "date":   3745,
"name": "GSPC.Close",
"price": 102.15,
"rsi": 41.852,
"ret": -0.0051617 
},
{
 "date":   3749,
"name": "GSPC.Close",
"price": 100.19,
"rsi": 40.324,
"ret": -0.019187 
},
{
 "date":   3750,
"name": "GSPC.Close",
"price":  101.2,
"rsi": 35.203,
"ret": 0.010081 
},
{
 "date":   3751,
"name": "GSPC.Close",
"price": 103.11,
"rsi": 39.469,
"ret": 0.018874 
},
{
 "date":   3752,
"name": "GSPC.Close",
"price": 104.08,
"rsi": 46.625,
"ret": 0.0094074 
},
{
 "date":   3753,
"name": "GSPC.Close",
"price": 103.79,
"rsi": 49.867,
"ret": -0.0027863 
},
{
 "date":   3756,
"name": "GSPC.Close",
"price": 102.84,
"rsi": 48.911,
"ret": -0.0091531 
},
{
 "date":   3757,
"name": "GSPC.Close",
"price": 102.63,
"rsi": 45.811,
"ret": -0.002042 
},
{
 "date":   3758,
"name": "GSPC.Close",
"price": 101.54,
"rsi":  45.13,
"ret": -0.010621 
},
{
 "date":   3759,
"name": "GSPC.Close",
"price": 101.05,
"rsi": 41.668,
"ret": -0.0048257 
},
{
 "date":   3760,
"name": "GSPC.Close",
"price": 100.55,
"rsi": 40.176,
"ret": -0.004948 
},
{
 "date":   3763,
"name": "GSPC.Close",
"price":   99.8,
"rsi": 38.655,
"ret": -0.007459 
},
{
 "date":   3764,
"name": "GSPC.Close",
"price": 103.43,
"rsi": 36.428,
"ret": 0.036373 
},
{
 "date":   3765,
"name": "GSPC.Close",
"price": 103.73,
"rsi": 51.113,
"ret": 0.0029005 
},
{
 "date":   3766,
"name": "GSPC.Close",
"price":  104.4,
"rsi": 52.097,
"ret": 0.0064591 
},
{
 "date":   3767,
"name": "GSPC.Close",
"price": 105.16,
"rsi": 54.311,
"ret": 0.0072797 
},
{
 "date":   3770,
"name": "GSPC.Close",
"price": 105.64,
"rsi": 56.752,
"ret": 0.0045645 
},
{
 "date":   3771,
"name": "GSPC.Close",
"price": 105.86,
"rsi": 58.269,
"ret": 0.0020825 
},
{
 "date":   3772,
"name": "GSPC.Close",
"price": 106.29,
"rsi": 58.979,
"ret": 0.004062 
},
{
 "date":   3773,
"name": "GSPC.Close",
"price": 105.46,
"rsi": 60.398,
"ret": -0.0078088 
},
{
 "date":   3774,
"name": "GSPC.Close",
"price": 105.58,
"rsi": 56.347,
"ret": 0.0011379 
},
{
 "date":   3777,
"name": "GSPC.Close",
"price": 106.38,
"rsi": 56.799,
"ret": 0.0075772 
},
{
 "date":   3778,
"name": "GSPC.Close",
"price": 106.25,
"rsi": 59.782,
"ret": -0.001222 
},
{
 "date":   3779,
"name": "GSPC.Close",
"price": 107.18,
"rsi": 59.068,
"ret": 0.0087529 
},
{
 "date":   3780,
"name": "GSPC.Close",
"price": 106.13,
"rsi": 62.517,
"ret": -0.0097966 
},
{
 "date":   3781,
"name": "GSPC.Close",
"price": 104.72,
"rsi": 56.708,
"ret": -0.013286 
},
{
 "date":   3784,
"name": "GSPC.Close",
"price": 104.78,
"rsi":  49.99,
"ret": 0.00057296 
},
{
 "date":   3785,
"name": "GSPC.Close",
"price":  106.3,
"rsi":  50.26,
"ret": 0.014507 
},
{
 "date":   3786,
"name": "GSPC.Close",
"price": 106.85,
"rsi": 56.646,
"ret": 0.005174 
},
{
 "date":   3787,
"name": "GSPC.Close",
"price": 106.99,
"rsi": 58.712,
"ret": 0.0013102 
},
{
 "date":   3788,
"name": "GSPC.Close",
"price": 107.35,
"rsi": 59.244,
"ret": 0.0033648 
},
{
 "date":   3791,
"name": "GSPC.Close",
"price": 107.67,
"rsi": 60.649,
"ret": 0.0029809 
},
{
 "date":   3792,
"name": "GSPC.Close",
"price": 107.62,
"rsi": 61.906,
"ret": -0.00046438 
},
{
 "date":   3793,
"name": "GSPC.Close",
"price": 107.72,
"rsi": 61.575,
"ret": 0.0009292 
},
{
 "date":   3794,
"name": "GSPC.Close",
"price": 109.01,
"rsi": 62.013,
"ret": 0.011975 
},
{
 "date":   3795,
"name": "GSPC.Close",
"price": 110.62,
"rsi":   67.2,
"ret": 0.014769 
},
{
 "date":   3799,
"name": "GSPC.Close",
"price":  111.4,
"rsi": 72.287,
"ret": 0.0070512 
},
{
 "date":   3800,
"name": "GSPC.Close",
"price": 112.06,
"rsi": 74.361,
"ret": 0.0059246 
},
{
 "date":   3801,
"name": "GSPC.Close",
"price": 110.27,
"rsi": 75.998,
"ret": -0.015974 
},
{
 "date":   3802,
"name": "GSPC.Close",
"price": 111.24,
"rsi": 64.052,
"ret": 0.0087966 
},
{
 "date":   3805,
"name": "GSPC.Close",
"price": 110.76,
"rsi": 67.073,
"ret": -0.004315 
},
{
 "date":   3806,
"name": "GSPC.Close",
"price": 110.51,
"rsi": 64.198,
"ret": -0.0022571 
},
{
 "date":   3807,
"name": "GSPC.Close",
"price": 112.61,
"rsi": 62.691,
"ret": 0.019003 
},
{
 "date":   3808,
"name": "GSPC.Close",
"price": 112.78,
"rsi": 69.226,
"ret": 0.0015096 
},
{
 "date":   3809,
"name": "GSPC.Close",
"price":  113.2,
"rsi": 69.689,
"ret": 0.0037241 
},
{
 "date":   3812,
"name": "GSPC.Close",
"price": 113.71,
"rsi": 70.855,
"ret": 0.0045053 
},
{
 "date":   3813,
"name": "GSPC.Close",
"price": 114.66,
"rsi": 72.252,
"ret": 0.0083546 
},
{
 "date":   3814,
"name": "GSPC.Close",
"price": 116.02,
"rsi": 74.685,
"ret": 0.011861 
},
{
 "date":   3815,
"name": "GSPC.Close",
"price": 115.52,
"rsi": 77.699,
"ret": -0.0043096 
},
{
 "date":   3816,
"name": "GSPC.Close",
"price": 115.81,
"rsi": 74.201,
"ret": 0.0025104 
},
{
 "date":   3819,
"name": "GSPC.Close",
"price": 116.09,
"rsi": 74.906,
"ret": 0.0024178 
},
{
 "date":   3820,
"name": "GSPC.Close",
"price": 116.03,
"rsi":   75.6,
"ret": -0.00051684 
},
{
 "date":   3821,
"name": "GSPC.Close",
"price": 116.26,
"rsi": 75.121,
"ret": 0.0019822 
},
{
 "date":   3822,
"name": "GSPC.Close",
"price": 114.66,
"rsi": 75.756,
"ret": -0.013762 
},
{
 "date":   3823,
"name": "GSPC.Close",
"price": 114.06,
"rsi": 63.601,
"ret": -0.0052329 
},
{
 "date":   3826,
"name": "GSPC.Close",
"price": 114.51,
"rsi":  59.73,
"ret": 0.0039453 
},
{
 "date":   3827,
"name": "GSPC.Close",
"price": 115.14,
"rsi": 61.617,
"ret": 0.0055017 
},
{
 "date":   3828,
"name": "GSPC.Close",
"price": 116.72,
"rsi": 64.149,
"ret": 0.013722 
},
{
 "date":   3829,
"name": "GSPC.Close",
"price": 116.19,
"rsi": 69.571,
"ret": -0.0045408 
},
{
 "date":   3830,
"name": "GSPC.Close",
"price":    116,
"rsi": 65.967,
"ret": -0.0016353 
},
{
 "date":   3833,
"name": "GSPC.Close",
"price": 114.24,
"rsi": 64.674,
"ret": -0.015172 
},
{
 "date":   3834,
"name": "GSPC.Close",
"price": 114.93,
"rsi": 54.093,
"ret": 0.0060399 
},
{
 "date":   3835,
"name": "GSPC.Close",
"price": 115.68,
"rsi": 57.059,
"ret": 0.0065257 
},
{
 "date":   3836,
"name": "GSPC.Close",
"price": 117.46,
"rsi": 60.078,
"ret": 0.015387 
},
{
 "date":   3840,
"name": "GSPC.Close",
"price": 118.29,
"rsi":  66.16,
"ret": 0.0070662 
},
{
 "date":   3841,
"name": "GSPC.Close",
"price": 117.84,
"rsi": 68.564,
"ret": -0.0038042 
},
{
 "date":   3842,
"name": "GSPC.Close",
"price": 117.98,
"rsi": 65.833,
"ret": 0.0011881 
},
{
 "date":   3843,
"name": "GSPC.Close",
"price": 116.95,
"rsi": 66.283,
"ret": -0.0087303 
},
{
 "date":   3844,
"name": "GSPC.Close",
"price": 117.84,
"rsi":  60.02,
"ret": 0.0076101 
},
{
 "date":   3847,
"name": "GSPC.Close",
"price": 120.01,
"rsi": 63.251,
"ret": 0.018415 
},
{
 "date":   3848,
"name": "GSPC.Close",
"price":  119.3,
"rsi": 69.685,
"ret": -0.0059162 
},
{
 "date":   3849,
"name": "GSPC.Close",
"price": 119.63,
"rsi": 65.636,
"ret": 0.0027661 
},
{
 "date":   3850,
"name": "GSPC.Close",
"price": 121.44,
"rsi": 66.607,
"ret": 0.01513 
},
{
 "date":   3851,
"name": "GSPC.Close",
"price": 122.04,
"rsi": 71.384,
"ret": 0.0049407 
},
{
 "date":   3854,
"name": "GSPC.Close",
"price": 122.51,
"rsi": 72.774,
"ret": 0.0038512 
},
{
 "date":   3855,
"name": "GSPC.Close",
"price": 122.19,
"rsi": 73.846,
"ret": -0.002612 
},
{
 "date":   3856,
"name": "GSPC.Close",
"price": 121.93,
"rsi": 71.774,
"ret": -0.0021278 
},
{
 "date":   3857,
"name": "GSPC.Close",
"price": 121.79,
"rsi": 70.054,
"ret": -0.0011482 
},
{
 "date":   3858,
"name": "GSPC.Close",
"price": 120.78,
"rsi": 69.094,
"ret": -0.008293 
},
{
 "date":   3861,
"name": "GSPC.Close",
"price": 121.43,
"rsi": 62.445,
"ret": 0.0053817 
},
{
 "date":   3862,
"name": "GSPC.Close",
"price":  122.4,
"rsi": 64.793,
"ret": 0.0079881 
},
{
 "date":   3863,
"name": "GSPC.Close",
"price": 122.23,
"rsi": 68.008,
"ret": -0.0013889 
},
{
 "date":   3864,
"name": "GSPC.Close",
"price": 121.67,
"rsi": 66.856,
"ret": -0.0045815 
},
{
 "date":   3865,
"name": "GSPC.Close",
"price": 121.21,
"rsi": 63.065,
"ret": -0.0037807 
},
{
 "date":   3868,
"name": "GSPC.Close",
"price": 120.98,
"rsi": 60.053,
"ret": -0.0018975 
},
{
 "date":   3869,
"name": "GSPC.Close",
"price": 120.74,
"rsi": 58.548,
"ret": -0.0019838 
},
{
 "date":   3870,
"name": "GSPC.Close",
"price": 121.55,
"rsi": 56.943,
"ret": 0.0067086 
},
{
 "date":   3871,
"name": "GSPC.Close",
"price":  123.3,
"rsi": 60.843,
"ret": 0.014397 
},
{
 "date":   3872,
"name": "GSPC.Close",
"price": 123.61,
"rsi": 67.659,
"ret": 0.0025142 
},
{
 "date":   3875,
"name": "GSPC.Close",
"price": 124.78,
"rsi": 68.698,
"ret": 0.0094653 
},
{
 "date":   3876,
"name": "GSPC.Close",
"price": 123.79,
"rsi": 72.314,
"ret": -0.007934 
},
{
 "date":   3877,
"name": "GSPC.Close",
"price": 123.28,
"rsi": 65.426,
"ret": -0.0041199 
},
{
 "date":   3878,
"name": "GSPC.Close",
"price": 125.25,
"rsi": 62.143,
"ret": 0.01598 
},
{
 "date":   3879,
"name": "GSPC.Close",
"price": 125.72,
"rsi": 68.682,
"ret": 0.0037525 
},
{
 "date":   3882,
"name": "GSPC.Close",
"price": 123.39,
"rsi": 70.012,
"ret": -0.018533 
},
{
 "date":   3883,
"name": "GSPC.Close",
"price":  122.6,
"rsi": 57.066,
"ret": -0.0064025 
},
{
 "date":   3884,
"name": "GSPC.Close",
"price": 123.77,
"rsi": 53.457,
"ret": 0.0095432 
},
{
 "date":   3885,
"name": "GSPC.Close",
"price": 125.46,
"rsi": 57.722,
"ret": 0.013654 
},
{
 "date":   3886,
"name": "GSPC.Close",
"price": 126.02,
"rsi": 62.996,
"ret": 0.0044636 
},
{
 "date":   3889,
"name": "GSPC.Close",
"price": 125.16,
"rsi": 64.574,
"ret": -0.0068243 
},
{
 "date":   3890,
"name": "GSPC.Close",
"price": 124.84,
"rsi": 60.321,
"ret": -0.0025567 
},
{
 "date":   3891,
"name": "GSPC.Close",
"price": 123.52,
"rsi": 58.771,
"ret": -0.010574 
},
{
 "date":   3892,
"name": "GSPC.Close",
"price": 122.08,
"rsi": 52.747,
"ret": -0.011658 
},
{
 "date":   3893,
"name": "GSPC.Close",
"price": 122.38,
"rsi": 47.078,
"ret": 0.0024574 
},
{
 "date":   3897,
"name": "GSPC.Close",
"price": 123.74,
"rsi": 48.324,
"ret": 0.011113 
},
{
 "date":   3898,
"name": "GSPC.Close",
"price": 126.12,
"rsi": 53.652,
"ret": 0.019234 
},
{
 "date":   3899,
"name": "GSPC.Close",
"price": 125.42,
"rsi": 61.192,
"ret": -0.0055503 
},
{
 "date":   3900,
"name": "GSPC.Close",
"price": 124.88,
"rsi": 58.193,
"ret": -0.0043055 
},
{
 "date":   3903,
"name": "GSPC.Close",
"price": 123.31,
"rsi": 55.917,
"ret": -0.012572 
},
{
 "date":   3904,
"name": "GSPC.Close",
"price": 124.07,
"rsi": 49.815,
"ret": 0.0061633 
},
{
 "date":   3905,
"name": "GSPC.Close",
"price": 124.81,
"rsi": 52.516,
"ret": 0.0059644 
},
{
 "date":   3906,
"name": "GSPC.Close",
"price": 125.66,
"rsi": 55.053,
"ret": 0.0068104 
},
{
 "date":   3907,
"name": "GSPC.Close",
"price": 125.54,
"rsi": 57.839,
"ret": -0.00095496 
},
{
 "date":   3910,
"name": "GSPC.Close",
"price": 125.67,
"rsi": 57.299,
"ret": 0.0010355 
},
{
 "date":   3911,
"name": "GSPC.Close",
"price": 126.74,
"rsi": 57.759,
"ret": 0.0085144 
},
{
 "date":   3912,
"name": "GSPC.Close",
"price": 128.87,
"rsi": 61.442,
"ret": 0.016806 
},
{
 "date":   3913,
"name": "GSPC.Close",
"price":  128.4,
"rsi": 67.514,
"ret": -0.0036471 
},
{
 "date":   3914,
"name": "GSPC.Close",
"price": 129.25,
"rsi": 65.079,
"ret": 0.0066199 
},
{
 "date":   3917,
"name": "GSPC.Close",
"price":  130.4,
"rsi": 67.371,
"ret": 0.0088975 
},
{
 "date":   3918,
"name": "GSPC.Close",
"price": 129.43,
"rsi": 70.219,
"ret": -0.0074387 
},
{
 "date":   3919,
"name": "GSPC.Close",
"price": 130.37,
"rsi":  65.06,
"ret": 0.0072626 
},
{
 "date":   3920,
"name": "GSPC.Close",
"price": 128.72,
"rsi": 67.548,
"ret": -0.012656 
},
{
 "date":   3921,
"name": "GSPC.Close",
"price": 126.35,
"rsi": 59.534,
"ret": -0.018412 
},
{
 "date":   3924,
"name": "GSPC.Close",
"price": 123.54,
"rsi": 50.303,
"ret": -0.02224 
},
{
 "date":   3925,
"name": "GSPC.Close",
"price": 125.46,
"rsi": 41.989,
"ret": 0.015542 
},
{
 "date":   3926,
"name": "GSPC.Close",
"price": 127.13,
"rsi": 48.279,
"ret": 0.013311 
},
{
 "date":   3927,
"name": "GSPC.Close",
"price": 128.09,
"rsi": 53.048,
"ret": 0.0075513 
},
{
 "date":   3928,
"name": "GSPC.Close",
"price": 129.33,
"rsi": 55.583,
"ret": 0.0096807 
},
{
 "date":   3931,
"name": "GSPC.Close",
"price": 131.73,
"rsi": 58.686,
"ret": 0.018557 
},
{
 "date":   3932,
"name": "GSPC.Close",
"price":    131,
"rsi": 63.937,
"ret": -0.0055416 
},
{
 "date":   3933,
"name": "GSPC.Close",
"price": 131.65,
"rsi": 61.382,
"ret": 0.0049618 
},
{
 "date":   3934,
"name": "GSPC.Close",
"price": 131.04,
"rsi": 62.807,
"ret": -0.0046335 
},
{
 "date":   3935,
"name": "GSPC.Close",
"price": 130.29,
"rsi": 60.548,
"ret": -0.0057234 
},
{
 "date":   3938,
"name": "GSPC.Close",
"price": 132.03,
"rsi": 57.796,
"ret": 0.013355 
},
{
 "date":   3939,
"name": "GSPC.Close",
"price": 132.02,
"rsi":   62.1,
"ret": -7.574e-05 
},
{
 "date":   3940,
"name": "GSPC.Close",
"price":  133.7,
"rsi": 62.061,
"ret": 0.012725 
},
{
 "date":   3941,
"name": "GSPC.Close",
"price": 132.22,
"rsi": 65.948,
"ret": -0.01107 
},
{
 "date":   3942,
"name": "GSPC.Close",
"price": 131.52,
"rsi": 60.106,
"ret": -0.0052942 
},
{
 "date":   3945,
"name": "GSPC.Close",
"price": 132.61,
"rsi": 57.511,
"ret": 0.0082877 
},
{
 "date":   3946,
"name": "GSPC.Close",
"price": 131.84,
"rsi":  60.38,
"ret": -0.0058065 
},
{
 "date":   3947,
"name": "GSPC.Close",
"price": 131.92,
"rsi":  57.43,
"ret": 0.0006068 
},
{
 "date":   3948,
"name": "GSPC.Close",
"price": 129.53,
"rsi": 57.662,
"ret": -0.018117 
},
{
 "date":   3949,
"name": "GSPC.Close",
"price": 129.85,
"rsi": 49.078,
"ret": 0.0024705 
},
{
 "date":   3952,
"name": "GSPC.Close",
"price": 127.88,
"rsi": 50.148,
"ret": -0.015171 
},
{
 "date":   3953,
"name": "GSPC.Close",
"price": 128.05,
"rsi": 44.017,
"ret": 0.0013294 
},
{
 "date":   3954,
"name": "GSPC.Close",
"price": 127.91,
"rsi": 44.646,
"ret": -0.0010933 
},
{
 "date":   3955,
"name": "GSPC.Close",
"price": 126.29,
"rsi": 44.205,
"ret": -0.012665 
},
{
 "date":   3956,
"name": "GSPC.Close",
"price": 127.47,
"rsi": 39.365,
"ret": 0.0093436 
},
{
 "date":   3959,
"name": "GSPC.Close",
"price": 129.04,
"rsi": 44.161,
"ret": 0.012317 
},
{
 "date":   3961,
"name": "GSPC.Close",
"price": 131.33,
"rsi": 49.845,
"ret": 0.017746 
},
{
 "date":   3962,
"name": "GSPC.Close",
"price": 128.91,
"rsi": 56.759,
"ret": -0.018427 
},
{
 "date":   3963,
"name": "GSPC.Close",
"price": 129.18,
"rsi": 49.062,
"ret": 0.0020945 
},
{
 "date":   3966,
"name": "GSPC.Close",
"price": 129.48,
"rsi": 49.879,
"ret": 0.0023223 
},
{
 "date":   3967,
"name": "GSPC.Close",
"price": 131.26,
"rsi": 50.822,
"ret": 0.013747 
},
{
 "date":   3968,
"name": "GSPC.Close",
"price": 134.59,
"rsi": 56.102,
"ret": 0.025369 
},
{
 "date":   3969,
"name": "GSPC.Close",
"price": 136.49,
"rsi": 63.908,
"ret": 0.014117 
},
{
 "date":   3970,
"name": "GSPC.Close",
"price": 137.15,
"rsi": 67.464,
"ret": 0.0048355 
},
{
 "date":   3973,
"name": "GSPC.Close",
"price": 137.75,
"rsi":  68.62,
"ret": 0.0043748 
},
{
 "date":   3974,
"name": "GSPC.Close",
"price":  139.7,
"rsi": 69.675,
"ret": 0.014156 
},
{
 "date":   3975,
"name": "GSPC.Close",
"price": 139.06,
"rsi": 72.868,
"ret": -0.0045812 
},
{
 "date":   3976,
"name": "GSPC.Close",
"price":  140.4,
"rsi": 70.254,
"ret": 0.0096361 
},
{
 "date":   3977,
"name": "GSPC.Close",
"price": 139.11,
"rsi":  72.48,
"ret": -0.009188 
},
{
 "date":   3980,
"name": "GSPC.Close",
"price": 138.31,
"rsi": 67.261,
"ret": -0.0057508 
},
{
 "date":   3981,
"name": "GSPC.Close",
"price": 139.33,
"rsi": 64.174,
"ret": 0.0073747 
},
{
 "date":   3982,
"name": "GSPC.Close",
"price": 140.17,
"rsi": 66.298,
"ret": 0.0060289 
},
{
 "date":   3984,
"name": "GSPC.Close",
"price": 140.52,
"rsi": 67.981,
"ret": 0.002497 
},
{
 "date":   3987,
"name": "GSPC.Close",
"price": 137.21,
"rsi": 68.683,
"ret": -0.023555 
},
{
 "date":   3988,
"name": "GSPC.Close",
"price": 136.97,
"rsi": 56.149,
"ret": -0.0017491 
},
{
 "date":   3989,
"name": "GSPC.Close",
"price": 136.71,
"rsi":  55.36,
"ret": -0.0018982 
},
{
 "date":   3990,
"name": "GSPC.Close",
"price": 136.48,
"rsi": 54.467,
"ret": -0.0016824 
},
{
 "date":   3991,
"name": "GSPC.Close",
"price": 134.03,
"rsi": 53.643,
"ret": -0.017951 
},
{
 "date":   3994,
"name": "GSPC.Close",
"price": 130.61,
"rsi": 45.709,
"ret": -0.025517 
},
{
 "date":   3995,
"name": "GSPC.Close",
"price": 130.48,
"rsi": 37.394,
"ret": -0.00099533 
},
{
 "date":   3996,
"name": "GSPC.Close",
"price": 128.26,
"rsi": 37.118,
"ret": -0.017014 
},
{
 "date":   3997,
"name": "GSPC.Close",
"price": 127.36,
"rsi": 32.676,
"ret": -0.007017 
},
{
 "date":   3998,
"name": "GSPC.Close",
"price": 129.23,
"rsi": 31.054,
"ret": 0.014683 
},
{
 "date":   4001,
"name": "GSPC.Close",
"price": 129.45,
"rsi": 37.948,
"ret": 0.0017024 
},
{
 "date":   4002,
"name": "GSPC.Close",
"price":  130.6,
"rsi": 38.724,
"ret": 0.0088837 
},
{
 "date":   4003,
"name": "GSPC.Close",
"price": 132.89,
"rsi": 42.755,
"ret": 0.017534 
},
{
 "date":   4004,
"name": "GSPC.Close",
"price":    133,
"rsi": 49.833,
"ret": 0.00082775 
},
{
 "date":   4005,
"name": "GSPC.Close",
"price":  133.7,
"rsi": 50.152,
"ret": 0.0052632 
},
{
 "date":   4008,
"name": "GSPC.Close",
"price": 135.78,
"rsi": 52.232,
"ret": 0.015557 
},
{
 "date":   4009,
"name": "GSPC.Close",
"price":  135.3,
"rsi":  57.86,
"ret": -0.0035351 
},
{
 "date":   4010,
"name": "GSPC.Close",
"price": 135.88,
"rsi": 56.214,
"ret": 0.0042868 
},
{
 "date":   4012,
"name": "GSPC.Close",
"price": 136.57,
"rsi": 57.777,
"ret": 0.005078 
},
{
 "date":   4015,
"name": "GSPC.Close",
"price": 135.03,
"rsi": 59.624,
"ret": -0.011276 
},
{
 "date":   4016,
"name": "GSPC.Close",
"price": 135.33,
"rsi": 53.952,
"ret": 0.0022217 
},
{
 "date":   4017,
"name": "GSPC.Close",
"price": 135.76,
"rsi": 54.853,
"ret": 0.0031774 
},
{
 "date":   4019,
"name": "GSPC.Close",
"price": 136.34,
"rsi": 56.177,
"ret": 0.0042722 
},
{
 "date":   4022,
"name": "GSPC.Close",
"price": 137.97,
"rsi": 57.967,
"ret": 0.011955 
},
{
 "date":   4023,
"name": "GSPC.Close",
"price": 138.12,
"rsi": 62.591,
"ret": 0.0010872 
},
{
 "date":   4024,
"name": "GSPC.Close",
"price": 135.08,
"rsi": 62.994,
"ret": -0.02201 
},
{
 "date":   4025,
"name": "GSPC.Close",
"price": 133.06,
"rsi": 50.991,
"ret": -0.014954 
},
{
 "date":   4026,
"name": "GSPC.Close",
"price": 133.48,
"rsi": 44.873,
"ret": 0.0031565 
},
{
 "date":   4029,
"name": "GSPC.Close",
"price": 133.52,
"rsi": 46.315,
"ret": 0.00029967 
},
{
 "date":   4030,
"name": "GSPC.Close",
"price": 133.29,
"rsi": 46.459,
"ret": -0.0017226 
},
{
 "date":   4031,
"name": "GSPC.Close",
"price": 133.47,
"rsi": 45.702,
"ret": 0.0013504 
},
{
 "date":   4032,
"name": "GSPC.Close",
"price": 134.22,
"rsi": 46.438,
"ret": 0.0056192 
},
{
 "date":   4033,
"name": "GSPC.Close",
"price": 134.77,
"rsi": 49.508,
"ret": 0.0040977 
},
{
 "date":   4036,
"name": "GSPC.Close",
"price": 134.37,
"rsi": 51.695,
"ret": -0.002968 
},
{
 "date":   4037,
"name": "GSPC.Close",
"price": 131.65,
"rsi": 49.999,
"ret": -0.020243 
},
{
 "date":   4038,
"name": "GSPC.Close",
"price": 131.36,
"rsi": 40.313,
"ret": -0.0022028 
},
{
 "date":   4039,
"name": "GSPC.Close",
"price": 130.26,
"rsi": 39.436,
"ret": -0.0083739 
},
{
 "date":   4040,
"name": "GSPC.Close",
"price": 130.23,
"rsi": 36.216,
"ret": -0.00023031 
},
{
 "date":   4043,
"name": "GSPC.Close",
"price": 129.84,
"rsi":  36.13,
"ret": -0.0029947 
},
{
 "date":   4044,
"name": "GSPC.Close",
"price": 131.12,
"rsi": 34.959,
"ret": 0.0098583 
},
{
 "date":   4045,
"name": "GSPC.Close",
"price": 130.34,
"rsi": 41.642,
"ret": -0.0059487 
},
{
 "date":   4046,
"name": "GSPC.Close",
"price": 130.24,
"rsi": 39.012,
"ret": -0.00076722 
},
{
 "date":   4047,
"name": "GSPC.Close",
"price": 129.55,
"rsi": 38.674,
"ret": -0.0052979 
},
{
 "date":   4050,
"name": "GSPC.Close",
"price": 126.91,
"rsi": 36.339,
"ret": -0.020378 
},
{
 "date":   4051,
"name": "GSPC.Close",
"price": 128.46,
"rsi": 29.101,
"ret": 0.012213 
},
{
 "date":   4052,
"name": "GSPC.Close",
"price": 128.59,
"rsi": 37.032,
"ret": 0.001012 
},
{
 "date":   4053,
"name": "GSPC.Close",
"price": 129.63,
"rsi": 37.661,
"ret": 0.0080877 
},
{
 "date":   4054,
"name": "GSPC.Close",
"price":  130.6,
"rsi": 42.607,
"ret": 0.0074828 
},
{
 "date":   4057,
"name": "GSPC.Close",
"price": 129.27,
"rsi": 46.844,
"ret": -0.010184 
},
{
 "date":   4058,
"name": "GSPC.Close",
"price": 129.24,
"rsi":  42.24,
"ret": -0.00023207 
},
{
 "date":   4059,
"name": "GSPC.Close",
"price": 128.24,
"rsi": 42.139,
"ret": -0.0077375 
},
{
 "date":   4060,
"name": "GSPC.Close",
"price": 127.48,
"rsi":  38.82,
"ret": -0.0059264 
},
{
 "date":   4061,
"name": "GSPC.Close",
"price": 126.98,
"rsi": 36.469,
"ret": -0.0039222 
},
{
 "date":   4065,
"name": "GSPC.Close",
"price": 127.81,
"rsi": 34.969,
"ret": 0.0065365 
},
{
 "date":   4066,
"name": "GSPC.Close",
"price": 128.48,
"rsi": 39.424,
"ret": 0.0052422 
},
{
 "date":   4067,
"name": "GSPC.Close",
"price": 126.61,
"rsi": 42.829,
"ret": -0.014555 
},
{
 "date":   4068,
"name": "GSPC.Close",
"price": 126.58,
"rsi": 36.639,
"ret": -0.00023695 
},
{
 "date":   4071,
"name": "GSPC.Close",
"price": 127.35,
"rsi": 36.548,
"ret": 0.0060831 
},
{
 "date":   4072,
"name": "GSPC.Close",
"price": 127.39,
"rsi": 40.635,
"ret": 0.0003141 
},
{
 "date":   4073,
"name": "GSPC.Close",
"price": 128.52,
"rsi": 40.848,
"ret": 0.0088704 
},
{
 "date":   4074,
"name": "GSPC.Close",
"price":  130.1,
"rsi": 46.673,
"ret": 0.012294 
},
{
 "date":   4075,
"name": "GSPC.Close",
"price": 131.27,
"rsi":  53.56,
"ret": 0.0089931 
},
{
 "date":   4078,
"name": "GSPC.Close",
"price": 132.01,
"rsi": 57.896,
"ret": 0.0056372 
},
{
 "date":   4079,
"name": "GSPC.Close",
"price": 130.56,
"rsi": 60.414,
"ret": -0.010984 
},
{
 "date":   4080,
"name": "GSPC.Close",
"price": 130.86,
"rsi": 53.645,
"ret": 0.0022978 
},
{
 "date":   4081,
"name": "GSPC.Close",
"price": 129.93,
"rsi": 54.774,
"ret": -0.0071068 
},
{
 "date":   4082,
"name": "GSPC.Close",
"price": 129.85,
"rsi": 50.655,
"ret": -0.00061572 
},
{
 "date":   4085,
"name": "GSPC.Close",
"price": 131.12,
"rsi": 50.305,
"ret": 0.0097805 
},
{
 "date":   4086,
"name": "GSPC.Close",
"price": 130.46,
"rsi":  55.56,
"ret": -0.0050336 
},
{
 "date":   4087,
"name": "GSPC.Close",
"price": 129.95,
"rsi": 52.456,
"ret": -0.0039092 
},
{
 "date":   4088,
"name": "GSPC.Close",
"price": 133.19,
"rsi": 50.125,
"ret": 0.024933 
},
{
 "date":   4089,
"name": "GSPC.Close",
"price": 133.11,
"rsi": 61.753,
"ret": -0.00060065 
},
{
 "date":   4092,
"name": "GSPC.Close",
"price": 134.68,
"rsi": 61.372,
"ret": 0.011795 
},
{
 "date":   4093,
"name": "GSPC.Close",
"price": 133.92,
"rsi": 65.823,
"ret": -0.005643 
},
{
 "date":   4094,
"name": "GSPC.Close",
"price": 134.22,
"rsi": 62.093,
"ret": 0.0022401 
},
{
 "date":   4095,
"name": "GSPC.Close",
"price": 133.46,
"rsi": 62.985,
"ret": -0.0056623 
},
{
 "date":   4096,
"name": "GSPC.Close",
"price": 134.08,
"rsi": 59.187,
"ret": 0.0046456 
},
{
 "date":   4099,
"name": "GSPC.Close",
"price": 135.69,
"rsi":  61.24,
"ret": 0.012008 
},
{
 "date":   4100,
"name": "GSPC.Close",
"price": 134.67,
"rsi": 66.021,
"ret": -0.0075171 
},
{
 "date":   4101,
"name": "GSPC.Close",
"price": 137.11,
"rsi": 60.896,
"ret": 0.018118 
},
{
 "date":   4102,
"name": "GSPC.Close",
"price": 136.27,
"rsi": 67.412,
"ret": -0.0061265 
},
{
 "date":   4103,
"name": "GSPC.Close",
"price": 134.65,
"rsi":  63.49,
"ret": -0.011888 
},
{
 "date":   4106,
"name": "GSPC.Close",
"price": 134.28,
"rsi": 56.645,
"ret": -0.0027479 
},
{
 "date":   4107,
"name": "GSPC.Close",
"price":    136,
"rsi": 55.181,
"ret": 0.012809 
},
{
 "date":   4108,
"name": "GSPC.Close",
"price": 136.57,
"rsi": 60.314,
"ret": 0.0041912 
},
{
 "date":   4109,
"name": "GSPC.Close",
"price": 136.32,
"rsi": 61.872,
"ret": -0.0018306 
},
{
 "date":   4110,
"name": "GSPC.Close",
"price": 135.49,
"rsi": 60.746,
"ret": -0.0060886 
},
{
 "date":   4113,
"name": "GSPC.Close",
"price": 133.93,
"rsi": 57.033,
"ret": -0.011514 
},
{
 "date":   4114,
"name": "GSPC.Close",
"price": 133.91,
"rsi": 50.753,
"ret": -0.00014933 
},
{
 "date":   4115,
"name": "GSPC.Close",
"price": 134.31,
"rsi": 50.676,
"ret": 0.0029871 
},
{
 "date":   4116,
"name": "GSPC.Close",
"price": 134.67,
"rsi": 52.238,
"ret": 0.0026804 
},
{
 "date":   4117,
"name": "GSPC.Close",
"price": 134.51,
"rsi":  53.66,
"ret": -0.0011881 
},
{
 "date":   4120,
"name": "GSPC.Close",
"price": 133.15,
"rsi": 52.906,
"ret": -0.010111 
},
{
 "date":   4121,
"name": "GSPC.Close",
"price": 132.68,
"rsi": 46.878,
"ret": -0.0035299 
},
{
 "date":   4122,
"name": "GSPC.Close",
"price": 134.17,
"rsi": 44.971,
"ret": 0.01123 
},
{
 "date":   4123,
"name": "GSPC.Close",
"price":  134.7,
"rsi": 51.681,
"ret": 0.0039502 
},
{
 "date":   4127,
"name": "GSPC.Close",
"price": 135.45,
"rsi": 53.838,
"ret": 0.0055679 
},
{
 "date":   4128,
"name": "GSPC.Close",
"price": 134.23,
"rsi": 56.778,
"ret": -0.009007 
},
{
 "date":   4129,
"name": "GSPC.Close",
"price": 134.14,
"rsi": 51.079,
"ret": -0.00067049 
},
{
 "date":   4130,
"name": "GSPC.Close",
"price": 133.94,
"rsi": 50.675,
"ret": -0.001491 
},
{
 "date":   4131,
"name": "GSPC.Close",
"price": 135.14,
"rsi": 49.734,
"ret": 0.0089592 
},
{
 "date":   4134,
"name": "GSPC.Close",
"price": 135.48,
"rsi": 55.121,
"ret": 0.0025159 
},
{
 "date":   4135,
"name": "GSPC.Close",
"price": 134.33,
"rsi": 56.543,
"ret": -0.0084883 
},
{
 "date":   4136,
"name": "GSPC.Close",
"price": 133.05,
"rsi": 50.695,
"ret": -0.0095288 
},
{
 "date":   4137,
"name": "GSPC.Close",
"price": 132.81,
"rsi": 45.103,
"ret": -0.0018038 
},
{
 "date":   4138,
"name": "GSPC.Close",
"price": 132.72,
"rsi": 44.121,
"ret": -0.00067766 
},
{
 "date":   4141,
"name": "GSPC.Close",
"price": 130.67,
"rsi": 43.736,
"ret": -0.015446 
},
{
 "date":   4142,
"name": "GSPC.Close",
"price": 130.32,
"rsi": 36.028,
"ret": -0.0026785 
},
{
 "date":   4143,
"name": "GSPC.Close",
"price": 130.78,
"rsi": 34.897,
"ret": 0.0035298 
},
{
 "date":   4144,
"name": "GSPC.Close",
"price": 131.67,
"rsi": 37.666,
"ret": 0.0068053 
},
{
 "date":   4145,
"name": "GSPC.Close",
"price": 131.66,
"rsi": 42.741,
"ret": -7.5947e-05 
},
{
 "date":   4148,
"name": "GSPC.Close",
"price": 129.71,
"rsi": 42.699,
"ret": -0.014811 
},
{
 "date":   4149,
"name": "GSPC.Close",
"price": 130.72,
"rsi": 35.386,
"ret": 0.0077866 
},
{
 "date":   4150,
"name": "GSPC.Close",
"price": 130.55,
"rsi":  41.02,
"ret": -0.0013005 
},
{
 "date":   4151,
"name": "GSPC.Close",
"price": 131.28,
"rsi": 40.382,
"ret": 0.0055917 
},
{
 "date":   4152,
"name": "GSPC.Close",
"price": 132.17,
"rsi": 44.384,
"ret": 0.0067794 
},
{
 "date":   4155,
"name": "GSPC.Close",
"price": 132.54,
"rsi": 48.889,
"ret": 0.0027994 
},
{
 "date":   4156,
"name": "GSPC.Close",
"price": 132.09,
"rsi": 50.678,
"ret": -0.0033952 
},
{
 "date":   4157,
"name": "GSPC.Close",
"price":    132,
"rsi": 48.457,
"ret": -0.00068135 
},
{
 "date":   4158,
"name": "GSPC.Close",
"price": 131.75,
"rsi": 48.003,
"ret": -0.0018939 
},
{
 "date":   4159,
"name": "GSPC.Close",
"price": 131.33,
"rsi": 46.697,
"ret": -0.0031879 
},
{
 "date":   4163,
"name": "GSPC.Close",
"price": 132.77,
"rsi": 44.506,
"ret": 0.010965 
},
{
 "date":   4164,
"name": "GSPC.Close",
"price": 133.77,
"rsi": 52.701,
"ret": 0.0075318 
},
{
 "date":   4165,
"name": "GSPC.Close",
"price": 133.45,
"rsi": 57.405,
"ret": -0.0023922 
},
{
 "date":   4166,
"name": "GSPC.Close",
"price": 132.59,
"rsi": 55.503,
"ret": -0.0064444 
},
{
 "date":   4169,
"name": "GSPC.Close",
"price": 132.41,
"rsi": 50.645,
"ret": -0.0013576 
},
{
 "date":   4170,
"name": "GSPC.Close",
"price": 130.62,
"rsi": 49.666,
"ret": -0.013519 
},
{
 "date":   4171,
"name": "GSPC.Close",
"price": 130.71,
"rsi": 41.142,
"ret": 0.00068902 
},
{
 "date":   4172,
"name": "GSPC.Close",
"price": 130.96,
"rsi": 41.684,
"ret": 0.0019126 
},
{
 "date":   4173,
"name": "GSPC.Close",
"price": 132.22,
"rsi": 43.247,
"ret": 0.0096213 
},
{
 "date":   4176,
"name": "GSPC.Close",
"price": 132.24,
"rsi": 50.455,
"ret": 0.00015126 
},
{
 "date":   4177,
"name": "GSPC.Close",
"price": 131.97,
"rsi": 50.562,
"ret": -0.0020417 
},
{
 "date":   4178,
"name": "GSPC.Close",
"price": 132.32,
"rsi": 49.019,
"ret": 0.0026521 
},
{
 "date":   4179,
"name": "GSPC.Close",
"price": 133.75,
"rsi": 51.103,
"ret": 0.010807 
},
{
 "date":   4180,
"name": "GSPC.Close",
"price": 133.49,
"rsi": 58.558,
"ret": -0.0019439 
},
{
 "date":   4183,
"name": "GSPC.Close",
"price": 133.61,
"rsi":  56.86,
"ret": 0.00089894 
},
{
 "date":   4184,
"name": "GSPC.Close",
"price": 132.15,
"rsi": 57.473,
"ret": -0.010927 
},
{
 "date":   4185,
"name": "GSPC.Close",
"price": 133.32,
"rsi": 48.456,
"ret": 0.0088536 
},
{
 "date":   4186,
"name": "GSPC.Close",
"price": 131.64,
"rsi": 54.603,
"ret": -0.012601 
},
{
 "date":   4187,
"name": "GSPC.Close",
"price": 132.27,
"rsi": 46.101,
"ret": 0.0047858 
},
{
 "date":   4190,
"name": "GSPC.Close",
"price": 131.95,
"rsi":  49.29,
"ret": -0.0024193 
},
{
 "date":   4191,
"name": "GSPC.Close",
"price": 133.35,
"rsi": 47.745,
"ret": 0.01061 
},
{
 "date":   4192,
"name": "GSPC.Close",
"price": 132.66,
"rsi": 54.469,
"ret": -0.0051744 
},
{
 "date":   4193,
"name": "GSPC.Close",
"price": 132.81,
"rsi": 50.987,
"ret": 0.0011307 
},
{
 "date":   4194,
"name": "GSPC.Close",
"price": 132.56,
"rsi": 51.709,
"ret": -0.0018824 
},
{
 "date":   4197,
"name": "GSPC.Close",
"price": 131.89,
"rsi": 50.376,
"ret": -0.0050543 
},
{
 "date":   4198,
"name": "GSPC.Close",
"price": 131.21,
"rsi": 46.886,
"ret": -0.0051558 
},
{
 "date":   4199,
"name": "GSPC.Close",
"price": 129.77,
"rsi": 43.586,
"ret": -0.010975 
},
{
 "date":   4200,
"name": "GSPC.Close",
"price": 128.64,
"rsi": 37.558,
"ret": -0.0087077 
},
{
 "date":   4204,
"name": "GSPC.Close",
"price": 127.37,
"rsi": 33.628,
"ret": -0.0098725 
},
{
 "date":   4205,
"name": "GSPC.Close",
"price": 128.24,
"rsi": 29.847,
"ret": 0.0068305 
},
{
 "date":   4206,
"name": "GSPC.Close",
"price": 128.32,
"rsi":  35.22,
"ret": 0.00062383 
},
{
 "date":   4207,
"name": "GSPC.Close",
"price":  129.3,
"rsi": 35.707,
"ret": 0.0076372 
},
{
 "date":   4208,
"name": "GSPC.Close",
"price": 129.37,
"rsi": 41.515,
"ret": 0.00054138 
},
{
 "date":   4211,
"name": "GSPC.Close",
"price": 129.64,
"rsi": 41.919,
"ret": 0.002087 
},
{
 "date":   4212,
"name": "GSPC.Close",
"price": 129.65,
"rsi": 43.537,
"ret": 7.7137e-05 
},
{
 "date":   4213,
"name": "GSPC.Close",
"price": 130.23,
"rsi":   43.6,
"ret": 0.0044736 
},
{
 "date":   4214,
"name": "GSPC.Close",
"price": 130.34,
"rsi": 47.257,
"ret": 0.00084466 
},
{
 "date":   4215,
"name": "GSPC.Close",
"price": 130.76,
"rsi": 47.947,
"ret": 0.0032223 
},
{
 "date":   4218,
"name": "GSPC.Close",
"price": 128.72,
"rsi": 50.602,
"ret": -0.015601 
},
{
 "date":   4219,
"name": "GSPC.Close",
"price": 128.34,
"rsi": 39.944,
"ret": -0.0029521 
},
{
 "date":   4220,
"name": "GSPC.Close",
"price": 127.13,
"rsi": 38.325,
"ret": -0.0094281 
},
{
 "date":   4221,
"name": "GSPC.Close",
"price":  127.4,
"rsi": 33.648,
"ret": 0.0021238 
},
{
 "date":   4222,
"name": "GSPC.Close",
"price": 128.46,
"rsi": 35.538,
"ret": 0.0083203 
},
{
 "date":   4225,
"name": "GSPC.Close",
"price":  129.9,
"rsi": 42.469,
"ret": 0.01121 
},
{
 "date":   4226,
"name": "GSPC.Close",
"price": 129.14,
"rsi": 50.288,
"ret": -0.0058507 
},
{
 "date":   4227,
"name": "GSPC.Close",
"price": 129.16,
"rsi": 46.682,
"ret": 0.00015487 
},
{
 "date":   4228,
"name": "GSPC.Close",
"price": 130.01,
"rsi":  46.79,
"ret": 0.006581 
},
{
 "date":   4229,
"name": "GSPC.Close",
"price": 130.92,
"rsi": 51.309,
"ret": 0.0069995 
},
{
 "date":   4232,
"name": "GSPC.Close",
"price": 130.48,
"rsi": 55.652,
"ret": -0.0033608 
},
{
 "date":   4233,
"name": "GSPC.Close",
"price": 131.18,
"rsi": 53.182,
"ret": 0.0053648 
},
{
 "date":   4234,
"name": "GSPC.Close",
"price": 132.67,
"rsi": 56.491,
"ret": 0.011358 
},
{
 "date":   4235,
"name": "GSPC.Close",
"price": 132.64,
"rsi": 62.557,
"ret": -0.00022612 
},
{
 "date":   4236,
"name": "GSPC.Close",
"price": 131.75,
"rsi": 62.368,
"ret": -0.0067099 
},
{
 "date":   4239,
"name": "GSPC.Close",
"price": 132.54,
"rsi":  56.89,
"ret": 0.0059962 
},
{
 "date":   4240,
"name": "GSPC.Close",
"price": 133.85,
"rsi": 60.229,
"ret": 0.0098838 
},
{
 "date":   4241,
"name": "GSPC.Close",
"price":  133.4,
"rsi": 65.062,
"ret": -0.003362 
},
{
 "date":   4242,
"name": "GSPC.Close",
"price": 133.51,
"rsi": 62.263,
"ret": 0.00082459 
},
{
 "date":   4243,
"name": "GSPC.Close",
"price": 132.49,
"rsi": 62.686,
"ret": -0.0076399 
},
{
 "date":   4246,
"name": "GSPC.Close",
"price": 131.22,
"rsi": 56.381,
"ret": -0.0095856 
},
{
 "date":   4247,
"name": "GSPC.Close",
"price": 130.11,
"rsi": 49.682,
"ret": -0.0084591 
},
{
 "date":   4248,
"name": "GSPC.Close",
"price": 130.49,
"rsi": 44.684,
"ret": 0.0029206 
},
{
 "date":   4249,
"name": "GSPC.Close",
"price": 130.69,
"rsi": 46.662,
"ret": 0.0015327 
},
{
 "date":   4250,
"name": "GSPC.Close",
"price": 129.23,
"rsi": 47.722,
"ret": -0.011171 
},
{
 "date":   4253,
"name": "GSPC.Close",
"price":  125.5,
"rsi": 41.275,
"ret": -0.028863 
},
{
 "date":   4254,
"name": "GSPC.Close",
"price": 125.13,
"rsi": 30.091,
"ret": -0.0029482 
},
{
 "date":   4255,
"name": "GSPC.Close",
"price": 124.96,
"rsi": 29.245,
"ret": -0.0013586 
},
{
 "date":   4256,
"name": "GSPC.Close",
"price": 123.51,
"rsi": 28.843,
"ret": -0.011604 
},
{
 "date":   4257,
"name": "GSPC.Close",
"price": 124.08,
"rsi": 25.613,
"ret": 0.004615 
},
{
 "date":   4260,
"name": "GSPC.Close",
"price": 122.79,
"rsi":  28.98,
"ret": -0.010397 
},
{
 "date":   4261,
"name": "GSPC.Close",
"price": 123.02,
"rsi": 26.101,
"ret": 0.0018731 
},
{
 "date":   4262,
"name": "GSPC.Close",
"price": 123.49,
"rsi": 27.484,
"ret": 0.0038205 
},
{
 "date":   4263,
"name": "GSPC.Close",
"price": 121.24,
"rsi": 30.353,
"ret": -0.01822 
},
{
 "date":   4264,
"name": "GSPC.Close",
"price": 120.07,
"rsi": 25.211,
"ret": -0.0096503 
},
{
 "date":   4268,
"name": "GSPC.Close",
"price": 117.98,
"rsi": 23.026,
"ret": -0.017407 
},
{
 "date":   4269,
"name": "GSPC.Close",
"price":  118.4,
"rsi": 19.736,
"ret": 0.0035599 
},
{
 "date":   4270,
"name": "GSPC.Close",
"price": 120.14,
"rsi": 22.144,
"ret": 0.014696 
},
{
 "date":   4271,
"name": "GSPC.Close",
"price": 121.61,
"rsi": 31.333,
"ret": 0.012236 
},
{
 "date":   4274,
"name": "GSPC.Close",
"price": 120.66,
"rsi": 37.991,
"ret": -0.0078119 
},
{
 "date":   4275,
"name": "GSPC.Close",
"price": 119.77,
"rsi":  35.59,
"ret": -0.0073761 
},
{
 "date":   4276,
"name": "GSPC.Close",
"price": 118.87,
"rsi": 33.456,
"ret": -0.0075144 
},
{
 "date":   4277,
"name": "GSPC.Close",
"price": 117.15,
"rsi": 31.405,
"ret": -0.01447 
},
{
 "date":   4278,
"name": "GSPC.Close",
"price": 116.26,
"rsi": 27.887,
"ret": -0.0075971 
},
{
 "date":   4281,
"name": "GSPC.Close",
"price": 117.24,
"rsi": 26.248,
"ret": 0.0084294 
},
{
 "date":   4282,
"name": "GSPC.Close",
"price": 116.68,
"rsi": 31.052,
"ret": -0.0047765 
},
{
 "date":   4283,
"name": "GSPC.Close",
"price": 115.65,
"rsi": 29.856,
"ret": -0.0088276 
},
{
 "date":   4284,
"name": "GSPC.Close",
"price": 115.01,
"rsi": 27.738,
"ret": -0.0055339 
},
{
 "date":   4285,
"name": "GSPC.Close",
"price": 112.77,
"rsi": 26.481,
"ret": -0.019477 
},
{
 "date":   4288,
"name": "GSPC.Close",
"price": 115.53,
"rsi": 22.619,
"ret": 0.024475 
},
{
 "date":   4289,
"name": "GSPC.Close",
"price": 115.94,
"rsi": 35.167,
"ret": 0.0035489 
},
{
 "date":   4290,
"name": "GSPC.Close",
"price": 116.18,
"rsi": 36.807,
"ret": 0.00207 
},
{
 "date":   4291,
"name": "GSPC.Close",
"price": 117.08,
"rsi": 37.798,
"ret": 0.0077466 
},
{
 "date":   4292,
"name": "GSPC.Close",
"price": 119.36,
"rsi": 41.505,
"ret": 0.019474 
},
{
 "date":   4295,
"name": "GSPC.Close",
"price": 119.51,
"rsi": 49.685,
"ret": 0.0012567 
},
{
 "date":   4296,
"name": "GSPC.Close",
"price": 119.39,
"rsi": 50.178,
"ret": -0.0010041 
},
{
 "date":   4297,
"name": "GSPC.Close",
"price": 121.31,
"rsi": 49.758,
"ret": 0.016082 
},
{
 "date":   4298,
"name": "GSPC.Close",
"price": 122.31,
"rsi": 56.098,
"ret": 0.0082433 
},
{
 "date":   4299,
"name": "GSPC.Close",
"price": 121.45,
"rsi":     59,
"ret": -0.0070313 
},
{
 "date":   4302,
"name": "GSPC.Close",
"price": 121.21,
"rsi": 55.596,
"ret": -0.0019761 
},
{
 "date":   4303,
"name": "GSPC.Close",
"price": 120.78,
"rsi": 54.649,
"ret": -0.0035476 
},
{
 "date":   4304,
"name": "GSPC.Close",
"price":  118.8,
"rsi": 52.909,
"ret": -0.016393 
},
{
 "date":   4305,
"name": "GSPC.Close",
"price": 119.71,
"rsi": 45.695,
"ret": 0.0076599 
},
{
 "date":   4306,
"name": "GSPC.Close",
"price": 119.19,
"rsi": 49.128,
"ret": -0.0043438 
},
{
 "date":   4309,
"name": "GSPC.Close",
"price": 118.98,
"rsi": 47.288,
"ret": -0.0017619 
},
{
 "date":   4310,
"name": "GSPC.Close",
"price": 120.28,
"rsi": 46.531,
"ret": 0.010926 
},
{
 "date":   4311,
"name": "GSPC.Close",
"price":  120.1,
"rsi": 51.692,
"ret": -0.0014965 
},
{
 "date":   4312,
"name": "GSPC.Close",
"price": 119.64,
"rsi": 50.958,
"ret": -0.0038301 
},
{
 "date":   4313,
"name": "GSPC.Close",
"price":  118.6,
"rsi": 49.043,
"ret": -0.0086927 
},
{
 "date":   4316,
"name": "GSPC.Close",
"price": 118.16,
"rsi": 44.932,
"ret": -0.0037099 
},
{
 "date":   4317,
"name": "GSPC.Close",
"price": 119.29,
"rsi": 43.279,
"ret": 0.0095633 
},
{
 "date":   4318,
"name": "GSPC.Close",
"price": 119.45,
"rsi": 48.517,
"ret": 0.0013413 
},
{
 "date":   4319,
"name": "GSPC.Close",
"price": 119.06,
"rsi": 49.232,
"ret": -0.003265 
},
{
 "date":   4320,
"name": "GSPC.Close",
"price": 121.89,
"rsi": 47.501,
"ret": 0.02377 
},
{
 "date":   4323,
"name": "GSPC.Close",
"price":  124.2,
"rsi": 58.819,
"ret": 0.018952 
},
{
 "date":   4324,
"name": "GSPC.Close",
"price":  124.8,
"rsi":  65.38,
"ret": 0.0048309 
},
{
 "date":   4325,
"name": "GSPC.Close",
"price": 124.74,
"rsi": 66.857,
"ret": -0.00048077 
},
{
 "date":   4326,
"name": "GSPC.Close",
"price": 123.54,
"rsi": 66.551,
"ret": -0.00962 
},
{
 "date":   4327,
"name": "GSPC.Close",
"price": 122.67,
"rsi": 60.583,
"ret": -0.0070423 
},
{
 "date":   4330,
"name": "GSPC.Close",
"price": 123.29,
"rsi": 56.619,
"ret": 0.0050542 
},
{
 "date":   4331,
"name": "GSPC.Close",
"price":  122.7,
"rsi": 58.693,
"ret": -0.0047855 
},
{
 "date":   4332,
"name": "GSPC.Close",
"price": 122.92,
"rsi": 55.952,
"ret": 0.001793 
},
{
 "date":   4333,
"name": "GSPC.Close",
"price": 123.19,
"rsi": 56.763,
"ret": 0.0021966 
},
{
 "date":   4334,
"name": "GSPC.Close",
"price": 121.67,
"rsi":  57.79,
"ret": -0.012339 
},
{
 "date":   4337,
"name": "GSPC.Close",
"price": 120.24,
"rsi": 50.514,
"ret": -0.011753 
},
{
 "date":   4338,
"name": "GSPC.Close",
"price": 121.15,
"rsi": 44.799,
"ret": 0.0075682 
},
{
 "date":   4339,
"name": "GSPC.Close",
"price": 120.26,
"rsi": 48.771,
"ret": -0.0073463 
},
{
 "date":   4340,
"name": "GSPC.Close",
"price": 120.71,
"rsi": 45.336,
"ret": 0.0037419 
},
{
 "date":   4341,
"name": "GSPC.Close",
"price": 121.71,
"rsi": 47.355,
"ret": 0.0082843 
},
{
 "date":   4344,
"name": "GSPC.Close",
"price":  121.6,
"rsi": 51.631,
"ret": -0.00090379 
},
{
 "date":   4345,
"name": "GSPC.Close",
"price": 123.51,
"rsi": 51.139,
"ret": 0.015707 
},
{
 "date":   4346,
"name": "GSPC.Close",
"price": 124.05,
"rsi": 58.529,
"ret": 0.0043721 
},
{
 "date":   4348,
"name": "GSPC.Close",
"price": 125.09,
"rsi": 60.355,
"ret": 0.0083837 
},
{
 "date":   4351,
"name": "GSPC.Close",
"price": 126.35,
"rsi": 63.672,
"ret": 0.010073 
},
{
 "date":   4352,
"name": "GSPC.Close",
"price":  126.1,
"rsi": 67.248,
"ret": -0.0019786 
},
{
 "date":   4353,
"name": "GSPC.Close",
"price": 124.69,
"rsi": 65.863,
"ret": -0.011182 
},
{
 "date":   4354,
"name": "GSPC.Close",
"price": 125.12,
"rsi": 58.539,
"ret": 0.0034486 
},
{
 "date":   4355,
"name": "GSPC.Close",
"price": 126.26,
"rsi":     60,
"ret": 0.0091113 
},
{
 "date":   4358,
"name": "GSPC.Close",
"price": 125.19,
"rsi": 63.656,
"ret": -0.0084746 
},
{
 "date":   4359,
"name": "GSPC.Close",
"price": 124.82,
"rsi": 58.272,
"ret": -0.0029555 
},
{
 "date":   4360,
"name": "GSPC.Close",
"price": 125.48,
"rsi": 56.493,
"ret": 0.0052876 
},
{
 "date":   4361,
"name": "GSPC.Close",
"price": 125.71,
"rsi": 58.903,
"ret": 0.001833 
},
{
 "date":   4362,
"name": "GSPC.Close",
"price": 124.93,
"rsi": 59.741,
"ret": -0.0062048 
},
{
 "date":   4365,
"name": "GSPC.Close",
"price": 122.78,
"rsi": 55.604,
"ret": -0.01721 
},
{
 "date":   4366,
"name": "GSPC.Close",
"price": 122.99,
"rsi": 46.124,
"ret": 0.0017104 
},
{
 "date":   4367,
"name": "GSPC.Close",
"price": 122.42,
"rsi": 47.073,
"ret": -0.0046345 
},
{
 "date":   4368,
"name": "GSPC.Close",
"price": 123.12,
"rsi": 44.768,
"ret": 0.005718 
},
{
 "date":   4369,
"name": "GSPC.Close",
"price":    124,
"rsi": 48.128,
"ret": 0.0071475 
},
{
 "date":   4372,
"name": "GSPC.Close",
"price": 123.34,
"rsi": 52.075,
"ret": -0.0053226 
},
{
 "date":   4373,
"name": "GSPC.Close",
"price": 122.88,
"rsi":  49.06,
"ret": -0.0037295 
},
{
 "date":   4374,
"name": "GSPC.Close",
"price": 122.31,
"rsi": 47.016,
"ret": -0.0046387 
},
{
 "date":   4375,
"name": "GSPC.Close",
"price": 122.54,
"rsi": 44.541,
"ret": 0.0018805 
},
{
 "date":   4379,
"name": "GSPC.Close",
"price": 122.27,
"rsi": 45.781,
"ret": -0.0022034 
},
{
 "date":   4380,
"name": "GSPC.Close",
"price": 121.67,
"rsi": 44.522,
"ret": -0.0049072 
},
{
 "date":   4381,
"name": "GSPC.Close",
"price":  122.3,
"rsi": 41.773,
"ret": 0.0051779 
},
{
 "date":   4382,
"name": "GSPC.Close",
"price": 122.55,
"rsi": 45.573,
"ret": 0.0020442 
},
{
 "date":   4386,
"name": "GSPC.Close",
"price": 122.74,
"rsi":  47.05,
"ret": 0.0015504 
},
{
 "date":   4387,
"name": "GSPC.Close",
"price": 120.05,
"rsi": 48.201,
"ret": -0.021916 
},
{
 "date":   4388,
"name": "GSPC.Close",
"price": 119.18,
"rsi": 36.207,
"ret": -0.007247 
},
{
 "date":   4389,
"name": "GSPC.Close",
"price": 118.93,
"rsi": 33.319,
"ret": -0.0020977 
},
{
 "date":   4390,
"name": "GSPC.Close",
"price": 119.55,
"rsi": 32.517,
"ret": 0.0052132 
},
{
 "date":   4393,
"name": "GSPC.Close",
"price": 116.78,
"rsi": 36.595,
"ret": -0.02317 
},
{
 "date":   4394,
"name": "GSPC.Close",
"price":  116.3,
"rsi": 28.351,
"ret": -0.0041103 
},
{
 "date":   4395,
"name": "GSPC.Close",
"price": 114.88,
"rsi": 27.207,
"ret": -0.01221 
},
{
 "date":   4396,
"name": "GSPC.Close",
"price": 115.54,
"rsi": 24.108,
"ret": 0.0057451 
},
{
 "date":   4397,
"name": "GSPC.Close",
"price": 116.33,
"rsi": 28.201,
"ret": 0.0068375 
},
{
 "date":   4400,
"name": "GSPC.Close",
"price": 117.22,
"rsi": 32.869,
"ret": 0.0076506 
},
{
 "date":   4401,
"name": "GSPC.Close",
"price": 115.97,
"rsi": 37.776,
"ret": -0.010664 
},
{
 "date":   4402,
"name": "GSPC.Close",
"price": 115.27,
"rsi": 34.015,
"ret": -0.006036 
},
{
 "date":   4403,
"name": "GSPC.Close",
"price": 115.75,
"rsi": 32.088,
"ret": 0.0041641 
},
{
 "date":   4404,
"name": "GSPC.Close",
"price": 115.38,
"rsi": 34.815,
"ret": -0.0031965 
},
{
 "date":   4407,
"name": "GSPC.Close",
"price": 115.41,
"rsi": 33.692,
"ret": 0.00026001 
},
{
 "date":   4408,
"name": "GSPC.Close",
"price": 115.19,
"rsi": 33.878,
"ret": -0.0019062 
},
{
 "date":   4409,
"name": "GSPC.Close",
"price": 115.74,
"rsi": 33.143,
"ret": 0.0047747 
},
{
 "date":   4410,
"name": "GSPC.Close",
"price": 118.92,
"rsi": 36.833,
"ret": 0.027475 
},
{
 "date":   4411,
"name": "GSPC.Close",
"price":  120.4,
"rsi": 52.989,
"ret": 0.012445 
},
{
 "date":   4414,
"name": "GSPC.Close",
"price": 117.78,
"rsi": 58.331,
"ret": -0.021761 
},
{
 "date":   4415,
"name": "GSPC.Close",
"price": 118.01,
"rsi": 47.945,
"ret": 0.0019528 
},
{
 "date":   4416,
"name": "GSPC.Close",
"price": 116.48,
"rsi": 48.807,
"ret": -0.012965 
},
{
 "date":   4417,
"name": "GSPC.Close",
"price": 116.42,
"rsi": 43.632,
"ret": -0.00051511 
},
{
 "date":   4418,
"name": "GSPC.Close",
"price": 117.26,
"rsi": 43.438,
"ret": 0.0072153 
},
{
 "date":   4421,
"name": "GSPC.Close",
"price": 114.63,
"rsi":     47,
"ret": -0.022429 
},
{
 "date":   4422,
"name": "GSPC.Close",
"price": 113.68,
"rsi": 38.768,
"ret": -0.0082875 
},
{
 "date":   4423,
"name": "GSPC.Close",
"price": 114.66,
"rsi": 36.295,
"ret": 0.0086207 
},
{
 "date":   4424,
"name": "GSPC.Close",
"price": 114.43,
"rsi": 40.511,
"ret": -0.0020059 
},
{
 "date":   4425,
"name": "GSPC.Close",
"price": 114.38,
"rsi": 39.844,
"ret": -0.00043695 
},
{
 "date":   4429,
"name": "GSPC.Close",
"price": 114.06,
"rsi": 39.691,
"ret": -0.0027977 
},
{
 "date":   4430,
"name": "GSPC.Close",
"price": 113.69,
"rsi": 38.669,
"ret": -0.0032439 
},
{
 "date":   4431,
"name": "GSPC.Close",
"price": 113.82,
"rsi": 37.467,
"ret": 0.0011435 
},
{
 "date":   4432,
"name": "GSPC.Close",
"price": 113.22,
"rsi": 38.194,
"ret": -0.0052715 
},
{
 "date":   4435,
"name": "GSPC.Close",
"price": 111.59,
"rsi": 36.108,
"ret": -0.014397 
},
{
 "date":   4436,
"name": "GSPC.Close",
"price": 111.51,
"rsi": 31.133,
"ret": -0.00071691 
},
{
 "date":   4437,
"name": "GSPC.Close",
"price": 113.47,
"rsi": 30.908,
"ret": 0.017577 
},
{
 "date":   4438,
"name": "GSPC.Close",
"price": 113.21,
"rsi": 41.976,
"ret": -0.0022914 
},
{
 "date":   4439,
"name": "GSPC.Close",
"price": 113.11,
"rsi": 41.037,
"ret": -0.00088331 
},
{
 "date":   4442,
"name": "GSPC.Close",
"price": 113.31,
"rsi":  40.66,
"ret": 0.0017682 
},
{
 "date":   4443,
"name": "GSPC.Close",
"price": 112.68,
"rsi": 41.811,
"ret": -0.00556 
},
{
 "date":   4444,
"name": "GSPC.Close",
"price": 110.92,
"rsi":  39.23,
"ret": -0.015619 
},
{
 "date":   4445,
"name": "GSPC.Close",
"price": 109.88,
"rsi": 33.086,
"ret": -0.0093761 
},
{
 "date":   4446,
"name": "GSPC.Close",
"price": 109.34,
"rsi": 30.087,
"ret": -0.0049145 
},
{
 "date":   4449,
"name": "GSPC.Close",
"price": 107.34,
"rsi": 28.636,
"ret": -0.018292 
},
{
 "date":   4450,
"name": "GSPC.Close",
"price": 108.83,
"rsi": 24.016,
"ret": 0.013881 
},
{
 "date":   4451,
"name": "GSPC.Close",
"price": 109.41,
"rsi": 32.725,
"ret": 0.0053294 
},
{
 "date":   4452,
"name": "GSPC.Close",
"price": 109.36,
"rsi": 35.809,
"ret": -0.000457 
},
{
 "date":   4453,
"name": "GSPC.Close",
"price": 108.61,
"rsi": 35.657,
"ret": -0.0068581 
},
{
 "date":   4456,
"name": "GSPC.Close",
"price": 109.45,
"rsi": 33.372,
"ret": 0.0077341 
},
{
 "date":   4457,
"name": "GSPC.Close",
"price": 109.28,
"rsi": 38.152,
"ret": -0.0015532 
},
{
 "date":   4458,
"name": "GSPC.Close",
"price": 109.08,
"rsi": 37.565,
"ret": -0.0018302 
},
{
 "date":   4459,
"name": "GSPC.Close",
"price":  110.3,
"rsi": 36.846,
"ret": 0.011184 
},
{
 "date":   4460,
"name": "GSPC.Close",
"price": 110.61,
"rsi": 43.897,
"ret": 0.0028105 
},
{
 "date":   4463,
"name": "GSPC.Close",
"price": 112.77,
"rsi":  45.56,
"ret": 0.019528 
},
{
 "date":   4464,
"name": "GSPC.Close",
"price": 113.55,
"rsi": 55.467,
"ret": 0.0069167 
},
{
 "date":   4465,
"name": "GSPC.Close",
"price": 112.97,
"rsi":  58.41,
"ret": -0.0051079 
},
{
 "date":   4466,
"name": "GSPC.Close",
"price": 113.21,
"rsi": 55.474,
"ret": 0.0021245 
},
{
 "date":   4467,
"name": "GSPC.Close",
"price": 111.94,
"rsi":  56.45,
"ret": -0.011218 
},
{
 "date":   4470,
"name": "GSPC.Close",
"price":  112.3,
"rsi": 50.184,
"ret": 0.003216 
},
{
 "date":   4471,
"name": "GSPC.Close",
"price": 112.27,
"rsi": 51.817,
"ret": -0.00026714 
},
{
 "date":   4472,
"name": "GSPC.Close",
"price": 111.96,
"rsi": 51.665,
"ret": -0.0027612 
},
{
 "date":   4473,
"name": "GSPC.Close",
"price": 113.79,
"rsi": 50.032,
"ret": 0.016345 
},
{
 "date":   4474,
"name": "GSPC.Close",
"price": 115.12,
"rsi": 58.391,
"ret": 0.011688 
},
{
 "date":   4477,
"name": "GSPC.Close",
"price": 114.73,
"rsi": 63.209,
"ret": -0.0033878 
},
{
 "date":   4478,
"name": "GSPC.Close",
"price": 115.36,
"rsi": 60.979,
"ret": 0.0054912 
},
{
 "date":   4479,
"name": "GSPC.Close",
"price": 115.46,
"rsi": 63.235,
"ret": 0.00086685 
},
{
 "date":   4480,
"name": "GSPC.Close",
"price": 116.22,
"rsi": 63.595,
"ret": 0.0065824 
},
{
 "date":   4484,
"name": "GSPC.Close",
"price":    116,
"rsi": 66.294,
"ret": -0.001893 
},
{
 "date":   4485,
"name": "GSPC.Close",
"price": 115.99,
"rsi": 64.797,
"ret": -8.6207e-05 
},
{
 "date":   4486,
"name": "GSPC.Close",
"price": 115.83,
"rsi": 64.725,
"ret": -0.0013794 
},
{
 "date":   4487,
"name": "GSPC.Close",
"price": 116.35,
"rsi": 63.516,
"ret": 0.0044893 
},
{
 "date":   4488,
"name": "GSPC.Close",
"price": 116.81,
"rsi": 65.755,
"ret": 0.0039536 
},
{
 "date":   4491,
"name": "GSPC.Close",
"price":  116.7,
"rsi": 67.646,
"ret": -0.0009417 
},
{
 "date":   4492,
"name": "GSPC.Close",
"price": 115.44,
"rsi": 66.698,
"ret": -0.010797 
},
{
 "date":   4493,
"name": "GSPC.Close",
"price": 115.72,
"rsi":  56.86,
"ret": 0.0024255 
},
{
 "date":   4494,
"name": "GSPC.Close",
"price": 117.19,
"rsi": 58.331,
"ret": 0.012703 
},
{
 "date":   4495,
"name": "GSPC.Close",
"price": 118.64,
"rsi": 65.065,
"ret": 0.012373 
},
{
 "date":   4498,
"name": "GSPC.Close",
"price": 119.26,
"rsi": 70.184,
"ret": 0.0052259 
},
{
 "date":   4499,
"name": "GSPC.Close",
"price":    118,
"rsi": 72.068,
"ret": -0.010565 
},
{
 "date":   4500,
"name": "GSPC.Close",
"price": 117.26,
"rsi": 63.311,
"ret": -0.0062712 
},
{
 "date":   4501,
"name": "GSPC.Close",
"price": 116.14,
"rsi": 58.792,
"ret": -0.0095514 
},
{
 "date":   4502,
"name": "GSPC.Close",
"price": 116.44,
"rsi": 52.665,
"ret": 0.0025831 
},
{
 "date":   4505,
"name": "GSPC.Close",
"price": 116.82,
"rsi": 54.047,
"ret": 0.0032635 
},
{
 "date":   4506,
"name": "GSPC.Close",
"price": 117.46,
"rsi": 55.806,
"ret": 0.0054785 
},
{
 "date":   4507,
"name": "GSPC.Close",
"price": 117.67,
"rsi": 58.676,
"ret": 0.0017878 
},
{
 "date":   4508,
"name": "GSPC.Close",
"price": 118.68,
"rsi": 59.602,
"ret": 0.0085833 
},
{
 "date":   4509,
"name": "GSPC.Close",
"price": 119.47,
"rsi": 63.807,
"ret": 0.0066566 
},
{
 "date":   4512,
"name": "GSPC.Close",
"price": 118.38,
"rsi": 66.725,
"ret": -0.0091236 
},
{
 "date":   4513,
"name": "GSPC.Close",
"price": 119.42,
"rsi": 59.588,
"ret": 0.0087853 
},
{
 "date":   4514,
"name": "GSPC.Close",
"price": 119.17,
"rsi": 63.589,
"ret": -0.0020935 
},
{
 "date":   4515,
"name": "GSPC.Close",
"price": 118.22,
"rsi":     62,
"ret": -0.0079718 
},
{
 "date":   4516,
"name": "GSPC.Close",
"price": 118.01,
"rsi": 56.247,
"ret": -0.0017763 
},
{
 "date":   4519,
"name": "GSPC.Close",
"price": 116.71,
"rsi": 55.031,
"ret": -0.011016 
},
{
 "date":   4520,
"name": "GSPC.Close",
"price": 115.84,
"rsi": 48.101,
"ret": -0.0074544 
},
{
 "date":   4521,
"name": "GSPC.Close",
"price": 114.89,
"rsi": 44.098,
"ret": -0.008201 
},
{
 "date":   4522,
"name": "GSPC.Close",
"price": 114.59,
"rsi": 40.168,
"ret": -0.0026112 
},
{
 "date":   4523,
"name": "GSPC.Close",
"price": 114.89,
"rsi": 38.986,
"ret": 0.002618 
},
{
 "date":   4526,
"name": "GSPC.Close",
"price": 114.79,
"rsi":  40.86,
"ret": -0.0008704 
},
{
 "date":   4527,
"name": "GSPC.Close",
"price":  114.4,
"rsi": 40.414,
"ret": -0.0033975 
},
{
 "date":   4528,
"name": "GSPC.Close",
"price": 113.11,
"rsi": 38.645,
"ret": -0.011276 
},
{
 "date":   4529,
"name": "GSPC.Close",
"price": 112.66,
"rsi":  33.43,
"ret": -0.0039784 
},
{
 "date":   4530,
"name": "GSPC.Close",
"price": 111.88,
"rsi": 31.817,
"ret": -0.0069235 
},
{
 "date":   4534,
"name": "GSPC.Close",
"price": 111.68,
"rsi": 29.188,
"ret": -0.0017876 
},
{
 "date":   4535,
"name": "GSPC.Close",
"price": 112.04,
"rsi": 28.537,
"ret": 0.0032235 
},
{
 "date":   4536,
"name": "GSPC.Close",
"price": 111.86,
"rsi": 31.499,
"ret": -0.0016066 
},
{
 "date":   4537,
"name": "GSPC.Close",
"price": 110.09,
"rsi": 30.811,
"ret": -0.015823 
},
{
 "date":   4540,
"name": "GSPC.Close",
"price": 110.12,
"rsi": 25.026,
"ret": 0.0002725 
},
{
 "date":   4541,
"name": "GSPC.Close",
"price": 109.63,
"rsi": 25.282,
"ret": -0.0044497 
},
{
 "date":   4542,
"name": "GSPC.Close",
"price": 108.99,
"rsi": 23.849,
"ret": -0.0058378 
},
{
 "date":   4543,
"name": "GSPC.Close",
"price": 109.61,
"rsi": 22.089,
"ret": 0.0056886 
},
{
 "date":   4544,
"name": "GSPC.Close",
"price": 111.24,
"rsi": 27.661,
"ret": 0.014871 
},
{
 "date":   4547,
"name": "GSPC.Close",
"price": 109.96,
"rsi": 39.842,
"ret": -0.011507 
},
{
 "date":   4548,
"name": "GSPC.Close",
"price": 109.69,
"rsi": 34.875,
"ret": -0.0024554 
},
{
 "date":   4549,
"name": "GSPC.Close",
"price": 108.87,
"rsi": 33.915,
"ret": -0.0074756 
},
{
 "date":   4550,
"name": "GSPC.Close",
"price":  107.6,
"rsi": 31.113,
"ret": -0.011665 
},
{
 "date":   4551,
"name": "GSPC.Close",
"price": 107.28,
"rsi": 27.345,
"ret": -0.002974 
},
{
 "date":   4554,
"name": "GSPC.Close",
"price":  107.2,
"rsi": 26.475,
"ret": -0.00074571 
},
{
 "date":   4555,
"name": "GSPC.Close",
"price":  108.3,
"rsi":  26.25,
"ret": 0.010261 
},
{
 "date":   4556,
"name": "GSPC.Close",
"price": 110.14,
"rsi": 34.489,
"ret": 0.01699 
},
{
 "date":   4557,
"name": "GSPC.Close",
"price": 109.83,
"rsi": 45.465,
"ret": -0.0028146 
},
{
 "date":   4558,
"name": "GSPC.Close",
"price": 109.14,
"rsi": 44.124,
"ret": -0.0062824 
},
{
 "date":   4561,
"name": "GSPC.Close",
"price": 110.26,
"rsi":  41.21,
"ret": 0.010262 
},
{
 "date":   4562,
"name": "GSPC.Close",
"price": 110.21,
"rsi": 47.294,
"ret": -0.00045347 
},
{
 "date":   4563,
"name": "GSPC.Close",
"price": 109.61,
"rsi":  47.06,
"ret": -0.0054442 
},
{
 "date":   4564,
"name": "GSPC.Close",
"price": 108.71,
"rsi":  44.23,
"ret": -0.0082109 
},
{
 "date":   4565,
"name": "GSPC.Close",
"price": 107.65,
"rsi": 40.314,
"ret": -0.0097507 
},
{
 "date":   4569,
"name": "GSPC.Close",
"price": 107.29,
"rsi": 36.243,
"ret": -0.0033442 
},
{
 "date":   4570,
"name": "GSPC.Close",
"price": 107.22,
"rsi": 34.953,
"ret": -0.00065244 
},
{
 "date":   4571,
"name": "GSPC.Close",
"price": 107.53,
"rsi": 34.694,
"ret": 0.0028913 
},
{
 "date":   4572,
"name": "GSPC.Close",
"price": 108.83,
"rsi": 36.921,
"ret": 0.01209 
},
{
 "date":   4575,
"name": "GSPC.Close",
"price": 109.57,
"rsi": 45.339,
"ret": 0.0067996 
},
{
 "date":   4576,
"name": "GSPC.Close",
"price": 109.45,
"rsi": 49.472,
"ret": -0.0010952 
},
{
 "date":   4577,
"name": "GSPC.Close",
"price": 110.44,
"rsi": 48.827,
"ret": 0.0090452 
},
{
 "date":   4578,
"name": "GSPC.Close",
"price": 110.47,
"rsi": 54.138,
"ret": 0.00027164 
},
{
 "date":   4579,
"name": "GSPC.Close",
"price": 111.07,
"rsi": 54.293,
"ret": 0.0054313 
},
{
 "date":   4582,
"name": "GSPC.Close",
"price": 110.73,
"rsi": 57.391,
"ret": -0.0030611 
},
{
 "date":   4583,
"name": "GSPC.Close",
"price": 111.54,
"rsi": 55.111,
"ret": 0.0073151 
},
{
 "date":   4584,
"name": "GSPC.Close",
"price": 111.42,
"rsi": 59.262,
"ret": -0.0010758 
},
{
 "date":   4585,
"name": "GSPC.Close",
"price": 111.48,
"rsi": 58.401,
"ret": 0.0005385 
},
{
 "date":   4586,
"name": "GSPC.Close",
"price": 111.17,
"rsi": 58.724,
"ret": -0.0027808 
},
{
 "date":   4589,
"name": "GSPC.Close",
"price": 110.36,
"rsi": 56.291,
"ret": -0.0072861 
},
{
 "date":   4590,
"name": "GSPC.Close",
"price": 109.43,
"rsi": 50.413,
"ret": -0.008427 
},
{
 "date":   4591,
"name": "GSPC.Close",
"price": 107.74,
"rsi": 44.649,
"ret": -0.015444 
},
{
 "date":   4592,
"name": "GSPC.Close",
"price": 107.72,
"rsi": 36.485,
"ret": -0.00018563 
},
{
 "date":   4593,
"name": "GSPC.Close",
"price": 107.09,
"rsi":   36.4,
"ret": -0.0058485 
},
{
 "date":   4596,
"name": "GSPC.Close",
"price": 108.98,
"rsi": 33.739,
"ret": 0.017649 
},
{
 "date":   4597,
"name": "GSPC.Close",
"price": 107.83,
"rsi": 46.399,
"ret": -0.010552 
},
{
 "date":   4598,
"name": "GSPC.Close",
"price": 106.14,
"rsi": 41.236,
"ret": -0.015673 
},
{
 "date":   4599,
"name": "GSPC.Close",
"price": 105.16,
"rsi": 35.062,
"ret": -0.0092331 
},
{
 "date":   4600,
"name": "GSPC.Close",
"price": 103.71,
"rsi": 32.064,
"ret": -0.013789 
},
{
 "date":   4603,
"name": "GSPC.Close",
"price": 103.08,
"rsi":  28.22,
"ret": -0.0060746 
},
{
 "date":   4604,
"name": "GSPC.Close",
"price": 102.84,
"rsi":  26.72,
"ret": -0.0023283 
},
{
 "date":   4605,
"name": "GSPC.Close",
"price":  102.6,
"rsi":  26.15,
"ret": -0.0023337 
},
{
 "date":   4606,
"name": "GSPC.Close",
"price": 102.42,
"rsi": 25.563,
"ret": -0.0017544 
},
{
 "date":   4607,
"name": "GSPC.Close",
"price": 103.85,
"rsi": 25.108,
"ret": 0.013962 
},
{
 "date":   4610,
"name": "GSPC.Close",
"price": 104.09,
"rsi": 35.012,
"ret": 0.002311 
},
{
 "date":   4611,
"name": "GSPC.Close",
"price": 109.04,
"rsi": 36.529,
"ret": 0.047555 
},
{
 "date":   4612,
"name": "GSPC.Close",
"price": 108.54,
"rsi": 58.203,
"ret": -0.0045855 
},
{
 "date":   4613,
"name": "GSPC.Close",
"price": 109.16,
"rsi": 56.118,
"ret": 0.0057122 
},
{
 "date":   4614,
"name": "GSPC.Close",
"price": 113.02,
"rsi": 58.121,
"ret": 0.035361 
},
{
 "date":   4617,
"name": "GSPC.Close",
"price": 116.11,
"rsi": 67.934,
"ret": 0.02734 
},
{
 "date":   4618,
"name": "GSPC.Close",
"price": 115.35,
"rsi": 73.323,
"ret": -0.0065455 
},
{
 "date":   4619,
"name": "GSPC.Close",
"price": 117.58,
"rsi": 70.198,
"ret": 0.019332 
},
{
 "date":   4620,
"name": "GSPC.Close",
"price": 118.55,
"rsi": 73.735,
"ret": 0.0082497 
},
{
 "date":   4621,
"name": "GSPC.Close",
"price": 117.11,
"rsi": 75.118,
"ret": -0.012147 
},
{
 "date":   4624,
"name": "GSPC.Close",
"price": 117.66,
"rsi": 69.285,
"ret": 0.0046964 
},
{
 "date":   4625,
"name": "GSPC.Close",
"price": 119.51,
"rsi": 70.235,
"ret": 0.015723 
},
{
 "date":   4626,
"name": "GSPC.Close",
"price": 118.25,
"rsi": 73.236,
"ret": -0.010543 
},
{
 "date":   4627,
"name": "GSPC.Close",
"price": 120.29,
"rsi": 68.193,
"ret": 0.017252 
},
{
 "date":   4628,
"name": "GSPC.Close",
"price": 122.68,
"rsi": 71.603,
"ret": 0.019869 
},
{
 "date":   4632,
"name": "GSPC.Close",
"price": 121.37,
"rsi": 74.986,
"ret": -0.010678 
},
{
 "date":   4633,
"name": "GSPC.Close",
"price":  122.2,
"rsi": 70.059,
"ret": 0.0068386 
},
{
 "date":   4634,
"name": "GSPC.Close",
"price": 121.97,
"rsi": 71.344,
"ret": -0.0018822 
},
{
 "date":   4635,
"name": "GSPC.Close",
"price": 120.97,
"rsi": 70.442,
"ret": -0.0081987 
},
{
 "date":   4638,
"name": "GSPC.Close",
"price": 122.24,
"rsi": 66.505,
"ret": 0.010498 
},
{
 "date":   4639,
"name": "GSPC.Close",
"price":  123.1,
"rsi": 68.883,
"ret": 0.0070353 
},
{
 "date":   4640,
"name": "GSPC.Close",
"price": 124.29,
"rsi": 70.415,
"ret": 0.0096669 
},
{
 "date":   4641,
"name": "GSPC.Close",
"price": 123.77,
"rsi": 72.438,
"ret": -0.0041838 
},
{
 "date":   4642,
"name": "GSPC.Close",
"price": 122.55,
"rsi":  70.18,
"ret": -0.009857 
},
{
 "date":   4645,
"name": "GSPC.Close",
"price": 122.51,
"rsi": 65.058,
"ret": -0.0003264 
},
{
 "date":   4646,
"name": "GSPC.Close",
"price": 124.88,
"rsi":  64.89,
"ret": 0.019345 
},
{
 "date":   4647,
"name": "GSPC.Close",
"price": 123.99,
"rsi": 69.838,
"ret": -0.0071268 
},
{
 "date":   4648,
"name": "GSPC.Close",
"price": 123.81,
"rsi": 66.073,
"ret": -0.0014517 
},
{
 "date":   4649,
"name": "GSPC.Close",
"price": 123.32,
"rsi": 65.306,
"ret": -0.0039577 
},
{
 "date":   4652,
"name": "GSPC.Close",
"price": 123.62,
"rsi": 63.157,
"ret": 0.0024327 
},
{
 "date":   4653,
"name": "GSPC.Close",
"price": 123.24,
"rsi": 63.939,
"ret": -0.0030739 
},
{
 "date":   4654,
"name": "GSPC.Close",
"price": 121.63,
"rsi": 62.139,
"ret": -0.013064 
},
{
 "date":   4655,
"name": "GSPC.Close",
"price": 120.42,
"rsi": 55.066,
"ret": -0.0099482 
},
{
 "date":   4656,
"name": "GSPC.Close",
"price": 121.97,
"rsi": 50.421,
"ret": 0.012872 
},
{
 "date":   4659,
"name": "GSPC.Close",
"price": 121.51,
"rsi": 55.589,
"ret": -0.0037714 
},
{
 "date":   4660,
"name": "GSPC.Close",
"price": 121.98,
"rsi": 53.797,
"ret": 0.003868 
},
{
 "date":   4661,
"name": "GSPC.Close",
"price": 125.97,
"rsi":  55.38,
"ret": 0.03271 
},
{
 "date":   4662,
"name": "GSPC.Close",
"price":  128.8,
"rsi": 66.022,
"ret": 0.022466 
},
{
 "date":   4663,
"name": "GSPC.Close",
"price": 131.05,
"rsi": 71.259,
"ret": 0.017469 
},
{
 "date":   4666,
"name": "GSPC.Close",
"price": 134.47,
"rsi": 74.609,
"ret": 0.026097 
},
{
 "date":   4667,
"name": "GSPC.Close",
"price": 134.44,
"rsi": 78.678,
"ret": -0.0002231 
},
{
 "date":   4668,
"name": "GSPC.Close",
"price": 136.71,
"rsi": 78.559,
"ret": 0.016885 
},
{
 "date":   4669,
"name": "GSPC.Close",
"price": 134.57,
"rsi":  80.91,
"ret": -0.015654 
},
{
 "date":   4670,
"name": "GSPC.Close",
"price": 133.57,
"rsi": 72.805,
"ret": -0.0074311 
},
{
 "date":   4673,
"name": "GSPC.Close",
"price": 136.73,
"rsi": 69.311,
"ret": 0.023658 
},
{
 "date":   4674,
"name": "GSPC.Close",
"price": 136.58,
"rsi": 73.619,
"ret": -0.0010971 
},
{
 "date":   4675,
"name": "GSPC.Close",
"price": 139.23,
"rsi": 73.095,
"ret": 0.019403 
},
{
 "date":   4676,
"name": "GSPC.Close",
"price": 139.06,
"rsi": 76.307,
"ret": -0.001221 
},
{
 "date":   4677,
"name": "GSPC.Close",
"price": 138.83,
"rsi": 75.683,
"ret": -0.001654 
},
{
 "date":   4680,
"name": "GSPC.Close",
"price": 133.32,
"rsi": 74.791,
"ret": -0.039689 
},
{
 "date":   4681,
"name": "GSPC.Close",
"price": 134.48,
"rsi":  57.36,
"ret": 0.0087009 
},
{
 "date":   4682,
"name": "GSPC.Close",
"price": 135.29,
"rsi":   59.5,
"ret": 0.0060232 
},
{
 "date":   4683,
"name": "GSPC.Close",
"price": 133.59,
"rsi": 60.973,
"ret": -0.012566 
},
{
 "date":   4684,
"name": "GSPC.Close",
"price": 133.72,
"rsi": 56.342,
"ret": 0.00097313 
},
{
 "date":   4687,
"name": "GSPC.Close",
"price": 135.47,
"rsi": 56.613,
"ret": 0.013087 
},
{
 "date":   4688,
"name": "GSPC.Close",
"price": 137.49,
"rsi":   60.2,
"ret": 0.014911 
},
{
 "date":   4689,
"name": "GSPC.Close",
"price": 142.87,
"rsi": 63.909,
"ret": 0.03913 
},
{
 "date":   4690,
"name": "GSPC.Close",
"price": 141.85,
"rsi": 71.521,
"ret": -0.0071394 
},
{
 "date":   4691,
"name": "GSPC.Close",
"price": 142.16,
"rsi": 68.568,
"ret": 0.0021854 
},
{
 "date":   4694,
"name": "GSPC.Close",
"price": 140.44,
"rsi": 68.987,
"ret": -0.012099 
},
{
 "date":   4695,
"name": "GSPC.Close",
"price": 143.02,
"rsi": 63.897,
"ret": 0.018371 
},
{
 "date":   4696,
"name": "GSPC.Close",
"price": 141.16,
"rsi": 67.742,
"ret": -0.013005 
},
{
 "date":   4697,
"name": "GSPC.Close",
"price": 141.75,
"rsi": 62.568,
"ret": 0.0041797 
},
{
 "date":   4698,
"name": "GSPC.Close",
"price": 139.53,
"rsi":  63.52,
"ret": -0.015661 
},
{
 "date":   4701,
"name": "GSPC.Close",
"price": 137.03,
"rsi": 57.587,
"ret": -0.017917 
},
{
 "date":   4702,
"name": "GSPC.Close",
"price": 135.42,
"rsi": 51.728,
"ret": -0.011749 
},
{
 "date":   4703,
"name": "GSPC.Close",
"price": 137.93,
"rsi": 48.318,
"ret": 0.018535 
},
{
 "date":   4704,
"name": "GSPC.Close",
"price": 138.34,
"rsi": 53.468,
"ret": 0.0029725 
},
{
 "date":   4705,
"name": "GSPC.Close",
"price": 137.02,
"rsi": 54.269,
"ret": -0.0095417 
},
{
 "date":   4708,
"name": "GSPC.Close",
"price": 134.22,
"rsi": 51.211,
"ret": -0.020435 
},
{
 "date":   4709,
"name": "GSPC.Close",
"price": 132.93,
"rsi":  45.37,
"ret": -0.0096111 
},
{
 "date":   4710,
"name": "GSPC.Close",
"price": 133.88,
"rsi":  42.94,
"ret": 0.0071466 
},
{
 "date":   4712,
"name": "GSPC.Close",
"price": 134.88,
"rsi": 45.265,
"ret": 0.0074694 
},
{
 "date":   4715,
"name": "GSPC.Close",
"price":  134.2,
"rsi": 47.681,
"ret": -0.0050415 
},
{
 "date":   4716,
"name": "GSPC.Close",
"price": 138.53,
"rsi": 46.188,
"ret": 0.032265 
},
{
 "date":   4717,
"name": "GSPC.Close",
"price": 138.72,
"rsi": 55.702,
"ret": 0.0013715 
},
{
 "date":   4718,
"name": "GSPC.Close",
"price": 138.82,
"rsi": 56.069,
"ret": 0.00072088 
},
{
 "date":   4719,
"name": "GSPC.Close",
"price": 138.69,
"rsi": 56.274,
"ret": -0.00093646 
},
{
 "date":   4722,
"name": "GSPC.Close",
"price": 141.77,
"rsi": 55.909,
"ret": 0.022208 
},
{
 "date":   4723,
"name": "GSPC.Close",
"price": 142.72,
"rsi": 62.182,
"ret": 0.006701 
},
{
 "date":   4724,
"name": "GSPC.Close",
"price": 141.82,
"rsi": 63.889,
"ret": -0.0063061 
},
{
 "date":   4725,
"name": "GSPC.Close",
"price":    140,
"rsi": 61.077,
"ret": -0.012833 
},
{
 "date":   4726,
"name": "GSPC.Close",
"price": 139.57,
"rsi": 55.734,
"ret": -0.0030714 
},
{
 "date":   4729,
"name": "GSPC.Close",
"price": 139.95,
"rsi": 54.521,
"ret": 0.0027226 
},
{
 "date":   4730,
"name": "GSPC.Close",
"price":  137.4,
"rsi": 55.444,
"ret": -0.018221 
},
{
 "date":   4731,
"name": "GSPC.Close",
"price": 135.24,
"rsi": 48.351,
"ret": -0.015721 
},
{
 "date":   4732,
"name": "GSPC.Close",
"price":  135.3,
"rsi": 43.298,
"ret": 0.00044366 
},
{
 "date":   4733,
"name": "GSPC.Close",
"price": 137.49,
"rsi": 43.475,
"ret": 0.016186 
},
{
 "date":   4736,
"name": "GSPC.Close",
"price": 136.25,
"rsi": 49.643,
"ret": -0.0090188 
},
{
 "date":   4737,
"name": "GSPC.Close",
"price": 138.61,
"rsi": 46.546,
"ret": 0.017321 
},
{
 "date":   4738,
"name": "GSPC.Close",
"price": 138.83,
"rsi": 52.607,
"ret": 0.0015872 
},
{
 "date":   4739,
"name": "GSPC.Close",
"price": 139.72,
"rsi":  53.14,
"ret": 0.0064107 
},
{
 "date":   4743,
"name": "GSPC.Close",
"price": 142.17,
"rsi":  55.33,
"ret": 0.017535 
},
{
 "date":   4744,
"name": "GSPC.Close",
"price": 140.77,
"rsi": 60.767,
"ret": -0.0098474 
},
{
 "date":   4745,
"name": "GSPC.Close",
"price": 141.24,
"rsi": 56.533,
"ret": 0.0033388 
},
{
 "date":   4746,
"name": "GSPC.Close",
"price": 140.33,
"rsi": 57.601,
"ret": -0.0064429 
},
{
 "date":   4747,
"name": "GSPC.Close",
"price": 140.64,
"rsi": 54.794,
"ret": 0.0022091 
},
{
 "date":   4750,
"name": "GSPC.Close",
"price": 138.34,
"rsi": 55.588,
"ret": -0.016354 
},
{
 "date":   4751,
"name": "GSPC.Close",
"price": 141.36,
"rsi": 48.746,
"ret": 0.02183 
},
{
 "date":   4752,
"name": "GSPC.Close",
"price": 141.96,
"rsi": 56.344,
"ret": 0.0042445 
},
{
 "date":   4753,
"name": "GSPC.Close",
"price": 145.27,
"rsi": 57.686,
"ret": 0.023316 
},
{
 "date":   4754,
"name": "GSPC.Close",
"price": 145.18,
"rsi": 64.221,
"ret": -0.00061954 
},
{
 "date":   4757,
"name": "GSPC.Close",
"price": 146.78,
"rsi": 63.931,
"ret": 0.011021 
},
{
 "date":   4758,
"name": "GSPC.Close",
"price": 145.78,
"rsi": 66.793,
"ret": -0.0068129 
},
{
 "date":   4759,
"name": "GSPC.Close",
"price": 146.69,
"rsi": 63.407,
"ret": 0.0062423 
},
{
 "date":   4760,
"name": "GSPC.Close",
"price": 145.73,
"rsi": 65.139,
"ret": -0.0065444 
},
{
 "date":   4761,
"name": "GSPC.Close",
"price": 146.65,
"rsi": 61.815,
"ret": 0.006313 
},
{
 "date":   4764,
"name": "GSPC.Close",
"price": 146.72,
"rsi": 63.725,
"ret": 0.00047733 
},
{
 "date":   4765,
"name": "GSPC.Close",
"price":  146.4,
"rsi": 63.874,
"ret": -0.002181 
},
{
 "date":   4766,
"name": "GSPC.Close",
"price": 145.27,
"rsi": 62.615,
"ret": -0.0077186 
},
{
 "date":   4767,
"name": "GSPC.Close",
"price": 146.29,
"rsi":  58.25,
"ret": 0.0070214 
},
{
 "date":   4768,
"name": "GSPC.Close",
"price": 143.85,
"rsi":   60.9,
"ret": -0.016679 
},
{
 "date":   4771,
"name": "GSPC.Close",
"price": 139.97,
"rsi": 52.342,
"ret": -0.026973 
},
{
 "date":   4772,
"name": "GSPC.Close",
"price": 141.75,
"rsi":  42.19,
"ret": 0.012717 
},
{
 "date":   4773,
"name": "GSPC.Close",
"price": 141.54,
"rsi": 47.245,
"ret": -0.0014815 
},
{
 "date":   4774,
"name": "GSPC.Close",
"price": 144.27,
"rsi": 46.726,
"ret": 0.019288 
},
{
 "date":   4775,
"name": "GSPC.Close",
"price": 144.51,
"rsi": 53.829,
"ret": 0.0016635 
},
{
 "date":   4778,
"name": "GSPC.Close",
"price":  145.3,
"rsi": 54.404,
"ret": 0.0054667 
},
{
 "date":   4779,
"name": "GSPC.Close",
"price": 142.96,
"rsi": 56.334,
"ret": -0.016105 
},
{
 "date":   4780,
"name": "GSPC.Close",
"price": 143.23,
"rsi": 49.634,
"ret": 0.0018886 
},
{
 "date":   4781,
"name": "GSPC.Close",
"price": 144.26,
"rsi": 50.367,
"ret": 0.0071912 
},
{
 "date":   4782,
"name": "GSPC.Close",
"price": 146.14,
"rsi": 53.169,
"ret": 0.013032 
},
{
 "date":   4785,
"name": "GSPC.Close",
"price": 146.93,
"rsi": 57.847,
"ret": 0.0054058 
},
{
 "date":   4786,
"name": "GSPC.Close",
"price":  145.7,
"rsi":  59.67,
"ret": -0.0083713 
},
{
 "date":   4787,
"name": "GSPC.Close",
"price":    145,
"rsi": 55.636,
"ret": -0.0048044 
},
{
 "date":   4788,
"name": "GSPC.Close",
"price":  147.5,
"rsi": 53.422,
"ret": 0.017241 
},
{
 "date":   4789,
"name": "GSPC.Close",
"price": 147.65,
"rsi": 59.604,
"ret": 0.0010169 
},
{
 "date":   4792,
"name": "GSPC.Close",
"price": 148.93,
"rsi": 59.947,
"ret": 0.0086692 
},
{
 "date":   4793,
"name": "GSPC.Close",
"price":  148.3,
"rsi":  62.85,
"ret": -0.0042302 
},
{
 "date":   4794,
"name": "GSPC.Close",
"price": 147.43,
"rsi": 60.525,
"ret": -0.0058665 
},
{
 "date":   4795,
"name": "GSPC.Close",
"price": 147.44,
"rsi": 57.369,
"ret": 6.7829e-05 
},
{
 "date":   4796,
"name": "GSPC.Close",
"price":    148,
"rsi": 57.396,
"ret": 0.0037982 
},
{
 "date":   4800,
"name": "GSPC.Close",
"price": 145.48,
"rsi": 58.992,
"ret": -0.017027 
},
{
 "date":   4801,
"name": "GSPC.Close",
"price": 146.79,
"rsi":  49.93,
"ret": 0.0090047 
},
{
 "date":   4802,
"name": "GSPC.Close",
"price":  149.6,
"rsi": 53.895,
"ret": 0.019143 
},
{
 "date":   4803,
"name": "GSPC.Close",
"price": 149.74,
"rsi": 61.024,
"ret": 0.00093583 
},
{
 "date":   4806,
"name": "GSPC.Close",
"price": 148.06,
"rsi": 61.345,
"ret": -0.011219 
},
{
 "date":   4807,
"name": "GSPC.Close",
"price": 150.88,
"rsi": 55.449,
"ret": 0.019046 
},
{
 "date":   4808,
"name": "GSPC.Close",
"price":  152.3,
"rsi": 62.044,
"ret": 0.0094115 
},
{
 "date":   4809,
"name": "GSPC.Close",
"price": 153.48,
"rsi": 64.864,
"ret": 0.0077479 
},
{
 "date":   4810,
"name": "GSPC.Close",
"price": 153.67,
"rsi": 67.055,
"ret": 0.0012379 
},
{
 "date":   4813,
"name": "GSPC.Close",
"price": 153.67,
"rsi": 67.407,
"ret":      0 
},
{
 "date":   4814,
"name": "GSPC.Close",
"price": 151.26,
"rsi": 67.407,
"ret": -0.015683 
},
{
 "date":   4815,
"name": "GSPC.Close",
"price": 152.87,
"rsi": 58.243,
"ret": 0.010644 
},
{
 "date":   4816,
"name": "GSPC.Close",
"price":  151.8,
"rsi": 61.963,
"ret": -0.0069994 
},
{
 "date":   4817,
"name": "GSPC.Close",
"price": 151.24,
"rsi": 58.249,
"ret": -0.0036891 
},
{
 "date":   4820,
"name": "GSPC.Close",
"price": 150.83,
"rsi": 56.345,
"ret": -0.0027109 
},
{
 "date":   4821,
"name": "GSPC.Close",
"price": 151.37,
"rsi": 54.929,
"ret": 0.0035802 
},
{
 "date":   4822,
"name": "GSPC.Close",
"price": 149.81,
"rsi":  56.48,
"ret": -0.010306 
},
{
 "date":   4823,
"name": "GSPC.Close",
"price": 149.59,
"rsi": 51.019,
"ret": -0.0014685 
},
{
 "date":   4824,
"name": "GSPC.Close",
"price":  149.9,
"rsi": 50.281,
"ret": 0.0020723 
},
{
 "date":   4827,
"name": "GSPC.Close",
"price": 151.19,
"rsi": 51.349,
"ret": 0.0086057 
},
{
 "date":   4828,
"name": "GSPC.Close",
"price": 150.66,
"rsi": 55.623,
"ret": -0.0035055 
},
{
 "date":   4829,
"name": "GSPC.Close",
"price": 152.81,
"rsi": 53.542,
"ret": 0.014271 
},
{
 "date":   4830,
"name": "GSPC.Close",
"price": 153.37,
"rsi": 60.068,
"ret": 0.0036647 
},
{
 "date":   4831,
"name": "GSPC.Close",
"price": 152.67,
"rsi": 61.582,
"ret": -0.0045641 
},
{
 "date":   4834,
"name": "GSPC.Close",
"price": 151.85,
"rsi": 58.592,
"ret": -0.0053711 
},
{
 "date":   4835,
"name": "GSPC.Close",
"price": 151.59,
"rsi":  55.21,
"ret": -0.0017122 
},
{
 "date":   4836,
"name": "GSPC.Close",
"price": 153.39,
"rsi": 54.143,
"ret": 0.011874 
},
{
 "date":   4837,
"name": "GSPC.Close",
"price": 152.96,
"rsi": 59.919,
"ret": -0.0028033 
},
{
 "date":   4841,
"name": "GSPC.Close",
"price": 153.02,
"rsi": 58.038,
"ret": 0.00039226 
},
{
 "date":   4842,
"name": "GSPC.Close",
"price":  151.9,
"rsi": 58.235,
"ret": -0.0073193 
},
{
 "date":   4843,
"name": "GSPC.Close",
"price": 151.04,
"rsi": 53.214,
"ret": -0.0056616 
},
{
 "date":   4844,
"name": "GSPC.Close",
"price": 151.76,
"rsi": 49.672,
"ret": 0.0047669 
},
{
 "date":   4845,
"name": "GSPC.Close",
"price": 152.85,
"rsi": 52.521,
"ret": 0.0071824 
},
{
 "date":   4848,
"name": "GSPC.Close",
"price": 155.14,
"rsi": 56.533,
"ret": 0.014982 
},
{
 "date":   4849,
"name": "GSPC.Close",
"price": 155.82,
"rsi": 63.509,
"ret": 0.0043831 
},
{
 "date":   4850,
"name": "GSPC.Close",
"price": 156.77,
"rsi": 65.291,
"ret": 0.0060968 
},
{
 "date":   4851,
"name": "GSPC.Close",
"price": 158.12,
"rsi": 67.666,
"ret": 0.0086113 
},
{
 "date":   4852,
"name": "GSPC.Close",
"price": 158.75,
"rsi": 70.731,
"ret": 0.0039843 
},
{
 "date":   4855,
"name": "GSPC.Close",
"price": 159.74,
"rsi": 72.062,
"ret": 0.0062362 
},
{
 "date":   4856,
"name": "GSPC.Close",
"price": 158.71,
"rsi": 74.058,
"ret": -0.006448 
},
{
 "date":   4857,
"name": "GSPC.Close",
"price": 160.71,
"rsi": 68.568,
"ret": 0.012602 
},
{
 "date":   4858,
"name": "GSPC.Close",
"price": 160.05,
"rsi": 72.787,
"ret": -0.0041068 
},
{
 "date":   4859,
"name": "GSPC.Close",
"price": 160.42,
"rsi": 69.473,
"ret": 0.0023118 
},
{
 "date":   4862,
"name": "GSPC.Close",
"price": 158.81,
"rsi":  70.29,
"ret": -0.010036 
},
{
 "date":   4863,
"name": "GSPC.Close",
"price": 161.81,
"rsi": 62.461,
"ret": 0.01889 
},
{
 "date":   4864,
"name": "GSPC.Close",
"price": 161.44,
"rsi": 69.318,
"ret": -0.0022866 
},
{
 "date":   4865,
"name": "GSPC.Close",
"price": 162.95,
"rsi": 67.676,
"ret": 0.0093533 
},
{
 "date":   4866,
"name": "GSPC.Close",
"price": 164.43,
"rsi": 70.724,
"ret": 0.0090825 
},
{
 "date":   4869,
"name": "GSPC.Close",
"price": 162.11,
"rsi": 73.374,
"ret": -0.014109 
},
{
 "date":   4870,
"name": "GSPC.Close",
"price": 162.34,
"rsi": 63.648,
"ret": 0.0014188 
},
{
 "date":   4871,
"name": "GSPC.Close",
"price": 163.31,
"rsi": 64.155,
"ret": 0.0059751 
},
{
 "date":   4872,
"name": "GSPC.Close",
"price": 164.28,
"rsi": 66.292,
"ret": 0.0059396 
},
{
 "date":   4873,
"name": "GSPC.Close",
"price":  166.1,
"rsi": 68.325,
"ret": 0.011079 
},
{
 "date":   4876,
"name": "GSPC.Close",
"price": 165.81,
"rsi": 71.766,
"ret": -0.0017459 
},
{
 "date":   4877,
"name": "GSPC.Close",
"price": 165.95,
"rsi": 70.453,
"ret": 0.00084434 
},
{
 "date":   4878,
"name": "GSPC.Close",
"price": 164.96,
"rsi": 70.731,
"ret": -0.0059657 
},
{
 "date":   4879,
"name": "GSPC.Close",
"price": 164.25,
"rsi": 65.995,
"ret": -0.0043041 
},
{
 "date":   4880,
"name": "GSPC.Close",
"price": 164.91,
"rsi": 62.749,
"ret": 0.0040183 
},
{
 "date":   4883,
"name": "GSPC.Close",
"price":  163.4,
"rsi": 64.497,
"ret": -0.0091565 
},
{
 "date":   4884,
"name": "GSPC.Close",
"price": 163.71,
"rsi": 57.813,
"ret": 0.0018972 
},
{
 "date":   4885,
"name": "GSPC.Close",
"price": 163.27,
"rsi": 58.758,
"ret": -0.0026877 
},
{
 "date":   4886,
"name": "GSPC.Close",
"price": 161.99,
"rsi": 56.813,
"ret": -0.0078398 
},
{
 "date":   4887,
"name": "GSPC.Close",
"price": 162.14,
"rsi": 51.475,
"ret": 0.00092598 
},
{
 "date":   4890,
"name": "GSPC.Close",
"price": 163.43,
"rsi": 52.044,
"ret": 0.0079561 
},
{
 "date":   4891,
"name": "GSPC.Close",
"price": 165.54,
"rsi": 56.739,
"ret": 0.012911 
},
{
 "date":   4892,
"name": "GSPC.Close",
"price": 166.21,
"rsi": 63.103,
"ret": 0.0040474 
},
{
 "date":   4893,
"name": "GSPC.Close",
"price": 165.48,
"rsi":  64.87,
"ret": -0.004392 
},
{
 "date":   4894,
"name": "GSPC.Close",
"price": 164.46,
"rsi": 61.418,
"ret": -0.0061639 
},
{
 "date":   4898,
"name": "GSPC.Close",
"price": 162.39,
"rsi": 56.866,
"ret": -0.012587 
},
{
 "date":   4899,
"name": "GSPC.Close",
"price": 162.55,
"rsi": 48.938,
"ret": 0.00098528 
},
{
 "date":   4900,
"name": "GSPC.Close",
"price": 163.98,
"rsi": 49.523,
"ret": 0.0087973 
},
{
 "date":   4901,
"name": "GSPC.Close",
"price": 164.42,
"rsi": 54.543,
"ret": 0.0026833 
},
{
 "date":   4904,
"name": "GSPC.Close",
"price": 164.83,
"rsi": 55.993,
"ret": 0.0024936 
},
{
 "date":   4905,
"name": "GSPC.Close",
"price": 162.77,
"rsi": 57.358,
"ret": -0.012498 
},
{
 "date":   4906,
"name": "GSPC.Close",
"price": 161.36,
"rsi": 49.115,
"ret": -0.0086625 
},
{
 "date":   4907,
"name": "GSPC.Close",
"price": 161.83,
"rsi":  44.41,
"ret": 0.0029127 
},
{
 "date":   4908,
"name": "GSPC.Close",
"price": 162.68,
"rsi": 46.258,
"ret": 0.0052524 
},
{
 "date":   4911,
"name": "GSPC.Close",
"price": 164.84,
"rsi": 49.526,
"ret": 0.013278 
},
{
 "date":   4912,
"name": "GSPC.Close",
"price": 165.53,
"rsi": 56.727,
"ret": 0.0041859 
},
{
 "date":   4913,
"name": "GSPC.Close",
"price": 167.12,
"rsi": 58.751,
"ret": 0.0096055 
},
{
 "date":   4914,
"name": "GSPC.Close",
"price": 169.14,
"rsi": 63.042,
"ret": 0.012087 
},
{
 "date":   4915,
"name": "GSPC.Close",
"price": 169.13,
"rsi": 67.646,
"ret": -5.9123e-05 
},
{
 "date":   4918,
"name": "GSPC.Close",
"price": 169.02,
"rsi": 67.601,
"ret": -0.00065039 
},
{
 "date":   4919,
"name": "GSPC.Close",
"price": 170.53,
"rsi": 67.074,
"ret": 0.0089339 
},
{
 "date":   4920,
"name": "GSPC.Close",
"price": 170.99,
"rsi": 70.479,
"ret": 0.0026975 
},
{
 "date":   4921,
"name": "GSPC.Close",
"price": 170.57,
"rsi": 71.448,
"ret": -0.0024563 
},
{
 "date":   4922,
"name": "GSPC.Close",
"price": 170.41,
"rsi": 69.214,
"ret": -0.00093803 
},
{
 "date":   4925,
"name": "GSPC.Close",
"price": 168.46,
"rsi": 68.338,
"ret": -0.011443 
},
{
 "date":   4926,
"name": "GSPC.Close",
"price": 165.68,
"rsi": 58.601,
"ret": -0.016502 
},
{
 "date":   4927,
"name": "GSPC.Close",
"price": 166.64,
"rsi": 48.082,
"ret": 0.0057943 
},
{
 "date":   4928,
"name": "GSPC.Close",
"price": 167.64,
"rsi": 51.331,
"ret": 0.006001 
},
{
 "date":   4929,
"name": "GSPC.Close",
"price": 168.64,
"rsi": 54.523,
"ret": 0.0059652 
},
{
 "date":   4933,
"name": "GSPC.Close",
"price":  166.6,
"rsi": 57.524,
"ret": -0.012097 
},
{
 "date":   4934,
"name": "GSPC.Close",
"price": 168.48,
"rsi": 50.241,
"ret": 0.011285 
},
{
 "date":   4935,
"name": "GSPC.Close",
"price": 167.56,
"rsi": 55.795,
"ret": -0.0054606 
},
{
 "date":   4936,
"name": "GSPC.Close",
"price": 167.08,
"rsi": 52.696,
"ret": -0.0028646 
},
{
 "date":   4939,
"name": "GSPC.Close",
"price": 168.11,
"rsi": 51.101,
"ret": 0.0061647 
},
{
 "date":   4940,
"name": "GSPC.Close",
"price": 165.53,
"rsi": 54.297,
"ret": -0.015347 
},
{
 "date":   4941,
"name": "GSPC.Close",
"price": 165.46,
"rsi": 46.157,
"ret": -0.00042288 
},
{
 "date":   4942,
"name": "GSPC.Close",
"price": 166.01,
"rsi": 45.956,
"ret": 0.0033241 
},
{
 "date":   4943,
"name": "GSPC.Close",
"price": 164.29,
"rsi": 47.879,
"ret": -0.010361 
},
{
 "date":   4946,
"name": "GSPC.Close",
"price": 163.95,
"rsi": 42.755,
"ret": -0.0020695 
},
{
 "date":   4947,
"name": "GSPC.Close",
"price": 164.82,
"rsi": 41.802,
"ret": 0.0053065 
},
{
 "date":   4948,
"name": "GSPC.Close",
"price": 169.29,
"rsi": 45.168,
"ret": 0.02712 
},
{
 "date":   4949,
"name": "GSPC.Close",
"price": 169.06,
"rsi": 58.462,
"ret": -0.0013586 
},
{
 "date":   4950,
"name": "GSPC.Close",
"price": 168.89,
"rsi": 57.687,
"ret": -0.0010056 
},
{
 "date":   4953,
"name": "GSPC.Close",
"price": 169.53,
"rsi": 57.085,
"ret": 0.0037894 
},
{
 "date":   4954,
"name": "GSPC.Close",
"price": 170.53,
"rsi": 58.827,
"ret": 0.0058987 
},
{
 "date":   4955,
"name": "GSPC.Close",
"price": 167.59,
"rsi": 61.461,
"ret": -0.01724 
},
{
 "date":   4956,
"name": "GSPC.Close",
"price": 165.04,
"rsi":  51.11,
"ret": -0.015216 
},
{
 "date":   4957,
"name": "GSPC.Close",
"price": 162.56,
"rsi": 44.162,
"ret": -0.015027 
},
{
 "date":   4960,
"name": "GSPC.Close",
"price": 162.04,
"rsi": 38.658,
"ret": -0.0031988 
},
{
 "date":   4961,
"name": "GSPC.Close",
"price": 162.01,
"rsi":   37.6,
"ret": -0.00018514 
},
{
 "date":   4962,
"name": "GSPC.Close",
"price": 163.44,
"rsi": 37.536,
"ret": 0.0088266 
},
{
 "date":   4963,
"name": "GSPC.Close",
"price": 161.33,
"rsi": 42.544,
"ret": -0.01291 
},
{
 "date":   4964,
"name": "GSPC.Close",
"price": 161.74,
"rsi": 37.737,
"ret": 0.0025414 
},
{
 "date":   4967,
"name": "GSPC.Close",
"price": 159.18,
"rsi": 39.175,
"ret": -0.015828 
},
{
 "date":   4968,
"name": "GSPC.Close",
"price": 160.13,
"rsi": 33.908,
"ret": 0.0059681 
},
{
 "date":   4969,
"name": "GSPC.Close",
"price": 161.54,
"rsi": 37.278,
"ret": 0.0088053 
},
{
 "date":   4970,
"name": "GSPC.Close",
"price": 161.54,
"rsi": 42.004,
"ret":      0 
},
{
 "date":   4971,
"name": "GSPC.Close",
"price": 162.16,
"rsi": 42.004,
"ret": 0.0038381 
},
{
 "date":   4974,
"name": "GSPC.Close",
"price":  163.7,
"rsi": 44.151,
"ret": 0.0094968 
},
{
 "date":   4975,
"name": "GSPC.Close",
"price": 163.41,
"rsi": 49.181,
"ret": -0.0017715 
},
{
 "date":   4976,
"name": "GSPC.Close",
"price": 165.29,
"rsi": 48.299,
"ret": 0.011505 
},
{
 "date":   4977,
"name": "GSPC.Close",
"price": 163.55,
"rsi": 54.053,
"ret": -0.010527 
},
{
 "date":   4978,
"name": "GSPC.Close",
"price": 163.98,
"rsi": 48.656,
"ret": 0.0026292 
},
{
 "date":   4981,
"name": "GSPC.Close",
"price": 164.34,
"rsi": 49.985,
"ret": 0.0021954 
},
{
 "date":   4982,
"name": "GSPC.Close",
"price": 162.77,
"rsi": 51.126,
"ret": -0.0095534 
},
{
 "date":   4983,
"name": "GSPC.Close",
"price": 161.25,
"rsi": 46.179,
"ret": -0.0093383 
},
{
 "date":   4984,
"name": "GSPC.Close",
"price": 160.84,
"rsi": 41.947,
"ret": -0.0025426 
},
{
 "date":   4985,
"name": "GSPC.Close",
"price": 162.14,
"rsi":  40.86,
"ret": 0.0080826 
},
{
 "date":   4988,
"name": "GSPC.Close",
"price": 162.25,
"rsi":  45.67,
"ret": 0.00067843 
},
{
 "date":   4989,
"name": "GSPC.Close",
"price": 162.58,
"rsi":  46.07,
"ret": 0.0020339 
},
{
 "date":   4990,
"name": "GSPC.Close",
"price":  164.4,
"rsi": 47.322,
"ret": 0.011194 
},
{
 "date":   4991,
"name": "GSPC.Close",
"price": 164.23,
"rsi": 53.706,
"ret": -0.0010341 
},
{
 "date":   4992,
"name": "GSPC.Close",
"price":    165,
"rsi": 53.059,
"ret": 0.0046885 
},
{
 "date":   4996,
"name": "GSPC.Close",
"price": 167.89,
"rsi": 55.663,
"ret": 0.017515 
},
{
 "date":   4997,
"name": "GSPC.Close",
"price": 167.96,
"rsi": 63.785,
"ret": 0.00041694 
},
{
 "date":   4998,
"name": "GSPC.Close",
"price": 167.77,
"rsi": 63.958,
"ret": -0.0011312 
},
{
 "date":   4999,
"name": "GSPC.Close",
"price": 166.92,
"rsi": 63.081,
"ret": -0.0050665 
},
{
 "date":   5002,
"name": "GSPC.Close",
"price": 165.48,
"rsi": 59.172,
"ret": -0.0086269 
},
{
 "date":   5003,
"name": "GSPC.Close",
"price":  164.8,
"rsi": 53.162,
"ret": -0.0041093 
},
{
 "date":   5004,
"name": "GSPC.Close",
"price": 165.35,
"rsi": 50.551,
"ret": 0.0033374 
},
{
 "date":   5005,
"name": "GSPC.Close",
"price": 164.38,
"rsi":  52.58,
"ret": -0.0058663 
},
{
 "date":   5006,
"name": "GSPC.Close",
"price": 166.25,
"rsi": 48.779,
"ret": 0.011376 
},
{
 "date":   5009,
"name": "GSPC.Close",
"price": 167.62,
"rsi": 55.463,
"ret": 0.0082406 
},
{
 "date":   5010,
"name": "GSPC.Close",
"price": 169.24,
"rsi":  59.62,
"ret": 0.0096647 
},
{
 "date":   5011,
"name": "GSPC.Close",
"price": 168.41,
"rsi":  63.91,
"ret": -0.0049043 
},
{
 "date":   5012,
"name": "GSPC.Close",
"price": 169.76,
"rsi": 60.371,
"ret": 0.0080162 
},
{
 "date":   5013,
"name": "GSPC.Close",
"price": 169.51,
"rsi": 63.875,
"ret": -0.0014727 
},
{
 "date":   5016,
"name": "GSPC.Close",
"price": 170.07,
"rsi": 62.768,
"ret": 0.0033036 
},
{
 "date":   5017,
"name": "GSPC.Close",
"price": 168.43,
"rsi": 64.262,
"ret": -0.0096431 
},
{
 "date":   5018,
"name": "GSPC.Close",
"price":    168,
"rsi": 57.044,
"ret": -0.002553 
},
{
 "date":   5019,
"name": "GSPC.Close",
"price": 167.23,
"rsi":  55.29,
"ret": -0.0045833 
},
{
 "date":   5020,
"name": "GSPC.Close",
"price": 166.07,
"rsi": 52.196,
"ret": -0.0069366 
},
{
 "date":   5023,
"name": "GSPC.Close",
"price": 165.81,
"rsi": 47.851,
"ret": -0.0015656 
},
{
 "date":   5024,
"name": "GSPC.Close",
"price": 166.27,
"rsi": 46.909,
"ret": 0.0027743 
},
{
 "date":   5025,
"name": "GSPC.Close",
"price": 167.74,
"rsi": 48.829,
"ret": 0.008841 
},
{
 "date":   5026,
"name": "GSPC.Close",
"price": 170.28,
"rsi": 54.494,
"ret": 0.015142 
},
{
 "date":   5027,
"name": "GSPC.Close",
"price":  170.8,
"rsi": 62.267,
"ret": 0.0030538 
},
{
 "date":   5030,
"name": "GSPC.Close",
"price": 172.65,
"rsi": 63.636,
"ret": 0.010831 
},
{
 "date":   5031,
"name": "GSPC.Close",
"price": 170.34,
"rsi": 68.075,
"ret": -0.01338 
},
{
 "date":   5032,
"name": "GSPC.Close",
"price": 169.62,
"rsi": 58.476,
"ret": -0.0042268 
},
{
 "date":   5033,
"name": "GSPC.Close",
"price": 169.87,
"rsi": 55.833,
"ret": 0.0014739 
},
{
 "date":   5034,
"name": "GSPC.Close",
"price": 169.86,
"rsi": 56.567,
"ret": -5.8869e-05 
},
{
 "date":   5037,
"name": "GSPC.Close",
"price": 170.43,
"rsi": 56.527,
"ret": 0.0033557 
},
{
 "date":   5038,
"name": "GSPC.Close",
"price": 167.81,
"rsi": 58.356,
"ret": -0.015373 
},
{
 "date":   5039,
"name": "GSPC.Close",
"price": 166.73,
"rsi": 48.299,
"ret": -0.0064359 
},
{
 "date":   5040,
"name": "GSPC.Close",
"price": 166.98,
"rsi": 44.867,
"ret": 0.0014994 
},
{
 "date":   5041,
"name": "GSPC.Close",
"price": 165.95,
"rsi": 45.826,
"ret": -0.0061684 
},
{
 "date":   5044,
"name": "GSPC.Close",
"price": 165.99,
"rsi": 42.541,
"ret": 0.00024104 
},
{
 "date":   5045,
"name": "GSPC.Close",
"price": 166.47,
"rsi": 42.712,
"ret": 0.0028917 
},
{
 "date":   5046,
"name": "GSPC.Close",
"price": 165.38,
"rsi": 44.843,
"ret": -0.0065477 
},
{
 "date":   5047,
"name": "GSPC.Close",
"price": 164.84,
"rsi": 41.104,
"ret": -0.0032652 
},
{
 "date":   5048,
"name": "GSPC.Close",
"price": 163.37,
"rsi": 39.354,
"ret": -0.0089177 
},
{
 "date":   5051,
"name": "GSPC.Close",
"price": 163.55,
"rsi": 34.985,
"ret": 0.0011018 
},
{
 "date":   5052,
"name": "GSPC.Close",
"price": 163.66,
"rsi": 35.923,
"ret": 0.00067258 
},
{
 "date":   5053,
"name": "GSPC.Close",
"price": 164.84,
"rsi": 36.526,
"ret": 0.0072101 
},
{
 "date":   5054,
"name": "GSPC.Close",
"price": 163.45,
"rsi": 42.746,
"ret": -0.0084324 
},
{
 "date":   5055,
"name": "GSPC.Close",
"price": 162.44,
"rsi":  38.02,
"ret": -0.0061793 
},
{
 "date":   5058,
"name": "GSPC.Close",
"price": 161.91,
"rsi": 34.992,
"ret": -0.0032627 
},
{
 "date":   5059,
"name": "GSPC.Close",
"price": 161.76,
"rsi": 33.485,
"ret": -0.00092644 
},
{
 "date":   5060,
"name": "GSPC.Close",
"price": 163.97,
"rsi": 33.051,
"ret": 0.013662 
},
{
 "date":   5061,
"name": "GSPC.Close",
"price": 164.41,
"rsi": 44.467,
"ret": 0.0026834 
},
{
 "date":   5062,
"name": "GSPC.Close",
"price": 166.29,
"rsi": 46.426,
"ret": 0.011435 
},
{
 "date":   5065,
"name": "GSPC.Close",
"price": 166.58,
"rsi": 53.907,
"ret": 0.0017439 
},
{
 "date":   5066,
"name": "GSPC.Close",
"price": 165.36,
"rsi": 54.951,
"ret": -0.0073238 
},
{
 "date":   5067,
"name": "GSPC.Close",
"price": 166.08,
"rsi": 49.833,
"ret": 0.0043541 
},
{
 "date":   5068,
"name": "GSPC.Close",
"price": 166.13,
"rsi": 52.637,
"ret": 0.00030106 
},
{
 "date":   5069,
"name": "GSPC.Close",
"price": 165.09,
"rsi": 52.834,
"ret": -0.0062602 
},
{
 "date":   5072,
"name": "GSPC.Close",
"price": 166.05,
"rsi": 48.328,
"ret": 0.005815 
},
{
 "date":   5073,
"name": "GSPC.Close",
"price": 166.84,
"rsi": 52.367,
"ret": 0.0047576 
},
{
 "date":   5074,
"name": "GSPC.Close",
"price": 166.96,
"rsi": 55.452,
"ret": 0.00071925 
},
{
 "date":   5076,
"name": "GSPC.Close",
"price": 167.18,
"rsi": 55.919,
"ret": 0.0013177 
},
{
 "date":   5079,
"name": "GSPC.Close",
"price": 166.54,
"rsi": 56.813,
"ret": -0.0038282 
},
{
 "date":   5080,
"name": "GSPC.Close",
"price": 167.91,
"rsi": 53.419,
"ret": 0.0082263 
},
{
 "date":   5081,
"name": "GSPC.Close",
"price":  166.4,
"rsi": 59.058,
"ret": -0.0089929 
},
{
 "date":   5082,
"name": "GSPC.Close",
"price": 166.49,
"rsi": 51.638,
"ret": 0.00054087 
},
{
 "date":   5083,
"name": "GSPC.Close",
"price": 165.44,
"rsi": 52.025,
"ret": -0.0063067 
},
{
 "date":   5086,
"name": "GSPC.Close",
"price": 165.76,
"rsi": 47.274,
"ret": 0.0019342 
},
{
 "date":   5087,
"name": "GSPC.Close",
"price": 165.47,
"rsi": 48.808,
"ret": -0.0017495 
},
{
 "date":   5088,
"name": "GSPC.Close",
"price": 165.91,
"rsi":  47.46,
"ret": 0.0026591 
},
{
 "date":   5089,
"name": "GSPC.Close",
"price":  165.2,
"rsi": 49.729,
"ret": -0.0042794 
},
{
 "date":   5090,
"name": "GSPC.Close",
"price": 165.08,
"rsi": 46.258,
"ret": -0.00072639 
},
{
 "date":   5093,
"name": "GSPC.Close",
"price": 165.62,
"rsi": 45.677,
"ret": 0.0032711 
},
{
 "date":   5094,
"name": "GSPC.Close",
"price": 164.93,
"rsi": 48.791,
"ret": -0.0041662 
},
{
 "date":   5095,
"name": "GSPC.Close",
"price": 163.33,
"rsi": 45.224,
"ret": -0.0097011 
},
{
 "date":   5096,
"name": "GSPC.Close",
"price": 161.66,
"rsi": 38.243,
"ret": -0.010225 
},
{
 "date":   5097,
"name": "GSPC.Close",
"price": 162.39,
"rsi": 32.589,
"ret": 0.0045157 
},
{
 "date":   5100,
"name": "GSPC.Close",
"price": 162.32,
"rsi": 36.976,
"ret": -0.00043106 
},
{
 "date":   5101,
"name": "GSPC.Close",
"price":    162,
"rsi": 36.729,
"ret": -0.0019714 
},
{
 "date":   5102,
"name": "GSPC.Close",
"price": 163.56,
"rsi":  35.56,
"ret": 0.0096296 
},
{
 "date":   5103,
"name": "GSPC.Close",
"price": 163.53,
"rsi": 44.783,
"ret": -0.00018342 
},
{
 "date":   5104,
"name": "GSPC.Close",
"price": 163.22,
"rsi": 44.651,
"ret": -0.0018957 
},
{
 "date":   5108,
"name": "GSPC.Close",
"price": 164.76,
"rsi": 43.229,
"ret": 0.0094351 
},
{
 "date":   5109,
"name": "GSPC.Close",
"price": 165.34,
"rsi": 51.492,
"ret": 0.0035203 
},
{
 "date":   5110,
"name": "GSPC.Close",
"price": 164.86,
"rsi": 54.196,
"ret": -0.0029031 
},
{
 "date":   5111,
"name": "GSPC.Close",
"price": 164.93,
"rsi": 51.631,
"ret": 0.0004246 
},
{
 "date":   5115,
"name": "GSPC.Close",
"price": 164.04,
"rsi": 51.988,
"ret": -0.0053962 
},
{
 "date":   5116,
"name": "GSPC.Close",
"price": 166.78,
"rsi": 47.218,
"ret": 0.016703 
},
{
 "date":   5117,
"name": "GSPC.Close",
"price": 168.81,
"rsi":  59.53,
"ret": 0.012172 
},
{
 "date":   5118,
"name": "GSPC.Close",
"price": 169.28,
"rsi":  65.88,
"ret": 0.0027842 
},
{
 "date":   5121,
"name": "GSPC.Close",
"price":  168.9,
"rsi": 67.164,
"ret": -0.0022448 
},
{
 "date":   5122,
"name": "GSPC.Close",
"price": 167.95,
"rsi": 65.033,
"ret": -0.0056246 
},
{
 "date":   5123,
"name": "GSPC.Close",
"price":  167.8,
"rsi": 59.913,
"ret": -0.00089312 
},
{
 "date":   5124,
"name": "GSPC.Close",
"price": 167.75,
"rsi": 59.121,
"ret": -0.00029797 
},
{
 "date":   5125,
"name": "GSPC.Close",
"price": 167.02,
"rsi": 58.842,
"ret": -0.0043517 
},
{
 "date":   5128,
"name": "GSPC.Close",
"price": 167.18,
"rsi": 54.777,
"ret": 0.00095797 
},
{
 "date":   5129,
"name": "GSPC.Close",
"price": 167.83,
"rsi": 55.503,
"ret": 0.003888 
},
{
 "date":   5130,
"name": "GSPC.Close",
"price": 167.55,
"rsi": 58.421,
"ret": -0.0016684 
},
{
 "date":   5131,
"name": "GSPC.Close",
"price": 167.04,
"rsi": 56.696,
"ret": -0.0030439 
},
{
 "date":   5132,
"name": "GSPC.Close",
"price": 166.21,
"rsi": 53.592,
"ret": -0.0049689 
},
{
 "date":   5135,
"name": "GSPC.Close",
"price": 164.87,
"rsi":   48.9,
"ret": -0.0080621 
},
{
 "date":   5136,
"name": "GSPC.Close",
"price": 165.94,
"rsi": 42.439,
"ret": 0.00649 
},
{
 "date":   5137,
"name": "GSPC.Close",
"price": 164.84,
"rsi": 48.311,
"ret": -0.0066289 
},
{
 "date":   5138,
"name": "GSPC.Close",
"price": 164.24,
"rsi": 43.408,
"ret": -0.0036399 
},
{
 "date":   5139,
"name": "GSPC.Close",
"price": 163.94,
"rsi": 40.966,
"ret": -0.0018266 
},
{
 "date":   5142,
"name": "GSPC.Close",
"price": 162.87,
"rsi": 39.762,
"ret": -0.0065268 
},
{
 "date":   5143,
"name": "GSPC.Close",
"price": 163.41,
"rsi": 35.727,
"ret": 0.0033155 
},
{
 "date":   5144,
"name": "GSPC.Close",
"price": 162.74,
"rsi": 39.086,
"ret": -0.0041001 
},
{
 "date":   5145,
"name": "GSPC.Close",
"price": 163.36,
"rsi": 36.535,
"ret": 0.0038098 
},
{
 "date":   5146,
"name": "GSPC.Close",
"price": 160.91,
"rsi": 40.411,
"ret": -0.014998 
},
{
 "date":   5149,
"name": "GSPC.Close",
"price": 158.08,
"rsi": 32.074,
"ret": -0.017587 
},
{
 "date":   5150,
"name": "GSPC.Close",
"price": 158.74,
"rsi": 25.523,
"ret": 0.0041751 
},
{
 "date":   5151,
"name": "GSPC.Close",
"price": 155.85,
"rsi": 29.157,
"ret": -0.018206 
},
{
 "date":   5152,
"name": "GSPC.Close",
"price": 155.42,
"rsi": 23.703,
"ret": -0.0027591 
},
{
 "date":   5153,
"name": "GSPC.Close",
"price":  156.3,
"rsi": 23.014,
"ret": 0.0056621 
},
{
 "date":   5156,
"name": "GSPC.Close",
"price": 154.95,
"rsi": 27.653,
"ret": -0.0086372 
},
{
 "date":   5157,
"name": "GSPC.Close",
"price": 156.61,
"rsi": 25.149,
"ret": 0.010713 
},
{
 "date":   5158,
"name": "GSPC.Close",
"price": 156.25,
"rsi": 33.164,
"ret": -0.0022987 
},
{
 "date":   5159,
"name": "GSPC.Close",
"price": 156.13,
"rsi": 32.355,
"ret": -0.000768 
},
{
 "date":   5160,
"name": "GSPC.Close",
"price": 155.74,
"rsi": 32.074,
"ret": -0.0024979 
},
{
 "date":   5164,
"name": "GSPC.Close",
"price": 154.64,
"rsi": 31.128,
"ret": -0.0070631 
},
{
 "date":   5165,
"name": "GSPC.Close",
"price": 154.31,
"rsi": 28.569,
"ret": -0.002134 
},
{
 "date":   5166,
"name": "GSPC.Close",
"price": 154.29,
"rsi":  27.83,
"ret": -0.00012961 
},
{
 "date":   5167,
"name": "GSPC.Close",
"price": 157.51,
"rsi": 27.783,
"ret": 0.02087 
},
{
 "date":   5170,
"name": "GSPC.Close",
"price":  159.3,
"rsi": 44.117,
"ret": 0.011364 
},
{
 "date":   5171,
"name": "GSPC.Close",
"price": 156.82,
"rsi": 50.782,
"ret": -0.015568 
},
{
 "date":   5172,
"name": "GSPC.Close",
"price": 157.06,
"rsi": 43.111,
"ret": 0.0015304 
},
{
 "date":   5173,
"name": "GSPC.Close",
"price": 158.19,
"rsi": 43.992,
"ret": 0.0071947 
},
{
 "date":   5174,
"name": "GSPC.Close",
"price": 159.24,
"rsi": 48.073,
"ret": 0.0066376 
},
{
 "date":   5177,
"name": "GSPC.Close",
"price": 157.89,
"rsi": 51.602,
"ret": -0.0084778 
},
{
 "date":   5178,
"name": "GSPC.Close",
"price": 156.25,
"rsi": 47.164,
"ret": -0.010387 
},
{
 "date":   5179,
"name": "GSPC.Close",
"price": 154.57,
"rsi": 42.394,
"ret": -0.010752 
},
{
 "date":   5180,
"name": "GSPC.Close",
"price": 155.19,
"rsi": 38.139,
"ret": 0.0040111 
},
{
 "date":   5181,
"name": "GSPC.Close",
"price": 154.35,
"rsi": 40.512,
"ret": -0.0054127 
},
{
 "date":   5184,
"name": "GSPC.Close",
"price": 156.34,
"rsi": 38.365,
"ret": 0.012893 
},
{
 "date":   5185,
"name": "GSPC.Close",
"price": 156.78,
"rsi": 45.707,
"ret": 0.0028144 
},
{
 "date":   5186,
"name": "GSPC.Close",
"price": 156.77,
"rsi": 47.204,
"ret": -6.3784e-05 
},
{
 "date":   5187,
"name": "GSPC.Close",
"price": 157.41,
"rsi": 47.172,
"ret": 0.0040824 
},
{
 "date":   5188,
"name": "GSPC.Close",
"price": 159.27,
"rsi":  49.52,
"ret": 0.011816 
},
{
 "date":   5191,
"name": "GSPC.Close",
"price": 157.78,
"rsi": 55.683,
"ret": -0.0093552 
},
{
 "date":   5192,
"name": "GSPC.Close",
"price": 158.86,
"rsi": 50.377,
"ret": 0.006845 
},
{
 "date":   5193,
"name": "GSPC.Close",
"price": 158.66,
"rsi": 53.812,
"ret": -0.001259 
},
{
 "date":   5194,
"name": "GSPC.Close",
"price": 156.69,
"rsi": 53.079,
"ret": -0.012416 
},
{
 "date":   5195,
"name": "GSPC.Close",
"price": 156.86,
"rsi": 46.379,
"ret": 0.0010849 
},
{
 "date":   5198,
"name": "GSPC.Close",
"price": 156.67,
"rsi": 47.001,
"ret": -0.0012113 
},
{
 "date":   5199,
"name": "GSPC.Close",
"price":  157.3,
"rsi": 46.354,
"ret": 0.0040212 
},
{
 "date":   5200,
"name": "GSPC.Close",
"price": 159.88,
"rsi": 48.867,
"ret": 0.016402 
},
{
 "date":   5201,
"name": "GSPC.Close",
"price": 159.52,
"rsi": 57.622,
"ret": -0.0022517 
},
{
 "date":   5202,
"name": "GSPC.Close",
"price": 159.18,
"rsi": 56.177,
"ret": -0.0021314 
},
{
 "date":   5205,
"name": "GSPC.Close",
"price": 157.98,
"rsi": 54.779,
"ret": -0.0075386 
},
{
 "date":   5206,
"name": "GSPC.Close",
"price": 157.66,
"rsi": 50.047,
"ret": -0.0020256 
},
{
 "date":   5207,
"name": "GSPC.Close",
"price": 157.54,
"rsi": 48.835,
"ret": -0.00076113 
},
{
 "date":   5208,
"name": "GSPC.Close",
"price": 155.04,
"rsi": 48.363,
"ret": -0.015869 
},
{
 "date":   5209,
"name": "GSPC.Close",
"price": 155.48,
"rsi": 39.732,
"ret": 0.002838 
},
{
 "date":   5212,
"name": "GSPC.Close",
"price": 155.45,
"rsi": 41.704,
"ret": -0.00019295 
},
{
 "date":   5213,
"name": "GSPC.Close",
"price": 155.87,
"rsi": 41.604,
"ret": 0.0027018 
},
{
 "date":   5214,
"name": "GSPC.Close",
"price":    155,
"rsi":  43.64,
"ret": -0.0055816 
},
{
 "date":   5215,
"name": "GSPC.Close",
"price": 157.73,
"rsi":  40.49,
"ret": 0.017613 
},
{
 "date":   5216,
"name": "GSPC.Close",
"price": 157.31,
"rsi": 52.159,
"ret": -0.0026628 
},
{
 "date":   5219,
"name": "GSPC.Close",
"price": 158.32,
"rsi": 50.518,
"ret": 0.0064204 
},
{
 "date":   5220,
"name": "GSPC.Close",
"price": 158.97,
"rsi": 54.247,
"ret": 0.0041056 
},
{
 "date":   5221,
"name": "GSPC.Close",
"price":  157.9,
"rsi": 56.517,
"ret": -0.0067308 
},
{
 "date":   5222,
"name": "GSPC.Close",
"price": 158.02,
"rsi": 51.947,
"ret": 0.00075997 
},
{
 "date":   5226,
"name": "GSPC.Close",
"price":  156.8,
"rsi": 52.412,
"ret": -0.0077205 
},
{
 "date":   5227,
"name": "GSPC.Close",
"price": 158.07,
"rsi": 47.393,
"ret": 0.0080995 
},
{
 "date":   5228,
"name": "GSPC.Close",
"price": 158.65,
"rsi": 52.493,
"ret": 0.0036693 
},
{
 "date":   5229,
"name": "GSPC.Close",
"price":  160.3,
"rsi": 54.655,
"ret": 0.0104 
},
{
 "date":   5230,
"name": "GSPC.Close",
"price": 159.89,
"rsi": 60.203,
"ret": -0.0025577 
},
{
 "date":   5233,
"name": "GSPC.Close",
"price": 160.05,
"rsi": 58.295,
"ret": 0.0010007 
},
{
 "date":   5234,
"name": "GSPC.Close",
"price": 161.68,
"rsi": 58.843,
"ret": 0.010184 
},
{
 "date":   5235,
"name": "GSPC.Close",
"price":  161.9,
"rsi": 64.032,
"ret": 0.0013607 
},
{
 "date":   5236,
"name": "GSPC.Close",
"price":  161.2,
"rsi": 64.679,
"ret": -0.0043237 
},
{
 "date":   5237,
"name": "GSPC.Close",
"price": 159.11,
"rsi": 60.923,
"ret": -0.012965 
},
{
 "date":   5240,
"name": "GSPC.Close",
"price": 159.47,
"rsi": 51.335,
"ret": 0.0022626 
},
{
 "date":   5241,
"name": "GSPC.Close",
"price": 160.52,
"rsi": 52.716,
"ret": 0.0065843 
},
{
 "date":   5242,
"name": "GSPC.Close",
"price": 160.11,
"rsi": 56.584,
"ret": -0.0025542 
},
{
 "date":   5243,
"name": "GSPC.Close",
"price":    160,
"rsi": 54.702,
"ret": -0.00068703 
},
{
 "date":   5244,
"name": "GSPC.Close",
"price": 158.49,
"rsi": 54.181,
"ret": -0.0094375 
},
{
 "date":   5247,
"name": "GSPC.Close",
"price":  157.5,
"rsi": 47.499,
"ret": -0.0062465 
},
{
 "date":   5248,
"name": "GSPC.Close",
"price":    158,
"rsi": 43.693,
"ret": 0.0031746 
},
{
 "date":   5249,
"name": "GSPC.Close",
"price": 157.99,
"rsi": 46.044,
"ret": -6.3291e-05 
},
{
 "date":   5250,
"name": "GSPC.Close",
"price": 156.57,
"rsi": 46.003,
"ret": -0.0089879 
},
{
 "date":   5251,
"name": "GSPC.Close",
"price": 155.78,
"rsi": 40.446,
"ret": -0.0050457 
},
{
 "date":   5254,
"name": "GSPC.Close",
"price": 154.73,
"rsi": 37.716,
"ret": -0.0067403 
},
{
 "date":   5255,
"name": "GSPC.Close",
"price": 153.88,
"rsi": 34.394,
"ret": -0.0054934 
},
{
 "date":   5256,
"name": "GSPC.Close",
"price": 153.15,
"rsi": 31.941,
"ret": -0.004744 
},
{
 "date":   5257,
"name": "GSPC.Close",
"price": 151.23,
"rsi": 29.964,
"ret": -0.012537 
},
{
 "date":   5258,
"name": "GSPC.Close",
"price": 151.62,
"rsi": 25.495,
"ret": 0.0025789 
},
{
 "date":   5262,
"name": "GSPC.Close",
"price": 150.29,
"rsi": 27.849,
"ret": -0.0087719 
},
{
 "date":   5263,
"name": "GSPC.Close",
"price": 150.35,
"rsi": 24.954,
"ret": 0.00039923 
},
{
 "date":   5264,
"name": "GSPC.Close",
"price": 150.55,
"rsi": 25.331,
"ret": 0.0013302 
},
{
 "date":   5265,
"name": "GSPC.Close",
"price": 153.24,
"rsi": 26.654,
"ret": 0.017868 
},
{
 "date":   5268,
"name": "GSPC.Close",
"price": 154.34,
"rsi": 41.635,
"ret": 0.0071783 
},
{
 "date":   5269,
"name": "GSPC.Close",
"price": 153.65,
"rsi": 46.452,
"ret": -0.0044706 
},
{
 "date":   5270,
"name": "GSPC.Close",
"price": 155.01,
"rsi": 43.999,
"ret": 0.0088513 
},
{
 "date":   5271,
"name": "GSPC.Close",
"price": 154.92,
"rsi": 49.643,
"ret": -0.00058061 
},
{
 "date":   5272,
"name": "GSPC.Close",
"price": 155.17,
"rsi": 49.289,
"ret": 0.0016137 
},
{
 "date":   5275,
"name": "GSPC.Close",
"price": 153.06,
"rsi": 50.348,
"ret": -0.013598 
},
{
 "date":   5276,
"name": "GSPC.Close",
"price": 152.19,
"rsi": 42.315,
"ret": -0.005684 
},
{
 "date":   5277,
"name": "GSPC.Close",
"price": 152.13,
"rsi": 39.515,
"ret": -0.00039424 
},
{
 "date":   5278,
"name": "GSPC.Close",
"price": 150.39,
"rsi": 39.322,
"ret": -0.011438 
},
{
 "date":   5279,
"name": "GSPC.Close",
"price": 149.03,
"rsi": 34.112,
"ret": -0.0090432 
},
{
 "date":   5282,
"name": "GSPC.Close",
"price": 151.73,
"rsi":  30.69,
"ret": 0.018117 
},
{
 "date":   5283,
"name": "GSPC.Close",
"price": 152.61,
"rsi": 42.931,
"ret": 0.0057998 
},
{
 "date":   5284,
"name": "GSPC.Close",
"price": 154.84,
"rsi": 46.263,
"ret": 0.014612 
},
{
 "date":   5285,
"name": "GSPC.Close",
"price": 154.51,
"rsi": 53.647,
"ret": -0.0021312 
},
{
 "date":   5286,
"name": "GSPC.Close",
"price": 154.46,
"rsi": 52.497,
"ret": -0.0003236 
},
{
 "date":   5289,
"name": "GSPC.Close",
"price": 153.97,
"rsi": 52.314,
"ret": -0.0031723 
},
{
 "date":   5290,
"name": "GSPC.Close",
"price": 152.71,
"rsi": 50.459,
"ret": -0.0081834 
},
{
 "date":   5291,
"name": "GSPC.Close",
"price": 151.64,
"rsi": 45.946,
"ret": -0.0070067 
},
{
 "date":   5292,
"name": "GSPC.Close",
"price": 152.84,
"rsi": 42.472,
"ret": 0.0079135 
},
{
 "date":   5293,
"name": "GSPC.Close",
"price": 153.18,
"rsi": 47.285,
"ret": 0.0022245 
},
{
 "date":   5296,
"name": "GSPC.Close",
"price":  153.2,
"rsi": 48.598,
"ret": 0.00013057 
},
{
 "date":   5297,
"name": "GSPC.Close",
"price":  153.7,
"rsi": 48.679,
"ret": 0.0032637 
},
{
 "date":   5299,
"name": "GSPC.Close",
"price": 152.76,
"rsi": 50.766,
"ret": -0.0061158 
},
{
 "date":   5300,
"name": "GSPC.Close",
"price": 152.24,
"rsi": 46.904,
"ret": -0.003404 
},
{
 "date":   5303,
"name": "GSPC.Close",
"price": 153.36,
"rsi":  44.87,
"ret": 0.0073568 
},
{
 "date":   5304,
"name": "GSPC.Close",
"price": 152.89,
"rsi": 49.908,
"ret": -0.0030647 
},
{
 "date":   5305,
"name": "GSPC.Close",
"price": 150.56,
"rsi": 47.929,
"ret": -0.01524 
},
{
 "date":   5306,
"name": "GSPC.Close",
"price": 150.03,
"rsi": 39.554,
"ret": -0.0035202 
},
{
 "date":   5307,
"name": "GSPC.Close",
"price": 150.88,
"rsi":  37.93,
"ret": 0.0056655 
},
{
 "date":   5310,
"name": "GSPC.Close",
"price":  151.6,
"rsi": 42.039,
"ret": 0.004772 
},
{
 "date":   5311,
"name": "GSPC.Close",
"price": 152.38,
"rsi":  45.34,
"ret": 0.0051451 
},
{
 "date":   5312,
"name": "GSPC.Close",
"price":  151.4,
"rsi": 48.746,
"ret": -0.0064313 
},
{
 "date":   5313,
"name": "GSPC.Close",
"price": 150.37,
"rsi": 44.956,
"ret": -0.0068032 
},
{
 "date":   5314,
"name": "GSPC.Close",
"price": 149.55,
"rsi":  41.32,
"ret": -0.0054532 
},
{
 "date":   5317,
"name": "GSPC.Close",
"price": 148.95,
"rsi":  38.64,
"ret": -0.004012 
},
{
 "date":   5318,
"name": "GSPC.Close",
"price": 147.82,
"rsi": 36.762,
"ret": -0.0075864 
},
{
 "date":   5319,
"name": "GSPC.Close",
"price": 148.83,
"rsi": 33.463,
"ret": 0.0068326 
},
{
 "date":   5320,
"name": "GSPC.Close",
"price": 150.08,
"rsi": 38.754,
"ret": 0.0083988 
},
{
 "date":   5321,
"name": "GSPC.Close",
"price": 151.19,
"rsi": 44.623,
"ret": 0.0073961 
},
{
 "date":   5324,
"name": "GSPC.Close",
"price": 150.19,
"rsi": 49.272,
"ret": -0.0066142 
},
{
 "date":   5325,
"name": "GSPC.Close",
"price": 150.66,
"rsi": 45.561,
"ret": 0.0031294 
},
{
 "date":   5326,
"name": "GSPC.Close",
"price": 154.08,
"rsi":  47.56,
"ret": 0.0227 
},
{
 "date":   5327,
"name": "GSPC.Close",
"price": 157.99,
"rsi": 59.278,
"ret": 0.025376 
},
{
 "date":   5328,
"name": "GSPC.Close",
"price": 162.35,
"rsi": 68.064,
"ret": 0.027597 
},
{
 "date":   5331,
"name": "GSPC.Close",
"price":  162.6,
"rsi": 74.636,
"ret": 0.0015399 
},
{
 "date":   5332,
"name": "GSPC.Close",
"price": 162.72,
"rsi": 74.954,
"ret": 0.00073801 
},
{
 "date":   5333,
"name": "GSPC.Close",
"price": 161.75,
"rsi": 75.116,
"ret": -0.0059612 
},
{
 "date":   5334,
"name": "GSPC.Close",
"price": 165.54,
"rsi": 71.126,
"ret": 0.023431 
},
{
 "date":   5335,
"name": "GSPC.Close",
"price": 165.42,
"rsi":   76.4,
"ret": -0.0007249 
},
{
 "date":   5338,
"name": "GSPC.Close",
"price": 165.43,
"rsi": 75.927,
"ret": 6.0452e-05 
},
{
 "date":   5339,
"name": "GSPC.Close",
"price": 164.42,
"rsi": 75.941,
"ret": -0.0061053 
},
{
 "date":   5340,
"name": "GSPC.Close",
"price":  162.8,
"rsi": 71.616,
"ret": -0.0098528 
},
{
 "date":   5341,
"name": "GSPC.Close",
"price": 163.77,
"rsi": 65.201,
"ret": 0.0059582 
},
{
 "date":   5342,
"name": "GSPC.Close",
"price": 164.14,
"rsi": 67.101,
"ret": 0.0022593 
},
{
 "date":   5345,
"name": "GSPC.Close",
"price": 164.94,
"rsi": 67.823,
"ret": 0.0048739 
},
{
 "date":   5346,
"name": "GSPC.Close",
"price": 167.83,
"rsi": 69.387,
"ret": 0.017522 
},
{
 "date":   5347,
"name": "GSPC.Close",
"price": 167.06,
"rsi": 74.254,
"ret": -0.004588 
},
{
 "date":   5348,
"name": "GSPC.Close",
"price": 167.12,
"rsi": 71.015,
"ret": 0.00035915 
},
{
 "date":   5349,
"name": "GSPC.Close",
"price": 167.51,
"rsi":  71.12,
"ret": 0.0023337 
},
{
 "date":   5352,
"name": "GSPC.Close",
"price": 166.44,
"rsi": 71.839,
"ret": -0.0063877 
},
{
 "date":   5353,
"name": "GSPC.Close",
"price":  167.4,
"rsi": 66.916,
"ret": 0.0057678 
},
{
 "date":   5354,
"name": "GSPC.Close",
"price": 167.09,
"rsi": 68.971,
"ret": -0.0018519 
},
{
 "date":   5355,
"name": "GSPC.Close",
"price":  166.6,
"rsi": 67.513,
"ret": -0.0029326 
},
{
 "date":   5356,
"name": "GSPC.Close",
"price": 166.68,
"rsi": 65.168,
"ret": 0.00048019 
},
{
 "date":   5360,
"name": "GSPC.Close",
"price": 164.88,
"rsi": 65.379,
"ret": -0.010799 
},
{
 "date":   5361,
"name": "GSPC.Close",
"price": 164.29,
"rsi": 56.996,
"ret": -0.0035784 
},
{
 "date":   5362,
"name": "GSPC.Close",
"price": 165.65,
"rsi": 54.528,
"ret": 0.008278 
},
{
 "date":   5363,
"name": "GSPC.Close",
"price": 164.37,
"rsi": 58.941,
"ret": -0.0077271 
},
{
 "date":   5366,
"name": "GSPC.Close",
"price": 164.26,
"rsi": 53.662,
"ret": -0.00066922 
},
{
 "date":   5367,
"name": "GSPC.Close",
"price": 164.45,
"rsi": 53.221,
"ret": 0.0011567 
},
{
 "date":   5368,
"name": "GSPC.Close",
"price": 164.68,
"rsi": 53.925,
"ret": 0.0013986 
},
{
 "date":   5369,
"name": "GSPC.Close",
"price": 167.94,
"rsi": 54.813,
"ret": 0.019796 
},
{
 "date":   5370,
"name": "GSPC.Close",
"price": 168.78,
"rsi": 65.078,
"ret": 0.0050018 
},
{
 "date":   5373,
"name": "GSPC.Close",
"price": 168.87,
"rsi": 67.149,
"ret": 0.00053324 
},
{
 "date":   5374,
"name": "GSPC.Close",
"price": 167.65,
"rsi": 67.372,
"ret": -0.0072245 
},
{
 "date":   5375,
"name": "GSPC.Close",
"price": 166.94,
"rsi": 61.292,
"ret": -0.004235 
},
{
 "date":   5376,
"name": "GSPC.Close",
"price": 167.47,
"rsi":  58.01,
"ret": 0.0031748 
},
{
 "date":   5377,
"name": "GSPC.Close",
"price": 165.67,
"rsi": 59.743,
"ret": -0.010748 
},
{
 "date":   5380,
"name": "GSPC.Close",
"price": 165.28,
"rsi": 51.909,
"ret": -0.0023541 
},
{
 "date":   5381,
"name": "GSPC.Close",
"price": 165.62,
"rsi": 50.368,
"ret": 0.0020571 
},
{
 "date":   5382,
"name": "GSPC.Close",
"price": 166.28,
"rsi": 51.714,
"ret": 0.003985 
},
{
 "date":   5383,
"name": "GSPC.Close",
"price": 166.96,
"rsi": 54.304,
"ret": 0.0040895 
},
{
 "date":   5384,
"name": "GSPC.Close",
"price":  166.1,
"rsi": 56.871,
"ret": -0.0051509 
},
{
 "date":   5387,
"name": "GSPC.Close",
"price": 164.62,
"rsi": 52.829,
"ret": -0.0089103 
},
{
 "date":   5388,
"name": "GSPC.Close",
"price": 163.59,
"rsi":  46.68,
"ret": -0.0062568 
},
{
 "date":   5389,
"name": "GSPC.Close",
"price": 162.44,
"rsi": 42.934,
"ret": -0.0070298 
},
{
 "date":   5390,
"name": "GSPC.Close",
"price": 162.92,
"rsi": 39.157,
"ret": 0.0029549 
},
{
 "date":   5391,
"name": "GSPC.Close",
"price": 162.68,
"rsi": 41.472,
"ret": -0.0014731 
},
{
 "date":   5394,
"name": "GSPC.Close",
"price": 162.13,
"rsi": 40.639,
"ret": -0.0033809 
},
{
 "date":   5395,
"name": "GSPC.Close",
"price": 161.67,
"rsi": 38.721,
"ret": -0.0028372 
},
{
 "date":   5396,
"name": "GSPC.Close",
"price": 162.11,
"rsi": 37.141,
"ret": 0.0027216 
},
{
 "date":   5397,
"name": "GSPC.Close",
"price": 162.78,
"rsi": 39.676,
"ret": 0.004133 
},
{
 "date":   5398,
"name": "GSPC.Close",
"price": 164.18,
"rsi": 43.417,
"ret": 0.0086006 
},
{
 "date":   5401,
"name": "GSPC.Close",
"price": 165.77,
"rsi": 50.346,
"ret": 0.0096845 
},
{
 "date":   5402,
"name": "GSPC.Close",
"price": 164.78,
"rsi": 56.814,
"ret": -0.0059721 
},
{
 "date":   5403,
"name": "GSPC.Close",
"price": 164.14,
"rsi":  52.25,
"ret": -0.003884 
},
{
 "date":   5404,
"name": "GSPC.Close",
"price":  168.1,
"rsi": 49.483,
"ret": 0.024126 
},
{
 "date":   5405,
"name": "GSPC.Close",
"price": 167.96,
"rsi": 62.661,
"ret": -0.00083284 
},
{
 "date":   5408,
"name": "GSPC.Close",
"price": 167.36,
"rsi": 62.045,
"ret": -0.0035723 
},
{
 "date":   5409,
"name": "GSPC.Close",
"price": 167.09,
"rsi": 59.351,
"ret": -0.0016133 
},
{
 "date":   5410,
"name": "GSPC.Close",
"price":  167.2,
"rsi": 58.128,
"ret": 0.00065833 
},
{
 "date":   5411,
"name": "GSPC.Close",
"price": 166.31,
"rsi": 58.503,
"ret": -0.005323 
},
{
 "date":   5412,
"name": "GSPC.Close",
"price": 165.29,
"rsi": 54.266,
"ret": -0.0061331 
},
{
 "date":   5415,
"name": "GSPC.Close",
"price": 164.78,
"rsi": 49.814,
"ret": -0.0030855 
},
{
 "date":   5416,
"name": "GSPC.Close",
"price": 166.84,
"rsi": 47.706,
"ret": 0.012502 
},
{
 "date":   5417,
"name": "GSPC.Close",
"price": 166.09,
"rsi": 55.835,
"ret": -0.0044953 
},
{
 "date":   5418,
"name": "GSPC.Close",
"price": 167.49,
"rsi": 52.627,
"ret": 0.0084292 
},
{
 "date":   5419,
"name": "GSPC.Close",
"price": 167.42,
"rsi": 57.531,
"ret": -0.00041794 
},
{
 "date":   5422,
"name": "GSPC.Close",
"price": 168.58,
"rsi": 57.213,
"ret": 0.0069287 
},
{
 "date":   5423,
"name": "GSPC.Close",
"price": 170.41,
"rsi": 61.064,
"ret": 0.010855 
},
{
 "date":   5424,
"name": "GSPC.Close",
"price": 169.17,
"rsi": 66.229,
"ret": -0.0072766 
},
{
 "date":   5425,
"name": "GSPC.Close",
"price": 168.68,
"rsi": 60.384,
"ret": -0.0028965 
},
{
 "date":   5426,
"name": "GSPC.Close",
"price":  167.6,
"rsi": 58.198,
"ret": -0.0064027 
},
{
 "date":   5429,
"name": "GSPC.Close",
"price": 167.36,
"rsi": 53.593,
"ret": -0.001432 
},
{
 "date":   5430,
"name": "GSPC.Close",
"price": 165.97,
"rsi": 52.597,
"ret": -0.0083054 
},
{
 "date":   5431,
"name": "GSPC.Close",
"price": 165.99,
"rsi": 47.134,
"ret": 0.0001205 
},
{
 "date":   5432,
"name": "GSPC.Close",
"price": 165.89,
"rsi": 47.219,
"ret": -0.00060245 
},
{
 "date":   5433,
"name": "GSPC.Close",
"price":  164.1,
"rsi": 46.814,
"ret": -0.01079 
},
{
 "date":   5436,
"name": "GSPC.Close",
"price": 163.09,
"rsi": 40.171,
"ret": -0.0061548 
},
{
 "date":   5437,
"name": "GSPC.Close",
"price": 164.18,
"rsi": 36.982,
"ret": 0.0066834 
},
{
 "date":   5438,
"name": "GSPC.Close",
"price": 164.51,
"rsi": 42.305,
"ret": 0.00201 
},
{
 "date":   5440,
"name": "GSPC.Close",
"price": 166.92,
"rsi": 43.851,
"ret": 0.01465 
},
{
 "date":   5443,
"name": "GSPC.Close",
"price": 165.55,
"rsi": 53.626,
"ret": -0.0082075 
},
{
 "date":   5444,
"name": "GSPC.Close",
"price": 166.29,
"rsi": 48.461,
"ret": 0.0044699 
},
{
 "date":   5445,
"name": "GSPC.Close",
"price": 165.02,
"rsi": 51.196,
"ret": -0.0076373 
},
{
 "date":   5446,
"name": "GSPC.Close",
"price": 163.91,
"rsi": 46.624,
"ret": -0.0067265 
},
{
 "date":   5447,
"name": "GSPC.Close",
"price": 163.58,
"rsi": 43.009,
"ret": -0.0020133 
},
{
 "date":   5450,
"name": "GSPC.Close",
"price": 162.82,
"rsi": 41.967,
"ret": -0.004646 
},
{
 "date":   5451,
"name": "GSPC.Close",
"price": 163.38,
"rsi": 39.589,
"ret": 0.0034394 
},
{
 "date":   5452,
"name": "GSPC.Close",
"price":  162.1,
"rsi": 42.189,
"ret": -0.0078345 
},
{
 "date":   5453,
"name": "GSPC.Close",
"price": 162.76,
"rsi": 38.148,
"ret": 0.0040716 
},
{
 "date":   5454,
"name": "GSPC.Close",
"price": 162.26,
"rsi": 41.271,
"ret": -0.003072 
},
{
 "date":   5457,
"name": "GSPC.Close",
"price": 162.83,
"rsi": 39.638,
"ret": 0.0035129 
},
{
 "date":   5458,
"name": "GSPC.Close",
"price": 163.07,
"rsi": 42.435,
"ret": 0.0014739 
},
{
 "date":   5459,
"name": "GSPC.Close",
"price": 162.63,
"rsi": 43.619,
"ret": -0.0026982 
},
{
 "date":   5460,
"name": "GSPC.Close",
"price": 161.81,
"rsi": 41.916,
"ret": -0.0050421 
},
{
 "date":   5461,
"name": "GSPC.Close",
"price": 162.69,
"rsi": 38.871,
"ret": 0.0054385 
},
{
 "date":   5464,
"name": "GSPC.Close",
"price": 163.61,
"rsi": 43.606,
"ret": 0.0056549 
},
{
 "date":   5465,
"name": "GSPC.Close",
"price": 168.11,
"rsi":  48.13,
"ret": 0.027504 
},
{
 "date":   5466,
"name": "GSPC.Close",
"price": 167.16,
"rsi": 63.538,
"ret": -0.0056511 
},
{
 "date":   5467,
"name": "GSPC.Close",
"price": 166.38,
"rsi": 59.519,
"ret": -0.0046662 
},
{
 "date":   5468,
"name": "GSPC.Close",
"price": 165.51,
"rsi": 56.366,
"ret": -0.005229 
},
{
 "date":   5471,
"name": "GSPC.Close",
"price": 166.76,
"rsi": 52.994,
"ret": 0.0075524 
},
{
 "date":   5473,
"name": "GSPC.Close",
"price": 166.47,
"rsi": 56.976,
"ret": -0.001739 
},
{
 "date":   5474,
"name": "GSPC.Close",
"price": 165.75,
"rsi": 55.795,
"ret": -0.0043251 
},
{
 "date":   5475,
"name": "GSPC.Close",
"price": 166.26,
"rsi": 52.865,
"ret": 0.0030769 
},
{
 "date":   5478,
"name": "GSPC.Close",
"price": 167.24,
"rsi": 54.681,
"ret": 0.0058944 
},
{
 "date":   5480,
"name": "GSPC.Close",
"price": 165.37,
"rsi": 58.026,
"ret": -0.011182 
},
{
 "date":   5481,
"name": "GSPC.Close",
"price": 164.57,
"rsi": 50.383,
"ret": -0.0048376 
},
{
 "date":   5482,
"name": "GSPC.Close",
"price": 163.68,
"rsi": 47.501,
"ret": -0.005408 
},
{
 "date":   5485,
"name": "GSPC.Close",
"price": 164.24,
"rsi": 44.454,
"ret": 0.0034213 
},
{
 "date":   5486,
"name": "GSPC.Close",
"price": 163.99,
"rsi": 46.767,
"ret": -0.0015222 
},
{
 "date":   5487,
"name": "GSPC.Close",
"price": 165.18,
"rsi": 45.849,
"ret": 0.0072565 
},
{
 "date":   5488,
"name": "GSPC.Close",
"price": 168.31,
"rsi": 50.801,
"ret": 0.018949 
},
{
 "date":   5489,
"name": "GSPC.Close",
"price": 167.91,
"rsi": 60.923,
"ret": -0.0023766 
},
{
 "date":   5492,
"name": "GSPC.Close",
"price": 170.51,
"rsi": 59.245,
"ret": 0.015484 
},
{
 "date":   5493,
"name": "GSPC.Close",
"price": 170.81,
"rsi": 65.831,
"ret": 0.0017594 
},
{
 "date":   5494,
"name": "GSPC.Close",
"price": 171.19,
"rsi": 66.504,
"ret": 0.0022247 
},
{
 "date":   5495,
"name": "GSPC.Close",
"price": 170.73,
"rsi": 67.379,
"ret": -0.0026871 
},
{
 "date":   5496,
"name": "GSPC.Close",
"price": 171.32,
"rsi": 65.158,
"ret": 0.0034557 
},
{
 "date":   5499,
"name": "GSPC.Close",
"price": 175.23,
"rsi": 66.676,
"ret": 0.022823 
},
{
 "date":   5500,
"name": "GSPC.Close",
"price": 175.48,
"rsi": 74.578,
"ret": 0.0014267 
},
{
 "date":   5501,
"name": "GSPC.Close",
"price":  177.3,
"rsi": 74.986,
"ret": 0.010372 
},
{
 "date":   5502,
"name": "GSPC.Close",
"price": 176.71,
"rsi": 77.784,
"ret": -0.0033277 
},
{
 "date":   5503,
"name": "GSPC.Close",
"price": 177.35,
"rsi": 74.861,
"ret": 0.0036218 
},
{
 "date":   5506,
"name": "GSPC.Close",
"price":  177.4,
"rsi": 75.918,
"ret": 0.00028193 
},
{
 "date":   5507,
"name": "GSPC.Close",
"price": 179.18,
"rsi": 76.003,
"ret": 0.010034 
},
{
 "date":   5508,
"name": "GSPC.Close",
"price": 179.39,
"rsi": 78.861,
"ret": 0.001172 
},
{
 "date":   5509,
"name": "GSPC.Close",
"price": 179.63,
"rsi": 79.176,
"ret": 0.0013379 
},
{
 "date":   5510,
"name": "GSPC.Close",
"price": 178.63,
"rsi": 79.551,
"ret": -0.005567 
},
{
 "date":   5513,
"name": "GSPC.Close",
"price": 180.35,
"rsi": 73.601,
"ret": 0.0096288 
},
{
 "date":   5514,
"name": "GSPC.Close",
"price": 180.61,
"rsi": 76.813,
"ret": 0.0014416 
},
{
 "date":   5515,
"name": "GSPC.Close",
"price": 180.43,
"rsi": 77.264,
"ret": -0.00099662 
},
{
 "date":   5516,
"name": "GSPC.Close",
"price": 181.82,
"rsi": 76.161,
"ret": 0.0077038 
},
{
 "date":   5517,
"name": "GSPC.Close",
"price": 182.19,
"rsi": 78.691,
"ret": 0.002035 
},
{
 "date":   5520,
"name": "GSPC.Close",
"price": 180.51,
"rsi":  79.32,
"ret": -0.0092211 
},
{
 "date":   5521,
"name": "GSPC.Close",
"price": 180.56,
"rsi": 69.314,
"ret": 0.00027699 
},
{
 "date":   5522,
"name": "GSPC.Close",
"price": 183.35,
"rsi": 69.438,
"ret": 0.015452 
},
{
 "date":   5523,
"name": "GSPC.Close",
"price": 182.41,
"rsi": 75.392,
"ret": -0.0051268 
},
{
 "date":   5524,
"name": "GSPC.Close",
"price":  181.6,
"rsi": 70.415,
"ret": -0.0044405 
},
{
 "date":   5528,
"name": "GSPC.Close",
"price": 181.33,
"rsi": 66.349,
"ret": -0.0014868 
},
{
 "date":   5529,
"name": "GSPC.Close",
"price": 181.18,
"rsi": 65.002,
"ret": -0.00082722 
},
{
 "date":   5530,
"name": "GSPC.Close",
"price": 180.19,
"rsi": 64.222,
"ret": -0.0054642 
},
{
 "date":   5531,
"name": "GSPC.Close",
"price": 179.36,
"rsi": 59.174,
"ret": -0.0046062 
},
{
 "date":   5534,
"name": "GSPC.Close",
"price": 179.23,
"rsi": 55.253,
"ret": -0.0007248 
},
{
 "date":   5535,
"name": "GSPC.Close",
"price": 181.17,
"rsi": 54.643,
"ret": 0.010824 
},
{
 "date":   5536,
"name": "GSPC.Close",
"price": 180.71,
"rsi": 61.484,
"ret": -0.0025391 
},
{
 "date":   5537,
"name": "GSPC.Close",
"price": 181.18,
"rsi": 59.204,
"ret": 0.0026009 
},
{
 "date":   5538,
"name": "GSPC.Close",
"price": 183.23,
"rsi": 60.804,
"ret": 0.011315 
},
{
 "date":   5541,
"name": "GSPC.Close",
"price": 182.06,
"rsi":   66.9,
"ret": -0.0063854 
},
{
 "date":   5542,
"name": "GSPC.Close",
"price": 182.23,
"rsi": 61.063,
"ret": 0.00093376 
},
{
 "date":   5543,
"name": "GSPC.Close",
"price": 180.65,
"rsi": 61.587,
"ret": -0.0086704 
},
{
 "date":   5544,
"name": "GSPC.Close",
"price": 179.51,
"rsi": 54.271,
"ret": -0.0063105 
},
{
 "date":   5545,
"name": "GSPC.Close",
"price":  179.1,
"rsi": 49.684,
"ret": -0.002284 
},
{
 "date":   5548,
"name": "GSPC.Close",
"price": 178.79,
"rsi":  48.11,
"ret": -0.0017309 
},
{
 "date":   5549,
"name": "GSPC.Close",
"price": 179.66,
"rsi": 46.899,
"ret": 0.004866 
},
{
 "date":   5550,
"name": "GSPC.Close",
"price": 178.19,
"rsi": 50.651,
"ret": -0.0081821 
},
{
 "date":   5551,
"name": "GSPC.Close",
"price": 177.84,
"rsi": 44.881,
"ret": -0.0019642 
},
{
 "date":   5552,
"name": "GSPC.Close",
"price": 176.53,
"rsi": 43.607,
"ret": -0.0073662 
},
{
 "date":   5555,
"name": "GSPC.Close",
"price": 176.88,
"rsi":  39.13,
"ret": 0.0019827 
},
{
 "date":   5556,
"name": "GSPC.Close",
"price": 179.54,
"rsi": 40.876,
"ret": 0.015038 
},
{
 "date":   5557,
"name": "GSPC.Close",
"price": 179.08,
"rsi":  52.12,
"ret": -0.0025621 
},
{
 "date":   5558,
"name": "GSPC.Close",
"price": 179.35,
"rsi": 50.337,
"ret": 0.0015077 
},
{
 "date":   5559,
"name": "GSPC.Close",
"price": 179.04,
"rsi": 51.388,
"ret": -0.0017285 
},
{
 "date":   5562,
"name": "GSPC.Close",
"price": 177.97,
"rsi": 50.078,
"ret": -0.0059763 
},
{
 "date":   5563,
"name": "GSPC.Close",
"price": 178.43,
"rsi": 45.742,
"ret": 0.0025847 
},
{
 "date":   5564,
"name": "GSPC.Close",
"price": 179.54,
"rsi": 47.833,
"ret": 0.0062209 
},
{
 "date":   5565,
"name": "GSPC.Close",
"price": 179.54,
"rsi": 52.582,
"ret":      0 
},
{
 "date":   5566,
"name": "GSPC.Close",
"price": 180.66,
"rsi": 52.582,
"ret": 0.0062382 
},
{
 "date":   5569,
"name": "GSPC.Close",
"price": 181.27,
"rsi": 57.147,
"ret": 0.0033765 
},
{
 "date":   5570,
"name": "GSPC.Close",
"price": 180.53,
"rsi": 59.438,
"ret": -0.0040823 
},
{
 "date":   5571,
"name": "GSPC.Close",
"price": 179.11,
"rsi": 55.558,
"ret": -0.0078657 
},
{
 "date":   5572,
"name": "GSPC.Close",
"price": 179.03,
"rsi": 48.955,
"ret": -0.00044665 
},
{
 "date":   5576,
"name": "GSPC.Close",
"price": 178.03,
"rsi": 48.604,
"ret": -0.0055857 
},
{
 "date":   5577,
"name": "GSPC.Close",
"price": 178.21,
"rsi": 44.332,
"ret": 0.0010111 
},
{
 "date":   5578,
"name": "GSPC.Close",
"price": 179.42,
"rsi": 45.265,
"ret": 0.0067897 
},
{
 "date":   5579,
"name": "GSPC.Close",
"price": 180.19,
"rsi": 51.185,
"ret": 0.0042916 
},
{
 "date":   5580,
"name": "GSPC.Close",
"price": 180.54,
"rsi": 54.554,
"ret": 0.0019424 
},
{
 "date":   5583,
"name": "GSPC.Close",
"price": 180.92,
"rsi": 56.039,
"ret": 0.0021048 
},
{
 "date":   5584,
"name": "GSPC.Close",
"price":  181.2,
"rsi": 57.657,
"ret": 0.0015476 
},
{
 "date":   5585,
"name": "GSPC.Close",
"price": 181.68,
"rsi": 58.859,
"ret": 0.002649 
},
{
 "date":   5586,
"name": "GSPC.Close",
"price": 180.84,
"rsi": 60.907,
"ret": -0.0046235 
},
{
 "date":   5587,
"name": "GSPC.Close",
"price": 181.11,
"rsi": 55.683,
"ret": 0.001493 
},
{
 "date":   5590,
"name": "GSPC.Close",
"price":  180.7,
"rsi": 56.961,
"ret": -0.0022638 
},
{
 "date":   5591,
"name": "GSPC.Close",
"price": 181.88,
"rsi": 54.396,
"ret": 0.0065302 
},
{
 "date":   5592,
"name": "GSPC.Close",
"price": 182.26,
"rsi": 59.981,
"ret": 0.0020893 
},
{
 "date":   5593,
"name": "GSPC.Close",
"price": 183.43,
"rsi": 61.612,
"ret": 0.0064194 
},
{
 "date":   5594,
"name": "GSPC.Close",
"price": 182.18,
"rsi":  66.18,
"ret": -0.0068146 
},
{
 "date":   5597,
"name": "GSPC.Close",
"price": 180.63,
"rsi": 58.209,
"ret": -0.0085081 
},
{
 "date":   5598,
"name": "GSPC.Close",
"price": 179.83,
"rsi": 50.144,
"ret": -0.0044289 
},
{
 "date":   5599,
"name": "GSPC.Close",
"price": 178.37,
"rsi": 46.559,
"ret": -0.0081188 
},
{
 "date":   5600,
"name": "GSPC.Close",
"price": 179.01,
"rsi": 40.822,
"ret": 0.003588 
},
{
 "date":   5601,
"name": "GSPC.Close",
"price": 180.08,
"rsi": 44.075,
"ret": 0.0059773 
},
{
 "date":   5604,
"name": "GSPC.Close",
"price": 179.99,
"rsi": 49.112,
"ret": -0.00049978 
},
{
 "date":   5605,
"name": "GSPC.Close",
"price": 180.76,
"rsi": 48.714,
"ret": 0.004278 
},
{
 "date":   5606,
"name": "GSPC.Close",
"price": 180.62,
"rsi": 52.273,
"ret": -0.00077451 
},
{
 "date":   5607,
"name": "GSPC.Close",
"price": 181.92,
"rsi": 51.572,
"ret": 0.0071974 
},
{
 "date":   5608,
"name": "GSPC.Close",
"price": 184.28,
"rsi": 57.296,
"ret": 0.012973 
},
{
 "date":   5611,
"name": "GSPC.Close",
"price": 184.61,
"rsi": 65.311,
"ret": 0.0017908 
},
{
 "date":   5612,
"name": "GSPC.Close",
"price": 183.87,
"rsi": 66.265,
"ret": -0.0040085 
},
{
 "date":   5613,
"name": "GSPC.Close",
"price": 184.54,
"rsi":  62.14,
"ret": 0.0036439 
},
{
 "date":   5614,
"name": "GSPC.Close",
"price": 185.66,
"rsi": 64.306,
"ret": 0.0060691 
},
{
 "date":   5615,
"name": "GSPC.Close",
"price": 187.42,
"rsi":  67.64,
"ret": 0.0094797 
},
{
 "date":   5618,
"name": "GSPC.Close",
"price": 189.72,
"rsi": 72.056,
"ret": 0.012272 
},
{
 "date":   5619,
"name": "GSPC.Close",
"price": 189.64,
"rsi": 76.559,
"ret": -0.00042167 
},
{
 "date":   5620,
"name": "GSPC.Close",
"price": 188.56,
"rsi": 76.099,
"ret": -0.005695 
},
{
 "date":   5621,
"name": "GSPC.Close",
"price":  187.6,
"rsi": 69.995,
"ret": -0.0050912 
},
{
 "date":   5622,
"name": "GSPC.Close",
"price": 188.29,
"rsi": 65.003,
"ret": 0.003678 
},
{
 "date":   5626,
"name": "GSPC.Close",
"price": 187.86,
"rsi": 66.834,
"ret": -0.0022837 
},
{
 "date":   5627,
"name": "GSPC.Close",
"price": 187.68,
"rsi": 64.567,
"ret": -0.00095816 
},
{
 "date":   5628,
"name": "GSPC.Close",
"price": 187.75,
"rsi": 63.594,
"ret": 0.00037298 
},
{
 "date":   5629,
"name": "GSPC.Close",
"price": 189.55,
"rsi": 63.822,
"ret": 0.0095872 
},
{
 "date":   5632,
"name": "GSPC.Close",
"price": 189.32,
"rsi": 69.173,
"ret": -0.0012134 
},
{
 "date":   5633,
"name": "GSPC.Close",
"price": 190.04,
"rsi": 67.793,
"ret": 0.0038031 
},
{
 "date":   5634,
"name": "GSPC.Close",
"price": 190.16,
"rsi": 69.823,
"ret": 0.00063145 
},
{
 "date":   5635,
"name": "GSPC.Close",
"price": 191.06,
"rsi":  70.16,
"ret": 0.0047329 
},
{
 "date":   5636,
"name": "GSPC.Close",
"price": 189.68,
"rsi": 72.632,
"ret": -0.0072229 
},
{
 "date":   5639,
"name": "GSPC.Close",
"price": 189.51,
"rsi": 63.892,
"ret": -0.00089625 
},
{
 "date":   5640,
"name": "GSPC.Close",
"price": 189.04,
"rsi": 62.888,
"ret": -0.0024801 
},
{
 "date":   5641,
"name": "GSPC.Close",
"price": 187.61,
"rsi": 60.078,
"ret": -0.0075645 
},
{
 "date":   5642,
"name": "GSPC.Close",
"price": 185.33,
"rsi": 52.404,
"ret": -0.012153 
},
{
 "date":   5643,
"name": "GSPC.Close",
"price":  187.1,
"rsi": 42.978,
"ret": 0.0095505 
},
{
 "date":   5646,
"name": "GSPC.Close",
"price": 186.53,
"rsi": 50.432,
"ret": -0.0030465 
},
{
 "date":   5647,
"name": "GSPC.Close",
"price": 187.34,
"rsi": 48.245,
"ret": 0.0043425 
},
{
 "date":   5648,
"name": "GSPC.Close",
"price": 186.63,
"rsi": 51.466,
"ret": -0.0037899 
},
{
 "date":   5649,
"name": "GSPC.Close",
"price": 186.73,
"rsi":  48.61,
"ret": 0.00053582 
},
{
 "date":   5650,
"name": "GSPC.Close",
"price": 189.61,
"rsi": 49.039,
"ret": 0.015423 
},
{
 "date":   5653,
"name": "GSPC.Close",
"price": 189.15,
"rsi": 59.519,
"ret": -0.002426 
},
{
 "date":   5654,
"name": "GSPC.Close",
"price": 189.74,
"rsi": 57.485,
"ret": 0.0031192 
},
{
 "date":   5655,
"name": "GSPC.Close",
"price": 190.06,
"rsi": 59.401,
"ret": 0.0016865 
},
{
 "date":   5656,
"name": "GSPC.Close",
"price": 191.23,
"rsi": 60.442,
"ret": 0.006156 
},
{
 "date":   5657,
"name": "GSPC.Close",
"price": 191.85,
"rsi":  64.07,
"ret": 0.0032422 
},
{
 "date":   5660,
"name": "GSPC.Close",
"price": 192.43,
"rsi": 65.857,
"ret": 0.0030232 
},
{
 "date":   5661,
"name": "GSPC.Close",
"price": 192.01,
"rsi": 67.487,
"ret": -0.0021826 
},
{
 "date":   5662,
"name": "GSPC.Close",
"price": 191.45,
"rsi": 65.065,
"ret": -0.0029165 
},
{
 "date":   5664,
"name": "GSPC.Close",
"price": 192.52,
"rsi": 61.878,
"ret": 0.0055889 
},
{
 "date":   5667,
"name": "GSPC.Close",
"price": 191.93,
"rsi": 65.369,
"ret": -0.0030646 
},
{
 "date":   5668,
"name": "GSPC.Close",
"price": 191.05,
"rsi": 61.997,
"ret": -0.004585 
},
{
 "date":   5669,
"name": "GSPC.Close",
"price": 192.37,
"rsi": 57.254,
"ret": 0.0069092 
},
{
 "date":   5670,
"name": "GSPC.Close",
"price": 192.94,
"rsi": 61.956,
"ret": 0.002963 
},
{
 "date":   5671,
"name": "GSPC.Close",
"price": 193.29,
"rsi": 63.807,
"ret": 0.001814 
},
{
 "date":   5674,
"name": "GSPC.Close",
"price": 192.72,
"rsi": 64.936,
"ret": -0.0029489 
},
{
 "date":   5675,
"name": "GSPC.Close",
"price": 194.72,
"rsi": 61.569,
"ret": 0.010378 
},
{
 "date":   5676,
"name": "GSPC.Close",
"price": 195.65,
"rsi": 67.864,
"ret": 0.0047761 
},
{
 "date":   5677,
"name": "GSPC.Close",
"price": 194.38,
"rsi": 70.301,
"ret": -0.0064912 
},
{
 "date":   5678,
"name": "GSPC.Close",
"price": 195.13,
"rsi": 63.249,
"ret": 0.0038584 
},
{
 "date":   5681,
"name": "GSPC.Close",
"price": 194.35,
"rsi": 65.453,
"ret": -0.0039973 
},
{
 "date":   5682,
"name": "GSPC.Close",
"price": 192.55,
"rsi": 61.334,
"ret": -0.0092616 
},
{
 "date":   5683,
"name": "GSPC.Close",
"price": 191.58,
"rsi": 53.038,
"ret": -0.0050377 
},
{
 "date":   5684,
"name": "GSPC.Close",
"price": 192.06,
"rsi": 49.178,
"ret": 0.0025055 
},
{
 "date":   5685,
"name": "GSPC.Close",
"price":  192.4,
"rsi": 51.075,
"ret": 0.0017703 
},
{
 "date":   5688,
"name": "GSPC.Close",
"price":  189.6,
"rsi":  52.43,
"ret": -0.014553 
},
{
 "date":   5689,
"name": "GSPC.Close",
"price": 189.93,
"rsi": 42.092,
"ret": 0.0017405 
},
{
 "date":   5690,
"name": "GSPC.Close",
"price": 190.92,
"rsi": 43.506,
"ret": 0.0052124 
},
{
 "date":   5691,
"name": "GSPC.Close",
"price": 192.11,
"rsi": 47.636,
"ret": 0.006233 
},
{
 "date":   5692,
"name": "GSPC.Close",
"price": 191.48,
"rsi": 52.164,
"ret": -0.0032794 
},
{
 "date":   5695,
"name": "GSPC.Close",
"price": 190.62,
"rsi": 49.713,
"ret": -0.0044913 
},
{
 "date":   5696,
"name": "GSPC.Close",
"price": 187.93,
"rsi": 46.502,
"ret": -0.014112 
},
{
 "date":   5697,
"name": "GSPC.Close",
"price": 187.68,
"rsi": 38.191,
"ret": -0.0013303 
},
{
 "date":   5698,
"name": "GSPC.Close",
"price": 188.95,
"rsi":  37.52,
"ret": 0.0067668 
},
{
 "date":   5699,
"name": "GSPC.Close",
"price": 188.32,
"rsi":     43,
"ret": -0.0033342 
},
{
 "date":   5702,
"name": "GSPC.Close",
"price": 187.63,
"rsi": 41.075,
"ret": -0.003664 
},
{
 "date":   5703,
"name": "GSPC.Close",
"price":  187.3,
"rsi": 39.016,
"ret": -0.0017588 
},
{
 "date":   5704,
"name": "GSPC.Close",
"price": 187.41,
"rsi": 38.033,
"ret": 0.00058729 
},
{
 "date":   5705,
"name": "GSPC.Close",
"price": 187.26,
"rsi": 38.588,
"ret": -0.00080038 
},
{
 "date":   5706,
"name": "GSPC.Close",
"price":  186.1,
"rsi": 38.087,
"ret": -0.0061946 
},
{
 "date":   5709,
"name": "GSPC.Close",
"price": 186.38,
"rsi": 34.371,
"ret": 0.0015046 
},
{
 "date":   5710,
"name": "GSPC.Close",
"price": 188.08,
"rsi": 35.995,
"ret": 0.0091212 
},
{
 "date":   5711,
"name": "GSPC.Close",
"price": 189.16,
"rsi": 44.905,
"ret": 0.0057422 
},
{
 "date":   5712,
"name": "GSPC.Close",
"price": 187.36,
"rsi": 49.696,
"ret": -0.0095158 
},
{
 "date":   5713,
"name": "GSPC.Close",
"price": 187.17,
"rsi": 42.987,
"ret": -0.0010141 
},
{
 "date":   5716,
"name": "GSPC.Close",
"price": 187.31,
"rsi": 42.337,
"ret": 0.00074798 
},
{
 "date":   5717,
"name": "GSPC.Close",
"price":  188.1,
"rsi":  43.02,
"ret": 0.0042176 
},
{
 "date":   5718,
"name": "GSPC.Close",
"price": 188.83,
"rsi": 46.849,
"ret": 0.0038809 
},
{
 "date":   5719,
"name": "GSPC.Close",
"price": 188.93,
"rsi":  50.18,
"ret": 0.00052958 
},
{
 "date":   5720,
"name": "GSPC.Close",
"price": 188.63,
"rsi": 50.636,
"ret": -0.0015879 
},
{
 "date":   5724,
"name": "GSPC.Close",
"price": 187.91,
"rsi": 49.181,
"ret": -0.003817 
},
{
 "date":   5725,
"name": "GSPC.Close",
"price": 187.37,
"rsi": 45.779,
"ret": -0.0028737 
},
{
 "date":   5726,
"name": "GSPC.Close",
"price": 187.27,
"rsi": 43.358,
"ret": -0.0005337 
},
{
 "date":   5727,
"name": "GSPC.Close",
"price": 188.24,
"rsi": 42.905,
"ret": 0.0051797 
},
{
 "date":   5730,
"name": "GSPC.Close",
"price": 188.25,
"rsi": 48.519,
"ret": 5.3124e-05 
},
{
 "date":   5731,
"name": "GSPC.Close",
"price":  186.9,
"rsi": 48.576,
"ret": -0.0071713 
},
{
 "date":   5732,
"name": "GSPC.Close",
"price": 185.03,
"rsi": 41.928,
"ret": -0.010005 
},
{
 "date":   5733,
"name": "GSPC.Close",
"price": 183.69,
"rsi": 34.819,
"ret": -0.0072421 
},
{
 "date":   5734,
"name": "GSPC.Close",
"price": 182.91,
"rsi": 30.791,
"ret": -0.0042463 
},
{
 "date":   5737,
"name": "GSPC.Close",
"price": 182.88,
"rsi": 28.709,
"ret": -0.00016402 
},
{
 "date":   5738,
"name": "GSPC.Close",
"price": 181.36,
"rsi": 28.629,
"ret": -0.0083115 
},
{
 "date":   5739,
"name": "GSPC.Close",
"price": 181.71,
"rsi": 24.843,
"ret": 0.0019299 
},
{
 "date":   5740,
"name": "GSPC.Close",
"price": 183.39,
"rsi": 27.229,
"ret": 0.0092455 
},
{
 "date":   5741,
"name": "GSPC.Close",
"price": 182.05,
"rsi": 37.489,
"ret": -0.0073068 
},
{
 "date":   5744,
"name": "GSPC.Close",
"price":  184.3,
"rsi": 33.439,
"ret": 0.012359 
},
{
 "date":   5745,
"name": "GSPC.Close",
"price": 182.62,
"rsi": 44.317,
"ret": -0.0091156 
},
{
 "date":   5746,
"name": "GSPC.Close",
"price": 180.66,
"rsi":  39.17,
"ret": -0.010733 
},
{
 "date":   5747,
"name": "GSPC.Close",
"price": 181.29,
"rsi": 34.182,
"ret": 0.0034872 
},
{
 "date":   5751,
"name": "GSPC.Close",
"price": 182.08,
"rsi":  36.96,
"ret": 0.0043577 
},
{
 "date":   5752,
"name": "GSPC.Close",
"price": 185.07,
"rsi": 40.361,
"ret": 0.016421 
},
{
 "date":   5753,
"name": "GSPC.Close",
"price": 184.06,
"rsi": 51.109,
"ret": -0.0054574 
},
{
 "date":   5754,
"name": "GSPC.Close",
"price": 184.36,
"rsi": 47.965,
"ret": 0.0016299 
},
{
 "date":   5755,
"name": "GSPC.Close",
"price": 183.22,
"rsi": 48.969,
"ret": -0.0061836 
},
{
 "date":   5758,
"name": "GSPC.Close",
"price": 181.87,
"rsi": 45.384,
"ret": -0.0073682 
},
{
 "date":   5759,
"name": "GSPC.Close",
"price": 181.87,
"rsi": 41.509,
"ret":      0 
},
{
 "date":   5760,
"name": "GSPC.Close",
"price": 182.52,
"rsi": 41.509,
"ret": 0.003574 
},
{
 "date":   5761,
"name": "GSPC.Close",
"price": 182.78,
"rsi": 44.171,
"ret": 0.0014245 
},
{
 "date":   5762,
"name": "GSPC.Close",
"price": 184.28,
"rsi": 45.244,
"ret": 0.0082066 
},
{
 "date":   5765,
"name": "GSPC.Close",
"price": 186.37,
"rsi": 51.088,
"ret": 0.011341 
},
{
 "date":   5766,
"name": "GSPC.Close",
"price": 186.08,
"rsi": 57.839,
"ret": -0.001556 
},
{
 "date":   5767,
"name": "GSPC.Close",
"price": 187.98,
"rsi":  56.67,
"ret": 0.010211 
},
{
 "date":   5768,
"name": "GSPC.Close",
"price": 187.66,
"rsi": 62.077,
"ret": -0.0017023 
},
{
 "date":   5769,
"name": "GSPC.Close",
"price": 187.04,
"rsi": 60.703,
"ret": -0.0033038 
},
{
 "date":   5772,
"name": "GSPC.Close",
"price": 186.96,
"rsi": 58.024,
"ret": -0.00042772 
},
{
 "date":   5773,
"name": "GSPC.Close",
"price": 188.04,
"rsi":  57.67,
"ret": 0.0057766 
},
{
 "date":   5774,
"name": "GSPC.Close",
"price": 189.09,
"rsi": 61.116,
"ret": 0.0055839 
},
{
 "date":   5775,
"name": "GSPC.Close",
"price":  188.5,
"rsi": 64.171,
"ret": -0.0031202 
},
{
 "date":   5776,
"name": "GSPC.Close",
"price": 187.52,
"rsi": 61.259,
"ret": -0.0051989 
},
{
 "date":   5779,
"name": "GSPC.Close",
"price": 187.76,
"rsi":  56.66,
"ret": 0.0012799 
},
{
 "date":   5780,
"name": "GSPC.Close",
"price": 189.23,
"rsi": 57.501,
"ret": 0.0078291 
},
{
 "date":   5781,
"name": "GSPC.Close",
"price": 190.07,
"rsi": 62.326,
"ret": 0.004439 
},
{
 "date":   5782,
"name": "GSPC.Close",
"price": 189.82,
"rsi": 64.786,
"ret": -0.0013153 
},
{
 "date":   5783,
"name": "GSPC.Close",
"price": 191.53,
"rsi": 63.458,
"ret": 0.0090085 
},
{
 "date":   5786,
"name": "GSPC.Close",
"price": 191.25,
"rsi": 68.252,
"ret": -0.0014619 
},
{
 "date":   5787,
"name": "GSPC.Close",
"price": 192.37,
"rsi": 66.709,
"ret": 0.0058562 
},
{
 "date":   5788,
"name": "GSPC.Close",
"price": 192.76,
"rsi": 69.664,
"ret": 0.0020273 
},
{
 "date":   5789,
"name": "GSPC.Close",
"price": 192.62,
"rsi": 70.641,
"ret": -0.00072629 
},
{
 "date":   5790,
"name": "GSPC.Close",
"price": 193.72,
"rsi": 69.772,
"ret": 0.0057107 
},
{
 "date":   5793,
"name": "GSPC.Close",
"price": 197.28,
"rsi": 72.622,
"ret": 0.018377 
},
{
 "date":   5794,
"name": "GSPC.Close",
"price": 198.08,
"rsi": 79.392,
"ret": 0.0040552 
},
{
 "date":   5795,
"name": "GSPC.Close",
"price":  197.1,
"rsi": 80.556,
"ret": -0.0049475 
},
{
 "date":   5796,
"name": "GSPC.Close",
"price": 199.06,
"rsi": 74.971,
"ret": 0.0099442 
},
{
 "date":   5797,
"name": "GSPC.Close",
"price": 198.11,
"rsi": 78.223,
"ret": -0.0047724 
},
{
 "date":   5800,
"name": "GSPC.Close",
"price": 198.71,
"rsi": 73.255,
"ret": 0.0030286 
},
{
 "date":   5801,
"name": "GSPC.Close",
"price": 198.67,
"rsi": 74.362,
"ret": -0.0002013 
},
{
 "date":   5802,
"name": "GSPC.Close",
"price": 198.99,
"rsi": 74.142,
"ret": 0.0016107 
},
{
 "date":   5803,
"name": "GSPC.Close",
"price": 201.41,
"rsi": 74.786,
"ret": 0.012161 
},
{
 "date":   5804,
"name": "GSPC.Close",
"price": 201.52,
"rsi": 79.037,
"ret": 0.00054615 
},
{
 "date":   5807,
"name": "GSPC.Close",
"price": 200.35,
"rsi": 79.209,
"ret": -0.0058059 
},
{
 "date":   5808,
"name": "GSPC.Close",
"price": 200.67,
"rsi": 72.418,
"ret": 0.0015972 
},
{
 "date":   5809,
"name": "GSPC.Close",
"price": 202.54,
"rsi": 73.098,
"ret": 0.0093188 
},
{
 "date":   5811,
"name": "GSPC.Close",
"price": 202.17,
"rsi": 76.708,
"ret": -0.0018268 
},
{
 "date":   5814,
"name": "GSPC.Close",
"price": 200.46,
"rsi": 74.575,
"ret": -0.0084582 
},
{
 "date":   5815,
"name": "GSPC.Close",
"price": 200.86,
"rsi": 65.511,
"ret": 0.0019954 
},
{
 "date":   5816,
"name": "GSPC.Close",
"price": 204.23,
"rsi": 66.536,
"ret": 0.016778 
},
{
 "date":   5817,
"name": "GSPC.Close",
"price": 203.88,
"rsi": 73.641,
"ret": -0.0017138 
},
{
 "date":   5818,
"name": "GSPC.Close",
"price": 202.99,
"rsi": 71.933,
"ret": -0.0043653 
},
{
 "date":   5821,
"name": "GSPC.Close",
"price": 204.25,
"rsi": 67.636,
"ret": 0.0062072 
},
{
 "date":   5822,
"name": "GSPC.Close",
"price": 204.39,
"rsi": 70.337,
"ret": 0.00068543 
},
{
 "date":   5823,
"name": "GSPC.Close",
"price": 206.31,
"rsi": 70.631,
"ret": 0.0093938 
},
{
 "date":   5824,
"name": "GSPC.Close",
"price": 206.73,
"rsi": 74.373,
"ret": 0.0020358 
},
{
 "date":   5825,
"name": "GSPC.Close",
"price": 209.94,
"rsi":  75.12,
"ret": 0.015527 
},
{
 "date":   5828,
"name": "GSPC.Close",
"price": 212.02,
"rsi": 79.934,
"ret": 0.0099076 
},
{
 "date":   5829,
"name": "GSPC.Close",
"price": 210.65,
"rsi": 82.321,
"ret": -0.0064617 
},
{
 "date":   5830,
"name": "GSPC.Close",
"price": 209.81,
"rsi": 75.915,
"ret": -0.0039877 
},
{
 "date":   5831,
"name": "GSPC.Close",
"price": 210.02,
"rsi": 72.206,
"ret": 0.0010009 
},
{
 "date":   5832,
"name": "GSPC.Close",
"price": 210.94,
"rsi": 72.567,
"ret": 0.0043805 
},
{
 "date":   5835,
"name": "GSPC.Close",
"price": 208.57,
"rsi":  74.15,
"ret": -0.011235 
},
{
 "date":   5836,
"name": "GSPC.Close",
"price": 207.14,
"rsi": 63.914,
"ret": -0.0068562 
},
{
 "date":   5838,
"name": "GSPC.Close",
"price": 207.65,
"rsi": 58.653,
"ret": 0.0024621 
},
{
 "date":   5839,
"name": "GSPC.Close",
"price": 209.61,
"rsi":  59.92,
"ret": 0.009439 
},
{
 "date":   5842,
"name": "GSPC.Close",
"price": 210.68,
"rsi": 64.432,
"ret": 0.0051047 
},
{
 "date":   5843,
"name": "GSPC.Close",
"price": 211.28,
"rsi": 66.639,
"ret": 0.0028479 
},
{
 "date":   5845,
"name": "GSPC.Close",
"price": 209.59,
"rsi": 67.845,
"ret": -0.0079989 
},
{
 "date":   5846,
"name": "GSPC.Close",
"price": 210.88,
"rsi": 61.144,
"ret": 0.0061549 
},
{
 "date":   5849,
"name": "GSPC.Close",
"price": 210.65,
"rsi": 64.062,
"ret": -0.0010907 
},
{
 "date":   5850,
"name": "GSPC.Close",
"price":  213.8,
"rsi": 63.151,
"ret": 0.014954 
},
{
 "date":   5851,
"name": "GSPC.Close",
"price": 207.97,
"rsi": 69.537,
"ret": -0.027268 
},
{
 "date":   5852,
"name": "GSPC.Close",
"price": 206.11,
"rsi": 51.684,
"ret": -0.0089436 
},
{
 "date":   5853,
"name": "GSPC.Close",
"price": 205.96,
"rsi": 47.495,
"ret": -0.00072777 
},
{
 "date":   5856,
"name": "GSPC.Close",
"price": 206.72,
"rsi": 47.163,
"ret": 0.00369 
},
{
 "date":   5857,
"name": "GSPC.Close",
"price": 206.64,
"rsi": 49.104,
"ret": -0.000387 
},
{
 "date":   5858,
"name": "GSPC.Close",
"price": 208.26,
"rsi":   48.9,
"ret": 0.0078397 
},
{
 "date":   5859,
"name": "GSPC.Close",
"price": 209.17,
"rsi": 53.139,
"ret": 0.0043695 
},
{
 "date":   5860,
"name": "GSPC.Close",
"price": 208.43,
"rsi": 55.378,
"ret": -0.0035378 
},
{
 "date":   5863,
"name": "GSPC.Close",
"price": 207.53,
"rsi": 53.154,
"ret": -0.004318 
},
{
 "date":   5864,
"name": "GSPC.Close",
"price": 205.79,
"rsi": 50.498,
"ret": -0.0083843 
},
{
 "date":   5865,
"name": "GSPC.Close",
"price": 203.49,
"rsi": 45.738,
"ret": -0.011176 
},
{
 "date":   5866,
"name": "GSPC.Close",
"price": 204.25,
"rsi": 40.328,
"ret": 0.0037348 
},
{
 "date":   5867,
"name": "GSPC.Close",
"price": 206.43,
"rsi": 42.738,
"ret": 0.010673 
},
{
 "date":   5870,
"name": "GSPC.Close",
"price": 207.39,
"rsi": 49.091,
"ret": 0.0046505 
},
{
 "date":   5871,
"name": "GSPC.Close",
"price": 209.81,
"rsi": 51.635,
"ret": 0.011669 
},
{
 "date":   5872,
"name": "GSPC.Close",
"price": 210.29,
"rsi": 57.414,
"ret": 0.0022878 
},
{
 "date":   5873,
"name": "GSPC.Close",
"price": 209.33,
"rsi": 58.474,
"ret": -0.0045651 
},
{
 "date":   5874,
"name": "GSPC.Close",
"price": 211.78,
"rsi": 55.499,
"ret": 0.011704 
},
{
 "date":   5877,
"name": "GSPC.Close",
"price": 213.96,
"rsi": 60.958,
"ret": 0.010294 
},
{
 "date":   5878,
"name": "GSPC.Close",
"price": 212.79,
"rsi": 65.064,
"ret": -0.0054683 
},
{
 "date":   5879,
"name": "GSPC.Close",
"price": 212.96,
"rsi": 61.336,
"ret": 0.00079891 
},
{
 "date":   5880,
"name": "GSPC.Close",
"price": 213.47,
"rsi": 61.679,
"ret": 0.0023948 
},
{
 "date":   5881,
"name": "GSPC.Close",
"price": 214.56,
"rsi": 62.749,
"ret": 0.0051061 
},
{
 "date":   5884,
"name": "GSPC.Close",
"price": 216.24,
"rsi": 64.998,
"ret": 0.00783 
},
{
 "date":   5885,
"name": "GSPC.Close",
"price": 215.92,
"rsi": 68.185,
"ret": -0.0014798 
},
{
 "date":   5886,
"name": "GSPC.Close",
"price": 215.97,
"rsi": 66.935,
"ret": 0.00023157 
},
{
 "date":   5887,
"name": "GSPC.Close",
"price":  217.4,
"rsi": 67.037,
"ret": 0.0066213 
},
{
 "date":   5888,
"name": "GSPC.Close",
"price": 219.76,
"rsi":  69.89,
"ret": 0.010856 
},
{
 "date":   5892,
"name": "GSPC.Close",
"price": 222.45,
"rsi": 73.904,
"ret": 0.012241 
},
{
 "date":   5893,
"name": "GSPC.Close",
"price": 219.76,
"rsi": 77.574,
"ret": -0.012093 
},
{
 "date":   5894,
"name": "GSPC.Close",
"price": 222.22,
"rsi": 67.371,
"ret": 0.011194 
},
{
 "date":   5895,
"name": "GSPC.Close",
"price": 224.62,
"rsi": 71.113,
"ret": 0.0108 
},
{
 "date":   5898,
"name": "GSPC.Close",
"price": 224.34,
"rsi": 74.219,
"ret": -0.0012465 
},
{
 "date":   5899,
"name": "GSPC.Close",
"price": 223.79,
"rsi":  73.23,
"ret": -0.0024516 
},
{
 "date":   5900,
"name": "GSPC.Close",
"price": 224.04,
"rsi": 71.221,
"ret": 0.0011171 
},
{
 "date":   5901,
"name": "GSPC.Close",
"price": 226.77,
"rsi": 71.603,
"ret": 0.012185 
},
{
 "date":   5902,
"name": "GSPC.Close",
"price": 226.92,
"rsi":  75.43,
"ret": 0.00066146 
},
{
 "date":   5905,
"name": "GSPC.Close",
"price": 225.42,
"rsi": 75.625,
"ret": -0.0066103 
},
{
 "date":   5906,
"name": "GSPC.Close",
"price": 224.38,
"rsi": 69.686,
"ret": -0.0046136 
},
{
 "date":   5907,
"name": "GSPC.Close",
"price": 224.34,
"rsi": 65.827,
"ret": -0.00017827 
},
{
 "date":   5908,
"name": "GSPC.Close",
"price": 225.13,
"rsi": 65.676,
"ret": 0.0035214 
},
{
 "date":   5909,
"name": "GSPC.Close",
"price": 225.57,
"rsi":  67.27,
"ret": 0.0019544 
},
{
 "date":   5912,
"name": "GSPC.Close",
"price": 226.58,
"rsi": 68.156,
"ret": 0.0044775 
},
{
 "date":   5913,
"name": "GSPC.Close",
"price": 231.69,
"rsi": 70.155,
"ret": 0.022553 
},
{
 "date":   5914,
"name": "GSPC.Close",
"price": 232.54,
"rsi":  77.76,
"ret": 0.0036687 
},
{
 "date":   5915,
"name": "GSPC.Close",
"price": 233.19,
"rsi": 78.731,
"ret": 0.0027952 
},
{
 "date":   5916,
"name": "GSPC.Close",
"price": 236.55,
"rsi": 79.469,
"ret": 0.014409 
},
{
 "date":   5919,
"name": "GSPC.Close",
"price": 234.67,
"rsi": 82.793,
"ret": -0.0079476 
},
{
 "date":   5920,
"name": "GSPC.Close",
"price": 235.78,
"rsi": 75.434,
"ret": 0.00473 
},
{
 "date":   5921,
"name": "GSPC.Close",
"price":  235.6,
"rsi": 76.748,
"ret": -0.00076342 
},
{
 "date":   5922,
"name": "GSPC.Close",
"price": 236.54,
"rsi": 76.038,
"ret": 0.0039898 
},
{
 "date":   5923,
"name": "GSPC.Close",
"price": 233.34,
"rsi": 77.223,
"ret": -0.013528 
},
{
 "date":   5926,
"name": "GSPC.Close",
"price": 235.33,
"rsi": 65.366,
"ret": 0.0085283 
},
{
 "date":   5927,
"name": "GSPC.Close",
"price": 234.72,
"rsi": 68.595,
"ret": -0.0025921 
},
{
 "date":   5928,
"name": "GSPC.Close",
"price":  237.3,
"rsi": 66.547,
"ret": 0.010992 
},
{
 "date":   5929,
"name": "GSPC.Close",
"price": 238.97,
"rsi": 70.552,
"ret": 0.0070375 
},
{
 "date":   5933,
"name": "GSPC.Close",
"price":  238.9,
"rsi": 72.821,
"ret": -0.00029292 
},
{
 "date":   5934,
"name": "GSPC.Close",
"price": 235.14,
"rsi": 72.568,
"ret": -0.015739 
},
{
 "date":   5935,
"name": "GSPC.Close",
"price": 235.71,
"rsi": 60.451,
"ret": 0.0024241 
},
{
 "date":   5936,
"name": "GSPC.Close",
"price": 232.47,
"rsi": 61.501,
"ret": -0.013746 
},
{
 "date":   5937,
"name": "GSPC.Close",
"price": 228.69,
"rsi": 52.906,
"ret": -0.01626 
},
{
 "date":   5940,
"name": "GSPC.Close",
"price": 228.63,
"rsi": 45.005,
"ret": -0.00026236 
},
{
 "date":   5941,
"name": "GSPC.Close",
"price": 233.52,
"rsi":  44.89,
"ret": 0.021388 
},
{
 "date":   5942,
"name": "GSPC.Close",
"price": 233.75,
"rsi": 54.957,
"ret": 0.00098493 
},
{
 "date":   5943,
"name": "GSPC.Close",
"price": 236.44,
"rsi":  55.37,
"ret": 0.011508 
},
{
 "date":   5944,
"name": "GSPC.Close",
"price": 235.97,
"rsi": 59.991,
"ret": -0.0019878 
},
{
 "date":   5947,
"name": "GSPC.Close",
"price": 237.28,
"rsi": 58.844,
"ret": 0.0055516 
},
{
 "date":   5948,
"name": "GSPC.Close",
"price": 237.73,
"rsi": 61.077,
"ret": 0.0018965 
},
{
 "date":   5949,
"name": "GSPC.Close",
"price": 242.22,
"rsi": 61.842,
"ret": 0.018887 
},
{
 "date":   5950,
"name": "GSPC.Close",
"price": 243.03,
"rsi":   68.5,
"ret": 0.0033441 
},
{
 "date":   5951,
"name": "GSPC.Close",
"price": 242.38,
"rsi": 69.533,
"ret": -0.0026746 
},
{
 "date":   5954,
"name": "GSPC.Close",
"price": 244.74,
"rsi": 67.617,
"ret": 0.0097368 
},
{
 "date":   5955,
"name": "GSPC.Close",
"price": 242.42,
"rsi": 70.767,
"ret": -0.0094794 
},
{
 "date":   5956,
"name": "GSPC.Close",
"price": 241.75,
"rsi":  64.16,
"ret": -0.0027638 
},
{
 "date":   5957,
"name": "GSPC.Close",
"price": 242.02,
"rsi":  62.35,
"ret": 0.0011169 
},
{
 "date":   5958,
"name": "GSPC.Close",
"price": 242.29,
"rsi": 62.806,
"ret": 0.0011156 
},
{
 "date":   5961,
"name": "GSPC.Close",
"price": 243.08,
"rsi": 63.284,
"ret": 0.0032606 
},
{
 "date":   5962,
"name": "GSPC.Close",
"price": 240.51,
"rsi": 64.714,
"ret": -0.010573 
},
{
 "date":   5963,
"name": "GSPC.Close",
"price": 235.52,
"rsi": 56.945,
"ret": -0.020748 
},
{
 "date":   5964,
"name": "GSPC.Close",
"price": 235.16,
"rsi": 45.518,
"ret": -0.0015285 
},
{
 "date":   5965,
"name": "GSPC.Close",
"price": 234.79,
"rsi": 44.819,
"ret": -0.0015734 
},
{
 "date":   5968,
"name": "GSPC.Close",
"price": 237.73,
"rsi": 44.071,
"ret": 0.012522 
},
{
 "date":   5969,
"name": "GSPC.Close",
"price": 237.24,
"rsi": 51.066,
"ret": -0.0020612 
},
{
 "date":   5970,
"name": "GSPC.Close",
"price": 236.08,
"rsi": 49.945,
"ret": -0.0048896 
},
{
 "date":   5971,
"name": "GSPC.Close",
"price": 237.13,
"rsi": 47.297,
"ret": 0.0044476 
},
{
 "date":   5972,
"name": "GSPC.Close",
"price": 237.85,
"rsi": 49.887,
"ret": 0.0030363 
},
{
 "date":   5975,
"name": "GSPC.Close",
"price": 237.58,
"rsi": 51.642,
"ret": -0.0011352 
},
{
 "date":   5976,
"name": "GSPC.Close",
"price": 236.41,
"rsi": 50.922,
"ret": -0.0049247 
},
{
 "date":   5977,
"name": "GSPC.Close",
"price": 237.54,
"rsi": 47.811,
"ret": 0.0047798 
},
{
 "date":   5978,
"name": "GSPC.Close",
"price": 234.43,
"rsi": 50.929,
"ret": -0.013093 
},
{
 "date":   5979,
"name": "GSPC.Close",
"price": 232.76,
"rsi": 43.267,
"ret": -0.0071237 
},
{
 "date":   5982,
"name": "GSPC.Close",
"price":  233.2,
"rsi": 39.804,
"ret": 0.0018904 
},
{
 "date":   5983,
"name": "GSPC.Close",
"price": 236.11,
"rsi": 41.141,
"ret": 0.012479 
},
{
 "date":   5984,
"name": "GSPC.Close",
"price": 235.45,
"rsi": 49.178,
"ret": -0.0027953 
},
{
 "date":   5985,
"name": "GSPC.Close",
"price": 240.12,
"rsi": 47.591,
"ret": 0.019834 
},
{
 "date":   5986,
"name": "GSPC.Close",
"price": 241.35,
"rsi": 57.937,
"ret": 0.0051224 
},
{
 "date":   5990,
"name": "GSPC.Close",
"price": 244.75,
"rsi": 60.167,
"ret": 0.014087 
},
{
 "date":   5991,
"name": "GSPC.Close",
"price": 246.63,
"rsi": 65.597,
"ret": 0.0076813 
},
{
 "date":   5992,
"name": "GSPC.Close",
"price": 247.98,
"rsi":  68.18,
"ret": 0.0054738 
},
{
 "date":   5993,
"name": "GSPC.Close",
"price": 247.35,
"rsi": 69.927,
"ret": -0.0025405 
},
{
 "date":   5996,
"name": "GSPC.Close",
"price": 245.04,
"rsi":  68.05,
"ret": -0.009339 
},
{
 "date":   5997,
"name": "GSPC.Close",
"price": 245.51,
"rsi": 61.529,
"ret": 0.0019181 
},
{
 "date":   5998,
"name": "GSPC.Close",
"price": 243.94,
"rsi":  62.32,
"ret": -0.0063949 
},
{
 "date":   5999,
"name": "GSPC.Close",
"price": 245.65,
"rsi": 58.027,
"ret": 0.0070099 
},
{
 "date":   6000,
"name": "GSPC.Close",
"price": 245.67,
"rsi": 61.165,
"ret": 8.1417e-05 
},
{
 "date":   6003,
"name": "GSPC.Close",
"price": 239.96,
"rsi": 61.202,
"ret": -0.023243 
},
{
 "date":   6004,
"name": "GSPC.Close",
"price": 239.58,
"rsi": 47.471,
"ret": -0.0015836 
},
{
 "date":   6005,
"name": "GSPC.Close",
"price": 241.13,
"rsi":  46.72,
"ret": 0.0064697 
},
{
 "date":   6006,
"name": "GSPC.Close",
"price": 241.49,
"rsi": 50.183,
"ret": 0.001493 
},
{
 "date":   6007,
"name": "GSPC.Close",
"price": 245.73,
"rsi":  50.98,
"ret": 0.017558 
},
{
 "date":   6010,
"name": "GSPC.Close",
"price": 246.13,
"rsi": 59.248,
"ret": 0.0016278 
},
{
 "date":   6011,
"name": "GSPC.Close",
"price": 244.35,
"rsi": 59.935,
"ret": -0.007232 
},
{
 "date":   6012,
"name": "GSPC.Close",
"price": 244.99,
"rsi": 55.457,
"ret": 0.0026192 
},
{
 "date":   6013,
"name": "GSPC.Close",
"price": 244.06,
"rsi": 56.709,
"ret": -0.0037961 
},
{
 "date":   6014,
"name": "GSPC.Close",
"price": 247.58,
"rsi":  54.32,
"ret": 0.014423 
},
{
 "date":   6017,
"name": "GSPC.Close",
"price": 245.26,
"rsi": 61.016,
"ret": -0.0093707 
},
{
 "date":   6018,
"name": "GSPC.Close",
"price": 247.03,
"rsi": 55.266,
"ret": 0.0072168 
},
{
 "date":   6019,
"name": "GSPC.Close",
"price": 248.93,
"rsi": 58.481,
"ret": 0.0076914 
},
{
 "date":   6020,
"name": "GSPC.Close",
"price": 248.74,
"rsi": 61.665,
"ret": -0.00076327 
},
{
 "date":   6021,
"name": "GSPC.Close",
"price":  249.6,
"rsi":  61.16,
"ret": 0.0034574 
},
{
 "date":   6024,
"name": "GSPC.Close",
"price": 250.84,
"rsi": 62.652,
"ret": 0.0049679 
},
{
 "date":   6025,
"name": "GSPC.Close",
"price": 252.04,
"rsi": 64.754,
"ret": 0.0047839 
},
{
 "date":   6026,
"name": "GSPC.Close",
"price":  252.7,
"rsi": 66.706,
"ret": 0.0026186 
},
{
 "date":   6027,
"name": "GSPC.Close",
"price": 251.79,
"rsi": 67.764,
"ret": -0.0036011 
},
{
 "date":   6031,
"name": "GSPC.Close",
"price": 244.05,
"rsi": 64.711,
"ret": -0.03074 
},
{
 "date":   6032,
"name": "GSPC.Close",
"price": 241.59,
"rsi": 45.808,
"ret": -0.01008 
},
{
 "date":   6033,
"name": "GSPC.Close",
"price": 242.82,
"rsi": 41.644,
"ret": 0.0050913 
},
{
 "date":   6034,
"name": "GSPC.Close",
"price": 243.01,
"rsi": 44.367,
"ret": 0.00078247 
},
{
 "date":   6035,
"name": "GSPC.Close",
"price": 242.22,
"rsi": 44.796,
"ret": -0.0032509 
},
{
 "date":   6038,
"name": "GSPC.Close",
"price": 238.11,
"rsi": 43.302,
"ret": -0.016968 
},
{
 "date":   6039,
"name": "GSPC.Close",
"price": 233.66,
"rsi": 36.487,
"ret": -0.018689 
},
{
 "date":   6040,
"name": "GSPC.Close",
"price": 235.01,
"rsi": 30.829,
"ret": 0.0057776 
},
{
 "date":   6041,
"name": "GSPC.Close",
"price": 236.07,
"rsi": 34.164,
"ret": 0.0045104 
},
{
 "date":   6042,
"name": "GSPC.Close",
"price": 236.36,
"rsi": 36.743,
"ret": 0.0012284 
},
{
 "date":   6045,
"name": "GSPC.Close",
"price": 236.24,
"rsi": 37.465,
"ret": -0.0005077 
},
{
 "date":   6046,
"name": "GSPC.Close",
"price": 238.18,
"rsi": 37.276,
"ret": 0.008212 
},
{
 "date":   6047,
"name": "GSPC.Close",
"price": 238.67,
"rsi": 42.353,
"ret": 0.0020573 
},
{
 "date":   6048,
"name": "GSPC.Close",
"price": 237.95,
"rsi": 43.595,
"ret": -0.0030167 
},
{
 "date":   6049,
"name": "GSPC.Close",
"price": 240.22,
"rsi": 42.158,
"ret": 0.0095398 
},
{
 "date":   6052,
"name": "GSPC.Close",
"price": 236.01,
"rsi": 47.981,
"ret": -0.017526 
},
{
 "date":   6053,
"name": "GSPC.Close",
"price": 234.55,
"rsi": 39.949,
"ret": -0.0061862 
},
{
 "date":   6054,
"name": "GSPC.Close",
"price": 236.59,
"rsi": 37.598,
"ret": 0.0086975 
},
{
 "date":   6055,
"name": "GSPC.Close",
"price": 236.12,
"rsi": 42.674,
"ret": -0.0019866 
},
{
 "date":   6056,
"name": "GSPC.Close",
"price": 234.91,
"rsi": 41.829,
"ret": -0.0051245 
},
{
 "date":   6059,
"name": "GSPC.Close",
"price": 235.99,
"rsi": 39.655,
"ret": 0.0045975 
},
{
 "date":   6060,
"name": "GSPC.Close",
"price": 237.03,
"rsi": 42.527,
"ret": 0.004407 
},
{
 "date":   6061,
"name": "GSPC.Close",
"price": 236.84,
"rsi": 45.231,
"ret": -0.00080159 
},
{
 "date":   6062,
"name": "GSPC.Close",
"price": 237.04,
"rsi": 44.816,
"ret": 0.00084445 
},
{
 "date":   6063,
"name": "GSPC.Close",
"price": 236.88,
"rsi": 45.384,
"ret": -0.00067499 
},
{
 "date":   6066,
"name": "GSPC.Close",
"price": 240.68,
"rsi": 44.985,
"ret": 0.016042 
},
{
 "date":   6067,
"name": "GSPC.Close",
"price": 243.34,
"rsi": 55.079,
"ret": 0.011052 
},
{
 "date":   6068,
"name": "GSPC.Close",
"price": 245.67,
"rsi": 60.538,
"ret": 0.0095751 
},
{
 "date":   6069,
"name": "GSPC.Close",
"price": 246.25,
"rsi": 64.596,
"ret": 0.0023609 
},
{
 "date":   6070,
"name": "GSPC.Close",
"price": 247.15,
"rsi": 65.546,
"ret": 0.0036548 
},
{
 "date":   6073,
"name": "GSPC.Close",
"price": 247.38,
"rsi": 67.024,
"ret": 0.00093061 
},
{
 "date":   6074,
"name": "GSPC.Close",
"price": 246.51,
"rsi": 67.409,
"ret": -0.0035169 
},
{
 "date":   6075,
"name": "GSPC.Close",
"price": 249.77,
"rsi": 64.349,
"ret": 0.013225 
},
{
 "date":   6076,
"name": "GSPC.Close",
"price": 249.67,
"rsi": 69.868,
"ret": -0.00040037 
},
{
 "date":   6077,
"name": "GSPC.Close",
"price": 250.19,
"rsi": 69.513,
"ret": 0.0020827 
},
{
 "date":   6080,
"name": "GSPC.Close",
"price": 247.81,
"rsi": 70.357,
"ret": -0.0095128 
},
{
 "date":   6081,
"name": "GSPC.Close",
"price": 252.84,
"rsi": 61.905,
"ret": 0.020298 
},
{
 "date":   6082,
"name": "GSPC.Close",
"price":  253.3,
"rsi": 70.085,
"ret": 0.0018193 
},
{
 "date":   6083,
"name": "GSPC.Close",
"price": 252.84,
"rsi": 70.704,
"ret": -0.001816 
},
{
 "date":   6084,
"name": "GSPC.Close",
"price": 252.93,
"rsi": 69.162,
"ret": 0.00035596 
},
{
 "date":   6088,
"name": "GSPC.Close",
"price": 248.52,
"rsi": 69.303,
"ret": -0.017436 
},
{
 "date":   6089,
"name": "GSPC.Close",
"price": 250.08,
"rsi": 55.824,
"ret": 0.0062772 
},
{
 "date":   6090,
"name": "GSPC.Close",
"price": 253.83,
"rsi": 58.871,
"ret": 0.014995 
},
{
 "date":   6091,
"name": "GSPC.Close",
"price": 250.47,
"rsi": 65.103,
"ret": -0.013237 
},
{
 "date":   6094,
"name": "GSPC.Close",
"price": 248.14,
"rsi": 56.799,
"ret": -0.0093025 
},
{
 "date":   6095,
"name": "GSPC.Close",
"price": 247.67,
"rsi": 51.859,
"ret": -0.0018941 
},
{
 "date":   6096,
"name": "GSPC.Close",
"price": 247.06,
"rsi": 50.897,
"ret": -0.002463 
},
{
 "date":   6097,
"name": "GSPC.Close",
"price": 235.18,
"rsi": 49.612,
"ret": -0.048085 
},
{
 "date":   6098,
"name": "GSPC.Close",
"price": 230.67,
"rsi": 32.429,
"ret": -0.019177 
},
{
 "date":   6101,
"name": "GSPC.Close",
"price": 231.94,
"rsi": 28.407,
"ret": 0.0055057 
},
{
 "date":   6102,
"name": "GSPC.Close",
"price": 231.72,
"rsi": 31.002,
"ret": -0.00094852 
},
{
 "date":   6103,
"name": "GSPC.Close",
"price": 231.68,
"rsi": 30.794,
"ret": -0.00017262 
},
{
 "date":   6104,
"name": "GSPC.Close",
"price": 232.31,
"rsi": 30.753,
"ret": 0.0027193 
},
{
 "date":   6105,
"name": "GSPC.Close",
"price": 232.21,
"rsi": 32.263,
"ret": -0.00043046 
},
{
 "date":   6108,
"name": "GSPC.Close",
"price": 234.93,
"rsi": 32.143,
"ret": 0.011714 
},
{
 "date":   6109,
"name": "GSPC.Close",
"price": 235.67,
"rsi": 38.797,
"ret": 0.0031499 
},
{
 "date":   6110,
"name": "GSPC.Close",
"price": 236.28,
"rsi": 40.506,
"ret": 0.0025884 
},
{
 "date":   6111,
"name": "GSPC.Close",
"price": 231.83,
"rsi": 41.946,
"ret": -0.018834 
},
{
 "date":   6112,
"name": "GSPC.Close",
"price": 232.23,
"rsi": 35.246,
"ret": 0.0017254 
},
{
 "date":   6115,
"name": "GSPC.Close",
"price": 229.91,
"rsi": 36.232,
"ret": -0.0099901 
},
{
 "date":   6116,
"name": "GSPC.Close",
"price": 231.32,
"rsi": 33.086,
"ret": 0.0061328 
},
{
 "date":   6117,
"name": "GSPC.Close",
"price":  233.6,
"rsi": 36.685,
"ret": 0.0098565 
},
{
 "date":   6118,
"name": "GSPC.Close",
"price": 233.92,
"rsi": 42.106,
"ret": 0.0013699 
},
{
 "date":   6119,
"name": "GSPC.Close",
"price": 233.71,
"rsi": 42.846,
"ret": -0.00089774 
},
{
 "date":   6122,
"name": "GSPC.Close",
"price": 234.78,
"rsi": 42.463,
"ret": 0.0045783 
},
{
 "date":   6123,
"name": "GSPC.Close",
"price": 234.41,
"rsi": 45.156,
"ret": -0.0015759 
},
{
 "date":   6124,
"name": "GSPC.Close",
"price": 236.68,
"rsi": 44.382,
"ret": 0.0096839 
},
{
 "date":   6125,
"name": "GSPC.Close",
"price": 235.85,
"rsi": 50.038,
"ret": -0.0035068 
},
{
 "date":   6126,
"name": "GSPC.Close",
"price": 235.48,
"rsi": 48.112,
"ret": -0.0015688 
},
{
 "date":   6129,
"name": "GSPC.Close",
"price": 235.91,
"rsi": 47.239,
"ret": 0.0018261 
},
{
 "date":   6130,
"name": "GSPC.Close",
"price": 235.37,
"rsi":  48.41,
"ret": -0.002289 
},
{
 "date":   6131,
"name": "GSPC.Close",
"price":  238.8,
"rsi": 46.999,
"ret": 0.014573 
},
{
 "date":   6132,
"name": "GSPC.Close",
"price": 239.53,
"rsi": 55.812,
"ret": 0.003057 
},
{
 "date":   6133,
"name": "GSPC.Close",
"price": 238.84,
"rsi": 57.435,
"ret": -0.0028806 
},
{
 "date":   6136,
"name": "GSPC.Close",
"price": 235.97,
"rsi": 55.365,
"ret": -0.012016 
},
{
 "date":   6137,
"name": "GSPC.Close",
"price": 235.88,
"rsi": 47.672,
"ret": -0.0003814 
},
{
 "date":   6138,
"name": "GSPC.Close",
"price": 236.26,
"rsi":  47.45,
"ret": 0.001611 
},
{
 "date":   6139,
"name": "GSPC.Close",
"price": 239.28,
"rsi": 48.543,
"ret": 0.012783 
},
{
 "date":   6140,
"name": "GSPC.Close",
"price": 238.26,
"rsi": 56.317,
"ret": -0.0042628 
},
{
 "date":   6143,
"name": "GSPC.Close",
"price": 238.77,
"rsi": 53.384,
"ret": 0.0021405 
},
{
 "date":   6144,
"name": "GSPC.Close",
"price": 239.26,
"rsi": 54.656,
"ret": 0.0020522 
},
{
 "date":   6145,
"name": "GSPC.Close",
"price": 240.94,
"rsi": 55.901,
"ret": 0.0070217 
},
{
 "date":   6146,
"name": "GSPC.Close",
"price": 243.71,
"rsi":  59.96,
"ret": 0.011497 
},
{
 "date":   6147,
"name": "GSPC.Close",
"price": 243.98,
"rsi": 65.585,
"ret": 0.0011079 
},
{
 "date":   6150,
"name": "GSPC.Close",
"price":  245.8,
"rsi": 66.085,
"ret": 0.0074596 
},
{
 "date":   6151,
"name": "GSPC.Close",
"price":  246.2,
"rsi": 69.321,
"ret": 0.0016273 
},
{
 "date":   6152,
"name": "GSPC.Close",
"price": 246.58,
"rsi": 69.999,
"ret": 0.0015435 
},
{
 "date":   6153,
"name": "GSPC.Close",
"price": 245.87,
"rsi": 70.662,
"ret": -0.0028794 
},
{
 "date":   6154,
"name": "GSPC.Close",
"price": 245.77,
"rsi": 67.654,
"ret": -0.00040672 
},
{
 "date":   6157,
"name": "GSPC.Close",
"price": 246.13,
"rsi": 67.219,
"ret": 0.0014648 
},
{
 "date":   6158,
"name": "GSPC.Close",
"price": 247.08,
"rsi": 68.015,
"ret": 0.0038597 
},
{
 "date":   6159,
"name": "GSPC.Close",
"price": 246.64,
"rsi": 70.079,
"ret": -0.0017808 
},
{
 "date":   6160,
"name": "GSPC.Close",
"price": 243.02,
"rsi": 67.894,
"ret": -0.014677 
},
{
 "date":   6161,
"name": "GSPC.Close",
"price":  244.5,
"rsi": 53.198,
"ret": 0.00609 
},
{
 "date":   6164,
"name": "GSPC.Close",
"price": 243.21,
"rsi":  57.27,
"ret": -0.0052761 
},
{
 "date":   6165,
"name": "GSPC.Close",
"price": 236.78,
"rsi": 52.946,
"ret": -0.026438 
},
{
 "date":   6166,
"name": "GSPC.Close",
"price": 237.66,
"rsi": 37.676,
"ret": 0.0037165 
},
{
 "date":   6167,
"name": "GSPC.Close",
"price": 242.05,
"rsi": 40.217,
"ret": 0.018472 
},
{
 "date":   6168,
"name": "GSPC.Close",
"price": 245.86,
"rsi":  50.96,
"ret": 0.015741 
},
{
 "date":   6171,
"name": "GSPC.Close",
"price": 247.45,
"rsi": 58.012,
"ret": 0.0064671 
},
{
 "date":   6172,
"name": "GSPC.Close",
"price": 248.17,
"rsi":  60.56,
"ret": 0.0029097 
},
{
 "date":   6173,
"name": "GSPC.Close",
"price": 248.77,
"rsi": 61.694,
"ret": 0.0024177 
},
{
 "date":   6175,
"name": "GSPC.Close",
"price": 249.22,
"rsi": 62.658,
"ret": 0.0018089 
},
{
 "date":   6178,
"name": "GSPC.Close",
"price": 249.05,
"rsi": 63.401,
"ret": -0.00068213 
},
{
 "date":   6179,
"name": "GSPC.Close",
"price":    254,
"rsi": 62.892,
"ret": 0.019876 
},
{
 "date":   6180,
"name": "GSPC.Close",
"price": 253.85,
"rsi": 70.361,
"ret": -0.00059055 
},
{
 "date":   6181,
"name": "GSPC.Close",
"price": 253.04,
"rsi": 69.902,
"ret": -0.0031909 
},
{
 "date":   6182,
"name": "GSPC.Close",
"price": 251.17,
"rsi": 67.346,
"ret": -0.0073901 
},
{
 "date":   6185,
"name": "GSPC.Close",
"price": 251.16,
"rsi": 61.734,
"ret": -3.9814e-05 
},
{
 "date":   6186,
"name": "GSPC.Close",
"price": 249.28,
"rsi": 61.705,
"ret": -0.0074853 
},
{
 "date":   6187,
"name": "GSPC.Close",
"price": 250.96,
"rsi": 56.243,
"ret": 0.0067394 
},
{
 "date":   6188,
"name": "GSPC.Close",
"price": 248.17,
"rsi": 59.678,
"ret": -0.011117 
},
{
 "date":   6189,
"name": "GSPC.Close",
"price": 247.35,
"rsi": 52.332,
"ret": -0.0033042 
},
{
 "date":   6192,
"name": "GSPC.Close",
"price": 248.21,
"rsi": 50.369,
"ret": 0.0034769 
},
{
 "date":   6193,
"name": "GSPC.Close",
"price": 250.04,
"rsi": 52.386,
"ret": 0.0073728 
},
{
 "date":   6194,
"name": "GSPC.Close",
"price": 247.56,
"rsi": 56.442,
"ret": -0.0099184 
},
{
 "date":   6195,
"name": "GSPC.Close",
"price": 246.78,
"rsi": 50.201,
"ret": -0.0031508 
},
{
 "date":   6196,
"name": "GSPC.Close",
"price": 249.73,
"rsi": 48.388,
"ret": 0.011954 
},
{
 "date":   6199,
"name": "GSPC.Close",
"price": 248.75,
"rsi": 55.005,
"ret": -0.0039242 
},
{
 "date":   6200,
"name": "GSPC.Close",
"price": 246.34,
"rsi": 52.593,
"ret": -0.0096884 
},
{
 "date":   6201,
"name": "GSPC.Close",
"price": 246.75,
"rsi":  47.12,
"ret": 0.0016644 
},
{
 "date":   6203,
"name": "GSPC.Close",
"price": 246.92,
"rsi":  48.11,
"ret": 0.00068896 
},
{
 "date":   6206,
"name": "GSPC.Close",
"price": 244.67,
"rsi": 48.539,
"ret": -0.0091123 
},
{
 "date":   6207,
"name": "GSPC.Close",
"price": 243.37,
"rsi": 43.414,
"ret": -0.0053133 
},
{
 "date":   6208,
"name": "GSPC.Close",
"price": 242.17,
"rsi": 40.737,
"ret": -0.0049308 
},
{
 "date":   6210,
"name": "GSPC.Close",
"price": 246.45,
"rsi": 38.384,
"ret": 0.017674 
},
{
 "date":   6213,
"name": "GSPC.Close",
"price": 252.19,
"rsi": 49.571,
"ret": 0.023291 
},
{
 "date":   6214,
"name": "GSPC.Close",
"price": 252.78,
"rsi": 60.047,
"ret": 0.0023395 
},
{
 "date":   6215,
"name": "GSPC.Close",
"price": 255.33,
"rsi": 60.945,
"ret": 0.010088 
},
{
 "date":   6216,
"name": "GSPC.Close",
"price": 257.28,
"rsi": 64.644,
"ret": 0.0076372 
},
{
 "date":   6217,
"name": "GSPC.Close",
"price": 258.73,
"rsi": 67.203,
"ret": 0.0056359 
},
{
 "date":   6220,
"name": "GSPC.Close",
"price":  260.3,
"rsi": 68.999,
"ret": 0.0060681 
},
{
 "date":   6221,
"name": "GSPC.Close",
"price": 259.95,
"rsi":  70.86,
"ret": -0.0013446 
},
{
 "date":   6222,
"name": "GSPC.Close",
"price": 262.64,
"rsi": 69.853,
"ret": 0.010348 
},
{
 "date":   6223,
"name": "GSPC.Close",
"price": 265.49,
"rsi": 73.025,
"ret": 0.010851 
},
{
 "date":   6224,
"name": "GSPC.Close",
"price": 266.28,
"rsi": 75.917,
"ret": 0.0029756 
},
{
 "date":   6227,
"name": "GSPC.Close",
"price": 269.34,
"rsi": 76.663,
"ret": 0.011492 
},
{
 "date":   6228,
"name": "GSPC.Close",
"price": 269.04,
"rsi": 79.336,
"ret": -0.0011138 
},
{
 "date":   6229,
"name": "GSPC.Close",
"price": 267.84,
"rsi": 78.388,
"ret": -0.0044603 
},
{
 "date":   6230,
"name": "GSPC.Close",
"price": 273.91,
"rsi": 74.551,
"ret": 0.022663 
},
{
 "date":   6231,
"name": "GSPC.Close",
"price":  270.1,
"rsi": 79.908,
"ret": -0.01391 
},
{
 "date":   6234,
"name": "GSPC.Close",
"price": 269.61,
"rsi": 69.955,
"ret": -0.0018141 
},
{
 "date":   6235,
"name": "GSPC.Close",
"price": 273.75,
"rsi": 68.768,
"ret": 0.015356 
},
{
 "date":   6236,
"name": "GSPC.Close",
"price":  275.4,
"rsi": 72.943,
"ret": 0.0060274 
},
{
 "date":   6237,
"name": "GSPC.Close",
"price": 274.24,
"rsi": 74.412,
"ret": -0.0042121 
},
{
 "date":   6238,
"name": "GSPC.Close",
"price": 274.08,
"rsi": 71.475,
"ret": -0.00058343 
},
{
 "date":   6241,
"name": "GSPC.Close",
"price": 276.45,
"rsi": 71.059,
"ret": 0.0086471 
},
{
 "date":   6242,
"name": "GSPC.Close",
"price": 275.99,
"rsi":  73.52,
"ret": -0.001664 
},
{
 "date":   6243,
"name": "GSPC.Close",
"price": 279.64,
"rsi": 72.236,
"ret": 0.013225 
},
{
 "date":   6244,
"name": "GSPC.Close",
"price": 281.16,
"rsi": 75.842,
"ret": 0.0054356 
},
{
 "date":   6245,
"name": "GSPC.Close",
"price": 280.04,
"rsi": 77.172,
"ret": -0.0039835 
},
{
 "date":   6248,
"name": "GSPC.Close",
"price": 278.16,
"rsi": 73.942,
"ret": -0.0067133 
},
{
 "date":   6249,
"name": "GSPC.Close",
"price": 275.07,
"rsi": 68.742,
"ret": -0.011109 
},
{
 "date":   6250,
"name": "GSPC.Close",
"price": 277.54,
"rsi": 61.132,
"ret": 0.0089795 
},
{
 "date":   6251,
"name": "GSPC.Close",
"price": 275.62,
"rsi": 64.514,
"ret": -0.0069179 
},
{
 "date":   6252,
"name": "GSPC.Close",
"price":  279.7,
"rsi": 60.134,
"ret": 0.014803 
},
{
 "date":   6256,
"name": "GSPC.Close",
"price": 285.49,
"rsi": 65.495,
"ret": 0.020701 
},
{
 "date":   6257,
"name": "GSPC.Close",
"price": 285.42,
"rsi": 71.377,
"ret": -0.00024519 
},
{
 "date":   6258,
"name": "GSPC.Close",
"price": 285.57,
"rsi": 71.219,
"ret": 0.00052554 
},
{
 "date":   6259,
"name": "GSPC.Close",
"price": 285.48,
"rsi": 71.365,
"ret": -0.00031516 
},
{
 "date":   6262,
"name": "GSPC.Close",
"price": 282.38,
"rsi": 71.132,
"ret": -0.010859 
},
{
 "date":   6263,
"name": "GSPC.Close",
"price": 282.88,
"rsi": 63.427,
"ret": 0.0017707 
},
{
 "date":   6264,
"name": "GSPC.Close",
"price":    284,
"rsi": 64.102,
"ret": 0.0039593 
},
{
 "date":   6265,
"name": "GSPC.Close",
"price": 282.96,
"rsi": 65.633,
"ret": -0.003662 
},
{
 "date":   6266,
"name": "GSPC.Close",
"price":  284.2,
"rsi": 62.948,
"ret": 0.0043822 
},
{
 "date":   6269,
"name": "GSPC.Close",
"price":    283,
"rsi": 64.797,
"ret": -0.0042224 
},
{
 "date":   6270,
"name": "GSPC.Close",
"price": 284.12,
"rsi": 61.594,
"ret": 0.0039576 
},
{
 "date":   6271,
"name": "GSPC.Close",
"price": 288.62,
"rsi": 63.412,
"ret": 0.015838 
},
{
 "date":   6272,
"name": "GSPC.Close",
"price": 290.52,
"rsi": 69.632,
"ret": 0.0065831 
},
{
 "date":   6273,
"name": "GSPC.Close",
"price": 290.66,
"rsi": 71.811,
"ret": 0.00048189 
},
{
 "date":   6276,
"name": "GSPC.Close",
"price":  288.3,
"rsi": 71.971,
"ret": -0.0081195 
},
{
 "date":   6277,
"name": "GSPC.Close",
"price": 290.86,
"rsi": 65.263,
"ret": 0.0088796 
},
{
 "date":   6278,
"name": "GSPC.Close",
"price": 290.31,
"rsi": 68.674,
"ret": -0.0018909 
},
{
 "date":   6279,
"name": "GSPC.Close",
"price": 291.22,
"rsi": 67.148,
"ret": 0.0031346 
},
{
 "date":   6280,
"name": "GSPC.Close",
"price": 289.89,
"rsi": 68.399,
"ret": -0.004567 
},
{
 "date":   6283,
"name": "GSPC.Close",
"price": 288.23,
"rsi": 64.532,
"ret": -0.0057263 
},
{
 "date":   6284,
"name": "GSPC.Close",
"price": 292.47,
"rsi": 59.974,
"ret": 0.01471 
},
{
 "date":   6285,
"name": "GSPC.Close",
"price": 292.78,
"rsi": 66.485,
"ret": 0.0010599 
},
{
 "date":   6286,
"name": "GSPC.Close",
"price": 294.08,
"rsi": 66.909,
"ret": 0.0044402 
},
{
 "date":   6287,
"name": "GSPC.Close",
"price": 298.17,
"rsi": 68.697,
"ret": 0.013908 
},
{
 "date":   6290,
"name": "GSPC.Close",
"price": 301.16,
"rsi":  73.54,
"ret": 0.010028 
},
{
 "date":   6291,
"name": "GSPC.Close",
"price": 301.64,
"rsi": 76.413,
"ret": 0.0015938 
},
{
 "date":   6292,
"name": "GSPC.Close",
"price": 300.38,
"rsi": 76.848,
"ret": -0.0041772 
},
{
 "date":   6293,
"name": "GSPC.Close",
"price": 300.93,
"rsi": 73.043,
"ret": 0.001831 
},
{
 "date":   6294,
"name": "GSPC.Close",
"price": 296.13,
"rsi": 73.656,
"ret": -0.015951 
},
{
 "date":   6297,
"name": "GSPC.Close",
"price":  289.2,
"rsi": 60.684,
"ret": -0.023402 
},
{
 "date":   6298,
"name": "GSPC.Close",
"price":  291.7,
"rsi": 47.638,
"ret": 0.0086445 
},
{
 "date":   6299,
"name": "GSPC.Close",
"price": 292.38,
"rsi": 51.674,
"ret": 0.0023312 
},
{
 "date":   6300,
"name": "GSPC.Close",
"price": 293.63,
"rsi": 52.741,
"ret": 0.0042753 
},
{
 "date":   6301,
"name": "GSPC.Close",
"price": 300.41,
"rsi": 54.721,
"ret": 0.02309 
},
{
 "date":   6304,
"name": "GSPC.Close",
"price": 301.95,
"rsi":  63.62,
"ret": 0.0051263 
},
{
 "date":   6305,
"name": "GSPC.Close",
"price": 296.69,
"rsi": 65.289,
"ret": -0.01742 
},
{
 "date":   6306,
"name": "GSPC.Close",
"price": 297.26,
"rsi": 55.863,
"ret": 0.0019212 
},
{
 "date":   6307,
"name": "GSPC.Close",
"price": 292.86,
"rsi": 56.594,
"ret": -0.014802 
},
{
 "date":   6308,
"name": "GSPC.Close",
"price": 292.49,
"rsi": 49.743,
"ret": -0.0012634 
},
{
 "date":   6311,
"name": "GSPC.Close",
"price": 285.62,
"rsi": 49.203,
"ret": -0.023488 
},
{
 "date":   6312,
"name": "GSPC.Close",
"price": 279.16,
"rsi": 40.435,
"ret": -0.022617 
},
{
 "date":   6313,
"name": "GSPC.Close",
"price": 284.44,
"rsi": 34.254,
"ret": 0.018914 
},
{
 "date":   6314,
"name": "GSPC.Close",
"price": 286.91,
"rsi": 42.051,
"ret": 0.0086837 
},
{
 "date":   6318,
"name": "GSPC.Close",
"price": 286.09,
"rsi": 45.318,
"ret": -0.002858 
},
{
 "date":   6319,
"name": "GSPC.Close",
"price": 293.07,
"rsi": 44.423,
"ret": 0.024398 
},
{
 "date":   6320,
"name": "GSPC.Close",
"price": 287.19,
"rsi": 52.946,
"ret": -0.020063 
},
{
 "date":   6321,
"name": "GSPC.Close",
"price": 286.82,
"rsi": 46.479,
"ret": -0.0012883 
},
{
 "date":   6322,
"name": "GSPC.Close",
"price": 281.52,
"rsi": 46.098,
"ret": -0.018478 
},
{
 "date":   6325,
"name": "GSPC.Close",
"price": 281.83,
"rsi": 40.917,
"ret": 0.0011012 
},
{
 "date":   6326,
"name": "GSPC.Close",
"price": 282.51,
"rsi": 41.332,
"ret": 0.0024128 
},
{
 "date":   6327,
"name": "GSPC.Close",
"price": 284.57,
"rsi": 42.291,
"ret": 0.0072918 
},
{
 "date":   6328,
"name": "GSPC.Close",
"price": 288.36,
"rsi":  45.21,
"ret": 0.013318 
},
{
 "date":   6329,
"name": "GSPC.Close",
"price": 288.03,
"rsi": 50.203,
"ret": -0.0011444 
},
{
 "date":   6332,
"name": "GSPC.Close",
"price": 289.36,
"rsi": 49.777,
"ret": 0.0046176 
},
{
 "date":   6333,
"name": "GSPC.Close",
"price": 295.34,
"rsi": 51.558,
"ret": 0.020666 
},
{
 "date":   6334,
"name": "GSPC.Close",
"price": 295.47,
"rsi": 58.658,
"ret": 0.00044017 
},
{
 "date":   6335,
"name": "GSPC.Close",
"price": 294.71,
"rsi": 58.799,
"ret": -0.0025722 
},
{
 "date":   6336,
"name": "GSPC.Close",
"price": 293.37,
"rsi":  57.56,
"ret": -0.0045468 
},
{
 "date":   6339,
"name": "GSPC.Close",
"price": 291.57,
"rsi": 55.345,
"ret": -0.0061356 
},
{
 "date":   6340,
"name": "GSPC.Close",
"price":  293.3,
"rsi": 52.427,
"ret": 0.0059334 
},
{
 "date":   6341,
"name": "GSPC.Close",
"price": 293.98,
"rsi": 54.889,
"ret": 0.0023184 
},
{
 "date":   6342,
"name": "GSPC.Close",
"price": 294.24,
"rsi": 55.856,
"ret": 0.00088441 
},
{
 "date":   6343,
"name": "GSPC.Close",
"price": 287.43,
"rsi": 56.242,
"ret": -0.023144 
},
{
 "date":   6346,
"name": "GSPC.Close",
"price": 286.65,
"rsi":  45.11,
"ret": -0.0027137 
},
{
 "date":   6347,
"name": "GSPC.Close",
"price": 279.62,
"rsi": 44.035,
"ret": -0.024525 
},
{
 "date":   6348,
"name": "GSPC.Close",
"price": 278.21,
"rsi": 35.762,
"ret": -0.0050426 
},
{
 "date":   6349,
"name": "GSPC.Close",
"price": 280.17,
"rsi": 34.367,
"ret": 0.007045 
},
{
 "date":   6350,
"name": "GSPC.Close",
"price": 282.16,
"rsi": 37.988,
"ret": 0.0071028 
},
{
 "date":   6354,
"name": "GSPC.Close",
"price": 289.11,
"rsi": 41.515,
"ret": 0.024631 
},
{
 "date":   6355,
"name": "GSPC.Close",
"price": 288.73,
"rsi": 51.822,
"ret": -0.0013144 
},
{
 "date":   6356,
"name": "GSPC.Close",
"price": 290.76,
"rsi": 51.289,
"ret": 0.0070308 
},
{
 "date":   6357,
"name": "GSPC.Close",
"price":  290.1,
"rsi": 54.007,
"ret": -0.0022699 
},
{
 "date":   6360,
"name": "GSPC.Close",
"price": 289.83,
"rsi": 52.972,
"ret": -0.00093071 
},
{
 "date":   6361,
"name": "GSPC.Close",
"price": 288.46,
"rsi": 52.529,
"ret": -0.0047269 
},
{
 "date":   6362,
"name": "GSPC.Close",
"price": 293.47,
"rsi": 50.231,
"ret": 0.017368 
},
{
 "date":   6363,
"name": "GSPC.Close",
"price": 295.09,
"rsi": 57.544,
"ret": 0.0055202 
},
{
 "date":   6364,
"name": "GSPC.Close",
"price": 293.45,
"rsi": 59.611,
"ret": -0.0055576 
},
{
 "date":   6367,
"name": "GSPC.Close",
"price": 296.72,
"rsi": 56.607,
"ret": 0.011143 
},
{
 "date":   6368,
"name": "GSPC.Close",
"price": 297.28,
"rsi": 60.844,
"ret": 0.0018873 
},
{
 "date":   6369,
"name": "GSPC.Close",
"price": 297.47,
"rsi": 61.537,
"ret": 0.00063913 
},
{
 "date":   6370,
"name": "GSPC.Close",
"price": 298.73,
"rsi": 61.784,
"ret": 0.0042357 
},
{
 "date":   6371,
"name": "GSPC.Close",
"price": 301.62,
"rsi": 63.459,
"ret": 0.0096743 
},
{
 "date":   6374,
"name": "GSPC.Close",
"price": 303.14,
"rsi": 67.031,
"ret": 0.0050395 
},
{
 "date":   6375,
"name": "GSPC.Close",
"price": 304.76,
"rsi":  68.76,
"ret": 0.0053441 
},
{
 "date":   6376,
"name": "GSPC.Close",
"price": 304.81,
"rsi": 70.534,
"ret": 0.00016406 
},
{
 "date":   6377,
"name": "GSPC.Close",
"price": 305.69,
"rsi":  70.59,
"ret": 0.002887 
},
{
 "date":   6378,
"name": "GSPC.Close",
"price": 306.97,
"rsi": 71.604,
"ret": 0.0041872 
},
{
 "date":   6381,
"name": "GSPC.Close",
"price": 309.65,
"rsi": 73.059,
"ret": 0.0087305 
},
{
 "date":   6382,
"name": "GSPC.Close",
"price": 308.43,
"rsi": 75.849,
"ret": -0.0039399 
},
{
 "date":   6383,
"name": "GSPC.Close",
"price": 306.86,
"rsi": 72.184,
"ret": -0.0050903 
},
{
 "date":   6384,
"name": "GSPC.Close",
"price": 308.96,
"rsi": 67.653,
"ret": 0.0068435 
},
{
 "date":   6385,
"name": "GSPC.Close",
"price": 307.16,
"rsi": 70.335,
"ret": -0.005826 
},
{
 "date":   6388,
"name": "GSPC.Close",
"price":  307.9,
"rsi": 65.335,
"ret": 0.0024092 
},
{
 "date":   6389,
"name": "GSPC.Close",
"price":    304,
"rsi": 66.393,
"ret": -0.012666 
},
{
 "date":   6390,
"name": "GSPC.Close",
"price": 302.94,
"rsi": 56.592,
"ret": -0.0034868 
},
{
 "date":   6391,
"name": "GSPC.Close",
"price": 305.63,
"rsi": 54.248,
"ret": 0.0088796 
},
{
 "date":   6395,
"name": "GSPC.Close",
"price": 304.92,
"rsi":   58.9,
"ret": -0.0023231 
},
{
 "date":   6396,
"name": "GSPC.Close",
"price":  307.4,
"rsi": 57.245,
"ret": 0.0081333 
},
{
 "date":   6397,
"name": "GSPC.Close",
"price": 308.29,
"rsi": 61.332,
"ret": 0.0028953 
},
{
 "date":   6398,
"name": "GSPC.Close",
"price": 307.52,
"rsi": 62.709,
"ret": -0.0024976 
},
{
 "date":   6399,
"name": "GSPC.Close",
"price": 308.37,
"rsi": 60.695,
"ret": 0.002764 
},
{
 "date":   6402,
"name": "GSPC.Close",
"price": 307.63,
"rsi":  62.14,
"ret": -0.0023997 
},
{
 "date":   6403,
"name": "GSPC.Close",
"price": 310.68,
"rsi": 60.069,
"ret": 0.0099145 
},
{
 "date":   6404,
"name": "GSPC.Close",
"price": 310.42,
"rsi": 65.216,
"ret": -0.00083687 
},
{
 "date":   6405,
"name": "GSPC.Close",
"price":  312.7,
"rsi": 64.453,
"ret": 0.0073449 
},
{
 "date":   6406,
"name": "GSPC.Close",
"price": 314.59,
"rsi": 67.989,
"ret": 0.0060441 
},
{
 "date":   6409,
"name": "GSPC.Close",
"price": 311.39,
"rsi": 70.599,
"ret": -0.010172 
},
{
 "date":   6410,
"name": "GSPC.Close",
"price": 308.55,
"rsi":  61.46,
"ret": -0.0091204 
},
{
 "date":   6411,
"name": "GSPC.Close",
"price": 308.47,
"rsi": 54.694,
"ret": -0.00025928 
},
{
 "date":   6412,
"name": "GSPC.Close",
"price": 307.81,
"rsi": 54.512,
"ret": -0.0021396 
},
{
 "date":   6413,
"name": "GSPC.Close",
"price": 309.27,
"rsi": 52.946,
"ret": 0.0047432 
},
{
 "date":   6416,
"name": "GSPC.Close",
"price": 310.65,
"rsi":  55.96,
"ret": 0.0044621 
},
{
 "date":   6417,
"name": "GSPC.Close",
"price": 312.33,
"rsi": 58.655,
"ret": 0.005408 
},
{
 "date":   6418,
"name": "GSPC.Close",
"price": 315.65,
"rsi": 61.726,
"ret": 0.01063 
},
{
 "date":   6419,
"name": "GSPC.Close",
"price": 318.05,
"rsi": 66.951,
"ret": 0.0076034 
},
{
 "date":   6420,
"name": "GSPC.Close",
"price": 318.66,
"rsi": 70.126,
"ret": 0.0019179 
},
{
 "date":   6423,
"name": "GSPC.Close",
"price": 317.57,
"rsi": 70.891,
"ret": -0.0034206 
},
{
 "date":   6424,
"name": "GSPC.Close",
"price": 316.23,
"rsi":  67.56,
"ret": -0.0042195 
},
{
 "date":   6425,
"name": "GSPC.Close",
"price": 318.45,
"rsi": 63.604,
"ret": 0.0070202 
},
{
 "date":   6426,
"name": "GSPC.Close",
"price": 322.09,
"rsi": 67.047,
"ret": 0.01143 
},
{
 "date":   6427,
"name": "GSPC.Close",
"price":    323,
"rsi": 71.764,
"ret": 0.0028253 
},
{
 "date":   6430,
"name": "GSPC.Close",
"price":    328,
"rsi": 72.811,
"ret": 0.01548 
},
{
 "date":   6431,
"name": "GSPC.Close",
"price": 333.33,
"rsi": 77.706,
"ret": 0.01625 
},
{
 "date":   6432,
"name": "GSPC.Close",
"price": 332.39,
"rsi": 81.525,
"ret": -0.00282 
},
{
 "date":   6433,
"name": "GSPC.Close",
"price": 334.65,
"rsi": 78.956,
"ret": 0.0067992 
},
{
 "date":   6434,
"name": "GSPC.Close",
"price": 333.99,
"rsi": 80.543,
"ret": -0.0019722 
},
{
 "date":   6437,
"name": "GSPC.Close",
"price": 334.11,
"rsi": 78.677,
"ret": 0.00035929 
},
{
 "date":   6438,
"name": "GSPC.Close",
"price": 329.25,
"rsi": 78.773,
"ret": -0.014546 
},
{
 "date":   6439,
"name": "GSPC.Close",
"price": 329.83,
"rsi":  65.81,
"ret": 0.0017616 
},
{
 "date":   6440,
"name": "GSPC.Close",
"price": 334.84,
"rsi": 66.518,
"ret": 0.01519 
},
{
 "date":   6441,
"name": "GSPC.Close",
"price":  335.9,
"rsi": 71.927,
"ret": 0.0031657 
},
{
 "date":   6444,
"name": "GSPC.Close",
"price": 333.33,
"rsi": 72.924,
"ret": -0.0076511 
},
{
 "date":   6445,
"name": "GSPC.Close",
"price": 336.77,
"rsi": 66.737,
"ret": 0.01032 
},
{
 "date":   6446,
"name": "GSPC.Close",
"price": 334.57,
"rsi": 70.362,
"ret": -0.0065326 
},
{
 "date":   6447,
"name": "GSPC.Close",
"price": 331.38,
"rsi":  65.45,
"ret": -0.0095346 
},
{
 "date":   6448,
"name": "GSPC.Close",
"price": 327.04,
"rsi": 59.017,
"ret": -0.013097 
},
{
 "date":   6451,
"name": "GSPC.Close",
"price":  329.8,
"rsi": 51.588,
"ret": 0.0084393 
},
{
 "date":   6452,
"name": "GSPC.Close",
"price":  323.4,
"rsi":  55.43,
"ret": -0.019406 
},
{
 "date":   6453,
"name": "GSPC.Close",
"price": 321.68,
"rsi": 46.261,
"ret": -0.0053185 
},
{
 "date":   6454,
"name": "GSPC.Close",
"price": 320.21,
"rsi": 44.147,
"ret": -0.0045698 
},
{
 "date":   6455,
"name": "GSPC.Close",
"price":  316.7,
"rsi": 42.366,
"ret": -0.010962 
},
{
 "date":   6459,
"name": "GSPC.Close",
"price": 313.56,
"rsi": 38.383,
"ret": -0.0099147 
},
{
 "date":   6460,
"name": "GSPC.Close",
"price": 313.92,
"rsi": 35.195,
"ret": 0.0011481 
},
{
 "date":   6461,
"name": "GSPC.Close",
"price": 317.13,
"rsi": 35.853,
"ret": 0.010226 
},
{
 "date":   6462,
"name": "GSPC.Close",
"price": 321.98,
"rsi":  41.55,
"ret": 0.015293 
},
{
 "date":   6465,
"name": "GSPC.Close",
"price": 323.08,
"rsi":  48.93,
"ret": 0.0034164 
},
{
 "date":   6466,
"name": "GSPC.Close",
"price": 317.74,
"rsi": 50.458,
"ret": -0.016528 
},
{
 "date":   6467,
"name": "GSPC.Close",
"price": 314.86,
"rsi": 43.633,
"ret": -0.009064 
},
{
 "date":   6468,
"name": "GSPC.Close",
"price": 314.93,
"rsi": 40.455,
"ret": 0.00022232 
},
{
 "date":   6469,
"name": "GSPC.Close",
"price": 314.86,
"rsi": 40.569,
"ret": -0.00022227 
},
{
 "date":   6472,
"name": "GSPC.Close",
"price": 310.54,
"rsi": 40.486,
"ret": -0.01372 
},
{
 "date":   6473,
"name": "GSPC.Close",
"price":  319.5,
"rsi": 35.642,
"ret": 0.028853 
},
{
 "date":   6474,
"name": "GSPC.Close",
"price": 321.19,
"rsi": 49.214,
"ret": 0.0052895 
},
{
 "date":   6475,
"name": "GSPC.Close",
"price": 319.72,
"rsi":   51.3,
"ret": -0.0045767 
},
{
 "date":   6476,
"name": "GSPC.Close",
"price": 320.16,
"rsi":   49.4,
"ret": 0.0013762 
},
{
 "date":   6479,
"name": "GSPC.Close",
"price":  323.2,
"rsi": 49.997,
"ret": 0.0094953 
},
{
 "date":   6480,
"name": "GSPC.Close",
"price": 321.69,
"rsi": 54.034,
"ret": -0.004672 
},
{
 "date":   6481,
"name": "GSPC.Close",
"price": 321.83,
"rsi": 51.797,
"ret": 0.0004352 
},
{
 "date":   6482,
"name": "GSPC.Close",
"price": 327.33,
"rsi": 51.995,
"ret": 0.01709 
},
{
 "date":   6483,
"name": "GSPC.Close",
"price": 328.07,
"rsi": 59.115,
"ret": 0.0022607 
},
{
 "date":   6486,
"name": "GSPC.Close",
"price": 328.08,
"rsi": 59.975,
"ret": 3.0481e-05 
},
{
 "date":   6487,
"name": "GSPC.Close",
"price": 319.22,
"rsi": 59.988,
"ret": -0.027006 
},
{
 "date":   6488,
"name": "GSPC.Close",
"price": 318.54,
"rsi": 46.428,
"ret": -0.0021302 
},
{
 "date":   6489,
"name": "GSPC.Close",
"price": 314.16,
"rsi": 45.577,
"ret": -0.01375 
},
{
 "date":   6490,
"name": "GSPC.Close",
"price": 311.07,
"rsi": 40.433,
"ret": -0.0098358 
},
{
 "date":   6493,
"name": "GSPC.Close",
"price": 309.39,
"rsi":  37.24,
"ret": -0.0054007 
},
{
 "date":   6494,
"name": "GSPC.Close",
"price": 314.52,
"rsi": 35.594,
"ret": 0.016581 
},
{
 "date":   6495,
"name": "GSPC.Close",
"price": 305.23,
"rsi": 43.767,
"ret": -0.029537 
},
{
 "date":   6496,
"name": "GSPC.Close",
"price": 298.08,
"rsi": 35.084,
"ret": -0.023425 
},
{
 "date":   6497,
"name": "GSPC.Close",
"price":  282.7,
"rsi":  30.13,
"ret": -0.051597 
},
{
 "date":   6500,
"name": "GSPC.Close",
"price": 224.84,
"rsi": 22.704,
"ret": -0.20467 
},
{
 "date":   6501,
"name": "GSPC.Close",
"price": 236.83,
"rsi":  11.36,
"ret": 0.053327 
},
{
 "date":   6502,
"name": "GSPC.Close",
"price": 258.38,
"rsi": 20.252,
"ret": 0.090994 
},
{
 "date":   6503,
"name": "GSPC.Close",
"price": 248.25,
"rsi": 33.219,
"ret": -0.039206 
},
{
 "date":   6504,
"name": "GSPC.Close",
"price": 248.22,
"rsi": 30.693,
"ret": -0.00012085 
},
{
 "date":   6507,
"name": "GSPC.Close",
"price": 227.67,
"rsi": 30.685,
"ret": -0.082789 
},
{
 "date":   6508,
"name": "GSPC.Close",
"price": 233.19,
"rsi": 26.029,
"ret": 0.024246 
},
{
 "date":   6509,
"name": "GSPC.Close",
"price": 233.28,
"rsi": 29.139,
"ret": 0.00038595 
},
{
 "date":   6510,
"name": "GSPC.Close",
"price": 244.77,
"rsi": 29.192,
"ret": 0.049254 
},
{
 "date":   6511,
"name": "GSPC.Close",
"price": 251.79,
"rsi": 35.713,
"ret": 0.02868 
},
{
 "date":   6514,
"name": "GSPC.Close",
"price": 255.75,
"rsi": 39.386,
"ret": 0.015727 
},
{
 "date":   6515,
"name": "GSPC.Close",
"price": 250.82,
"rsi": 41.419,
"ret": -0.019277 
},
{
 "date":   6516,
"name": "GSPC.Close",
"price": 248.96,
"rsi": 39.636,
"ret": -0.0074157 
},
{
 "date":   6517,
"name": "GSPC.Close",
"price": 254.48,
"rsi": 38.955,
"ret": 0.022172 
},
{
 "date":   6518,
"name": "GSPC.Close",
"price": 250.41,
"rsi": 42.134,
"ret": -0.015993 
},
{
 "date":   6521,
"name": "GSPC.Close",
"price": 243.17,
"rsi": 40.461,
"ret": -0.028913 
},
{
 "date":   6522,
"name": "GSPC.Close",
"price":    239,
"rsi": 37.601,
"ret": -0.017148 
},
{
 "date":   6523,
"name": "GSPC.Close",
"price":  241.9,
"rsi": 36.022,
"ret": 0.012134 
},
{
 "date":   6524,
"name": "GSPC.Close",
"price": 248.52,
"rsi": 37.973,
"ret": 0.027367 
},
{
 "date":   6525,
"name": "GSPC.Close",
"price": 245.64,
"rsi": 42.299,
"ret": -0.011589 
},
{
 "date":   6528,
"name": "GSPC.Close",
"price": 246.76,
"rsi":  40.96,
"ret": 0.0045595 
},
{
 "date":   6529,
"name": "GSPC.Close",
"price": 243.04,
"rsi": 41.733,
"ret": -0.015075 
},
{
 "date":   6530,
"name": "GSPC.Close",
"price": 245.55,
"rsi": 39.868,
"ret": 0.010328 
},
{
 "date":   6531,
"name": "GSPC.Close",
"price": 240.05,
"rsi": 41.759,
"ret": -0.022399 
},
{
 "date":   6532,
"name": "GSPC.Close",
"price":    242,
"rsi": 38.874,
"ret": 0.0081233 
},
{
 "date":   6535,
"name": "GSPC.Close",
"price": 242.99,
"rsi": 40.445,
"ret": 0.0040909 
},
{
 "date":   6536,
"name": "GSPC.Close",
"price": 246.39,
"rsi":  41.27,
"ret": 0.013992 
},
{
 "date":   6537,
"name": "GSPC.Close",
"price":  244.1,
"rsi": 44.133,
"ret": -0.0092942 
},
{
 "date":   6539,
"name": "GSPC.Close",
"price": 240.34,
"rsi": 42.626,
"ret": -0.015404 
},
{
 "date":   6542,
"name": "GSPC.Close",
"price":  230.3,
"rsi": 40.198,
"ret": -0.041774 
},
{
 "date":   6543,
"name": "GSPC.Close",
"price":    232,
"rsi": 34.541,
"ret": 0.0073817 
},
{
 "date":   6544,
"name": "GSPC.Close",
"price": 233.45,
"rsi": 36.179,
"ret": 0.00625 
},
{
 "date":   6545,
"name": "GSPC.Close",
"price": 225.21,
"rsi": 37.613,
"ret": -0.035297 
},
{
 "date":   6546,
"name": "GSPC.Close",
"price": 223.92,
"rsi": 33.066,
"ret": -0.005728 
},
{
 "date":   6549,
"name": "GSPC.Close",
"price": 228.76,
"rsi": 32.406,
"ret": 0.021615 
},
{
 "date":   6550,
"name": "GSPC.Close",
"price": 234.91,
"rsi": 37.453,
"ret": 0.026884 
},
{
 "date":   6551,
"name": "GSPC.Close",
"price": 238.89,
"rsi": 43.252,
"ret": 0.016943 
},
{
 "date":   6552,
"name": "GSPC.Close",
"price": 233.57,
"rsi": 46.696,
"ret": -0.02227 
},
{
 "date":   6553,
"name": "GSPC.Close",
"price": 235.32,
"rsi": 42.944,
"ret": 0.0074924 
},
{
 "date":   6556,
"name": "GSPC.Close",
"price": 242.19,
"rsi": 44.523,
"ret": 0.029194 
},
{
 "date":   6557,
"name": "GSPC.Close",
"price": 242.81,
"rsi": 50.334,
"ret": 0.00256 
},
{
 "date":   6558,
"name": "GSPC.Close",
"price": 248.08,
"rsi": 50.834,
"ret": 0.021704 
},
{
 "date":   6559,
"name": "GSPC.Close",
"price": 242.98,
"rsi": 54.986,
"ret": -0.020558 
},
{
 "date":   6560,
"name": "GSPC.Close",
"price": 249.16,
"rsi": 50.538,
"ret": 0.025434 
},
{
 "date":   6563,
"name": "GSPC.Close",
"price": 249.54,
"rsi": 55.261,
"ret": 0.0015251 
},
{
 "date":   6564,
"name": "GSPC.Close",
"price": 249.95,
"rsi": 55.542,
"ret": 0.001643 
},
{
 "date":   6565,
"name": "GSPC.Close",
"price": 253.16,
"rsi": 55.865,
"ret": 0.012843 
},
{
 "date":   6566,
"name": "GSPC.Close",
"price": 252.03,
"rsi": 58.406,
"ret": -0.0044636 
},
{
 "date":   6570,
"name": "GSPC.Close",
"price": 245.57,
"rsi": 57.158,
"ret": -0.025632 
},
{
 "date":   6571,
"name": "GSPC.Close",
"price": 244.59,
"rsi": 50.514,
"ret": -0.0039907 
},
{
 "date":   6572,
"name": "GSPC.Close",
"price": 247.86,
"rsi": 49.572,
"ret": 0.013369 
},
{
 "date":   6573,
"name": "GSPC.Close",
"price": 247.08,
"rsi": 52.738,
"ret": -0.0031469 
},
{
 "date":   6577,
"name": "GSPC.Close",
"price": 255.94,
"rsi": 51.901,
"ret": 0.035859 
},
{
 "date":   6578,
"name": "GSPC.Close",
"price": 258.63,
"rsi":  59.72,
"ret": 0.01051 
},
{
 "date":   6579,
"name": "GSPC.Close",
"price": 258.89,
"rsi": 61.753,
"ret": 0.0010053 
},
{
 "date":   6580,
"name": "GSPC.Close",
"price": 261.07,
"rsi": 61.953,
"ret": 0.0084206 
},
{
 "date":   6581,
"name": "GSPC.Close",
"price":  243.4,
"rsi": 63.667,
"ret": -0.067683 
},
{
 "date":   6584,
"name": "GSPC.Close",
"price": 247.49,
"rsi": 45.694,
"ret": 0.016804 
},
{
 "date":   6585,
"name": "GSPC.Close",
"price": 245.42,
"rsi": 49.264,
"ret": -0.008364 
},
{
 "date":   6586,
"name": "GSPC.Close",
"price": 245.81,
"rsi":  47.56,
"ret": 0.0015891 
},
{
 "date":   6587,
"name": "GSPC.Close",
"price": 245.88,
"rsi": 47.925,
"ret": 0.00028477 
},
{
 "date":   6588,
"name": "GSPC.Close",
"price": 252.05,
"rsi": 47.995,
"ret": 0.025094 
},
{
 "date":   6591,
"name": "GSPC.Close",
"price": 251.88,
"rsi": 53.885,
"ret": -0.00067447 
},
{
 "date":   6592,
"name": "GSPC.Close",
"price": 249.32,
"rsi": 53.704,
"ret": -0.010164 
},
{
 "date":   6593,
"name": "GSPC.Close",
"price": 242.63,
"rsi": 50.938,
"ret": -0.026833 
},
{
 "date":   6594,
"name": "GSPC.Close",
"price": 243.14,
"rsi": 44.488,
"ret": 0.002102 
},
{
 "date":   6595,
"name": "GSPC.Close",
"price":  246.5,
"rsi": 45.059,
"ret": 0.013819 
},
{
 "date":   6598,
"name": "GSPC.Close",
"price": 252.17,
"rsi": 48.797,
"ret": 0.023002 
},
{
 "date":   6599,
"name": "GSPC.Close",
"price": 249.57,
"rsi": 54.431,
"ret": -0.010311 
},
{
 "date":   6600,
"name": "GSPC.Close",
"price": 249.38,
"rsi": 51.626,
"ret": -0.00076131 
},
{
 "date":   6601,
"name": "GSPC.Close",
"price": 253.29,
"rsi": 51.417,
"ret": 0.015679 
},
{
 "date":   6602,
"name": "GSPC.Close",
"price": 257.07,
"rsi": 55.409,
"ret": 0.014924 
},
{
 "date":   6605,
"name": "GSPC.Close",
"price": 255.04,
"rsi": 58.923,
"ret": -0.0078967 
},
{
 "date":   6606,
"name": "GSPC.Close",
"price": 255.57,
"rsi": 56.354,
"ret": 0.0020781 
},
{
 "date":   6607,
"name": "GSPC.Close",
"price": 252.21,
"rsi": 56.883,
"ret": -0.013147 
},
{
 "date":   6608,
"name": "GSPC.Close",
"price": 252.21,
"rsi":  52.54,
"ret":      0 
},
{
 "date":   6609,
"name": "GSPC.Close",
"price": 250.96,
"rsi":  52.54,
"ret": -0.0049562 
},
{
 "date":   6612,
"name": "GSPC.Close",
"price":  249.1,
"rsi": 50.864,
"ret": -0.0074115 
},
{
 "date":   6613,
"name": "GSPC.Close",
"price": 251.72,
"rsi": 48.391,
"ret": 0.010518 
},
{
 "date":   6614,
"name": "GSPC.Close",
"price": 256.66,
"rsi": 51.936,
"ret": 0.019625 
},
{
 "date":   6615,
"name": "GSPC.Close",
"price": 255.95,
"rsi": 57.819,
"ret": -0.0027663 
},
{
 "date":   6616,
"name": "GSPC.Close",
"price": 257.63,
"rsi": 56.744,
"ret": 0.0065638 
},
{
 "date":   6620,
"name": "GSPC.Close",
"price": 259.83,
"rsi": 58.701,
"ret": 0.0085394 
},
{
 "date":   6621,
"name": "GSPC.Close",
"price": 259.21,
"rsi": 61.178,
"ret": -0.0023862 
},
{
 "date":   6622,
"name": "GSPC.Close",
"price": 257.91,
"rsi": 60.084,
"ret": -0.0050152 
},
{
 "date":   6623,
"name": "GSPC.Close",
"price": 261.61,
"rsi": 57.753,
"ret": 0.014346 
},
{
 "date":   6626,
"name": "GSPC.Close",
"price": 265.64,
"rsi": 62.243,
"ret": 0.015405 
},
{
 "date":   6627,
"name": "GSPC.Close",
"price": 265.02,
"rsi": 66.428,
"ret": -0.002334 
},
{
 "date":   6628,
"name": "GSPC.Close",
"price": 264.43,
"rsi":  65.23,
"ret": -0.0022262 
},
{
 "date":   6629,
"name": "GSPC.Close",
"price": 261.58,
"rsi": 64.046,
"ret": -0.010778 
},
{
 "date":   6630,
"name": "GSPC.Close",
"price": 262.46,
"rsi": 58.522,
"ret": 0.0033642 
},
{
 "date":   6633,
"name": "GSPC.Close",
"price": 267.82,
"rsi": 59.679,
"ret": 0.020422 
},
{
 "date":   6634,
"name": "GSPC.Close",
"price": 267.22,
"rsi": 65.913,
"ret": -0.0022403 
},
{
 "date":   6635,
"name": "GSPC.Close",
"price": 267.98,
"rsi": 64.707,
"ret": 0.0028441 
},
{
 "date":   6636,
"name": "GSPC.Close",
"price": 267.88,
"rsi": 65.566,
"ret": -0.00037316 
},
{
 "date":   6637,
"name": "GSPC.Close",
"price":  267.3,
"rsi": 65.341,
"ret": -0.0021651 
},
{
 "date":   6640,
"name": "GSPC.Close",
"price": 267.38,
"rsi": 63.967,
"ret": 0.00029929 
},
{
 "date":   6641,
"name": "GSPC.Close",
"price": 269.43,
"rsi": 64.079,
"ret": 0.007667 
},
{
 "date":   6642,
"name": "GSPC.Close",
"price": 269.06,
"rsi": 66.921,
"ret": -0.0013733 
},
{
 "date":   6643,
"name": "GSPC.Close",
"price": 263.84,
"rsi": 65.908,
"ret": -0.019401 
},
{
 "date":   6644,
"name": "GSPC.Close",
"price": 264.94,
"rsi": 53.578,
"ret": 0.0041692 
},
{
 "date":   6647,
"name": "GSPC.Close",
"price": 266.37,
"rsi": 55.468,
"ret": 0.0053974 
},
{
 "date":   6648,
"name": "GSPC.Close",
"price": 266.13,
"rsi":  57.87,
"ret": -0.000901 
},
{
 "date":   6649,
"name": "GSPC.Close",
"price": 268.65,
"rsi": 57.312,
"ret": 0.0094691 
},
{
 "date":   6650,
"name": "GSPC.Close",
"price": 271.22,
"rsi": 61.514,
"ret": 0.0095664 
},
{
 "date":   6651,
"name": "GSPC.Close",
"price": 271.12,
"rsi": 65.268,
"ret": -0.0003687 
},
{
 "date":   6654,
"name": "GSPC.Close",
"price": 268.74,
"rsi": 65.003,
"ret": -0.0087784 
},
{
 "date":   6655,
"name": "GSPC.Close",
"price": 268.84,
"rsi":  58.86,
"ret": 0.00037211 
},
{
 "date":   6656,
"name": "GSPC.Close",
"price": 268.91,
"rsi": 59.035,
"ret": 0.00026038 
},
{
 "date":   6657,
"name": "GSPC.Close",
"price": 263.35,
"rsi": 59.166,
"ret": -0.020676 
},
{
 "date":   6658,
"name": "GSPC.Close",
"price": 258.51,
"rsi": 46.454,
"ret": -0.018379 
},
{
 "date":   6661,
"name": "GSPC.Close",
"price": 258.06,
"rsi": 38.665,
"ret": -0.0017407 
},
{
 "date":   6662,
"name": "GSPC.Close",
"price": 260.07,
"rsi": 38.027,
"ret": 0.0077889 
},
{
 "date":   6663,
"name": "GSPC.Close",
"price": 258.07,
"rsi": 42.587,
"ret": -0.0076902 
},
{
 "date":   6664,
"name": "GSPC.Close",
"price": 258.89,
"rsi": 39.474,
"ret": 0.0031774 
},
{
 "date":   6668,
"name": "GSPC.Close",
"price": 256.09,
"rsi": 41.366,
"ret": -0.010815 
},
{
 "date":   6669,
"name": "GSPC.Close",
"price": 258.51,
"rsi": 37.102,
"ret": 0.0094498 
},
{
 "date":   6670,
"name": "GSPC.Close",
"price": 265.49,
"rsi": 42.609,
"ret": 0.027001 
},
{
 "date":   6671,
"name": "GSPC.Close",
"price": 266.16,
"rsi":  54.88,
"ret": 0.0025236 
},
{
 "date":   6672,
"name": "GSPC.Close",
"price": 269.43,
"rsi": 55.856,
"ret": 0.012286 
},
{
 "date":   6675,
"name": "GSPC.Close",
"price": 270.16,
"rsi": 60.361,
"ret": 0.0027094 
},
{
 "date":   6676,
"name": "GSPC.Close",
"price": 271.37,
"rsi":  61.31,
"ret": 0.0044788 
},
{
 "date":   6677,
"name": "GSPC.Close",
"price": 271.58,
"rsi": 62.896,
"ret": 0.00077385 
},
{
 "date":   6678,
"name": "GSPC.Close",
"price": 259.75,
"rsi": 63.178,
"ret": -0.04356 
},
{
 "date":   6679,
"name": "GSPC.Close",
"price": 259.77,
"rsi": 43.234,
"ret": 7.6997e-05 
},
{
 "date":   6682,
"name": "GSPC.Close",
"price": 259.21,
"rsi": 43.266,
"ret": -0.0021558 
},
{
 "date":   6683,
"name": "GSPC.Close",
"price": 257.92,
"rsi":  42.53,
"ret": -0.0049767 
},
{
 "date":   6684,
"name": "GSPC.Close",
"price": 256.13,
"rsi": 40.806,
"ret": -0.0069401 
},
{
 "date":   6685,
"name": "GSPC.Close",
"price": 256.42,
"rsi": 38.476,
"ret": 0.0011322 
},
{
 "date":   6686,
"name": "GSPC.Close",
"price": 260.14,
"rsi": 39.083,
"ret": 0.014507 
},
{
 "date":   6689,
"name": "GSPC.Close",
"price": 262.51,
"rsi": 46.389,
"ret": 0.0091105 
},
{
 "date":   6690,
"name": "GSPC.Close",
"price": 263.93,
"rsi": 50.465,
"ret": 0.0054093 
},
{
 "date":   6691,
"name": "GSPC.Close",
"price":  263.8,
"rsi": 52.781,
"ret": -0.00049255 
},
{
 "date":   6692,
"name": "GSPC.Close",
"price": 262.61,
"rsi": 52.539,
"ret": -0.004511 
},
{
 "date":   6693,
"name": "GSPC.Close",
"price": 261.33,
"rsi": 50.265,
"ret": -0.0048741 
},
{
 "date":   6696,
"name": "GSPC.Close",
"price": 261.56,
"rsi": 47.865,
"ret": 0.00088011 
},
{
 "date":   6697,
"name": "GSPC.Close",
"price":    263,
"rsi": 48.342,
"ret": 0.0055054 
},
{
 "date":   6698,
"name": "GSPC.Close",
"price": 260.32,
"rsi": 51.345,
"ret": -0.01019 
},
{
 "date":   6699,
"name": "GSPC.Close",
"price": 258.79,
"rsi": 45.987,
"ret": -0.0058774 
},
{
 "date":   6700,
"name": "GSPC.Close",
"price": 257.48,
"rsi": 43.214,
"ret": -0.005062 
},
{
 "date":   6703,
"name": "GSPC.Close",
"price": 256.54,
"rsi": 40.938,
"ret": -0.0036508 
},
{
 "date":   6704,
"name": "GSPC.Close",
"price": 257.62,
"rsi": 39.338,
"ret": 0.0042099 
},
{
 "date":   6705,
"name": "GSPC.Close",
"price": 253.31,
"rsi": 42.137,
"ret": -0.01673 
},
{
 "date":   6706,
"name": "GSPC.Close",
"price": 253.85,
"rsi": 35.163,
"ret": 0.0021318 
},
{
 "date":   6707,
"name": "GSPC.Close",
"price": 256.78,
"rsi": 36.579,
"ret": 0.011542 
},
{
 "date":   6710,
"name": "GSPC.Close",
"price": 258.71,
"rsi": 43.758,
"ret": 0.0075162 
},
{
 "date":   6711,
"name": "GSPC.Close",
"price": 255.39,
"rsi": 47.939,
"ret": -0.012833 
},
{
 "date":   6712,
"name": "GSPC.Close",
"price": 251.35,
"rsi": 42.137,
"ret": -0.015819 
},
{
 "date":   6713,
"name": "GSPC.Close",
"price": 252.57,
"rsi": 36.368,
"ret": 0.0048538 
},
{
 "date":   6714,
"name": "GSPC.Close",
"price": 253.02,
"rsi":  39.08,
"ret": 0.0017817 
},
{
 "date":   6717,
"name": "GSPC.Close",
"price": 250.83,
"rsi": 40.095,
"ret": -0.0086554 
},
{
 "date":   6718,
"name": "GSPC.Close",
"price": 253.51,
"rsi": 36.877,
"ret": 0.010685 
},
{
 "date":   6719,
"name": "GSPC.Close",
"price": 253.76,
"rsi": 42.915,
"ret": 0.00098615 
},
{
 "date":   6720,
"name": "GSPC.Close",
"price": 254.63,
"rsi": 43.458,
"ret": 0.0034284 
},
{
 "date":   6721,
"name": "GSPC.Close",
"price": 253.42,
"rsi": 45.405,
"ret": -0.004752 
},
{
 "date":   6725,
"name": "GSPC.Close",
"price": 262.16,
"rsi": 43.178,
"ret": 0.034488 
},
{
 "date":   6726,
"name": "GSPC.Close",
"price": 266.69,
"rsi": 58.872,
"ret": 0.01728 
},
{
 "date":   6727,
"name": "GSPC.Close",
"price": 265.33,
"rsi": 64.365,
"ret": -0.0050996 
},
{
 "date":   6728,
"name": "GSPC.Close",
"price": 266.45,
"rsi": 61.701,
"ret": 0.0042212 
},
{
 "date":   6731,
"name": "GSPC.Close",
"price": 267.05,
"rsi": 63.057,
"ret": 0.0022518 
},
{
 "date":   6732,
"name": "GSPC.Close",
"price": 265.17,
"rsi": 63.797,
"ret": -0.0070399 
},
{
 "date":   6733,
"name": "GSPC.Close",
"price": 271.52,
"rsi": 59.759,
"ret": 0.023947 
},
{
 "date":   6734,
"name": "GSPC.Close",
"price":  270.2,
"rsi": 67.289,
"ret": -0.0048615 
},
{
 "date":   6735,
"name": "GSPC.Close",
"price": 271.26,
"rsi": 64.584,
"ret": 0.003923 
},
{
 "date":   6738,
"name": "GSPC.Close",
"price": 271.43,
"rsi": 65.774,
"ret": 0.00062671 
},
{
 "date":   6739,
"name": "GSPC.Close",
"price":  274.3,
"rsi": 65.971,
"ret": 0.010574 
},
{
 "date":   6740,
"name": "GSPC.Close",
"price": 274.45,
"rsi": 69.202,
"ret": 0.00054685 
},
{
 "date":   6741,
"name": "GSPC.Close",
"price": 269.77,
"rsi": 69.366,
"ret": -0.017052 
},
{
 "date":   6742,
"name": "GSPC.Close",
"price": 270.68,
"rsi": 58.854,
"ret": 0.0033732 
},
{
 "date":   6745,
"name": "GSPC.Close",
"price": 268.94,
"rsi":  60.12,
"ret": -0.0064283 
},
{
 "date":   6746,
"name": "GSPC.Close",
"price": 271.67,
"rsi": 56.539,
"ret": 0.010151 
},
{
 "date":   6747,
"name": "GSPC.Close",
"price": 275.66,
"rsi": 60.513,
"ret": 0.014687 
},
{
 "date":   6748,
"name": "GSPC.Close",
"price": 274.82,
"rsi": 65.481,
"ret": -0.0030472 
},
{
 "date":   6749,
"name": "GSPC.Close",
"price": 273.78,
"rsi": 63.665,
"ret": -0.0037843 
},
{
 "date":   6752,
"name": "GSPC.Close",
"price": 269.06,
"rsi": 61.395,
"ret": -0.01724 
},
{
 "date":   6753,
"name": "GSPC.Close",
"price": 272.31,
"rsi": 52.283,
"ret": 0.012079 
},
{
 "date":   6754,
"name": "GSPC.Close",
"price": 270.98,
"rsi": 57.013,
"ret": -0.0048841 
},
{
 "date":   6755,
"name": "GSPC.Close",
"price":  273.5,
"rsi": 54.627,
"ret": 0.0092996 
},
{
 "date":   6756,
"name": "GSPC.Close",
"price": 271.78,
"rsi": 58.198,
"ret": -0.0062888 
},
{
 "date":   6760,
"name": "GSPC.Close",
"price": 275.81,
"rsi": 55.015,
"ret": 0.014828 
},
{
 "date":   6761,
"name": "GSPC.Close",
"price": 272.02,
"rsi":  60.47,
"ret": -0.013741 
},
{
 "date":   6762,
"name": "GSPC.Close",
"price": 271.78,
"rsi": 53.856,
"ret": -0.00088229 
},
{
 "date":   6763,
"name": "GSPC.Close",
"price": 270.02,
"rsi": 53.457,
"ret": -0.0064758 
},
{
 "date":   6766,
"name": "GSPC.Close",
"price": 270.55,
"rsi": 50.504,
"ret": 0.0019628 
},
{
 "date":   6767,
"name": "GSPC.Close",
"price": 267.85,
"rsi": 51.375,
"ret": -0.0099797 
},
{
 "date":   6768,
"name": "GSPC.Close",
"price": 269.32,
"rsi": 46.852,
"ret": 0.0054881 
},
{
 "date":   6769,
"name": "GSPC.Close",
"price": 270.26,
"rsi": 49.461,
"ret": 0.0034903 
},
{
 "date":   6770,
"name": "GSPC.Close",
"price": 272.05,
"rsi": 51.114,
"ret": 0.0066233 
},
{
 "date":   6773,
"name": "GSPC.Close",
"price": 270.51,
"rsi": 54.186,
"ret": -0.0056607 
},
{
 "date":   6774,
"name": "GSPC.Close",
"price": 268.47,
"rsi": 51.204,
"ret": -0.0075413 
},
{
 "date":   6775,
"name": "GSPC.Close",
"price":    270,
"rsi": 47.478,
"ret": 0.005699 
},
{
 "date":   6776,
"name": "GSPC.Close",
"price": 266.66,
"rsi": 50.394,
"ret": -0.01237 
},
{
 "date":   6777,
"name": "GSPC.Close",
"price":  263.5,
"rsi": 44.575,
"ret": -0.01185 
},
{
 "date":   6780,
"name": "GSPC.Close",
"price": 264.68,
"rsi": 39.883,
"ret": 0.0044782 
},
{
 "date":   6781,
"name": "GSPC.Close",
"price": 265.19,
"rsi": 42.325,
"ret": 0.0019269 
},
{
 "date":   6782,
"name": "GSPC.Close",
"price":  262.5,
"rsi": 43.395,
"ret": -0.010144 
},
{
 "date":   6783,
"name": "GSPC.Close",
"price": 266.02,
"rsi": 39.258,
"ret": 0.01341 
},
{
 "date":   6784,
"name": "GSPC.Close",
"price": 272.02,
"rsi": 46.452,
"ret": 0.022555 
},
{
 "date":   6787,
"name": "GSPC.Close",
"price": 272.21,
"rsi": 56.014,
"ret": 0.00069848 
},
{
 "date":   6788,
"name": "GSPC.Close",
"price": 272.06,
"rsi":  56.28,
"ret": -0.00055105 
},
{
 "date":   6789,
"name": "GSPC.Close",
"price": 272.98,
"rsi": 55.992,
"ret": 0.0033816 
},
{
 "date":   6790,
"name": "GSPC.Close",
"price": 271.93,
"rsi": 57.432,
"ret": -0.0038464 
},
{
 "date":   6791,
"name": "GSPC.Close",
"price": 271.15,
"rsi": 55.212,
"ret": -0.0028684 
},
{
 "date":   6794,
"name": "GSPC.Close",
"price": 269.98,
"rsi": 53.556,
"ret": -0.004315 
},
{
 "date":   6795,
"name": "GSPC.Close",
"price": 266.49,
"rsi": 51.081,
"ret": -0.012927 
},
{
 "date":   6796,
"name": "GSPC.Close",
"price":  261.9,
"rsi": 44.478,
"ret": -0.017224 
},
{
 "date":   6797,
"name": "GSPC.Close",
"price": 262.75,
"rsi": 37.595,
"ret": 0.0032455 
},
{
 "date":   6798,
"name": "GSPC.Close",
"price": 262.55,
"rsi": 39.463,
"ret": -0.00076118 
},
{
 "date":   6801,
"name": "GSPC.Close",
"price": 258.69,
"rsi": 39.166,
"ret": -0.014702 
},
{
 "date":   6802,
"name": "GSPC.Close",
"price": 260.56,
"rsi": 33.867,
"ret": 0.0072287 
},
{
 "date":   6803,
"name": "GSPC.Close",
"price": 260.77,
"rsi": 38.227,
"ret": 0.00080596 
},
{
 "date":   6804,
"name": "GSPC.Close",
"price": 261.03,
"rsi": 38.716,
"ret": 0.00099705 
},
{
 "date":   6805,
"name": "GSPC.Close",
"price": 260.24,
"rsi": 39.356,
"ret": -0.0030265 
},
{
 "date":   6808,
"name": "GSPC.Close",
"price": 256.98,
"rsi": 38.056,
"ret": -0.012527 
},
{
 "date":   6809,
"name": "GSPC.Close",
"price": 257.09,
"rsi": 33.185,
"ret": 0.00042805 
},
{
 "date":   6810,
"name": "GSPC.Close",
"price": 261.13,
"rsi": 33.494,
"ret": 0.015714 
},
{
 "date":   6811,
"name": "GSPC.Close",
"price": 259.18,
"rsi": 43.787,
"ret": -0.0074675 
},
{
 "date":   6812,
"name": "GSPC.Close",
"price": 259.68,
"rsi": 40.527,
"ret": 0.0019292 
},
{
 "date":   6815,
"name": "GSPC.Close",
"price": 262.33,
"rsi": 41.725,
"ret": 0.010205 
},
{
 "date":   6816,
"name": "GSPC.Close",
"price": 262.51,
"rsi": 47.735,
"ret": 0.00068616 
},
{
 "date":   6817,
"name": "GSPC.Close",
"price": 261.52,
"rsi": 48.126,
"ret": -0.0037713 
},
{
 "date":   6818,
"name": "GSPC.Close",
"price": 258.35,
"rsi": 46.083,
"ret": -0.012121 
},
{
 "date":   6819,
"name": "GSPC.Close",
"price": 264.48,
"rsi": 40.197,
"ret": 0.023728 
},
{
 "date":   6823,
"name": "GSPC.Close",
"price": 265.59,
"rsi": 52.762,
"ret": 0.0041969 
},
{
 "date":   6824,
"name": "GSPC.Close",
"price": 265.87,
"rsi": 54.621,
"ret": 0.0010543 
},
{
 "date":   6825,
"name": "GSPC.Close",
"price": 265.88,
"rsi": 55.101,
"ret": 3.7612e-05 
},
{
 "date":   6826,
"name": "GSPC.Close",
"price": 266.84,
"rsi": 55.119,
"ret": 0.0036107 
},
{
 "date":   6829,
"name": "GSPC.Close",
"price": 266.47,
"rsi": 56.931,
"ret": -0.0013866 
},
{
 "date":   6830,
"name": "GSPC.Close",
"price": 267.43,
"rsi": 55.993,
"ret": 0.0036027 
},
{
 "date":   6831,
"name": "GSPC.Close",
"price": 269.31,
"rsi": 57.929,
"ret": 0.0070299 
},
{
 "date":   6832,
"name": "GSPC.Close",
"price": 268.13,
"rsi": 61.502,
"ret": -0.0043816 
},
{
 "date":   6833,
"name": "GSPC.Close",
"price": 270.65,
"rsi": 58.163,
"ret": 0.0093984 
},
{
 "date":   6836,
"name": "GSPC.Close",
"price": 268.82,
"rsi": 62.807,
"ret": -0.0067615 
},
{
 "date":   6837,
"name": "GSPC.Close",
"price": 269.73,
"rsi":  57.79,
"ret": 0.0033852 
},
{
 "date":   6838,
"name": "GSPC.Close",
"price": 270.16,
"rsi": 59.522,
"ret": 0.0015942 
},
{
 "date":   6839,
"name": "GSPC.Close",
"price": 269.18,
"rsi": 60.349,
"ret": -0.0036275 
},
{
 "date":   6840,
"name": "GSPC.Close",
"price": 269.76,
"rsi": 57.466,
"ret": 0.0021547 
},
{
 "date":   6843,
"name": "GSPC.Close",
"price": 268.88,
"rsi": 58.723,
"ret": -0.0032622 
},
{
 "date":   6844,
"name": "GSPC.Close",
"price": 268.26,
"rsi": 56.018,
"ret": -0.0023059 
},
{
 "date":   6845,
"name": "GSPC.Close",
"price": 269.08,
"rsi": 54.126,
"ret": 0.0030567 
},
{
 "date":   6846,
"name": "GSPC.Close",
"price": 272.59,
"rsi": 56.231,
"ret": 0.013044 
},
{
 "date":   6847,
"name": "GSPC.Close",
"price": 271.91,
"rsi": 63.874,
"ret": -0.0024946 
},
{
 "date":   6850,
"name": "GSPC.Close",
"price": 271.38,
"rsi": 61.629,
"ret": -0.0019492 
},
{
 "date":   6851,
"name": "GSPC.Close",
"price": 270.62,
"rsi": 59.863,
"ret": -0.0028005 
},
{
 "date":   6852,
"name": "GSPC.Close",
"price": 271.86,
"rsi": 57.326,
"ret": 0.0045821 
},
{
 "date":   6853,
"name": "GSPC.Close",
"price": 272.39,
"rsi": 60.283,
"ret": 0.0019495 
},
{
 "date":   6854,
"name": "GSPC.Close",
"price": 278.07,
"rsi": 61.511,
"ret": 0.020852 
},
{
 "date":   6857,
"name": "GSPC.Close",
"price": 278.24,
"rsi": 71.633,
"ret": 0.00061136 
},
{
 "date":   6858,
"name": "GSPC.Close",
"price": 277.93,
"rsi": 71.871,
"ret": -0.0011141 
},
{
 "date":   6859,
"name": "GSPC.Close",
"price": 273.98,
"rsi": 70.704,
"ret": -0.014212 
},
{
 "date":   6860,
"name": "GSPC.Close",
"price": 275.22,
"rsi": 57.821,
"ret": 0.0045259 
},
{
 "date":   6861,
"name": "GSPC.Close",
"price":  275.5,
"rsi": 60.268,
"ret": 0.0010174 
},
{
 "date":   6864,
"name": "GSPC.Close",
"price": 276.41,
"rsi": 60.821,
"ret": 0.0033031 
},
{
 "date":   6865,
"name": "GSPC.Close",
"price": 279.38,
"rsi": 62.641,
"ret": 0.010745 
},
{
 "date":   6866,
"name": "GSPC.Close",
"price": 276.97,
"rsi": 67.883,
"ret": -0.0086262 
},
{
 "date":   6867,
"name": "GSPC.Close",
"price": 282.88,
"rsi": 60.468,
"ret": 0.021338 
},
{
 "date":   6868,
"name": "GSPC.Close",
"price": 283.66,
"rsi": 69.319,
"ret": 0.0027574 
},
{
 "date":   6871,
"name": "GSPC.Close",
"price": 282.28,
"rsi": 70.265,
"ret": -0.004865 
},
{
 "date":   6872,
"name": "GSPC.Close",
"price": 282.38,
"rsi": 66.365,
"ret": 0.00035426 
},
{
 "date":   6873,
"name": "GSPC.Close",
"price": 281.38,
"rsi":  66.51,
"ret": -0.0035413 
},
{
 "date":   6874,
"name": "GSPC.Close",
"price": 277.28,
"rsi": 63.559,
"ret": -0.014571 
},
{
 "date":   6875,
"name": "GSPC.Close",
"price": 278.53,
"rsi": 53.145,
"ret": 0.0045081 
},
{
 "date":   6878,
"name": "GSPC.Close",
"price": 278.97,
"rsi": 55.537,
"ret": 0.0015797 
},
{
 "date":   6879,
"name": "GSPC.Close",
"price": 279.06,
"rsi": 56.381,
"ret": 0.00032262 
},
{
 "date":   6880,
"name": "GSPC.Close",
"price": 279.06,
"rsi": 56.563,
"ret":      0 
},
{
 "date":   6881,
"name": "GSPC.Close",
"price":  279.2,
"rsi": 56.563,
"ret": 0.00050168 
},
{
 "date":   6882,
"name": "GSPC.Close",
"price": 276.31,
"rsi": 56.886,
"ret": -0.010351 
},
{
 "date":   6885,
"name": "GSPC.Close",
"price": 273.93,
"rsi": 48.797,
"ret": -0.0086135 
},
{
 "date":   6886,
"name": "GSPC.Close",
"price": 275.15,
"rsi": 43.332,
"ret": 0.0044537 
},
{
 "date":   6887,
"name": "GSPC.Close",
"price": 273.33,
"rsi": 46.632,
"ret": -0.0066146 
},
{
 "date":   6888,
"name": "GSPC.Close",
"price": 273.69,
"rsi": 42.643,
"ret": 0.0013171 
},
{
 "date":   6889,
"name": "GSPC.Close",
"price": 267.92,
"rsi": 43.669,
"ret": -0.021082 
},
{
 "date":   6892,
"name": "GSPC.Close",
"price": 267.72,
"rsi": 33.364,
"ret": -0.00074649 
},
{
 "date":   6893,
"name": "GSPC.Close",
"price": 268.34,
"rsi": 33.073,
"ret": 0.0023159 
},
{
 "date":   6894,
"name": "GSPC.Close",
"price": 263.82,
"rsi": 34.968,
"ret": -0.016844 
},
{
 "date":   6895,
"name": "GSPC.Close",
"price":  264.6,
"rsi": 28.607,
"ret": 0.0029566 
},
{
 "date":   6896,
"name": "GSPC.Close",
"price": 266.47,
"rsi": 30.941,
"ret": 0.0070673 
},
{
 "date":   6899,
"name": "GSPC.Close",
"price": 266.22,
"rsi": 36.319,
"ret": -0.00093819 
},
{
 "date":   6900,
"name": "GSPC.Close",
"price": 267.21,
"rsi": 35.916,
"ret": 0.0037187 
},
{
 "date":   6901,
"name": "GSPC.Close",
"price":    269,
"rsi": 38.809,
"ret": 0.0066989 
},
{
 "date":   6903,
"name": "GSPC.Close",
"price": 267.23,
"rsi": 43.753,
"ret": -0.0065799 
},
{
 "date":   6906,
"name": "GSPC.Close",
"price": 268.64,
"rsi": 40.287,
"ret": 0.0052764 
},
{
 "date":   6907,
"name": "GSPC.Close",
"price": 270.91,
"rsi": 44.087,
"ret": 0.00845 
},
{
 "date":   6908,
"name": "GSPC.Close",
"price":  273.7,
"rsi": 49.643,
"ret": 0.010299 
},
{
 "date":   6909,
"name": "GSPC.Close",
"price": 272.49,
"rsi": 55.497,
"ret": -0.0044209 
},
{
 "date":   6910,
"name": "GSPC.Close",
"price": 271.81,
"rsi": 52.639,
"ret": -0.0024955 
},
{
 "date":   6913,
"name": "GSPC.Close",
"price": 274.93,
"rsi": 51.048,
"ret": 0.011479 
},
{
 "date":   6914,
"name": "GSPC.Close",
"price": 277.59,
"rsi": 57.409,
"ret": 0.0096752 
},
{
 "date":   6915,
"name": "GSPC.Close",
"price": 278.13,
"rsi": 61.948,
"ret": 0.0019453 
},
{
 "date":   6916,
"name": "GSPC.Close",
"price": 276.59,
"rsi": 62.815,
"ret": -0.005537 
},
{
 "date":   6917,
"name": "GSPC.Close",
"price": 277.03,
"rsi": 58.709,
"ret": 0.0015908 
},
{
 "date":   6920,
"name": "GSPC.Close",
"price": 276.52,
"rsi": 59.523,
"ret": -0.001841 
},
{
 "date":   6921,
"name": "GSPC.Close",
"price": 276.31,
"rsi": 58.093,
"ret": -0.00075944 
},
{
 "date":   6922,
"name": "GSPC.Close",
"price": 275.31,
"rsi": 57.481,
"ret": -0.0036191 
},
{
 "date":   6923,
"name": "GSPC.Close",
"price": 274.28,
"rsi": 54.534,
"ret": -0.0037412 
},
{
 "date":   6924,
"name": "GSPC.Close",
"price": 276.29,
"rsi": 51.599,
"ret": 0.0073283 
},
{
 "date":   6927,
"name": "GSPC.Close",
"price": 278.91,
"rsi": 56.517,
"ret": 0.0094828 
},
{
 "date":   6928,
"name": "GSPC.Close",
"price": 277.47,
"rsi": 61.945,
"ret": -0.005163 
},
{
 "date":   6929,
"name": "GSPC.Close",
"price": 277.38,
"rsi": 57.683,
"ret": -0.00032436 
},
{
 "date":   6930,
"name": "GSPC.Close",
"price": 276.87,
"rsi": 57.417,
"ret": -0.0018386 
},
{
 "date":   6931,
"name": "GSPC.Close",
"price": 277.87,
"rsi": 55.846,
"ret": 0.0036118 
},
{
 "date":   6935,
"name": "GSPC.Close",
"price": 276.83,
"rsi": 58.258,
"ret": -0.0037428 
},
{
 "date":   6936,
"name": "GSPC.Close",
"price": 277.08,
"rsi": 54.899,
"ret": 0.00090308 
},
{
 "date":   6937,
"name": "GSPC.Close",
"price":  279.4,
"rsi": 55.562,
"ret": 0.008373 
},
{
 "date":   6938,
"name": "GSPC.Close",
"price": 277.72,
"rsi": 61.256,
"ret": -0.0060129 
},
{
 "date":   6942,
"name": "GSPC.Close",
"price": 275.31,
"rsi": 55.691,
"ret": -0.0086778 
},
{
 "date":   6943,
"name": "GSPC.Close",
"price": 279.43,
"rsi": 48.838,
"ret": 0.014965 
},
{
 "date":   6944,
"name": "GSPC.Close",
"price": 280.01,
"rsi": 58.288,
"ret": 0.0020757 
},
{
 "date":   6945,
"name": "GSPC.Close",
"price": 280.67,
"rsi": 59.425,
"ret": 0.0023571 
},
{
 "date":   6948,
"name": "GSPC.Close",
"price": 280.98,
"rsi": 60.735,
"ret": 0.0011045 
},
{
 "date":   6949,
"name": "GSPC.Close",
"price": 280.38,
"rsi": 61.367,
"ret": -0.0021354 
},
{
 "date":   6950,
"name": "GSPC.Close",
"price": 282.01,
"rsi": 59.377,
"ret": 0.0058135 
},
{
 "date":   6951,
"name": "GSPC.Close",
"price": 283.17,
"rsi": 62.897,
"ret": 0.0041133 
},
{
 "date":   6952,
"name": "GSPC.Close",
"price": 283.87,
"rsi": 65.207,
"ret": 0.002472 
},
{
 "date":   6955,
"name": "GSPC.Close",
"price": 284.14,
"rsi":  66.56,
"ret": 0.00095114 
},
{
 "date":   6956,
"name": "GSPC.Close",
"price": 283.55,
"rsi": 67.092,
"ret": -0.0020764 
},
{
 "date":   6957,
"name": "GSPC.Close",
"price": 286.53,
"rsi": 64.672,
"ret": 0.01051 
},
{
 "date":   6958,
"name": "GSPC.Close",
"price": 286.91,
"rsi": 70.466,
"ret": 0.0013262 
},
{
 "date":   6959,
"name": "GSPC.Close",
"price": 286.63,
"rsi": 71.116,
"ret": -0.00097592 
},
{
 "date":   6962,
"name": "GSPC.Close",
"price":  284.5,
"rsi": 69.895,
"ret": -0.0074312 
},
{
 "date":   6963,
"name": "GSPC.Close",
"price": 288.49,
"rsi": 61.272,
"ret": 0.014025 
},
{
 "date":   6964,
"name": "GSPC.Close",
"price": 289.14,
"rsi":  68.99,
"ret": 0.0022531 
},
{
 "date":   6965,
"name": "GSPC.Close",
"price": 291.69,
"rsi": 70.037,
"ret": 0.0088193 
},
{
 "date":   6966,
"name": "GSPC.Close",
"price": 293.82,
"rsi": 73.779,
"ret": 0.0073023 
},
{
 "date":   6969,
"name": "GSPC.Close",
"price": 294.99,
"rsi": 76.427,
"ret": 0.003982 
},
{
 "date":   6970,
"name": "GSPC.Close",
"price": 297.47,
"rsi": 77.756,
"ret": 0.0084071 
},
{
 "date":   6971,
"name": "GSPC.Close",
"price": 297.09,
"rsi": 80.292,
"ret": -0.0012774 
},
{
 "date":   6972,
"name": "GSPC.Close",
"price": 296.84,
"rsi":  78.81,
"ret": -0.0008415 
},
{
 "date":   6973,
"name": "GSPC.Close",
"price": 296.97,
"rsi": 77.792,
"ret": 0.00043795 
},
{
 "date":   6976,
"name": "GSPC.Close",
"price": 296.04,
"rsi": 77.951,
"ret": -0.0031316 
},
{
 "date":   6977,
"name": "GSPC.Close",
"price": 299.63,
"rsi": 73.865,
"ret": 0.012127 
},
{
 "date":   6978,
"name": "GSPC.Close",
"price": 298.65,
"rsi": 78.541,
"ret": -0.0032707 
},
{
 "date":   6979,
"name": "GSPC.Close",
"price": 296.06,
"rsi": 74.617,
"ret": -0.0086724 
},
{
 "date":   6980,
"name": "GSPC.Close",
"price": 292.02,
"rsi": 65.326,
"ret": -0.013646 
},
{
 "date":   6983,
"name": "GSPC.Close",
"price": 292.54,
"rsi": 54.025,
"ret": 0.0017807 
},
{
 "date":   6984,
"name": "GSPC.Close",
"price": 291.81,
"rsi": 55.102,
"ret": -0.0024954 
},
{
 "date":   6985,
"name": "GSPC.Close",
"price": 294.24,
"rsi": 53.218,
"ret": 0.0083273 
},
{
 "date":   6986,
"name": "GSPC.Close",
"price": 294.81,
"rsi": 58.326,
"ret": 0.0019372 
},
{
 "date":   6987,
"name": "GSPC.Close",
"price": 296.76,
"rsi": 59.444,
"ret": 0.0066144 
},
{
 "date":   6991,
"name": "GSPC.Close",
"price": 295.98,
"rsi": 63.094,
"ret": -0.0026284 
},
{
 "date":   6992,
"name": "GSPC.Close",
"price": 290.91,
"rsi":  60.74,
"ret": -0.01713 
},
{
 "date":   6993,
"name": "GSPC.Close",
"price": 292.05,
"rsi": 48.159,
"ret": 0.0039187 
},
{
 "date":   6994,
"name": "GSPC.Close",
"price": 287.13,
"rsi": 50.635,
"ret": -0.016846 
},
{
 "date":   6997,
"name": "GSPC.Close",
"price": 287.82,
"rsi": 41.437,
"ret": 0.0024031 
},
{
 "date":   6998,
"name": "GSPC.Close",
"price": 288.86,
"rsi": 43.001,
"ret": 0.0036134 
},
{
 "date":   6999,
"name": "GSPC.Close",
"price": 287.11,
"rsi": 45.369,
"ret": -0.0060583 
},
{
 "date":   7000,
"name": "GSPC.Close",
"price": 289.95,
"rsi": 42.192,
"ret": 0.0098917 
},
{
 "date":   7001,
"name": "GSPC.Close",
"price": 291.18,
"rsi": 48.494,
"ret": 0.0042421 
},
{
 "date":   7004,
"name": "GSPC.Close",
"price": 294.81,
"rsi": 50.987,
"ret": 0.012467 
},
{
 "date":   7005,
"name": "GSPC.Close",
"price": 293.87,
"rsi": 57.519,
"ret": -0.0031885 
},
{
 "date":   7006,
"name": "GSPC.Close",
"price": 294.08,
"rsi": 55.458,
"ret": 0.0007146 
},
{
 "date":   7007,
"name": "GSPC.Close",
"price": 293.93,
"rsi": 55.839,
"ret": -0.00051007 
},
{
 "date":   7008,
"name": "GSPC.Close",
"price": 292.88,
"rsi": 55.474,
"ret": -0.0035723 
},
{
 "date":   7011,
"name": "GSPC.Close",
"price": 295.32,
"rsi":  52.87,
"ret": 0.0083311 
},
{
 "date":   7012,
"name": "GSPC.Close",
"price": 295.14,
"rsi": 57.824,
"ret": -0.00060951 
},
{
 "date":   7013,
"name": "GSPC.Close",
"price": 296.67,
"rsi": 57.345,
"ret": 0.005184 
},
{
 "date":   7014,
"name": "GSPC.Close",
"price": 299.44,
"rsi": 60.351,
"ret": 0.009337 
},
{
 "date":   7015,
"name": "GSPC.Close",
"price": 292.69,
"rsi": 65.141,
"ret": -0.022542 
},
{
 "date":   7018,
"name": "GSPC.Close",
"price": 289.92,
"rsi": 49.461,
"ret": -0.0094639 
},
{
 "date":   7019,
"name": "GSPC.Close",
"price": 291.33,
"rsi": 44.706,
"ret": 0.0048634 
},
{
 "date":   7020,
"name": "GSPC.Close",
"price": 290.49,
"rsi": 47.474,
"ret": -0.0028833 
},
{
 "date":   7021,
"name": "GSPC.Close",
"price": 288.98,
"rsi": 45.997,
"ret": -0.0051981 
},
{
 "date":   7025,
"name": "GSPC.Close",
"price": 290.57,
"rsi": 43.383,
"ret": 0.0055021 
},
{
 "date":   7026,
"name": "GSPC.Close",
"price": 291.59,
"rsi":  46.81,
"ret": 0.0035103 
},
{
 "date":   7027,
"name": "GSPC.Close",
"price": 292.35,
"rsi": 48.946,
"ret": 0.0026064 
},
{
 "date":   7028,
"name": "GSPC.Close",
"price": 292.52,
"rsi": 50.539,
"ret": 0.00058149 
},
{
 "date":   7029,
"name": "GSPC.Close",
"price": 294.87,
"rsi": 50.908,
"ret": 0.0080336 
},
{
 "date":   7032,
"name": "GSPC.Close",
"price": 296.39,
"rsi": 55.816,
"ret": 0.0051548 
},
{
 "date":   7033,
"name": "GSPC.Close",
"price": 295.31,
"rsi": 58.692,
"ret": -0.0036438 
},
{
 "date":   7034,
"name": "GSPC.Close",
"price": 296.24,
"rsi": 55.907,
"ret": 0.0031492 
},
{
 "date":   7035,
"name": "GSPC.Close",
"price": 295.29,
"rsi": 57.766,
"ret": -0.0032069 
},
{
 "date":   7036,
"name": "GSPC.Close",
"price": 297.16,
"rsi": 55.206,
"ret": 0.0063328 
},
{
 "date":   7039,
"name": "GSPC.Close",
"price": 297.11,
"rsi": 59.052,
"ret": -0.00016826 
},
{
 "date":   7040,
"name": "GSPC.Close",
"price": 298.49,
"rsi": 58.907,
"ret": 0.0046447 
},
{
 "date":   7041,
"name": "GSPC.Close",
"price": 298.99,
"rsi": 61.714,
"ret": 0.0016751 
},
{
 "date":   7042,
"name": "GSPC.Close",
"price":  296.4,
"rsi": 62.707,
"ret": -0.0086625 
},
{
 "date":   7043,
"name": "GSPC.Close",
"price": 301.36,
"rsi": 54.775,
"ret": 0.016734 
},
{
 "date":   7046,
"name": "GSPC.Close",
"price": 301.72,
"rsi": 64.132,
"ret": 0.0011946 
},
{
 "date":   7047,
"name": "GSPC.Close",
"price": 306.02,
"rsi": 64.703,
"ret": 0.014252 
},
{
 "date":   7048,
"name": "GSPC.Close",
"price": 307.15,
"rsi": 70.701,
"ret": 0.0036926 
},
{
 "date":   7049,
"name": "GSPC.Close",
"price": 306.19,
"rsi": 72.046,
"ret": -0.0031255 
},
{
 "date":   7050,
"name": "GSPC.Close",
"price": 309.61,
"rsi": 69.143,
"ret": 0.01117 
},
{
 "date":   7053,
"name": "GSPC.Close",
"price": 308.69,
"rsi": 73.274,
"ret": -0.0029715 
},
{
 "date":   7054,
"name": "GSPC.Close",
"price": 306.75,
"rsi": 70.538,
"ret": -0.0062846 
},
{
 "date":   7055,
"name": "GSPC.Close",
"price": 306.93,
"rsi": 65.025,
"ret": 0.0005868 
},
{
 "date":   7056,
"name": "GSPC.Close",
"price": 309.58,
"rsi": 65.296,
"ret": 0.0086339 
},
{
 "date":   7057,
"name": "GSPC.Close",
"price": 309.64,
"rsi": 69.093,
"ret": 0.00019381 
},
{
 "date":   7060,
"name": "GSPC.Close",
"price": 309.12,
"rsi": 69.176,
"ret": -0.0016794 
},
{
 "date":   7061,
"name": "GSPC.Close",
"price": 308.12,
"rsi": 67.499,
"ret": -0.003235 
},
{
 "date":   7062,
"name": "GSPC.Close",
"price": 308.16,
"rsi": 64.274,
"ret": 0.00012982 
},
{
 "date":   7063,
"name": "GSPC.Close",
"price": 307.77,
"rsi": 64.347,
"ret": -0.0012656 
},
{
 "date":   7064,
"name": "GSPC.Close",
"price": 307.61,
"rsi": 62.988,
"ret": -0.00051987 
},
{
 "date":   7067,
"name": "GSPC.Close",
"price":    306,
"rsi": 62.406,
"ret": -0.0052339 
},
{
 "date":   7068,
"name": "GSPC.Close",
"price": 305.19,
"rsi": 56.725,
"ret": -0.0026471 
},
{
 "date":   7069,
"name": "GSPC.Close",
"price":  305.8,
"rsi": 54.058,
"ret": 0.0019988 
},
{
 "date":   7070,
"name": "GSPC.Close",
"price": 306.95,
"rsi": 55.745,
"ret": 0.0037606 
},
{
 "date":   7071,
"name": "GSPC.Close",
"price": 313.84,
"rsi": 58.816,
"ret": 0.022447 
},
{
 "date":   7074,
"name": "GSPC.Close",
"price": 316.16,
"rsi": 71.552,
"ret": 0.0073923 
},
{
 "date":   7075,
"name": "GSPC.Close",
"price": 315.28,
"rsi":  74.42,
"ret": -0.0027834 
},
{
 "date":   7076,
"name": "GSPC.Close",
"price": 317.48,
"rsi": 71.476,
"ret": 0.0069779 
},
{
 "date":   7077,
"name": "GSPC.Close",
"price": 317.97,
"rsi": 74.222,
"ret": 0.0015434 
},
{
 "date":   7078,
"name": "GSPC.Close",
"price": 321.24,
"rsi": 74.804,
"ret": 0.010284 
},
{
 "date":   7081,
"name": "GSPC.Close",
"price": 321.98,
"rsi":  78.32,
"ret": 0.0023036 
},
{
 "date":   7082,
"name": "GSPC.Close",
"price": 318.32,
"rsi": 79.033,
"ret": -0.011367 
},
{
 "date":   7083,
"name": "GSPC.Close",
"price": 319.14,
"rsi": 67.251,
"ret": 0.002576 
},
{
 "date":   7084,
"name": "GSPC.Close",
"price": 319.17,
"rsi": 68.388,
"ret": 9.4003e-05 
},
{
 "date":   7085,
"name": "GSPC.Close",
"price": 321.59,
"rsi": 68.431,
"ret": 0.0075822 
},
{
 "date":   7089,
"name": "GSPC.Close",
"price": 319.05,
"rsi":  71.78,
"ret": -0.0078983 
},
{
 "date":   7090,
"name": "GSPC.Close",
"price": 320.52,
"rsi": 64.095,
"ret": 0.0046074 
},
{
 "date":   7091,
"name": "GSPC.Close",
"price": 321.97,
"rsi": 66.341,
"ret": 0.0045239 
},
{
 "date":   7092,
"name": "GSPC.Close",
"price": 325.52,
"rsi": 68.438,
"ret": 0.011026 
},
{
 "date":   7095,
"name": "GSPC.Close",
"price": 322.03,
"rsi": 72.892,
"ret": -0.010721 
},
{
 "date":   7096,
"name": "GSPC.Close",
"price": 324.24,
"rsi": 63.418,
"ret": 0.0068627 
},
{
 "date":   7097,
"name": "GSPC.Close",
"price": 326.95,
"rsi": 66.396,
"ret": 0.008358 
},
{
 "date":   7098,
"name": "GSPC.Close",
"price": 326.75,
"rsi": 69.659,
"ret": -0.00061171 
},
{
 "date":   7099,
"name": "GSPC.Close",
"price": 326.69,
"rsi": 69.125,
"ret": -0.00018363 
},
{
 "date":   7102,
"name": "GSPC.Close",
"price": 326.24,
"rsi": 68.955,
"ret": -0.0013775 
},
{
 "date":   7103,
"name": "GSPC.Close",
"price": 323.91,
"rsi": 67.607,
"ret": -0.007142 
},
{
 "date":   7104,
"name": "GSPC.Close",
"price": 323.83,
"rsi": 60.964,
"ret": -0.00024698 
},
{
 "date":   7105,
"name": "GSPC.Close",
"price": 320.08,
"rsi": 60.743,
"ret": -0.01158 
},
{
 "date":   7106,
"name": "GSPC.Close",
"price": 321.35,
"rsi": 51.358,
"ret": 0.0039678 
},
{
 "date":   7109,
"name": "GSPC.Close",
"price": 321.89,
"rsi": 53.953,
"ret": 0.0016804 
},
{
 "date":   7110,
"name": "GSPC.Close",
"price": 321.25,
"rsi": 55.051,
"ret": -0.0019883 
},
{
 "date":   7111,
"name": "GSPC.Close",
"price": 320.48,
"rsi": 53.425,
"ret": -0.0023969 
},
{
 "date":   7112,
"name": "GSPC.Close",
"price": 322.32,
"rsi": 51.456,
"ret": 0.0057414 
},
{
 "date":   7113,
"name": "GSPC.Close",
"price":    328,
"rsi": 55.661,
"ret": 0.017622 
},
{
 "date":   7116,
"name": "GSPC.Close",
"price":  326.6,
"rsi": 65.576,
"ret": -0.0042683 
},
{
 "date":   7117,
"name": "GSPC.Close",
"price": 328.44,
"rsi": 61.902,
"ret": 0.0056338 
},
{
 "date":   7118,
"name": "GSPC.Close",
"price": 325.81,
"rsi": 64.701,
"ret": -0.0080076 
},
{
 "date":   7119,
"name": "GSPC.Close",
"price": 319.68,
"rsi": 58.127,
"ret": -0.018815 
},
{
 "date":   7120,
"name": "GSPC.Close",
"price": 317.98,
"rsi": 46.315,
"ret": -0.0053178 
},
{
 "date":   7123,
"name": "GSPC.Close",
"price": 319.23,
"rsi": 43.664,
"ret": 0.0039311 
},
{
 "date":   7125,
"name": "GSPC.Close",
"price": 320.64,
"rsi": 46.106,
"ret": 0.0044169 
},
{
 "date":   7126,
"name": "GSPC.Close",
"price": 321.55,
"rsi": 48.802,
"ret": 0.0028381 
},
{
 "date":   7127,
"name": "GSPC.Close",
"price": 324.91,
"rsi": 50.522,
"ret": 0.010449 
},
{
 "date":   7130,
"name": "GSPC.Close",
"price": 327.07,
"rsi": 56.353,
"ret": 0.006648 
},
{
 "date":   7131,
"name": "GSPC.Close",
"price": 328.78,
"rsi": 59.646,
"ret": 0.0052282 
},
{
 "date":   7132,
"name": "GSPC.Close",
"price": 329.81,
"rsi": 62.084,
"ret": 0.0031328 
},
{
 "date":   7133,
"name": "GSPC.Close",
"price": 329.95,
"rsi": 63.514,
"ret": 0.00042449 
},
{
 "date":   7134,
"name": "GSPC.Close",
"price": 331.84,
"rsi": 63.715,
"ret": 0.0057281 
},
{
 "date":   7137,
"name": "GSPC.Close",
"price": 332.44,
"rsi": 66.397,
"ret": 0.0018081 
},
{
 "date":   7138,
"name": "GSPC.Close",
"price": 331.35,
"rsi": 67.226,
"ret": -0.0032788 
},
{
 "date":   7139,
"name": "GSPC.Close",
"price": 335.73,
"rsi": 64.133,
"ret": 0.013219 
},
{
 "date":   7140,
"name": "GSPC.Close",
"price": 333.51,
"rsi": 70.088,
"ret": -0.0066125 
},
{
 "date":   7141,
"name": "GSPC.Close",
"price":  335.9,
"rsi": 64.264,
"ret": 0.0071662 
},
{
 "date":   7144,
"name": "GSPC.Close",
"price": 333.67,
"rsi": 67.404,
"ret": -0.0066389 
},
{
 "date":   7145,
"name": "GSPC.Close",
"price": 333.88,
"rsi": 61.935,
"ret": 0.00062936 
},
{
 "date":   7146,
"name": "GSPC.Close",
"price": 338.05,
"rsi": 62.246,
"ret": 0.01249 
},
{
 "date":   7147,
"name": "GSPC.Close",
"price": 341.99,
"rsi": 67.856,
"ret": 0.011655 
},
{
 "date":   7148,
"name": "GSPC.Close",
"price": 342.15,
"rsi": 72.078,
"ret": 0.00046785 
},
{
 "date":   7151,
"name": "GSPC.Close",
"price": 346.08,
"rsi": 72.237,
"ret": 0.011486 
},
{
 "date":   7152,
"name": "GSPC.Close",
"price": 343.75,
"rsi": 75.881,
"ret": -0.0067325 
},
{
 "date":   7153,
"name": "GSPC.Close",
"price": 344.34,
"rsi": 70.014,
"ret": 0.0017164 
},
{
 "date":   7154,
"name": "GSPC.Close",
"price": 344.74,
"rsi": 70.633,
"ret": 0.0011616 
},
{
 "date":   7155,
"name": "GSPC.Close",
"price": 343.92,
"rsi": 71.069,
"ret": -0.0023786 
},
{
 "date":   7158,
"name": "GSPC.Close",
"price": 349.41,
"rsi": 68.813,
"ret": 0.015963 
},
{
 "date":   7159,
"name": "GSPC.Close",
"price": 349.35,
"rsi": 74.622,
"ret": -0.00017172 
},
{
 "date":   7160,
"name": "GSPC.Close",
"price": 346.94,
"rsi": 74.459,
"ret": -0.0068985 
},
{
 "date":   7161,
"name": "GSPC.Close",
"price": 348.25,
"rsi": 68.022,
"ret": 0.0037759 
},
{
 "date":   7162,
"name": "GSPC.Close",
"price": 344.74,
"rsi": 69.563,
"ret": -0.010079 
},
{
 "date":   7165,
"name": "GSPC.Close",
"price": 343.06,
"rsi": 61.074,
"ret": -0.0048732 
},
{
 "date":   7166,
"name": "GSPC.Close",
"price": 344.71,
"rsi":  57.46,
"ret": 0.0048097 
},
{
 "date":   7167,
"name": "GSPC.Close",
"price": 345.66,
"rsi": 59.966,
"ret": 0.0027559 
},
{
 "date":   7168,
"name": "GSPC.Close",
"price": 344.45,
"rsi": 61.377,
"ret": -0.0035005 
},
{
 "date":   7169,
"name": "GSPC.Close",
"price": 346.03,
"rsi": 58.547,
"ret": 0.004587 
},
{
 "date":   7172,
"name": "GSPC.Close",
"price": 340.67,
"rsi": 61.071,
"ret": -0.01549 
},
{
 "date":   7173,
"name": "GSPC.Close",
"price": 341.19,
"rsi": 49.958,
"ret": 0.0015264 
},
{
 "date":   7174,
"name": "GSPC.Close",
"price":  344.7,
"rsi": 50.892,
"ret": 0.010288 
},
{
 "date":   7175,
"name": "GSPC.Close",
"price": 351.52,
"rsi": 56.756,
"ret": 0.019785 
},
{
 "date":   7176,
"name": "GSPC.Close",
"price": 350.52,
"rsi": 65.402,
"ret": -0.0028448 
},
{
 "date":   7179,
"name": "GSPC.Close",
"price": 352.09,
"rsi":   63.4,
"ret": 0.0044791 
},
{
 "date":   7180,
"name": "GSPC.Close",
"price": 349.84,
"rsi": 65.201,
"ret": -0.0063904 
},
{
 "date":   7181,
"name": "GSPC.Close",
"price": 350.65,
"rsi":   60.6,
"ret": 0.0023153 
},
{
 "date":   7182,
"name": "GSPC.Close",
"price": 351.45,
"rsi": 61.649,
"ret": 0.0022815 
},
{
 "date":   7183,
"name": "GSPC.Close",
"price": 353.73,
"rsi": 62.705,
"ret": 0.0064874 
},
{
 "date":   7187,
"name": "GSPC.Close",
"price": 352.56,
"rsi": 65.613,
"ret": -0.0033076 
},
{
 "date":   7188,
"name": "GSPC.Close",
"price": 349.24,
"rsi": 62.903,
"ret": -0.0094168 
},
{
 "date":   7189,
"name": "GSPC.Close",
"price": 348.35,
"rsi": 55.854,
"ret": -0.0025484 
},
{
 "date":   7190,
"name": "GSPC.Close",
"price": 348.76,
"rsi": 54.103,
"ret": 0.001177 
},
{
 "date":   7193,
"name": "GSPC.Close",
"price": 347.66,
"rsi": 54.806,
"ret": -0.003154 
},
{
 "date":   7194,
"name": "GSPC.Close",
"price":  348.7,
"rsi": 52.484,
"ret": 0.0029914 
},
{
 "date":   7195,
"name": "GSPC.Close",
"price": 345.46,
"rsi": 54.449,
"ret": -0.0092917 
},
{
 "date":   7196,
"name": "GSPC.Close",
"price": 343.16,
"rsi": 47.816,
"ret": -0.0066578 
},
{
 "date":   7197,
"name": "GSPC.Close",
"price": 345.06,
"rsi": 43.742,
"ret": 0.0055368 
},
{
 "date":   7200,
"name": "GSPC.Close",
"price": 346.73,
"rsi": 47.706,
"ret": 0.0048397 
},
{
 "date":   7201,
"name": "GSPC.Close",
"price": 346.55,
"rsi": 50.975,
"ret": -0.00051914 
},
{
 "date":   7202,
"name": "GSPC.Close",
"price": 346.47,
"rsi": 50.608,
"ret": -0.00023085 
},
{
 "date":   7203,
"name": "GSPC.Close",
"price":  345.7,
"rsi": 50.434,
"ret": -0.0022224 
},
{
 "date":   7204,
"name": "GSPC.Close",
"price": 347.05,
"rsi": 48.699,
"ret": 0.0039051 
},
{
 "date":   7207,
"name": "GSPC.Close",
"price": 344.23,
"rsi": 51.828,
"ret": -0.0081256 
},
{
 "date":   7208,
"name": "GSPC.Close",
"price": 344.33,
"rsi": 45.575,
"ret": 0.0002905 
},
{
 "date":   7209,
"name": "GSPC.Close",
"price":  345.1,
"rsi": 45.825,
"ret": 0.0022362 
},
{
 "date":   7210,
"name": "GSPC.Close",
"price":  348.6,
"rsi":  47.81,
"ret": 0.010142 
},
{
 "date":   7211,
"name": "GSPC.Close",
"price": 349.15,
"rsi": 55.746,
"ret": 0.0015777 
},
{
 "date":   7214,
"name": "GSPC.Close",
"price": 350.87,
"rsi": 56.856,
"ret": 0.0049262 
},
{
 "date":   7215,
"name": "GSPC.Close",
"price": 354.71,
"rsi": 60.217,
"ret": 0.010944 
},
{
 "date":   7216,
"name": "GSPC.Close",
"price": 356.94,
"rsi": 66.493,
"ret": 0.0062868 
},
{
 "date":   7217,
"name": "GSPC.Close",
"price": 356.97,
"rsi": 69.502,
"ret": 8.4048e-05 
},
{
 "date":   7218,
"name": "GSPC.Close",
"price": 358.78,
"rsi": 69.542,
"ret": 0.0050705 
},
{
 "date":   7221,
"name": "GSPC.Close",
"price":  359.8,
"rsi": 71.913,
"ret": 0.002843 
},
{
 "date":   7222,
"name": "GSPC.Close",
"price": 359.13,
"rsi":  73.18,
"ret": -0.0018621 
},
{
 "date":   7223,
"name": "GSPC.Close",
"price": 356.99,
"rsi": 70.917,
"ret": -0.0059588 
},
{
 "date":   7224,
"name": "GSPC.Close",
"price": 355.39,
"rsi": 64.098,
"ret": -0.0044819 
},
{
 "date":   7225,
"name": "GSPC.Close",
"price": 333.65,
"rsi": 59.492,
"ret": -0.061172 
},
{
 "date":   7228,
"name": "GSPC.Close",
"price": 342.85,
"rsi":     29,
"ret": 0.027574 
},
{
 "date":   7229,
"name": "GSPC.Close",
"price": 341.16,
"rsi": 42.444,
"ret": -0.0049293 
},
{
 "date":   7230,
"name": "GSPC.Close",
"price": 341.76,
"rsi": 40.912,
"ret": 0.0017587 
},
{
 "date":   7231,
"name": "GSPC.Close",
"price": 347.13,
"rsi": 41.716,
"ret": 0.015713 
},
{
 "date":   7232,
"name": "GSPC.Close",
"price": 347.16,
"rsi": 48.478,
"ret": 8.6423e-05 
},
{
 "date":   7235,
"name": "GSPC.Close",
"price": 344.83,
"rsi": 48.514,
"ret": -0.0067116 
},
{
 "date":   7236,
"name": "GSPC.Close",
"price":  343.7,
"rsi":  45.84,
"ret": -0.003277 
},
{
 "date":   7237,
"name": "GSPC.Close",
"price":  342.5,
"rsi": 44.557,
"ret": -0.0034914 
},
{
 "date":   7238,
"name": "GSPC.Close",
"price": 337.93,
"rsi": 43.175,
"ret": -0.013343 
},
{
 "date":   7239,
"name": "GSPC.Close",
"price": 335.06,
"rsi": 38.303,
"ret": -0.0084929 
},
{
 "date":   7242,
"name": "GSPC.Close",
"price": 335.07,
"rsi": 35.587,
"ret": 2.9845e-05 
},
{
 "date":   7243,
"name": "GSPC.Close",
"price": 340.36,
"rsi": 35.605,
"ret": 0.015788 
},
{
 "date":   7244,
"name": "GSPC.Close",
"price":  341.2,
"rsi": 44.078,
"ret": 0.002468 
},
{
 "date":   7245,
"name": "GSPC.Close",
"price": 338.48,
"rsi": 45.309,
"ret": -0.0079719 
},
{
 "date":   7246,
"name": "GSPC.Close",
"price": 337.62,
"rsi":  42.08,
"ret": -0.0025408 
},
{
 "date":   7249,
"name": "GSPC.Close",
"price": 332.61,
"rsi": 41.083,
"ret": -0.014839 
},
{
 "date":   7250,
"name": "GSPC.Close",
"price": 334.81,
"rsi": 35.766,
"ret": 0.0066144 
},
{
 "date":   7251,
"name": "GSPC.Close",
"price": 338.15,
"rsi":  39.47,
"ret": 0.0099758 
},
{
 "date":   7252,
"name": "GSPC.Close",
"price": 336.57,
"rsi": 44.686,
"ret": -0.0046725 
},
{
 "date":   7253,
"name": "GSPC.Close",
"price":  339.1,
"rsi": 42.807,
"ret": 0.007517 
},
{
 "date":   7256,
"name": "GSPC.Close",
"price": 339.55,
"rsi": 46.674,
"ret": 0.001327 
},
{
 "date":   7257,
"name": "GSPC.Close",
"price": 337.99,
"rsi": 47.355,
"ret": -0.0045943 
},
{
 "date":   7258,
"name": "GSPC.Close",
"price": 340.54,
"rsi": 45.198,
"ret": 0.0075446 
},
{
 "date":   7259,
"name": "GSPC.Close",
"price": 340.58,
"rsi": 49.267,
"ret": 0.00011746 
},
{
 "date":   7260,
"name": "GSPC.Close",
"price": 341.61,
"rsi":  49.33,
"ret": 0.0030243 
},
{
 "date":   7263,
"name": "GSPC.Close",
"price": 339.35,
"rsi": 51.031,
"ret": -0.0066157 
},
{
 "date":   7264,
"name": "GSPC.Close",
"price": 339.59,
"rsi": 47.281,
"ret": 0.00070723 
},
{
 "date":   7265,
"name": "GSPC.Close",
"price": 341.91,
"rsi":  47.72,
"ret": 0.0068318 
},
{
 "date":   7267,
"name": "GSPC.Close",
"price": 343.97,
"rsi": 51.894,
"ret": 0.006025 
},
{
 "date":   7270,
"name": "GSPC.Close",
"price": 345.61,
"rsi": 55.306,
"ret": 0.0047679 
},
{
 "date":   7271,
"name": "GSPC.Close",
"price": 345.77,
"rsi": 57.868,
"ret": 0.00046295 
},
{
 "date":   7272,
"name": "GSPC.Close",
"price":  343.6,
"rsi": 58.121,
"ret": -0.0062758 
},
{
 "date":   7273,
"name": "GSPC.Close",
"price": 345.99,
"rsi": 53.447,
"ret": 0.0069558 
},
{
 "date":   7274,
"name": "GSPC.Close",
"price": 350.63,
"rsi":   57.5,
"ret": 0.013411 
},
{
 "date":   7277,
"name": "GSPC.Close",
"price": 351.41,
"rsi": 64.046,
"ret": 0.0022246 
},
{
 "date":   7278,
"name": "GSPC.Close",
"price": 349.58,
"rsi": 65.021,
"ret": -0.0052076 
},
{
 "date":   7279,
"name": "GSPC.Close",
"price": 348.55,
"rsi": 60.851,
"ret": -0.0029464 
},
{
 "date":   7280,
"name": "GSPC.Close",
"price": 347.59,
"rsi": 58.574,
"ret": -0.0027543 
},
{
 "date":   7281,
"name": "GSPC.Close",
"price": 348.69,
"rsi": 56.453,
"ret": 0.0031646 
},
{
 "date":   7284,
"name": "GSPC.Close",
"price": 348.56,
"rsi": 58.315,
"ret": -0.00037282 
},
{
 "date":   7285,
"name": "GSPC.Close",
"price": 351.73,
"rsi":     58,
"ret": 0.0090946 
},
{
 "date":   7286,
"name": "GSPC.Close",
"price": 352.75,
"rsi": 63.227,
"ret": 0.0029 
},
{
 "date":   7287,
"name": "GSPC.Close",
"price": 350.93,
"rsi": 64.747,
"ret": -0.0051595 
},
{
 "date":   7288,
"name": "GSPC.Close",
"price": 350.14,
"rsi": 59.982,
"ret": -0.0022512 
},
{
 "date":   7291,
"name": "GSPC.Close",
"price": 343.69,
"rsi": 57.987,
"ret": -0.018421 
},
{
 "date":   7292,
"name": "GSPC.Close",
"price": 342.46,
"rsi": 44.866,
"ret": -0.0035788 
},
{
 "date":   7293,
"name": "GSPC.Close",
"price": 342.84,
"rsi": 42.874,
"ret": 0.0011096 
},
{
 "date":   7294,
"name": "GSPC.Close",
"price": 344.78,
"rsi": 43.706,
"ret": 0.0056586 
},
{
 "date":   7295,
"name": "GSPC.Close",
"price": 347.42,
"rsi": 47.878,
"ret": 0.0076571 
},
{
 "date":   7299,
"name": "GSPC.Close",
"price": 346.81,
"rsi": 52.984,
"ret": -0.0017558 
},
{
 "date":   7300,
"name": "GSPC.Close",
"price": 348.81,
"rsi": 51.723,
"ret": 0.0057668 
},
{
 "date":   7301,
"name": "GSPC.Close",
"price": 350.67,
"rsi": 55.465,
"ret": 0.0053324 
},
{
 "date":   7302,
"name": "GSPC.Close",
"price":  353.4,
"rsi": 58.674,
"ret": 0.0077851 
},
{
 "date":   7306,
"name": "GSPC.Close",
"price": 359.69,
"rsi": 62.899,
"ret": 0.017799 
},
{
 "date":   7307,
"name": "GSPC.Close",
"price": 358.76,
"rsi": 70.405,
"ret": -0.0025856 
},
{
 "date":   7308,
"name": "GSPC.Close",
"price": 355.67,
"rsi": 68.208,
"ret": -0.008613 
},
{
 "date":   7309,
"name": "GSPC.Close",
"price":  352.2,
"rsi": 61.356,
"ret": -0.0097562 
},
{
 "date":   7312,
"name": "GSPC.Close",
"price": 353.79,
"rsi": 54.709,
"ret": 0.0045145 
},
{
 "date":   7313,
"name": "GSPC.Close",
"price": 349.62,
"rsi": 57.007,
"ret": -0.011787 
},
{
 "date":   7314,
"name": "GSPC.Close",
"price": 347.31,
"rsi": 49.861,
"ret": -0.0066072 
},
{
 "date":   7315,
"name": "GSPC.Close",
"price": 348.53,
"rsi": 46.392,
"ret": 0.0035127 
},
{
 "date":   7316,
"name": "GSPC.Close",
"price": 339.93,
"rsi": 48.432,
"ret": -0.024675 
},
{
 "date":   7319,
"name": "GSPC.Close",
"price":    337,
"rsi": 37.574,
"ret": -0.0086194 
},
{
 "date":   7320,
"name": "GSPC.Close",
"price": 340.75,
"rsi": 34.718,
"ret": 0.011128 
},
{
 "date":   7321,
"name": "GSPC.Close",
"price":  337.4,
"rsi": 40.909,
"ret": -0.0098313 
},
{
 "date":   7322,
"name": "GSPC.Close",
"price": 338.19,
"rsi": 37.488,
"ret": 0.0023414 
},
{
 "date":   7323,
"name": "GSPC.Close",
"price": 339.15,
"rsi": 38.788,
"ret": 0.0028386 
},
{
 "date":   7326,
"name": "GSPC.Close",
"price": 330.38,
"rsi": 40.409,
"ret": -0.025859 
},
{
 "date":   7327,
"name": "GSPC.Close",
"price": 331.61,
"rsi": 32.056,
"ret": 0.003723 
},
{
 "date":   7328,
"name": "GSPC.Close",
"price": 330.26,
"rsi": 34.113,
"ret": -0.004071 
},
{
 "date":   7329,
"name": "GSPC.Close",
"price": 326.08,
"rsi": 32.935,
"ret": -0.012657 
},
{
 "date":   7330,
"name": "GSPC.Close",
"price":  325.8,
"rsi": 29.532,
"ret": -0.00085868 
},
{
 "date":   7333,
"name": "GSPC.Close",
"price":  325.2,
"rsi": 29.314,
"ret": -0.0018416 
},
{
 "date":   7334,
"name": "GSPC.Close",
"price": 322.98,
"rsi": 28.822,
"ret": -0.0068266 
},
{
 "date":   7335,
"name": "GSPC.Close",
"price": 329.08,
"rsi": 27.015,
"ret": 0.018887 
},
{
 "date":   7336,
"name": "GSPC.Close",
"price": 328.79,
"rsi": 38.435,
"ret": -0.00088124 
},
{
 "date":   7337,
"name": "GSPC.Close",
"price": 330.92,
"rsi":  38.13,
"ret": 0.0064783 
},
{
 "date":   7340,
"name": "GSPC.Close",
"price": 331.85,
"rsi": 41.789,
"ret": 0.0028103 
},
{
 "date":   7341,
"name": "GSPC.Close",
"price": 329.66,
"rsi": 43.364,
"ret": -0.0065994 
},
{
 "date":   7342,
"name": "GSPC.Close",
"price": 333.75,
"rsi": 40.579,
"ret": 0.012407 
},
{
 "date":   7343,
"name": "GSPC.Close",
"price": 332.96,
"rsi": 47.375,
"ret": -0.002367 
},
{
 "date":   7344,
"name": "GSPC.Close",
"price": 333.62,
"rsi": 46.275,
"ret": 0.0019822 
},
{
 "date":   7347,
"name": "GSPC.Close",
"price": 330.08,
"rsi": 47.375,
"ret": -0.010611 
},
{
 "date":   7348,
"name": "GSPC.Close",
"price": 331.02,
"rsi": 42.364,
"ret": 0.0028478 
},
{
 "date":   7349,
"name": "GSPC.Close",
"price": 332.01,
"rsi": 44.056,
"ret": 0.0029908 
},
{
 "date":   7350,
"name": "GSPC.Close",
"price": 334.89,
"rsi": 45.859,
"ret": 0.0086744 
},
{
 "date":   7351,
"name": "GSPC.Close",
"price": 332.72,
"rsi": 50.824,
"ret": -0.0064797 
},
{
 "date":   7355,
"name": "GSPC.Close",
"price": 327.99,
"rsi": 47.304,
"ret": -0.014216 
},
{
 "date":   7356,
"name": "GSPC.Close",
"price": 327.67,
"rsi": 40.689,
"ret": -0.00097564 
},
{
 "date":   7357,
"name": "GSPC.Close",
"price":  325.7,
"rsi": 40.278,
"ret": -0.0060121 
},
{
 "date":   7358,
"name": "GSPC.Close",
"price": 324.15,
"rsi": 37.754,
"ret": -0.004759 
},
{
 "date":   7361,
"name": "GSPC.Close",
"price": 328.67,
"rsi":  35.85,
"ret": 0.013944 
},
{
 "date":   7362,
"name": "GSPC.Close",
"price": 330.26,
"rsi":  44.62,
"ret": 0.0048377 
},
{
 "date":   7363,
"name": "GSPC.Close",
"price": 331.89,
"rsi": 47.347,
"ret": 0.0049355 
},
{
 "date":   7364,
"name": "GSPC.Close",
"price": 332.74,
"rsi": 50.062,
"ret": 0.0025611 
},
{
 "date":   7365,
"name": "GSPC.Close",
"price": 335.54,
"rsi": 51.468,
"ret": 0.008415 
},
{
 "date":   7368,
"name": "GSPC.Close",
"price": 333.74,
"rsi": 55.873,
"ret": -0.0053645 
},
{
 "date":   7369,
"name": "GSPC.Close",
"price": 337.93,
"rsi": 52.569,
"ret": 0.012555 
},
{
 "date":   7370,
"name": "GSPC.Close",
"price": 336.95,
"rsi": 58.692,
"ret": -0.0029 
},
{
 "date":   7371,
"name": "GSPC.Close",
"price": 340.27,
"rsi": 56.844,
"ret": 0.0098531 
},
{
 "date":   7372,
"name": "GSPC.Close",
"price": 337.93,
"rsi": 61.291,
"ret": -0.0068769 
},
{
 "date":   7375,
"name": "GSPC.Close",
"price": 338.67,
"rsi": 56.845,
"ret": 0.0021898 
},
{
 "date":   7376,
"name": "GSPC.Close",
"price":    336,
"rsi": 57.885,
"ret": -0.0078838 
},
{
 "date":   7377,
"name": "GSPC.Close",
"price": 336.87,
"rsi": 52.927,
"ret": 0.0025893 
},
{
 "date":   7378,
"name": "GSPC.Close",
"price": 338.07,
"rsi":   54.3,
"ret": 0.0035622 
},
{
 "date":   7379,
"name": "GSPC.Close",
"price": 341.91,
"rsi": 56.199,
"ret": 0.011359 
},
{
 "date":   7382,
"name": "GSPC.Close",
"price": 343.53,
"rsi": 61.685,
"ret": 0.0047381 
},
{
 "date":   7383,
"name": "GSPC.Close",
"price": 341.57,
"rsi": 63.747,
"ret": -0.0057055 
},
{
 "date":   7384,
"name": "GSPC.Close",
"price": 339.74,
"rsi": 59.569,
"ret": -0.0053576 
},
{
 "date":   7385,
"name": "GSPC.Close",
"price": 335.69,
"rsi": 55.886,
"ret": -0.011921 
},
{
 "date":   7386,
"name": "GSPC.Close",
"price": 337.22,
"rsi": 48.708,
"ret": 0.0045578 
},
{
 "date":   7389,
"name": "GSPC.Close",
"price": 337.63,
"rsi": 51.255,
"ret": 0.0012158 
},
{
 "date":   7390,
"name": "GSPC.Close",
"price":  341.5,
"rsi": 51.943,
"ret": 0.011462 
},
{
 "date":   7391,
"name": "GSPC.Close",
"price":    342,
"rsi": 57.979,
"ret": 0.0014641 
},
{
 "date":   7392,
"name": "GSPC.Close",
"price": 340.79,
"rsi":   58.7,
"ret": -0.003538 
},
{
 "date":   7393,
"name": "GSPC.Close",
"price": 339.94,
"rsi": 56.186,
"ret": -0.0024942 
},
{
 "date":   7396,
"name": "GSPC.Close",
"price":  338.7,
"rsi": 54.422,
"ret": -0.0036477 
},
{
 "date":   7397,
"name": "GSPC.Close",
"price": 343.64,
"rsi": 51.864,
"ret": 0.014585 
},
{
 "date":   7398,
"name": "GSPC.Close",
"price": 341.09,
"rsi": 59.941,
"ret": -0.0074206 
},
{
 "date":   7399,
"name": "GSPC.Close",
"price": 340.73,
"rsi": 54.827,
"ret": -0.0010554 
},
{
 "date":   7400,
"name": "GSPC.Close",
"price": 340.08,
"rsi": 54.125,
"ret": -0.0019077 
},
{
 "date":   7403,
"name": "GSPC.Close",
"price": 341.37,
"rsi":  52.81,
"ret": 0.0037932 
},
{
 "date":   7404,
"name": "GSPC.Close",
"price": 342.07,
"rsi": 55.139,
"ret": 0.0020506 
},
{
 "date":   7405,
"name": "GSPC.Close",
"price": 341.92,
"rsi": 56.397,
"ret": -0.00043851 
},
{
 "date":   7406,
"name": "GSPC.Close",
"price": 344.34,
"rsi": 56.035,
"ret": 0.0070777 
},
{
 "date":   7410,
"name": "GSPC.Close",
"price": 344.74,
"rsi": 60.452,
"ret": 0.0011616 
},
{
 "date":   7411,
"name": "GSPC.Close",
"price": 344.68,
"rsi": 61.147,
"ret": -0.00017404 
},
{
 "date":   7412,
"name": "GSPC.Close",
"price": 340.72,
"rsi": 60.974,
"ret": -0.011489 
},
{
 "date":   7413,
"name": "GSPC.Close",
"price": 338.09,
"rsi": 50.762,
"ret": -0.0077189 
},
{
 "date":   7414,
"name": "GSPC.Close",
"price": 335.12,
"rsi": 45.332,
"ret": -0.0087846 
},
{
 "date":   7417,
"name": "GSPC.Close",
"price": 331.05,
"rsi": 40.114,
"ret": -0.012145 
},
{
 "date":   7418,
"name": "GSPC.Close",
"price": 330.36,
"rsi": 34.289,
"ret": -0.0020843 
},
{
 "date":   7419,
"name": "GSPC.Close",
"price": 332.03,
"rsi": 33.403,
"ret": 0.0050551 
},
{
 "date":   7420,
"name": "GSPC.Close",
"price": 332.92,
"rsi": 37.603,
"ret": 0.0026805 
},
{
 "date":   7421,
"name": "GSPC.Close",
"price": 329.11,
"rsi": 39.783,
"ret": -0.011444 
},
{
 "date":   7424,
"name": "GSPC.Close",
"price":  330.8,
"rsi": 34.265,
"ret": 0.0051351 
},
{
 "date":   7425,
"name": "GSPC.Close",
"price": 332.25,
"rsi":  38.35,
"ret": 0.0043833 
},
{
 "date":   7426,
"name": "GSPC.Close",
"price": 334.48,
"rsi": 41.698,
"ret": 0.0067118 
},
{
 "date":   7427,
"name": "GSPC.Close",
"price": 335.57,
"rsi": 46.509,
"ret": 0.0032588 
},
{
 "date":   7428,
"name": "GSPC.Close",
"price": 338.39,
"rsi": 48.735,
"ret": 0.0084036 
},
{
 "date":   7431,
"name": "GSPC.Close",
"price": 340.53,
"rsi": 54.063,
"ret": 0.0063241 
},
{
 "date":   7432,
"name": "GSPC.Close",
"price": 342.01,
"rsi": 57.659,
"ret": 0.0043462 
},
{
 "date":   7433,
"name": "GSPC.Close",
"price": 342.86,
"rsi": 59.992,
"ret": 0.0024853 
},
{
 "date":   7434,
"name": "GSPC.Close",
"price": 343.82,
"rsi": 61.311,
"ret": 0.0028 
},
{
 "date":   7435,
"name": "GSPC.Close",
"price":    352,
"rsi": 62.801,
"ret": 0.023792 
},
{
 "date":   7438,
"name": "GSPC.Close",
"price": 354.75,
"rsi": 72.519,
"ret": 0.0078125 
},
{
 "date":   7439,
"name": "GSPC.Close",
"price": 354.28,
"rsi": 74.894,
"ret": -0.0013249 
},
{
 "date":   7440,
"name": "GSPC.Close",
"price":    354,
"rsi": 73.721,
"ret": -0.00079034 
},
{
 "date":   7441,
"name": "GSPC.Close",
"price": 354.47,
"rsi": 72.988,
"ret": 0.0013277 
},
{
 "date":   7442,
"name": "GSPC.Close",
"price": 354.64,
"rsi": 73.465,
"ret": 0.00047959 
},
{
 "date":   7445,
"name": "GSPC.Close",
"price":    358,
"rsi": 73.646,
"ret": 0.0094744 
},
{
 "date":   7446,
"name": "GSPC.Close",
"price": 358.43,
"rsi": 76.992,
"ret": 0.0012011 
},
{
 "date":   7447,
"name": "GSPC.Close",
"price": 359.29,
"rsi": 77.387,
"ret": 0.0023994 
},
{
 "date":   7448,
"name": "GSPC.Close",
"price": 358.41,
"rsi": 78.195,
"ret": -0.0024493 
},
{
 "date":   7449,
"name": "GSPC.Close",
"price": 354.58,
"rsi": 75.234,
"ret": -0.010686 
},
{
 "date":   7453,
"name": "GSPC.Close",
"price": 360.65,
"rsi": 63.895,
"ret": 0.017119 
},
{
 "date":   7454,
"name": "GSPC.Close",
"price": 360.86,
"rsi": 71.282,
"ret": 0.00058228 
},
{
 "date":   7455,
"name": "GSPC.Close",
"price": 361.23,
"rsi":   71.5,
"ret": 0.0010253 
},
{
 "date":   7456,
"name": "GSPC.Close",
"price": 363.16,
"rsi": 71.903,
"ret": 0.0053429 
},
{
 "date":   7459,
"name": "GSPC.Close",
"price":  367.4,
"rsi": 73.972,
"ret": 0.011675 
},
{
 "date":   7460,
"name": "GSPC.Close",
"price": 366.64,
"rsi": 77.834,
"ret": -0.0020686 
},
{
 "date":   7461,
"name": "GSPC.Close",
"price": 364.96,
"rsi": 75.667,
"ret": -0.0045822 
},
{
 "date":   7462,
"name": "GSPC.Close",
"price": 363.15,
"rsi": 70.963,
"ret": -0.0049594 
},
{
 "date":   7463,
"name": "GSPC.Close",
"price": 358.71,
"rsi": 66.189,
"ret": -0.012226 
},
{
 "date":   7466,
"name": "GSPC.Close",
"price": 361.63,
"rsi": 56.201,
"ret": 0.0081403 
},
{
 "date":   7467,
"name": "GSPC.Close",
"price": 366.25,
"rsi":  60.43,
"ret": 0.012775 
},
{
 "date":   7468,
"name": "GSPC.Close",
"price":  364.9,
"rsi":  66.02,
"ret": -0.003686 
},
{
 "date":   7469,
"name": "GSPC.Close",
"price":  362.9,
"rsi":  63.21,
"ret": -0.005481 
},
{
 "date":   7470,
"name": "GSPC.Close",
"price": 362.91,
"rsi":  59.19,
"ret": 2.7556e-05 
},
{
 "date":   7473,
"name": "GSPC.Close",
"price": 356.88,
"rsi": 59.204,
"ret": -0.016616 
},
{
 "date":   7474,
"name": "GSPC.Close",
"price": 358.47,
"rsi": 48.437,
"ret": 0.0044553 
},
{
 "date":   7475,
"name": "GSPC.Close",
"price":  359.1,
"rsi": 50.969,
"ret": 0.0017575 
},
{
 "date":   7476,
"name": "GSPC.Close",
"price": 360.47,
"rsi": 51.976,
"ret": 0.0038151 
},
{
 "date":   7477,
"name": "GSPC.Close",
"price": 355.43,
"rsi": 54.178,
"ret": -0.013982 
},
{
 "date":   7480,
"name": "GSPC.Close",
"price": 352.31,
"rsi": 45.848,
"ret": -0.0087781 
},
{
 "date":   7481,
"name": "GSPC.Close",
"price": 352.06,
"rsi": 41.585,
"ret": -0.0007096 
},
{
 "date":   7482,
"name": "GSPC.Close",
"price": 355.14,
"rsi": 41.254,
"ret": 0.0087485 
},
{
 "date":   7483,
"name": "GSPC.Close",
"price": 357.63,
"rsi": 46.865,
"ret": 0.0070113 
},
{
 "date":   7484,
"name": "GSPC.Close",
"price": 358.02,
"rsi": 50.944,
"ret": 0.0010905 
},
{
 "date":   7487,
"name": "GSPC.Close",
"price": 359.54,
"rsi": 51.571,
"ret": 0.0042456 
},
{
 "date":   7488,
"name": "GSPC.Close",
"price": 360.16,
"rsi": 54.038,
"ret": 0.0017244 
},
{
 "date":   7490,
"name": "GSPC.Close",
"price": 355.68,
"rsi": 55.043,
"ret": -0.012439 
},
{
 "date":   7491,
"name": "GSPC.Close",
"price": 358.42,
"rsi": 47.035,
"ret": 0.0077036 
},
{
 "date":   7494,
"name": "GSPC.Close",
"price": 359.52,
"rsi": 51.667,
"ret": 0.003069 
},
{
 "date":   7495,
"name": "GSPC.Close",
"price": 356.49,
"rsi": 53.428,
"ret": -0.0084279 
},
{
 "date":   7496,
"name": "GSPC.Close",
"price": 361.23,
"rsi": 48.217,
"ret": 0.013296 
},
{
 "date":   7497,
"name": "GSPC.Close",
"price": 365.44,
"rsi": 55.524,
"ret": 0.011655 
},
{
 "date":   7498,
"name": "GSPC.Close",
"price": 367.31,
"rsi": 60.814,
"ret": 0.0051171 
},
{
 "date":   7501,
"name": "GSPC.Close",
"price": 368.95,
"rsi": 62.923,
"ret": 0.0044649 
},
{
 "date":   7502,
"name": "GSPC.Close",
"price": 367.52,
"rsi": 64.717,
"ret": -0.0038759 
},
{
 "date":   7503,
"name": "GSPC.Close",
"price": 364.22,
"rsi": 61.905,
"ret": -0.0089791 
},
{
 "date":   7504,
"name": "GSPC.Close",
"price": 365.32,
"rsi": 55.871,
"ret": 0.0030202 
},
{
 "date":   7505,
"name": "GSPC.Close",
"price": 361.61,
"rsi": 57.363,
"ret": -0.010155 
},
{
 "date":   7508,
"name": "GSPC.Close",
"price": 355.31,
"rsi":  51.09,
"ret": -0.017422 
},
{
 "date":   7509,
"name": "GSPC.Close",
"price": 355.79,
"rsi": 42.575,
"ret": 0.0013509 
},
{
 "date":   7510,
"name": "GSPC.Close",
"price": 357.09,
"rsi":  43.35,
"ret": 0.0036538 
},
{
 "date":   7511,
"name": "GSPC.Close",
"price": 355.91,
"rsi": 45.494,
"ret": -0.0033045 
},
{
 "date":   7512,
"name": "GSPC.Close",
"price": 353.44,
"rsi": 43.871,
"ret": -0.00694 
},
{
 "date":   7515,
"name": "GSPC.Close",
"price": 355.55,
"rsi": 40.604,
"ret": 0.0059699 
},
{
 "date":   7516,
"name": "GSPC.Close",
"price": 356.15,
"rsi": 44.412,
"ret": 0.0016875 
},
{
 "date":   7517,
"name": "GSPC.Close",
"price": 355.52,
"rsi": 45.482,
"ret": -0.0017689 
},
{
 "date":   7518,
"name": "GSPC.Close",
"price": 351.48,
"rsi": 44.513,
"ret": -0.011364 
},
{
 "date":   7519,
"name": "GSPC.Close",
"price": 344.86,
"rsi": 38.803,
"ret": -0.018835 
},
{
 "date":   7522,
"name": "GSPC.Close",
"price": 334.43,
"rsi": 31.641,
"ret": -0.030244 
},
{
 "date":   7523,
"name": "GSPC.Close",
"price": 334.83,
"rsi": 24.095,
"ret": 0.0011961 
},
{
 "date":   7524,
"name": "GSPC.Close",
"price": 338.35,
"rsi": 24.836,
"ret": 0.010513 
},
{
 "date":   7525,
"name": "GSPC.Close",
"price": 339.94,
"rsi": 31.196,
"ret": 0.0046993 
},
{
 "date":   7526,
"name": "GSPC.Close",
"price": 335.52,
"rsi": 33.916,
"ret": -0.013002 
},
{
 "date":   7529,
"name": "GSPC.Close",
"price": 338.84,
"rsi": 30.327,
"ret": 0.0098951 
},
{
 "date":   7530,
"name": "GSPC.Close",
"price": 339.39,
"rsi":  35.82,
"ret": 0.0016232 
},
{
 "date":   7531,
"name": "GSPC.Close",
"price": 340.06,
"rsi": 36.711,
"ret": 0.0019741 
},
{
 "date":   7532,
"name": "GSPC.Close",
"price": 332.39,
"rsi": 37.842,
"ret": -0.022555 
},
{
 "date":   7533,
"name": "GSPC.Close",
"price": 327.83,
"rsi": 31.009,
"ret": -0.013719 
},
{
 "date":   7536,
"name": "GSPC.Close",
"price": 328.51,
"rsi": 27.796,
"ret": 0.0020742 
},
{
 "date":   7537,
"name": "GSPC.Close",
"price": 321.86,
"rsi": 28.977,
"ret": -0.020243 
},
{
 "date":   7538,
"name": "GSPC.Close",
"price": 316.55,
"rsi": 24.716,
"ret": -0.016498 
},
{
 "date":   7539,
"name": "GSPC.Close",
"price": 307.06,
"rsi": 21.942,
"ret": -0.029979 
},
{
 "date":   7540,
"name": "GSPC.Close",
"price": 311.51,
"rsi": 18.043,
"ret": 0.014492 
},
{
 "date":   7543,
"name": "GSPC.Close",
"price": 321.44,
"rsi": 24.791,
"ret": 0.031877 
},
{
 "date":   7544,
"name": "GSPC.Close",
"price": 321.34,
"rsi": 37.214,
"ret": -0.0003111 
},
{
 "date":   7545,
"name": "GSPC.Close",
"price": 324.19,
"rsi": 37.147,
"ret": 0.0088691 
},
{
 "date":   7546,
"name": "GSPC.Close",
"price": 318.71,
"rsi": 40.417,
"ret": -0.016904 
},
{
 "date":   7547,
"name": "GSPC.Close",
"price": 322.56,
"rsi": 36.487,
"ret": 0.01208 
},
{
 "date":   7551,
"name": "GSPC.Close",
"price": 323.09,
"rsi":  40.84,
"ret": 0.0016431 
},
{
 "date":   7552,
"name": "GSPC.Close",
"price": 324.39,
"rsi": 41.435,
"ret": 0.0040236 
},
{
 "date":   7553,
"name": "GSPC.Close",
"price": 320.46,
"rsi": 42.951,
"ret": -0.012115 
},
{
 "date":   7554,
"name": "GSPC.Close",
"price":  323.4,
"rsi": 39.613,
"ret": 0.0091743 
},
{
 "date":   7557,
"name": "GSPC.Close",
"price": 321.63,
"rsi": 43.171,
"ret": -0.0054731 
},
{
 "date":   7558,
"name": "GSPC.Close",
"price": 321.04,
"rsi": 41.582,
"ret": -0.0018344 
},
{
 "date":   7559,
"name": "GSPC.Close",
"price": 322.54,
"rsi":  41.04,
"ret": 0.0046723 
},
{
 "date":   7560,
"name": "GSPC.Close",
"price": 318.65,
"rsi": 43.072,
"ret": -0.012061 
},
{
 "date":   7561,
"name": "GSPC.Close",
"price": 316.83,
"rsi":  39.29,
"ret": -0.0057116 
},
{
 "date":   7564,
"name": "GSPC.Close",
"price": 317.77,
"rsi": 37.626,
"ret": 0.0029669 
},
{
 "date":   7565,
"name": "GSPC.Close",
"price":  318.6,
"rsi": 39.062,
"ret": 0.002612 
},
{
 "date":   7566,
"name": "GSPC.Close",
"price":  316.6,
"rsi": 40.367,
"ret": -0.0062775 
},
{
 "date":   7567,
"name": "GSPC.Close",
"price": 311.48,
"rsi": 38.241,
"ret": -0.016172 
},
{
 "date":   7568,
"name": "GSPC.Close",
"price": 311.32,
"rsi": 33.393,
"ret": -0.00051368 
},
{
 "date":   7571,
"name": "GSPC.Close",
"price": 304.59,
"rsi": 33.251,
"ret": -0.021618 
},
{
 "date":   7572,
"name": "GSPC.Close",
"price": 308.26,
"rsi": 27.885,
"ret": 0.012049 
},
{
 "date":   7573,
"name": "GSPC.Close",
"price": 305.06,
"rsi": 34.128,
"ret": -0.010381 
},
{
 "date":   7574,
"name": "GSPC.Close",
"price": 300.97,
"rsi": 31.562,
"ret": -0.013407 
},
{
 "date":   7575,
"name": "GSPC.Close",
"price": 306.05,
"rsi": 28.602,
"ret": 0.016879 
},
{
 "date":   7578,
"name": "GSPC.Close",
"price": 314.94,
"rsi":  36.56,
"ret": 0.029048 
},
{
 "date":   7579,
"name": "GSPC.Close",
"price": 315.21,
"rsi": 47.573,
"ret": 0.00085731 
},
{
 "date":   7580,
"name": "GSPC.Close",
"price":  311.4,
"rsi": 47.869,
"ret": -0.012087 
},
{
 "date":   7581,
"name": "GSPC.Close",
"price": 312.69,
"rsi": 44.086,
"ret": 0.0041426 
},
{
 "date":   7582,
"name": "GSPC.Close",
"price":  311.5,
"rsi": 45.652,
"ret": -0.0038057 
},
{
 "date":   7585,
"name": "GSPC.Close",
"price": 313.48,
"rsi": 44.416,
"ret": 0.0063563 
},
{
 "date":   7586,
"name": "GSPC.Close",
"price":  305.1,
"rsi": 46.988,
"ret": -0.026732 
},
{
 "date":   7587,
"name": "GSPC.Close",
"price": 300.39,
"rsi": 38.806,
"ret": -0.015438 
},
{
 "date":   7588,
"name": "GSPC.Close",
"price": 295.46,
"rsi": 35.106,
"ret": -0.016412 
},
{
 "date":   7589,
"name": "GSPC.Close",
"price": 300.03,
"rsi": 31.699,
"ret": 0.015467 
},
{
 "date":   7592,
"name": "GSPC.Close",
"price": 303.23,
"rsi": 37.732,
"ret": 0.010666 
},
{
 "date":   7593,
"name": "GSPC.Close",
"price": 298.92,
"rsi":  41.62,
"ret": -0.014214 
},
{
 "date":   7594,
"name": "GSPC.Close",
"price": 298.76,
"rsi": 38.163,
"ret": -0.00053526 
},
{
 "date":   7595,
"name": "GSPC.Close",
"price": 305.74,
"rsi": 38.037,
"ret": 0.023363 
},
{
 "date":   7596,
"name": "GSPC.Close",
"price": 312.48,
"rsi": 46.374,
"ret": 0.022045 
},
{
 "date":   7599,
"name": "GSPC.Close",
"price": 314.76,
"rsi": 52.957,
"ret": 0.0072965 
},
{
 "date":   7600,
"name": "GSPC.Close",
"price": 312.36,
"rsi":  54.97,
"ret": -0.0076249 
},
{
 "date":   7601,
"name": "GSPC.Close",
"price":  312.6,
"rsi": 52.426,
"ret": 0.00076834 
},
{
 "date":   7602,
"name": "GSPC.Close",
"price": 310.17,
"rsi": 52.662,
"ret": -0.0077735 
},
{
 "date":   7603,
"name": "GSPC.Close",
"price": 304.71,
"rsi": 49.961,
"ret": -0.017603 
},
{
 "date":   7606,
"name": "GSPC.Close",
"price": 301.88,
"rsi": 44.444,
"ret": -0.0092875 
},
{
 "date":   7607,
"name": "GSPC.Close",
"price": 304.06,
"rsi": 41.864,
"ret": 0.0072214 
},
{
 "date":   7608,
"name": "GSPC.Close",
"price":    304,
"rsi": 44.535,
"ret": -0.00019733 
},
{
 "date":   7609,
"name": "GSPC.Close",
"price": 307.02,
"rsi": 44.475,
"ret": 0.0099342 
},
{
 "date":   7610,
"name": "GSPC.Close",
"price": 311.85,
"rsi": 48.287,
"ret": 0.015732 
},
{
 "date":   7613,
"name": "GSPC.Close",
"price": 314.59,
"rsi": 53.756,
"ret": 0.0087863 
},
{
 "date":   7614,
"name": "GSPC.Close",
"price": 311.62,
"rsi": 56.562,
"ret": -0.0094409 
},
{
 "date":   7615,
"name": "GSPC.Close",
"price": 306.01,
"rsi": 52.821,
"ret": -0.018003 
},
{
 "date":   7616,
"name": "GSPC.Close",
"price": 307.61,
"rsi": 46.556,
"ret": 0.0052286 
},
{
 "date":   7617,
"name": "GSPC.Close",
"price": 313.74,
"rsi": 48.434,
"ret": 0.019928 
},
{
 "date":   7620,
"name": "GSPC.Close",
"price": 319.48,
"rsi": 54.965,
"ret": 0.018295 
},
{
 "date":   7621,
"name": "GSPC.Close",
"price": 317.67,
"rsi": 60.066,
"ret": -0.0056655 
},
{
 "date":   7622,
"name": "GSPC.Close",
"price":  320.4,
"rsi": 57.841,
"ret": 0.0085938 
},
{
 "date":   7623,
"name": "GSPC.Close",
"price": 317.02,
"rsi": 60.233,
"ret": -0.010549 
},
{
 "date":   7624,
"name": "GSPC.Close",
"price": 317.12,
"rsi": 55.997,
"ret": 0.00031544 
},
{
 "date":   7627,
"name": "GSPC.Close",
"price": 319.34,
"rsi": 56.095,
"ret": 0.0070005 
},
{
 "date":   7628,
"name": "GSPC.Close",
"price": 315.31,
"rsi": 58.323,
"ret": -0.01262 
},
{
 "date":   7629,
"name": "GSPC.Close",
"price": 316.03,
"rsi": 53.059,
"ret": 0.0022835 
},
{
 "date":   7631,
"name": "GSPC.Close",
"price":  315.1,
"rsi": 53.861,
"ret": -0.0029428 
},
{
 "date":   7634,
"name": "GSPC.Close",
"price": 316.51,
"rsi": 52.611,
"ret": 0.0044748 
},
{
 "date":   7635,
"name": "GSPC.Close",
"price":  318.1,
"rsi":  54.34,
"ret": 0.0050235 
},
{
 "date":   7636,
"name": "GSPC.Close",
"price": 317.95,
"rsi": 56.278,
"ret": -0.00047155 
},
{
 "date":   7637,
"name": "GSPC.Close",
"price": 316.42,
"rsi": 56.036,
"ret": -0.0048121 
},
{
 "date":   7638,
"name": "GSPC.Close",
"price": 322.22,
"rsi": 53.513,
"ret": 0.01833 
},
{
 "date":   7641,
"name": "GSPC.Close",
"price":  324.1,
"rsi": 60.731,
"ret": 0.0058345 
},
{
 "date":   7642,
"name": "GSPC.Close",
"price": 326.35,
"rsi":  62.75,
"ret": 0.0069423 
},
{
 "date":   7643,
"name": "GSPC.Close",
"price": 329.92,
"rsi": 65.065,
"ret": 0.010939 
},
{
 "date":   7644,
"name": "GSPC.Close",
"price": 329.07,
"rsi": 68.419,
"ret": -0.0025764 
},
{
 "date":   7645,
"name": "GSPC.Close",
"price": 327.75,
"rsi": 66.775,
"ret": -0.0040113 
},
{
 "date":   7648,
"name": "GSPC.Close",
"price": 328.89,
"rsi": 64.196,
"ret": 0.0034783 
},
{
 "date":   7649,
"name": "GSPC.Close",
"price": 326.44,
"rsi": 65.437,
"ret": -0.0074493 
},
{
 "date":   7650,
"name": "GSPC.Close",
"price": 330.19,
"rsi": 60.576,
"ret": 0.011488 
},
{
 "date":   7651,
"name": "GSPC.Close",
"price": 329.34,
"rsi": 64.877,
"ret": -0.0025743 
},
{
 "date":   7652,
"name": "GSPC.Close",
"price": 326.82,
"rsi": 63.194,
"ret": -0.0076517 
},
{
 "date":   7655,
"name": "GSPC.Close",
"price": 326.02,
"rsi":  58.36,
"ret": -0.0024478 
},
{
 "date":   7656,
"name": "GSPC.Close",
"price": 330.05,
"rsi": 56.873,
"ret": 0.012361 
},
{
 "date":   7657,
"name": "GSPC.Close",
"price":  330.2,
"rsi": 62.111,
"ret": 0.00045448 
},
{
 "date":   7658,
"name": "GSPC.Close",
"price": 330.12,
"rsi": 62.295,
"ret": -0.00024228 
},
{
 "date":   7659,
"name": "GSPC.Close",
"price": 331.75,
"rsi": 62.122,
"ret": 0.0049376 
},
{
 "date":   7662,
"name": "GSPC.Close",
"price":  329.9,
"rsi": 64.296,
"ret": -0.0055765 
},
{
 "date":   7664,
"name": "GSPC.Close",
"price": 330.85,
"rsi": 60.081,
"ret": 0.0028797 
},
{
 "date":   7665,
"name": "GSPC.Close",
"price": 328.29,
"rsi": 61.478,
"ret": -0.0077376 
},
{
 "date":   7666,
"name": "GSPC.Close",
"price": 328.72,
"rsi": 55.811,
"ret": 0.0013098 
},
{
 "date":   7669,
"name": "GSPC.Close",
"price": 330.22,
"rsi": 56.536,
"ret": 0.0045632 
},
{
 "date":   7671,
"name": "GSPC.Close",
"price": 326.45,
"rsi": 59.058,
"ret": -0.011417 
},
{
 "date":   7672,
"name": "GSPC.Close",
"price": 321.91,
"rsi": 51.041,
"ret": -0.013907 
},
{
 "date":   7673,
"name": "GSPC.Close",
"price":    321,
"rsi":   43.4,
"ret": -0.0028269 
},
{
 "date":   7676,
"name": "GSPC.Close",
"price": 315.44,
"rsi": 42.042,
"ret": -0.017321 
},
{
 "date":   7677,
"name": "GSPC.Close",
"price":  314.9,
"rsi": 34.862,
"ret": -0.0017119 
},
{
 "date":   7678,
"name": "GSPC.Close",
"price": 311.49,
"rsi":  34.25,
"ret": -0.010829 
},
{
 "date":   7679,
"name": "GSPC.Close",
"price": 314.53,
"rsi": 30.598,
"ret": 0.0097595 
},
{
 "date":   7680,
"name": "GSPC.Close",
"price": 315.23,
"rsi": 37.043,
"ret": 0.0022255 
},
{
 "date":   7683,
"name": "GSPC.Close",
"price": 312.49,
"rsi":  38.46,
"ret": -0.0086921 
},
{
 "date":   7684,
"name": "GSPC.Close",
"price": 313.73,
"rsi": 35.127,
"ret": 0.0039681 
},
{
 "date":   7685,
"name": "GSPC.Close",
"price": 316.17,
"rsi": 37.756,
"ret": 0.0077774 
},
{
 "date":   7686,
"name": "GSPC.Close",
"price": 327.97,
"rsi": 42.678,
"ret": 0.037322 
},
{
 "date":   7687,
"name": "GSPC.Close",
"price": 332.23,
"rsi":   59.4,
"ret": 0.012989 
},
{
 "date":   7690,
"name": "GSPC.Close",
"price": 331.06,
"rsi": 63.536,
"ret": -0.0035217 
},
{
 "date":   7691,
"name": "GSPC.Close",
"price": 328.31,
"rsi": 61.677,
"ret": -0.0083067 
},
{
 "date":   7692,
"name": "GSPC.Close",
"price": 330.21,
"rsi": 57.426,
"ret": 0.0057872 
},
{
 "date":   7693,
"name": "GSPC.Close",
"price": 334.78,
"rsi": 59.503,
"ret": 0.01384 
},
{
 "date":   7694,
"name": "GSPC.Close",
"price": 336.07,
"rsi": 64.046,
"ret": 0.0038533 
},
{
 "date":   7697,
"name": "GSPC.Close",
"price": 336.03,
"rsi": 65.232,
"ret": -0.00011902 
},
{
 "date":   7698,
"name": "GSPC.Close",
"price": 335.84,
"rsi":  65.16,
"ret": -0.00056543 
},
{
 "date":   7699,
"name": "GSPC.Close",
"price": 340.91,
"rsi": 64.796,
"ret": 0.015096 
},
{
 "date":   7700,
"name": "GSPC.Close",
"price": 343.93,
"rsi": 69.673,
"ret": 0.0088586 
},
{
 "date":   7701,
"name": "GSPC.Close",
"price": 343.05,
"rsi": 72.148,
"ret": -0.0025587 
},
{
 "date":   7704,
"name": "GSPC.Close",
"price": 348.34,
"rsi": 70.346,
"ret": 0.01542 
},
{
 "date":   7705,
"name": "GSPC.Close",
"price": 351.26,
"rsi": 74.473,
"ret": 0.0083826 
},
{
 "date":   7706,
"name": "GSPC.Close",
"price": 358.07,
"rsi": 76.423,
"ret": 0.019387 
},
{
 "date":   7707,
"name": "GSPC.Close",
"price": 356.52,
"rsi": 80.219,
"ret": -0.0043288 
},
{
 "date":   7708,
"name": "GSPC.Close",
"price": 359.35,
"rsi": 77.173,
"ret": 0.0079378 
},
{
 "date":   7711,
"name": "GSPC.Close",
"price": 368.58,
"rsi": 78.759,
"ret": 0.025685 
},
{
 "date":   7712,
"name": "GSPC.Close",
"price":  365.5,
"rsi": 82.925,
"ret": -0.0083564 
},
{
 "date":   7713,
"name": "GSPC.Close",
"price": 369.02,
"rsi": 77.465,
"ret": 0.0096306 
},
{
},
