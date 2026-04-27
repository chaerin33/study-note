# study-note
학습기록

# Lumped Parameter System — 핵심 개념 누적

---

## Week 1: 시스템 모델링 개요 & 상태변수 해석 입문 (2025.03.03)

**핵심 식:**

$$\dot{\mathbf{x}}(t) = A\mathbf{x}(t) + B\mathbf{u}(t)$$

$$\mathbf{x}(t) = e^{At}\mathbf{x}(0) + \int_0^t e^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau$$

$$e^{At} = \Phi(t) = \Phi\, e^{\Lambda t}\,\Phi^{-1} \quad \text{(State Transition Matrix)}$$

**핵심 개념:**

- **Lumped Parameter System**: 집중 매개변수 시스템. 공간 분포 무시 → ODE로 기술 가능
- **Interdisciplinary System**: ME + EE 결합 시스템 (병진계, 회전계, 전기계 통합 모델링)
- **Linearization**: 비선형 ODE를 Taylor Series로 선형 근사
- **State-Variable Form**: $n$개의 2차 ODE → $2n$개의 1차 ODE, 수치해석(Runge-Kutta) 적용에 필수
- **System Matrix $A$**: 시스템 물성($m$, $c$, $k$) 정보를 담은 행렬
- **Eigenvalue/Eigenvector**: 상태변수 방정식의 해 구조 결정
- **Matrix Exponential $e^{At}$**: State Transition Matrix $\Phi(t)$ — 초기조건 → 임의 시점 상태 전이
- **Cayley-Hamilton Theorem**: $e^{At}$ 계산에 사용 (다음 주 세부 커버 예정)
- **Jordan Canonical Form**: 고유값 중복(multiplicity) 시 적용 (다음 주 세부 커버 예정)

**이번 주 과제:** 없음 (첫 주 — 강의 개요 및 로드맵 소개)

---

## Week 2: Parameter/Property 정의 & 1차 시스템 분석 (2025.03.10)

**핵심 식:**

$$\tau\frac{di}{dt} + i(t) = \frac{1}{R}e_s(t), \quad \tau = \frac{L}{R} \quad \text{(RL 1차 시스템)}$$

$$i(t) = \frac{1}{R}\!\left(1 - e^{-t/\tau}\right) \quad \text{(단위 계단 입력, 영 초기조건)}$$

$$H(s) = \frac{I(s)}{E_s(s)} = \frac{1/R}{\tau s + 1} \quad \text{(전달 함수)}$$

$$J\dot{\omega}(t) + b\omega(t) = T_E(t) \quad \text{(회전계 1차 형태)}$$

**핵심 개념:**

- **Property (속성)**: 시스템 물성 — 직접 측정 가능 ($m$: 질량, $k$: 강성, $c$: 감쇠)
- **Parameter (매개변수)**: ODE 안에서 각 미분 항을 연결하는 계수 역할. 물성이 수식에 들어오면 parameter
- **Parameterization**: 물성 정보를 내재한 무차원 척도로 재표현 (예: $r = \omega/\omega_n$)
- **Duffing Equation**: $m\ddot{x}+c\dot{x}+kx+\beta x^3 = F(t)$ — 비선형 ODE
- **Mathieu Equation**: $m\ddot{x}+c\dot{x}+k(t)x = F(t)$ — Linear Time-Variant (LTV)
- **Parameter Excitation**: 시스템 파라미터 자체가 시간에 따라 변해 가진력 역할 (예: 기어 강성 변동)
- **Variable Separation**: Distributed Parameter System(PDE) 해법 — $u(x,t)=X(x)T(t)$
- **FEM 이산화**: 연속체 → 유한 집중질량 집합 → Lumped Parameter System으로 변환
- **Time Constant $\tau$**: 1차 시스템에서 최종값의 63%에 도달하는 시간. $\tau = L/R$ (RL 회로)
- **Transfer Function $H(s)$**: 영 초기조건 하에서 출력/입력의 Laplace 비
- **전기-기계 Analogy**: $\tau \leftrightarrow J$, $i \leftrightarrow \omega$, $e_s \leftrightarrow T_E$ — 전기계와 회전계 구조 동일
- **Back-EMF**: $e_m = K_E \omega$ — 모터 내부 역기전력; $T_D = K_T i$ — 발생 토크. $K_T \approx K_E \equiv K$

