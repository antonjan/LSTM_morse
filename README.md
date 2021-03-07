# LSTM_morse

More details in the blog. 
See http://ag1le.blogspot.com/2017/11/tensorflow-revisited-new-lstm-dynamic.html

You can clone this repo by 

```
git clone https://github.com/ag1le/LSTM_morse.git
```

Create virtual environment by: 

```
virtualenv venv
```

Activate virtualenv 

```
. venv/bin/activate
```

Install dependencies by 

```
pip install -r requirements.txt

#  Software and Instructions
The initial version of the software is available in Github - see here

Using from the command line:

python MorseDecoder.py -h
usage: MorseDecoder.py [-h] [--train] [--validate] [--generate] [-f FILE]

optional arguments:
  -h, --help  show this help message and exit
  --train     train the NN
  --validate  validate the NN
  --generate  generate a Morse dataset of random words
  -f FILE     input audio file


To get started you need to generate audio training material. The count variable in model.yaml config file tells how many samples will get generated. Default is 5000.

python MorseDecoder.py --generate


Next you need to perform the training. You need to have "audio/", "image/" and "model/" subdirectories on the folder you are running the program.

python MorseDecoder.py --train


Last this to do is to validate the model:

python MorseDecoder.py --validate

To have the model decode a file you should use:

python MorseDecoder.py -f audio/myfilename.wav 




Config file model.yaml  (first training session):
model:
    # model constants
    batchSize: 100  
    imgSize: !!python/tuple [128,32] 
    maxTextLen: 32
    earlyStopping: 20 

morse:
    fnTrain:    "morsewords.txt"
    fnAudio:    "audio/"
    count:      5000
    SNR_dB:     20
    f_code:     600
    Fs:         8000
    code_speed: 30
    length_N:   65000
    play_sound: False
    word_max_length: 5
    words_in_sample: 2

experiment:
    modelDir:   "model/"
    fnAccuracy: "model/accuracy.txt"
    fnTrain:    "model/morsewords.txt"
    fnInfer:    "model/test.png"
    fnCorpus:   "model/corpus.txt"
    fnCharList: "model/charList.txt"
Config file model.yaml  (second training session):
model:
    # model constants
    batchSize: 100  
    imgSize: !!python/tuple [128,32] 
    maxTextLen: 32
    earlyStopping: 5

morse:
    fnTrain:    "morsewords.txt"
    fnAudio:    "audio/"
    count:      5000
    SNR_dB:     
      - 20
      - 30
      - 40
    f_code:     600
    Fs:         8000
    code_speed: 
      - 30
      - 25
      - 20
    length_N:   65000
    play_sound: False
    word_max_length: 5
    words_in_sample: 1

experiment:
    modelDir:   "model/"
    fnAccuracy: "model/accuracy.txt"
    fnTrain:    "model/morsewords.txt"
    fnInfer:    "model/test.png"
    fnCorpus:   "model/corpus.txt"
    fnCharList: "model/charList.txt"



```
