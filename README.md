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
- Ran the code on CPU/
2. Google Cloud Platform
- Debian 10.12
- a2-highgpu-1g (vCPU x 12, memory 85 GB)
- 1 x NVIDIA Tesla A100
- Ran the code on GPU/

## Data download
Plese download data to `./CPU/data` and `./GPU/data` from https://www.kaggle.com/competitions/foursquare-location-matching/data and unzip it.

## Environment
Please execute the following command ./GPU and ./CPU directory.
```
$ docker-compose up --build
```

### Our code consists of 4 stages. Please run the code.
For those that need to be uploaded to kaggle dataset to be used for submission, I have marked them as submission.</br>
 As for Train, note that there is one for evaluation with train data and one for submission. The evaluation version is trained with cross validation (n_splits = 2), and the submission version is trained with all data.
## 1st Stage
- Create candidate pairs using latitude and longitude
    - Feature engineering</br>
        ``` ./CPU/fe/fe035_near100_feature.ipynb ```</br>

        ``` ./CPU/fe/fe042_near100_feature.ipynb ```
    - Train LightGBM</br>
        fold 0,1</br>
        ```./CPU/exp/ex037_stage1_fold_0_1.ipynb ```</br>

        all data</br>
        ``` ./CPU/exp/ex073_stage1_all.ipynb ``` (submission) </br>
        
- Create candidate pairs using name
    - Feature engineering</br>
        ``` ./GPU/fe/fe029_foursquare_bert-base-multilingual-uncased.ipynb ``` </br>

        ``` ./GPU/fe/fe054_near100_feature_bert_base.ipynb ```</br>
    
      Plase copy ```"./GPU/output/fe/fe054/fe054_100_name_emb_near.pkl"``` to ```"./CPU/output/fe/fe054/fe054_100_name_emb_near.pkl"```

        ``` ./CPU/fe/fe065_make_distance_100.ipynb  ```
    - Train LightGBM</br>
        fold 0,1</br>
        ``` ./CPU/exp/exp061_stage1_fold_0_1.ipynb ```</br>
        
        all data</br>
        ``` ./CPU/exp/exp074_stage1_all.ipynb ``` (submission) </br>

## 2nd stage
- Feature engineering</br>
     ``` ./CPU/fe/fe045_2nd_categorical_feature.ipynb ``` (submission)</br>

    ```./CPU/fe/fe066_make_distance_2nd_stage.ipynb ```</br>

    ```./CPU/fe/fe067_2nd_stage_distance_agg.ipynb```</br>

    ```./CPU/fe/fe068_2nd_categorical_feature.ipynb```</br>

    Plase copy ```"./GPU/output/fe/fe029/bert_base_multilingual_embedding.npy"``` to ```"./CPU/output/fe/fe029/bert_base_multilingual_embedding.npy"``` and copy ```"./GPU/output/fe/fe029/name.npy"``` to ```"./CPU/output/fe/fe029/name.npy"```

    ```./CPU/fe/fe046_2nd_stage_emb_svd.ipynb``` (submission)</br>

    ```./CPU/fe/fe069_2nd_stage_emb_svd.ipynb```</br>
- Train LightGBM</br>
    fold 0</br>
    ```./CPU/exp/exp062_2nd_stage_fold0.ipynb```</br>

    fold 1</br>
    ```./CPU/exp/exp063_2nd_stage_fold1.ipynb```</br>
    
    all data</br>
    ```./CPU/exp/exp075_2nd_stage_all.ipynb``` (submission)</br>

- Data preparation for 3rd stage
    ```./CPU/exp/exp062[save]_for_3rd_stage.ipynb```</br>

    ```./CPU/exp/exp062[save_fe]_for_3rd_stage.ipynb```</br>

    ```./CPU/exp/exp063[save]_for_3rd_stage.ipynb```</br>

    ```./CPU/exp/exp063[save_fe]_for_3rd_stage.ipynb```</br>

    Plase copy ```"./CPU/output/exp/ex062/ex062_pred.csv"``` to ```"./GPU/output/exp/ex062/ex062_pred.csv"``` and copy ```"./CPU/output/exp/ex062/ex062_fe.csv"``` to ```"./GPU/output/exp/ex062/ex062_fe.csv"``` and copy ```"./CPU/output/exp/ex063/ex063_pred.csv"``` to ```"./GPU/output/exp/ex063/ex063_pred.csv"``` and copy ```"./CPU/output/exp/ex063/ex063_fe.csv"``` to ```"./GPU/output/exp/ex063/ex063_fe.csv"```.

## 3rd stage
In the 3rd stage, I only trained fold0 and all data. 3rd stage was validated using fold0 only.
- Train Catboost </br>
    fold 0</br> 
    ```./CPU/exp/exp087_3rd_stage_catboost.ipynb```</br>

    all data </br>
    ```./CPU/exp/exp090_3rd_stage_catboost_all.ipynb``` (submission)</br>

    Plase copy ```"./CPU/output/exp/ex087/ex087_pred.csv"``` to ```"./GPU/output/exp/ex087/ex087_pred.csv"```


- Train xlm-roberta-large </br>
    fold 0</br>
    ```./GPU/exp/exp100_roberta_large_fold0.ipynb```</br>

    all data</br>
    ```./GPU/exp/exp104_roberta_large_val0.ipynb``` (submission)

- Train mdeberta-v3-base</br>
    fold 0 </br>
    ```./GPU/exp/exp_charm_05_mdeberta_fgm_fold0.ipynb```</br>

    all data</br>
    ```./GPU/exp/exp115_mdeberta_fgm_ema_all.ipynb.ipynb``` (submission)</br>

## 4th stage
In the 4th stage, I only trained fold0 and all data. 4th stage was validated using fold0 only.
- Train xlm-roberta-large </br>
    fold 0 </br>
    ```./GPU/exp/exp070_roberta_large_fold0.ipynb```

    all data </br>
    ```./GPU/exp/exp101_roberta_large_all.ipynb``` (submission)

- Ensemble + PostProcess</br>
    ```./GPU/exp/exp113[ensemble_pp].ipynb```</br>
         I used the weight of the ensemble in my submission.
    
    ```./GPU/exp/exp113[pp_inference]_roberta_large_fold0.ipynb```</br>

    ```./GPU/exp/exp113[pp_final]_pp_pred.ipynb```</br>
        I used this notebook's threshold as a reference for the submission threshold.








    








