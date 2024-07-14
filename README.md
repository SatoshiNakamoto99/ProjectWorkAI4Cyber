# Artificial Intelligence For Cyber Security Project

This is the Artificial Intelligence for Cyber Security Project of Group 7 composed of:

- Iovaro Damiana: d.iovaro@studenti.unisa.it
- Massaro Sara: s.massaro3@studenti.unisa.it
- Nocerino Antonio: a.nocerino15@studenti.unisa.it
- Trotta Prisco: p.trotta12@studenti.unisa.it

# How to execute

The preparation of the dataset is already done, so is not needed to execute `1. PrepareTestSet.ipynb`, `2. Processing_and_store_MTCNN.ipynb`, `3. Evaluate_NN1.ipynb`, `9. Evaluate_NN2.ipynb`.

These files are present in the directory called `utilities` and in order to not get errors from their execution they have to be moved in the principal directory.

To perform the attacks you have to execute:

- `4. FGSM.ipynb`,
- `5. BIM.ipynb`,
- `6. PGD.ipynb`,
- `7. DeepFool.ipynb`,
- `8. CarliniWagner.ipynb`.

In each of these, to choose to generate attacks on NN1, NN2 or NN1+defense there are variables to set to `True` or `False` when needed, as default are all set to `False`.

To see the SEC you have to execute the `13. Show_results.ipynb` notebook.

# Content

## 1. Prepare Test Set

`1. PrepareTestSet.ipynb`

In this notebook the VGGFace2 csv containing the dataset identities is cleaned from wrong formatted lines.

Then are selected randomly 100 identities used to form the test set used later. For each identity are extracted randomly 1000 images.

## 2. Processing and store images with MTCNN

`2. Processing_and_store_MTCNN.ipynb`

Here the previous extracted images are passed through the MTCNN module in order to follow the preprocessing path used when training the model.

## 3. Evaluate NN1

`3. Evaluate_NN1.ipynb`

Firstly, the pretrained model (InceptionResnetV1) is loaded. Then the LABELS are loaded and the identity selected to test the model are loaded.

In this notebook is defined the class `VGGFace2Dataset` to create the dataset element used to test the model.

Then are defined the functions to evaluate and to make inference on the model.

At the end, the model is evaluated on clean data.

## 4. Evaluate NN2

`9. Evaluate_NN2.ipynb`

Firstly, the pretrained model (Senet50) is loaded. Then the test set is loaded and prepared to be used in evaluating the model on clean data.

This file is in the `utilities` folder.

## 5. Generate adversarial examples

There are in the directory five notebook:

- `4. FGSM.ipynb`,
- `5. BIM.ipynb`,
- `6. PGD.ipynb`,
- `7. DeepFool.ipynb`,
- `8. CarliniWagner.ipynb`.

They have a similar structure descrived below:

- load model NN1,
- load labels of the model,
- load model NN2,
- load and prepare test set for both model,
- evaluate NN1 and NN2 on clean data,
- perform attack on NN1,
- perform attack on NN2,
- perform attack on NN1 with defense.

## 6. Defense

As defense is chosen to add a detector before NN1, thus is firstly prepared the training set.

### Training set

`10. Prepare Detector Train Set.ipynb`
`11. Prepare for detector.ipynb`

From the VGGFace2 dataset are extracted other 1000 identities not used in the test set defined before. For each identity are selected 10 images. Thus, the 10000 images are divided among the five attacks: 2000 for each attack, and for each type of attack (expect for DeepFool) these images are divided 1000 for generating the targeted attacks and 1000 for untargeted attacks. These images are processed with MTCNN module (as done before) and then generated the attacks.

Thus the training set has 10000 clean images and 10000 images adversarial images, obtaining a training set of 20000 images.

These files are in the `utilities` folder.

### Detector

`12. Detector.ipynb`

In this notebook is executed the training of the detector. The detector is a MobileNetV2 pre-trained model to which the last layer was changed to binary classification.

## 7. Show results

`13. Show_results.ipynb`

This notebook shows all the graphs saved in the different csv.
