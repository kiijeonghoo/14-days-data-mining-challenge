# 14-days-data-mining-challenge 📊

2020年3月Datawhale第十一期组队学习挑战    

学习内容为：数据挖掘之二手车交易价格预测，来自 Datawhale与天池联合发起的“0基础入门系列”赛事第一场。

https://tianchi.aliyun.com/competition/entrance/231784/introduction   

**Star⭐ me if you find useful🤣**

## 学习内容与进度

详细的个人笔记和注解见notebook中批注，以下是每个task的总结👇

### Task01 - [赛题理解](/nbs/Task1-赛题理解.ipynb) 🍦

- 分类评价指标 - accuracy / precision / recall / f1-score / AUC
- 回归评价指标 - MAE / MSE / MAPE / RMSE / R2
- 数据 - 匿名特征15维 / 非匿名特征15d维 / 训练集15万条 / 测试集5万条
### Task02 - [数据的探索性分析 (EDA)](/nbs/Task2-数据分析.ipynb) 🍦

- 相关包 - pandas / numpy / scipy / matplotlib / seaborn / missingno-用于缺失值可视化 / pandas_profiling
- 载入数据 - head() / tail() / shape 
- 数据总览 - describe() 熟悉数据统计量 / info() 熟悉数据类型
- 缺失和异常 - isnull().sum() / msno.matrix() / msno.bar() / value_counts() / replace() / 类别特征出现严重偏斜的处理
- 预测值分布 - sns.distplot() 可用scipy库fit拟合参数分布 / skew() 偏度 / kurt() 峰度 /  数据呈偏态分布可用log变换
- 数字特征 - corr() 相关性分析(默认Pearson) / heatmap() / facetgrids() / pairplot() / 多图可视化分布和相互关系
- 类别特征 - nunique() + value_counts() 查看类别变量分布 / boxplot() / violinplot / barplot() / countplot() 可视化
- 数据报告 - pandas_profiling 生成数据报告 (简单全面，但速度较慢)
- pandas查漏补缺 - append() / plot() / sample() / melt() / DF['col'].astype('category').cat.add_categories() 

### Task03：数据的特征工程
### Task04：建模与调参
### Task05：模型结果融合 

## 参考资料

Datawhale开源学习资料：https://github.com/datawhalechina/team-learning 

天池比赛论坛：https://tianchi.aliyun.com/competition/entrance/231784/forum