**이전 개념과의 연결:** Week 1의 State-Variable Form(1차 ODE 시스템)이 이번 주 1차 시스템 분석의 기반. RL 회로와 회전계 모두 $\dot{x} = ax + bu$ 형태의 스칼라 버전임.

**이번 주 과제:** 없음

---

## Week 3: DC 모터 전달함수 & 유압 시스템 모델링 (2025.03.17)

**핵심 식:**

$$\frac{W(s)}{E_i(s)} = \frac{K_T}{(L_a s+R_a)(Js+B)+K_T K_V} \quad \text{(DC 모터 전달함수, 완전형)}$$

$$\frac{W(s)}{E_i(s)} \approx \frac{G_3}{\tau s+1}, \quad \tau = \frac{R_a J}{R_a B + K_T K_V} \quad (L_a \approx 0 \text{ 근사})$$

$$i_a(t) = G_2 + C\,e^{-t/\tau}, \quad \omega(t) = G_3\!\left(1 - e^{-t/\tau}\right) \quad \text{(단위 계단 응답)}$$

$$T_m = \Delta P_m \cdot D_m, \quad D_m = \frac{Q_m}{\omega_m} \quad \text{(유압 모터 기본식)}$$

$$C_f \dot{P} + \frac{1}{R_f}P + D_m \dot{\theta}_m = Q_i(t) \quad \text{(유압-기계 복합계 ①)}$$

$$J\ddot{\theta}_m + B\dot{\theta}_m = D_m \cdot P(t) \quad \text{(유압-기계 복합계 ②)}$$

**핵심 개념:**

- **Armature-controlled DC Motor**: 전기자 회로(KVL) + 기계계(Newton 2nd) 연성 → 2×2 시스템
- **$L_a \approx 0$ 근사**: 실제 armature 인덕턴스는 매우 작음 → 2차 → 1차 시스템으로 단순화
- **복합 시정수 $\tau$**: $\tau = R_a J/(R_a B + K_T K_V)$ — 전기 파라미터($R_a$)와 기계 파라미터($J, B$) 동시 포함
- **Pole**: 전달함수 분모의 근 → 자유응답 모드(자연주파수, 감쇠율) 결정, 안정성 판별
- **Zero**: 전달함수 분자의 근 → 입력 조건의 동적 특성; 해당 주파수에서 입력 소거
- **Amplifier + Motor**: 앰프 이득 $G$ 도입 → $J\ddot{\theta}_m + (B + k^2/R_m)\dot{\theta}_m + T_L = (kG/R_m)E_d$
- **PDP (Positive Displacement Pump)**: 고정 체적 변위, 일정 압력/유량 → Yongjeok pump (용적 펌프)
- **Centrifugal Pump**: 내외부 압력차 이용 (터빈형)
- **유체계 동력**: $P_{power} = \Delta P \cdot Q$ (압력×유량) $\equiv T \cdot \omega$ (토크×각속도)
- **Displacement $D_m$**: 단위 라디안당 유량 [m³/rad] — 유압 모터/펌프의 기계-유체 연성 계수
- **유체 Capacitance $C_f$**: 저장조의 압력에 따른 유량 저장 능력 ($Q = C_f \dot{P}$)
- **유체 Resistance $R_f$**: 누설 저항 ($Q_{leak} = P/R_f$)
- **유체-전기 Analogy**: $P \leftrightarrow V$, $Q \leftrightarrow i$, $C_f \leftrightarrow C$, $R_f \leftrightarrow R$

**이전 개념과의 연결:** Week 2의 Back-EMF/토크 상수 개념($K_T, K_V$)이 이번 주 모터 전달함수 유도의 핵심 연성 항으로 등장. 1차 시스템 구조($\tau s+1$ 형태)는 Week 2와 동일하며, 시정수 $\tau$의 구성만 복잡해짐.

**이번 주 과제:**
- 계자권선 포함 DC 모터($L_f, R_f, L_a, R_a$): $K_t, K_a$ 기본 방정식 유도
- 유압 펌프-모터 시스템($D_p, D_m, R_{leak}, C_{ac}, J_v$): 복합 운동방정식 유도

---

## Week 4: 2-DOF 자유진동 & 고유값 분석 + State-Variable 변환 + 주파수 응답 (2025.03.24)

