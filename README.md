# text-summarisation-with-BART
[Dacon AI 기반 회의 녹취록 요약 경진대회](https://dacon.io/competitions/official/235813/overview/description)

### 지난 프로젝트 회고
- 지난 번 분류 프로젝트를 통해 분석 - 전처리(증식) - 훈련 - 검증 - 시험을 아우르는 NLP 전반의 과정을 경험할 수 있었다.
- 특히 EDA와 Back Translation을 통해 한정된 데이터를 효율적으로 모델 훈련에 투입할 수 있음을 알 게 된 것은 상당한 교훈이었으며, 
- K-Fold 및 앙상블 기법을 실제로 적용해보며 성능 극대화를 위한 여러 가지 가능성에 대해서도 생각해볼 수 있었다.

### 이번 프로젝트 선정
- 작년 여름 LG AI Research에서 주최하고 Dacon이 주관한 <AI 기반 회의 녹취록 요약 경진대회>의 연습 참가가 가능했다. 채용이 전제된 만큼 상위권과 그 외의 격차가 컸으며 상위권 내에서도 오차 범위 내 경쟁이 치열한 대회였다. 지난 프로젝트와 마찬가지로 상위권 진입을 목표로 아는 것과 할 수 있는 것 전부를 동원해보기로 했다.

### 목표
- 상위 4% 진입
- 사전 데이터 분석을 통한 뚜렷한 목표 수립
- Back Translation 및 EDA의 4가지 영역인 SR/RI/RD/RR을 전부 적용한 데이터 증식
- 높은 성적을 내기에 적합한 모델 선정
- Epoch / Batch Size / Early Stopping / LR Warmup / LR Scheduler 등 각종 하이퍼 파라미터 조율을 통한 효과적인 훈련
- Mixed Precision / Gradient Accumulation을 통한 효율적인 자원 활용
- 다양한 실험을 위한 Logging 방법의 개선
- 평가 지표에 대한 이해와 그를 통한 모델 검증(Rouge or Loss)

### 진행
- 데이터 변환: JSON ⇒ Pandas Data Frame
- 데이터 분석 및 시각화: 시퀀스 길이 분포 파악 및 가용성 검토
- 데이터 증식: SR/RI (2994 x 3)
- 모델 선택: ainize/kobart-news / csebuetnlp/mT5_multilingual_XLSum / google/mt5-small
- 파인 튜닝: 하이퍼 파라미터 및 max_position_embeddings 조정
- 훈련 모델 사용: 그리디 서치와 빔 서치 각각의 성적 비교
- Data Augmentation: RD/RS (2994 x 3 ⇒247756)
- WandB 로깅을 시작하여 효과적인 훈련 전략 모색
- 원본 데이터로만 구성된 검증 세트 활용
- 증식 데이터가 원본의 파생임을 감안해 Step(Iteration) 기준으로 검증과 체크포인트 생성 시작
- 증식 데이터 전체 활용을 위해 LR Warmup 및 코사인 LR Scheduler를 적용한 1에폭 훈련
- Rouge와 Loss를 기준으로 각각 검증 시도

### 결과
- 최종 성적 7위로 상위 1.5% 진입

### 회고
- 지난 번에 비해 발전된 생각과 역량으로 임했기에 좀 더 촘촘하게 NLP의 전반적인 과정을 이해하고 익힐 수 있었다.
- 증식된 데이터가 원본의 파생이라는 것을 염두에 두고 훈련 루틴을 짜야 함을 알게 됐다.
- [증식 데이터 불균형에 대해 생각하지 못 함](https://colab.research.google.com/drive/16DKcmA9iqA7Bp9Q2nd57WLdlfhd7hT9s?usp=sharing)
- 다양한 하이퍼 파라미터 설정 실험을 통해 모델 훈련에 대한 이해도를 높힐 수 있었다.
- [로깅 툴을 적극적으로 활용해야 함](https://wandb.ai/dotsnangles/BART-Generative-Summarization)
- 데이터/모델에 대한 이해와 더불어 구현과 직결된 프로그래밍 역량을 더욱 더 길러나가야 한다.
- 협업 툴 사용을 좀 더 활성화하여 팀 내 작업 상황 공유도를 높혀야 한다.

### 예정 사항
- 파이토치 해커톤
- 논문 리뷰
- 챗봇 프로젝트
