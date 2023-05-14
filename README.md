# BackPropagation From Scratch 

## Inspiration
With the rise of AI and Deep Learning these days, people who are jumping into the field seem to forget that all of this 'magic' is actully just calculus and linear algebra acting behind the scenes. 
The idea of propagating error backwards through the network to change the weights and biases seems to have been placed under all the hype about Deep Learning. Overlooking this crucial idea will definitely make 
[Dr Hinton](https://en.wikipedia.org/wiki/Geoffrey_Hinton), [Dr Ng](https://en.wikipedia.org/wiki/Andrew_Ng), [Dr Schmidhuber](https://en.wikipedia.org/wiki/J%C3%BCrgen_Schmidhuber) and so many others would be highly disappointed.
So, being the curious and trouble seeking monkey that I am, I was inspired to stress myself out to build a Neural Network with 41 parameters without using any frameworks, just pure calculus and linear algebra.

## Workings
![img](https://github.com/vanilladucky/BackPropagation/assets/77542415/1369a788-dd02-424c-82ca-ff75f1d3a3ab)
As you can see, it all started from my iPad's notes app. My **idea** was to come up with a network that would be able to learn the function $z = 5 \times a^2 + 3 \times b^2$. With sufficient layers, hidden nodes and an appropriate 
non-linear activation function, I convinced myself that I can come up with a sufficiently accurate model. 
<br></br>
So I came up with 2 models. As someone who has been utilizing PyTorch for about a year or two, I built one model with PyTorch and another from scratch. 
<br></br>
Obviously, building with PyTorch was way simpler. All I needed was to add two linear layers and an softmax activation layer in the middle. With the model from scratch, I used the same architecture but I had to
code up the famous `loss.backward()` and `optimizer.step()` steps from scratch. I could not explain how much of a pain in the back it was. So I religiously listened to [3Blue1Brown](https://www.youtube.com/watch?v=tIeHLnjs5U8&ab_channel=3Blue1Brown)'s
video about BackPropagation Calculus. With only that video in my hands, I managed to come up with a somewhat similar model to the PyTorch one. 
<br></br>
As you can see in the image above, that is where I laid out all the mathematics that were required in my calculations. I do not believe I made any significant mistakes throughout the calculation
as my model showed improvement throughout training. However, if you do see a mistake, please feel free to open a pull request and fix it. I would appreciate it!

## Results 
As you can see in the codes, the results are very different. The PyTorch model performed immensely better while my custom model trained and was stuck at the loss of around 68. I have attempted to 
alter the learning rate and such but I do not seem to be able to get it lower than 68. It might be that the gradient descent failed and was stuck at a local optima. If any of you have any suggestions or fixes, 
again, please feel free to open a pull request. 

## Conclusion 
Personally, I learnt a lot throughout this endeavour. Although it took me roughly 12 hours from coming up with the idea to seeing the training and validation loss drop, I am proud to say I have understood how 
deep learning models work behind the scenes and what is exactly going on behind `loss.backward()` and `optimizer.step()`. 
<br></br>
And the most important point is that now that I can confidently say I understand the mathematics and mechanics behind deep leaning, I shall stick to the PyTorch framework, and heavily abuse the magical `loss.backward()` and `optimizer.step()` methods 🤓

## Credits
* https://www.youtube.com/watch?v=tIeHLnjs5U8&ab_channel=3Blue1Brown
* All of my mathematics teachers so far who have kept up with me and taught me calculus and linear algebra 😇

## Fixes (14/05/23)
The idea of the significantly poor performance of the custom model has bothered me to I decided to take a look at what the problem could be. After manually observing the changes in weights and biases and the changes in it, I have stumbled upon several findings. 
1) The initial set up of weights and biases is crucial. Certain set up such as a normal distribution within the ranges of -4 and 4 gave a result that is significantly better than when using `torch.randn`.
2) The problem of exploding gradients was severe as well. Just after the first epoch, the weights and biases figures were off the chart and reaching six figures. This is where I realized the importance of gradient clipping and normalization. As you can see in the code, I have experimented with several different values of clipping and I found out for this specific problem, values around the magnitude of 0.5 and 2 were the most optimal. However, the alternative method of gradient normalization was not as effective as I thought it would be. 
