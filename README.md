# 📊 카드 소비 데이터 기반 잠재 고객 유치 분석

## **🧐 숨겨진 VIP와 무늬만 VIP 🧐**

**– 회원등급과 소비 행태 괴리 분석을 중심으로**

<br/>

---

## 🧑‍💻 팀원 소개


| ![](https://avatars.githubusercontent.com/u/181299322?v=4) | ![](https://avatars.githubusercontent.com/u/89902255?v=4) | ![](https://avatars.githubusercontent.com/u/204296918?v=4) |![](https://avatars.githubusercontent.com/u/180767288?v=4)|
|:---:|:---:|:---:|:---:|
| **신성혁**<br>[@ShinSungHyuk](https://github.com/ssh221) | **유예원**<br>[@Yewon0106](https://github.com/Yewon0106) | **이준호**<br>[@Junhoss](https://github.com/Junhoss) | **조민우**<br>[@MinWoo Cho](https://github.com/minwoo-00) |

<br/>

--- 
## 👨‍🏫 프로젝트 개요 (Overview)

본 프로젝트는 **실제 우리카드 소비 데이터**를 활용하여 

**기존 회원등급 체계와 실제 소비 실적 간의 괴리**를 분석하고, 이를 통해 **잠재적인 고가치 고객을 식별**하여 향후 **고객 유치 및 마케팅 전략 수립**에 활용 가능한 인사이트를 도출하는 것을 목표로 한다.



<br/>

---

## 🔍 분석 배경 및 문제 정의

일반적으로 카드사의 회원등급(VVIP, VIP 등)은 고객의 소비 실적을 기반으로 산정되지만,

- 실제로는 **상위 등급 대비 더 높은 소비를 하는 일반 고객**이 존재할 수 있고
- 반대로 등급은 높지만 실적이 상대적으로 낮은 고객도 존재할 수 있다.

이러한 괴리는

- **우수 고객을 제대로 대우하지 못해 이탈 위험**을 높이고
- 불필요한 혜택 제공으로 비용 효율을 저하시킬 가능성이 있다.

<br/>


따라서 본 프로젝트에서는

> **“현재 등급이 아닌, 실제 소비 행동을 기준으로 한 잠재 고객은 누구인가?”**
> 
> 
> 라는 질문에서 분석을 시작하였다.
> 

<br/>

---

## 📚 데이터 및 분석 범위

### 📁 데이터 구성

- **우리카드 이용 데이터**
- **주요 컬럼**
    - 회원등급 (21: VVIP, 22: VIP, 23~25: 일반)
    - 총 소비금액
    - 업종별 소비 금액
    - LIFE_STAGE
    - 기준 분기

<br/>


### ⏱ 분석 기간

- **최근 4개 분기 데이터 활용**
    - 2024 Q3 / 2024 Q4 / 2025 Q1 / 2025 Q2
- 팀원 4명이 각 분기 데이터를 나누어 동일한 분석 프레임으로 분석 수행

<br/>


### 🚨 분기 단위 분석 설계 배경

본 프로젝트에서는 원본 데이터의 구조적 특성을 고려하여 **분기 단위로 데이터를 분리하여 분석**을 진행하였다.

원본 데이터는 동일 고객에 대한 정보가 분기별로 나누어 저장된 형태로 구성되어 있었으며, 이를 하나의 테이블로 통합하여 분석할 경우 다음과 같은 문제가 발생할 수 있었다.

- **고객 단위 중복 집계 가능성 문제**
- **시점이 다른 소비 정보가 혼합되는 문제**


<br/>
    

이에 따라 데이터의 시계열적 일관성과 고객 단위 분석의 정확성을 확보하기 위해,

최근 4개 분기(2024 Q3 ~ 2025 Q2)를 기준으로 **분기별로 데이터를 분리하여 동일한 분석 프레임으로 반복 분석을 수행**하였다.

<br/>

또한 **각 분기별로 도출된 시각화 및 분석 결과**는

세부 수치에는 차이가 있었으나 등급별 소비 구조, Hidden VIP의 존재, 핵심 소비 업종 및 LIFE_STAGE 등 **주요 인사이트는 일관되게 동일한 패턴**을 보였다.

<br/>


**이에 본문에서는 분기 간 결과의 대표성을 확보할 수 있다고 판단하여 2025년 1분기(2025Q1)를 기준으로 분석 과정을 상세히 설명하였다.**

<br/>

**👉 2025년 2분기**
<br/>
<img width="1907" height="786" alt="image" src="https://github.com/user-attachments/assets/187ae9c8-4927-485e-ac34-87e309e8627d" />

<br/>

**👉 2025년 1분기**
<img width="1859" height="812" alt="image" src="https://github.com/user-attachments/assets/9dc19aa5-cf78-42d0-a883-68a512c1b2a5" />

<br/>

**👉 2024년 4분기**
<img width="1281" height="803" alt="image" src="https://github.com/user-attachments/assets/714d9d5e-f817-4b46-8551-2049b833e52a" />

<br/>

**👉 2024년 3분기**
<img width="1758" height="807" alt="image" src="https://github.com/user-attachments/assets/62f49d92-720f-439a-b157-7e7f0663c86c" />




---

## 🛠️ 기술 스택 (Tech Stack)

- **DuckDB + SQL**
    - 대용량 우리카드 CSV 데이터 처리
    - 조건 기반 고객 추출 및 파생 테이블 생성
- **DBeaver**
    - DuckDB SQL 실행 및 데이터 가공
- **Kibana**
    - 소비 분포 및 고객 비중 시각화
    - Pie Chart, Bar Chart, Treemap 등 활용
- **GitHub**
    - 프로젝트 문서화 및 결과 공유

<br/>

---

## 🔥 분석 과정 및 주요 결과


### ☑️ 1단계 : 등급별 고객 수 비중 분석

- 전체 고객 수 대비 회원등급별 비중 분석

<img width="955" height="536" alt="image" src="https://github.com/user-attachments/assets/64384d19-6837-471e-b2dc-6ae8ea6eead1" />

<br/>

**✨ 결과**

- 25(해당 없음): **48%**
- 24(골드): **34%**
- 23(플래티넘): **12%**
- VIP(22), VVIP(21): 상대적으로 소수

<br/>

👉 **고객 수는 일반 등급이 압도적으로 많은 것을 확인**

---

### ☑️ 2단계 : 상위 등급 평균 소비금액 대비 일반 고객 분석

- VVIP, VIP 고객의 평균 소비금액 산출
```sql
  select round(avg(tot_use_am)) from wooricard_2024q4 where mbr_rk in (21, 22);
```
- 해당 평균과 **같거나 높은 소비를 하는 일반 고객(23~25)** 을 추출
- 이들이 각 등급 내에서 차지하는 비율을 **Bar Chart**로 시각화

  <br/>
  

<img width="922" height="571" alt="image" src="https://github.com/user-attachments/assets/00a7e6de-44a2-43ea-b9a6-48e2a5b3667a" />


<br/>

**✨ 결과**

- 일반 등급 내에서도 상위 등급 평균 이상의 소비를 하는 고객이 유의미하게 존재
- 즉, 등급 대비 과소평가된 고객 **(Hidden VIP)** 존재 확인

---

### ☑️ 3단계 : 전체 고객 기준 최다 소비 업종 분석

- 각 고객들의 주요 소비 업종(TOP3)에 대한 결과 추출 
```sql
SELECT 
    seq,
    -- 1순위
    MAX(CASE WHEN rn = 1 THEN category END) AS top1_category,
    MAX(CASE WHEN rn = 1 THEN amount END)   AS top1_amount,
    -- 2순위
    MAX(CASE WHEN rn = 2 THEN category END) AS top2_category,
    -- 3순위
    MAX(CASE WHEN rn = 3 THEN category END) AS top3_category
FROM (
    SELECT 
        seq,
        category,
        amount,
        -- 금액 높은 순으로 랭킹 (금액 같으면 카테고리명 순)
        ROW_NUMBER() OVER (PARTITION BY seq ORDER BY amount DESC, category ASC) AS rn
    FROM (
        /* 1. 일단 _AM으로 끝나는 모든 컬럼을 Unpivot 합니다 */
        UNPIVOT (select * from wooricard_2024q4 where mbr_rk in (23, 24, 25) and tot_use_am >= 861)
        ON COLUMNS('.*_AM')
        INTO NAME category VALUE amount
    ) unpvt_base
    /* 2. 여기서 원하지 않는 합계/집계성 컬럼 3개를 제외합니다 */
    WHERE category NOT IN ('TOT_USE_AM', 'CRDSL_USE_AM', 'CNF_USE_AM')
) ranking_base
WHERE rn <= 3 -- 3등까지만 남김
GROUP BY seq;
```


- 전체 고객의 업종별 소비 금액을 **Treemap**으로 시각화

<br/>


<img width="1044" height="577" alt="image" src="https://github.com/user-attachments/assets/5806fb7f-aaf0-42f1-a1e5-6a3a32bbccd4" />


<br/>


**✨ 결과**

- **AUTO_AM (**자동차 업종**)** 이 전체 소비 금액에서 가장 큰 비중 차지

<br/>

👉 카드 소비의 핵심 축이 **자동차 관련 지출**임을 확인

---

### ☑️ 4-1단계 : Hidden VIP 고객의 업종 소비 특성 분석

- 상위 등급 평균 소비금액보다 높은 일반 고객을 대상으로 업종별 소비 비교

<br/>

<img width="927" height="470" alt="image" src="https://github.com/user-attachments/assets/c9f0fdb7-b2e0-4a57-b56d-d9f451e428d3" />

<br/>


**✨ 결과**

- **DISTBP_AM (**유통업영리**)** 업종에서 소비 금액이 가장 크게 나타남

<br/>


👉 Hidden VIP 고객은 **생활 밀착형 유통 소비**에서 강한 성향을 보임

---

### ☑️ 4-2단계 : Hidden VIP 고객의 LIFE_STAGE 분석

- Hidden VIP 고객의 LIFE_STAGE 분포 분석

<br/>


<img width="922" height="597" alt="image" src="https://github.com/user-attachments/assets/12488313-e44e-41aa-ac66-2f3ae3f5708f" />

<br/>


**✨ 결과**

- **CHILD_TEEN**
- **CHILD_UNI**
    
    순으로 가장 높은 비중을 차지

  <br/>
    

👉 자녀를 둔 가구에서 소비 여력과 확장 가능성이 높은 고객군임을 시사

<br/>

---

## 💯 인사이트 및 마케팅 활용 방안

### 👨‍🏫 핵심 인사이트

**1. 현재 회원등급은 모든 고가치 고객을 포착하지 못하고 있다.**  
2. 상위 등급 평균 이상의 소비를 하는 일반 고객은
    - **유통업 중심 소비 성향**
    - **자녀(청소년·대학생)를 둔 LIFE_STAGE에 집중**  되었다.
3. 이들은 향후 고가치 고객으로 전환될 가능성이 높은 잠재 고객층이다.


<br/>


### 🎯 마케팅 및 전략 제안

- **Hidden VIP 대상 선제적 등급 혜택 제공**
    - 한시적 VIP 체험
    - 유통·생활 소비 중심 혜택 강화
- **LIFE_STAGE 기반 맞춤 마케팅**
    - 교육, 생활비, 가족 소비 연계 프로모션
- **등급 산정 로직 고도화**
    - 소비 패턴과 총액·업종·라이프스테이지를 반영한 평가 필요

<br/>

### 🔮 Future Work (확장 방향) : **이탈 위험 고객 탐지 (Risk Scoring)**

> “혜택 대비 실적이 높은 고객은 이탈 위험이 높은가?”
>


- Hidden VIP는 “혜택 대비 실적이 높은데 등급은 낮음”
- 이탈 위험이 가장 높은 그룹

<br/>


**🧠 접근 방식**



본 프로젝트는 탐색적 데이터 분석을 기반으로 수행되었으나,
향후 다음과 같은 머신러닝 기법을 활용하여 이탈 위험 고객 탐지로 확장 가능하다.

- 규칙 기반 점수 + ML 혼합
- 이상치 탐지 (Isolation Forest)


<br/>

**🎯 결과**

- “지금 이 고객을 잡아야 한다” 리스트 결과를 얻어 관련 마케팅에 활용 가능하다.

<br/>

## 💡 결론

  본 프로젝트는 기존 회원등급 체계의 한계를 데이터로 검증하고, **소비 행동을 기준으로 한 잠재 고가치 고객을 식별**함으로써 보다 정교한 고객 유치 및 유지 전략의 가능성을 제시하였다.

  **향후 분기별 추적 분석을 통해 Hidden VIP의 실제 등급 이동 여부를 검증**한다면 더욱 실질적인 전략 수립으로 확장할 수 있을 것이다.
