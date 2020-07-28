# Neural Style Transfer

## Single style

Interested in understanding neural style transfer, I set out to create one.  This is adapted from the tf implementation.  Obviously, I am going to use a photo of my beautiful dog, Bacchus.

<p align="center"><img src="ParentImages/Bacchus.jpg" alt="Bacchus" width="400"/></p>

The results are pretty great...

<img src="Images/Bacchus_Metz.jpg" alt="Metzinger's Two Nudes" width="230"/><img src="Images/Bacchus_Paris.jpg" alt="Gleizes's Bridges of Paris" width="230"/><img src="Images/Bacchus_Window.jpg" alt="Delaunay's Window on the City" width="230"/>  
<img src="Images/Bacchus_Comp.jpg" alt="Kandinsky's Composition VII" width="230"/><img src="Images/Bacchus_Monet.jpg" alt="Monet's The Water-Lily Pond" width="230"/><img src="Images/Bacchus_Babel.jpg" alt="Bruegel's Tower of Babel" width="230"/>  
<img src="Images/Bacchus_Triumph.jpg" alt="Bruegel's Triumph of Death" width="230"/>   <img src="Images/Bacchus_Limbo.jpg" alt="Bosch Follower's Christ in Limbo" width="230"/><img src="Images/Bacchus_Tondal.jpg" alt="Bosch's Tondal's Vision" width="230"/>
1) Metzinger's *Two Nudes*  
2) Gleizes's *The Bridges of Paris*
3) Delaunay's *Window on the City*  
4) Kandinsky's *Composition VII*
5) Monet's *The Water-Lily Pond*
6) Bruegel's *Tower of Babel*
7) Bruegel's *The Triumph of Death*
8) Bosch Follower's *Christ in Limbo*
9) Bosch Follower's *Tondal's Vision*


## What is Neural Style Transfer?

The basic idea behind neural style transfer is to take an image, and transfer the artistic style of an artist onto it.  This can be done by the following basic process:  
1) Take a CNN (convolutional neural network) trained for multi-purpose image examination (such as VGG19, used here)  
2) Extracting features from some of the layers of the network for both a "content" image and "style" image  
3) Creating a new image, "combo," that minimizes the loss from the content's deviation from "content" and the loss from the style's deviation from "style"  

In a paper by Gatys et al (https://arxiv.org/pdf/1508.06576.pdf), the authors construct this method by using two loss functions:  
1) Content loss:  The "pixel" distance between the "combo" and "content" on a deep layer of the network.   
2) Style loss:  The difference in the Gram matrix of the "combo" and "style" across several layers throughout the network.  In essence the Gram matrix takes a pixel image h x w x n_f, where h and w are the height and width of the image, and converts it into a n_f x n_f matrix that is a measure of how many and by how much each of the layer's features have been represented in that image.  The difference between the gram matrix then tracks how much these features matter.  Importantly, this doesn't care so much *where* the features are located, only that they are there.  This is pulled over multiple layers of the CNN.   


## What is different about my implementation?

1) Adam optimizer: Many implementations use L-BFGS-B to minimize the loss.  This is included in scipy as a wrapper to a FORTRAN function.  Here, I use Adam because it is easier to implement and seems to function just fine.  
2) Variational loss:  This demands adjancent pixels in the combo image do not move too much, i.e. the image is somewhat smooth.  
3) High tunability:  The three different sources of loss are weighted by scalable parameters and raised to variable powers, allowing for an arbiratry customization of transfer.  (Up until now, I have been mostly following in the footsteps of others, but here I start to deviate.)   
4) Common weighting:  I normalize the style losses so that the style image has the same contribution from all included layers.  This means that the features that are present are rewarded, but more significantly, the features that do appear in the combo image that are absent in the style are punished.  The effect of this is sizable, and I found that it tends to create a more interesting combined image.    
5) Removing content loss:  Interestingly, I found starting with the content image, but not having any contribution to the content loss results in the most interesting images (i.e., I typically set the content weight to 0).   
6) Option to start with "combo" = "content" or "combo" = noise: code allows for either option, which was heavily used in the Exploration/ folder.  For the noise, I simply construct an image from random uniformly distributed values for each pixel channel.  

# Dual style transfer

