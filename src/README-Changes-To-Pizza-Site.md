README-Changes-To-Pizza-Site

Note: I completed this project with advice taken from the Udacity Office Hours which may be viewed here: https://www.youtube.com/watch?v=iccaPsYn5qA 

The stock main.js file alongside other helpful advice can be found here: https://github.com/udacity/fend-office-hours/tree/master/Web%20Optimization/Effective%20Optimizations%20for%2060%20FPS

-----

How to inspect the site on a local server:

1) Open up terminal and change directory to the project repository you want to view. The "dist" folder holds the optimized and minified code while the "src" folder holds the optimized code (with comments) that hasn't been minified.

2) In the repository you're viewing, install ngrok. You can view additional instructions and the source for ngrok here: https://ngrok.com/download 

Once ngrok is installed you may view various ngrok commands by typing "ngrok help"

3) After installing ngrok, open up another terminal (you should have two terminal windows up) and change its current working directory to the repository in which you installed ngrok. In this newly opened terminal, enter command "python -m SimpleHTTPServer 8080"

4) In the other terminal, enter "./ngrok http 8080"

You should see some output in the terminal displaying "Tunnel Status" as "online" alongside other details such as "Version"and "Region."

You will see a couple links prefixed with http:// and https://

Copy and paste either of those links to your web browser to view the site.

-----

Steps taken to make the site perform at 60fps, changes made to views/main.js:

1) Open the html page in Chromium (or Chrome Canary) or normal up-to-date Google Chrome and inspect the site in dev tools. 

2) Record a timeline and scroll around the site to measure FPS. It helps to utilize dev tool's fps meter throughout the optimization process. I would check the scripting timeline and fps throughout optimization to see if any changes were beneficial to getting the site to run at 60fps.

3) Upon looking at the code, towards line 545, I noticed that 200 animated pizzas were being generated and updated. 200 pizzas aren't actually showing, so the for loop was changed to iterate up to 25 animated pizzas. 

4) In the updatePositions function, located around line 506, I took five values there were constantly being recalculated and moved them into an array (aka list). 

5) Replaced queryselctor methods with getClassName methods.

-----

Steps taken to make the site generate new pizza sizes within 5 ms:

1) Moved all pizzas to be changed into a variable outside of the for loop.

2) Moved variables dx and newwidth out of the for loop. Variable dx changes based on the 'size' parameter passed into the changePizzaSizes, so it doesn't need to be called on multiple times in the for loop. 

3) Variable newwidth's definition depends on the definition of dx, which is a variable that is defined outside of the for loop, so it is also moved outside of the for loop.

4) In the for loop, I replaced the document.querySelectorAll with the  changePizzaContainer variable. Instead of accessing the DOM over and over, we are accessing a local variable holding the same pizzas that are being manipulated.