**핵심 식:**

$$\det(\underline{K} - \lambda\underline{M}) = 0 \quad \text{(일반 고유값 특성방정식, } s^2=-\lambda \text{ 치환)}$$

$$\underline{X}(t) = \underline{u}_1[A_1\cos(\sqrt{\lambda_1}\,t)+B_1\sin(\sqrt{\lambda_1}\,t)] + \underline{u}_2[A_2\cos(\sqrt{\lambda_2}\,t)+B_2\sin(\sqrt{\lambda_2}\,t)]$$

$$\underline{A} = \begin{pmatrix}\underline{0} & \underline{I} \\ -\underline{M}^{-1}\underline{K} & -\underline{M}^{-1}\underline{C}\end{pmatrix} \quad \text{(N-DOF State-Variable Compact Form)}$$

$$X_{k+1} = X_k + \dot{X}(t_k)\cdot\Delta t \quad \text{(Euler 수치적분)}$$

$$\tilde{\underline{X}} = [(\underline{K}-\omega^2\underline{M})+i\omega\underline{C}]^{-1}\tilde{F}_0 \quad \text{(주파수 응답 함수)}$$

**핵심 개념:**

- **Definite System**: $X^TAX>0$, $\lambda\neq 0$ → 모든 자연주파수 존재. 모든 고유값 양수
- **Semi-Definite System**: $X^TAX\geq 0$, $\lambda=0$ 포함 → 첫 자연주파수 $=0$ (rigid-body mode)
- **Rigid-body Mode**: Semi-definite 시스템에서 두 질량이 함께 병진운동, 상대변위=0, $\omega_1=0$
- **Out-of-phase Mode**: 두 질량이 반대 방향으로 진동하는 모드
- **$\underline{M}$-직교성**: 일반 고유값 문제 $\underline{K}\underline{x}=\lambda\underline{M}\underline{x}$에서 $\underline{u}_i^T\underline{M}\underline{u}_j=0$ ($i\neq j$)
- **Mode Shape $\underline{u}_i$**: 고유벡터의 물리적 해석 — 각 자연주파수에서의 진동 형태
- **Nullspace**: $B\underline{x}=0$의 해 집합 → 고유벡터 계산의 수학적 기반
- **Euler Method**: $X_{k+1}=X_k+\dot{X}\Delta t$ — 수치해석의 가장 기본적인 시간적분법
- **Homogeneous + Particular Solution**: $X(t)=X_h(t)+X_p(t)$ — 강제진동 완전해 구조
- **Frequency Response Function (FRF)**: $\tilde{X}=[(\underline{K}-\omega^2\underline{M})+i\omega\underline{C}]^{-1}\tilde{F}_0$ — 주파수 영역 응답
- **Resonance 개수**: N-DOF 시스템 → N개의 공진 피크 (일반적)
- **Taylor Series (Power Series)**: $f(x)=\sum_{n=0}^\infty\frac{1}{n!}\frac{d^nf}{dx^n}\big|_{\bar{x}}(x-\bar{x})^n$ — 비선형 함수 선형화 수학적 기반

**이전 개념과의 연결:**
- Week 1의 State-Variable Form $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$가 이번 주 N-DOF compact 형태로 완성됨
- Week 1의 Linearization 개념이 이번 주 Taylor Series 유도로 수학적으로 완결됨
- Week 1의 Eigenvalue/Eigenvector가 이번 주 물리 시스템(2-DOF)에서 구체적으로 계산됨

**이번 주 과제:**
- 2-DOF 시스템에서 $\omega=0.2$ Hz, $0.3$ Hz 가진 조건에서 주파수응답 계산 및 MATLAB 그래프 작성
  - 핵심 개념: 복소 행렬 역산 $[(\underline{K}-\omega^2\underline{M})+i\omega\underline{C}]^{-1}$ 적용

---

## Week 5: 비선형 시스템 선형화 & Jacobian 안정성 분석 (2025.03.31)

**핵심 식:**

$$x(t) = \bar{x} + \hat{x}(t) \quad \text{(운용점 + 섭동 분해)}$$

$$f(x) \approx f(\bar{x}) + \left.\frac{df}{dx}\right|_{x=\bar{x}}(x-\bar{x}) = \bar{f} + k\hat{x} \quad \text{(Taylor 1차 선형화)}$$

