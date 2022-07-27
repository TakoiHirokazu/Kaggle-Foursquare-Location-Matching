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

### Our code consists of 4 stages. Please run the code.
For those that need to be uploaded to kaggle dataset to be used for submission, I have marked them as submission.</br>
 As for Train, note that there is one for evaluation with train data and one for submission. The evaluation version is trained with cross validation, and the submission version is trained with all data.
## 1st Stage
- Create candidate pairs using latitude and longitude
    - Feature engineering</br>
        ``` ./CPU/fe/fe035_near100_feature.ipynb ```</br>

        ``` ./CPU/fe/fe042_near100_feature.ipynb ```
    - Train</br>
        ```./CPU/exp/ex037_stage1_fold_0_1.ipynb ```</br>
        
        ``` ./CPU/exp/ex073_stage1_all.ipynb ``` </br>
        submission
- Create candidate pairs using name
    - Feature engineering</br>
        ``` ./GPU/fe/fe029_foursquare_bert-base-multilingual-uncased.ipynb ``` </br>

        ``` ./GPU/fe/fe054_near100_feature_bert_base.ipynb ```</br>
    
      Plase copy "./GPU/output/fe/fe054/fe054_100_name_emb_near.pkl" to "./CPU/output/fe/fe054/fe054_100_name_emb_near.pkl"

        ``` ./CPU/fe/fe065_make_distance_100.ipynb  ```
    - Train </br>
        ``` ./CPU/exp/exp061_stage1_fold_0_1.ipynb ```</br>

        ``` ./CPU/exp/exp074_stage1_all.ipynb ```</br>
            submission
## 2nd stage
Please run the following all notebooks.

- Feature engineering</br>
     ``` ./CPU/fe/fe045_2nd_categorical_feature.ipynb ```</br>
        submission

    ```./CPU/fe/fe066_make_distance_2nd_stage.ipynb ```</br>

    ```./CPU/fe/fe067_2nd_stage_distance_agg.ipynb```</br>

    ```./CPU/fe/fe068_2nd_categorical_feature.ipynb```</br>

    Plase copy "./GPU/output/fe/fe029/bert_base_multilingual_embedding.npy" to "./CPU/output/fe/fe029/bert_base_multilingual_embedding.npy" and copy "./GPU/output/fe/fe029/name.npy" to "./CPU/output/fe/fe029/name.npy"

    ```./CPU/fe/fe046_2nd_stage_emb_svd.ipynb```</br>
        submission

    ```./CPU/fe/fe069_2nd_stage_emb_svd.ipynb```</br>
- Train</br>
    ```./CPU/exp/exp062_2nd_stage_fold0.ipynb```</br>

    ```./CPU/exp/exp063_2nd_stage_fold1.ipynb```</br>
    
    ```./CPU/exp/exp075_2nd_stage_all.ipynb```</br>
        submission




