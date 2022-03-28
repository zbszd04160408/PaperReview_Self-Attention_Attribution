# Paper Review: Self-Attention Attribution: Interpreting Information Interactions Inside Transformer

## Overview

1. As Transformer-based models benefits from the powerful multi-head self-attention mechanism, till this paper is published, there was no paper explain how these input features interact with each other to reach predictions. Therefore, to address the above issues, they propose a self-attention attribution method. 


<img width="466" alt="image" src="https://user-images.githubusercontent.com/56851668/160319071-5b2f7fa6-f436-43e6-9264-c53cbc3a7ea0.png">

- The attention score matrix is quite dense, so burden on us to understand how words interact with each other within Transformer
- Even if an attention score is large, it does not mean the pair of words is important to model decisions
- Self-Attention Attribution: assign  higher  scores  if  the  interaction  contributes  more  to the final prediction

2. Self-Attention Attribution Score:

<img width="346" alt="image" src="https://user-images.githubusercontent.com/56851668/160320623-39d0e9ac-3bab-4353-9778-c62e9fe84b1d.png">

3. Effective Analysis

<img width="415" alt="image" src="https://user-images.githubusercontent.com/56851668/160323010-993dccb3-2b66-4f90-bbbf-7ffe313fb697.png">

4. Use Case 1: Attention Head Pruning

<img width="402" alt="image" src="https://user-images.githubusercontent.com/56851668/160328722-3083b379-615c-4070-b432-91f396d3ff9d.png">

5. Use Case 2: Visualizing Information Flow Inside Transformer

<img width="336" alt="image" src="https://user-images.githubusercontent.com/56851668/160330492-0f01221c-6fe8-4f8f-84ad-4bc16fbee1ae.png">

6. Use Case 3: Adversarial Attack

<img width="430" alt="image" src="https://user-images.githubusercontent.com/56851668/160335207-c4480e92-0401-418f-aeef-03f7d98127d9.png">


## Critical Analysis

This paper kind of missing details of each experiment. For the first use case, I actually did not see a great improvment of AttAttr compared with the Taylor method. For the second use case, when they implement the tree visualization, they chose tau = 0.4 as a threshold, but did not explain on their choice of this threshold. Intuitively, a threashold of 0.5 makes more sense. The process of deciding on 0.4 as their threshold should be more discussed. Also, there is no baseline model for this part of experiment. For the third use case, there are only three sets of triggers from each dataset. I am concerned if this is enough, and why they choose such sets of triggers.  


## Discussion

### Topic 1:



### Topic 2:

What other use cases can you come up with the Self-Attention Attribution method? 


### Topic 3:

As this paper is nominated as the Best Paper Award, why do you think this paper can stand out? 

## Resource Links

## Video Recording
