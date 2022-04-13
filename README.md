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
Here, the first and second term can be further write respectively as follows

<img src="https://latex.codecogs.com/svg.image?L_{content}(C,X)&space;=&space;\frac{1}{2}\sum_lu_l\|F_C^l-P_X^l\|_F^2"/>. </br>

<img src="https://latex.codecogs.com/svg.image?L_{style}(S,X)&space;=&space;\frac{1}{2}\sum_lw_l\|A_S^l-Q_X^l\|_F^2"/>. </br>

Here, the matrices <img src="https://latex.codecogs.com/svg.image?F_C^l,&space;P_X^l"/> represent the extracted features on layer <img src="https://latex.codecogs.com/svg.image?l"/> of content image and target image respectively (row-based). And, matrices <img src="https://latex.codecogs.com/svg.image?A_S^l,Q_X^l"/> are the (normalized) Gram matrices of feature correlations regarding style image and target image respectively. See eg, <img src="https://latex.codecogs.com/svg.image?A_S^l&space;=&space;\frac{1}{N_l^2M_l^2}\sum_k&space;F_S^l(i,k)F_S(j,k)^l"/>. The content loss and the style loss stand for the idea of matching the content of C and X, matching the style of S and X. Content loss stands for content fidelity is direct, while one may find more infor of why this style loss stands for style fidelity in [Texture Synthesis Using CNN](https://arxiv.org/pdf/1505.07376.pdf), and [Perceptural Losses for Real-Time Style Transfer and Super-Resolution](https://arxiv.org/pdf/1603.08155.pdf).


### Implementation 
