# Team-project

---

## **1. GitHub 프로젝트 구조**

```
project-directory/
├── arduino/               # 아두이노 관련 코드와 회로도
│   ├── grove_dust_sensor.ino   # 아두이노 스케치 파일
│   └── circuit_diagram.png      # 회로도 이미지
├── jetson-nano/           # 젯슨 나노 관련 코드
│   ├── sensor_read.py          # 센서 값 읽기 코드
│   ├── setup.md                # 젯슨 나노에서 Grove 센서 설정 방법
├── jupyter-notebook/      # 주피터 노트북 관련 파일
│   ├── compare_pm10.ipynb      # 기상청 API와 비교하는 코드
│   ├── api_integration.py      # 기상청 API 연동 코드
├── data/                  # 측정 데이터
│   ├── pm10_data.csv           # 저장된 미세먼지 데이터
├── README.md              # 프로젝트 설명 및 가이드
├── requirements.txt       # Python 의존성 패키지
└── LICENSE                # 프로젝트 라이선스 (선택 사항)
```

---

## **2. 주요 내용 정리**
GitHub에 올릴 프로젝트의 주요 내용을 아래와 같은 순서로 정리하세요.

### **(1) 프로젝트 소개 (README.md)**

```markdown
# Grove Dust Sensor를 활용한 미세먼지 측정 프로젝트

이 프로젝트는 **Grove Dust Sensor**를 활용하여 미세먼지를 측정하고, 이를 **젯슨 나노**와 **주피터 노트북**을 통해 분석합니다. 또한, 기상청 API를 이용해 실시간 데이터를 가져와 비교 분석합니다.

## 주요 기능
1. Grove Dust Sensor로 실시간 미세먼지 측정.
2. 젯슨 나노에서 센서 데이터를 처리 및 저장.
3. 주피터 노트북에서 데이터 시각화 및 기상청 API 데이터를 비교 분석.
4. 최신 데이터를 기반으로 미세먼지 상태를 모니터링.
```

---

### **(2) 아두이노 코드 (arduino/)**
`grove_dust_sensor.ino`에 아두이노 스케치를 업로드하세요.

```c
// Grove Dust Sensor 사용 예제 코드
int measurePin = A0; // 센서 핀 연결
void setup() {
  Serial.begin(9600);
}
void loop() {
  int sensorValue = analogRead(measurePin);
  Serial.println(sensorValue);
  delay(1000); // 1초마다 데이터 전송
}
```

`circuit_diagram.png`에는 회로도를 포함하세요.

---

### **(3) 젯슨 나노 코드 (jetson-nano/)**
- `sensor_read.py`에는 Grove Dust Sensor의 데이터를 젯슨 나노에서 읽는 코드를 작성합니다.
- `setup.md`에는 Grove Sensor를 젯슨 나노와 연결하는 방법(설정 방법)을 포함하세요.

---

### **(4) 기상청 API 연동 및 비교 분석 (jupyter-notebook/)**
`compare_pm10.ipynb`에는 주피터 노트북에서 아래와 같은 과정을 포함합니다:
- Grove Dust Sensor 데이터를 읽어와 최신 값 추출
- 기상청 API에서 실시간 미세먼지 데이터를 가져와 비교
- 데이터를 시각화하여 분석 결과 출력

예제 코드:
```python
import pandas as pd
import matplotlib.pyplot as plt

# 센서 데이터 로드
sensor_data = pd.read_csv('data/pm10_data.csv')
latest_sensor_value = sensor_data['PM10'].iloc[-1]

# 기상청 API 데이터 가져오기
api_value = 25  # 예제 값 (기상청 API 값)

# 비교 출력
print(f"Grove Dust Sensor 값: {latest_sensor_value}")
print(f"기상청 API 값: {api_value}")

# 시각화
plt.bar(['Sensor', 'API'], [latest_sensor_value, api_value])
plt.title('미세먼지 비교')
plt.show()
```

---

### **(5) 데이터 파일 및 의존성 (data/, requirements.txt)**
- **`data/`**: 센서 데이터(`pm10_data.csv`)를 저장합니다.
- **`requirements.txt`**: 필요한 Python 패키지를 명시합니다.
  ```plaintext
  pandas
  matplotlib
  requests
  ```

---

### **(6) 프로젝트 실행 가이드**
`README.md`에 프로젝트 실행 방법을 포함합니다.

```markdown
## 프로젝트 실행 방법

### 1. 아두이노
1. `arduino/grove_dust_sensor.ino` 코드를 업로드합니다.
2. Grove Dust Sensor를 아두이노에 연결합니다.

### 2. 젯슨 나노
1. `jetson-nano/sensor_read.py`를 실행하여 데이터를 읽고 저장합니다.
2. 데이터를 `data/pm10_data.csv`에 저장합니다.

### 3. 주피터 노트북
1. `requirements.txt`를 설치합니다:
   ```bash
   pip install -r requirements.txt
   ```
2. `jupyter-notebook/compare_pm10.ipynb`를 실행합니다.
3. 결과를 확인합니다.
```

---

## **3. GitHub 관리 팁**
1. **명확한 커밋 메시지 작성**: 각 파일 추가나 수정 시 상세히 기록.
   - 예: `Add Arduino sketch for Grove Dust Sensor`
2. **스크린샷 및 이미지 포함**: `README.md`에 실행 결과 스크린샷 추가.
3. **라이선스 명시**: 필요한 경우 오픈소스 라이선스 파일 추가.

---
