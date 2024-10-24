# Deep Learning for Premature Ventricular Contraction-Cardiomyopathy Are We Digging Deep Enough

室性早搏（PVC）非常普遍，在高达75%的接受霍尔特监测的患者中具有特征。1室性早搏的丰富程度可能是左心室（LV）功能障碍严重程度的预兆。2对室性早搏介导的心肌病（PVC-CM）的理解仍处于初期阶段，因为并非所有频繁发生室性早搏的患者最终都会发展为PVC-CM。以下几个因素-例如总PVC负荷、心外膜病灶、正常和PVC搏动之间的短偶联间期、LV不同步、房室分离和期外收缩后增强-已经被推测为预测PVC-CM的发展。3-5然而，关于风险分层的共识仍然难以捉摸。对高PVC计数的无症状患者的管理仍然模糊，充满了潜在的临床意义，从药物干预和导管消融到监测，所有这些都具有进行性心力衰竭的基础风险。

人工智能（AI）的出现促进了电生理学实践的范式转变。7人工智能方法（如机器学习和深度学习）已被集成到各种应用中，包括心律失常检测、异常分类、风险分层、8这些人工智能框架采用了大量的心电图（ECG）数据集，人工智能算法已经显示出超越人类诊断能力的潜力。深度学习模型已经被设计用于使用12导联ECG检测收缩功能障碍，但仍不确定这些模型是否同样适用于PVC的ECG。9这个问题需要进一步探索，因为它在PVC-CM的检测和管理中具有巨大的潜力。

在本期JACC中：临床电生理学，Lampert等人10报告了他们基于深度学习模型进行的研究结果，该模型采用12导联ECG输入来预测ECG上记录的PVC患者的心肌病。该预测模型的训练在一个单独的中心进行，并应用于4个额外的设施，以进行外部验证。左心室射血分数（LVEF）从ECG检查后6个月内的超声心动图中获得数值。在索引ECG检查前LVEF异常的患者被忽略。来自单个中心的13,553名患者的ECG被用于训练模型，来自688名患者的数据用于外部验证。主要结局是LVEF $\leq$40%的诊断Lampert等10报道他们的模型预测主要结果，受试者工作特征曲线下面积为0.79。梯度类激活图评估用于分析模型的可解释性，并且它强调了窦性心律QRS波群而不是PVC搏动。Lampert等人10得出结论，该模型可以准确预测PVC患者的心肌病，而不管他们的PVC负担如何。在随后的文章中，我们将试图提供一些关于这一重要研究的发人深省的方面的观点

## 在检测PVC-CM时，我们是否可以保证？

对于在12导联心电图上检测到1个或多个PVC的无症状患者，潜在频谱从完全良性的特发性PVC到那些有诱发心肌病倾向的PVC。12导联ECG的成本效益和可及性使其成为筛查PVC诱导的心肌病的一种引人注目的模式。先前的模型报告了12导联ECG的出色LVEF预测能力，但并未排除PVC患者。9因此，PVC ECG的独特模型的必要性引起了争论。广泛地说，在这种情况下，一致认为为特定人群制作的模型应该在相同的表现出PVC的患者上训练以检测PVC-CM。但是我们真的检测到PVC-CM吗？

Lampert等人10优雅地展示了窦性QRS波群似乎比PVC搏动本身具有更多的相关信息。因此，我们正在开发在检测亚临床CM方面表现良好的模型是合理的，但我们需要前瞻性招募和随访来确信我们确实是专门挑选PVC-CM。在当前的研究中，少数患者（n = 15）在消融术后有随访LVEF数据，60%的患者LVEF恢复。Lampert等10报道，其余患者消融术失败;但是，在此情况下，需要更大的样本来巩固这一论点。正在进行的调查的一个途径是将该模型应用于ECG上的相同患者，研究正在评估接受PVC消融术和LVEF恢复的患者，他们应该询问AI-ECG低LVEF预测恢复正常需要多长时间。

## 模型输入应该是矩阵还是图像？

针对涉及图像的任务的最流行的深度学习模型使用2维（2D）或3D卷积神经网络来执行分类或分割等任务。ECG被认为是2D图像，因为存在针对时间（x轴）绘制的幅度轴（y轴）。因此，训练用于ECG分析的2D卷积神经网络模型具有直观意义。然而，对于时间序列数据，我们可以通过将ECG数据作为矩阵输入并训练1D卷积神经网络来节省计算资源，而性能没有任何下降，因为存在于2D图像中的所有信息已经存在于1D信号中。对于ECG，一种方法是将每个样本作为输入(number of samples = sampling frequency $\times$ time).9这种技术允许我们在其他地方分配计算资源，并优选地训练更大的数字以构建更鲁棒的模型。Lampert等人10确实==从ECG波形数据开始，但后来将其绘制为图像==。==尽管这种转换有助于人类理解，这是一个无关的步骤，无意中将人工智能限制在类似人类的处理上。将人工智能从这种人类-定向约束可能会导致更优化的结果。该转换以图像分辨率的形式引入了不必要的限制，并在ECG描记图周围生成多余的多余白色像素。因此，可以质疑这是否值得额外的计算量。==

## 这种深度学习模式适合广泛使用吗？

随着我们进入人工智能增强医学的时代，我们被大量的机器学习模型所淹没，这些模型有望改变我们的医学实践。我们主张在以下关键领域对每个模型进行严格审查：

1. 临床实用性和安全性：目前的模型具有巨大的临床应用潜力，有望识别有发生CM风险的PVC患者。因此，它可以影响早期干预并积极改善结局。在开发此类模型的同时保持患者机密性至关重要。尽管存在局限性，Lampert等10报告了受试者工作特征曲线下的可观区域为0.79，精确度召回率曲线下面积为0.50，这对于低事件率的模型来说是很好的。外部数据集优于训练集是非常有趣的，需要进一步探索以排除可能限制模型泛化的显著方差。在大数据时代，我们可以同意，通过数据共享实现的更大样本可能是提高模型性能的最佳方式，并且在我们将模型应用于临床实践之前可能至关重要。
2. 健康公平和偏见：Lampert等人10==纳入多种族患者队列的努力值得称赞;==然而，超过一半的患者的种族未知。未来的模型可以建立在这些努力的基础上，也许有更大的样本，亚组分析可以排除未知种族的患者，以获得种族比较的准确想法。
3. 透明度：Lampert等人10尝试对具有梯度类激活的模型进行可解释性分析，地图评估，并报告了一个有趣的发现，该模型利用窦性QRS搏动来检测心肌病。这暗示着，这些作者使用没有任何PVC的ECG来评估训练模型预测未来心肌病的熟练程度可能是谨慎的。这是因为他们的假设是，室性心动过速引起的心室收缩可能导致一些亚临床结构变化，人类无法解释，但模型可以识别。这个概念并不陌生，因为它类似于我们如何使用窦性搏动来测量LVEF，而不是超声心动图上的室性心动过速。也就是说，亚临床CM已经发生，我们根本无法感知它。我们自然渴望理解机器是如何运作的，但实际上，我们永远不会实现这一点，因为，如果我们能破译它，计算机将永远不会超越我们。我们的视觉和大脑能力使我们无法通过模型进行特征识别。因此，尽管这是一个令人满意的智力练习，随着模型越来越复杂，我们应该克服这种自然倾向，只要模型表现良好，我们就应该接受它。

总之，Lampert等人10对困扰许多心脏病专家的临床难题做出了标记。随着模型的进一步完善，数据共享和前瞻性多中心研究，我们希望未来可以早期识别和治疗高风险的PVC患者。
