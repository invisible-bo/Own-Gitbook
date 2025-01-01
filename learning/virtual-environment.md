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

pip freeze > requirements.txt

pip install -r requirements.txt
{% endhint %}

