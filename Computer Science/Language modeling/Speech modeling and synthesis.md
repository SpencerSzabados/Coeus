Speech modeling, whether it be automatic speech recognition (ASR) used for transcribing spoken words or text-to-speech (TTS) for performing the reverse, is closely related to the topic of [[Natural language processing]].

# Problems in speech modeling
## Bandwidth extension
The problem of bandwidth extension is to fill-in missing portions of an audio (or other spectra) based on available information, with the goal of increasing the fidelity of the signal ("signal upsampling").

In [[@Peharz_2014]] the authors utilise [[Sum-product networks]] to fill in missing frequency bands in speech audio spectra (log shot-time spectra) in combination with a [[Markov chains|hidden Markov model]] (HMM) which is used to model the temporal evolution of the spectra. At the time of writing the authors say the method is not suitable for real-time application, as the model took 1-2mins to process a single utterance (not much slower than other sate-of-the-art performant methods at the time).


https://en.wikipedia.org/wiki/Speech_synthesis#Deep_learning-based_synthesis

# Neural network models 
https://machinelearning.apple.com/research/siri-voices