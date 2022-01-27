---
title: ML/TA Sentiment Analysis
date: 2022-01-26 00:00:01
categories:

- ML
tags:
- TA

---

# ML 감성분석(Sentiment Analysis)
감성분석은 문서의 주관적인 의견/감정/기분등을 파악하기 위한 방법으로 소셜미디어, 여론조사, 온라인리뷰, 피드백 등 다양한 분야에서 활용되고 있다. **감성분석은 문서내 텍스트가 나타내는 여러가지 주관적인 단어와 문백을 기반으로 감성 수치를 계산 하는 방법**을 이용한다. 감성지수는 긍정/부정으로 구성되며 이들을 합산해 긍정 감성 또는 부정 감성 을 결정한다.

감성분석은 머신러닝 관점에서 지도학습과 비지도 학습으로 나눌 수 있다.
- **지도학습**<Br>학습데이터와 타켓 레이블 값을 기반으로 감성분석 학습을 수행한뒤 이를 기반으로 다른 데이터의 감성 분석을 예측하는 방법으로 일반적인 텍스트 기반의 분류와 거의 동일함. `CountVectorizer`, `TfidfVectorizer`

- **비지도학습**<br>`Lexicon`이라는 일종의 감성 어휘 사전을 이용한다. `Lexicon`은 감성분석을 위한 용어와 문맥에 대한 다양한 정보를 가지고 있으며, 이를 이용해 문서의 긍정적 부정적 감성여부를 판단한다.

---

## Lexicon
Lexicon은 Positive, Negative 감성의 정도를 의미하는 감성지수(Polarity score)를 가지고 있다. <br>감성지수는 주변단어, 문맥, Part of Speech 를 참고해 결정된다. 

대표적인 감성사전은 다음과 같다.
- WordNet<br>다양한 상황에서 같은 어휘라도 다르게 사용되는 어휘의 semantic 정보를 제공한다. 이를위해 품사로 구별된 단어를 Synset(Set of cognitive synonyms;동의어세트)이라는 개념을 이용해 표현한다.

- SentiWordNet <br>WordNet의 Synset 개념을 감성분석에 적용한 것이다.
    ### Process
    1. 문서를 문장 단위로 분해
    2. 문장을 단어로 분해 후 토큰화&품사태깅
    3. 품사가 붙여진 단어를 기반으로 synset객체와 senti_synset 객체 생성
    4.  senti_synset에서 positive, negative 지수를 합산해 특정 threshold기준으로 긍정/부정 감성 판별


- VADER <br> 소셜미디어 텍스트에 대해 감성분석을 제공하기 위한 패키지다.<br>비교적 빠른 속도로 인해 다용량 텍스트 데이터에 이용된다.

- Pattern <br>예측성능측면에서 가장 주목받고 있는데 python 3 호환안됨...

---

## Unsupervised Sentiment Analysis Tutorial
### SentiWordNet을 이용한 영화 감상평 감성분석
문장 - 단어토큰 - 품사 - 감성지수 계산을 진행한다. 

```python
from nltk.stem import WordNetLemmatizer
from nltk.corpus import sentiwordnet as swn
from nltk import sent_tokenize, word_tokenize, pos_tag

# 문장 - 단어토큰 - 품사 - 감성지수 계산
def swn_polarity(text):
    # 감성지수 초기화
    sentiment = 0
    tokens_cnt = 0
    
    lemmatizer = WordNetLemmatizer()
    raw_sentences = sent_tokenize(text)
    # 분해된 문장 별 단어토큰화& 품사태깅후 SentiSynSet 생성 -> 긍정/부정 점수 합산
    for row_sentence in raw_sentences:
        # NTLK기반 품사 태깅 문장 추출
        tagged_sentence = pos_tag(word_tokenize(row_sentence))
        for word, tag in tagged_sentence:
            wn_tag = penn_to_wn(tag)
            # WordNet 기반 품사 태깅과 어근 추출
            if wn_tag not in (wn.ADJ, wn.NOUN, wn.ADV, wn.VERB):
                continue
            lemma = lemmatizer.lemmatize(word,pos=wn_tag)
            if not lemma :
                continue
            # 어근 추출한 단어와 WordNet 기반 품사 태깅을 입력해 Synset 객체 생성
            synsets = wn.synsets(lemma, pos=wn_tag)
            if not synsets:
                continue
            # 감성 단어 분석으로 감성 Synset 추출
            # 긍정은 + 부정은 - 로 점수 합산
            synset = synsets[0]
            swn_synset = swn.senti_synset(synset.name())
            sentiment += (swn_synset.pos_score() - swn_synset.neg_score())
            tokens_cnt +=1
    if not tokens_cnt :
        return 0 
    if sentiment >= 0 : # 0보다 클경우 긍정 
        return 1
    return 0
    
```

### VADER를 이용한 감성분석
polarity_scores 함수 덕에 sentiwordNet 보다 쉽게 감성 분석을 할 수 있다. <br> `neg` : 부정 `neu`: 중립 `pos` : 긍정 `compound` 부정/중립/긍정을 조합해서 -1~ 1사이값으로 나타냄

```python
from nltk.sentiment.vader import SentimentIntensityAnalyzer
senti_analyzer = SentimentIntensityAnalyzer()
senti_scores = senti_analyzer.polarity_scores(train_df['review'][0])
print(senti_scores)
# {'neg': 0.13, 'neu': 0.743, 'pos': 0.127, 'compound': -0.7943}

```

---
##  Practice

- Sentiment Analysis [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/sentiment-analysis-unsupervised-and-supervised.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적

