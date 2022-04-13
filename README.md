# Style_blending
In 2015, there was a paper named ["A Neural Algorithm of Artistic Style"](https://arxiv.org/pdf/1508.06576.pdf) trying to transfer the style of Van Gogh's painting to any of the given pictures. It seemed an interesting thing and it attracted me to explore this project. Later in 2018, on my Statistical Learning classes, our team tried to demo and repeat this project. By doing so, I got an A++ in this course. 4 years later, today, I would love to rewrite explaination about this project and try to provide a more clear pipeline of codes. I hope I could demo the project as brief and clear as possible. 

### Introduction for VGG-19
VGG is a convolutional neural network that has a depth of 19 layers. It was build and trained by K. Simonyan and A. Zisserman at the University of Oxford in 2014. The VGG-19 network is trained using more than 1 million images from the ImageNet database. It was trained on 224x224 pixels colored images. Naturally, you can import the model with the ImageNet trained weights. This pre-trained network can classify up to 1000 objects. The structure is as follows.
![Drag Racing](/images/vgg19.jpeg)</br>
However, VGG-19 is not the most "efficient" choice regarding computational cost and accuracy, see the following comparison. Therefore, I will use GoogLeNet or ResNet to do this project. But, the original paper and my original projects in Statisical Learning course used the VGG-19.
![Drag Racing](/images/Net_comparison.jpg)</br>


### Method of style transfering
The method is more like transfer learning, as we need to make use of pre-trained weights from VGG-19 and do optimization on the ouput by pushing it to learn content from image <img src="https://latex.codecogs.com/svg.image?C"/>  and learn style from image <img src="https://latex.codecogs.com/svg.image?S"/> . The initialization of the output image <img src="https://latex.codecogs.com/svg.image?X"/>  is from a white noise picture, and the loss function <img src="https://latex.codecogs.com/svg.image?f(X)"/>  has two parts combined. The first part is to regularize the content fidelity and the second part is to regularize the style blending.


<img src="https://latex.codecogs.com/svg.image?L_{C,S}(X)=\alpha&space;L_{content}(C,X)&plus;\beta&space;L_{style}(S,X)"/>.
Here, the first term can be further write as follows
<img src="https://latex.codecogs.com/svg.image?L_{C,S}(X)=\alpha&space;L_{content}(C,X)&plus;\beta&space;L_{style}(S,X)"/>.


<img src=" https://latex.codecogs.com/svg.image?L_{style}(S,X)=\frac{1}{2}\sum_{l=1}^K&space;w_l&space;\sum_{(i,j)\in&space;I_l}(F_{i,j}^l-P_{i,j}^l)^2 "/>


