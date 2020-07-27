# Neural Style Transfer

Interested in understanding style transfer, I set out to create one.  The first version is inline with the tf implementation (from which I adapted my code).  It is pretty awesome.  I definitely want to experiment with it some more, but here are results.  Obviously, I am going to use a photo of my beautiful dog, Bacchus.

<p align="center"><img src="ParentImages/Bacchus.jpg" alt="Bacchus" width="400"/></p>

The results are pretty great...

<img src="Images/Bacchus_Metzinger.jpg" alt="Metzinger's Two Nudes" width="230"/><img src="Images/Bacchus_Paris.jpg" alt="Gleizes's Bridges of Paris" width="230"/><img src="Images/Bacchus_Window.jpg" alt="Delaunay's Window on the City" width="230"/>
<img src="Images/Bacchus_Composition.jpg" alt="Kandinsky's Composition VII" width="230"/>
<img src="Images/Bacchus_Limbo.jpg" alt="Bosch Follower's Christ in Limbo" width="230"/><img src="Images/Bacchus_Tondal.jpg" alt="Bosch's Tondal's Vision" width="230"/><img src="Images/Bacchus_Triumph.jpg" alt="Bruegel's Triumph of Death" width="230"/><img src="Images/Bacchus_Babel.jpg" alt="Bruegel's Tower of Babel" width="230"/>

These examples are all very heavy on the style.  In my implementation this is a tunable parameter.  Effectively, there are three losses:  
1) Content loss:  pixel distance between the created image and the content source image on a layer of the network (I used VGG19) 
2) Style loss: difference in the Gram matrix of the style source and the created image - essentially it says the features from the layers overlap significantly in the two images.  This is pulled over multiple layers of the CNN.   
3) Variational loss: demands adjancent pixels in the combo image do not move too much, i.e. the image is somewhat smooth  

More to come...
