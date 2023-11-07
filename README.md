# 5th place Brief Solution (write by ΜΑΡΙΟΣ ΜΙΧΑΗΛΙΔΗΣ KAZANOVA)
First of all congrats to the winners for a solid performance and obviously my teammates for this competitive top 10 finish. There was lots of buzz and sharing in this competition and we have learnt a lot - credit should be given to all people who shared stuff - you are all part of this solution :)

We have Implemented most of the kernels in this competition - Found the Neptune examples to perform very well on the leader-board, so thank you very much for the share!

The best linear model was around 0.9814 at LB and It was an LSVC (linear support vector machine) model.

Best lightgbm was around 0.9830 and had up to 2-gram words, stemming and up to 6 char char-grams along with some features generated from word2vec and pre-trained embeddings.

Our best NN was a 2-level bidirectional gru followed by max pooling and 2 fully-connected layers. Core improvements over baseline were exponential learning rate annealing, skip-connections around hidden layers, and 900d embeddings that consisted of concatenated glove, fasttext with subword information and fasttext crawl. This scored 0.9865 (and 0.9861 private).

Other notable mentions include a char-level DPCNN and RNN trained over wordparts produced by byte-pair encoding. Other strong NNs were based on the implementation shared by Pavel Ostyakov

Also the lstm from Neptune with an additional input for chars (dual input) and stemming had a score near 0.9860.

In meta modelling we had 2 layers of stacking:

The first layer consisted of more than 120 base models (all x6 columns), mostly Deep nns trained with slightly different architectures and different embeddings. We trained a 2-hidden layer NN, an ET and a lightgbm (per target-column) model. Then the same 3 models including some additional count features for uppercase words. And finally the same 3 models but all input data transformed into ranks as well as a linear combination of some of the input (120) models. So uplift of about .0012 (to 0.9877 from 0.9865) came from this layer of stacking.

Second layer is essentially a weighted average of all these models after transforming them to ranks. Got a further +0.0004 to 0.9881)

Ps. Third Layer did not add value.

Also this is a photo of our ensemble:

imagehttps://kaggle2.blob.core.windows.net/forum-message-attachments/300446/8841/stacking_5th_place.png

stacking_5th_place.png