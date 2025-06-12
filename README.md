# Class-A_TeamD
Team D – Project Materials Experiment Code, Execution Results, Experiment Environment Information

# A_Class_TeamD_Experiment_Code.ipynb

본 Jupyter Notebook 파일(`A_Class_TeamD_Experiment_Code.ipynbb`)은 **A분반 D팀의 실험 코드**를 포함하고 있습니다.  
데이터 전처리, 클러스터링, 시각화 등 지하철역 광고 전략 수립을 위한 전체 분석 과정이 구현되어 있습니다.

# Python 및 사용 라이브러리 목록

 Python Version: 3.10.16

## 라이브러리 목록

- absl-py==2.2.2  
- anyascii==0.3.2  
- asttokens==3.0.0  
- astunparse==1.6.3  
- beautifulsoup4==4.13.4  
- bs4==0.0.2  
- cachetools==5.5.2  
- certifi==2025.4.26  
- charset-normalizer==3.4.2  
- click==8.2.1  
- colorama==0.4.6  
- comm==0.2.2  
- contourpy==1.3.2  
- contractions==0.1.73  
- cycler==0.12.1  
- debugpy==1.8.14  
- decorator==5.2.1  
- exceptiongroup==1.3.0  
- executing==2.2.0  
- flatbuffers==25.2.10  
- fonttools==4.58.0  
- gast==0.4.0  
- gensim==4.3.3  
- google-auth==2.40.2  
- google-auth-oauthlib==1.0.0  
- google-pasta==0.2.0  
- grpcio==1.71.0  
- h5py==3.13.0  
- idna==3.10  
- ipykernel==6.29.5  
- ipython==8.36.0  
- jax==0.4.30  
- jaxlib==0.4.30  
- jedi==0.19.2  
- joblib==1.5.1  
- jupyter_client==8.6.3  
- jupyter_core==5.7.2  
- keras==2.12.0  
- kiwisolver==1.4.8  
- libclang==18.1.1  
- Markdown==3.8  
- MarkupSafe==3.0.2  
- matplotlib==3.10.3  
- matplotlib-inline==0.1.7  
- ml_dtypes==0.5.1  
- nest-asyncio==1.6.0  
- nltk==3.9.1  
- numpy==1.23.5  
- oauthlib==3.2.2  
- opt_einsum==3.4.0  
- packaging==25.0  
- pandas==2.2.3  
- parso==0.8.4  
- pillow==11.2.1  
- platformdirs==4.3.8  
- prompt_toolkit==3.0.51  
- protobuf==4.25.7  
- psutil==7.0.0  
- pure_eval==0.2.3  
- pyahocorasick==2.1.0  
- pyasn1==0.6.1  
- pyasn1_modules==0.4.2  
- Pygments==2.19.1  
- pyparsing==3.2.3  
- python-dateutil==2.9.0.post0  
- pytz==2025.2  
- pywin32==310  
- pyzmq==26.4.0  
- regex==2024.11.6  
- requests==2.32.3  
- requests-oauthlib==2.0.0  
- rsa==4.9.1  
- scikit-learn==1.6.1  
- scipy==1.13.1  
- six==1.17.0  
- smart-open==7.1.0  
- soupsieve==2.7  
- stack-data==0.6.3  
- tensorboard==2.12.3  
- tensorboard-data-server==0.7.2  
- tensorflow==2.12.0  
- tensorflow-estimator==2.12.0  
- tensorflow-intel==2.12.0  
- tensorflow-io-gcs-filesystem==0.31.0  
- termcolor==3.1.0  
- textsearch==0.0.24  
- threadpoolctl==3.6.0  
- tornado==6.5.1  
- tqdm==4.67.1  
- traitlets==5.14.3  
- typing_extensions==4.13.2  
- tzdata==2025.2  
- urllib3==2.4.0  
- wcwidth==0.2.13  
- Werkzeug==3.1.3  
- wrapt==1.14.1  

