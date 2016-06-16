README-Changes-To-Pizza-Site

Note: I completed this project with advice taken from the Udacity Office Hours which may be viewed here: https://www.youtube.com/watch?v=iccaPsYn5qA 

The stock main.js file alongside other helpful advice can be found here: https://github.com/udacity/fend-office-hours/tree/master/Web%20Optimization/Effective%20Optimizations%20for%2060%20FPS

-----

Steps taken to make the site perform at 60fps, changes made to views/main.js:

1) Open the html page in Chromium (or Chrome Canary) or normal up-to-date Google Chrome and inspect the site in dev tools. 

2) Record a timeline and scroll around the site to measure FPS. It helps to utilize dev tool's fps meter throughout the optimization process. I would check the scripting timeline and fps throughout optimization to see if any changes were beneficial to getting the site to run at 60fps.

3) Upon looking at the code, towards line 545, I noticed that 200 animated pizzas were being generated and updated. 200 pizzas aren't actually showing, so the for loop was changed to iterate up to 25 animated pizzas. 

4) In the updatePositions function, located around line 506, I took five values there were constantly being recalculated and moved them into an array (aka list). 

5) Replaced queryselctor methods with getClassName methods.

Steps taken to make the site generate new pizza sizes within 5 ms:

1) Moved all pizzas to be changed into a variable outside of the for loop.

2) Moved variables dx and newwidth out of the for loop. Variable dx changes based on the 'size' parameter passed into the changePizzaSizes, so it doesn't need to be called on multiple times in the for loop. 

3) Variable newwidth's definition depends on the definition of dx, which is a variable that is defined outside of the for loop, so it is also moved outside of the for loop.

4) In the for loop, I replaced the document.querySelectorAll with the  changePizzaContainer variable. Instead of accessing the DOM over and over, we are accessing a local variable holding the same pizzas that are being manipulated.