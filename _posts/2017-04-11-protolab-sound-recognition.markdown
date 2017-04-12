---
layout: post
title:  "Protolab Sound Recognition"
date:   2017-04-11 00:33:14 +0530
categories: Audio identification, Sound
---

### Sound Recognition

- Audio Conversion from other formats:
    - [PyDub](http://pydub.com/)
    - Seems to support all the formats ffmpeg seems to support
- Sound Silence Detection:
    - Average the sound over a period of 10 samples and check whether it crosses a threshold. (Assuming a 44.1Khz Sampling rate this comes to a 0.2 msec)
    - If this keeps happening continously for a period segment that region and send it for further processing. Lets say around 70-80 percent in a period of 1 second.
    - We can play around with the values
    - http://dsp.stackexchange.com/questions/1522/simplest-way-of-detecting-where-audio-envelopes-start-and-stop

#### Modifications Done to code
- Samples removed from test:
    - 237791__fusarof__door-open2.wav, 237791__fusarof__door-open4.wav - Sampling frequency seems to be less than the 2*highest frequency (22050Hz)
    - 184307__swiftoid__bedroom-door-close.wav, 369620__cribbler__door-closes-int.wav, 331138__fabuafrica__door-close-modern-metal-punch-low-bass-lock-click-interior-room-echo.wav, 242403__noctaro__midsized-dog-bark-02.wav - Sampling frequency is 96KHz and so the sample size is 2227
- FFT size of the feature vector increased to 2048:
    - 1024 fft seems to be 0.0232sec * 44100 is around 1023
    - Since most 'fs' are around 48KHz. So this was truncating the fft. Currently increasing the fft size to 2048
- Some files where mp3 and were converted to wav

#### Results:
- Current Confidence threshold:
    - {'GunShot': 0.25201142465371296, 'DogBark': 0.56000000000000005, 'DoorBell': 0.25201142465371296, 'DoorOpen': 0.78000000000000003, 'DoorClose': 0.76000000000000001, 'FootSteps': 0.25201142465371296 }
- Confidence Coefficients: [1/Confidence threshold]
    - {'GunShot': 3.9680740719357965, 'DogBark': 1.7857142857142856, 'DoorBell': 3.9680740719357965, 'DoorOpen': 1.282051282051282, 'DoorClose': 1.3157894736842106, 'FootSteps': 3.9680740719357965}
- For the total 67 test files the Actual Pass fail results are:
    - {'GunShot': 2/9, 'DogBark': 18/21, 'DoorBell': 0/4, 'DoorOpen': 1/9, 'DoorClose': 20/20, 'FootSteps': 0/4}
- Class Spred used for training:
    - {'GunShot': 37, 'DogBark': 88, 'DoorBell': 19, 'DoorOpen': 41, 'DoorClose': 83, 'FootSteps': 17}

#### Sound Feature and Score Understanding:
- [Mel Frequency Cepstral Coefficients](http://www.practicalcryptography.com/miscellaneous/machine-learning/guide-mel-frequency-cepstral-coefficients-mfccs/)
    - Suggest using only bottom 12-13 bands rther than the entire 26 filters
    - Wrong understanding uses 40 filters of which 26 coefficients are taken so seems right
    - No delta-delta features are generated
    - nfft = 1024 may be restricting the numsamples calculated using the mfcc window dimension 0.026 sec and sampleing frequency of 48000 or 41000
    - num samples are 1248 for 48KHz and 0.026 and 1066 for 41KHz
- [Python Speech Features](https://github.com/jameslyons/python_speech_features)
- Calculating Confidence threshold:
    - mask_wrong = (df.class_predicted == true_positive_class) & (df.class_expected != true_positive_class)  # FALSE POSITIVE
    - The probability threshold after which the predicted class is always equal to the expeted class and not a false positive
    - This is calculated over the stratified fold for test,train features 
    - 1/(probability threshold) is the confidence threshold
    - In the test phase, the predicted probability for a particular class along with the score. The larger the score the better the predicted class for that particular time interval. It seems to normalise the value across the classes since it is the min probability value for which we have no false positive and 1/probability of this value is the confidence threshold. 
    - So higher the probability and smaller the threshold the product is a very high score and so it is high probability for that class
    - Larger probability is required when the threshold is high probability for it to have that particular class

#### Pitfalls
- Docker image does not work outof the box. Probably because the python module fails to be identified. 
- Use latest version of libsnffile on MAC. libsndfile-1.0.27.tar.gz
- The features not found issue. python_speech_features has been updated to new version. Use python_speech_features instead of feature module
- pytest on mac may require a uninstall and install. <http://stackoverflow.com/questions/35998992/py-test-command-not-found-but-library-is-installed/36006909>



#### Classifier Understanding:
- [Support Vector Machines](http://scikit-learn.org/stable/modules/svm.html)
- [SVM Classifier](http://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html)
- [RBF - Radial Basis Functions](http://scikit-learn.org/stable/auto_examples/svm/plot_rbf_parameters.html)

#### Understanding Scikit Learn Function
- [SklearnPandas](https://github.com/paulgb/sklearn-pandas)
- [DictVectorizer](http://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.DictVectorizer.html)
    - Converting Panda dataframes in form of Dictionary features into numpy arrays used for scikit learn
- [StandardScaler](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html)
    - Scaling and normalising input for mean and std deviation (0,1)
- [StratifiedKFold](http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.StratifiedKFold.html)
    - The folds are made by preserving the percentage of samples for each class.


#### Things to understand
- [Cepstrum and LPCC](http://www.practicalcryptography.com/miscellaneous/machine-learning/tutorial-cepstrum-and-lpccs/)
- [HMM Tutorial](http://practicalcryptography.com/miscellaneous/machine-learning/hidden-markov-model-hmm-tutorial/)
- https://github.com/jameslyons/python_speech_features

#### References:
- [Protolab Sound Recognition](https://github.com/laurent-george/protolab_sound_recognition)
- [libsndfile](http://www.mega-nerd.com/libsndfile/files/)
- [python_speech_features](https://github.com/jameslyons/python_speech_features)
- [List dependent child images](http://stackoverflow.com/questions/36584122/docker-how-can-i-get-the-list-of-dependent-child-images)


