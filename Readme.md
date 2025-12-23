## The DREAM deepfake assessment dataset 
The dataset can be applied [here](https://docs.google.com/forms/d/e/1FAIpQLSc7GdEJAhCkqLkl_wydfSdywSh_EL0cb27Uct7aJMyM-Y3oyw/viewform?usp=dialog). It is available for research purposes only, and please input your institutional email address to recieve the dataset link.
```
Dataset structure
|__videos
|    |__C1/(280 muted videos)
|    |__C2/(560 muted videos)
|    |__C3/(680 muted videos)
|
|__splits
|    |__0/(train_set.csv, test_set1.csv, test_set2.csv, test_set3.csv with video names and groundtruth MOS values)
|    |__...
|    |__9/(train_set.csv, test_set1.csv, test_set2.csv, test_set3.csv with video names and groundtruth MOS values)
|
|__all_descriptions_en.csv (Original annotations 140,000 rows, and columns include video names, opinion scores, descriptions in Chinese, and descriptions in English)
```

## The prompts for obtaining catergorization of description sentences
We employed ChatGPT-o3, a powerful OpenAI large model for reasoning, to analyze the distribution of described places, artifacts, and extents. 
After careful prompting, checking, and re-prompting, we ended up with 14 categories of places, 19 categories of artifacts, and 4 categories of extents, 
and their ratios to the total number of descriptions in the dataset are obtained.   
The prompts we used are shown [here](./Prompts_categorization.md).

## External datasets
We employed two external datasets to test the generalization ability of different methods, and the annotation files are in the ``external_dataset`` folder. The FaceForensics++ (FF++) dataset [1] contains 100 videos sampled from the C23 quality subset of FF++, and we annotate each video with 10 annotators to obtain MOS values. The Q-Eval-100K dataset [2] contains 207 videos sampled from the original training set that includes human faces, and the MOS is also from the original dataset with each video annotated by at least three annotators.

[1] Rossler, Andreas, et al. "Faceforensics++: Learning to detect manipulated facial images." Proceedings of the IEEE/CVF international conference on computer vision. 2019.   
[2] Zhang, Zicheng, et al. "Q-eval-100k: Evaluating visual quality and alignment level for text-to-vision content." Proceedings of the Computer Vision and Pattern Recognition Conference. 2025.
