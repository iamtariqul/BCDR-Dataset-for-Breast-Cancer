## Data set

1. Breast cancer diagnostic images collected from the Popular Diagnostic Center, Savar, Dhaka, Bangladesh. The dataset has been curated to support research in breast cancer detection and classification. It provides a valuable resource for machine learning and medical imaging studies. This dataset aims to facilitate advancements in breast cancer research and empower developers and researchers to create impactful solutions in medical diagnostics. Dataset [(Download)](BCDR_D01%20Dataset/BCDR_D01%20Dataset%20Original.xlsx) that contains 79 biopsy-proven lesions (~150 digital mammograms) of 64 women, rendering 143 segmentations (average of 1.81 images per lesion) including clinical data and image-based descriptors.

2. To obtain the masks (from the outlines provided in the database) you can use [createMasks.m](database_info/createMask/createMask.m). This reads the mammogram info from a couple of files provided in the database: [sample bcdr_d01_img.csv](database_info/createMask/bcdr_d01_img.csv) and [sample bcdr_d01_outlines.csv](database_info/createMask/bcdr_d01_outlines.csv)

   The output should look like this:  
   <img src="database_info/createMask/img_20_30_1_RCC.png" width="250"/> <img src="database_info/createMask/img_20_30_1_RCC_mask.png" width="250"/>

3. Use [prepareDB](code/prepareDB.py) to enhance the contrast of the mammograms and downsample them to have a manageable size (2cmx2cm in the mammogram in 128x128).

   The output looks like this:  
   <img src="database_info/createMask/mammogram_resized.png" width="250" align='center'>

4. Finally you would need to divide the dataset into training, validation, and test patients. You would need to produce a .csv with an image and label filenames as [this](code/example.csv) for each set.

### Training

1. You would need to [install Tensorflow](https://www.tensorflow.org/install/)
2. Run [train](code/train.py) or [train_with_val_split](code/train_with_val_split.py) to train networks. These train the network defined in [model_v3](code/model_v3.py), a fully convolutional network with 10 layers (900K parameters) that uses dilated convolution and is modeled in a ResNet network. Training is done image by image (no batch, but cost is computed in every pixel of the thousand of pixels) and uses dropout among other things
   Note: The code was written for TensorFlow 1.11.0 so it would need to be modified to make work in tf1.0

### Evaluation

1. You can use [compute_metrics](code/compute_metrics.py) or [compute_FROC](code/compute_FROC.py) to compute evaluation metrics or the FROC curve.

You are invited to check the code for more details, I tried to document it nicely.
