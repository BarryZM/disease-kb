# disease-kb
# 常见疾病相关信息构建knowledge graph

**本项目根据从权威医药网站上爬取的医疗数据，对数据进行处理，从而运用到中文开放知识图谱（OpenKG.cn）中，以便需要者直接使用。**
**OpenKG链接：http://openkg.cn/dataset/disease-information**
 
**本项目借鉴前人智慧，但基于其爬取数据的方法对数据进行了更加充分的使用，https://github.com/liuhuanyong/QASystemOnMedicalKG。**
 
**对获得的医疗数据进行整理，使其可直接用于知识图谱的搭建（Neo4j），文件处理成json格式。文件分为实体（实体基本信息与属性）和关系（不同实体间关系）两个类别。**
## 文件介绍
```shell
diseaseKB
├── data
│   └── medical.json 结构化疾病医疗知识
├── prepare_data
│   ├── build_data.py 数据处理到数据库
│   ├── data_spider.py 爬取数据
│   └── max_cut.py 根据给定的词典对文本进行前向、后向和双向最大匹配
├── dict 各种类别的词典
├── build_medicalgraph.py 利用结构化的数据建立Neo4j知识图谱 
├── build_medicalgraph_from_json.py 利用实体和关系json文件据建立知识图谱 
└── build_json.py 利用爬取的数据生成提炼的实体和关系json文件
```


## 数据获取与处理
### 获取
  数据从“寻医问药”医疗网站上爬取原始数据，将其保存到本地数据库（mongodb)中。爬取数据以疾病为单位，获得其各方面的信息，如：成因、症状、服用药物等。爬取时，根据疾病id爬取不同的网站。除疾病外，还爬取了疾病监测的相关数据，也将其保存到数据库中。
### 处理
  对爬取的数据进行预处理，筛选适合做知识图谱知识存储的相关信息。最后从数据库中提取出结构化的文件medical.json,用于搭建知识图谱。数据大致信息如下：
  <p align="left">
	<img src=./pic/json.png alt="Sample"  width="500">
	<p align="center">
		<em> </em>
	</p>
</p>

## 知识图谱
  利用结构化的知识，选择相关内容作为实体、关系与属性，搭建Neo4j上的知识图谱。为方便使用，将搭建图谱的实体、关系与属性保存为json格式，即方便搭建知识图谱，也利于阅读。
### 搭建
  medical.json为从数据中导出的整理后的疾病医疗数据，读取该文件获得各类别的实体、关系，从而搭建知识图谱。
  同时，也可以先从medical.json提炼出实体与关系的json文件，再通过这两个文件生成知识图谱。
  这两种生成的知识图谱等价。
### 文件介绍
