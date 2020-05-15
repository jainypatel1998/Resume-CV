
# KDTraining Fashion - MNIST dataset with ResNET50

In this project, We sought to create a lightweight, but still accurate model for a classification problem. We trained a model on the pre-standardized Fashion-MNIST dataset. We aimed to create a classification model that could categorize the outfits into different pieces of clothing. We tested different model parameters in hopes to create the most efficient but still accurate model, to ensure we didn�t reach diminishing returns, in reference to time and resources spent in training.

The purpose of replacing the original MNIST dataset is because it�s commonly used to train models detecting handwritten digits. In our case, we are using images of different parts of clothing and classifying them as 10 different labels. We chose the Fashion-MNIST dataset over the MNIST dataset due to the increased complexity of each dataset. 

We also needed to find the point of diminishing returns, to ensure we were able to reach the highest point of accuracy, while maintaining proper training times, and resource usage. To ensure this, we used a dataset with about 60,000 training images as well as 10,000 testing images.


## Getting Started

Start the project by installing TensorFlow GPU version 2.0. This part is very crucial for the project since the dataset used is very large and therefore won�t work on a standard CPU. For our convenience, we used Google Colab as the platform to perform training and testing on the given dataset. Ensure the runtime you�re running has GPU acceleration enabled.

### Imports

Tensorflow is widely used to design our model. To be specific, we used the ResNET model provided by TensorFlow via Keras. Karas is the high-level API used to build and train models in deep learning.�

Along with that, many other libraries have also been used for minor purposes such as time, numpy and matplot. Each of these play a special role to make the user understand their model better. Numpy helped us keep track of the number of epochs, loss, accuracy and as well as time spent to run each epoch. Matplot makes it easier to include diagrams in your model. It helped print data visually in a graph to show changes in model accuracy throughout the total number of epochs. 


### MaxPooling

To simplify the input, we start by max pooling the dataset. However, to make the process of max pooling easier, we start by applying batch normalization to the input first. The purpose of doing this is because it helps with speed, accuracy and efficiency of the database.�

After that, we proceed with applying max pooling operation to the output from the batch normalization. When added to a model, max pooling reduces the dimensionality of images by reducing the number of pixels in the output of the previous layer. For our purposes, our model downsizes the input to a 3 x 3 and uses a stride of two for max coverage of the image before it proceeds next to the bottleneck architecture. 


### Bottleneck Architecture

Bottleneck Architecture is used in deep learning to simplify computational considerations. In simple terms it is just a layer with less neurons than the layer above or below it. The purpose of having such layers encourages the network to compress representations to best fit the available space to get the accurate loss during training. Currently used by many high-end models such as GoogLeNet, this type of architecture helps simplify the structure of the input data as shown in the image below.�

A basic block is what is used for resNet 18 and resNet 34 because it is affordable using a simple GPU ram however when it comes to having as many as 50 neural network layers in between, using a basic block wastes much of the GPU ram to run expensive 3 x 3 convolutions.�The visual difference between a basic block and a bottleneck block is shown in figure 2. A simple bottleneck uses a 1 x 1 convolution to reduce the channels of the input before performing the expensive 3 x 3 convolutions. Once this has been done, it uses another 1 x 1 convolution to restore the dimensions back to the original shape. For our project, we have used sixteen residual blocks with different input dimensions taken from the output of the previous layer. To simplify the number of blocks used in one run, we divided all sixteen blocks into four stages with different numbers of blocks in every stage. Stage 1 contains three blocks, stage 2 contains four blocks, stage 3 contains six blocks and stage 4 contains three blocks.�

Throughout the bottleneck blocks, we also used ReLU activation at every point after the dimensions of the data were resized. Activation functions are a very crucial part of any neural network model. They help determine the output of the model itself by defining its accuracy and efficiency of the training model. ReLU is also shown to be very efficient as well as very simple to use in deep learning. The reason why we used ReLU for this specific model is mainly because ResNet was initially designed this way.� To simplify the flow of one residual block in ResNet, take a look at figure 3.�


### Average Pooling

Once all stages have been run, the final step is to apply average pooling on the output given from the stage 4. Average pooling is used to compute the average for each patch of the feature map. Since at this point we have completed computing all residual blocks therefore to get accurate results we choose to use average pooling over max pooling. In simple terms, the difference between max pooling and average pooling is mainly the fact that max pooling will extract the most important features of an image like edges whereas average pooling takes everything into account and returns an average value which is beneficial for us since now we read though all of our input images.��


## Running the Tests

To test and train the model, run the ipynb model file on google colab. Use a GPU enabled runtime for decreased training and testing time. Initialize the dataset by importing it from the tensorflow dataset library. Edit the batch size and epoch count in the block titled �model parameters.� Epoch count greatly affects the training time, and accuracy, therefore it is important to find a balance between an epoch high enough to maintain proper accuracy, but low enough to maintain proper training times. Train the model using the aforementioned parameters, and test it after training is concluded. After testing is concluded, charts are generated depicting training and testing accuracy.


## Results

As can be seen with figure 4 and 5, training stagnates after a certain point, exposing the diminishing returns we referenced earlier. After epoch 100, it�s nearly impossible to see any difference in testing accuracy improving, however, time to train and test still grows at a linear rate. The small improvements (less than 1 thousandth) are not worth the linear time and resource toll, showing that epoch training is no longer bottlenecked by the number of epochs being trained over, but rather the model itself or the loss being applied.


## Built With

 * [Fashion-MNIST]( https://research.zalando.com/welcome/mission/research-projects/fashion-mnist/) � Dataset used to train and test model
 * TensorFlow � Used to import dataset and to create model architecture
 * NumPy � Used to print training and testing accuracy
 * MatPlot � Used to display results as plots











    * For deletions, consider the routine `findMin()` that we did in
      class. How can you use it to cover the special cases of
      deletion?

    * Consider the theory behind range and NN-Queries **before** you
      attempt to implement them. How do we behave in the
      descending/greedy phase? How do we behave in the
      ascending/pruning phase? What about the edge cases? How do we
      behave?

    * You can choose to leave the implementation of
      `BoundedPriorityQueue` implementation for after you implement
      `kNearestNeighbors()` if you wish, but realize that proper
      $`k`$-NN functionality depends on proper BPQ functionality.

 * For the PR-QuadTree component:

    * There are three types of students in this class. Those who study
      the parameter `PRQuadTreeNode.k` **well**, those who don't, and
      others.

    * In the backtracking phase of the range and nearest neighbor
      queries in a PR-QuadTree, while you **should** only recurse to
      quadrants which **intersect** with the given range (or current
      *worst* range, for $`k`$-NN), you should **not** be prioritizing
      the quadrants by the area of intersection; instead, keep it
      simple and loop through only the **valid** quadrants in
      **Z-order**. Finding the area of intersection is a hard
      numerical problem which we will not solve in this project.

   * Speaking of intersection of a quadrant with a given range, check
     the `protected` method
     `PRQuadNode.doesQuadIntersectAnchorRange()`. It might be useful
     to you.
