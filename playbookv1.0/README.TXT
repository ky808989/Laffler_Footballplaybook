/* MYONLINEPLAYBOOK Playbook Editor v0.2 (2017/04/08 16:00)
 * Created by: Kuei Yuan (Peter) Chen, Andrew Hampson, Feng (York) Liu, Po-Ying (Zach) Yu
 * BCIT 3900 ACIT Set 4A (Spring 2017)
 * Based on design by Dr. Bethany Edmunds
 */
 
/* This initial release contains 2 prototypes that do essentially the same thing, written with different design 
 * ideals. Each prototype consists of one HTML file, one external JavaScript file, and a shared image folder that 
 * both depend on. 
 * The CreateJS Prototype uses the HTML5 canvas element with extended functionality to draw shapes on the playbook. 
 * It changes their position by redrawing them. RECOMMENDED.
 * The XML prototype uses pure JavaScript to create HTML elements, then manipulates their position.
 * NONE OF THE PROTOTYPES IMPLEMENT PREMIUM CONTENT OR LOGGING IN.
 */
 
 //     C R E A T E   J S

 // Description
 
/* The recommended prototype (CreateJSIndex.html and CreateJSScript.js) has extended functionality.
 * It requires an external library to function (http://code.createjs.com/easeljs-0.7.0.min.js)
 * The Crosses, Circles, Lines and Curves are all canvas drawings. The tools need to select the 
 * exact bounds of the drawing in order to select or delete them. It does not support saving at this time.
 */
 
 // Bugs

/* Curve tool is very inaccurate. The start point and end point are dozens of pixels off when the curve is
 * created. The cause of this bug is unknown, but may relate to the Placement Inaccuracy bug in the XML 
 * version below. (It seems to consider the first click the center of the circle, the second the radius
 * and a portion of the circle is deleted according to where the mouse is clicked. A bezier curve would be
 * better.
 *
 * Chrome Security. A recent patch to Chrome seems to be preventing the event handler from working.
 * It has something to do with restricting data in the canvas element. Whoops.
 */
 
 // Next Improvements

/* Save feature. It would need one function to read all elements in the canvas field, convert each one to a
 * xml element, then save to a database. Not sure how hard this would be, because integration is a concern.
 * 
 * Line preview. We were making headway in this, but ran out of time. The way we were going to implement it
 * was by using a dual canvas system. On the first click, create a canvas with one line in it. On each frame
 * (mousehover event), redraw the line between intial click and current position. On second click, delete
 * the second canvas, and on the first canvas create a line between the first click and second click. This
 * method would prevent redrawing all objects on the canvas every frame, while still offering UI output.
 * Placement bug might rear its head, though.
 * 
 * Color changing. When the color is changed, delete the initial line, then create a line in the new color
 * and redraw the canvas. Keep It Simple, Stupid.
 * 
 * Arc preview. You're on your own with this one. It might be similar to the line preview feature, but the
 * other, bezier points would be near uncontrollable. Sorry.
 */
 
 //    X M L 
 
 // Description
 
/* This prototype (TestXMLPage.html and XMLTestScript.js) uses pure, out-of-the-box JavaScript.
 * The Crosses and Circles are img elements with absolute positions and unique IDs. There are no 
 * Lines or Arcs, but they were planned on being SVG elements with absolute positions. The images have 
 * boxes around them that make selection easier. The move tool uses HTML5 drag functions. It also does
 * not support saving.
 */
  
 // Bugs
  
/* Placement Inaccuracy. When the screen is resized, the placement and movement of images becomes
 * inaccurate. The cause is as follows: when a mouseclick event is capture, it contains the x and y coords
 * related to the window. When an object is placed inside the editor, it uses the editor's local coordinate
 * system. The difference between these two causes the inaccuracy. In the regular program THIS IS ACCOUNTED
 * FOR BY THE fieldClick(e) FUNCTION, USING HARD-CODED NUMBERS. Potential solution? Make the playbook 
 * positions static (buttons, fields, etc.) so that a resizing pushes it off the screen. The original is
 * already unresponsive, so it's not a loss of functionality.
 */
 
 // Next Improvements

/* Line tool. Inside an svg element under the playContent div, create a line element with the position
 * value of 2 clicks. Only problem is how to get a function to respond to 2 different events and to get
 * it to respond to the other tools as well. The tools will likely need overhauls.
 * 
 * Arc tool. Same as above, just harder. An SVG path tag can make bezier curves natively.
 *
 * Saving. As all of the positions, placements and types of content are valid XML anyway, you can just rip 
 * the contents of the playContent and SVG elements and then store them. You can load a play, or a 
 * combination of plays just by adding the content back in. Simple.
 * 
 * Line previews. During line creation, change the value of the endpoint to the current mouse position 
 * (mousehover events)
 *
 * Arc preview. Again, same but harder. If you get the above working, this probably won't be too far behind
 *
 * Color changing. Because the crosses and circles are images, the only way to change their color is to make
 * multiple images in the different colors and change the img src. The svg elements can have their colors 
 * changed with attributes, so easy enough. You just need two tools to do one job.
 */
 