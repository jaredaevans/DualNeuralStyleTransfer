# Neural Style Transfer

## Single style

Interested in understanding neural style transfer, I set out to create one.  This is adapted from the tf implementation.  It is pretty awesome.  I definitely want to experiment with it some more, but here are results.  Obviously, I am going to use a photo of my beautiful dog, Bacchus.

<p align="center"><img src="ParentImages/Bacchus.jpg" alt="Bacchus" width="400"/></p>

The results are pretty great...

<img src="Images/Bacchus_Metz.jpg" alt="Metzinger's Two Nudes" width="230"/><img src="Images/Bacchus_Paris.jpg" alt="Gleizes's Bridges of Paris" width="230"/><img src="Images/Bacchus_Window.jpg" alt="Delaunay's Window on the City" width="230"/>  
<img src="Images/Bacchus_Comp.jpg" alt="Kandinsky's Composition VII" width="230"/><img src="Images/Bacchus_Monet.jpg" alt="Monet's The Water-Lily Pond" width="230"/><img src="Images/Bacchus_Babel.jpg" alt="Bruegel's Tower of Babel" width="230"/>  
<img src="Images/Bacchus_Limbo.jpg" alt="Bosch Follower's Christ in Limbo" width="230"/><img src="Images/Bacchus_Tondal.jpg" alt="Bosch's Tondal's Vision" width="230"/><img src="Images/Bacchus_Triumph.jpg" alt="Bruegel's Triumph of Death" width="230"/>  


## What is Neural Style Transfer

The baisc idea behind neural style transfer is to take an image, and transfer the artistic style of an artist onto it.  This can be done by the following basic process:  
1) Take a CNN trained for multi-purpose image examination (such as VGG19, used here)  
2) Extracting features from some of the layers of the network for both a "content" image and "style" image  
3) Creating a new image, "combo," that minimizes the loss from the content's deviation from "content" and the loss from the style's deviation from "style"  

In a paper by Gatys et al (https://arxiv.org/pdf/1508.06576.pdf), the authors construct this method by using two loss functions:  
1) Content loss:  The "pixel" distance between the "combo" and "content" on a deep layer of the network.   
2) Style loss:  The difference in the Gram matrix of the "combo" and "style" across several layers throughout the network.  In essence the Gram matrix takes a pixel image h x w x n_f, where h and w are the height and width of the image, and converts it into a n_f x n_f matrix that is a measure of how many and by how much each of the layer's features have been represented in that image.  The difference between the gram matrix then tracks how much these features matter.  Importantly, this doesn't care so much *where* the features are located, only that they are there.  This is pulled over multiple layers of the CNN.   


## What is different about my implementation?

1) Adam optimizer: Many implementations use L-BFGS-B to minimize the loss.  This is included in scipy as a wrapper to a FORTRAN function or something.  Here, I use Adam because it is easier to implement and seems to function just fine.  
2) Variational loss:  This demands adjancent pixels in the combo image do not move too much, i.e. the image is somewhat smooth.  
3) High tunability:  The three different sources of loss are weighted by scalable parameters and raised to variable powers allowing for an arbiratry customization of transfer.  Up until now, I have been mostly following in the footsteps of others, but here I start to deviate.   
4) Common weighting:  I normalize the style losses so that the style image has the same contribution from all included layers.  This means that the feautres that are present are rewarded, but more significantly the features that do appear in the combo image that are absent in the style are punished.  The effect of this is sizable, and I found that it tends to create a more interesting combined image.    
5) Removing content loss:  Interestingly, I found starting with the content image, but not having any contribution to the content loss results in the most interesting images.   
6) Option to start with "combo" = "content" or "combo" = noise: code allows for either option, which was heavily used in the Exploration/ folder  

# Dual style transfer

Instead of transfering one style, we could try to transfer two: a fine style, which captures colors and textures from the early layers, and a coarse style, which captures more global stylistic features from the image.  This is implemented in the file DualNST.ipynb.  

<img src="ParentImages/Bacchus.jpg" alt="Bacchus!" width="200"/><img src="ParentImages/Kandinsky_Composition_7.jpg" alt="Composition VII" width="200"  height="150"/><img src="ParentImages/Tondals_Vision.jpg" alt="Tondal's Vision" width="200"  height="150"/><img src="ParentImages/Gleizes_The_Bridges_of_Paris.jpg" alt="The Bridges of Paris" width="200"  height="150"/>  
<img src="ParentImages/Babel_Bruegel.jpg" alt="Tower of Babel" width="200"  height="150"/><img src="DualImages/Bacchus_Babel_Comp.jpg" alt="Fine: Tower of Babel; Coarse: Composition VII" width="200"/><img src="DualImages/Bacchus_Babel_Tondal.jpg" alt="Fine: Tower of Babel; Coarse: Tondal's Vision" width="200"/><img src="DualImages/Bacchus_Babel_Paris.jpg" alt="Fine: Tower of Babel; Coarse: Bridges of Paris" width="200"/>  
<img src="ParentImages/Water_Lily_Pond_Monet.jpg" alt="The Water-lily Pond" width="200"  height="150"/><img src="DualImages/Bacchus_Monet_Comp.jpg" alt="Fine: The Water-lily Pond; Coarse: Composition VII" width="200"/><img src="DualImages/Bacchus_Monet_Tondal.jpg" alt="Fine: The Water-lily Pond; Coarse: Tondal's Vision" width="200"/><img src="DualImages/Bacchus_Monet_Paris.jpg" alt="Fine: The Water-lily Pond; Coarse: Bridges of Paris" width="200"/>  
<img src="ParentImages/The_Triumph_of_Death_Bruegel.jpg" alt="The Triumph of Death" width="200"  height="150"/><img src="DualImages/Bacchus_Triumph_Comp.jpg" alt="Fine: Triumph of Death; Coarse: Composition VII" width="200"/><img src="DualImages/Bacchus_Triumph_Tondal.jpg" alt="Fine: Triumph of Death; Coarse: Tondal's Vision" width="200"/><img src="DualImages/Bacchus_Triumph_Paris.jpg" alt="Fine: Triumph of Death; Coarse: Bridges of Paris" width="200"/>  
