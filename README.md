# Additional answers for rebuttal


## Visual comparison with and without rotation strategy

We conducted a visual comparison of whether to use the rotation strategy. We chose to migrate from FFHQ to Amedeo as the experimental setting. The results are shown in the figure below.

![Vis_comparison](5.png)

It is evident that without applying rotation, the generated results tend to overfit, closely matching the tonal and expressive characteristics of the target domain training set. In contrast, with the addition of rotation, the generated images exhibit distinct features from the source domain, such as skin tone. This demonstrates the beneficial impact of rotation on the quality and diversity of the generated outcomes.


## Proof of the two problems mentioned in the introduction

We conducted additional experiments on FFHQ to Babies domain. We selected different data as reference datasets for calculating evaluation metrics. We selected FID as the evaluation metric. The experimental results are shown in the following table.

| Method  | Source domain dataset | Target domain train dataset | Target domain test dataset |
|---------|-----------------------|-----------------------------|----------------------------|
| MineGAN | 95.36                 | 27.53                       | 87.48                      |
| RSSA    | 45.32                 | 65.77                       | 66.81                      |
| Ours    | 50.67                 | 36.25                       | 37.16                      |

The few-shot generation task involves fine-tuning a model, initially trained on a source domain dataset, using a limited amount of target domain training data. As a result, evaluating the model with the source domain dataset would reveal underfitting, while using the target domain training set as a test reference risks overfitting to these specific samples. The appropriate evaluation is on the target domain test dataset, where strong performance indicates effective generalization. As shown in the table above, RSSR exhibits underfitting, while MineGAN suffers from severe overfitting. Only our approach achieves satisfactory performance.