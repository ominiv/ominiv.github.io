---
title: 로컬환경에 Spark 설치
date: 2022-02-04 00:00:01
categories:
- Spark
tags:
- Download
---

# [Spark] 로컬환경에 Spark 설치하는 방법


## Java, Python, Scala 설치
https://www.oracle.com/java/technologies/javase-downloads.html<br>https://www.python.org/downloads/<br>https://www.scala-lang.org/download/2.11.12.html<br>`C:\Program Files\Java\jdk1.8.0_121`<br>`C:\Users\user\anaconda3`<br> `C:\HadoopEco\scala-2.11.12`

---

## Spark 2.7 다운로드후 압축풀기
https://spark.apache.org/downloads.html<br>`C:\HadoopEco\spark-3.2.1-bin-hadoop2.7`

## winutils.exe 다운로드
Spark 다운로드할 때 선택한 하둡 버전에 맞춰 winutils.exe 파일을 다운로드<br>`C:\Hadoop\bin\winutils.exe`

---

## 시스템변수 편집 (내PC > 속성 > 환경변수)
SPARK_HOME : `C:\HadoopEco\spark-3.2.1-bin-hadoop2.7`<br>HADOOP_HOME : `C:\Hadoop`<br>SCALA_HOME : `C:\HadoopEco\scala-2.11.12`

## 시스템변수 **Path**편집 (내PC > 속성 > 환경변수 > )
`%SPARK_HOME%\bin`, `%HADOOP_HOME%\bin`, `%SCALA_HOME%\bin`

---

## anaconda prompt에서 pyspark 설치
`pip install pyspark`
## anaconda prompt에서 pyspark 실행
`pyspark`<br>
<img src ='https://drive.google.com/uc?export=download&id=1POofw5ZQu33vp4bkeOhXHrlT8H_RUPYX' width = 450>