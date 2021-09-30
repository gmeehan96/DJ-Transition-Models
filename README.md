# DJ Transition Models
This repository contains the code for a DJ transition labelling system. An important part of producing smooth DJ transitions is ensuring that the outgoing and incoming song are phrase-matched, as this maintains the musical structure of the mix. The aim of this project is to build an end-to-end system which, given an MP3 file of a song as input, can label appropriate transition points in the song which will allow phrase-matched blended transitions to be produced programmatically.

Using a library of 1,146 EDM MP3 files from the author's personal collection (mainly sourced from DJ record pools), the notebooks in this repository train deep learning models which leverage the rigid gridded beat structure of EDM to identify phrase and downbeat locations, along with appropriate transition points in the introduction and outro of each song. The input to the models are the song's Mel Spectrogram and Chromagram, and the models are trained using manual labels of appropriate transition points. These labels were produced iteratively: after the first 200 songs were labelled, the models were then trained to produce initial predictions, which were manually corrected and used to train the models again, and so on. The [TransitionModels SoundCloud page](https://soundcloud.com/user-552039305) contains several examples of how the resulting labels can be used to produce DJ mixes with smooth transitions. The tracklists for most of these examples, found in [this playlist](https://soundcloud.com/user-552039305/sets/tracklist-generator-examples), were created using our [Tracklist Generator](https://github.com/gmeehan96/tracklist-generator), restricted to the population of labelled MP3s. 
## Code
This repository contains three notebooks which outline the steps taken to produce the model inputs and train the Intro/Outro models.
- The [Data Preparation notebook](https://github.com/gmeehan96/DJ-Transition-Models/blob/main/1.%20Data%20Preparation.ipynb) describes in detail the manual labelling process and how these labels can be used to programmatically create smooth transitions. It also outlines how the audio features were extracted from the MP3 file for each song.
- The [Introduction Models notebook](https://github.com/gmeehan96/DJ-Transition-Models/blob/main/2.%20Introduction%20Transition%20Models.ipynb) trains three models which, taken together, constitute a pipeline which produces labels of appropriate transition points at the beginning of a song. The models use 1D convolution and an LSTM on the Mel Spectrogram/Chromagram input to predict several key features of the structure of the song's introduction. The resulting process produces labels which match the manual labels either exactly or very closely in 67 out of 100 songs in the test set.
- The [Outro Models notebook](https://github.com/gmeehan96/DJ-Transition-Models/blob/main/3.%20Outro%20Transition%20Models.ipynb) follows a similar approach and model architecture to the Introduction Models, although the logic of the pipeline is slightly different. The labelling task in the outro is more difficult because the beginning of the song is not as reliable an anchor point for prediction. 57 out of 100 songs in the test set are labelled with high-quality outro transition timings. 

If you have any questions or comments, please get in touch via email to gregor.meehan at gmail.com.
