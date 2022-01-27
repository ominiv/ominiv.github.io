---
title: Python Unzip (zipfile)
date: 2022-01-27 00:00:01
categories:
- Python
tags:
- unzip
---

# Python Unzip 하는 방법

```python
zip_file_path = ['path/file1.tsv.zip','path/file2.tsv.zip','path/file3.tsv.zip'] # zip 파일 경로
output_path = '/working/' # 저장될 장소

import zipfile
for path in zip_file_path :
    with zipfile.ZipFile(path,'r') as zip_ref:
        zip_ref.extractall(output_path)
```