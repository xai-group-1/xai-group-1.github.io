\documentclass{article}
\usepackage{markdown}
\begin{document}
\begin{markdown}

# Team 123

*Authors: Mikołaj Pacek, Mateusz Kierznowski, Piotr Nawrot, Robert Krawczyk*

*Mentors: Michał Miktus (McKinsey & Company)*


## Introduction 

Running a business is a big challenge. Especially when the business is in e-commerce's branch. There are a lot of minutiae that can give a company a competitive edge and establish customer confidence. One of them is felicitous recommendation model, which contributes to the best fitting products to the firstly choice.

Only 7% orders from schumee contains more than one product. It could not only increse the probability that the customer buy more products, but also makes shopping on that website more instinctive and comfortable.  



## Data preprocessing
TODO


## Model 

Our main target is to build a model, which could recommend products similar to products in the basket. The model has 3 steps

- word2vec (BERT)
- clustering
- recommendation 


### BERT

BERT stands for Bidirectional Encoder Representations from Transformers. That language model can manage with ambiguity of the text by following steps. Firstly BERT is based on the Transformer architecture. Secondly BERT is a deeply bidirectional which  means that BERT learns information from both the left and the right side of a word’s context during the training.The bidirectionality of a model is extremely important in understanding context of a sentence. Provided illustration shows how BERT understand context bidirectionally.
![BERT](BERT.png "BERT bidirectional context")


In paper we have used BERT to provide word embeddings for every product name within the data. The quality of embedded word is vastly important in following cluster phase. In work we have used sentence_transformers module to provide BERT model


### Clustering

Once we have a representation of products in the vector space we want to cluster them. The embeddings we got from BERT have a property, that sentences that are semantically similar are mapped to vectors that are close to each other. The intuition behind clustering is that we want to create groups of products that are similar to each other. However it is not obvious how big such clusters should be. 

#### Metrics
We defined 2 metrics that helped us to decide whether given clustering is 'good'.

##### Percent of orders inside clusters
TODO describe it

##### Scraped categories fit
TODO describe it

#### Clustering tuning (TODO better title)
We chose 2 clustering algorithms (KMeans and AglomerativeClustering) and clustered the data with different hyperparameters (number of clusters). Then we plotted metrics that we defined before and chose the best algorithm with best hyperparameter based on a human intuition. 


### Recommendation
Given a new product (its name), we pass it to the BERT to get its embedding, then we search for the closest cluster and then we choose from this cluster, a product to recommend. We can choose this product based on 


## Explanations


### Reccomendation Interpretability

#### Lime 

In order to explain clusters we use LIME method. In our case LIME shows contribution of each word to the cluster of that word. This provides local interpretability which can be extend to determine the core words for every cluster.

Recommendation system may be interpret by providing LIME method into input which stands for product client wants to buy and recommendation which is a product our system may choose.

Suppose client wants to buy product named 'metal fence + pvc roll' (siatka ogrodzeniowa metal + pcv rolka).
Firstly LIME can help undestanding why this specific product is located in peculiar cluster.

![lime1](limet1.png "lime product")

Now we can ask system about recommendation to this product. Our model shows that galvanized fence mesh (siatka ogrodzeniowa ocynkowana) is the proper recommendation.
Secondly we can use LIME to see contributions within the same cluster. 

![lime2](limet2.png "lime recomendation")

This case provide an insight that word “ogrodzeniowa” connects this two sentences and it’s explanations why our model recommended that specific sentence. 

As mentioned LIME contributions per word can be accumulated in specific cluster. Thus LIME indicate words which has vast positive or negative contributions within cluster.

For cluster NO.1 which is presented by following fig.

![cluster0](cluster0.png "cluster No. 1")

we cumulated LIME method for every word. LIME indicate five words which provide positive impact to the cluster and another five with negative impact:

![cluster0bestwords](cluster0bestwords.png "best and worst words")

The data shows that words connected to the light have positive impact to the cluster. As we can see from figure 3 all sentences connect it's meaning to the lighting. Other words has rather zero or provide negative impact within cluster. 

#### Shap

##### Issues with implementation

##### Classic

##### Owen Values


### Cluster Interpretability

#### Lime

#### Shap


## Buisness validation on historical data

### 2 metrics


## Summary and conclusions 


### Why tokens like "n czarny" appear?

### Comparing explanations with Lipschitz's method

### AB testing


\end{markdown}
\end{document}