$$\dot{\underline{\xi}} = J_x\big|_{\tilde{\underline{x}},\tilde{\underline{u}}}\cdot\underline{\xi} + J_u\big|_{\tilde{\underline{x}},\tilde{\underline{u}}}\cdot\delta\underline{u}, \quad J_x = \frac{\partial\underline{f}}{\partial\underline{x}}\bigg|_{\tilde{\underline{x}},\tilde{\underline{u}}} \quad \text{(Jacobian 선형화)}$$

$$\lambda_i = a_i + ib_i: \quad \text{모든 }a_i \leq 0 \Rightarrow \text{안정}, \quad \exists\, a_i>0 \Rightarrow \text{불안정}$$

**핵심 개념:**

- **Operating Point $\bar{x}$**: 운용점(평형점, fixed point, mean value) — 비선형 시스템에서 선형화의 기준점
- **Perturbation Term $\hat{x}$**: 운용점 기준 소변위 동적 항 — DC/AC 분리와 동일 개념
- **Taylor 1차 선형화**: 비선형 함수를 운용점 근방에서 접선 기울기($k$)로 근사
- **Jacobian 행렬 $J_x$**: 다변수 비선형 함수의 편미분 행렬 → 선형화된 시스템 행렬 $A$에 해당
- **고유값 실수부 $a_i$**: 각 모드의 증폭/감쇠 결정. 안정 판별의 핵심 지표
- **Marginal Stability (한계 안정)**: 모든 $a_i \leq 0$이나 일부 $a_i=0$ → 지속 진동
- **Phase Plane (위상 평면)**: 상태변수 $x_1$-$x_2$ 평면에서 궤적으로 안정성 시각화. 내향 나선=안정, 외향 나선=불안정
- **Engineering Stability**: 동적 응답 자체의 수렴/발산. Lyapunov 안정성과 동일 개념
- **Structural Stability**: 파라미터 소변화에 따른 동적 거동의 질적 변화. Bifurcation 이론으로 분석
- **Bifurcation (분기)**: 파라미터 미소 변화로 동적 거동이 급변하는 현상 (역진자, Duffing jump 현상)
- **중력항 소거**: 평형점 $\bar{x}=mg/k$ 정의 후 $x(t)=\bar{x}+\hat{x}(t)$ 대입 → $mg$와 $k\bar{x}$ 상쇄

**이전 개념과의 연결:**
- Week 1의 Linearization 개념이 이번 주 Taylor Series + Jacobian으로 완전히 수학화됨
- Week 1의 Eigenvalue/Eigenvector(안정성 판별)가 이번 주 Jacobian 고유값 안정성으로 비선형계까지 확장됨
- Week 4의 Taylor Series가 이번 주 다변수 Jacobian 선형화의 기초로 재활용됨

**이번 주 과제:** 없음 (녹음 확인)

---

## Week 6: Fourier Transform & Discrete Fourier Transform (DFT) (2025.04.07)

**핵심 식:**

$$\hat{X}(\omega) = \mathcal{F}\{x(t)\} = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{\infty} x(t)\, e^{-i\omega t}\, dt$$

$$\mathcal{F}\{A\cos(\omega_0 t)\} = A\left[\delta(\omega - \omega_0) + \delta(\omega + \omega_0)\right]$$

$$\Delta t = h = \frac{T}{N}, \quad \Delta f = \frac{1}{T}, \quad f_s = \frac{N}{T}, \quad f_H = \frac{f_s}{2} \leq f_N$$

$$\omega_k = \frac{2\pi}{T}\cdot n, \quad n = 0,\,1,\,2,\,\ldots,\,N-1$$

**핵심 개념:**

