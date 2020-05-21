<br>为了方便下载，将代码部分与数据集部分分开存放，所以训练集和两个测试集需要另行下载后放在相应的位置。
<br>train_datasets训练集复制到  /group7_houtai/train/datasets
<br>test1_datasets测试集复制到 /group7_houtai/test1/datasets
<br>test2_datasets测试集复制到 /group7_houtai/test2/datasets
<br>只需要复制里面的csv文件，不要复制文件夹

# train数据集
## CWRU四分类任务实验

### 一、数据说明
数据中包含一个文件夹，datasets，用作训练集。   
datasets文件夹中有多个数据文件，文件名含义如下：   
B代表故障发生在Ball位置，同理IR代表故障发生在inner race位置，OR代表故障发生在outer race位置，NORMAL代表数据文件是正常数据文件；   
每个数据文件可能包含如下多维信号（部分文件可能其中不包括某些维度的信号）：   
DE_time:驱动端加速度数据   
FE_time:风扇端加速度数据   
BA_time:基本加速度数据   
RPM:每分钟转速数据，在提取时实际上RPM对于每个文件只有一个值，但为了文件格式整齐，扩展成了一列，即实际上这一列都是同一个值，代表该文件的RPM

### 二、任务说明
1、训练一个四分类模型，预测目标为故障发生的位置(normal, ball, inner race, outer race)   
2、以train文件夹中的数据为训练集，可自行划分数据作为验证集进行模型的验证调优。

### 三、可供参考的评分规则
评分score为分别单独计算四类预测结果的f1-score加权求和，
其中三个故障类的权重ball,inner race,outer race均为0.3，正常类的权重为0.1   



# test数据集


## CWRU四分类任务实验

### 一、测试集数据说明
数据中包含一个文件夹，datasets，用作测试集。   
datasets文件夹中包含多个数据文件，文件名并不包含含义，仅用作记号。    
每个数据文件可能包含如下多维信号（部分文件可能其中不包括某些维度的信号）：   
DE_time:驱动端加速度数据   
FE_time:风扇端加速度数据   
BA_time:基本加速度数据   
RPM:每分钟转速数据，在提取时实际上RPM对于每个文件只有一个值，但为了文件格式整齐，扩展成了一列，即实际上这一列都是同一个值，代表该文件的RPM

特别说明：TEST08的原始数据不含RPM，经查，该数据的RPM是1750，有需要的可以使用该数值作为TEST08中RPM的参考值

### 二、测试集答案提交形式
提交答案时，约定normal(NORMAL), ball(B), outer race(OR), inner race(IR)的预测输出标签为0, 1, 2, 3。   
提交csv文件，文件分两列，第一列为按序预测结果(0/1/2/3)，第二列为预测结果所在的测试集文件(字符串形式，例如TEST01)，分别以label和filename作为列名。具体形式参照提供的example.csv。

### 三、评分规则
使用四类的f1-score(precision和recall值的调和平均数)加权和进行评价，按照上面的标签约定，即：   
score = [0.3×f1score(class1) + 0.3×f1score(class2) + 0.3×f1score(class3) + 0.1×f1score(class0)]*100   
满分为100分。






