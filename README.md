ECG Signal Classification using CNN and wavelet transform

This project aims to classify human ECG signals into three categories: NSR (normal sinus rhythm), ARR (atrial premature beat), and CHF (congestive heart failure). The project was conducted in the Signal and Image Processing Lab of the Electrical Engineering Faculty at the Technion, under the supervision of Dr. Meir Bar Zohar.

Data

The Physionet database is a publicly available collection of ECG signals recorded from various sources. The database contains 162 recordings of 512-second ECG signals, with a sampling frequency of 128 Hz, including normal and abnormal rhythms, as well as signals from healthy individuals and those with various cardiac conditions.

Part 1 - Wavelet Transform

In this section, we preprocess each signal using wavelet transform and create scalograms for the whole 512 seconds. Additionally, we break each signal into four segments of 128 seconds each, eight segments of 64 seconds each, and 64 segments of 8 seconds each. We apply wavelet transform to each segment and create scalograms for each segment. We then save all the scalograms as RGB images to the PC memory. Each scalogram is shaped 224 X 224 X 3.

Part 2 - CNN

We utilize the ResNet 18 architecture to train four different models, each trained on a different scalogram length, namely, 512 seconds, 128 seconds, 64 seconds, and 8 seconds. We use the scalograms generated from Part 1 and their corresponding ground truth to train, validate, and test each model. To train each model, we preprocess the scalogram images using PyTorch dataset and dataloader. We train each model with its specific scalogram length and save each model to the PC memory. We aim to train each model to achieve a test score of approximately 0.95.

Part 3 - Patient Classification using Multiple Scalogram Lengths and FC Neural Network

In this part, we train a patient classifier using the scalograms generated in Part 1 and the trained ResNet models from Part 2. The objective is to collect 76 scalograms from each patient, including four of length 128, eight of length 64, and 64 of length 8 seconds. These scalograms are processed through the corresponding ResNet model trained on the appropriate scalogram length, resulting in three probabilities for each scalogram indicating whether it belongs to an ARR patient, CHF patient, or NSR patient. In total, each patient is represented by a feature vector of 228 values.
The combination of different scalogram lengths provides a rich representation of the signal as the short length can reveal short phenomena from one heartbeat to another, while the longer length can demonstrate how the signal changes over a more extended period.

The classifier used for this part is a fully connected neural network (FC NN), which is trained on the feature vectors of the training set and validated on the validation set. The accuracy of the system is evaluated on the test set, and it is found that the system only made an incorrect prediction for one patient out of 32 patients. The accuracy of the system is 96.88%, where the one incorrect prediction was for a patient whose ground truth label was ARR, but the system predicted CHF.
In most cases, the system correctly predicts the label of the patient with over 99% confidence, indicating high accuracy in the classification task.


Conclusion

This project demonstrates the effectiveness of using wavelet transform and CNN to classify ECG signals. The use of multiple scalogram lengths provides a rich representation of the signal, which can significantly improve the accuracy of the classification task. The FC NN classifier trained on the feature vectors achieved high accuracy in the patient classification task, with only one incorrect prediction out of 32 patients. This project can be useful in diagnosing cardiac conditions and improving patient care.