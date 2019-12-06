# [presentation CSS shaders](https://MaxYashch.github.io/presentation-shaders/)
Hi everybody!
I am **Max Yashchikovskiy**. 
Let me introduce Y a short review of CCS instrument called Shaders.

CSS shaders were prepared by the W3C team. The development of this technology has been actively conducted since 2011.
CSS shaders are designed to expand the effects of filters and provide animated visual effects to all HTML content. They work especially well with CSS animations and CSS transitions. CSS shaders provide the flexibility and expressiveness needed to create custom effects: from the simplest to the most complex.
 
Before we talk about shaders, I need to mention a few words about CSS filters.
CSS filters are a powerful tool that web developers and designers can use for interesting visual effects. Filter effects appeared as part of the SVG specification. They were created to apply various effects based on bitmap images. Over time, browser makers have added support for SVG filters in their browsers.
Mozilla came up with the idea of using an SVG filter by applying CSS. It was a brilliant idea, prototypes showed how powerful CSS filters can be. 
Let’s look how CSS Filters Work
When the browser loads the web page, it must apply the styles connected to this page. Filters are copied to the screen before loading the page. At this time, the filters take a snapshot of the image on the loaded page as a bitmap, and then the result appears on top of the original image of the page.
If used correctly, they will not affect the download speed of your site!

`(Slide - example of setting filters)`  

Here is another SLIDE with example of working with filters.  

`(Slide - filters for mandrill)`

Further we can see available filter effects in CSS.
The value of the filters can be settled from 0 to 1 or in percentage. 

`(Slide - available filter effects)`

Now we can switch to CSS shaders
Shaders (usually) are small programs that are actively used in working with 3D graphics. They handle the vertices of 3D geometry and pixel colors.
Shaders operate with polygonal meshes. Polygonal meshes are a set of vertices, edges, and faces that determines the shape of a polyhedral object in three-dimensional computer graphics and solid modeling.
Shaders work directly on the hardware of the video card. They can process a large amount of data in parallel, which means that they can be very fast, but often redundant compared to the typical cycle of programs running on the processor. CSS shaders take advantages of hardware acceleration.
For example, vertex shaders can create a surface effect, or a change effect. Fragment shaders (also called pixel shaders) can take arbitrary calculations to determine the color of a pixel.

The shaders used in CSS are of two types: vertex shaders and fragment shaders.
Vertex shaders determine where and what is located. They allow you to move the vertices of the grid in 3D space, deforming and rearranging objects.
It would be better to explain with an example. Imagine a standard primitive shape, like a sphere. A vertex shader is provided to each of these vertices in turn and can manipulate them. It depends on the vertex shader what it actually does with each, but it has an obligation: it must at some point establish something called gl_Position, a 4D-floating-point vector, which is the end position of the vertex on the screen. This is a rather interesting process of getting a 3D position (vertices with x, y, z) projected onto a 2D screen.
Fragment shaders are responsible for how the surfaces of objects look. They allow you to draw on objects or change the belonging of existing pixels to the appearance of objects.
We can try to explain this by following. So, we have an object with certain vertices, and we projected them onto a 2D screen, but what about the colors we use? What about texturing and lighting? This is exactly what the fragment shader is for.
The fragment shader performs 1 main function: it must set or discard the variable called gl_FragColor, another 4D floating-point vector, which is the final color of our fragment. But what is a fragment? Think of the three vertices that make up the triangle. Each pixel in this triangle must be elongated. A fragment is data provided by these three vertices in order to draw each pixel in this triangle. Due to this, fragments get interpolated values from their component vertices. If one vertex is colored red and its neighbor is blue, we will see that the color values are interpolated from red to purple and blue.
In general, in order to be able to create a valid program for the GPU, you need both shaders. However, for custom CSS filters, only one of these types is needed, and for the missing browser, it uses the default pass-through shader.

Shaders accept three parameters as input
Vertex and fragment shaders can accept parameters of three types:
1. uniforms
2. attributes
3. differences
Uniforms are parameters with a single value for all vertices and pixels of the grid (for example, the color of an object). Embedded forms provide information about DOM element data common to the entire grid.
Attributes are individual parameters of the vertices, each mesh vertex gets its own value for each attribute (for example, the vertex position). Built-in attributes allow you to identify and find individual vertices and triangles in the grid.
Differences are parameters passed by vertices to fragments. They are indicated for each vertex of the triangle and their values for points inside the triangle are interpolated by the GPU (for example, lighting). Built-in differences provide texture coordinates in case the effect uses default shaders.

Let’s look at Shader’s working algorithm
  
`(Slide - example of setting shader)` 

 Another SLIDE shows us the CSS Shaders algorithm 

 `(Slide - CSS Shaders algorith)`  

 (step 1) a polygonal mesh overlays on any HTML or SVG element, with which the vertex shader works. 
(step 2)The object can be transformed in three-dimensional space. 
(step 3) After transformation rendering is performed, that is, translation into raster graphics.

CSS Shaders developers have borrowed a lot from the specifications of SVG filters (Filter Effects 1.0). The main difference is that they added a custom () function for the filter element, through which you can specify arbitrary effects properties. It would seem that a trifle allows you to create effects of a fundamentally higher level.

Why using CSS filters alone is not enough
The answer is very simple. Due to the limited functionality.
The beauty of Filter Effects lies in its simple syntax and integration with CSS. But the capabilities of these filters are very limited, only nine predefined effects for filter are registered in the specifications:
1. blur (5, 5)
2. drop-shadow (10, 5, 5)
3.hue-rotate (328deg)
4. saturate (5)
5. invert (1)
6. grayscale (1)
7.opacity (0.5)
8.gamma (1.1, 3.6, 0)
9.sepia (0.5)

The result of applying filters with such parameters is shown in the next illustration.

`(Slide - css-filters-only)`

And that’s all, there are no other filters there. CSS shaders are a completely different matter. Thanks to custom () function, you can impose additional effects. For example, the conversion of a picture from black and white to color is complemented by a slight tilt of the picture and the “wave” effect, when the color gradually fills the picture from the bottom up.

Here we can see how shader’s effect works.

`(Slide - shader’s effect)`  
Thank you.

