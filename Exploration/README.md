# Exploration of Neural Style Transfer

Here I do a bit more of a deep dive into what the style really means.  There are many layers in VGG, so here I will take the layers individually, and match the style onto a "content image" of noise.  I will also match the single layer onto the content image of my dog.  I will consider two images, "Water Lillies (n>>1)" by Monet and "Tondal's Vision" by (a follower of) Hieronymus Bosch.

<p align="center"><img src="Images/Monet_Resize.png" alt="Water Lillies" width="300"/><img src="Images/Tondal_Resize.png" alt="Tondal's Vision" width="300"/></p>



'block1_conv1' <img src="Images/Monet_block1_conv1smoothed.png" alt="Monet11" width="200"/><img src="Images/Tondal_block1_conv1smoothed.png" alt="Tondal11" width="200"/><img src="Images/Tondal_Bacchus_block1_conv1smoothed.png" alt="Tondal+Bacchus11" width="200"/>  
'block1_conv2' <img src="Images/Monet_block1_conv2smoothed.png" alt="Monet12" width="200"/><img src="Images/Tondal_block1_conv2smoothed.png" alt="Tondal12" width="200"/><img src="Images/Tondal_Bacchus_block1_conv2smoothed.png" alt="Tondal+Bacchus12" width="200"/>  
'block2_conv1' <img src="Images/Monet_block2_conv1smoothed.png" alt="Monet21" width="200"/><img src="Images/Tondal_block2_conv1smoothed.png" alt="Tondal21" width="200"/><img src="Images/Tondal_Bacchus_block2_conv1smoothed.png" alt="Tondal+Bacchus21" width="200"/>  
'block2_conv2' <img src="Images/Monet_block2_conv2smoothed.png" alt="Monet22" width="200"/><img src="Images/Tondal_block2_conv2smoothed.png" alt="Tondal22" width="200"/><img src="Images/Tondal_Bacchus_block2_conv2smoothed.png" alt="Tondal+Bacchus22" width="200"/>  
'block3_conv1' <img src="Images/Monet_block3_conv1smoothed.png" alt="Monet31" width="200"/><img src="Images/Tondal_block3_conv1smoothed.png" alt="Tondal31" width="200"/><img src="Images/Tondal_Bacchus_block3_conv1smoothed.png" alt="Tondal+Bacchus31" width="200"/>  
'block3_conv2' <img src="Images/Monet_block3_conv2smoothed.png" alt="Monet32" width="200"/><img src="Images/Tondal_block3_conv2smoothed.png" alt="Tondal32" width="200"/><img src="Images/Tondal_Bacchus_block3_conv2smoothed.png" alt="Tondal+Bacchus32" width="200"/>  
'block3_conv3' <img src="Images/Monet_block3_conv3smoothed.png" alt="Monet33" width="200"/><img src="Images/Tondal_block3_conv3smoothed.png" alt="Tondal33" width="200"/><img src="Images/Tondal_Bacchus_block3_conv3smoothed.png" alt="Tondal+Bacchus33" width="200"/>  
'block3_conv4' <img src="Images/Monet_block3_conv4smoothed.png" alt="Monet34" width="200"/><img src="Images/Tondal_block3_conv4smoothed.png" alt="Tondal34" width="200"/><img src="Images/Tondal_Bacchus_block3_conv4smoothed.png" alt="Tondal+Bacchus34" width="200"/>  
'block4_conv1' <img src="Images/Monet_block4_conv1smoothed.png" alt="Monet41" width="200"/><img src="Images/Tondal_block4_conv1smoothed.png" alt="Tondal41" width="200"/><img src="Images/Tondal_Bacchus_block4_conv1smoothed.png" alt="Tondal+Bacchus41" width="200"/>  
'block4_conv2' <img src="Images/Monet_block4_conv2smoothed.png" alt="Monet42" width="200"/><img src="Images/Tondal_block4_conv2smoothed.png" alt="Tondal42" width="200"/><img src="Images/Tondal_Bacchus_block4_conv2smoothed.png" alt="Tondal+Bacchus42" width="200"/>  
'block4_conv3' <img src="Images/Monet_block4_conv3smoothed.png" alt="Monet43" width="200"/><img src="Images/Tondal_block4_conv3smoothed.png" alt="Tondal43" width="200"/><img src="Images/Tondal_Bacchus_block4_conv3smoothed.png" alt="Tondal+Bacchus43" width="200"/>  
'block4_conv4' <img src="Images/Monet_block4_conv4smoothed.png" alt="Monet44" width="200"/><img src="Images/Tondal_block4_conv4smoothed.png" alt="Tondal44" width="200"/><img src="Images/Tondal_Bacchus_block4_conv4smoothed.png" alt="Tondal+Bacchus44" width="200"/>  
'block5_conv1' <img src="Images/Monet_block5_conv1smoothed.png" alt="Monet51" width="200"/><img src="Images/Tondal_block5_conv1smoothed.png" alt="Tondal51" width="200"/><img src="Images/Tondal_Bacchus_block5_conv1smoothed.png" alt="Tondal+Bacchus51" width="200"/>  
'block5_conv2' <img src="Images/Monet_block5_conv2smoothed.png" alt="Monet52" width="200"/><img src="Images/Tondal_block5_conv2smoothed.png" alt="Tondal52" width="200"/><img src="Images/Tondal_Bacchus_block5_conv2smoothed.png" alt="Tondal+Bacchus52" width="200"/>  
'block5_conv3' <img src="Images/Monet_block5_conv3smoothed.png" alt="Monet53" width="200"/><img src="Images/Tondal_block5_conv3smoothed.png" alt="Tondal53" width="200"/><img src="Images/Tondal_Bacchus_block5_conv3smoothed.png" alt="Tondal+Bacchus53" width="200"/>  
'block5_conv4' <img src="Images/Monet_block5_conv4smoothed.png" alt="Monet54" width="200"/><img src="Images/Tondal_block5_conv4smoothed.png" alt="Tondal54" width="200"/><img src="Images/Tondal_Bacchus_block5_conv4smoothed.png" alt="Tondal+Bacchus54" width="200"/>  




