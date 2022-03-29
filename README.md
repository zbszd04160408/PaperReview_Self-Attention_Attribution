# Paper Review: Self-Attention Attribution: Interpreting Information Interactions Inside Transformer

## Overview

1. As Transformer-based models benefits from the powerful multi-head self-attention mechanism, till this paper is published, there was no paper explain how these input features interact with each other to reach predictions. Therefore, to address the above issues, they propose a self-attention attribution method. 


<img width="466" alt="image" src="https://user-images.githubusercontent.com/56851668/160319071-5b2f7fa6-f436-43e6-9264-c53cbc3a7ea0.png">

- The attention score matrix is quite dense, so burden on us to understand how words interact with each other within Transformer
- Even if an attention score is large, it does not mean the pair of words is important to model decisions
- Self-Attention Attribution: assign  higher  scores  if  the  interaction  contributes  more  to the final prediction

2. Self-Attention Attribution Score:

<img width="346" alt="image" src="https://user-images.githubusercontent.com/56851668/160320623-39d0e9ac-3bab-4353-9778-c62e9fe84b1d.png">

- dot product means element-wise multiplication
- Ah denotes the h-th head's attention weight matrix
- the integral part computes the gradient of model F


3. Effective Analysis

<img width="415" alt="image" src="https://user-images.githubusercontent.com/56851668/160323010-993dccb3-2b66-4f90-bbbf-7ffe313fb697.png">

If we prune the heads with small attribution score first, the accuracy can even increase. 
If we prune the heads with large attribution score, the accuracy will decrease majorly.
Compared with pruning heads with large or small attention scores, the influence on pruning head with attribution score is more obvious. 


4. Use Case 1: Attention Head Pruning

<img width="402" alt="image" src="https://user-images.githubusercontent.com/56851668/160328722-3083b379-615c-4070-b432-91f396d3ff9d.png">

According to the previous sections, they get the idea that only a small part of attention heads contribute to the final prediction, while others are less helpful. 
To do the experiment, they calculated the importance score from 200 different examples. They sort all the heads according to the importance metrics, and less important heads are first pruned. In their experiment, they used the Taylor Expansion as a baseline model to compare with. 
From this graph, we can see that the pruning performance of the attribution methods is competitive with the Taylor expansion method. 
On the MNLI dataset, when only 10% attention heads are retained, the attribution method can still achieve ~60%  accuracy. 


5. Use Case 2: Visualizing Information Flow Inside Transformer

<img width="336" alt="image" src="https://user-images.githubusercontent.com/56851668/160330492-0f01221c-6fe8-4f8f-84ad-4bc16fbee1ae.png">

The second use case is to construct attribution tree based on the attribution method. This tree helps indicate how information flows from input tokens to the final prediction. 

Algorithm: 

For each layer we first calculate AttATTR scores of different heads, then sum then up. 
Then, they need to decide a threshold between maximizing the summation of attribution scores and minimizing the number of edges in the tree. Here they chose 0.4 as their threshold. 

This sentence is from SST-2 dataset, which the task of this dataset is to classify the sentiment of each sentence. This sentence is positive, and from this tree, we can observe that information in the first part of the sentence ”seldom has a movie so” is aggregated to the “has” token. “the spirit of a man and his work” flows to the sprit token. Both words have strong positive tendency. Finally, all the information aggregates to the verb “matched”, give us better understanding on how the model makes the prediction. 


6. Use Case 3: Adversarial Attack

<img width="430" alt="image" src="https://user-images.githubusercontent.com/56851668/160335207-c4480e92-0401-418f-aeef-03f7d98127d9.png">

The third use case is the adversarial attack. 
They noticed that some of the models tend to over-emphasize some individual patterns to make the prediction but omitting most of the input. 

They extract the attention dependencies with the largest attribution scores across different layers from the input and employ these patterns as the adversarial triggers. They insert the triggers into the test input at the same relative position as in the original sentence.  

Two patterns “floods-ice” and “Iowa-Florida” contributes most to the prediction contradict in the source sentence. Then, they put the two patterns into other sentences as an attack. The second sentence here originally has a relationship of entailment. After adding triggers, it turns out to be contradiction. The third one is originally neutral, and becomes contradiction after adding the triggers. 


## Critical Analysis

I like this paper because
- Not only proposing a new methods, but also come up with a lot of use cases of this methods
- Practical and enlightening for future use either in the industry or in the academia. 

Some improvement I can think of:
- some typos
- For the second use case, when they implement the tree visualization, they chose tau = 0.4 as a threshold, but did not explain on their choice of this threshold. Intuitively, a threshold of 0.5 makes more sense. I believe they did not select 0.4 as the threshold randomly. The process of deciding on 0.4 as their threshold should be more discussed. This can be helpful when people use this visualization in the future.
- For the third use case, there are only three sets of triggers from each dataset. I am concerned if this is enough. They said they chose top 3 patterns, but what is the process of choosing the top 3 patterns? Also, how did they decide on trigger positions? I am wondering have they tried different positions, and will different positions make the result different.


## Discussion

### Topic 1:

Do you think more tokens means higher accuracy when training Transformer models? 

### Topic 2:

What other use cases can you come up with the Self-Attention Attribution method? 

### Topic 3:

As this paper is nominated as the Best Paper Award, why do you think this paper can stand out? 

## Resource Links

Paper: https://arxiv.org/abs/2004.11207

Repo: https://github.com/YRdddream/attattr

Video: https://www.youtube.com/watch?v=0keN57ao9J8

## Video Recording

https://youtu.be/lhvjhozmDlE

## Code Demo

In this repo. 
