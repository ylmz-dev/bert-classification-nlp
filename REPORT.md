Firstly, I have started to examine the data to catch some relations and differences. Main problem was chemistry and material science were so similar domains and even an advanced RNN model LSTM with pre-trained word embeddings would not be enough to obtain goot performance results. To check my guess, I have implemented a Bidirectional LSTM model and performance results were terrible as I had expected.

However at least to check I have found some datasets about chemistry domain words, dictionaries, frequent words to catch some differences from the domains.


             precision    recall  f1-score   support

           0       0.47      0.46      0.47       740
           1       0.48      0.49      0.49       759

    accuracy        -         -        0.48      1499
   macro avg       0.48      0.48      0.48      1499
weighted avg       0.48      0.48      0.48      1499
