## Build

``` bash
$ cmake -S . -B build && cmake --build build
```

## Demo

``` bash
$ git clone https://github.com.cnpmjs.org/smallmuou/wavutils
$ wavutils/bin/wav2pcm noisy.wav noisy.pcm
$ build/rnnoise_demo noisy.pcm denoised.pcm
$ wavutils/bin/pcm2wav 1 48000 16 denoised.pcm denoised.wav
```

## Train and Test

### Prepare Data

``` bash
$ wavutils/bin/wav2pcm clean.wav clean.pcm
$ wavutils/bin/wav2pcm noise.wav noise.pcm
$ build/denoise_training clean.pcm noise.pcm 50000 > feats.txt
$ export HDF5_USE_FILE_LOCKING=FALSE
$ python training/bin2hdf5.py feats.txt 50000 87 training.h5
```

### Train

``` bash
$ python training/rnn_train.py
```

### Test

``` bash
$ python training/dump_rnn.py weights.hdf5 src/rnn_data.c src/rnn_data orig
$ cmake --build build
$ build/rnnoise_demo noisy.pcm denoised.pcm
```
