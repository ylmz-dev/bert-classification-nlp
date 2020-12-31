Firstly, I have started to examine the data to catch some relations and differences. Main problem was chemistry and material science were so similar domains and even an advanced RNN model LSTM with pre-trained word embeddings would not be enough to obtain goot performance results. To check my guess, I have implemented a Bidirectional LSTM model and performance results were terrible as I had expected.

### Performance results of Bidirectional LSTM
| Class | Precision | Recall | F1-score  |Support
| ------ | ------ | ------ | ------ |------ |
| 0 | 0.47 | 0.46 | 0.47 |740
| 1 |  0.48  |  0.49 |0.49 |759

At least to check I have found some datasets about chemistry domain words, dictionaries, frequent words to catch some differences from the domains. However, frequencies of the words used in chemistry domain and material science were also very similar, so it did not work.

Secondly, I have thought that maybe using transformers can be a good solution for such data and for this purpose, I have frozen weights of BERT and also I have fine tuned BERT. Fine tuned BERT showed better performance than frozen weights and LSTM based model. After freezing weights of BERT, I have used output of last 4 hidden states of it since it was recommended in the BERT paper. I have tried to tune hyper-parameters manually using a small subset of data.

### Performance results of Fine Tuned BERT

| Class | Precision | Recall | F1-score  |Support
| ------ | ------ | ------ | ------ |------ |
| 0 | 0.71  | 0.80  | 0.75  |740
| 1 |  0.77  |  0.68 |0.72 |759

In addition, I have conducted a literature search and I have seen that XLnet which is a modified version of BERT shows the new state of the art performance results for the most of the task and datasets including text classification. I have fine tuned XLNet to see can we also get better performance. I did not try to freeze its weights and add combine with some additional layers since BERT had better performance results with only fine tuning. Results were slightly better, F1 score and accuracy has increased around 2 percent.

### Performance results of Fine Tuned XLNet

| Class | Precision | Recall | F1-score  |Support
| ------ | ------ | ------ | ------ |------ |
| 0 | 0.73  | 0.78  | 0.75  |740
| 1 |  0.77  |  0.72 |0.76 |759

