# HABC: Stress, Affect, and Activity Recognition

This repository contains work from our B.Tech project on classifying human stress, affect, cognitive load, and physical activity from wearable and multimodal sensor data.

We developed the **Hybrid Attention-Based CNN-BiLSTM Classifier (HABC)**, a parallel deep-learning architecture that learns local signal patterns and long-range temporal dependencies at the same time. The project was evaluated across four public datasets covering physiological signals, emotion, cognitive load, and human activity.

> This is a team project completed at ABV-IIITM Gwalior under the supervision of Dr. Anjali.

## Why this project?

Wearable sensors make continuous mental-health and activity monitoring possible, but their signals are noisy, multimodal, and highly dependent on context. A reliable system must learn both:

- **Spatial features**, such as localized waveform patterns in ECG or rapid changes in EDA.
- **Temporal features**, such as how heart rate, respiration, or motion evolves over time.

It must also distinguish psychological stress from physical exertion, since both can produce similar physiological responses.

## Model architecture

HABC processes every input through two parallel branches:

1. **CNN branch** - extracts localized and morphological signal features.
2. **BiLSTM + Attention branch** - captures bidirectional temporal dependencies and gives greater weight to informative time steps.
3. **Feature fusion** - concatenates the representations learned by both branches.
4. **Classifier** - maps the fused representation to the target classes.

The parallel design preserves temporal information that can be weakened when convolution and recurrent layers are arranged sequentially.

## Datasets

| Dataset | Task | Modalities / context |
| --- | --- | --- |
| WESAD | Baseline, stress, and amusement classification | Wearable physiological signals including ECG, EDA, respiration, and acceleration |
| MUSE | Low, medium, and high valence classification | Multimodal stressed-emotion data |
| SWELL-KW | Neutral, interruption, and time-pressure classification | Cognitive load and HRV in an office setting |
| UTD-MHAD | 27-class human action recognition | Accelerometer and multimodal activity data covering 27 physical actions |

UTD-MHAD was included to test whether the model could recognize a wide range of physical actions and help separate physical exertion from psychological arousal, reducing stress-related false positives in more realistic settings.

## Results

| Dataset | Accuracy | Precision | Recall | F1-score |
| --- | ---: | ---: | ---: | ---: |
| WESAD | 96.63% | 96.00% | 96.00% | 96.00% |
| MUSE | 95.29% | 95.00% | 95.00% | 95.00% |
| SWELL-KW | 98.78% | 99.00% | 99.00% | 99.00% |
| UTD-MHAD | 93.33% | - | - | - |

The results show that the same architectural idea can generalize across stress detection, affect recognition, cognitive-load classification, and physical-activity recognition.

### UTD-MHAD result

The CNN-BiLSTM with Attention model achieved **93.33% accuracy on the complete 27-class UTD-MHAD human-action recognition task**. The confusion matrix showed a strong diagonal across the action classes, indicating that the model learned discriminative patterns for different forms of physical activity.

This experiment addressed an important practical challenge in stress monitoring: physical exertion can produce physiological responses similar to psychological stress. Recognizing physical actions helps a future stress-monitoring system avoid treating activity-induced arousal as a stress event.

The final presentation reports accuracy for this experiment but does not provide aggregate precision, recall, or F1-score, so those values are intentionally left unreported above.

## Technology

- Python
- TensorFlow and Keras
- Scikit-learn
- NumPy and Pandas
- Matplotlib
- Jupyter Notebook

## Repository contents

- `Copy_of_BTP_UTD.ipynb` - preprocessing, model construction, training, and evaluation for the UTD-MHAD experiment.
- `utd (2)/utd/` - UTD-MHAD skeleton samples and prepared datasets used by the notebook.

## Getting started

1. Clone the repository:

   ```bash
   git clone https://github.com/Jasleenxddd/Stress_detection_model.git
   cd Stress_detection_model
   ```

2. Create an environment and install the core dependencies:

   ```bash
   pip install tensorflow keras scikit-learn numpy pandas matplotlib scipy jupyter
   ```

3. Start Jupyter Notebook:

   ```bash
   jupyter notebook
   ```

4. Open `Copy_of_BTP_UTD.ipynb` and update dataset paths if required before running the cells.

## Limitations

- Performance can decline as the proportion of missing sensor values increases.
- The full study should be extended to more datasets and wearable-sensor modalities.
- Real-world deployment requires additional validation across unseen users, devices, and noisy environments.
- This repository currently focuses on the UTD-MHAD implementation; the report covers the broader four-dataset evaluation.

## Future work

- Apply attention to CNN features or after feature fusion.
- Explore alternative dense-layer activation functions.
- Improve robustness to missing values and motion artifacts.
- Evaluate additional modalities such as PPG, blood pressure, and accelerometer signals.
- Validate subject-independent generalization for practical wearable deployment.

## Team

- Aswad Kulkarni (2022IMG017)
- Jasleen Kaur (2022IMG025)
- Prashant Sharma (2022IMG048)
- Yash Padme (2022IMG069)

**Supervisor:** Dr. Anjali, Department of Information Technology, ABV-IIITM Gwalior.

## Responsible use

This project is intended for research and educational use. It is not a medical diagnostic system and should not be used as a substitute for professional healthcare advice.
