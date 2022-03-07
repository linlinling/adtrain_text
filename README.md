Adtraing of textcnn on THUCNews dataset

一、背景
本实验测试对抗训练方法（Adversarial Training）在中文文本分类中的应用。文本分类模型为TextCNN，对抗训练测试了PGD、Free、FGSM等3种方法。基于THUCNEWS数据集进行实验。

二、数据介绍
从THUCNews中抽取了20万条新闻标题，文本长度在20到30之间。一共10个类别，每类2万条。标题共有10个类别类别：财经、房产、股票、教育、科技、社会、时政、体育、游戏、娱乐。
建模过程中，切分训练集一共18万，验证集1万， 测试集1万。不同方法使用的数据划分一致，确保结果有可对比性。预训练词向量使用搜狗新闻数据，本实验的对抗训练都是在Embedding数据上进行扰动。


三、试验结果
model	PRECISION	RECALL	F1-macro
baseline	0.9117	0.9116	0.9115
PGD k=3	0.9145	0.9141	0.9140
“Free”	0.9128	0.9119	0.9121
FGSM 	0.9109	0.9107	0.9105


四、实验步骤
Baseline:运行python run.py --model TextCNN
PGD：运行python run.py --model TextCNN --adv PGD
Free: 运行python run.py --model TextCNN --adv FreeAT
FGSM 运行python run.py --model TextCNN --adv FGSM

五、实验总结
1、PGD、“Free”在baseline的基础上有了一定的提升
2、FGSM在THUCNews数据上效果微弱于baseline
3、不同的方法在不同的数据集上有不同的效果，在使用对抗方法时需要做进一步分析验证。
4、本次时间因为时间原因，缺乏有效的参数调优时间，基于基础的参数可以看出，对抗方法可以有效的提升基准模型的性能，提升模型的泛化能力。
