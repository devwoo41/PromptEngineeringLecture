#### Vector representation types

- Distributed representation (Dense vector)
    => 정보가 분산되어 담긴 , 의미가 여러 차원에 퍼짐
    => Semantic meaning, elements are mostly non-zero
    => reduced dimensions, fixed-size vector has no zero values, relationships between words can be expressed
    ###### The reason why dense vector can represent reduced dimensions, we could see with the simple example as a transformer. On the paper, transformer is composed of the 512 word embedding vector, thus it means one token only need 512 dimensions with the dense vector. But let's think of there are 100,000 vocabulary, then if we represent with the sparse vector, we need 100,000 dimensions.
    => simple to implement, intuitive
    ex. [2.13, 0.41, 1.19 ...], word2vec ...

- Local representation (Sparse vector)
    => 정보가 한 위치에만 있는 벡터
    => Count-based, mostly zeros
    => simple to implement, intuitive
    ex. [0, 1, 0, 0, 0, 0 ...], one-hot encoding

#### Static(context-independent) word embedding vs. contextualized word embedding

#### Language model

- a model used to predict sequence probabilities of words in a language / developed to capture patterns and regularities in human language

- sentence probability is calculated as the product of each word's conditional probability given its history.

#### Four generations of LM
    => specific task-helper (n-gram) -> task-agnostic feature learner (word2vec) -> transferable nlp task solver (bert,gpt1/2) -> general purpose task solver (gpt3/4)

- n-gram : a countiguous sequence of N words from a given text
    ```
    unigram : a sequence of one item
    bigram : a sequence of two items
    trigram : a sequence of three items
    ```

#### Deep learning based LMs 
    => Auto-encoding model (BERT) : reconstruct the original data from corrupted data / Auto-regressive model (GPT) : estimate the probability distribution of a sequence

#### BERT (Bidirectional Encoder representations from transformer)

- masked language modeling, a method to facilitate bidirectional language modeling
    ```
    randomly masks some of the tokens from input
    predict the original vocabulary id of the msked word based only on its context
    fuse the left and the right context
    ```
    
    => masking ratio : 15%, if ratio be small -> it takes a lot of time to learn, if ratio be big -> failure to fully utilize context

    => masking strategy : 80/10/10, because during fine-tuning mask is not existing *(pre train-fine tune mismatching)*. if 100 is all masked, it could be overfitted to the filling the mask.

- NSP (Next Sentece Prediction)
    
    => a method for training a model that understands sentence relationships with special token ([CLS], [SEP])
    => CLS token is for classification, because it contains all the context of the sentence.
    => SEP token to seperate two input sentences
    => test ration (50/50) -> 50 is for actual next sentence, 50 is for random next sentence

    => In later studies, there were results showing that learning NSP may not be essential.

- Prompting technique with BERT

    =>  BERT : input -> BERT -> classifier -> Label

    => Prompting technique : input -> template -> BERT -> word -> change with label