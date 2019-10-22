# Artificial Intelligence with Python

>*Artificial Intelligence with Python*  
*Prateek Joshi*  
*2017, Packt Publishing Ltd.*  
*人工智能：Python实现*  
*影印版*  
*2017 东南大学出版社*  
*中南大学图书馆*  
*2019 02 22 - 萍乡，长沙*  

---

Source Code: [GitHub-PacktPublishing/Artificial-Intelligence-with-Python](https://github.com/PacktPublishing/Artificial-Intelligence-with-Python)

---

#### CONTENTS
* [Chapter 1: Introduction to Artificial Intelligence](#chapter-1-introduction-to-artificial-intelligence)
* [Chapter 2: Classification and Regression Using Supervised Learning](#chapter-2-classification-and-regression-using-supervised-learning)
* [Chapter 3: Predictive Analytics with Ensemble Learning](#chapter-3-predictive-analytics-with-ensemble-learning)


---

## Chapter 1: Introduction to Artificial Intelligence

## Chapter 2: Classification and Regression Using Supervised Learning

#### Preprocessing data | 数据预处理
```python
import numpy as np
from sklearn import preprocessing
input_data = np.array([[ 5.1, -2.9,  3.3],
                       [-1.2,  7.8, -6.1],
                       [ 3.9,  0.4,  2.1],
                       [ 7.3, -9.9, -4.5]])
```
##### Binarization | 二值化
以2.1为阈值将数据二值化。
```python
>>> data_binarized=preprocessing.Binarizer(threshold=2.1).transform(input_data)
>>> data_binarized
array([[1., 0., 1.],
       [0., 1., 0.],
       [1., 0., 0.],
       [1., 0., 0.]])
```
##### Mean removal | 标准化
将样本每一列分别线性变换为均值为0，标准差为1的数据。
```python
>>> # BEFORE
>>> input_data.mean(axis=0)
array([ 3.775, -1.15 , -1.3  ])
>>> input_data.std(axis=0)
array([3.12039661, 6.36651396, 4.0620192 ])

>>> # AFTER
>>> data_scaled=preprocessing.scale(input_data)
>>> data_scaled
array([[ 0.42462551, -0.2748757 ,  1.13244172],
       [-1.59434861,  1.40579288, -1.18167831],
       [ 0.04005901,  0.24346134,  0.83702214],
       [ 1.12966409, -1.37437851, -0.78778554]])
>>> data_scaled.mean(axis=0)
array([1.11022302e-16, 0.00000000e+00, 2.77555756e-17])
>>> data_scaled.std(axis=0)
array([1., 1., 1.])
```
##### Scaling | 放缩
将样本每一列分别线性变换为最大值为1，最小值为0的数据。
```python
>>> data_scaler_minmax=preprocessing.MinMaxScaler(feature_range=(0, 1))
>>> data_scaled_minmax=data_scaler_minmax.fit_transform(input_data)
>>> data_scaled_minmax
array([[0.74117647, 0.39548023, 1.        ],
       [0.        , 1.        , 0.        ],
       [0.6       , 0.5819209 , 0.87234043],
       [1.        , 0.        , 0.17021277]])
```
##### Normalization | 规范化
将样本每一列线性变换为单位范数的向量。

L1 normalization:

$$
z=\|x_1\|=\sum_{i=1}^n \vert x_i\vert
$$

L2 normalization:

$$
z=\|x_2\|=\sqrt{\sum_{i=1}^n x_i^2}
$$

一般来说，L1规范化的健壮性更好，它受偏离较大的分量的影响较小。若偏离的数据很重要，那么L2是更好的选择。
```python
>>> data_normalized_l1=preprocessing.normalize(input_data, norm='l1')
>>> data_normalized_l1
array([[ 0.45132743, -0.25663717,  0.2920354 ],
       [-0.0794702 ,  0.51655629, -0.40397351],
       [ 0.609375  ,  0.0625    ,  0.328125  ],
       [ 0.33640553, -0.4562212 , -0.20737327]])

>>> data_normalized_l2=preprocessing.normalize(input_data, norm='l2')
>>> data_normalized_l2
array([[ 0.75765788, -0.43082507,  0.49024922],
       [-0.12030718,  0.78199664, -0.61156148],
       [ 0.87690281,  0.08993875,  0.47217844],
       [ 0.55734935, -0.75585734, -0.34357152]])
```

#### Label encoding | 标签编码
`sklearn`模块要求数据的标签是数字。若原始标签是文字，则需要将它们转换。
```python
import numpy as np
from sklearn import preprocessing
input_labels = ['red', 'black', 'red', 'green', 'black', 'yellow', 'white']

# Create the encoder
encoder = preprocessing.LabelEncoder()
encoder.fit(input_labels)
```

```python
>>> for i, item in enumerate(encoder.classes_):
	print(item, '-->', i)
       	
black --> 0
green --> 1
red --> 2
white --> 3
yellow --> 4
```

编码
```python
>>> test_labels = ['green', 'red', 'black']
>>> encoded_values = encoder.transform(test_labels)
>>> list(encoded_values)
[1, 2, 0]
```

解码
```python
>>> encoded_values = [3, 0, 4, 1]
>>> decoded_list = encoder.inverse_transform(encoded_values)
>>> list(decoded_list)
['white', 'black', 'yellow', 'green']
```

### Classifier | 分类算法

#### 绘图函数
```python
import numpy as np
import matplotlib.pyplot as plt

def visualize_classifier(classifier, X, y):
    # 坐标图范围和最小分度
    min_x, max_x = X[:, 0].min() - 1.0, X[:, 0].max() + 1.0
    min_y, max_y = X[:, 1].min() - 1.0, X[:, 1].max() + 1.0
    mesh_step_size = 0.01

    # 定义坐标图
    x_vals, y_vals = np.meshgrid(np.arange(min_x, max_x, mesh_step_size), np.arange(min_y, max_y, mesh_step_size))

    # 执行分类算法
    output = classifier.predict(np.c_[x_vals.ravel(), y_vals.ravel()])

    # Reshape the output array
    output = output.reshape(x_vals.shape)

    # 生成坐标图
    plt.figure()

    # 选择颜色
    plt.pcolormesh(x_vals, y_vals, output, cmap=plt.cm.gray)

    # 绘制训练点
    plt.scatter(X[:, 0], X[:, 1], c=y, s=75, edgecolors='black', linewidth=1, cmap=plt.cm.Paired)

    # 绘制边界和坐标
    plt.xlim(x_vals.min(), x_vals.max())
    plt.ylim(y_vals.min(), y_vals.max())
    plt.xticks((np.arange(int(X[:, 0].min() - 1), int(X[:, 0].max() + 1), 1.0)))
    plt.yticks((np.arange(int(X[:, 1].min() - 1), int(X[:, 1].max() + 1), 1.0)))

    plt.show()
```

#### Logistic Regression classifier | 逻辑回归分类
```python
import numpy as np
from sklearn import linear_model 
import matplotlib.pyplot as plt

X = np.array([[3.1, 7.2], [4, 6.7], [2.9, 8], [5.1, 4.5], [6, 5], [5.6, 5], [3.3, 0.4], [3.9, 0.9], [2.8, 1], [0.5, 3.4], [1, 4], [0.6, 4.9]])
y = np.array([0, 0, 0, 1, 1, 1, 2, 2, 2, 3, 3, 3])

# 创建分类器
classifier = linear_model.LogisticRegression(solver='liblinear', C=1)

# 训练分类器
classifier.fit(X, y)

visualize_classifier(classifier, X, y)
```
输出在坐标图上依据点的分类将平面分为四组。

若将C值（与惩罚函数值正相关）调高，如100，可以得到更好的分类结果。但如果太高则会出现过拟合。

#### Naive Bayes classifier | 朴素贝叶斯分类
这种分类器基于贝叶斯定理。每一输入对输出的贡献视为相互独立的，故称为“朴素”。

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.naive_bayes import GaussianNB # Naive Bayes
from sklearn import cross_validation

# 文件中的数据每行第一二个为输入向量X，最后一个为y即输出
input_file = 'data_multivar_nb.txt'

# Load data from input file
data = np.loadtxt(input_file, delimiter=',')
X, y = data[:, :-1], data[:, -1] 

# 这里使用高斯朴素贝叶斯分类器，即假设变量服从高斯分布 
classifier = GaussianNB()

# Train the classifier
classifier.fit(X, y)

# Predict the values for training data
y_pred = classifier.predict(X)

# Compute accuracy
accuracy = 100.0 * (y == y_pred).sum() / X.shape[0]
print("Accuracy of Naive Bayes classifier =", round(accuracy, 2), "%")

visualize_classifier(classifier, X, y)
```

但是使用训练数据来测试肯定是不合理的，需要使用`cross validation`，即分离训练与测试。

```python
# Cross validation 

# Split data into training and test data 
X_train, X_test, y_train, y_test = cross_validation.train_test_split(X, y, test_size=0.2, random_state=3)
classifier_new = GaussianNB()
classifier_new.fit(X_train, y_train)
y_test_pred = classifier_new.predict(X_test)

# compute accuracy of the classifier
accuracy = 100.0 * (y_test == y_test_pred).sum() / X_test.shape[0]
print("Accuracy of the new classifier =", round(accuracy, 2), "%")

visualize_classifier(classifier_new, X_test, y_test)
```

#### Confusion matrix | 混淆矩阵
混淆矩阵用于评估分类器工作效果。举一个简单的例子，一个二元分类器混淆矩阵有四项：

* True positives: 预测=1，真值=1 
* True negatives: 预测=0，真值=0
* False positives: 预测=1，真值=0，即第一类错误
* False negatives: 预测=0，真值=1，即第二类错误

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.metrics import confusion_matrix
from sklearn.metrics import classification_report

# Define sample labels
true_labels = [2, 0, 0, 2, 4, 4, 1, 0, 3, 3, 3]
pred_labels = [2, 1, 0, 2, 4, 3, 1, 0, 1, 3, 3]

# Create confusion matrix
confusion_mat = confusion_matrix(true_labels, pred_labels)

# Visualize confusion matrix
plt.imshow(confusion_mat, interpolation='nearest', cmap=plt.cm.gray)
plt.title('Confusion matrix')
plt.colorbar()
ticks = np.arange(5)
plt.xticks(ticks, ticks)
plt.yticks(ticks, ticks)
plt.ylabel('True labels')
plt.xlabel('Predicted labels')
plt.show()

# Classification report
targets = ['Class-0', 'Class-1', 'Class-2', 'Class-3', 'Class-4']
print('\n', classification_report(true_labels, pred_labels, target_names=targets))
```

### Support Vector Machines (SVM) | 支持向量机
支持向量机在空间中找到一个最佳超平面，划分不同的数据类。这里的最佳被定义为各个训练点到超平面的距离之和最大。

下面使用支持向量机，由居民的14项属性预测年收入是否高于$50K。

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn import preprocessing
from sklearn.svm import LinearSVC
from sklearn.multiclass import OneVsOneClassifier
from sklearn import cross_validation

# Input file containing data
input_file = 'income_data.txt'

# Read the data
X = []
y = []
count_class1 = 0
count_class2 = 0
max_datapoints = 25000

with open(input_file, 'r') as f:
    for line in f.readlines():
        if count_class1 >= max_datapoints and count_class2 >= max_datapoints:
            break

        if '?' in line:
            continue

        data = line[:-1].split(', ')

        if data[-1] == '<=50K' and count_class1 < max_datapoints:
            X.append(data)
            count_class1 += 1

        if data[-1] == '>50K' and count_class2 < max_datapoints:
            X.append(data)
            count_class2 += 1

# Convert to numpy array
X = np.array(X)

# Convert string data to numerical data
label_encoder = [] 
X_encoded = np.empty(X.shape)
for i,item in enumerate(X[0]):
    if item.isdigit(): 
        X_encoded[:, i] = X[:, i]
    else:
        label_encoder.append(preprocessing.LabelEncoder())
        X_encoded[:, i] = label_encoder[-1].fit_transform(X[:, i])

X = X_encoded[:, :-1].astype(int)
y = X_encoded[:, -1].astype(int)

# Create SVM classifier
classifier = OneVsOneClassifier(LinearSVC(random_state=0))

# Train the classifier
classifier.fit(X, y)

# Cross validation
X_train, X_test, y_train, y_test = cross_validation.train_test_split(X, y, test_size=0.2, random_state=5)
classifier = OneVsOneClassifier(LinearSVC(random_state=0))
classifier.fit(X_train, y_train)
y_test_pred = classifier.predict(X_test)

# Compute the F1 score of the SVM classifier
f1 = cross_validation.cross_val_score(classifier, X, y, scoring='f1_weighted', cv=3)
print("F1 score: " + str(round(100*f1.mean(), 2)) + "%")

# Predict output for a test datapoint
input_data = ['37', 'Private', '215646', 'HS-grad', '9', 'Never-married', 'Handlers-cleaners', 'Not-in-family', 'White', 'Male', '0', '0', '40', 'United-States']

# Encode test datapoint
input_data_encoded = [-1] * len(input_data)
count = 0
for i, item in enumerate(input_data):
    if item.isdigit():
        input_data_encoded[i] = int(input_data[i])
    else:
        input_data_encoded[i] = int(label_encoder[count].transform(input_data[i]))
        count += 1 

input_data_encoded = np.array(input_data_encoded)

# Run classifier on encoded datapoint and print output
predicted_class = classifier.predict(input_data_encoded)
print(label_encoder[-1].inverse_transform(predicted_class)[0])
```

### Regression | 回归
回归是估计输入与输出关系的算法。  
回归的观点在于假设输入输出的向量之间存在某种待于揭示关系。  

输入变量被称为`independent variables`或`predictors`；  
输出变量被称为`dependent variables`或`criterion variables`。  

回归分析的结论在于分析只有某一个变化而其它变量保持不变时，输出量的变化趋势并作出预测。线性回归中，假设这种关系是线性的。在这种模型精度不足时，可以使用多项式回归。

#### 单变量回归器
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn import preprocessing
from sklearn.svm import LinearSVC
from sklearn.multiclass import OneVsOneClassifier
from sklearn import cross_validation

# Input file containing data
input_file = 'income_data.txt'

# Read the data
X = []
y = []
count_class1 = 0
count_class2 = 0
max_datapoints = 25000

with open(input_file, 'r') as f:
    for line in f.readlines():
        if count_class1 >= max_datapoints and count_class2 >= max_datapoints:
            break

        if '?' in line:
            continue

        data = line[:-1].split(', ')

        if data[-1] == '<=50K' and count_class1 < max_datapoints:
            X.append(data)
            count_class1 += 1

        if data[-1] == '>50K' and count_class2 < max_datapoints:
            X.append(data)
            count_class2 += 1

# Convert to numpy array
X = np.array(X)

# Convert string data to numerical data
label_encoder = [] 
X_encoded = np.empty(X.shape)
for i,item in enumerate(X[0]):
    if item.isdigit(): 
        X_encoded[:, i] = X[:, i]
    else:
        label_encoder.append(preprocessing.LabelEncoder())
        X_encoded[:, i] = label_encoder[-1].fit_transform(X[:, i])

X = X_encoded[:, :-1].astype(int)
y = X_encoded[:, -1].astype(int)

# Create SVM classifier
classifier = OneVsOneClassifier(LinearSVC(random_state=0))

# Train the classifier
classifier.fit(X, y)

# Cross validation
X_train, X_test, y_train, y_test = cross_validation.train_test_split(X, y, test_size=0.2, random_state=5)
classifier = OneVsOneClassifier(LinearSVC(random_state=0))
classifier.fit(X_train, y_train)
y_test_pred = classifier.predict(X_test)

# Compute the F1 score of the SVM classifier
f1 = cross_validation.cross_val_score(classifier, X, y, scoring='f1_weighted', cv=3)
print("F1 score: " + str(round(100*f1.mean(), 2)) + "%")

# Predict output for a test datapoint
input_data = ['37', 'Private', '215646', 'HS-grad', '9', 'Never-married', 'Handlers-cleaners', 'Not-in-family', 'White', 'Male', '0', '0', '40', 'United-States']

# Encode test datapoint
input_data_encoded = [-1] * len(input_data)
count = 0
for i, item in enumerate(input_data):
    if item.isdigit():
        input_data_encoded[i] = int(input_data[i])
    else:
        input_data_encoded[i] = int(label_encoder[count].transform(input_data[i]))
        count += 1 

input_data_encoded = np.array(input_data_encoded)

# Run classifier on encoded datapoint and print output
predicted_class = classifier.predict(input_data_encoded)
print(label_encoder[-1].inverse_transform(predicted_class)[0])
```

#### 多变量回归器
```python
import numpy as np
from sklearn import linear_model
import sklearn.metrics as sm
from sklearn.preprocessing import PolynomialFeatures

# Input file containing data
input_file = 'data_multivar_regr.txt'

# Load the data from the input file
data = np.loadtxt(input_file, delimiter=',')
X, y = data[:, :-1], data[:, -1]

# Split data into training and testing 
num_training = int(0.8 * len(X))
num_test = len(X) - num_training

# Training data
X_train, y_train = X[:num_training], y[:num_training]

# Test data
X_test, y_test = X[num_training:], y[num_training:]

# Create the linear regressor model
linear_regressor = linear_model.LinearRegression()

# Train the model using the training sets
linear_regressor.fit(X_train, y_train)

# Predict the output
y_test_pred = linear_regressor.predict(X_test)

# Measure performance
print("Linear Regressor performance:")
print("Mean absolute error =", round(sm.mean_absolute_error(y_test, y_test_pred), 2))
print("Mean squared error =", round(sm.mean_squared_error(y_test, y_test_pred), 2))
print("Median absolute error =", round(sm.median_absolute_error(y_test, y_test_pred), 2))
print("Explained variance score =", round(sm.explained_variance_score(y_test, y_test_pred), 2))
print("R2 score =", round(sm.r2_score(y_test, y_test_pred), 2))

# Polynomial regression
polynomial = PolynomialFeatures(degree=10)
X_train_transformed = polynomial.fit_transform(X_train)
datapoint = [[7.75, 6.35, 5.56]]
poly_datapoint = polynomial.fit_transform(datapoint)

poly_linear_model = linear_model.LinearRegression()
poly_linear_model.fit(X_train_transformed, y_train)
print("\nLinear regression:\n", linear_regressor.predict(datapoint))
print("\nPolynomial regression:\n", poly_linear_model.predict(poly_datapoint))
```

#### 支持向量回归预测房价

```python
import numpy as np
from sklearn import datasets
from sklearn.svm import SVR
from sklearn.metrics import mean_squared_error, explained_variance_score
from sklearn.utils import shuffle

# Load housing data
data = datasets.load_boston() 

# Shuffle the data
X, y = shuffle(data.data, data.target, random_state=7)

# Split the data into training and testing datasets 
num_training = int(0.8 * len(X))
X_train, y_train = X[:num_training], y[:num_training]
X_test, y_test = X[num_training:], y[num_training:]

# Create Support Vector Regression model
sv_regressor = SVR(kernel='linear', C=1.0, epsilon=0.1)

# Train Support Vector Regressor
sv_regressor.fit(X_train, y_train)

# Evaluate performance of Support Vector Regressor
y_test_pred = sv_regressor.predict(X_test)
mse = mean_squared_error(y_test, y_test_pred)
evs = explained_variance_score(y_test, y_test_pred) 
print("\n#### Performance ####")
print("Mean squared error =", round(mse, 2))
print("Explained variance score =", round(evs, 2))

# Test the regressor on test datapoint
test_data = [3.7, 0, 18.4, 1, 0.87, 5.95, 91, 2.5052, 26, 666, 20.2, 351.34, 15.27]
print("\nPredicted price:", sv_regressor.predict([test_data])[0])
```

## Chapter 3: Predictive Analytics with Ensemble Learning

### Ensemble Learning | 集成学习
集成学习指结合多个模型进行求解，以得到更好的结果。

#### Decision Trees | 决策树
决策树将数据集分组，在每一层作出简单决策，这样这棵树最后能得到最终结果。