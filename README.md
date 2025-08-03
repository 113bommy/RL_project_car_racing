# CarRacing DQN & Constrained RL Project

이 프로젝트는 **CarRacing-v2** 환경에서 DQN 및 Constrained DQN 접근을 통해 에이전트를 학습하는 예제입니다.  
병렬 환경, Shrink & Perturb, 맵 리셋 등 다양한 기법을 적용했으며,  
다음 논문 아이디어와 연관되어 있습니다:

1. [Constrained Reinforcement Learning]  
2. [Sample Efficient Reinforcement Learning (ICML 2024)]

---

## 주요 아이디어

1. **일반 DQN과 Constrained DQN**  
   - 일반 DQN(`module.py`의 `DQN` 클래스)과, 속도 초과/트랙 이탈을 페널티로 처리하는 Constrained DQN(`ConstrainedDQN` 클래스)을 구현.  
   - Constrained DQN은 라그랑주 승수를 동적으로 업데이트하여, 주행 속도가 너무 빠르거나 트랙에서 벗어나면 보상에 페널티를 부여함.

2. **병렬 환경(Parallel Environments)**  
   - 여러 개(`env_count`)의 CarRacing 환경을 동시에 구동하여, 한 에피소드 안에서도 다수의 경험을 빠르게 쌓도록 설계.  
   - 샘플 효율 증가, 학습 시간 단축 효과.

3. **Shrink & Perturb**  
   - 일정 주기(`TR`)마다 현재 네트워크 파라미터와 초기 파라미터를 혼합해(\(\alpha\)), 모델 파라미터가 과도하게 튀는 것을 방지.  
   - 안정적인 학습 유도.

4. **맵 리셋(Map Reset Interval)**  
   - `map_reset_interval`마다 CarRacing 맵을 변경(난수 시드 재설정)해, 특정 맵 구조에만 과적합되는 현상을 막음.

5. **실험 결과**  
   - `Score_performance.png`, `Time_performance.png` 등에 다양한 실험 결과(평균 점수, 에피소드 당 시간 등)가 시각화되어 있음.  
   - `CarRacing_eval_baseline.gif`, `CarRacing_eval_Constrained.gif`는 학습이 끝난 후 에이전트 주행 모습(애니메이션 GIF).

---