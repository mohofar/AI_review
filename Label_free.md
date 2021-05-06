

## Paper steps
1. Clip the raw image using HU in a range of [−800, 100] and scale the clipped image to [0, 1]
2. Creating mask using nnUnet [55]
3. Voxel-wise multiplication of steps 1 and 2
4. Remove erroneous edges
5. Synthetic ‘lesion’ generation 
6. Adding to healthy images
7. NormNet is applied
8. Because our training process is random, we form an ensemble by learning five random models under the same setting.
9. Post-processing procedure --what--> grow the localized lesion areas --why--> As NormNet is trained to segment the voxels with HU≥ T , a small number of lesion voxels whose HU< T are not taken into consideration and might get missed.

## Method

![1_1](https://user-images.githubusercontent.com/25353688/117303014-7d438500-ae91-11eb-9534-5ebf2c47ec4d.PNG)
Fig.1
![1_2](https://user-images.githubusercontent.com/25353688/117312619-6b1a1480-ae9a-11eb-8dad-144a8f78dc7e.PNG)
![1_3](https://user-images.githubusercontent.com/25353688/117312709-8127d500-ae9a-11eb-8acf-811bbba864f5.PNG)
![1_4](https://user-images.githubusercontent.com/25353688/117312714-838a2f00-ae9a-11eb-8425-7584c7933d1b.PNG)

## Conclusion
In this paper, we proposed the NormNet, a voxel-level anomaly modeling network to recognize normal voxels from possible anomalies. A decision boundary for normal contexts of the NormNet was learned by separating healthy tissues from the diverse synthetic ‘lesions’, which can be further used to segment COVID-19 lesions, without training on any labeled data. The experiments on three different COVID-19 datasets validated the effectiveness of the NormNet.

Despite the improvement compared to existing unsupervised anomaly detection methods, there was still a gap between our methods and supervised methods such as nnU-Net [55]. After exploring the failure predictions of our methods, we found that they were divided into three categories: 
1. The NormNet segments all anomalies such as pulmonary fibrosis (the first row shown in Fig. 9), rather than COVID-19 lesions only. 
2. Gaps between datasets: for example, most of the layer thicknesses in Luna16 dataset are around 1mm. However, in Radiopedia dataset slices were padded together, which generated different contexts. The unseen contextsYAO et al.: LABEL-FREE SEGMENTATION OF COVID-19 LESIONS IN LUNG CT 11 were treated as anomalies by our NormNet, which resulted in the most of false-positives in Radiopedia.
3. Our NormNet gave up modeling the noisy patterns in low-intensity range. Although most of lesions can be successfully detected, a small part of lesions with their intensity smaller than τ were still missed (as shown in the right column of Fig. 9). Segmenting these small lesions also serves as a difficult problem for both supervised methods [15] and anomaly detection.

---
## Lets review
