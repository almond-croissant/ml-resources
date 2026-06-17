#incomplete  [[machine unlearning]]

 link: https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9519428

### Problem
This paper provides a way to delete training data from the model. Previously the only way to do it was to just retrain the entire model without using the data which should be deleted/unlearned

### Key Idea
divide the training data into shrads and then slices and store the snapshot of the model after using every slice. When a user wants their data removed, the company only has to retrain the **single affected shard model** starting from the last checkpoint saved before that specific data was introduced.

### Important concepts
- Shrads
- slices
- aggregation

### Why it matters
Coz this is an easy algorithm to delete the data from the ml model and it is a much faster implementation than the traditional ones. 


