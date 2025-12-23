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
|    |__0/(train_set.csv, test_set1.csv, test_set2.csv, test_set3.csv with video names and groundtruth mos values)
|    |__...
|    |__9/(train_set.csv, test_set1.csv, test_set2.csv, test_set3.csv with video names and groundtruth mos values)
|
|__all_descriptions_en.csv (Original annotations 140,000 rows, and columns include video names, opinion scores, descriptions in Chinese, and descriptions in English)
```

## The prompts for obtaining catergorization of description sentences
We employed ChatGPT-o3, a powerful OpenAI large model for reasoning, to analyze the distribution of described places, artifacts, and extents. 
After careful prompting, checking, and re-prompting, we ended up with 14 categories of places, 19 categories of artifacts, and 4 categories of extents, 
and their ratios to the total number of descriptions in the dataset are obtained.   
The prompts we used are shown [here](./Prompts_categorization.md).
