#### Word Embeddings

- Word Embedding means vector representations of word, *Vector Semantics* is the standard way to represent word meaning in NLP

- *Vector Semantics*, we could simply say it as the way to represent a word as a point in a multidimensional semantic space that is drived from the distributions of word neighbors. Similar words have Similar vectors.

#### Evaluation of Semantic Similarity

- *Cosine Similarty* : The angle between the two vectors based on the operator from linear algebra. A measure of similarity between two non-zero vectors defined in an inner product space.
    => How similar the vectors are in terms of their direction, regardless of their magnitude. (코사인 유사도에서 중요한 것은 두개의 벡터가 방향성이 같을 수록 크다는 것이다.)
    ```
    cos(theta) = (A · B) / (||A|| ||B||)
    ```

#### Word Embedding types : Context independent & Context dependent

- Context independent Embedding : It is also referred as *static word embedding*, it has a *fixed vector representation* for each word regarldss of its context. They are typically generate learn embeddings based on *word co-occurence statistics from large text corpora.*

- Context dependent Embedding : *Contextualized word embeddings* are *dynamically generated* by models that take into *account the surrounding context* of a word within a sentence. same word's representation can be different based on its *surrounding context*.

#### Static word Embedding
    ex. Word2Vec
    ```
    CBoW(Continuous Bag of Words) : 주변 단어 -> 중심 단어
    Maximize P(current word | context word)

    Skip-gram : 중심 단어 -> 주변 단어 
    ```

#### Word Analogy (단어 관계도)

- Semantic relationships between words can be confirmed through mathematical operations on word vectors. Because similar words have similar vectors.

#### Contextualized Embedding

- To generate deep contextualized representations for natural language by understanding the context and relationships between words in a text

- The same word chan have different embeddings depending on its usage, context.

#### Necessity of Word Embedding

- Converting Text into numbers enable machines to process, understand, and generate human language by representing words and phrases as numerical values.

- NLP Performacne Improvement Enhance contextual analysis & word disambiguation, Generalization