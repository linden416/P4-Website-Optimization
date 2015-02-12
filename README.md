# P4-Website-Optimization
Project 4 Web Optimization and Performance / Front-End Web Developer Nanodegree

2-11-2015

Student

	Gordon Seeler
	Front-end Web Developer
	Cohort 2
	gs6687@att.com

Summary Objective

	This project enforces skills for altering the Critical Rendering Path,
	Content Efficiency, Computation Efficiency, and Framerate.

Installation Instructions

	GitHub address: https://github.com/linden416/P4-Website-Optimization.git

	Download GitHub repository and open local index.html and ./views/pizza.html files.

Instructions 

	1. Crticical Rendering Path Test:
	
		* Open the link to Google PageSpeed Insights and specify the URL to the index.html folder. This opens up a cloned optimized version of Cameron's portfolio website. View Mobile and Desktop scores, the optimized score is 91 for Mobile. This is an improvement from Cameron's base portfolio website which produced as score of 77.
	
		Optimizations:

		a) Added async to the script URL calls for the following JavaScript links:
			-  <script async src="http://www.google-analytics.com/analytics.js"></script>
    		
    		-  <script async src="js/perfmatters.js"></script

		b) Added media query to the print style sheet

		    -  <link href="css/print.css" rel="stylesheet" media="print">

		c) Converted the style.css file to inline code in the index.html page

		d) Removed the Google Fonts link and replaced it with the Google Fonts JavaScript API. Configured the API to run ASYNC.

		d) Optimized the following images:
			- Changed the 2048.png to a JPG file. Opacity was not needed so no need for PNG. This cut the size down a modest 8KB. 

			- Cut the size down and optimization quality level for the following images:
				+ cam_be_like.jpg to 63Kb down from 262Kb

				+ mobilewebdev.jpg to 47Kb down from 187Kb


	2. Content & Computational Efficiency and Framerate Test:
	
		* Open Chrome and open the file ./views/pizza.html 
		* Open Chrome Developer Tools and use the Timeline to view the 60 FPS threshold and Console to view Timing API statistics

		1. Scroll down and up the page as pizzas are sliding in the background. Analyze the average frame rate per 10 frames. Analyze the FPS monitor (Dev Tool) in the upper right corner. Scores are indicating an average of 0.20 ms to generate 10 frames which is a major improvement from the 21.0 ms average from Cameron's base site. 

		2. Open Dev Tool Timeline and record events as you again scroll down and up the page. Stop recording and view the scores which show a consistent rate in the 60 FPS threshold. This is a major improvement from Cameron's base portfolio site which produce a rate FAR LESS THAN 30 FPS.

		3. Slide the pizza size slider widget on the page. Analyze the time to resize pizzas, the time to produce the pizzas is showing scores of 1.09ms. Cameron's base site is producing a score of 103.9 ms. This achieves the rubric score of less than 5 ms.

		Optimizations:

		a) The default number of sliding "mover" pizzas created after the DOMContentLoaded event was 200. This made little sense because only 32 (8 per row; 4 rows) were needed to fill the page with the largest resolution. Changed the number to 32.

		b) The resizePizzas function which is called when the html slider widget is moved from small, medium, or large:
			- Merged the individual "sub" functions (4 in total) into the code of the function itself.

			- Removed the unneccesary repetition in the processing of each pizza specifically the logic for calculating the difference to change the size of each pizza. This calculation is only needed once since the pies will all be the same size. The one time calculation is applied to each pizza width only.

		c) The original javascript for generating a new pizza and its' ingredients utilized upwards to 10+ functions most of which contained only a few lines of code. To avoid the added cost calling these functions, I merged them down to 3 while maintaining good readability and even improving the names like chaning "generator" to "generatePizzaName".

		d) Changed all document.querySelector and document.querySelectorAll to use the faster performing document.getElementById and document.getElementsByClassName (see ** resource below).

		e) Changed all ParseInt functions to Math.floor (see * resource below).

		f) Created variables to hold the sizes of arrays and elements to avoid added expense for referencing the array length. This is debatable whether caching the value is faster than accessing the length property (see *** resource below).

		g) Manually capitalized the array values (the pizza nouns and adjectives) and removed the expensive string function calls (3 in total: charAt, toUpperCase, and slice) used to capitalize these values. 

		h) Resized the pizzeria.jpg image and lowered the quality level bring it to 34Kb down from 2.3Mb.

Resources

	http://www.html5rocks.com/en/tutorials/webperformance/usertiming/
	
	https://developers.google.com/fonts/docs/getting_started
	
	http://cssminifier.com/
	
	http://jscompress.com/
	
	https://www.google.com/analytics/web/
	
	http://andydavies.me/blog/2013/10/22/how-the-browser-pre-loader-makes-pages-load-faster/
	
	http://chimera.labs.oreilly.com/books/1230000000545
	
	https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp#performance-patterns
	
	https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path
	
	https://developers.google.com/web/fundamentals/layouts/rwd-fundamentals/use-media-queries
	
	https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer#minification-preprocessing--context-specific-optimizations
	
	https://developers.google.com/web/fundamentals/layouts/rwd-fundamentals/
	
	https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction
	
	https://developers.google.com/speed/pagespeed/insights/?url=http%3A%2F%2Fmyhighlandoaks.com&tab=desktop
	
	* http://jsperf.com/math-floor-vs-math-round-vs-parseint/55

	** https://thedotproduct.org/javascript-performance-document-getelementbyid-versus-document-queryselector-and-document-queryselectorall/

	*** http://jsperf.com/for-loop-caching
		
