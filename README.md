# Explaining Backpropogation using an excel

![image](https://github.com/KartikS07/ERAV1_S6_Assignment_Part_1/assets/135399864/d5edd423-5d79-49b2-af3f-d9dd5a7d6e92)

We will be using the above example with an input layer, 1 hidden layer & 1 output layer to explain backpropogation. 

Let's understand the nomeclature first:

i1, i2 -> Input Neurons
h1,h2 -> Nuerons in the hidden layer
a_h1, a_h2 -> Neurons in the hidden layer post the activation -> Also called activated hidden layer neurons -> In this example, we are using the Sigmoid Activation function
o1, o2 -> Output layer neurons
a_o1, a_o2 -> Activated output layer neurons
t1, t2 -> 2 Targets -> These are the ideal desired output values from the neural network
E1 -> Loss of the first ouput a_o1 as compared to the first target t1 -> In this example, we are computing the mean squared error
E2 -> Loss of the second ouput a_o2 as compared to the second target t2
E_Total -> Total Loss -> Used to determine model accuracy = E1+E2
w1,w2,w3...w8 -> Weights of the neural network connecting subsequent layers. These get updated after every epoch.

From the above image, A few equations can be derived based on the basic neural network architecture
h1 = w1*i1 + w2*i2		
h2 = w3*i1 + w4*i2		
a_h1 = σ(h1) = 1/(1 + exp(-h1))	-> Formula for Sigmoid
a_h2 = σ(h2)		
o1 = w5*a_h1 + w6*a_h2		
o2 = w7*a_h1 + w8*a_h2		
a_o1 = σ(o1)		
a_o2 = σ(o2)		
E_total = E1 + E2		
E1 = ½ * (t1 - a_o1)²		-> Formula for MSE
E2 = ½ * (t2 - a_o2)²		

Now, The Objective of backpropogation is to arrive at the final weights w1,w2 ... w8 as soon as possible so that the total loss (E_total) is miminum. To find this, the weights w1 ... w8 get updated using the below formula:

[w1 = w1 - (α) * ðE_total/ ðw1] & similar for all the other weights.


In order to compute the weights after every epoch, we need to compute the partial derivates of the total loss (E_total) with all the weights. Let us go that for one weight - w5 & then we will compute it similarly for all the other weights

ðE_total/ ðw5 = ð(E1+E2)/ðw5 = ðE1/ðw5 + ðE2/ðw5

Now, if we observe from the above diagram, w5 has no relation to E2 since w2 only contributes in computing o1 & by extension a_o1 & E1. Hence ðE2/ðw5 = 0.

Hence, ðE_total/ ðw5  = ðE1/ðw5

Now using the chain rule in differentiation,

ðE_total/ ðw5  = ðE1/ðw5 = (ðE1/ða_o1) * (ða_o1/ðo1) * (ðo1/ðw5)

ðE_total/ ðw5  = ðE1/ðw5 = (∂(½ * (t1 - a_o1)²)/∂a_o1) * (∂(σ(o1))/∂o1) * (a_h1)
**ðE_total/ ðw5  = ðE1/ðw5 = (a_01 - t1) * (a_o1 * (1 - a_o1)) * (a_h1)

Similarly, We can compute the other partial differentiations too using chain rule:
∂E_total/∂w5 = (a_01 - t1) * a_o1 * (1 - a_o1) *  a_h1					

∂E_total/∂w6 = (a_01 - t1) * a_o1 * (1 - a_o1) *  a_h2					

∂E_total/∂w7 = (a_02 - t2) * a_o2 * (1 - a_o2) *  a_h1					

∂E_total/∂w8 = (a_02 - t2) * a_o2 * (1 - a_o2) *  a_h2

∂E_total/∂w1 = ((a_01 - t1) * a_o1 * (1 - a_o1) * w5 +  (a_02 - t2) * a_o2 * (1 - a_o2) * w7) * a_h1 * (1 - a_h1) * i1												

∂E_total/∂w2 = ((a_01 - t1) * a_o1 * (1 - a_o1) * w5 +  (a_02 - t2) * a_o2 * (1 - a_o2) * w7) * a_h1 * (1 - a_h1) * i2												

∂E_total/∂w3 = ((a_01 - t1) * a_o1 * (1 - a_o1) * w6 +  (a_02 - t2) * a_o2 * (1 - a_o2) * w8) * a_h2 * (1 - a_h2) * i1												

∂E_total/∂w4 = ((a_01 - t1) * a_o1 * (1 - a_o1) * w6 +  (a_02 - t2) * a_o2 * (1 - a_o2) * w8) * a_h2 * (1 - a_h2) * i2												


The below part of the excel then just plugs in these values to update the weights across 68 epochs sequentially using the weight updation formula ([w1 = w1 - (α) * ðE_total/ ðw1])

![image](https://github.com/KartikS07/ERAV1_S6_Assignment_Part_1/assets/135399864/e9265572-eb0c-4566-ab54-e5a7b09c4c6d)



We have also plotted a graph of the loss against each of the epochs and we can see how it drops more steeply as we increase the learning rate from 0.1 to 2 in this case, thus needing lesser number of epochs to converge. This tells us that the ideal learning rate for this particular example is greater than 1 (It actually turns out to be somewhere between 60 & 70 for this example, which is much higher than the typical learning rates which are around 0.1):

Learning Rate = 0.1
![image](https://github.com/KartikS07/ERAV1_S6_Assignment_Part_1/assets/135399864/0f16e8af-5308-409f-aadc-dd9f2984864a)

Learning Rate = 0.2
![image](https://github.com/KartikS07/ERAV1_S6_Assignment_Part_1/assets/135399864/9bf7805f-9996-4899-9755-0b518a9243ff)

Learning Rate = 0.5
![image](https://github.com/KartikS07/ERAV1_S6_Assignment_Part_1/assets/135399864/8778cd5a-b0ae-4153-a119-30522738b00d)

Learning Rate = 1
![image](https://github.com/KartikS07/ERAV1_S6_Assignment_Part_1/assets/135399864/408921b0-23fe-4836-9324-e5e5a67753bf)

Learning Rate = 2
![image](https://github.com/KartikS07/ERAV1_S6_Assignment_Part_1/assets/135399864/565e674f-a0bb-4db3-bcf1-926e62278bbc)






