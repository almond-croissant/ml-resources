#incomplete  [[machine unlearning]]

link: https://ojs.aaai.org/index.php/AAAI/article/view/17371
gpt link: https://chatgpt.com/share/6a337e37-8800-83ee-a8c8-9e2accdbe4b5

### Problem
This paper provides a way to delete training data from the model. Previously the only way to do it was to just retrain the entire model without using the data which should be deleted/unlearned

### Key Idea
This paper proposes two methods to unlearn data. The first method is where we give random incorrect labels to the data which we need to unlearn so that the accuracy of the model on that particular dataset(which we wish to be unlearned) decreases, hence we are effectively deleting the data. 

This one is more clever. During normal training, you log which mini-batches contained which examples, and you save the parameter update (gradient step) produced by each batch. Training is just a sum of these updates added to the initial parameters:

![[Pasted image 20260618104552.png]]

When someone invokes their right to be forgotten, you simply **subtract out** the specific parameter updates that came from batches containing their data:

![[Pasted image 20260618104612.png]]




This is essentially "rewinding" just the learning steps that involved that data, in one shot — no retraining needed. The catch: because each update depends on the model state _at the time it was applied_, undoing a batch isn't mathematically identical to never having trained on it (since later updates were computed using a model that had already seen it). This approximation gets worse as more batches are removed — if you only remove a few batches, the model is barely affected and performance stays high; if you remove a lot (say, a whole class), the model takes a real accuracy hit and needs a bit of fine-tuning afterward to recover. The other cost is storage: you need to keep gradient updates around for every batch you might ever need to undo, though the authors argue this storage is still cheaper than full retraining.

### Important concepts
- log which stores parameter update caused by training of mini batches

### why does it matter
The amnesiac machine learning approach proposed by the authors here is literally subtracting the data from the neural net, literally. 

### downsides discussed in the paper
The paper is careful to note a subtlety — each update Δθe,b\Delta\theta_{e,b} Δθe,b​ depended on what the weights _were_ at that moment in training. If you trained on batch  b0​, then  b1​, then  b2​, and you undo b1​'s update, you don't get the same model as if you'd trained only on b0​ then  b2​ — because  b2​'s update was computed using weights that already included b1​'s influence. So there's a small approximation error baked in. But as long as the number of removed batches is small relative to total training, that error stays small and mostly washes out.


