Firstly, I have started to examine the data to catch some relations and differences. Main problem was chemistry and material science were so similar domains and even an advanced RNN model LSTM with pre-trained word embeddings would not be enough to obtain goot performance results. To check my guess, I have implemented a Bidirectional LSTM model and performance results were terrible as I had expected. To use as a main text I have combined title and abstract columns of dataset.

### Performance results of Bidirectional LSTM
| Class | Precision | Recall | F1-score  |Support
| ------ | ------ | ------ | ------ |------ |
| 0 | 0.47 | 0.46 | 0.47 |740
| 1 |  0.48  |  0.49 |0.49 |759

At least to check I have found some datasets about chemistry domain words, dictionaries, frequent words to catch some differences from the domains. However, frequencies of the words used in chemistry domain and material science were also very similar, so it did not work.

Secondly, I have thought that maybe using transformers can be a good solution for such data and for this purpose, I have frozen weights of BERT and also I have fine tuned BERT. Fine tuned BERT showed better performance than frozen weights and LSTM based model. After freezing weights of BERT, I have used output of last 4 hidden states of it since it was recommended in the BERT paper. I have tried to tune hyper-parameters manually using a small subset of data. In addition, I have tried to augment the data by substituting words by contextual word embeddings (BERT, DistilBERT, RoBERTA or XLNet) using nlpaug library, unfortunately it did not affect the model performance.

### Performance results of Fine Tuned BERT

| Class | Precision | Recall | F1-score  |Support
| ------ | ------ | ------ | ------ |------ |
| 0 | 0.71  | 0.80  | 0.75  |740
| 1 |  0.77  |  0.68 |0.72 |759

In addition, I have conducted a literature search and I have seen that XLnet which is a modified version of BERT shows the new state of the art performance results for the most of the task and datasets including text classification. I have fine tuned XLNet to see can we also get better performance. I did not try to freeze its weights and add combine with some additional layers since BERT had almost same performance results. Results were slightly better, F1 score and accuracy has increased around 2 percent.

### Performance results of Fine Tuned XLNet

| Class | Precision | Recall | F1-score  |Support
| ------ | ------ | ------ | ------ |------ |
| 0 | 0.73  | 0.78  | 0.75  |740
| 1 |  0.77  |  0.72 |0.76 |759

Even though XLNet showed better performance, I was expecting better performance results because when I search online or check articles using BERT or XLNet were generally performing so good. I was thinking about the reason behind of this situation and checked every step of my implementations. I believe that if I can tune hyper-parameters deeply using techniques such as bayesian search, it could increase the performance however I could only increase the batch size up to 12 which because of the computational power of Google Colab platform.

Finally, I have realized that our dataset is so scientific and includes so many technical terms since they are articles. BERT and XLNet have trained on so general vocabulary so, maybe that could be the reason of bad performance results. After some research I have discovered a BERT model which is trained on papers from the corpus of semanticscholar.org. It is called as SciBERT. I have implemented it to see is there a performance difference however performance was so close to XLNet.

### Performance results of Fine Tuned SciBERT

| Class | Precision | Recall | F1-score  |Support
| ------ | ------ | ------ | ------ |------ |
| 0 | 0.74  | 0.71  | 0.73  |740
| 1 |  0.73  |  0.76 |0.75 |759

### Best Model Detailed Performance Analysis
 XLNet was the best model among the all models, so let me compare and add other performance metrics and ROC curve as well.
 
#### Confusion Matrix
| Class | 0 | 1 | 
| ------ | ------ | ------ | 
| 0 | 571 | 169 | 
| 1 |  200 |  559 |

#### Performance
| Class | Precision | Recall | F1-score  |Support
| ------ | ------ | ------ | ------ |------ |
| 0 | 0.73  | 0.78  | 0.75  |740
| 1 |  0.77  |  0.72 |0.76 |759

![alt text](https://github.com/umitylmz/fixy/blob/master/IMG_2654.jpg)

### Comparison on Test dataset
| Model/Metric | Accuracy | F1-score |
| ------ | ------ | ------ |
| XLNet Fine-tuned | 0.754  | 0.752  |
| SciBERT Fine-tuned |  0.736  |  0.745 |
| BERT Fine-tuned |  0.730  |  0.723 |
| BERT Frozen |  0.724  |  0.729 |
| Bi-LSTM |  0.486  |  0.512 |


### Main Challenges and Future Work

I am planning to use an outlier detection technique on training data such as Tomek-Links to seperate classes more. Since classes are so similar to each other, models can not learn differences well.
Also, with scraping more data using different resources online about the domains and using this additional data directly or indirectly, I am planning to increase the model's performance.
In addition, I would like to focus more on feature engineering, I have tried something but it did not affect the performance well however I believe that there are some ways that I could not see right now. It is not an excuse however nowadays, while I was working in a company, also I am focusing on my classes since I will be graduating from my university in one month. I believe, If I had more time I could succeed more.
I would like to tune the hyper-parameters of the model using an advanced technique. My computational power was not enough since I was using a free GPU on Google Colab. Since it is free it was limiting the usage time and even though I was using 3 accounts the same, I had so many problems during the training phases. I have used Google Colab to implement models since they are very complex, my personal computer does not have a GPU and I did not want to use my company's cluster since it is not ethical. 



