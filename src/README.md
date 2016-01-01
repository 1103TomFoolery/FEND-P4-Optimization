## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository, inspect the code,

### Getting started

Some useful tips to help you get started:

1. Check out the repository
1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ngrok 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

Profile, optimize, measure... and then lather, rinse, and repeat. Good luck!

### Optimization Tips and Tricks
* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>

### Sample Portfolios

Feeling uninspired by the portfolio? Here's a list of cool portfolios I found after a few minutes of Googling.

* <a href="http://www.reddit.com/r/webdev/comments/280qkr/would_anybody_like_to_post_their_portfolio_site/">A great discussion about portfolios on reddit</a>
* <a href="http://ianlunn.co.uk/">http://ianlunn.co.uk/</a>
* <a href="http://www.adhamdannaway.com/portfolio">http://www.adhamdannaway.com/portfolio</a>
* <a href="http://www.timboelaars.nl/">http://www.timboelaars.nl/</a>
* <a href="http://futoryan.prosite.com/">http://futoryan.prosite.com/</a>
* <a href="http://playonpixels.prosite.com/21591/projects">http://playonpixels.prosite.com/21591/projects</a>
* <a href="http://colintrenter.prosite.com/">http://colintrenter.prosite.com/</a>
* <a href="http://calebmorris.prosite.com/">http://calebmorris.prosite.com/</a>
* <a href="http://www.cullywright.com/">http://www.cullywright.com/</a>
* <a href="http://yourjustlucky.com/">http://yourjustlucky.com/</a>
* <a href="http://nicoledominguez.com/portfolio/">http://nicoledominguez.com/portfolio/</a>
* <a href="http://www.roxannecook.com/">http://www.roxannecook.com/</a>
* <a href="http://www.84colors.com/portfolio.html">http://www.84colors.com/portfolio.html</a>


### Updates (Tom Allen)


In this project we were given a site to optimize with the following goals:

1)  Score above 90 for both Desktop and Mobile on Pagespeed Insights
2)  When scrolling pizza.html maintain 60 fps

Here are the optimizations I made.

To get the target page load speeds:

1)  Removed external link to Google Fonts and put the font definitions into style.css
2)  Added the media query to print.css
3)  Made the calls to the two js files async.
4)  Minified all html, css and js files
5)  Compressed images and pngs
6)  I used https://jonassebastianohlsson.com/criticalpathcssgenerator/ to identify "above the fold" css and implemented javascript borrowed with great appreciation from https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery to unblock rendering.

This resulted in PageSpeed Insight scores of Mobile 94 and Desktop 90.

I experimented with the javascript script runner Grunt to automate various repetitive optimization steps.  My script uses the following plugins:

1)  grunt-contrib-imagemin to minimize images (command line parameter = images)
2)  grunt-contrib-cssmin to minimize css files (command line parameter = css)
3)  grunt-contrib-htmlmin to minimize html files (command line parameter = htmL)
4)  grunt-contrib-uglify to minimize javascript files (command line parameter = js)

Each of the plugins can be run separately by entering the associated command line parameter.  For example; grunt js will run the uglify plugin.  
Alternatively, all four will run by default if you simply enter grunt on the command line.

All source files are under the src/ folder and the optimized files are saved in their respective dist/ folder.  There are two things to note.  First, minified css files are saved with the extension .min.css however index.html isn't smart enough to know to use them so I manually renamed them to .css.  More importantly, imagemin didn't optimize the images enough, even with optimization level set to 7, so I had to do an additional manual step using Shrink O'matic to compress the pisseria.jpg further.

To get the 60 fps performance I just watched the office hours video for that topic.  With those clues I optimized the updatePositions() function by moving the calculation for the relative position out of the for-loop and reduced the number of generated pizzas from 200 to 50.  After submitting for code review I made additional changes (thanks to Jose for stellar recommendations):

1)  Moved variable declarations out of the loops in main.js
	lines: 453, 454, 455, 456, 478, 538, and 539
2)  changed document.querySelectorAll to document.getElementsByClassName
    lines: 453 and 512
3)  changed document.querySelectorAll to document.getElementsByID
	line: 478
