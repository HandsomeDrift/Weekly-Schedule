# A Novel ECG-Based Deep Learning Algorithm to Predict Cardiomyopathy in Patients With Premature Ventricular Complexes

## 摘要

**背景**：早期心室复合搏动（PVCs）是常见的，虽然通常是良性的，但可能导致PVC诱导的心肌病。我们创建了一种深度学习算法，以从12导联心电图（ECG）中预测PVC患者的左心室射血分数（LVEF）下降。

**目标**：本研究旨在评估一种深度学习模型，以预测PVC患者中的心肌病。

**方法**：我们使用了来自5家医院的电子病历，识别出有记录的PVC成人的ECG。内部训练和测试在一家医院进行，外部验证在其他医院进行。主要结果是6个月内首次诊断LVEF降低至40%或以下。数据集中包含383,514个ECG，最终分析了14,241个。我们分析了受试者工作特征曲线下面积（AUC）以及代表性患者的可解释性图，算法预测，PVC负荷和多变量Cox模型中的人口统计学数据，以评估心肌病的独立预测因子。

**结果**：在14,241名患者的队列中（年龄67.6 ± 14.8岁；女性43.8%；白人29.5%，黑人8.6%，西班牙裔6.5%，亚裔2.2%），22.9%的患者在6个月内经历了LVEF降低至40%或以下。模型的预测表现良好，LVEF降低至40%或以下的AUC为0.79（95% CI：0.77-0.81）。梯度加权类别激活图的可解释性框架强调了窦性心律中的QRS波复杂-ST段。在接受成功PVC消融的患者中，绝大多数（89%）患者在消融后LVEF改善，心肌病得到缓解。

**结论**：仅基于12导联ECG的深度学习能够准确预测PVC患者中新发心肌病的发生，与PVC负荷无关。模型预测在性别和种族间表现良好，依赖于窦性心律中的QRS波复杂/ST段，而非PVC的形态。

## 引言

室性早搏（PVC）是心室心肌的早期去极化，在 12 导联心电图（ECG）和 Holter 监测中，室性早搏（PVC）的发生率分别为普通成年人的 1%至 4%和 40%至 75%。虽然最初被认为是良性的，但在 20 世纪 90 年代，我们对 PVC 诱导的心肌病（PVC-CM）这一概念有了新的认识--特发性心肌病患者通过药物抑制 PVC，左室射血分数（LVEF）有所改善。4 大量研究表明，PVC 负荷与左心室功能障碍的程度略有相关，可用于对可能发展为 PVC-CM 的患者进行风险分级5-7。在转诊消融的高 PVC 负荷患者中，PVC-CM 的发生率约为 33%，导致 PVC-CM 的最低 PVC 负荷为 10%。7 然而，一些高 PVC 负荷患者的射血分数（EF）并未下降，而另一些低 PVC 负荷患者则发展为 PVC-CM。7,10 在因 PVC 引起的心肌病患者中，82% 接受导管消融术的患者在 6 个月内 LVEF 恢复正常11。理想的筛查策略应结合常规临床实践中容易获得的临床信息。

卷积神经网络是深度学习（机器学习和人工智能的一个子集）的架构基础，经常被用于基于图像的心电图分析，以进行预测和识别重要特征，这反过来又被证明可以教给临床医生。虽然深度学习已被用于根据 12 导联心电图近似确定 PVC 的起源部位，但将其用于对可能从医疗干预中获益的 PVC 患者进行风险分层的数据却很少。为此，我们研究了使用深度学习算法预测 PVC 患者 LVEF 降低的可能性，该算法仅基于 12 导联心电图--一种价格低廉、随时可用且经常进行的检查。

## 方法

### 数据来源

我们使用了西奈山医疗系统内 5 家医院的心电图数据。这些医院，即西奈山医院、西奈山晨兴医院、西奈山西区医院、西奈山贝斯以色列医院和西奈山皇后区医院，为纽约市大量人口和社会经济多样化的人群提供服务。西奈山医院的数据用于模型训练和测试，而所有其他机构的集合数据则用于外部验证。

根据相关医生确认的 PVC 诊断，从 GE MUSE 系统中提取心电图数据。从电子病历中提取 LVEF 值、临床记录和《国际疾病分类-第 10 次修订》（ICD10）代码，并根据唯一的患者标识符与心电图相关联。机构审查委员会对研究的进行进行了审批和伦理监督。

### 纳入和排除标准

