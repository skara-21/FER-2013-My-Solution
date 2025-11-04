# FER-2013 Systematic Study

## Project Description

In this project, I conducted research on facial emotion recognition using the FER-2013 dataset. 
I divided the research into three parts. In each part, I investigated the impact of different architectures on the model's final performance.

## Project Structure

Assignment-4

├── phase1-depth-study/          # Phase 1: depth study         
│   ├── 2layer-baseline         
│   ├── 4layer-baseline         
│   ├── 6layer-baseline         
│   └── 8layer-baseline         
├── phase2-skip-connections/     # Phase 2: skip connections study         
│   ├── 6layer-standard-cnn         
│   ├── 6layer-skip-connections-cnn         
│   ├── 6layer-hybrid-skip-connections-cnn          
│   └── 6layer-dense-connections-cnn         
├── phase3-regularization/       # Phase 3: regularization study         
│   ├── best-arch-no-reg        
│   ├── best-arch-dropout       
│   ├── best-arch-batchnorm     
│   └── best-arch-both          
└── model-inference/            # Model evaluation on test set


## Research Phases

### Phase 1: Depth Study
At this stage, I observed the impact of neural network depth on model effectiveness:
### Expectation: The 4-layer model would achieve the best results

- **2-layer model**: Was highly underfitted
- **4-layer model**: Showed improvement
- **6-layer model**: Proved to have the best results
- **8-layer model**: Was overfitted

**Result**: The 6-layer model was the most optimal.



### Phase 2: Skip Connections Study
To improve the best architecture identified in the previous experiment, I tried different variants:
### Expectation: The hybrid skip connection model would achieve the best results

- **Standard 6-layer**: Used as baseline to make the relative results of other models easier to see
- **skip-connections-cnn**: The model already showed improvement
- **hybrid-skip-connections-cnn**: Although there wasn't significant improvement in validation accuracy, this model was less overfitted than the previous one
- **dense-connections-cnn**: This model showed the best results in terms of overfitting, though the hybrid was better in terms of accuracy

**Result**: I moved to the next stage with the 6-layer hybrid skip connection architecture.
It should be noted that all models in this phase were overfitted.



### Phase 3: Regularization Techniques
Considering the previous experiments, I moved to testing different regularization techniques, hoping that one of them would improve the overfitting score:
### Expectation: The batch normalization model would achieve the best results

- **Without regularization**: Used as baseline to make the relative results of other models easier to see
- **Dropout**: The model learned that regularization techniques were engaged :)
- **Batch Normalization**: This architecture increased both the model's accuracy on the validation set and reduced the overfitting score
- **Dropout+Batch Normalization**: Since the regularization methods worked individually, it wasn't surprising that their combination would produce good results

**Result**: The Batch Normalization model was the most accurate, though Dropout+Batch Normalization had better results in reducing overfitting, and its accuracy was comparable to the first (Batch Normalization-66.07% while Dropout+Batch Normalization-65.73%), so I decided to use this model for final predictions.

## Data

The **FER-2013** (Facial Expression Recognition 2013) dataset contains:
- 35,887 48x48 images
- Divided into 7 emotional classes:
  - Angry
  - Disgust
  - Fear
  - Happy
  - Sad
  - Surprise
  - Neutral


- It is known that recognizing the Disgust emotion is difficult in this dataset because its proportion is (1.3%)
My best model achieved the following results:
| Emotion | Recall | Samples |
|---------|--------|---------|
| Fear    | 0.310  | 496     |
| Disgust | 0.411  | 56      |
| Angry   | 0.559  | 467     |



### Wandb Reports

#### Phase 1: Depth Study
- **Comparative Depth Analysis**: [Depth Study](https://wandb.ai/skara21-free-university-of-tbilisi-/fer-2013-depth-study/reports/Depth-Study-Report--VmlldzoxMzEwODk3NQ?accessToken=7917x675zw2b6iisbx2h34c7zrtbm9v9g5mc7uqwdcfv7u8jp14xauvl7zy9zaio)

#### Phase 2: Skip Connections Study
- **Skip Connections Comparison**: [Skip Connections Study](https://wandb.ai/skara21-free-university-of-tbilisi-/fer-2013-connections-study/reports/Connection-Study-Report--VmlldzoxMzEwOTE0NA?accessToken=3ilnyff5qfc57lz6u55udqemqxz0paf3t42xgpjvba1eo2i095pqps2yte854q8o)

#### Phase 3: Regularization Techniques
- **Regularization Comparison**: [Regularization Study](https://wandb.ai/skara21-free-university-of-tbilisi-/fer-2013-regularization-study/reports/Regularization-Study-Report--VmlldzoxMzEwOTE5Ng?accessToken=qup21w5fth6fygyn7z7kzweidzch15k85df1sst83405no6cvi6eyc8g5cygn4qu)


### Conclusions:

1. **Optimal Depth**: 6 layers

2. **Skip Connections**: Hybrid Skip Connections CNN

3. **Regularization**: Batch Normalization + Dropout

### Metrics:
- **Accuracy**: **0.6397**
- **F1-Score**: **59%**
- **Precision**: **63%**
- **Recall**: **64%**


#### Detailed Results by Class:
| Emotion | Precision | Recall | F1-Score | Samples |
|--------|-----------|--------|----------|----------|
| Angry | 0.58 | 0.56 | 0.57 | 467 |
| Disgust | 0.50 | 0.41 | 0.45 | 56 |
| Fear | 0.46 | 0.31 | 0.37 | 496 |
| Happy | 0.83 | 0.86 | 0.85 | 895 |
| Sad | 0.51 | 0.57 | 0.54 | 653 |
| Surprise | 0.76 | 0.82 | 0.79 | 415 |
| Neutral | 0.57 | 0.61 | 0.59 | 607 |


- **Best Performance**: Happy, because it has the most samples
- **Weakest Performance**: Fear, often confused with anger and sadness
- **Impact of Class Imbalance**: Disgust performs poorly, most likely because it only has 56 samples


#### Notes: 
- When uploading to GitHub, I removed the dataset because it was very large and I didn't want to work with LFS files