Instead of transfering one style, we could try to transfer two styles: a fine style, which captures colors and textures from the early layers, and a coarse style, which captures more global stylistic features from the image.  This is implemented in the file DualNST.ipynb.  Below, we have a grid of images.  The top left is the content source (Bacchus), while the rest of the top row are the coarse style source images (Composition VII, Tondal's Vision, The Bridges of Paris).  The left column has the fine style source (Tower of Babel, The Water-Lily Pond, The Triumph of Death).  The remaining images are the fine + coarse styles applied as indicated by the image position. 

<img src="ParentImages/Bacchus.jpg" alt="Bacchus!" width="200"/><img src="ParentImages/Kandinsky_Composition_7.jpg" alt="Composition VII" width="200"  height="150"/><img src="ParentImages/Tondals_Vision.jpg" alt="Tondal's Vision" width="200"  height="150"/><img src="ParentImages/Gleizes_The_Bridges_of_Paris.jpg" alt="The Bridges of Paris" width="200"  height="150"/>  
<img src="ParentImages/Babel_Bruegel.jpg" alt="Tower of Babel" width="200"  height="150"/><img src="DualImages/Bacchus_Babel_Comp.jpg" alt="Fine: Tower of Babel; Coarse: Composition VII" width="200"/><img src="DualImages/Bacchus_Babel_Tondal.jpg" alt="Fine: Tower of Babel; Coarse: Tondal's Vision" width="200"/><img src="DualImages/Bacchus_Babel_Paris.jpg" alt="Fine: Tower of Babel; Coarse: Bridges of Paris" width="200"/>  
<img src="ParentImages/Water_Lily_Pond_Monet.jpg" alt="The Water-lily Pond" width="200"  height="150"/><img src="DualImages/Bacchus_Monet_Comp.jpg" alt="Fine: The Water-lily Pond; Coarse: Composition VII" width="200"/><img src="DualImages/Bacchus_Monet_Tondal.jpg" alt="Fine: The Water-lily Pond; Coarse: Tondal's Vision" width="200"/><img src="DualImages/Bacchus_Monet_Paris.jpg" alt="Fine: The Water-lily Pond; Coarse: Bridges of Paris" width="200"/>  
<img src="ParentImages/The_Triumph_of_Death_Bruegel.jpg" alt="The Triumph of Death" width="200"  height="150"/><img src="DualImages/Bacchus_Triumph_Comp.jpg" alt="Fine: Triumph of Death; Coarse: Composition VII" width="200"/><img src="DualImages/Bacchus_Triumph_Tondal.jpg" alt="Fine: Triumph of Death; Coarse: Tondal's Vision" width="200"/><img src="DualImages/Bacchus_Triumph_Paris.jpg" alt="Fine: Triumph of Death; Coarse: Bridges of Paris" width="200"/>  

Note how the colors are textures are mostly preserved from the images on the left (fine style), while larger features (music symbols, creepy faces, sharp angles) are largely preserved from the top row.  All look very "Bacchus," even though the content (his image) is only the initial condition.  We could also use noise as the initial condition and apply fine and coarse features:  

<p align="center"><img src="DualImages/Monet_Comp.jpg" alt="Fine: The Water-lily Pond; Coarse: Composition VII" width="400"/></p>

# Triple Neural Style Transfer

As can be observed from the Exploration folder, there is a lot of difference between the 1st, 3rd, and 5th block of the network.  We could instead 
try to transfer three styles to the image - roughly as colors, small features, and large features (A, B, C respectively). This is in TriNST.ipynb. These style transfers are definitely rather tempermental - if the adjacent style is too discordant, there tend to be a lot of artifacts produced.  Turning up the smoothing (v_w) can help a lot, but it isn't always enough.    

<img src="TriImages/Bacchus_Paris_Window_Limbo.jpg" alt="Colors: Bridges of Paris; Fine: Window on the City; Coarse: Christ in Limbo" width="200"/>><img src="TriImages/Bacchus_Metz_Paris_Window.jpg" alt="Colors: Two Nudes; Fine: Bridges of Paris; Coarse: Window on the City" width="200"/><img src="TriImages/Bacchus_Turner_Limbo_Comp.jpg" alt="Colors: Wrecker's Coast of Northumberland; Fine: Christ in Limbo; Coarse: Composition VII" width="200"/><img src="TriImages/Bacchus_Limbo_Triumph_Comp.jpg" alt="Colors: Christ in Limbo; Fine: Triumph of Death; Coarse: Composition VII" width="200"/><img src="TriImages/Bacchus_Window_Triumph_Comp.jpg" alt="Colors: Window on the City; Fine: Triumph of Death; Coarse: Composition VII" width="200"/><img src="TriImages/Bacchus_Paris_Babel_Limbo.jpg" alt="Colors: Bridges of Paris; Fine: Tower of Babel; Coarse: Christ in Limbo" width="200"/><img src="TriImages/Bacchus_Triumph_Tondal_Limbo.jpg" alt="Colors: Triumph of Death; Fine: Tondal's Vision; Coarse: Christ in Limbo" width="200"/><img src="TriImages/Bacchus_Paris_Window_Metz.jpg" alt="Colors: Bridges of Paris; Fine: Window on the City; Coarse: Two Nudes" width="200"/  

In order, these are:  
1) Colors: Bridges of Paris; Fine: Window on the City; Coarse: Christ in Limbo  
2) Colors: Two Nudes; Fine: Bridges of Paris; Coarse: Window on the City  
3) Colors: Wrecker's Coast of Northumberland (J.M.W. Turner); Fine: Christ in Limbo; Coarse: Composition VII  
4) Colors: Christ in Limbo; Fine: Triumph of Death; Coarse: Composition VII  
5) Colors: Window on the City; Fine: Triumph of Death; Coarse: Composition VII  
6) Colors: Bridges of Paris; Fine: Tower of Babel; Coarse: Christ in Limbo  
7) Colors: Triumph of Death; Fine: Tondal's Vision; Coarse: Christ in Limbo  
8) Colors: Bridges of Paris; Fine: Window on the City; Coarse: Two Nudes  

