# Kaggle-Foursquare-Location-Matching
This is repository of the 1st place solution of [Kaggle Foursquare Location-Matching](https://www.kaggle.com/competitions/foursquare-location-matching).</br>
The discription of this solution is available [here](https://www.kaggle.com/competitions/foursquare-location-matching/discussion/336055).</br>
The prediction notebook in the competition is available [here](https://www.kaggle.com/code/takoihiraokazu/sub-ex73-74-75-ex104-115-90-101-merge-train3).

## Summary

## Hardware
I used two different machines.
1. Google Cloud Platform
- Debian 10.12
- n1-standard-64 (vCPU x 64, memory 240 GB)
- This machine ran the code on CPU/
2. Google Cloud Platform
- 

## Data download
Plese download data to `./CPU/data` and `./GPU/data` from https://www.kaggle.com/competitions/foursquare-location-matching/data and unzip it.

## Environment
Please execute the following command ./GPU and ./CPU directory.
```
$ docker-compose up --build
```

### Our code consists of 4 stages. Please run the code for each stage.
## 1st Stage
Please run the following notebooks.
- Create candidate pairs using latitude and longitude
    - Feature engineering</br>
        ``` ./CPU/fe/fe035_near100_feature.ipynb ```</br>
        ``` ./CPU/fe/fe042_near100_feature.ipynb ```
    - Train</br>
     ```./CPU/exp/ex037_stage1_fold_0_1.ipynb ```</br>
            - For evaluation with train data
      ``` ./CPU/exp/ex073_stage1_all.ipynb ``` </br>
            - For submission
- Create candidate pairs using name
    - Feature engineering
        - ./GPU/fe/fe029_foursquare_bert-base-multilingual-uncased.ipynb
        - ./GPU/fe/fe054_near100_feature_bert_base.ipynb
        - Plase copy "./GPU/output/fe/fe054/fe054_100_name_emb_near.pkl" to "./CPU/output/fe/fe054/fe054_100_name_emb_near.pkl" 
            - This is because memory is insufficient in GPU environment. 
        - ./CPU/fe/fe065_make_distance_100.ipynb
    - Train
        - ./CPU/exp/exp061_stage1_fold_0_1.ipynb
            - For evaluation with train data
        - ./CPU/exp/exp074_stage1_all.ipynb
            - For submission
## 2nd stage
Please run the following notebooks.
- 
- Feature engineering
    - ./CPU/fe/fe045_2nd_categorical_feature.ipynb
        - This outputs are used for evaluation as well as final submission.
    - ./CPU/fe/fe066_make_distance_2nd_stage.ipynb
    - ./CPU/fe/fe067_2nd_stage_distance_agg.ipynb
    - ./