- **Fourier Transform (FT)**: 시간 영역 신호 → 주파수 영역 변환. 크기($|\hat{X}(\omega)|$)와 위상($\phi(\omega)$) 추출
- **Dirac Delta $\delta(\omega)$**: 순수 코사인/사인 신호의 FT 결과. $\omega=\pm\omega_0$에서만 임펄스 존재
- **Superharmonic**: 기본 주파수보다 높은 주파수 성분 (비선형 응답에서 발생)
- **Subharmonic**: 기본 주파수보다 낮은 주파수 성분 (Week 5의 Bifurcation과 연결)
- **$N$ (샘플 수)**: 한 주기 $T$ 안에 취득하는 이산 데이터 개수
- **$\Delta t = T/N$**: 시간 간격 (= $h$)
- **$\Delta f = 1/T$**: 주파수 해상도 — $T$가 클수록 주파수 분해능 향상
- **$f_s = N/T$**: 샘플링 주파수. $N$ 증가 → $f_s$ 증가 → 더 촘촘한 측정
- **$f_H = f_s/2$**: Nyquist 주파수 — 분석 가능한 최대 주파수의 이론적 한계
- **$f_N \leq f_H$**: 실용 주파수 — 산업 현장에서 $0.2 \sim 0.4 \times f_s$로 보수적 설정
- **Aliasing**: $f > f_H$ 영역의 DFT 결과는 낮은 주파수 구간의 거울 상(mirror image) → 가짜 신호
- **Sine vs. Cosine FT 차이**: 크기는 동일($A$), 위상만 다름 (코사인 → $\phi=0$, 사인 → $\phi=-\pi/2$)
- **시간 주기 $T$ 선택 기준**: 분석 대상 중 가장 낮은 주파수(가장 긴 주기)를 포함해야 함

**이전 개념과의 연결:**
- Week 4의 주파수응답함수(FRF)가 주파수 영역 분석의 출발점 → 이번 주 FT가 그 수학적 도구로 완성
- Week 5의 Subharmonic/Bifurcation 현상을 실제로 분석하려면 FT가 필수 → 두 개념 연결
- Zero input condition 하의 해법 ($\dot{x}=Ax$) 도입 예고 → 다음 주 본격 전개

**이번 주 과제:**
- $x(t) = A\sin(\omega_0 t)$ ($f_0 = 1, 2, 10$ Hz)에 대해 FT 수행, MATLAB `stem` 그래프 작성
  - 핵심 개념: Sine FT → 크기 $A$, 위상 $-\pi/2$ 확인; `angle()` 명령어 활용
  - $T = 1$ or $5$ or $10$ 초 선택 → DFT 파라미터 실습

---

## Week 7: Cayley-Hamilton Theorem & 행렬 함수 계산 (2025.04.14)

**핵심 식:**

$$P(\underline{A}) = a_n\underline{A}^n + a_{n-1}\underline{A}^{n-1} + \cdots + a_1\underline{A} + a_0\underline{I} = \underline{0} \quad \text{(Cayley-Hamilton Theorem)}$$

$$f(\underline{A}) = R(\underline{A}) = \sum_{k=0}^{n-1}\beta_k\,\underline{A}^k, \quad f(\lambda_i) = R(\lambda_i) \quad \text{(행렬 함수 = 잔류 다항식)}$$

$$e^{\underline{A}t} = \alpha_0(t)\underline{I} + \alpha_1(t)\underline{A} + \cdots + \alpha_{n-1}(t)\underline{A}^{n-1}, \quad e^{\lambda_i t} = \sum_{k=0}^{n-1}\alpha_k\lambda_i^k$$

**핵심 개념:**

- **Zero-input Condition**: $\dot{\mathbf{x}}=\underline{A}\mathbf{x}$ → 해: $\mathbf{x}(t)=e^{\underline{A}t}\mathbf{x}(0)$ — 시스템의 자유응답, 안정성 정보 내포
- **Cayley-Hamilton Theorem**: $n\times n$ 행렬 $\underline{A}$는 자신의 특성다항식을 만족 → $P(\underline{A})=\underline{0}$
- **Adjoint**: $\text{adj}(\underline{A}) = C_{\underline{A}}^T$ (cofactor 행렬의 전치). Cayley-Hamilton 증명의 핵심 도구
- **Adjoint의 차수**: $n\times n$ 행렬의 $\text{adj}(s\underline{I}-\underline{A})$는 최대 $s^{n-1}$ 차 행렬다항식
- **Remainder Polynomial $R(s)$**: $f(s) = Q(s)\Delta(s)+R(s)$ — $\Delta(\lambda_i)=0$이므로 $f(\lambda_i)=R(\lambda_i)$
- **$f(\underline{A})=R(\underline{A})$**: Cayley-Hamilton에 의해 $\Delta(\underline{A})=\underline{0}$ → 고차항 모두 소거, 잔류 다항식만 남음
- **Strong/Closed Form**: 유한 항의 닫힌 표현 (예: $e^t$, $\sin t$)
- **Weak/Open Form**: Taylor 급수 등 무한 항 급수 표현 — 불연속 함수, 복잡한 경계조건 처리에 활용
- **순허수 고유값 → 회전 행렬**: $\lambda=\pm i$ → $e^{\underline{A}t}=\begin{pmatrix}\cos t&\sin t\\-\sin t&\cos t\end{pmatrix}$ — Marginal Stability와 연결