---

`requirements.txt`는 이 프로젝트에서 사용하는 Python 라이브러리들의 **목록과 정확한 버전**이 기록된 파일입니다.

`D_subway_ad.ipynb` 첫 셀에 `pip install -r requirements.txt` 명령이 포함되어 있어,  
노트북 실행 시 자동으로 라이브러리가 설치됩니다.

가상환경에서 실행해야 합니다.

## 📁 데이터 파일 설명

본 프로젝트에서 사용된 데이터는 서울교통공사에서 제공한 공공데이터를 기반으로 하며,  
아래와 같이 총 4개의 CSV 파일을 사용하였습니다.
그외 광고시설물의 면적이나 광고단가는 하단 링크에서 수집한 정보를 기반으로 임의값을 설정하였습니다.

광고단가 정보
http://www.springbeat.co.kr/03/0101.php
https://goodadlab.co.kr/subway
광고면적 정보
https://jungsungad.com/65\
https://www.yeonsu.go.kr/main/

---

### 1. `passenger_info.CSV`
- **원본 파일명**: `서울교통공사_1_8호선 역별 일별 승객유형별 수송인원(환승유입인원 포함) 정보_20231231.csv`
- **설명**: 1~8호선의 역별 · 일별 · 승객유형별 수송 인원을 제공하며, 환승 유입 인원 포함
- **주요 컬럼**:
  - `날짜`: 수집일 (예: 2023-01-01)
  - `역명`: 지하철역 이름
  - `승객유형`: 일반 / 어린이 / 청소년 / 우대권 등
  - `승차인원`: 해당 유형의 당일 승차 인원
  - `환승유입인원`: 타 노선에서 환승을 통해 유입된 인원 수

---

### 2. `station_area_info.csv`
- **원본 파일명**: `서울교통공사_역사면적정보_20250310.csv`
- **설명**: 서울교통공사 소속 각 역사의 대합실 및 승강장 면적 정보를 포함
- **주요 컬럼**:
  - `호선`: 지하철 노선 (예: 1호선)
  - `역명`: 지하철역 이름
  - `대합실면적`: 대합실 면적 (㎡)
  - `승강장면적`: 승강장 면적 (㎡)

---

### 3. `ad_info.csv`
- **원본 파일명**: `서울교통공사_역사별 광고시설 현황 정보_20241128.csv`
- **설명**: 각 지하철역 내 광고시설물의 종류, 수량, 운영 대행사 정보를 포함
- **주요 컬럼**:
  - `역명`: 지하철역 이름 (호선 중복 시 괄호 표기)
  - `광고시설물명`: 시설물 유형 (예: 디지털포스터, 멀티비젼)
  - `광고시설물 수량`: 시설물 설치 개수
  - `광고대행사`: 운영 광고사
  - `데이터기준일자`: 기준 날짜

---

### 4. `transfer_time_info.csv`
- **원본 파일명**: `서울교통공사_환승역거리 소요시간 정보_20250310.csv`
- **설명**: 환승역 간 이동 거리 및 환승에 소요되는 평균 시간 제공
- **주요 컬럼**:
  - `환승역명`: 환승이 이루어지는 역 이름
  - `환승노선`: 환승 대상 노선
  - `환승거리`: 두 노선 간 이동 거리 (단위: m)
  - `환승소요시간`: 평균 소요 시간 (예: 02:13)

## 🔍 실험 결과 파일 설명

`final_with_subclusters` 파일은 클러스터링 실험 결과를 담고 있는 최종 데이터셋입니다.  
이 파일에는 클러스터링에 사용된 **4개의 주요 변수**와 함께, 각 지하철역에 대한 **클러스터 및 서브클러스터** 결과가 포함되어 있습니다.

이를 통해 각 역의 특성에 따라 분류된 클러스터 구조를 확인할 수 있으며, 광고 전략 수립을 위한 기반 데이터로 활용했습니다.



