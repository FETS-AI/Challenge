---
title: FAQ
permalink: /faq/
---

## Table of contents
* [What is the main website for the challenge?](#what-is-the-main-website-for-the-challenge)
* [How do I register for the challenge?](#how-do-i-register-for-the-challenge)
* [How do I obtain the data for the challenge?](#how-do-i-obtain-the-data-for-the-challenge)
* [Can I use additional data for model development?](#can-i-use-additional-data-for-model-development?)
* [What is the data citation?](#what-is-the-data-citation)
* [Why am I facing issues when using NVIDIA Ampere cards?](#why-am-i-facing-issues-when-using-nvidia-ampere-cards)
* [How can I ensure the predictions are in the same space as the input?](#how-can-i-ensure-the-predictions-are-in-the-same-space-as-the-input)
* [Where can I ask more questions?](#where-can-I-ask-more-questions)

## What is the main website for the challenge?

You are on the main website right now. Additionally, participants may follow the our [Twitter account](https://twitter.com/FeTS_Challenge) for updates and visit the [challenge repo](https://github.com/FETS-AI/Challenge).

## How do I register for the challenge?

This is described on the [participation page](participate.md/#registration-and-data-access).

## How do I obtain the data for the challenge?

This is described on the [participation page](participate.md/#registration-and-data-access).

## Can I use additional data for model development?

No. Participants are NOT allowed to use additional public and/or private data (from their own institutions) for extending the provided data. Similarly, using models that were pretrained on such datasets is NOT allowed. This is due to our intentions to provide a fair comparison among the participating methods.

## Why am I facing issues when using NVIDIA Ampere cards?

Please use PyTorch installation which is specific [to CUDA 11](https://pytorch.org/get-started/locally/). See [this issue](https://github.com/FETS-AI/Challenge/issues/42) for details.

## What is the data citation?

Please cite the following papers when using data from this challenge:

```bibtex
@misc{pati2021federated,
      title={The Federated Tumor Segmentation (FeTS) Challenge}, 
      author={Sarthak Pati and Ujjwal Baid and Maximilian Zenk and Brandon Edwards and Micah Sheller and G. Anthony Reina and Patrick Foley and Alexey Gruzdev and Jason Martin and Shadi Albarqouni and Yong Chen and Russell Taki Shinohara and Annika Reinke and David Zimmerer and John B. Freymann and Justin S. Kirby and Christos Davatzikos and Rivka R. Colen and Aikaterini Kotrotsou and Daniel Marcus and Mikhail Milchenko and Arash Nazer and Hassan Fathallah-Shaykh and Roland Wiest Andras Jakab and Marc-Andre Weber and Abhishek Mahajan and Lena Maier-Hein and Jens Kleesiek and Bjoern Menze and Klaus Maier-Hein and Spyridon Bakas},
      year={2021},
      eprint={2105.05874},
      archivePrefix={arXiv},
      primaryClass={eess.IV}
}
@article{sheller2020federated,
  title={Federated learning in medicine: facilitating multi-institutional collaborations without sharing patient data},
  author={Sheller, Micah J and Edwards, Brandon and Reina, G Anthony and Martin, Jason and Pati, Sarthak and Kotrotsou, Aikaterini and Milchenko, Mikhail and Xu, Weilin and Marcus, Daniel and Colen, Rivka R and others},
  journal={Scientific reports},
  volume={10},
  number={1},
  pages={1--12},
  year={2020},
  publisher={Nature Publishing Group}
}
@article{bakas2017advancing,
  title={Advancing the cancer genome atlas glioma MRI collections with expert segmentation labels and radiomic features},
  author={Bakas, Spyridon and Akbari, Hamed and Sotiras, Aristeidis and Bilello, Michel and Rozycki, Martin and Kirby, Justin S and Freymann, John B and Farahani, Keyvan and Davatzikos, Christos},
  journal={Scientific data},
  volume={4},
  number={1},
  pages={1--13},
  year={2017},
  publisher={Nature Publishing Group}
}
```

In addition, if there are no restrictions imposed from the journal/conference you submit your paper, please be specific and also cite the following:

```bibtex
@article{bakas2017segmentation,
  title={Segmentation labels and radiomic features for the pre-operative scans of the TCGA-LGG collection},
  author={Bakas, Spyridon and Akbari, Hamed and Sotiras, Aristeidis and Bilello, Michel and Rozycki, Martin and Kirby, Justin and Freymann, John and Farahani, Keyvan and Davatzikos, Christos},
  journal={The cancer imaging archive},
  volume={286},
  year={2017}
}
```

## How can I ensure the predictions are in the same space as the input?

Please follow these instructions [[ref](https://gist.github.com/sarthakpati/73c8ffd7586e715680f3679a791bbec3)]:
```python
import SimpleITK as sitk

# read image from where information is to be copied
inputImage = sitk.ReadImage('/path/to/input.nii.gz')

# get result in the form of a numpy array
npa_res = my_algorithm( # my_algorithm does something fancy with a numpy array
                  sitk.GetArrayFromImage(inputImage) # get array from image
            ) 

# Converting back to SimpleITK 
# (assumes we didn't move the image in space as we copy the information from the original)
result_image = sitk.GetImageFromArray(npa_res)
result_image.CopyInformation(inputImage)

# write the image, and this will have same information as inputImage
sitk.WriteImage(result_image, '/path/to/result.nii.gz')
```

## Where can I ask more questions?

You can get in touch with the organizers via the following mechanisms:
- Either use the [discussion forum](https://github.com/FETS-AI/Challenge/discussions), where you can get help from the organizers and other participants.
- If you do not want to discuss your issue publicly, send us an email to: [challenge@fets.ai](mailto:challenge@fets.ai).
