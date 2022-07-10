# Understanding Recurrent Neural Networks: Exploring the DeepConvLSTM framework for Human Activity Recognition (HAR)


This is the GitHub page of the repository containing our work project for the Data Science Seminar for the Summer 2022 semester at the University of Siegen. Our work was closely supervised by Marius Bock, and based on his work on Shallow LSTMs (CITE HIS WORK). This repository contains the same code utilised for that work, including specific modifications for our particular needs. The repository our code was based on can be found here: https://github.com/mariusbock/dl-for-har 

The Google Colab notebook in which we run our experiment by analysing the files of this repository can be found here: https://colab.research.google.com/drive/1ETH8zCtEHfxq0vSN9m7zoXKhjaZkTYEe?usp=sharing 

## Abstract
About the use of Deep Learning methods for the detection and prediction of patterns of human activity, known as Human Activity Recognition (HAR). DeepConvLSTM is a popular Deep Learning architecture for HAR data. Our work focuses on investigating the necessity and impact of LSTM layers in evaluating a HAR dataset for a case of climbing stairs and another case focused on floor prediction while climbing stairs. We compare the predictive performance of each case by employing three different types of DeepConvLSTM architecture (0-layers, 1-layer, and 2-layers of LSTMs) with the size of 128 hidden units. Results show that across each evaluation case, the 0-layered model had a better predictive performance in the climbing stairs detections, and the 1-layered model had an overall better predictive performance in the floor prediction case. Based on the findings, we also describe the observed limitations as well opportunities for future research. With our work, we hope to contribute to the discussion on the utility of the DeepConvLSTM framework, by identifying and understanding the strengths and weaknesses of each architecture.

<p align="center">
  <img width="" height="" src="images/architecture.png">
</p>

