---
layout: post
title:  "Callhome diarization recipe using x-vectors"
date:   2018-05-04 00:14:28 -0400
---

TODO

Pretrained Model
--------
Pretrained model to be uploaded on [kaldi-asr.org][pretrained-model]{:target="_blank"}.


# Files list

```
 ./
     README.txt               This file
     run.sh                   The recipe that was in egs/callhome_diarization/v2/run.sh

 local/nnet3/xvector/tuning/
     run_xvector_1a.sh        Generated the configs, egs, and trained the model

 conf/
     vad.conf                 Energy VAD configration
     mfcc.conf                MFCC configuration

 exp/xvector_nnet_1a/
     final.raw                The pretrained model
     nnet.config              An nnet3 config file for instantiating the model
     extract.config           An nnet3 config file for extracting xvectors
     min_chunk_size           Min chunk size used (see extract_xvectors.sh)
     max_chunk_size           Max chunk size used (see extract_xvectors.sh)
     srand                    The RNG seed used

 exp/xvectors_callhome1/
     mean.vec                 Vector for centering, from callhome1
     transform.mat            Whitening matrix, trained on callhome1
     plda                     PLDA model for callhome1, trained on SRE data

 exp/xvectors_callhome2/
     mean.vec                 Vector for centering, from callhome2
     transform.mat            Whitening matrix, trained on callhome2
     plda                     PLDA model for callhome1, trained on SRE data
```
# Training Data

The xvector DNN was trained on the following corpora:

```
     Corpus              LDC Catalog No.

     SRE2004             LDC2006S44
     SRE2005 Train       LDC2011S01
     SRE2005 Test        LDC2011S04
     SRE2006 Train       LDC2011S09
     SRE2006 Test 1      LDC2011S10
     SRE2006 Test 2      LDC2012S01
     SRE2008 Train       LDC2011S05
     SRE2008 Test        LDC2011S08
     SWBD2 Phase 2       LDC99S79
     SWBD2 Phase 3       LDC2002S06
     SWBD Cellular 1     LDC2001S13
     SWBD Cellular 2     LDC2004S07

 The following datasets were used in data augmentation.

     MUSAN               http://www.openslr.org/17
     RIR_NOISES          http://www.openslr.org/28
```

# Results

The models should produce results similar to the following on Callhome.
The acoustic ivector system is included for reference (see egs/callhome_diarization/v1).
```
  xvector              DER: 8.39% with supervised calibration, 7.12% with oracle number of speakers
  ivector (from ../v1) DER: 10.36% with supervised calibration, 8.69% with oracle number of speakers
```


# Citation

 If you want to use the pretrained model in a paper, please cite as:

```
@inproceedings{snyder2018xvector,
  title={X-vectors: Robust DNN Embeddings for Speaker Recognition},
  author={Snyder, D. and Garcia-Romero, D. and Sell, G. and Povey, D. and Khudanpur, S.},
  booktitle={2018 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)},
  year={2018},
  organization={IEEE},
  url={http://www.danielpovey.com/files/2018_icassp_xvectors.pdf}
}
```

[kaldi]: http://kaldi-asr.org/
[callhome_diarization_v1]: https://github.com/kaldi-asr/kaldi/tree/master/egs/callhome_diarization/v1 
[callhome_diarization_v2]: https://github.com/kaldi-asr/kaldi/tree/master/egs/callhome_diarization/v2
[xvector-pr]: https://github.com/kaldi-asr/kaldi/pull/2391
[ICASSP2018]: http://www.danielpovey.com/files/2018_icassp_xvectors.pdf
[xvector-pr]: https://github.com/kaldi-asr/kaldi/pull/1896/
[pretrained-model]: http://kaldi-asr.org/models.html
[commit-id]: https://github.com/kaldi-asr/kaldi/commit/080129e97a7effccc48a2234b1fc9f511ce52d57
