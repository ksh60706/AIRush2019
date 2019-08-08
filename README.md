# AIRush2019
Line AIRush2019 repository

# NSML 실행
### cmd 실행

```
nsml login
```

### 깃헙 아이디와 비밀번호 입력

완료되면 

https://airush.nsml.navercorp.com/ 접속



# LINE sticker Image Classification

### 1. Usage

#### How to run

```
nsml run -d airush1
```

#### How to check session logs
```
nsml logs -f nsml logs -f nsmlteam/airush1/1
```

#### How to list checkpoints saved
You can search model checkpoints by using the following command:
```
nsml model ls nsmlteam/airush1/1
```

#### How to submit
The following command is an example of running the evaluation code using the model checkpoint at 10th epoch.
```
nsml submit -v nsmlteam/airush1/1 1
```

#### How to check leaderboard
```
nsml dataset board airush1
```






Note : By participating in the competition, you agree to handle problem content and data according to the [AI RUSH 2019 Information Handling Guidelines](https://github.com/ai-rush-2019/Information-Handling-Guidelines). 

---

# Problem1 : image classification
## Overview
About 700,000 [LINE sticker](https://store.line.me/stickershop/home/user/en) images are manually classified by 350 tags that indicate their characteristics.
Build a model that can predict one tags for each sticker image.

## Data
### File descriptions
-	images - directory that stores sticker images Format: images/{package_id}/{sticker_id}.png

![image](https://user-images.githubusercontent.com/4004593/62457739-5e90f580-b7b6-11e9-96fb-10c4abae39f1.png)

-	train_with_valid_tags.csv - train_set meta info which is mapping images_dir and tags

![image](https://user-images.githubusercontent.com/4004593/62457778-6e103e80-b7b6-11e9-86a9-b135471bba33.png)

### Data fields
- train_with_valid_tags.csv
  -	package_id - ID assigned to packages containing multiple sticker images
  -	sticker_id - ID of each sticker image
  -	tags - data of comma-delimited tags

- tag.tsv (train/train_data/tag.tsv)
  -	tag - tag ID
  -	keywords - multilingual keywords corresponding to each tag (some tags only exist in certain languages)
  -	languages - languages of keywords corresponding to each tag
  -	name - tag name

## Evaluation	
### Metric
There are multiple tags but in test case(1\~3), the first one is only used as a true label.<br>
So in training case it is free to use the all tags, but the test data has only one tag label among 1\~3 tags.<br>
The test tag label is selected by np.argmax as the baseline code does, so there could be a bias to the left side(not proven).<br>
And submitted data will be evaluated based on accuracy.

### Submission File Format
Be careful not to shuffle the index order.<br>
Submission file is a numpy array which has a shape of (138343)<br>
ex) array([ 65, 121, 56, ..., 316, 249, 15])

