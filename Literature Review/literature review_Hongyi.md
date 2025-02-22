# 601A1 
## Multi-View Stereo(Building 3D scenes from 2D images using ML algorithms)
### What is Multi-View Stereo?
  Multi-view stereo (MVS) is a general term for a series of methods of multi-view 3D reconstruction which refers to the task of reconstructing a 3D shape from calibrated overlapping images captured from different viewpoints. In short, it uses multiple photos taken by one/multiple camera(s) to reconstruct the 3D scene in the photo.
![](/images/1.png)
<p align="center">
                                                                                    Figure1
  </p>
                                                                  
  For example, in the picture above, different images of the Buddha statue are taken in different orientations in advance. Different images contain different and overlapping information about the Buddha statues. The main goal of the MVS is to use an algorithm to maximize the use of overlapping information to map and different information to model the Buddha statue in 3D. 
### Why is MVS important?
  MVS is widely used range from 3D mapping and navigation to online shopping, 3D printing, computational photography, computer video games, or cultural heritage archival.
  
  ![](/images/AR.png) ![](/images/autonomous.png) ![](/images/robots.png)
<p align="center">
                                                                                    Figure2
  </p>
  
   In robotics, MVS can obtain the position and posture of an object through a single camera to assist the grasping of the robotic arm. In autonomous driving, the use of MVS can more accurately generate models of nearby objects to assist obstacle avoidance.
   
   In terms of remote sensing, mvs can effectively reconstruct metropolises and rural areas, processing millions of photos over hundreds of kilometers at a time. Apple Maps “Flyover” feature provides views of high quality texture mapped city building models. Google Maps “Earth View” also provides stunning 3D views of cities. These are the applications of MVS. They are widely used in our daily lives, but we rarely pay attention to them.  
   
   The demand for the 3d industry has increased significantly in recent years. As an indispensable part of 3d industry, mvs has also developed rapidly. Many emerging companies are gradually established, such as Acute3D and Pix4D, allowing users to build high quality and resolution 3D models. So in general, mvs has high practical value, and its future prospects are very promising.
   
### Literature review
  MVS originated from a natural improvement to the two-view case. Until today, two-view stereo algorithms have been a very active and fruitful research field. Instead of capturing two photographs from two different viewpoints, multi-view stereo would capture more viewpoints to increase robustness which significantly increase the difficulty. The current two major breakthroughs have gradually turned two-view into multi-view. The first is the improvement of digital cameras and computing power, which makes photos more accurate and allows algorithms to easily process tens of thousands of images. The second is the improvement of algorithms over the past few decades. With these two changes, MVS gradually entered the industry from the laboratory.
  
   After decades of development, the MVS algorithm has gradually matured, and the accuracy of 3D modeling has become higher and higher. According to the method, it can be divided into two categories. One is the hand-crafted traditional method, and the other is the modeling method based on deep learning after 2015.
  
#### hand-crafted method
  Before generalizing statistics-like method of mvs, it is worth mentioning the SFM(Structure for motion) algorithm. Its idea is very suitable for MVS and it is very valuable for reference. SFM refers to a series of algorithms for estimating three-dimensional structure from a sequence of moving two-dimensional images. Normally, SFM mainly focused on the geometry of two and three views. 
  
  ![](/images/sfm.png)
<p align="center">
                                                                                    Figure3
  </p>
  
 The SFM algorithm can be divided into the following steps: finding features, matching features, generating trajectories, and modeling trajectories. The SFM algorithm usually finds similar feature points in a pair of images, and uses the feature points as key points to fuse and reconstruct the 3D scene.
 Inspired by sfm, the mvs method can also be divided into two parts. First is the Photoconsistency method. And the second is the algorithms for 3d construction.
##### Photoconsistency
 Multi-view photo-consistency, similar to the matching features process in SFM, measures the agreement or consistency between a set of input images and all the components involved in its image formation (such as lighting and 3D geometric shapes). Photoconsistency lays the foundation for the next 3D reconstruction and determines the quality of the reconstruction. There are many photoconsistency algorithms for us to choose. Among them, the most popular are NCC and SAD. NCC is mainly used to match images with varying lighting conditions and generally good coverage. On the other hand, SAD  is used when the images are not expected to have bias or gain changes, and the coverage is low.
 