**이전 개념과의 연결:**
- Week 1의 $e^{At}=\Phi(t)$ (State Transition Matrix)가 이번 주 Cayley-Hamilton으로 실제 계산 가능해짐
- Week 5의 고유값 실수부 안정성 → 순허수 고유값($a_i=0$)이 회전 행렬(지속 진동, 한계 안정)로 구체화
- Week 1의 Jordan Canonical Form 예고가 다음 주(중복 고유값 처리)로 이어짐

**이번 주 과제:** 없음 (중간시험 4월 28일 예정)

---

## Week 8: Multiplicity 처리 & Eigendecomposition & 상태변수 해 유도 (2025.04.21)

**핵심 식:**

$$\left.\frac{d^k}{ds^k}e^{st}\right|_{s=\lambda_i} = \left.\frac{d^k}{ds^k}R(s)\right|_{s=\lambda_i} \Rightarrow t^k e^{\lambda_i t} = \frac{d^k R}{ds^k}\bigg|_{s=\lambda_i}, \quad k=0,1,\ldots,m-1$$

$$\underline{A}\,\underline{U} = \underline{U}\,\underline{\Lambda} \quad \Rightarrow \quad \underline{U}^{-1}\underline{A}\,\underline{U} = \underline{\Lambda}, \quad \underline{A} = \underline{U}\,\underline{\Lambda}\,\underline{U}^{-1}$$

$$\dot{\mathbf{x}} = \underline{A}\mathbf{x}, \quad \mathbf{x}(t) = e^{\underline{A}t}\mathbf{x}(0) \quad \text{(Zero-input 해, 초기조건 결정)}$$

**핵심 개념:**

- **Multiplicity $m$**: 특성방정식에서 동일 고유값이 $m$번 반복 → 독립 방정식 수 부족
- **미분 보충법**: $s$에 대한 $k$차 미분 → $t^k e^{\lambda_i t}$ 항 생성 → $m$개의 추가 방정식 확보
- **Eigendecomposition**: $\underline{A}\underline{U}=\underline{U}\underline{\Lambda}$ — 고유벡터 행렬 $\underline{U}$로 $\underline{A}$를 대각화
- **$\underline{U}^{-1}\underline{A}\underline{U}=\underline{\Lambda}$**: 좌×$\underline{U}^{-1}$ → 대각화 형태
- **$\underline{A}=\underline{U}\underline{\Lambda}\underline{U}^{-1}$**: 우×$\underline{U}^{-1}$ → Eigendecomposition 형태 (중간시험 주요 포인트)
- **System Matrix 명칭 이유**: $\underline{A}$ 성분이 시스템 물성($m, c, k$)을 직접 반영하기 때문
- **Trivial Condition 회피**: $(s\underline{I}-\underline{A})\mathbf{X}=\mathbf{0}$에서 non-trivial 해 → $\det(s\underline{I}-\underline{A})=0$ 필수
- **Superharmonic**: 기본 주파수보다 높은 스펙트럼 성분 — 1주기 캡처로 충분
- **Subharmonic**: 기본 주파수보다 낮은 스펙트럼 성분 — 더 긴 캡처 범위(저주파 1주기) 필요
- **검증 습관**: $e^{\underline{A}t}\big|_{t=0}=\underline{I}$ → 계산 결과 반드시 확인

**이전 개념과의 연결:**
- Week 7의 Cayley-Hamilton(계수 $\alpha_k$ 결정법)이 이번 주 Multiplicity 처리로 완전한 일반화
- Week 6의 FT 데이터 선택 기준이 Superharmonic/Subharmonic 개념과 연결하여 재정리
- Week 5의 안정성 판별 → 고유값 실수부 부호 → Eigendecomposition 구조와 연결

**이번 주 과제:** 없음 (중간시험 준비)
