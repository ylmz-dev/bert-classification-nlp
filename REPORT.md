Firstly, I have started to examine the data to catch some relations and differences. Main problem was chemistry and material science were so similar domains and even an advanced RNN model LSTM with pre-trained word embeddings would not be enough to obtain goot performance results. To check my guess, I have implemented a Bidirectional LSTM model and performance results were terrible as I had expected.

### Performance results of Bidirectional LSTM
| Class | Precision | Recall | F1-score  |Support
| ------ | ------ | ------ | ------ |------ |
| 0 | 0.47 | 0.46 | 0.47 |740
| 1 |  0.48  |  0.49 |0.49 |759

In addition, at least to check I have found some datasets about chemistry domain words, dictionaries, frequent words to catch some differences from the domains. However, frequencies of the words used in chemistry domain and material science were also very similar, so it did not work.

Secondly, I have thought that maybe using transformers can be a good solution for such data and for this purpose, I have frozen weights of BERT and also I have fine tuned BERT. Fine tuned BERT showed better performance than frozen weights and LSTM based model.

### Performance results of Fine Tuned BERT

| Class | Precision | Recall | F1-score  |Support
| ------ | ------ | ------ | ------ |------ |
| 0 | 0.71  | 0.80  | 0.75  |740
| 1 |  0.77  |  0.68 |0.72 |759
