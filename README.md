# Data _science_Bowl 

-----------------------------------------------------------------------------------------

# key for the competition 
- 생소한 game play 데이터를 사용하기 때문에 데이터에 대한 이해가
쉽지 않음.
- target값은 0.1,2,3으로 되어 있기 때문에 classification을 baseline으로 
생각했으나, 많은 사람들이 regression도 사용함을 확인함 
-  feature selection은 top k best feature을 null importance를 통해 
추출했다. 
- SOTA 모델들을 ensembling한 model을 사용하는 것이 optimal approach
라고 생각함. 또한 boosting model을 사용하는 것이 tabular데이터를 다루는데
가장 선호되는 방법이며, neural network를 사용하는 것도 다른 관점으로 확인이 
가능했다. 


# abount competition
- PBS KIDS app은 아이들이 학교생활과 라이프스타일에 대해 학습을 시킬 수 있는
신뢰도 있는 게임이다. 
- 이 대회에서는 각 아이들의 데이터를 주고, 게임에서 평가의 score을 예측하도록 하는 것이다. 
- 이 솔루션은 support discovering important relationships between different types of
high-quality educational media and learning process.

# approach
**1. validation strategy**
- K=5로 하여 KFold group을 installation_id를 기반으로 그룹지었다. 

**2. feature engineering8**
- world를 numerical 형태로 바꿔줬다. 
- add corresponing world of assesment 
- accumulated number of different previous assessment
- add duration_std along with duration_mean
- add accumulated_assesment_attemps
- add combination of session_title_code of an assessment with corresponding
accuracy_group assessment_accuracy_map
- add clip/activity/game duration mean and std
- no need to feature scaling as tree_based models are not affected by
different scales of features.

**3. feature selection**
- eliminate high correlated features ( >0.99 correlated coeff)

**4. modeling** 
- ensemble LightGBM, XGBoost, CatBoost, and Neural Network
with 0.25 weighted each.