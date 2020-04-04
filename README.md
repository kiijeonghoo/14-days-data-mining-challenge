# 14-days-data-mining-challenge 📊

2020年3月Datawhale第十一期组队学习挑战    

学习内容为：数据挖掘之二手车交易价格预测，来自 Datawhale与天池联合发起的“0基础入门系列”赛事第一场。

https://tianchi.aliyun.com/competition/entrance/231784/introduction   

**Star⭐ me if you find useful🤣**

## 学习内容与进度 完结撒花 🎉

详细的个人笔记和注解见[notebook](/nbs/)中批注，以下是每个task的总结👇

### Task00 - [**Baseline**](/nbs/Task0-Baseline.ipynb) 🍦

- 特征 - 数值特征 (gearbox, power, kilometer, v_0 - v14) / 类别特征没有选取
- 缺失值处理 - 填充 (-1)
- 单模型测试 - XGB + 5KFold (val MAE=714) / train : val (7 : 3) + LGB (val MAE=679) / train : val (7 : 3) + XGB (val MAE=704)
- 模型融合 - XGB + LGB + 简单加权 + 修正负值 (val MAE=676)

### Task01 - [赛题理解](/nbs/Task1-赛题理解.ipynb) 🍦

- 分类评价指标 - accuracy / precision / recall / f1-score / AUC
- 回归评价指标 - MAE / MSE / MAPE / RMSE / R2
- 数据 - 匿名特征15维 / 非匿名特征15d维 / 训练集15万条 / 测试集5万条
### Task02 - [探索性分析 (EDA)](/nbs/Task2-数据分析.ipynb) 🍦

- 相关包 - pandas / numpy / scipy / matplotlib / seaborn / missingno-用于缺失值可视化 / pandas_profiling
- 载入数据 - head() / tail() / shape 
- 数据总览 - describe() 熟悉数据统计量 / info() 熟悉数据类型
- 缺失和异常 - isnull().sum() / msno.matrix() / msno.bar() / value_counts() / replace() / 类别特征出现严重偏斜的处理
- 预测值分布 - sns.distplot() 可用scipy库fit拟合参数分布 / skew() 偏度 / kurt() 峰度 /  数据呈偏态分布可用log变换
- 数字特征 - corr() 相关性分析(默认Pearson) / heatmap() / facetgrids() / pairplot() / 多图可视化分布和相互关系
- 类别特征 - nunique() + value_counts() 查看类别变量分布 / boxplot() / violinplot / barplot() / countplot() 可视化
- 数据报告 - pandas_profiling 生成数据报告 (简单全面，但速度较慢)
- pandas查漏补缺 - append() / plot() / sample() / melt() / DF['col'].astype('category').cat.add_categories() 

### Task03 - [特征工程](/nbs/Task3-特征工程.ipynb) 🍦

- 异常值处理 - 箱线图删除异常值 / Box-Cox变换 如 log(1+x) / 长尾截断
- 缺失值处理 - XGBoost等树模型 (不处理) / 缺失太多 (删除) / 插值补全 (均值中位数众数等) / 分箱 (缺失值分一个箱)
- 特征归一化/标准化 - 标准化 - 标准正态分布 / 归一化 - [0,1]区间 / 幂律分布情况
- 数据分箱 - 数据离散化 / 等频分箱 / 等距分箱 / Best-KS分箱 / 卡方分箱
- 特征构造 - 统计量特征 (计数求和比例等) / 时间特征 / 地理信息 / 非线性变换 / 特征组合 特征交叉
- 特征筛选 - 过滤式 (先筛选后训练) / 包裹式 (将学习器性能作为特征子集的评价准则) / 嵌入式 (学习过程自动特征选择)
- 降维 - PCA / LDA / ICA / 特征筛选也是一种降维
- pandas查漏补缺 - quantile() / to_datatime() / groupby() 后的 for 遍历 / merge() / cut() 

### Task04 - [建模与调参](/nbs/Task4-建模调参.ipynb) 🍦

#### - 线性模型

- 线性模型对于特征的要求 -  数据项误差符合正态分布
- 处理长尾分布 - log(x + 1)
- 交叉验证 - `cross_val_score`，如k折交叉验证，每折数据都做过一次验证集
- 时间特征对于模型的影响 - 基于真实业务的模型在时间的顺序上必须正确
- 学习曲线和验证曲线 - **learing_curve**样本大小与准确率的关系 / **validation_curve**模型参数与准确率之间的关系
- 嵌入式特征选择 - 线性模型 + L1正则 = Ridge 岭回归 / 线性模型 + L2正则 = Lasso回归 / 决策树通过信息熵选择分裂节点

#### - 非线性模型