##### 3d construction
In this part, the algorithm makes use of the results from Photoconsistency to determine the key points. After years of development, many algorithms with excellent performance have emerged. In the Multiple-baseline stereo algorithm, the matching score w.r.t. all other images of each pixel in the reference image is calculated at the same time. In the Plane sweep stereo algorithm, for each depth, each input image is projected onto the plane(homography) and the generated image stacks are compared. In PMVS algorithm, key points are detected, matches are expanded to nearby locations iteratively, and erroneous matches are filtered out using visibility constraints. There are many algorithms for us to choose, mainly depending on their speed, accuracy, use environment and output model format.

Although traditional methods can achieve good results under many circumstances, low textured, specular and reflective regions of the scene make dense matching intractable and thus lead to incomplete reconstructions. Lack of texture，thin structures and non-Lambertian surfaces have become difficult to solve with hand-crafted similarity metrics and engineered regularizations methods. The MVS methods needs to be improved in these areas. 
#### Deep learning methed
##### MVSNet
  After 2010, cnn has achieved sota results in more and more image processing tasks. Many people began to consider whether CNN can be used in the mvs, but the final results obtained are not satisfactory. Until the proposal of MVSNet, the first to apply cost volume to the neural network, achieved very good experimental results. MVSNet can be regarded as the originator of neural networks in the field of MVS.
  
  ![](/images/MVSNet.png)
<p align="center">
                                                                                    Figure4
  </p>
  In the paper, the author proposed an end-to-end deep learning architecture for depth map inference(see Figure4). The network takes one reference image and several source images as input, and then use the convolutional network to obtain the feature maps respectively. The key insight is the differentiable homography warping operation, which implicitly encodes camera geometry in the network to build the 3D cost volumes from 2D image features maps. Then a variance-based metric was proposed that maps multiple features into one cost feature in the volume. Cost volume then undergoes multi-scale 3D convolutions and regress an initial depth map. Finally, the depth map is refined with the reference image to improve the accuracy of boundary areas.
  After the network was proposed, many researchers generally accepted this idea and proposed many improved versions were on MVSNET, such as R-MVSNet, Fast-MVSNet and Cas-MVSNet. 
  
![](/images/overall.png)
<p align="center">
                                                                                    Figure5
  </p>
  Figure5 is the performance comparison diagram of the existing neural network-based MVS algorithm. From this picture, we can find that the best method today is CVP-MVSNet based on neural networks, with a minimum distance error of 0.351 which is much smaller than the traditional method. It is worth noting that the unsupervised method proposed in 2021 has also achieved good results and has great potential in the future. he neural network method can well solve some of the shortcomings of traditional algorithms, improve the accuracy of MVS, and the process is relatively simple.
  
### Open Source Project
#### PMVS
  PMVS is probably the first successful open source MVS software, which has been extensively used by nonexperts such as artists and civil engineers. PMVS is a multi-view stereo software that takes a set of image and camera parameters, and then reconstructs 3D structure of the object or scenes visible in the images. This project started in 2007. With the emergence of new algorithms, this software is constantly updated, such as PMVS2, CMVS, etc., and it is now a relatively mature open source product.

#### MVE
  The Multi-View Environment MVE is an implementation of a complete end-to-end pipeline for image-based geometry reconstruction. It has the functions of SFM, MVS and Surface Reconstruction. MVE is written in C++ and comes with a set of efficient, cross-platform and easy-to-use libraries.
  
#### OpenMVG
  OpenMVG's mission is to extend awareness of the power of 3D reconstruction from images by developing a C++ framework. The library also includes the two complete SfM pipelines and provides customizable tools to help engineers to deal with MVS problems.

### Reference
##### Sinha S.N. (2014) Multiview Stereo. In: Ikeuchi K. (eds) Computer Vision. Springer, Boston, MA.
##### Yao Y, Luo Z, Li S, et al. Mvsnet: Depth inference for unstructured multi-view stereo[C]//Proceedings of the European Conference on Computer Vision (ECCV). 2018: 767-783.

##### Yasutaka Furukawa; Carlos Hernández, Multi-View Stereo: A Tutorial , now, 2015.
