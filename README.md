# Bengio et al. 2003 — Character Embedding Analysis

simple project but gotta start somewhere. read the paper, built the 
model, stared at a scatter plot for way too long.

A from-scratch implementation of the neural language model from 
Bengio et al. (2003), trained on a dataset of names. The main thing 
I wanted to do was visualise the 2D character embedding space and 
see what structure the network figures out on its own, without being 
told anything about phonetics or linguistics. turns out it figures 
out quite a bit, and what it figures out lines up pretty well with 
what the paper argues

## What I did
- Implemented the MLP from the paper in PyTorch from scratch
- Trained on 80/10/10 train/dev/test split of the names dataset
- Visualised the learned 2D embedding space and spent probably too 
  much time analysing why q is so lonely

## Main findings
- The paper argued that learned embeddings capture task-specific signal 
  rather than general corpus statistics, and the outlier analysis 
  directly confirms this. p and f are common in English generally but 
  rare in names, and the model pushes them to the periphery. a 
  pre-computed co-occurrence embedding would never do this.
- Phonetic category does not drive clustering, following distribution does.
  y and h end up close together despite having nothing phonetically in 
  common, purely because they share the same top two following characters. 
  the network does not care about linguistics, only statistics. which is 
  kind of the whole point of the paper.
- Vowels partially cluster but not uniformly, which also lines up with 
  the paper's claim that similar words (or in this case characters) end up 
  close in embedding space. i is isolated because of the ia ending pattern 
  in names like julia, olivia, sofia. a and e are basically best friends.

## To do
-[ ] Implement the skip connection from the original paper and compare 
  the embedding space against the baseline
-[ ]Repeat the analysis on a non-English names dataset to test whether 
  the same clusters emerge or whether the structure looks completely different

## Reference
Bengio et al. (2003). A Neural Probabilistic Language Model. JMLR.