## Results
Results were obtained on the Wetlab [[4]](#4), RWHAR [[6]](#6), SBHAR [[2]](#2) and HHAR [[5]](#5) dataset using LOSO cross-validation and Opportunity dataset [[3]](#3) using the train-test split as employed in [[1]](#1) averaged across 5 runs using a set of 5 different random seeds.

### Overall results
<p align="center">
  <img width="" height="" src="images/results.png">
</p>

### Standard deviation across runs
<p align="center">
  <img width="" height="" src="images/average_stdev_runs.png">
</p>

### Per-class results

<p align="center">
  <img width="" height="" src="images/per_class_HHAR.png">
</p>

<p align="center">
  <img width="" height="" src="images/per_class_RWHAR.png">
</p>

<p align="center">
  <img width="" height="" src="images/per_class_Wetlab.png">
</p>

<p align="center">
  <img width="" height="" src="images/per_class_sbhar.png">
</p>

<p align="center">
  <img width="" height="" src="images/per_class_opportunity.png">
</p>

## Repo Structure
- log_files: folder containing all log files of experiments mentioned in the paper
- job_scripts: contains files with terminal commands corresponding to the experiments mentioned in the paper
- data_processing: contains file for data processing (analysis, creation, preprocessing and sliding window approach)
- model: folder containing the DeepConvLSTM model, train and evaluation script
- main.py: main script which is to be run in order to commence experiments
- Results.xlsx: excel file containing all expererimental results presented in the paper

## Installing requirements

Please install the required python packages as noted in the ```requirements.txt```. We recommend using ```pip``` by running:

```
pip install -r requirements.txt
```

## Datasets

The datasets (raw and preprocessed data) used during experiments can be either downloaded via this link: 

Only processed dataset: https://uni-siegen.sciebo.de/s/XleBdbYic7ctiXF
Processed + raw data: https://uni-siegen.sciebo.de/s/J9AjZL2g30fPh6c

PW: iswc21

The datasets need to be put in a seperate '/data' directory within the main directory of the repository in order for the main.py script to work.

### Dataset creation

In order to (re-)create the datasets used within these experiments, please additionally install the modified version of ```PyAV``` by Philipp Scholl (https://github.com/pscholl/PyAV). 

- For Linux: 
```
cd data_processing
git clone https://github.com/pscholl/PyAV
sudo apt-get install libx264-dev
sudo apt-get install libavformat-dev
sudo apt-get install libavdevice-dev
cd PyAV
./scripts/build-deps
make
```

Once installed, you can run the ```dataset_creation.py``` file within the ```data_processing``` directory and it will create all relevant datasets and save them to the ```data``` directory within the root directory of this project.

## (Re-)running experiments

To run experiments one can either modify the main.py file (see hyperparameter settings in the beginning of the file or run the script via terminal and giving necessary hyperparameters via flags. See the main.py file for all possible hyperparameters which can be used. All terminal commands used during our experiments can be found in the corresponding job script file in the job_scripts folder. 

## Available log files of experiments

Note that within the log files accuracy, precision, recall and F1-score inbetween epochs were calculated using a 'weighted' and not 'macro' approach (see https://scikit-learn.org/stable/modules/generated/sklearn.metrics.f1_score.html for the difference between the two). Note that thus temporary results will be different if re-run, but final results will still be the same as reported in our publication.

## Results file

The results excel sheet (results.xlsx) contains all results mentioned within the paper and GitHub as well as aggregated information about the standard deviation across runs, per-class results and standard deviation across subjects.

## Citation
<a id="cite">Cite this work as: </a><br/> 
Marius Bock, Alexander Hölzemann, Michael Moeller, and Kristof Van Laerhoven. 2021. Improving Deep Learning for HAR with shallow LSTMs. In 2021 International Symposium on Wearable Computers (ISWC ’21), September 21–26, 2021, Virtual, USA. ACM, New York, NY, USA, 6 pages. https://doi.org/10.1145/3460421.3480419

## Dataset References
<a id="1">[1]</a> 
Francisco Javier Ordóñez and Daniel Roggen. 2016. 
Deep Convolutional and LSTM Recurrent Neural Networks for Multimodal Wearable Activity Recognition.
Sensors16, 1 (2016).  https://doi.org/10.3390/s16010115

<a id="2">[2]</a> 
Jorge-L. Reyes-Ortiz, Luca Oneto, Albert Samà, Xavier Parra, and Davide Anguita. 2016. Transition-Aware Human Activity Recognition Using Smartphoneson-Body Localization of Wearable Devices: An Investigation of Position-Aware ActivityRecognition. Neurocomputing 171 (2016), 754–767.    https://doi.org/10.1016/j.neucom.2015.07.085

<a id="3">[3]</a> 
Daniel Roggen, Alberto Calatroni, Mirco Rossi, Thomas Holleczek, Kilian Förster,Gerhard Tröster, Paul Lukowicz, David Bannach, Gerald Pirkl, Alois Ferscha, Jakob Doppler, Clemens Holzmann, Marc Kurz, Gerald Holl, Ricardo Chavarriaga, Hesam Sagha, Hamidreza Bayati, Marco Creatura, and José del R. Millàn. 2010. Collecting Complex Activity Datasets in Highly Rich Networked Sensor Environments. In 7th International Conference on Networked Sensing Systems. 233-240. https://doi.org/10.1109/INSS.2010.5573462

<a id="4">[4]</a> 
Philipp M. Scholl, Matthias Wille, and Kristof Van Laerhoven. 2015. Wearables in the Wet Lab: A Laboratory System for Capturing and Guiding Experiments. 589–599.  https://doi.org/10.1145/2750858.2807547

<a id="5">[5]</a> 
Allan Stisen, Henrik Blunck, Sourav Bhattacharya, Thor S. Prentow, Mikkel B.Kjærgaard, Anind Dey, Tobias Sonne, and Mads M. Jensen. 2015. Smart Devices are Different: Assessing and Mitigating Mobile Sensing Heterogeneities for Activity Recognition. In Proceedings of the 13th ACM Conference on Embedded Networked Sensor Systems. 127–140. https://doi.org/10.1145/2809695.2809718

<a id="6">[6]</a> 
Timo Sztyler and Heiner Stuckenschmidt. 2016. On-Body Localization of Wearable Devices: An Investigation of Position-Aware Activity Recognition. In IEEE International Conference on Pervasive Computing and Communications. 1–9. https://doi.org/10.1109/PERCOM.2016.7456521
  
