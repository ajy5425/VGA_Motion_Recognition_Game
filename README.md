# 🕺Let's Dance: VGA 기반 K-Dance 모션 인식 게임

## 팀원 

> 역할 분배  바로가기 :arrow_right: [[Role]](/History/Role.md) 

|Team Leader|Team Member1|Team Member2| 
:--:|:--:|:--:|
| [<img src="/History/img/another/profile_1.png" width=150 > </br> @문우진](https://github.com/) |  [<img src="/History/img/another/profile_2.jpg" width=150 > </br> @Kim ByeonHyeon](https://bhyeon1.github.io/)|  [<img src="/History/img/another/profile_3.png" width=150 > </br> @김을중](https://github.com/)| 

|Team Member3|Team Member4|Team Member5|Team Member6| 
:--:|:--:|:--:|:--:|
| [<img src="/History/img/another/profile_4.png" width=150 > </br> @박승범](https://github.com/) |  [<img src="/History/img/another/profile_5.png" width=150 > </br> @안재용](https://github.com/)| [<img src="/History/img/another/profile_6.png" width=150 > </br> @오정일](https://github.com/) |  [<img src="/History/img/another/profile_7.jpg" width=150 > </br> @Jung EunJi](https://github.com/2735C)|



## 📝 프로젝트 개요

실시간 카메라 입력(OV7670)을 VGA 파이프라인으로 처리하여 **댄스 가이드 패턴과 사용자의 동작 일치율을 측정**하고 점수를 산출하는 게임입니다. 시작/곡 선택은 **특정 색(빨간색) 인식**으로 입력받으며, 게임 종료 후 점수를 **랭킹 보드**에 기록합니다.

- **종료 조건**: 음악 선택 후 나오는 모든 안무 패턴 종료 시
- **점수 등급**: Perfect ≥ 80%, Good 50–80%, Bad < 50%
- **촬영 조건 예시**: 카메라–사용자 거리 약 4.8 m

##


### :one: 프로젝트 선정 배경


- 문제 인식 : 현대 사회에 들어 지속적으로 증가하는 우울감과 스트레스

- 해결 방안 : 글로벌 시장에서 큰 인기를 얻고 있는 K-POP을 통해 스트레스 해소 및 긍정적인 에너지를 전달

##

### :two: 주요 기능

#### 🎮 Game Rule

<table>
  <tr>
    <td align="center" width="400">
      <img src="https://github.com/2735C/VGA_Motion_Recognition_Game/blob/main/History/img/another/game_1.gif?raw=true" width="380" alt="게임 화면">
    </td>
    <td width="400">
      <br>
      <span style="font-size:25px; font-weight:bold;">:one: 곡을 선택한다. </span><br><br>
      <span style="font-size:25px; font-weight:bold;">:two: 패턴을 확인한다. </span><br><br>
      <span style="font-size:25px; font-weight:bold;">:three: 패턴에 맞춰 몸을 맞춘다. </span><br><br>
      <span style="font-size:25px; font-weight:bold;">:four: 점수 확인 후 랭킹 칸에 이름을 입력한다. </span><br><br>
    </td>
  </tr>
</table>



- **실시간 영상 전처리**: Median(노이즈 저감), Gray(색상 단순화), Sobel(에지 검출), + (파이프라인)
- **패턴 매칭**: PIP(Point In Polygon) + **Ray Crossing**으로 패턴 내부/외부 판정, 30개 선분 병렬 처리
- **게임 FSM**: 시작/선택/플레이/종료 상태 전이, **UART 연계 Python UI**로 랭킹 입력 및 UI 표시
- **타이밍 정합**: PIP 내부에서 **3FF**로 비디오 데이터 영역과 패턴 데이터 영역의 **CDC**문제 해결

##

### :three: 시스템 아키텍처


카메라(OV7670) → Basys3(PL) → VGA/HDMI 출력
**UART**를 통해 PC(Python GUI)와 통신

- **Toolchain**: Vivado 2020.2, Xilinx Vitis / VS Code
- **HW**: Basys3, OV7670, VGA→HDMI 케이블, 캡쳐 보드
- **Language**: systemverilog, python

<!--

본 프로젝트는 **ISP 알고리즘을 활용한 VGA 영상처리 모션 인식 게임**입니다. 

현대 사회는 지속적으로 **우울증 환자가 증가**하고 있습니다. 
건강보험공단 자료에 따르면, 2020년 약 87만 명이었던 우울증 환자 수가 2023년에는 약 109만 명으로 25% 증가했으며, 특히 아동 및 청소년, 청년층에서 급증하는 추세를 보였습니다.
연구 결과에 따르면 **능동적인 활동**은 **우울감이 감소**시키고 **스트레스 해소에 도움**이 된다고 합니다.

따라서, 저희 팀은 **"DDR"을 모티브**로 하여 최근 전세계적으로 선풍적인 인기를 얻고 있는 **"K-POP DEMON HUNTERS"** 라는 애니메이션의 **춤 동작을 배울 수 있는 모션 인식 게임**을 제작했습니다. 

### :two: 기술/하드웨어 요소

ISP 알고리즘: Sobel, Gaussian, Median 필터를 사용하여 영상 전처리

VGA 영상 처리: Zybo/ Basys3 보드 기반 실시간 영상 처리

모션 인식: PIP, Ray Crossing 알고리즘 활용

통신/인터페이스: SCCB, UART, HDMI, AXI4 프로토콜 사용

GUI/게임 구현: Python 기반 게임 UI 제작, 랭킹 보드, 화면 효과

### :three: 기대 효과 / 활용

- **Home Fitness / Smart Home IoT**: 집에서 쉽게 따라하는 체조 및 동작 인식  

- **안전 모니터링**: 낙상 방지—지정 영역 이탈 감지 알람

- **K-POP 챌린지**: 점수 공유/영상 업로드로 **SNS 확산** 기대

-->




<!--

<img src="/History/img/hw/img_109.png" width=300 >|<img src="/History/img/hw/img_110.png" width=300 >|
--|--

현대 사회에 들어 지속적으로 우울증 환자들이 증가

→ 능동적인 활동을 통해 우울감 감소, 스트레스 해소에 도움이 되는 연구결과가 존재

<img src="/History/img/hw/img_111.png" width=300 >|<img src="/History/img/hw/img_112.png" width=300 >|
--|--

현재 K-POP은 전세게적으로 큰 인기를 끌고 있는 가운데 특히 K-POP DEMON HUNTERS라는 애니메이션은 남녀노소 어른아이 할 거 없이 좋아하며 선풍적인 인기를 얻고 있음.

<img src="/History/img/hw/img_113.png" width=300> | 
--|

K-POP DEMON HUNTERS의 춤추는 동작을 바탕으로한 모션 인식 게임을 통해 우울감, 스트레스 해소에 도움이 되고자 함.
-->


## 연구 일정 250911~250926

|               | 9/8~9/10| 9/11~9/13| 9/14~9/16|9/17~9/21|9/22~9/23|9/24~26|
--|--|--|--|--|--|--
|주제 선정| O|   |  |  |  |  |
|전처리 필터, SCCB 설계|  |  O |  |  |  |  | 
|GUI 설계|  |  | O |  |  |  |
|HW 설계|  |  | O | O | O |  |
|GUI 보충 및 HW 최적화|  |  |  |  |  | O |
|Zybo board|  | O | O |  | O |  |
|발표 자료 제작|  |  |  |  | O | O | 




## 프로젝트 과정

**더 많은 내용을 확인하고 싶으면 -->** [[발표 자료]](/Report/AI시스템반도체_발표용_1조_우리함께춤을.pdf)

 <!--

### SW

> #### GUI

|START|SELECT|ENDING
---|--|--
|<img src="/History/img/sw/sw_1.png" alt="스위치 화면" width="400">|<img src="/History/img/sw/sw_2.png" alt="스위치 화면" width="400">|<img src="/History/img/sw/sw_6.png" alt="스위치 화면" width="400">

> #### SCORE

PERFECT|GOOD|BAD|
--|--|--
80% 이상 일치| 80%~50% 일치| 50% 미만 일치|
<img src="/History/img/sw/sw_3.png" alt="스위치 화면" width="400">|<img src="/History/img/sw/sw_4.png" alt="스위치 화면" width="400">|<img src="/History/img/sw/sw_5.png" alt="스위치 화면" width="400">|


### HW


-->

> ### :one: 전처리 필터


#### (1) Median / Gaussian Filter

소벨 필터의 노이즈 민감성을 보완하기 위해, 경계 검출 전에 스무딩(smoothing) 필터를 적용.
| 항목 | Median | Gaussian |
|---|---|---|
| 주 타겟 노이즈 | Salt & Pepper(임펄스) | 센서/가우시안 노이즈 |
| 작동 방식 | 중앙값 | 가중 평균 |
| 특징 | 에지 보존 성능 우수 | 연속적 블러, 에지 약화 |

| Median kernal (3x3) | Gaussian kernal (3x3) |
--|-- 
<img src="/History/img/hw/img_50.png" width=200 >|<img src="/History/img/hw/img_51.png" width=200 >|

#### median filter

```systemverilog
Sort #(.WIDTH(5)) U_Sort_R ( .din (r_data), .dout(sort_r_data)); // Red
Sort #(.WIDTH(6)) U_Sort_G ( .din (g_data), .dout(sort_g_data)); // Green
Sort #(.WIDTH(5)) U_Sort_B ( .din (b_data), .dout(sort_b_data)); // Blue

assign Median_result = {sort_r_data[4], sort_g_data[4], sort_b_data[4]};
```

####  gaussian filter

```systemverilog
assign red = (r_data[0] >> 4) + (r_data[1] >> 3) + (r_data[2] >> 4) + 
                 (r_data[3] >> 3) + (r_data[4] >> 1) + (r_data[5] >> 3) + 
                 (r_data[6] >> 4) + (r_data[7] >> 3) + (r_data[8] >> 4);

assign green = (g_data[0] >> 4) + (g_data[1] >> 3) + (g_data[2] >> 4) + 
                   (g_data[3] >> 3) + (g_data[4] >> 1) + (g_data[5] >> 3) + 
                   (g_data[6] >> 4) + (g_data[7] >> 3) + (g_data[8] >> 4);

assign blue = (b_data[0] >> 4) + (b_data[1] >> 3) + (b_data[2] >> 4) + 
                  (b_data[3] >> 3) + (b_data[4] >> 1) + (b_data[5] >> 3) + 
                  (b_data[6] >> 4) + (b_data[7] >> 3) + (b_data[8] >> 4);

assign Gaussian_Result = {red, green, blue};
```

#### (2) Sobel Filter

- 엣지 검출을 위한 대표적인 이미지 처리 기법 
- 이미지에서 픽셀의 밝기 값 변화를 이용해 경계선을 탐지

#### 🤔 Edge 검출 원리 

**Centered Difference:** $\frac{\partial I}{\partial x} = \frac{I(x+h) - I(x-h)}{2h}$

가운데를 기준으로 양쪽 값을 사용해 기울기 계산 → 편향 감소, 정확도 향상으로 안정적인 경계 검출 및 노이즈에 강함

 #### Edge 검출을 위한 Sobel Mask

|가로 방향 | 세로 방향|
--|--
<img src="/History/img/hw/img_1.png" width=150 >|<img src="/History/img/hw/img_2.png" width=150 >|

```systemverilog
localparam threshold = 1500;

assign xdata = data02 + (data12 << 1) + data22 - data00 - (data10 << 1) - data20;
assign ydata = data00 + (data01 << 1) + data02 - data20 - (data21 << 1) - data22;

assign absx = xdata[9] ? (~xdata + 1) : xdata;
assign absy = ydata[9] ? (~ydata + 1) : ydata;
assign sdata = (absx + absy > threshold) ? 1 : 0;
```


> ### :two: Color Detection Algorithm

- **색 검출 정확도를 올리기 위해서 RGB 방식 :arrow_right: HSV 방식 채택**

#### 🔙 RGB 방식

OpenCV 카메라로 게임에 사용할 빨간 장갑의 RGB 값 탐지

|RGB|8 bit(0~255)|4 bit(approx)(0~15)|
--|--|--
R |236| 236 * 15 / 255 ≈ 14
G |90|  90 * 15 / 255 ≈ 5
B |100| 100 * 15 / 255 ≈ 6


```systemverilog
// rgb565
assign red = (r5 >= 12) && (g6 <= 6) && (b5 <= 6); 
```

#### 🔜 HSV

레드 | RGB	| HSV
--|--|--
| # FF0000 | (255,0,0)	| (0 °, 100 %, 100 %)

#### RGB :arrow_right: HSV 변환 공식 활용

$C_{\max} = \max(R', G', B'), \quad 
C_{\min} = \min(R', G', B'), \quad 
\Delta = C_{\max} - C_{\min}$

$S = \frac{\Delta}{C_{\max}} \quad \text{if } C_{\max} \neq 0$



- 활용: 색조 및 채도 계산 방법 <br>
- 차이점: RGB666으로 최대한 원본 데이터 활용 → 데이터 손실, 오염 방지 가능

```systemverilog
// rgb666
assign max_val = (r6 > g6) ? ((r6 > b6) ? r6 : b6) : ((g6 > b6) ? g6 : b6);
assign min_val = (r6 < g6) ? ((r6 < b6) ? r6 : b6) : ((g6 < b6) ? g6 : b6);
assign delta = max_val - min_val;

assign r_is_max = (r6 > g6) && (r6 > b6) && (r6 > 32);
assign s_is_ok = (delta >= (max_val >> 2));

assign red = r_is_max && s_is_ok;
```

> ### :three: Uart
### Uart Blockdiagram

<img src="/History/img/hw/img_52.png" width=600 > | <img src="/History/img/hw/img_53.png" width=600 >
--|--

* 동일한 문자열을 **2초 동안 0.25초 간격(총 8회)**로 *연속* 전송하면 게이지가 0→100%로 차며,  
**Python GUI State**와 **FPGA 게임 FSM State**가 동시에 다음 단계로 전이.  
* 한 번이라도 **미수신/오수신/간격 위반**이 발생하면 **게이지는 0%로 즉시 리셋**.

<!--
|       구분      | 코드/비트 | 조건                | 송신 문자열 |
|:----------------:|:---------:|:--------------------:|:-----------:|
| **모드 선택**     | 0         | uart_mode_sel == 0  | 'qstick'  |
|                 | 1         | uart_mode_sel == 1  | 'golden'   |
|                 | 2         | uart_mode_sel == 2  | 'sodapop'  |
| **결과 플래그**   | 0         | result[0] == 1      | 'BAD'      |
|                 | 1         | result[1] == 1      | 'GOOD'     |
|                 | 2         | result[2] == 1      | 'PERFECT'  |

| 수신 문자열 | FSM 제어 신호 | 의미 / 트리거     |
|:---------:|:------------:|:----------------:|
|'g'        | uart_sig = 1 | golden 음악 선택  |
|'s'        | uart_sig = 2 | sodapop 음악 선택 |
|'p'        | uart_sig = 1 | 게임 카운트 종료   |
|'f'        | uart_sig = 1 | 점수 표시 완료     |
|'t'        | uart_sig = 1 | 게임 종료         | 
-->

Uart Sender FSM| tx | rx
--|--|--
<img src="/History/img/hw/img_54.png" width=400 >|<img src="/History/img/hw/img_55.png" width=400 > | <img src="/History/img/hw/img_56.png" width=200 > 

<!--

* 동일한 문자열을 **2초 동안 0.25초 간격(총 8회)**로 *연속* 전송하면 게이지가 0→100%로 차며,  
**Python GUI State**와 **FPGA 게임 FSM State**가 동시에 다음 단계로 전이.  
* 한 번이라도 **미수신/오수신/간격 위반**이 발생하면 **게이지는 0%로 즉시 리셋**.

-->

| 'qstick' | 'golden' | 'sodapop' |
|:---:|:---:|:---:|
| <img src="/History/img/hw/img_58.png" width=400 > | <img src="/History/img/hw/img_59.png" width=400 > | <img src="/History/img/hw/img_60.png" width=400 > |

* **패턴 일치율**에 따른 점수 판정 (80% 🔼 / 80% ~ 50% / 50% 🔽)  

| 'PERFECT' | 'GOOD' | 'BAD' |
|:---:|:---:|:---:|
| <img src="/History/img/hw/img_63.png" width=400 > | <img src="/History/img/hw/img_64.png" width=400 > | <img src="/History/img/hw/img_65.png" width=400 > |

> ### :four: Game FSM

<img src="/History/img/hw/img_57.png" width=600 >|
--|

### 단계별 게임 통신 흐름 요약
| 단계 | 트리거/타이밍 | 방향 | 토큰 | 의미 |
|---|---|---|---|---|
| ① Start | 게이지 규칙 충족(8/8) | FPGA→PC | `qstick` | 시작 신호 송신 (tx) |
| ② 곡 선택 | `golden` 또는 `sodapop` 게이지 규칙 충족(8/8) | FPGA→PC | `golden` / `sodapop` | 곡 선택 신호 송신 (tx) |
| ③ 곡 확정 | 3,2,1 카운트다운 끝나는 순간 | PC→FPGA | `g` / `s` | Golden/Sodapop 최종 확정 (rx) |
| ④ 게임 진행(루프) | 5,4,3,2,1 카운트다운 끝나는 순간 | PC→FPGA | `p` | 한 패턴의 판정 시점 도달 (rx) |
| ⑤ 판정 결과 | ④ 이후 즉시 | FPGA→PC | `BAD` / `GOOD` / `PERFECT` | 패턴 일치율 기반 판정 송신 (tx) |
| ⑥ 연출 종료 알림 | 점수 판정 연출이 끝나는 순간 | PC→FPGA | `f` | 해당 패턴 연출 종료 (rx) |
| ⑦ 반복 | 총 **7패턴**에 대해 ④~⑥ 반복 | — | — | `p→(결과)→f` 를 **7회** 수행 |
| ⑧ 종료/리셋 | 모든 패턴 결과 합산 후 | PC→FPGA | `t` | 스코어보드 반영 완료 → 초기 화면 복귀 (rx) |



> ### :five: Parttern Algorithm

### (1) Point In Polygon

어떤 점(Point)이 다각형(Polygon) 내부에 있는지 판별 <br>

|내/외부 판별 Algorithm | 핵심 기술|
--|--
|Ray Crossing | 단순 비교 나눗셈, 곱셈 연산|
|Winding Number | Vector 회전각 계산, 고정 소수점 연산|
|Triangle Fan | 삼각 분할 Data, Barycentric 좌표 연산|
|Bounding Volume | 사각 Grid, 공간 분할 연산|

☑️ 여러 Algorithm 후보들 중에서 제한된 리소스를 가지고 구현할 수 있는 **Ray Crossing** 사용

### (2) Ray Crossing

<img src="/History/img/hw/img_101.png" width=300> | <img src="/History/img/hw/img_102.png" width=300 >|<img src="/History/img/hw/img_103.png" width=300 >|
--|--|-- 

<!--
• 두쌍의 좌표를 입력 받아서 가상의 선분 생성 <br>
• x pixel의 위치가 왼쪽이면 0, 오른쪽이면 1 출력 <br>
-->

1) (x1,y1), (x2,y2) 두 쌍의 좌표를 입력 받아서 가상의 선분 생성 <br>
2) 총 30개의 Module 병렬 실행 → Pattern 제작 <br>
3) x좌표가 증가할 때마다 hit 횟수 Check (XOR 연산 : 홀수번 Hit = 1,짝수번 Hit = 0) <br>

> hit란? 
현재 픽셀이 선분 y 범위 안에 있으면서, 픽셀 x가 선분과 교차하는 x보다 오른쪽에 있는 경우 hit = 1.

:arrow_right: **Pattern 내부 = 1, 외부 = 0 출력**

<!--

#### (3) 패턴 구현 자동화 스크립트 (Python)

#### Issue

초기에는 수동으로 단순히 화면의 좌표를 직접 추출해 hex 코드로 변환해서 업로드

→ 측정오차, 비효율성, 비일관성

> 이러한 문제들을 해결하기 위해 파이썬을 이용해 패턴 구현 자동화 스크립트 구상

#### Process Flow
<img src="/History/img/hw/img_104.png" width=300> | 
--|
- 이미지를 불러온 후 사용하는 VGA 화면 크기로 맞춤
- 이미지 안에서 빨간색 테두리를 탐색
- 윤곽선을 꼭짓점 30개로 단순화
- 선택한 영역(x범위)에 맞추고 원하는 사이즈로 조정해서 바닥 정렬
- 꼭짓점을 연결한 선분 좌표를 추출해서 38비트로 packing → .hex 파일로 저장
- 결과를 미리보기로 확인하고, .hex 파일 다운로드

<img src="/History/img/hw/img_105.png" width=300> | 
--|


#### Result

|그림   |초기 ver | 최종 ver|
--|--|-- 
<img src="/History/img/hw/img_108.png" width=300 >|<img src="/History/img/hw/img_106.png" width=300 >|<img src="/History/img/hw/img_107.png" width=300 >|

> Auto pipeline 과정으로 정확성, 효율성, 일관성 확보

-->



## 🎥 시연 영상

| Game Start | Music Select |
|:--:|:--:|
| <img src="https://raw.githubusercontent.com/2735C/VGA_Motion_Recognition_Game/main/History/img/another/game_play_1.gif" width="380"> | <img src="https://raw.githubusercontent.com/2735C/VGA_Motion_Recognition_Game/main/History/img/another/game_play_2.gif" width="380"> |

| Game Play | Ranking Board |
|:--:|:--:|
| <img src="https://raw.githubusercontent.com/2735C/VGA_Motion_Recognition_Game/main/History/img/another/game_play_3.gif" width="380"> |<img src="https://raw.githubusercontent.com/2735C/VGA_Motion_Recognition_Game/main/History/img/another/game_play_4.gif" width="380"> |


## 💡활용 분야

- **Home Fitness / Smart Home IoT**: 집에서 쉽게 따라하는 체조 및 동작 인식
- **안전 모니터링**: 낙상 방지—지정 영역 이탈 감지 알람
- **K-POP 챌린지**: 점수 공유/영상 업로드로 **SNS 확산** 기대


## 🚀Trouble Shooting 
[⚒️[점수 계산 Error]](/History/trouble_shooting/Trouble_Shooting1.md)   <br>
[⚒️[GAME STATE 전이 실패]](/History/trouble_shooting/Trouble_Shooting2.md)  <br>
[⚒️[Pattern 구현 Module 리소스 초과]](/History/trouble_shooting/Trouble_Shooting3.md) <br>
[⚒️[패턴 구현 자동화 스크립트 (Python)]](/History/trouble_shooting/Trouble_Shooting7.md) <br>
[⚒️[Clock Domain Crossing Issue]](/History/trouble_shooting/Trouble_Shooting4.md) <br>

추가 가능 ~~ <br>
[⚒️[Trouble_Shooting5]](/History/trouble_shooting/Trouble_Shooting5.md) <br>
[⚒️[Trouble_Shooting6]](/History/trouble_shooting/Trouble_Shooting6.md) <br>
