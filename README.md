# canvas-presentation-transcript

## Introduction

Hello everybody.

Today we will talk about Canvas HTML, a technology that allows you to create interactive and dynamic elements on web pages.

Canvas HTML is a powerful tool that can significantly improve the user experience and make websites more attractive and functional. It opens up wide opportunities for creating graphics, animations and interactive elements that were previously only available in applications.

In this presentation, we will look at the basic concepts of Canvas HTML as well as examples of use. We will also look at some frameworks and libraries that make the work much more convenient.

Let's get started!

## Canvas Basics

We can create a simple canvas element by placing the following tag on the page:

```
<canvas id="myCanvas" width="300" height="300"></canvas>
```

Before using canvas, we need to get its drawing context, for this we use the following script

```
const canvas = document.getElementById("myCanvas");
let ctx = canvas.getContext("2d");
```

First we get our canvas element from the page, then we get its drawing context. 
In this case, we will get a 2D Canvas Rendering Context, this interface provides the 2D rendering context for the drawing surface of a <canvas> element. It is used for drawing shapes, text, images, and other objects. Let's look at the main features of this interface:

### Draw a Line

After getting the context, we can start using its methods from the property, let's start with a simple one - from the line.

```
const canvas = document.getElementById("myCanvas");
let ctx = canvas.getContext("2d");
ctx.moveTo(0, 0);
ctx.lineTo(250, 200);
ctx.stroke();
```

1. First, we use the `moveTo(x,y)` method to indicate the place where our line will start
2. Then we use the `lineTo(x,y)` method to connect the start point to the end point with a continuous line
3. Method `stroke()` strokes the current line with the current stroke style.

Congratulations! We drew our first line using canvas.

![image](https://github.com/mogitrash/canvas-presentation-transcript/assets/140188066/34228c9c-071f-4642-bba7-8a8435d68ff8)

### Draw a Circle

```
const canvas = document.getElementById("myCanvas");
let ctx = canvas.getContext("2d");
ctx.arc(95, 50, 40, 0, 2 * Math.PI);
ctx.stroke();
```

To draw a circle, we will use the method  `arc(x, y, radius, startAngle, endAngle) `

Also, by changing the startAngle and endAngle parameters, we can draw arcs of any kind

![image](https://github.com/mogitrash/canvas-presentation-transcript/assets/140188066/a46f7a83-b16e-42b6-a438-f650c99db90a)

### Draw/Stroke a Text

```
const canvas = document.getElementById("myCanvas");
let ctx = canvas.getContext("2d");
ctx.font = "30px Arial";
ctx.fillText("Hello World", 10, 50);
```

1. Font property specifies the current text style
2. Method `fillText(text, x, y)` draws a text string at the specified coordinates
   
![image](https://github.com/mogitrash/canvas-presentation-transcript/assets/140188066/435d7928-4f2e-4ae1-bef4-1eb7e915f3fb)

We can also use the `strokeText(text, x, y)` to outline the text.

![image](https://github.com/mogitrash/canvas-presentation-transcript/assets/140188066/5228b261-4fe6-4c4c-8e88-c234c439b9e4)

### Draw/Stroke a Rectangle

```
const canvas = document.getElementById("myCanvas");
let ctx = canvas.getContext("2d");
ctx.strokeRect(10,10, 150,100);
```

`strokeRect(x, y, width, height)` method draws a rectangle that is oultined according to current `strokeStyle`. We can change stroke color by changing `strokeStyle` propety

```
ctx.strokeStyle = "pink";
```

![image](https://github.com/mogitrash/canvas-presentation-transcript/assets/140188066/23deae9f-098d-4f39-8102-46bd3d423f4b)

there is also a `fillRect(x, y, width, height)` method that fills a rectangle with color according to current `fillStyle`

```
const canvas = document.getElementById("myCanvas");
let ctx = canvas.getContext("2d");
ctx.fillStyle = "pink";
ctx.fillRect(10, 10, 150, 100);
```

![image](https://github.com/mogitrash/canvas-presentation-transcript/assets/140188066/0af9a662-2d38-4d81-873e-e31f61b51eef)

## Basic animations

Since we're using JavaScript to control `<canvas>` elements, it's also very easy to make animations. In this chapter we will take a look at how to do some basic animations.

### Basic animations steps

1. **Clear the canvas.** Since each individual frame will occupy the entire surface of the canvas, we need to clean up before drawing a new frame of our animation. The easiest way to do this is using the `clearRect()` method.
2. **Save the canvas state.**
   - When you call the `save()` method on the canvas context, it saves the current state of the canvas, including all settings like styles, transformations, and other attributes.
   - Saving the canvas state is essential when you want to make temporary changes for a specific drawing operation and then revert to the original state.
3. **Draw animated shapes.** The step where you do the actual frame rendering.
4. **Restore the canvas state.**
   - After you have made changes to the canvas and want to revert to the saved state, you use the `restore()` method on the canvas context.
   - Restoring the canvas state allows you to go back to the original settings, transformations, and styles before any modifications were made.

### Controlling an animation

There are 3 main ways to **schedule update** of canvas: 
   1. `setInterval()`

      Starts repeatedly executing the `function` specified by function every `delay` milliseconds.

   2. `setTimeout()`
      
      Executes the function specified by function in delay milliseconds.
      
   3. `requestAnimationFrame(callback)`

      Tells the browser that you wish to perform an animation and requests that the browser call a specified function to update an animation before the next repaint.

Despite the first two methods, `requestAnimationFrame(callback)` copes with its task best, because it provides a smoother and more efficient way for animating by calling the animation frame when the system is ready to paint the frame. The number of callbacks is usually 60 times per second and may be reduced to a lower rate when running in background tabs.

Example of simple animation: 

```
const canvas = document.getElementById("myCanvas");
let ctx = canvas.getContext("2d");
ctx.fillStyle = "red";

let x = 0;
let y = 0;

window.requestAnimationFrame(anim);

function anim() {
  ctx.clearRect(0, 0, 300, 300);

  ctx.fillRect(x, y, 100, 100);

  x++;
  y++;

  if (x <= 200 && y <= 200) {
    window.requestAnimationFrame(anim);
  }
}
```

And here is the result of our code:

![CPT2404262208-300x300](https://github.com/mogitrash/canvas-presentation-transcript/assets/140188066/6d7703f1-3710-4c4a-b5c5-ba6b92a64ad0)      

But, our animation is not the top of canvases abilities. I found a couple of mesmerizing animations made with canvas:

1. This animation of the Earth and the Sun made by MDN
   
   ![CPT2404272141-333x331](https://github.com/mogitrash/canvas-presentation-transcript/assets/140188066/460bbad5-5187-4c0f-80ee-2baef212b316)

2. Next up is this beautiful interactive and fully customizable animation
 
 ![Animation3dsfsdf](https://github.com/mogitrash/canvas-presentation-transcript/assets/140188066/dce5f702-9469-4ec3-94ca-8f6c498f124e)

3. A Tearable Cloth animation that simulates the physics of the cloth and interacts with the user
  
   ![sdfsd](https://github.com/mogitrash/canvas-presentation-transcript/assets/140188066/9b59496d-8e9d-41f2-963e-61cd8baca532)

The above animations are only a small part of what canvas is capable of!

### Frameworks


