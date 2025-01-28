---
icon: vr-cardboard
description: 가상 환경
---

# Virtual Environment



```python
python -m venv venv
# Creating Virtual Environment

source venv/Scripts/activate
# Activate Virtual Environment(Windows에서)

source venv/bin/activate
# Activate Virtual Environment(MacOS)

deactivate
# deactivate Virtual Environment
```

#### pip

```bash
pip list
pip install
```

{% hint style="info" %}
패키지 설치 목록을 저장하고 나중에 동일한 환경을 복원



가상환경에서 사용 중인 패키지들을 `requirements.txt` 파일로 추출

* pip freeze > requirements.txt

이 파일을 다른 개발자나 서버에 배포하고, 같은 환경을 만들려면

* pip install -r requirements.txt
{% endhint %}