- 常用非线性模型 - 支持向量机 / 决策树 / 随机森林 / 梯度提升回归 / 多层感知机 / XGBoost / Lightgbm
- 模型调参 - 贪心调参 / Grid Search调参 / 贝叶斯调参

### Task05 - [模型融合](/nbs/Task5-模型融合.ipynb) 🍦

#### - 简单加权融合

- 回归 (分类概率) - 平均法 (多个学习器输出结果求均值) / 简单加权平均 / 算数平均 / 几何平均 / 中位数
- 分类 - 投票法 (选择多个学习器输出最多的类) / 硬投票 (不区分模型结果相对重要性, 得票数最多的类为最终结果) / 软投票 (为不同模型设置不同权重, 区别模型的重要性) / 使用`VotingClassifier`
- 综合 - 排序融合 / log融合


#### - Stacking

- 基本思想 - 初始训练数据 --> 训练若干初始学习器 --> 预测结果 --> 作为次级学习器的训练集 --> 训练次级学习器
- 解决过拟合问题 - 次级学习器尽量选择简单线性模型 / K折交叉验证
- 次级学习器训练集 - 多个初始学习器在**原train**上的预测 P1, P2 ... Pn, **原train**的真实标签label
- 次级学习器测试集 - 多个初始学习器在**原test**上的预测 T1, T2 ... Tn, **原test**的真实标签label
- `mlxtend`库 - `StackingClassifier()`简化了Stacking, `plot_decision_regions()`绘图可视化

#### - Blending

- 基本思想 - **原train**分为 sub_train, sub_test --> 若干初始学习器训练 sub_train --> 预测 sub_test 和原 test --> sub_test 预测结果作为次级学习器训练集，**原test**预测结果作为测试集 -->次级学习器
- 优点 - 比Stacking简单 (无需k折交叉验证) / 避免信息泄露 data leakage (初始学习器和次级学习器使用的训练集不同)
- 缺点 - 第二阶段使用了很少数据 / 过拟合 / 不如 Stacking 的k折交叉验证稳健

#### - 其他方法

- 如Stacking基础上对初始学习器的预测结果**做变换**(平方, 指数, log) 后形成次级学习器的训练集

### Python查漏补缺

#### pandas 🐼

- `memory_usage(deep=True)`返回每列的内存占用(Bytes)
- `sort_values("col")`按某一列排序
- `select_dtypes(exclude = 'object').columns`选取数值特征的 columns
- `select_dtypes(include = 'object').columns`选取类别特征的 columns

#### numpy 🧩

- `np.iinfo(np.int8)`, 查看数据类型的信息，如查看最大最小值`np.iinfo(np.int8).min`
- `np.percentile(array, 75)`, `np.quantile(a, 0.75)`分位数计算， 注意二者不同点
- `np.nan_to_num()`，把nan转换成0，inf转换成有限大小的数

#### sklearn 📚

- 线性模型`model = LinearRegression()`, `model.coef_`查看权重，`model.intercept_`查看截距
- `cross_val_score()`用于交叉验证
- `GridSearchCV()`用于网格调参
- `BayesianOptimization()`用于贝叶斯调参
- `VotingClassifier()`用于模型融合的投票法, 参数`voting`可选择 hard 硬投票 soft 软投票
- `KFold()`与`StratifiedKFold()`区别：后者是分层采样, 确保train, test中各类别样本的比例与原始数据集中相同
- `predict()`与`predict_proba()`区别：前者返回预测结果, 标签值, 后者返回样本在各个标签值上的概率

#### matplotlib 🎨

- `axes.fill_between()`填充两条线之间的区域
- [`gridspec.GridSpec()`](https://matplotlib.org/tutorials/intermediate/gridspec.html) 定义子图, 实现子图跨越分区

## 直播汇总 & 答疑汇总

- [Baseline + Task1- 赛题理解](https://tianchi.aliyun.com/course/video?liveId=41143) ([ppt](/ppt/天池直播-Baseline及赛题理解.pdf))
- [Task2 - EDA](https://tianchi.aliyun.com/course/video?liveId=41143) ([ppt](/ppt/天池直播-EDA.pdf))
- [Task3 - 特征工程](https://tianchi.aliyun.com/course/video?liveId=41145) ([ppt](/ppt/天池直播-特征工程.pdf))
- [Task4 - 建模调参](https://tianchi.aliyun.com/course/video?liveId=41146) ([ppt](/ppt/天池直播-模型构建及预测.pdf))
- [Task5 - 模型融合](https://tianchi.aliyun.com/course/live?liveId=41149) (ppt) #TODO
- [石墨答疑汇总](https://shimo.im/docs/HgcgKvDQTQx3gCWd)

## 参考资料

Datawhale开源学习资料：https://github.com/datawhalechina/team-learning 

天池比赛论坛：https://tianchi.aliyun.com/competition/entrance/231784/forum