## More control over dual transfer with triple transfer

In addition to making the transfer of three styles possible, there is an improvement on the dual transfer, for instance, having one image tranfer A & B, and the second transfer C, or one do A, and the other do B & C (where A = colors; B = small features; C = large features).   Below from left to right, we have Water-lily Pond + Composition VII using 1) the Dual method; 2) A & B - Water-lily, C - Composition; 3) A - Water-lily, B & C - Composition.  It is clear how much difference these middle layers can make.

<img src="DualImages/Bacchus_Monet_Comp.jpg" alt="Fine: The Water-lily Pond; Coarse: Composition VII" width="250"/><img src="TriImages/Bacchus_Monet_Monet_Comp.jpg" alt="Colors: The Water-lily Pond; Fine: The Water-lily Pond; Coarse: Composition VII" width="250"/><img src="TriImages/Bacchus_Monet_Comp_Comp.jpg" alt="Colors: The Water-lily Pond; Fine: Composition VII; Coarse: Composition VII" width="250"/>

## More control over single transfer with triple transfer

Similarly, we don't have to tranfer all levels.  By setting some weights to 0, we can just transfer some of the pieces.  Here we transfer only (left to right) 1) A & B; 2) A & C; 3) B & C from Albert Gleizes's Bridges of Paris.     

<img src="TriImages/Bacchus_Paris_Paris_0.jpg" alt="Colors: Bridges of Paris; Fine: Bridges of Paris; Coarse: None" width="250"/><img src="TriImages/Bacchus_Paris_0_Paris.jpg" alt="Colors: Bridges of Paris; Fine: None; Coarse: Bridges of Paris" width="250"/><img src="TriImages/Bacchus_0_Paris_Paris.jpg" alt="Colors: None; Fine: Bridges of Paris; Coarse: Bridges of Paris" width="250"/>  

## More subtle influence with triple transfer

We can also use the content image as a choice for style image in order to preserve more features.  For example here is Tower of Babel as content, with Monet's Blue Water Lillies applied in levels A & B, while C is again Tower of Babel Style:  

<p align="center"><img src="TriImages/Babel_Monet2_Monet2_Babel.jpg" alt="Colors: Blue Lillies; Fine: Blue Lillies; Coarse: Tower of Babel" width="400"/></p>

We can choose multiple ways to apply this, as an example we will show Tower of Babel as content, Bridges of Paris / Babel as style - in order 1) ABC - Babel (no Paris applied, only smoothing); 2) AB - Babel, C - Paris; 3) AC - Babel, B - Paris; 4) BC - Babel, A - Paris; 5) A - Babel, BC - Paris; 6) B - Babel, AC - Paris; 7) C - Babel, AB - Paris; 8) ABC - Paris  

<img src="TriImages/Babel_Babel_Babel_Babel.jpg" alt="Colors: Tower of Babel; Fine: Tower of Babel; Coarse: Tower of Babel" width="200"/><img src="TriImages/Babel_Babel_Babel_Paris.jpg" alt="Colors: Tower of Babel; Fine: Tower of Babel; Coarse: Bridges of Paris" width="200"/><img src="TriImages/Babel_Babel_Paris_Babel.jpg" alt="Colors: Tower of Babel; Fine: Bridges of Paris; Coarse: Tower of Babel" width="200"/><img src="TriImages/Babel_Paris_Babel_Babel.jpg" alt="Colors: Bridges of Paris; Fine: Tower of Babel; Coarse: Tower of Babel" width="200"/><img src="TriImages/Babel_Babel_Paris_Paris.jpg" alt="Colors: Tower of Babel; Fine: Bridges of Paris; Coarse: Bridges of Paris" width="200"/><img src="TriImages/Babel_Paris_Babel_Paris.jpg" alt="Colors: Bridges of Paris; Fine: Tower of Babel; Coarse: Bridges of Paris" width="200"/><img src="TriImages/Babel_Paris_Paris_Babel.jpg" alt="Colors: Bridges of Paris; Fine: Bridges of Paris; Coarse: Tower of Babel" width="200"/><img src="TriImages/Babel_Paris_Paris_Paris.jpg" alt="Colors: Bridges of Paris; Fine: Bridges of Paris; Coarse: Bridges of Paris" width="200"/>   

Notice how A is really governing the color scheme (1235 vs 4678); B is capturing small details, e.g., tower windows, foreground (1246 vs 3578); and C is getting the largest features, e.g., shape of the tower, surrounding hills (1347 vs 2568).

# Summary

Neural style transfer can be customized quite a bit.  The transfer of styles from different regions can result in very different images.  My interest in this was just to produce some fascinating visual art, and to better understand the layers in a convnet.
