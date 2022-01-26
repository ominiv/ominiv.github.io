---
title: ML Text Analytics
date: 2022-01-25 00:00:01
categories:

- ML
tags:
- TA
---

# [ML] Text Analytics
텍스트 분석은 비정형 데이터인 텍스트를 분석하는 것이다.<br>텍스트를 머신러닝에 적용하기 위해서는 비정형 텍스트 데이터를 어떻게 피처형태로 추출하고 추출된 피처에 의미있는 값을 부여하는 것이 매우 중요한 요소다. 
텍스트를 word기반의 다수의 피처로 추출하고 이 피처에 단어 빈도수와 같은 숫자값을 부여하면 텍스트는 단어의 조합인 벡터값으로 표현될수 있는데 이렇게 텍스트를 변환 하는 것을 **피처 벡터화(Feature Vectorization)** 또는 **피처 추출(Feature Extraction)** 이라고 한다.

대표적으로 피처벡터화 방법으로는 BOW , Word2Vec방법이 있다.

---

## Process
머신러닝 기반 텍스트 분석 프로세스는 아래와 같다.

1. 텍스트 전처리 <br>텍스트를 피처로 만들기 전에 대소문자변경, 특수기호 삭제 등의 클렌징 작업을 하고 word 토큰화 작업, stop word 제거 , stemming/lemmatization 등의 텍스트 정규화 작업을 수행하는 것을 통칭한다.
2. 피처 벡터화/추출 <br>사전 준비 작업으로 가공된 텍스트에서 피처를 추출하고 여기 벡터값을 할당한다. 대표적인 방법은 BOW, Word2Vec 존재 *(BOW는 count 기반과 TF-IDF기반 벡터화가 존재함)*
3. ML 모델 수립 및 학습/예측/평가 <br>피처 벡터화된 데이터 세트에 ML 모델을 적용해 학습/예측 및 평가를 수행한다.

<img src='https://drive.google.com/uc?export=download&id=1tzB9fHoP-KgZ4SYRYUX-stLHF4_hy6cK'>

---

## Related Packages 
- NLTK(Natural Language Toolkit for Python) <br>대표적인 NLP 패키지다. <br>방대한 데이터세트와 서브모듈을 가지고 있고 NLP의 거의 모든 영역을 커버한다.
- Gensism <br>토픽 모델링 분야에서 가장 두각을 나타내는 패키지다. <br>토픽모델링을 쉽게 구현할 수 있는 기능을 제공한다. 
- SpaCy <br>뛰어난 수행성능으로 최근 가장 주목을 받는 NLP 패키지다.

---

## Tutorial
NLTK 라이브러리를 통해 텍스트 전처리를 진행해보자.

### 텍스트 전처리(정규화)
텍스트 자체를 바로 피처로 만들수는 없다. 머신러닝 알고리즘이나 NLP 애플리케이션에 입력데이터로 사용하기 위해 클렌징, 정제, 토큰화, 어근화와 같은 다양한 사전작업이 필요하다. 

---
#### 클렌징 (Cleansing)
텍스트에서 분석에 방해가 되는 불필요한분자, 기호등을 사전에 제거 *(ex, HTML, XML tag)*

---
#### 토큰화 (Tokenization)
토큰화의 유형은 문서에서 문장을 분리하는 **문장 토큰화**와 단어를 토큰으로 분리하는 **단어 토큰화**로 나눌수 있다. 

- 문장 토큰화 (sentence tokenization) <br>문장의 마침표 개행문자로 분리하는게 일반적이다. `sent_tokenize`
- 단어 토큰화 (Word tokenization) <br>기본적으로 공백, 콤마, 마침표로 단어를 분리한다. `word_tokenize`

```python
from nltk import sent_tokenize, word_tokenize
import nltk
nltk.download('punkt')

text_sample = 'The matrix is everywhere its all around us, here even in my room. You can see it out your window or on your tv. you feel it when you go to work, or go to church or pay your taxes.'

#sentences = sent_tokenize(text =text_sample)
#words = word_tokenize(text= text_sample)
def tokenize_text(text):
    sentences = sent_tokenize(text=text)
    words = [word_tokenize(_) for _ in sentences]
    return words

result = tokenize_text(text=text_sample)
```
---
#### 필터링 (Filtering) / Stop word 제거 / 철자 수정
- Stop word 제거<br>Stop word는 분석에 큰 의미가 없는 단어를 뜻한다. *(ex, is, the, a ...etc)*

```python
import nltk 
nltk.download('stopwords')
stopwords = nltk.corpus.stopwords.words('english')
all_tokens=[]

for sentence in result :
    filtered_words=[]
    for word in sentence :
        word = word.lower()
        if word not in stopwords:
            filtered_words.append(word)
    all_tokens.append(filtered_words)
print(all_tokens)
# [['matrix', 'everywhere', 'around', 'us', ',', 'even', 'room', '.'], ['see', 'window', 'tv', '.'], ['feel', 'go', 'work', ',', 'go', 'church', 'pay', 'taxes', '.']]
```

---

#### 어간 추출 (Stemming) 표제어 추출 (Lemmatization)
두 기능 모두 원형 단어를 찾는 다는 목적은 유사하지만, Lemmatization이 Stemming보다 정교하고 의미론적인 기반에서 단어의 원형을 찾는다. 
**Lemmatization의 경우 품사를 input으로 받는다.**

```python
from nltk.stem import LancasterStemmer, WordNetLemmatizer
stemmer = LancasterStemmer()
lemmer = WordNetLemmatizer()
nltk.download('wordnet')
words_list = [['working','works','worked'],['amusing','amuses','amused'],['happier','happiest'],['fancier','fanciest']]
word_t=['v','v','a','a']
for i, words in enumerate(words_list):
    stem = []; lemm=[]
    for word in words :
        stem.append(stemmer.stem(word)) 
        lemm.append(lemmer.lemmatize(word, word_t[i])) 
    print('stem : ',stem)
    print('lemm : ',lemm)

# stem :  ['work', 'work', 'work']
# lemm :  ['work', 'work', 'work']
# stem :  ['amus', 'amus', 'amus']
# lemm :  ['amuse', 'amuse', 'amuse']
# stem :  ['happy', 'happiest']
# lemm :  ['happy', 'happy']
# stem :  ['fant', 'fanciest']
# lemm :  ['fancy', 'fancy']

```
---

##  Practice

- Text Preprocessing [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/Text_Preprocessing.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적

