# What's this
Implementation of Highway Networks by chainer


# Dependencies

    git clone https://github.com/nutszebra/highway_networks.git
    cd highway_networks
    git submodule init
    git submodule update

# How to run
    python main.py -p ./ -g 0 

# Details about my implementation
* Data augmentation  
Train: Pictures are randomly resized in the range of [32, 36], then 32x32 patches are extracted randomly and are normalized locally. Horizontal flipping is applied with 0.5 probability.  
Test: Pictures are resized to 32x32, then they are normalized locally. Single image test is used to calculate total accuracy.  

* Network detail  
Fitnet4 as [[1]][Paper]] said.

* Conv layers  
All conv layers are BN-ReLU-Conv

* T  
T is calculated by BN-ReLU-Conv(3x3)-BN-ReLU-Conv(1x1)-BN-ReLU-Conv(1x1). The weights of all convs on T are initialized to 0 and all bisas are initialized to -1.

* Optimization  
SGD momentum with weight decay is used.

| momentum              | weight decay | initial learning rate |
|:---------------------:|:------------:|:---------------------:|
|0.9                    |0.0001        |0.1                    |

Learning rate is divided by 10 at [60, 120, 180] and I totally run 240 epochs. 

# Cifar10 result

| network              | depth | total accuracy (%) |
|:---------------------|-------|-------------------:|
| my implementation    | 19    | soon               |
| [[1]][Paper]         | 19    | 92.46              |

<img src="https://github.com/nutszebra/highway_networks/blob/master/loss.jpg" alt="loss" title="loss">
<img src="https://github.com/nutszebra/highway_networks/blob/master/accuracy.jpg" alt="total accuracy" title="total accuracy">

# References
Training Very Deep Networks [[1]][Paper]

[paper]: https://arxiv.org/abs/1507.06228 "Paper"