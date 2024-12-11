# HUMAN ACTION RECOGNITION USING SPOOF DETECTION

This project focuses on Human Action Recognition (HAR) and anti-spoofing, leveraging advanced video processing techniques. It offers users the flexibility to either record videos directly within the application or upload pre-recorded videos for both training and evaluation purposes.The system tracks body pose, face, and hand landmarks to detect and classify human actions. Additionally, it integrates a robust pre-trained anti-spoofing module, designed to effectively identify and prevent video-based spoofing attempts, maintaining the system’s security.The incorporation of real-time audio feedback provides immediate announcements of detected actions, making the experience more interactive and engaging for the user.
## Main Features:
1. Human body landmarks, including facial, hand, and pose coordinates, are extracted from video frames and recorded in a CSV file.  
2. The HAR model is trained utilizing these landmarks to recognize and categorize various human actions.  
3. The anti-spoofing model analyzes video frames to identify discrepancies in the facial, pose, and hand landmarks.  
4. Labels of actions predicted by the model are the corresponding probabilities are displayed on the screen.  
5. Real-time audio feedback is provided to announce the actions as they are recognized by the system.  
6. Performance metrics such as confusion matrices, precision, recall, and F1 scores are calculated to assess the system’s effectiveness in both action recognition and spoof detection.

 ## DATASETS AND RESULTS:

This project uses three datasets for training, evaluation, and validation of its Human Action Recognition (HAR) and anti-spoofing features.The results obtained and the performance across action detection and spoofing identification tasks are detailed below.

### 1. [KTH Dataset:](https://www.csc.kth.se/cvap/actions/)
Originally developed by researchers at the Royal Institute of Technology (KTH) for studying human motion patterns in controlled environments.It includes six human action classes such as walking, jogging, and clapping, recorded under varying conditions.
#### Results:
![c](https://github.com/user-attachments/assets/fd41d21c-e37c-46f6-804a-fd04d3ac3a3b)


![kth_meas](https://github.com/user-attachments/assets/45a4edb2-e60a-4f52-9767-06cf10d49285)


### 2. [UCF50 Dataset:](https://www.crcv.ucf.edu/data/UCF50.php)

It is created by the Center for Research in Computer Vision (CRCV) at the University of Central Florida. It includes a wide variety of videos covering 50 action categories, ranging from sports to everyday activities, making it well-suited for addressing complex action recognition tasks.
#### Results:
![ucfsports](https://github.com/user-attachments/assets/3863d446-d1a4-4dee-92a3-cf794382f7a9)


![ucf_metttt](https://github.com/user-attachments/assets/3da65a99-3097-4016-8628-626b22fb7a25)
The lables correspind to the respective actions in the previous image.


### 3. [iBETA Level 2 Video Attack Dataset:](https://www.kaggle.com/datasets/unidatapro/ibeta-level-2-certification)

It is created by iBETA Quality Assurance to test the effectiveness of anti-spoofing algorithms in biometric systems.
It includes a variety of video-based spoofing attacks, such as screen replays and 3D mask attacks.
#### Results:
![spoof1](https://github.com/user-attachments/assets/ba405ef9-34ea-4951-a02c-aef08df109ad)


![spoof_metr](https://github.com/user-attachments/assets/0b54aeec-7892-49a1-8ec9-6250e98fe899)

## Requirements:


- Python 3.7+
- pip
- Mediapipe
- OpenCV
- NumPy
- Pandas
- scikit-learn
- matplotlib
- pyttsx3

## Installation
1. Clone the repository:
```
git clone https://github.com/your_username/HAR_Spoof_Det_Audio_Feedback.git
cd HAR_Spoof_Det_Audio_Feedback
```
2. Navigate to the relevant directory for the anti-spoofing module:
```
cd Silent-Face-Anti-Spoofing-master
```
3. Install the dependencies required for the project:
```
pip install -r requirements.txt
```
## EXECUTION:

1. The first step is providing datasets of videos or images to the model. Either the data can be manually updated or recorded via the webcam.

2. Input one of the options to record the videos into the /train or the /test folder or process the videos or images to extract data.
```
choice=input("Enter 'r' for training videos or 't' for testing videos or 'p' for processing videos:")
```
   The above code can be run multiple times until all the videos are recorded or processed.

3. Upon choosing 'r', enter the names of the folders for storing training and testing videos when prompted. For example, if you enter "jump" and "run," the following folder structure will be created:
 ```
train/jump
train/run
test/jump
test/run
```
   These folders can also be created manually under the train/ and test/ directories if preferred.

4. Custom training or testing videos can be recorded directly using the webcam. Multiple videos of different actions can be recorded in one go.
   1. The videos recorded for training are simultaneously processed when 'r' option is chosen.
   2. The videos are recorded and stored in the subfolders when 't' option is chosen. 

During the recording process, you will select the action folder where the videos will be stored. The recorded videos will automatically be placed in the corresponding train/ or test/ folders.


5. Datasets can be manually updated accordingly:

   1. Store your training videos in their respective action folders under the train/ directory.
   2. Store your testing videos in their respective action folders under the test/ directory.


6. The manually uploaded videos in the subfolders of /train directory need to be processed to extract the necessary features for training or testing. Input option 'p' for the same.


7. The videos in the /train directory are used to create pipelines upon splitting into training and testing datasets. To train the model with these pipelines run the following code:
```
fit_models = {}
for algo, pipeline in pipelines.items():
    model = pipeline.fit(X_train, y_train)  # Train the model on the training set with different algorithms
    fit_models[algo] = model
```
This will start the training process, and the suitable trained model will be saved in the directory for later use.

8. There are two options for evaluating the model and actions are predicted only if the frame is not detected as spoof. Upon spoof detection, the frame is labeled as spoof and the subsequent frame is accessed.

   1. The videos in the /test folders stored earlier either by recording or manually uploading are processed by the trained model. Predictions will be generated for selected frequency of frames, and the labeled videos (with detected actions and probabilities) will be stored in the processed_videos/ folder.
    To access the folder, navigate to it:
      ```
      ls processed_videos/
      ```
   2. Open the live webcam to recognize actions in real time. Detected actions and their probabilities will be displayed on the screen and the names of the actions are announced via audio feedback.

9. After the evaluation, metrics such as confusion matrices, precision, recall, and F1 scores are calculated.
    1. The confusion matrix will be displayed in the output section.
    2. The tables of the remaining metrics will be saved in the metrics/ folder. You can navigate to the folder to view these results:
       ```
       ls metrics/
       ```

## Acknowledgments

This project makes use of a pre-trained anti-spoofing model, developed by zhuying at Minivision, that is licensed under the **Apache License, Version 2.0**. We would like to thank **Minivision** for providing this model, which has been an integral part of this project.

- The model is provided under the terms of the License. A copy of the License can be found at: [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)






