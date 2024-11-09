# Response to Review Ca32

We apologize for taking up your time. Due to limitations on response length and format, we have provided an additional link to further address your question. We sincerely appreciate your patience in reviewing it.

## Q3: Measurement of distribution rotation.

For better evaluation, we also visualize generated results w/ and w/o our rotation strategy as follows. 

![Vis_comparison](5.png)

We can see that without applying rotation, the generated results tend to overfit, closely matching the tonal and expressive characteristics of the target domain training set. In contrast, with the addition of rotation, the generated images exhibit distinct features from the source domain, such as skin tone. This demonstrates the beneficial impact of rotation on the quality and diversity of the generated outcomes.


## Q5: More intuitive evaluation.

To better demonstrate the existence of the two issues, we conduct additional experiments on FFHQ to Babies domain. We select different data as reference datasets for calculating evaluation metrics and utilize FID as the evaluation metric. The experimental results are shown in the following.

| Method  | Source domain dataset | Target domain train dataset | Target domain test dataset |
|---------|-----------------------|-----------------------------|----------------------------|
| MineGAN | 95.36                 | 20.53                       | 87.48                      |
| RSSA    | 41.32                 | 65.77                       | 66.81                      |
| Ours    | 50.67                 | 36.25                       | 37.16                      |


The few-shot generation task involves fine-tuning a model, initially trained on a source domain dataset, using a limited amount of target domain training data. As a result, evaluating the model with the source domain dataset would reveal underfitting, while using the target domain training set as a test reference risks overfitting to these specific samples. The appropriate evaluation is on the target domain test dataset, where strong performance indicates effective generalization. As shown in the table above, RSSR exhibits underfitting, while MineGAN suffers from severe overfitting. Only our approach achieves satisfactory performance. This conclusion is consistent to Figure 1 in our paper. MineGAN without local content consistency produces generative results that overfit to target samples, whereas RSSA, with excessive local pairwise similarity constraints, yields underfitted generative results. Existing local content consistency constraints contribute to a global distribution shift during training, potentially resulting in overfitting, while imposing overly strong consistency constraints on local pairwise generative samples may lead to underfitting in generated results.


## Further explanation: Visualized Analysis of the actual feature distribution

To further illustrate the actual effects of the two losses we proposed, we utilized the labels provided in the [FFHQ features dataset](https://github.com/DCGM/ffhq-features-dataset) as our reference. We visualize the feature distribution of our method on FFHQ dataset by t-SNE. Here, we utilize the labels provided in the FFHQ features dataset as our reference. Specifically, we selected three mutually exclusive classes—non-smiling, non-glasses-wearing females; smiling, non-glasses-wearing males; and non-smiling, glasses-wearing males. We compare the feature distribution of our method w/ and w/o our proposed two specific losses. 

![Tsne_comparison](tsne.png)

From the visualization results, we can see that when the local-scale self-adaptive rotation ($L_{ins}$) is not applied, the shape of the class changes. This indicates that without the local-scale constraint, the features within the class become more dispersed. When global-scale optimal distribution matching ($L_{dis}$) is not applied, the relationship between classes collapses. This indicates that without the global-scale constraint, the relationships between classes are affected. It significantly demonstrates that our proposed losses can achieve the goal we have claimed.