年龄在18岁及以上的患者必须有一系列ECG，其中至少有一个需要显示医生证实的PVC，初始超声心动图LVEF正常，随访超声心动图。从第一次ECG到纳入正常超声心动图的时间不能超过6个月。由于患者在该时间范围结束时超声心动图最终正常，在预测模型中，假定LVEF正常，排除起搏心律和室性心动过速的ECG，排除任何时间有与心肌梗死或急性冠状动脉综合征相关的ICD-10编码的患者，即使在初次超声心动图检查时不存在。

### pvc 负担和消融

为了明确结果的来龙去脉，我们对算法标记为阳性的患者进行了人工复查，以评估是否存在巧合的PVC消融。对患者层面的数据进行了人工审核，包括笔记、扫描监护仪报告、消融程序报告以及（如适用）设备询问数据。Joshua Lampert 博士和 Vivek Reddy 博士进行了人工审核。在结果数据的解释或报告方面没有分歧。

### 数据预处理

心电图数据由 XML 文件组成，其中包含 I、II 和 V1-V6 导联的波形数据。其余导联（III、aVF、aVL 和 aVR）被称为 “衍生导联”，因为它们只包含其他导联的信息。应用==巴特沃斯带通滤波器==对心电图波形进行降噪处理，然后再进行==中值滤波==。结果波形数据被绘制成图像，以便使用==二维卷积神经网络==。

我们创建了一个基于规则的自然语言处理管道，用于解析临床记录中的PVC负荷，这些负荷是从非卧床贴片监护仪和 Holter 监护仪记录中获得并计算出来的。我们创建了正则表达式，根据与相关表达式的接近程度提取以百分比表示的任何数字。提取的值再次根据唯一的患者标识符与心电图配对。

对于有记录的 PVCs 患者，我们检查了首次低 LVEF（以 40% 或 50% 为临界值）的情况。在诊断出低 LVEF 后，如果患者发生了 ICD-10 确诊的心肌梗死，或者首次记录的 LVEF 值低于临界值，则患者数据将被丢弃。

### 主要成果的定义

如果PVC患者发生心肌病（定义为在ECG日期后6个月内LVEF下降至临界值以下），则ECG标记为结果阳性。由于结果变量只有2种可能的状态，因此该任务可视为二元分类问题。

### 模型开发和评估

我们选择了==最大的可用预训练ResNet模型（ResNet-152）==作为分析的起点。==使用在自然图像上预训练的模型==可以以更少的数据获得更好的性能，同时还需要更少的时间来实现最佳解决方案。

数据基于==组洗牌分割==进行分割，通过确保训练组和测试组中没有患者来==消除数据泄漏的可能性==。我们选择使用Adam优化器，学习率为3e-4，OneCycle学习率计划。模型训练了35个epoch，并在内部测试数据上报告了性能最佳的epoch。所得模型也分别在外部验证数据上进行了评估。==我们使用学习率调度以及持续记录损失和性能指标，以实现模型的最佳拟合。==当模型性能开始恶化时，停止训练（发生过拟合）内部队列是指西奈山医院的患者，而外部队列由外部队列组成。验证数据集从其他4家附属医院的合并患者中获得。

我们使用受试者工作特征曲线下面积（AUROC）和精确召回曲线下面积（AUPRC）指标来评估模型性能，这些指标使用模型输出的未校准概率估计值来生成曲线，这些曲线表示模型区分阳性和阴性的能力。

为所有识别出PVC负荷的患者生成校准的考克斯比例风险模型，图2续JACC：临床电生理学第9卷，第8期，2023年Lampert等人，2023年8月：1437 - 1451深度学习预测PVC心肌病1441通过自然语言处理来评估年龄、性别和PVC负荷作为协变量的背景下的模型性能。正模型输出（人工智能阳性[AI]）被定义为80%概率模型输出，用于将射血分数降低至<50%，我们使用保序回归对神经网络的输出进行校准。

### 可解释性

我们使用梯度加权类激活映射（GradCAM）方法生成类激活映射。这些映射显示了ECG的哪些区域是最负责将模型推向预测的区域。为了进一步评估算法预测，我们提取了模型预测随后LVEF受损的患者，其概率为80%，通过检查急性失血性贫血进行消融术的特异性。然后，由电生理学家进行手动图表审查。我们排除了没有随访的患者-我们通过采集心电图、监护仪和设备询问（包括电描记图），在随访时确定是否存在室性早搏。我们使用配对双尾Student t检验评估接受PVC消融术患者的EF变化。

### 软件和硬件

我们在自定义虚拟环境中使用numpy、pandas、scipy、scikit-learn、PyTorch和torchvision库进行分析。我们使用matplotlib和seaborn库进行绘图。所有代码都是为Python编程语言（3.8.x）编写的。

### 代码可用性

代码将在发布时提供