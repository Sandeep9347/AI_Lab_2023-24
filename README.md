# Ex.No: 13 Learning – Use Supervised Learning  
### DATE: 15-11-25                                                                           
### REGISTER NUMBER : 212222060215
### AIM: 
To write a program to train the classifier for Diabetes Prediction.
###  Algorithm:
1. Start the program.
2. Import required Python libraries, including NumPy, Pandas, Google Colab, Gradio, and various
scikit-learn modules.
3. Mount Google Drive using Google Colab's 'drive.mount()' method to access the data file
located in Google Drive.
4. Install the Gradio library using 'pip install gradio'.
5. Load the diabetes dataset from a CSV file ('diabetes.csv') using Pandas.
6. Separate the target variable ('Outcome') from the input features and Scale the input features
using the StandardScaler from scikit-learn.
7. Create a multi-layer perceptron (MLP) classifier model using scikit-learn's 'MLPClassifier'.
8. Train the model using the training data (x_train and y_train).
9. Define a function named 'diabetes' that takes input parameters for various features and Use
the trained machine learning model to predict the outcome based on the input features.
10. Create a Gradio interface using 'gr.Interface' and Specify the function to be used to make
predictions based on user inputs.
11. Launch the Gradio web application, enabling sharing, to allow users to input their data and
get predictions regarding diabetes risk.
12. Stop the program.
### Program:
```
from google.colab import drive
drive.mount('/content/gdrive')
```
```
#import packages
import numpy as np
import pandas as pd
```
```
pip install gradio
```
```
pip install typing-extensions --upgrade
```
```
!python --version
```
```
 pip install --upgrade typing
```
```
import gradio as gr
import pandas as pd
```
```
cd /content/gdrive/MyDrive/demo/gradio_project-main
```
```
#get the data
data = pd.read_csv('diabetes.csv')
data.head()
```
```
print(data.columns)
```
```
x = data.drop(['Outcome'], axis=1)
y = data['Outcome']
print(x[:5])
```
```
#split data
from sklearn.model_selection import train_test_split

x_train, x_test, y_train, y_test= train_test_split(x,y)
```
```
#scale data
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
x_train_scaled = scaler.fit_transform(x_train)
x_test_scaled = scaler.fit_transform(x_test)
```
```
#instatiate model
from sklearn.neural_network import MLPClassifier
model = MLPClassifier(max_iter=1000, alpha=1)
model.fit(x_train, y_train)
print("Model Accuracy on training set:", model.score(x_train, y_train))
print("Model Accuracy on Test Set:", model.score(x_test, y_test))
```
```
print(data.columns)
```
```
#create a function for gradio
def diabetes(Pregnancies, Glucose, Blood_Pressure, SkinThickness, Insulin, BMI,Diabetes_Pedigree, Age):
    x = np.array([Pregnancies,Glucose,Blood_Pressure,SkinThickness,Insulin,BMI,Diabetes_Pedigree,Age])
    prediction = model.predict(x.reshape(1, -1))
    if(prediction==0):
      return "NO"
    else:
      return "YES"
```
```
outputs = gr.Textbox()
app = gr.Interface(fn=diabetes, inputs=['number','number','number','number','number','number','number','number'], outputs=outputs,description="Detection of Diabeties")
app.launch(share=True)
```

### Output:
![image](https://github.com/NithishThirumalai/AI_Lab_2023-24/assets/114301782/f65f8935-6a7a-4259-80d1-9ad3f507c81a)
![image](https://github.com/NithishThirumalai/AI_Lab_2023-24/assets/114301782/f06f890e-a127-43ed-84d0-c0630ea114bb)
![image](https://github.com/NithishThirumalai/AI_Lab_2023-24/assets/114301782/afa24ae2-4f97-4a7a-b291-0c63aa878612)
![280472576-361414a1-d8fa-4fe0-a7b7-6cfc96201742](https://github.com/NithishThirumalai/AI_Lab_2023-24/assets/114301782/d907f1f6-49ff-41c9-95c1-09d90122ee41)




### Result:
Thus the system was trained successfully and the prediction was carried out.
