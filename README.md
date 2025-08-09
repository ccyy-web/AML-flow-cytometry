# AML Flow Cytometry Classification

## 项目简介

本项目基于来自 [FlowRepository FR-FCM-ZZYA](https://flowrepository.org/id/FR-FCM-ZZYA) 的急性髓系白血病（AML）流式细胞数据，构建并比较多种机器学习模型在患者与健康对照分类任务中的表现。

## 数据说明

- **原始数据格式**：`.fcs`
- **预处理特征**：83 个统计特征（均值与标准差）
- **标签**：1 = AML 患者，0 = 健康对照

## 方法

1. **数据预处理**：使用 `FlowCytometryTools` 提取特征。
2. **模型比较**：Logistic Regression、Random Forest、SVM、KNN、XGBoost。
3. **评估指标**：Accuracy、Precision、Recall、F1、AUC。
4. **可视化**：ROC 曲线、混淆矩阵、UMAP。

## 结果

### 测试集表现

| Model               | Accuracy | Precision | Recall | F1    | AUC   |
| ------------------- | -------- | --------- | ------ | ----- | ----- |
| SVM                 | 0.945    | 1.000     | 0.556  | 0.714 | 0.993 |
| Logistic Regression | 0.959    | 1.000     | 0.667  | 0.800 | 0.988 |
| Random Forest       | 0.918    | 0.800     | 0.444  | 0.571 | 0.979 |
| XGBoost             | 0.945    | 1.000     | 0.556  | 0.714 | 0.976 |
| KNN                 | 0.904    | 1.000     | 0.222  | 0.364 | 0.874 |

### 交叉验证表现

| Model               | AUC      | Avg Precision |
| ------------------- | -------- | ------------- |
| SVM                 | 0.993671 | 0.969697      |
| Logistic Regression | 0.992641 | 0.981319      |
| Random Forest       | 0.976045 | 0.938236      |
| XGBoost             | 0.974389 | 0.927180      |
| KNN                 | 0.960627 | 0.893833      |

**结论简述**

- SVM 和 Logistic Regression 在 **AUC** 上都接近 0.993，性能非常稳定。
- Logistic Regression 在 **平均精确率** 上略优（0.9813）。
- 随机森林和 XGBoost 性能次之，但仍然表现良好。
- KNN 相对较弱，尤其在召回率方面。

## 结论

AML 流式细胞数据中包含明显的判别信号，机器学习模型可实现高精度分类。未来优化方向应侧重提升召回率以减少漏诊。