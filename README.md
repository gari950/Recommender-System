# Recommender-System

Library used:

![](https://img.shields.io/static/v1?label=LightFM&message=light-fm&color=orange)

A hybrid recommender is a special kind of recommender that uses both collaborative and content based filtering for making recommendations.

Put simply, LightFM can use the normal user-item interactions for making predictions for known users. In the case of new users, it can make predictions if it knows some additional information about these new users. This additional information could be features like gender, age, ethnicity, etc and must be fed to the algorithm during training.

Four loss functions are available:

- logistic: useful when both positive (1) and negative (-1) interactions
  are present.
  
- BPR: Bayesian Personalised Ranking pairwise loss. Maximises the
  prediction difference between a positive example and a randomly
  chosen negative example. Useful when only positive interactions
  are present and optimising ROC AUC is desired.
  
- WARP: Weighted Approximate-Rank Pairwise loss. Maximises
  the rank of positive examples by repeatedly sampling negative
  examples until rank violating one is found. Useful when only
  positive interactions are present and optimising the top of
  the recommendation list (precision@k) is desired.
  
- k-OS WARP: k-th order statistic loss. A modification of WARP that
  uses the k-th positive example for any given user as a basis for pairwise
  updates.
  
 # AUC graph by comparing the loses
![image](https://user-images.githubusercontent.com/80147820/179364918-ce670018-bfa4-4454-a01c-8f2c6ae867c5.png)

# efficiency of the models
Hybrid training set AUC using warp loss: 0.9327615
Hybrid training set AUC using bpr loss: 0.88347363
Hybrid training set AUC using logistic loss: 0.8658272
Hybrid training set AUC using warp_kos loss: 0.9050389

Conculsion: 

- unlike BPR that updates parameters for every iteration, WARP only updates parameters when the model predicts the negative item has a higher score than the positive item.

- At a high level, WARP loss will randomly sample output labels of a model, until it finds a pair which it knows are wrongly labelled, and will then only apply an update to these two incorrectly labelled examples.

- In particular, its approach of optimizing for ranking instead of absolute outputs makes it particularly well suited to recommenders, and in addition to its current applications in matrix factorisation recommenders, it can also be applied to neural network — based recommenders.
