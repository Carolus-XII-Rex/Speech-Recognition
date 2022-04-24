# Speech-Recognition
DNN that allows to recognize digits from audio records  
A link to the code at Jupyter nbviewer: https://nbviewer.org/github/Carolus-XII-Rex/Speech-Recognition/blob/master/AudioRecognition.ipynb (allows to see the IPython widgets)  


## Tasking

This is an academic assignment completed by me during the study at Lomonosov Moscow State University.  
This is the design situation: given audio records of digits pronounced by different people, a list of “telephone numbers” must be recognized. 
A “telephone number” consists of 10 random digits recorded in one audio file.
The algorithm can be split into two parts: 
 1. Feature extraction
 2. Applying the model (Dense neural network)  
  
  
The Data folder contains Train and Test folders. The former contains “0” - “9” with the records of corresponding digits whereas the latter - audio files with “telephone numbers” to be recognized.
The prediction of the model had to be uploaded into the evaluating system. Thus only metrics for validation are available. 

## Algorithm description
 1. Feature extraction. We will use *librosa* library to extract the following features:  
- RMS for each frame: [librosa.feature.rms](https://librosa.org/doc/0.9.1/generated/librosa.feature.rms.html#librosa.feature.rms)
- Chromagram: [librosa.feature.chroma_stft](https://librosa.org/doc/0.9.1/generated/librosa.feature.chroma_stft.html#librosa.feature.chroma_stft)
- Spectral centroid: [librosa.feature.spectral_centroid](https://librosa.org/doc/0.9.1/generated/librosa.feature.spectral_centroid.html)
- Second-order spectral bandwidth: [librosa.feature.spectral_bandwidth](https://librosa.org/doc/0.9.1/generated/librosa.feature.spectral_bandwidth.html#librosa.feature.spectral_bandwidth)
- Roll-off frequency: [librosa.feature.spectral_rolloff](https://librosa.org/doc/0.9.1/generated/librosa.feature.spectral_rolloff.html)
- Zero-crossing rate: [librosa.feature.zero_crossing_rate](https://librosa.org/doc/0.9.1/generated/librosa.feature.zero_crossing_rate.html#librosa.feature.zero_crossing_rate)
- Mel-frequency cepstral coefficients: [librosa.feature.mfcc](https://librosa.org/doc/0.9.1/generated/librosa.feature.mfcc.html)

 3. After training the model there still is a problem before it can be applied to testing data. The models are trained to recognize a single digit, whereas the test dataset contains “telephone numbers” of 10 digits in one file. In order to solve it with the help of *pydub* library we split the “telephone number” using silence detection. Two parameters are concerned: the minimal silence length and silence threshold. There are chosen via grid search. After that, the separated fragments are used to make predictions.  

