---
title: Tableau에 대해 알아보자
date: 2022-03-15 00:00:01
categories:
- Tableau
tags:
- Tableau
---

# Tableau Public 시작
데이터 시각화에 활용되는 태블로에 대해 알아보자.<br>
나는 주로 R,Python으로 시각화를 진행했었다. 하지만 태블로는 GUI만으로 비교적 간단하게 시각화를 진행할 수 있는 유용한 도구다. 마치 고도화된 ppt같은 느낌이 든다. 

유료로 알려진 태블로는 무료버전도 존재한다. ^^<br>나는 무료인 Tableau Public 버전을 이용하면서 유료로 넘어갈지 말지를 결정하려한다.

---
## 다운로드
아래 링크에서 다운로드 후 exe 파일 실행하면 tableau를 사용할 수 있다. <br>
[tableau download link](https://public.tableau.com/ko-kr/s/download) https://public.tableau.com/ko-kr/s/download

---
## 태블로 파일 유형 및 폴더
태블로에는 다양한 파일유형이 존재한다. <br> 예제들을 실행하기 앞서 한번 읽어보면 좋다. 

- **통합문서(.twb)** : 하나 이상의 워크시트와 0개 이상의 대시보드 및 스토리가 포함된다. 데이터원본을 포함하지 않는다.

- **책갈피(.tbm)** : 단일 워크시트를 포함해 작업을 빠르게 공유하는데 사용한다.
- **패키지 통합문서(.twbx)** : 패키지 통합문서는 지원되는 로컬파일 데이터 및 배경 이미지와 함께 통합문서를 포함하는 zip 파일으로 데이터원본을 포함한다. <br>패키지를 해제할 경우, twb파일과 데이터 원본 파일로 분리된다.
    -  *.twbx 패키지 해제 방법<br>*.twbx 파일 확장자를 *.zip으로 변경 후 압축을 풀어준다.* <br>

- **추출(.hyper 또는 .tde)** : 추출을 만들 때 사용된 버전에 따라 Tableau 추출의 파일 확장명은 .hyper 또는 .tde일 수 있습니다. 추출 파일은 다른 사용자와 데이터를 공유하는 경우, 오프라인으로 작업해야 하는 경우 및 성능 향상을 위해 사용할 수 있는 하위 집합 또는 전체 데이터의 로컬 복사본이다.

- **데이터 원본(.tds)** : Tableau 데이터 원본 파일의 파일 확장명은 .tds입니다. 데이터 원본 파일은 자주 사용하는 원본 데이터에 빠르게 연결하기 위한 바로 가기입니다. 데이터 원본 파일은 실제 데이터가 아니라 실제 데이터에 연결하는 데 필요한 정보와 기본 속성 변경, 계산된 필드 만들기, 그룹 추가 등 실제 데이터를 기반으로 수행한 모든 수정 내용을 포함합니다. 

---
## Practice
[Sample Workbooks](https://tableaubook.com/v8/workbooks.asp) 에 예시 twbx 파일이 제공된다. <br>나 같은 입문자는 workbooks를 하나씩 실행해보며 기능을 익히는 것이 좋아보인다.<br>각 챕터별로 포스팅 될 예정이다.

---
## Reference
- [Tableau 시작하기](https://help.tableau.com/current/pro/desktop/ko-kr/gettingstarted_overview.htm)
- [Sample Workbooks](https://tableaubook.com/v8/workbooks.asp)
