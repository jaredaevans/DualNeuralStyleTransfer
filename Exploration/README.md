# Exploration of Neural Style Transfer

Here I do a bit more of a deep dive into what the style really means.  There are many layers in VGG, so here I will take the layers individually, and match the style onto a "content image" of noise.  I will also match the single layer onto the content image of my dog.  I will consider two images, "Water Lillies (n>>1)" by Monet and "Tondal's Vision" by (a follower of) Hieronymus Bosch.

<p align="center"><img src="Images/Monet_Resize.jpg" alt="Water Lillies" width="350"/><img src="Images/Tondal_Resize.jpg" alt="Tondal's Vision" width="350"/></p>



'block1_conv1' <img src="Images/Monet_block1_conv1smoothed.jpg" alt="Monet11" width="230"/><img src="Images/Tondal_block1_conv1smoothed.jpg" alt="Tondal11" width="230"/><img src="Images/Tondal_Bacchus_block1_conv1smoothed.jpg" alt="Tondal+Bacchus11" width="230"/>  
'block1_conv2' <img src="Images/Monet_block1_conv2smoothed.jpg" alt="Monet12" width="230"/><img src="Images/Tondal_block1_conv2smoothed.jpg" alt="Tondal12" width="230"/><img src="Images/Tondal_Bacchus_block1_conv2smoothed.jpg" alt="Tondal+Bacchus12" width="230"/>  
'block2_conv1' <img src="Images/Monet_block2_conv1smoothed.jpg" alt="Monet21" width="230"/><img src="Images/Tondal_block2_conv1smoothed.jpg" alt="Tondal21" width="230"/><img src="Images/Tondal_Bacchus_block2_conv1smoothed.jpg" alt="Tondal+Bacchus21" width="230"/>  
'block2_conv2' <img src="Images/Monet_block2_conv2smoothed.jpg" alt="Monet22" width="230"/><img src="Images/Tondal_block2_conv2smoothed.jpg" alt="Tondal22" width="230"/><img src="Images/Tondal_Bacchus_block2_conv2smoothed.jpg" alt="Tondal+Bacchus22" width="230"/>  
'block3_conv1' <img src="Images/Monet_block3_conv1smoothed.jpg" alt="Monet31" width="230"/><img src="Images/Tondal_block3_conv1smoothed.jpg" alt="Tondal31" width="230"/><img src="Images/Tondal_Bacchus_block3_conv1smoothed.jpg" alt="Tondal+Bacchus31" width="230"/>  
'block3_conv2' <img src="Images/Monet_block3_conv2smoothed.jpg" alt="Monet32" width="230"/><img src="Images/Tondal_block3_conv2smoothed.jpg" alt="Tondal32" width="230"/><img src="Images/Tondal_Bacchus_block3_conv2smoothed.jpg" alt="Tondal+Bacchus32" width="230"/>  
'block3_conv3' <img src="Images/Monet_block3_conv3smoothed.jpg" alt="Monet33" width="230"/><img src="Images/Tondal_block3_conv3smoothed.jpg" alt="Tondal33" width="230"/><img src="Images/Tondal_Bacchus_block3_conv3smoothed.jpg" alt="Tondal+Bacchus33" width="230"/>  
'block3_conv4' <img src="Images/Monet_block3_conv4smoothed.jpg" alt="Monet34" width="230"/><img src="Images/Tondal_block3_conv4smoothed.jpg" alt="Tondal34" width="230"/><img src="Images/Tondal_Bacchus_block3_conv4smoothed.jpg" alt="Tondal+Bacchus34" width="230"/>  
'block4_conv1' <img src="Images/Monet_block4_conv1smoothed.jpg" alt="Monet41" width="230"/><img src="Images/Tondal_block4_conv1smoothed.jpg" alt="Tondal41" width="230"/><img src="Images/Tondal_Bacchus_block4_conv1smoothed.jpg" alt="Tondal+Bacchus41" width="230"/>  
'block4_conv2' <img src="Images/Monet_block4_conv2smoothed.jpg" alt="Monet42" width="230"/><img src="Images/Tondal_block4_conv2smoothed.jpg" alt="Tondal42" width="230"/><img src="Images/Tondal_Bacchus_block4_conv2smoothed.jpg" alt="Tondal+Bacchus42" width="230"/>  
'block4_conv3' <img src="Images/Monet_block4_conv3smoothed.jpg" alt="Monet43" width="230"/><img src="Images/Tondal_block4_conv3smoothed.jpg" alt="Tondal43" width="230"/><img src="Images/Tondal_Bacchus_block4_conv3smoothed.jpg" alt="Tondal+Bacchus43" width="230"/>  
'block4_conv4' <img src="Images/Monet_block4_conv4smoothed.jpg" alt="Monet44" width="230"/><img src="Images/Tondal_block4_conv4smoothed.jpg" alt="Tondal44" width="230"/><img src="Images/Tondal_Bacchus_block4_conv4smoothed.jpg" alt="Tondal+Bacchus44" width="230"/>  
'block5_conv1' <img src="Images/Monet_block5_conv1smoothed.jpg" alt="Monet51" width="230"/><img src="Images/Tondal_block5_conv1smoothed.jpg" alt="Tondal51" width="230"/><img src="Images/Tondal_Bacchus_block5_conv1smoothed.jpg" alt="Tondal+Bacchus51" width="230"/>  
'block5_conv2' <img src="Images/Monet_block5_conv2smoothed.jpg" alt="Monet52" width="230"/><img src="Images/Tondal_block5_conv2smoothed.jpg" alt="Tondal52" width="230"/><img src="Images/Tondal_Bacchus_block5_conv2smoothed.jpg" alt="Tondal+Bacchus52" width="230"/>  
'block5_conv3' <img src="Images/Monet_block5_conv3smoothed.jpg" alt="Monet53" width="230"/><img src="Images/Tondal_block5_conv3smoothed.jpg" alt="Tondal53" width="230"/><img src="Images/Tondal_Bacchus_block5_conv3smoothed.jpg" alt="Tondal+Bacchus53" width="230"/>  

Several features are pretty clear here:  
1) 'block1_conv1': really seems to only have color information  
2) 'block1_conv2': seems to have color and very local texture information information  
3) 'block2_conv1': catches little lines, which may be important in combining with other layers, but doesn't do much here  
4) 'block2_conv2': catches a bit longer lines, does more than above. but not much overall  
5) 'block3_conv1' & 'block3_conv2': now we can really see structure emerging  
6) 'block3_conv3' & 'block3_conv4' & 'block4_conv1': there is definite structure that gets larger with each layer, but aspects of the parent image not aligned with the features are beginning to fade into the background  
7) 'block4_conv2' & 'block4_conv3': the structure that emerges is no longer local (also this layer does creepy things to my dog's face)  
8) 'block4_conv4' and up: global structures, many weird features: in Monet the bridge emerges, in Tondal there are faces everywhere, there is almost no influence from the style image colors (both Tondal and Monet have the same color scheme, Bacchus is the same color as before)  


