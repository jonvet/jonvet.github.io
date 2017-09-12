---
layout: post
title:  "Inferring Sentence Features from Sentence Embeddings"
date:   2017-09-12 16:05:18 +0100
categories: NLP
---
In my thesis I investigate which sentence features are encoded by Recurrent Neural Networks (RNNs). I train two state-of-the-art RNN sentence encoders:
- Skip-thought [(Kiros et al, 2015)](https://arxiv.org/abs/1506.06726); and
- BiLSTM-max [(Conneau et al, 2017)](https://arxiv.org/abs/1705.02364);

and compare them against a CBOW (continuous-bag-of-words) baseline, which represents sentences by averaging pre-trained word vectors. 

I evaluate the models on three tasks: 
- Predicting the length of a sentence;
- Predicting the presence of a word; and 
- Predicting dependencies between words. 

My findings are that on tasks where information about the full sentence or the order of words is not important (e.g. the word content task) the CBOW baseline performs on par with the RNN encoders. And on tasks where information about the full sentence or order of words is important (e.g. the sentence length and dependency tag tasks), the RNNs outperform the CBOW baseline. 

The main contribution of this thesis is to show that dependency tags can be retrieved from a classifier which has only access to the sentence embedding, and the embeddings of two words. This provides some evidence that RNNs are capable of learning syntactic relationships between words, even if this was not part of the objective they were trained on. 

<!-- https://s20.postimg.org/9s759vtjx/results_con_exec.png -->
<!-- https://s20.postimg.org/pg8cgo95p/results_len_exec.png -->
<br>
<center>
<figure>
    <figcaption><b>Figure 1: </b>F1 score on dependency tag prediction task</figcaption>
    <img src="https://s20.postimg.org/q4h6zm7vh/results_dep_50_m_nn_exec.png" alt="Drawing" style="width: 400px;"/>
</figure>
</center>

<br>
Upon further inspection of sentence embeddings, I also illustrate that certain dimensions carry information about specific aspects of the sentence. I show that there are differences across models with respect to how strongly, and in how many dimensions such aspects are encoded.
<br>
<br>
<center>
<figure>
    <figcaption><b>Figure 2: </b>Visualization of sentence embeddings</figcaption>
    <img src="https://s20.postimg.org/julxcm8gt/Screen_Shot_2017-09-12_at_18.42.59.png" alt="Drawing" style="width: 400px;"/>
</figure>
</center>
<br>
Full thesis can be found [here](https://github.com/jonvet/thesis/blob/master/Inferring_Sentence_Features_from_Sentence_Embeddings.pdf).

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
