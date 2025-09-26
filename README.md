<플레이 영상_사망> -> 소리 나오는 버전 : https://drive.google.com/file/d/14jJ3N_jKSOX2zaoOEs4HkbWbqRcuvtjr/view?usp=sharing

https://github.com/user-attachments/assets/735ac9b8-49ab-46e7-b44b-df35ca2850a4

<플레이 영상_스킵_엔딩> -> 소리 나오는 버전 : https://drive.google.com/file/d/1cv4aG5kUBNL8cWOW5KC5xKcXTDa4SWsk/view?usp=sharing


https://github.com/user-attachments/assets/6e9e627d-968f-4272-86ce-2b1505e19a61



## 게임명 : Backroom
#### 1인칭 스토리 호러 게임


## 기획 의도
#### 개인적으로 좋아하는 게임 장르인 공포게임을 언리얼 블루프린트로 구현하고 싶었고, 재미있게 플레이 했었던 Backroom 스토리를 인용하였음


## 진행 기간
#### 2025.03.19 ~ 26(8일간)


## (기술 스택)선택 이유
#### (Blueprint) 언리얼 C++ 구현 전에 언리얼 블루프린트 기능을 경험하기 위


## 프로젝트 진행 단계
1. 게임 기획 및 에셋 수집
2. Enemy 액터 구현(움직임, 콜리전 반응 등)
3. 맵 애셋 선택
4. 기타 기능 추가
5. 시작 및 엔딩 추가
6. 버그 픽스



## 프로젝트 세부 과정
### 게임 기획 및 에셋 수집

#### 게임 기획
- 게임 카테고리 : 공포게임
- 참고 : Backroom, SCP

#### 에셋 수집
- 맵 : Fab 활용 오픈월드 숲
- Enemy : Mixamo 활용

---
### Enemy 액터 구현(움직임, 콜리전 반응 등)

#### Enemy 콜리전 기본 구현
- Enemy와 Player가 충돌하면 Print 출력
- Enemy와 Player가 충돌하면 View Target 변경
  1. 타임라인과 Lerp를 활용하여 화면 전환

#### AI 구현
- Idle 및 Run 애니메이션 연결
- 언리얼에서 제공하는 AI 무브 및 Pawn Sensing 기능을 활용하여 Player가 탐지되면 추적하도록 구현

#### SCP173 구현
- 1차 구현(실수로 파일을 삭제하여 다시 구현)
1. 기본 이동은 AI 이동과 동일
2. Player 화면에 해당 Enemy가 랜더링 시 움직임 정지 >> Was Actor Recently Rendered 이벤트를 활용

- 다른 방법으로 2차 구현
1. 기본 이동은 AI 이동과 동일
2. 내적을 사용한 시야 판정
3. Collision 시 사망 연출 >> 모든 Enemy 오브젝트의 공격(플레이어 사망) 연출 동일
  1. Enemy와 Player 충돌
  2. Audio Component 재생하여 웃음소리 재생
  3. Player 시야 View에서 Enemy 정면 View로 이동할 때 TimeLine을 통해 천천히 이동 구현
  4. Enemy 정면 View로 이동한 화면을 Lerp를 통해 Player에게 다가가는 연출 구현
  5. 위젯 애니메이션과 버튼을 통해 Game Over 연출 및 Restart 버튼 활성화 (Restart 버튼 클릭 시 맨 처음 Backroom 레벨에서 시작)

#### DontMove Enemy 구현
- AI Move 및 PawnSinsing 등을 통해 AI 움직임 구현
- Player와 충돌 시 위젯을 통해 “Don’t Move”라는 문구가 정면에 뜨면 5초 동안 움직이면 안 되도록 구현(움직이면 Player 사망)
- 5초가 지나면 해당 몬스터는 사라짐(Don’t Move 문구 또한 사라짐)
---

### 맵 에셋 선택

#### 오픈월드 맵 최적화
- 게임 스타트 시 긴 로딩을 해소하기 위해 맵 최적화 노력(실패)
1. 엔진 퀄리티 낮춤
2. 안개 활용
3. 컬 디스턴스 볼륨 활용
4. 월드 파티션 활용
- 최적화 기법을 효율적이고 제대로 사용하는 방법에 대해 더 찾아볼 필요 有
- 맵 변경 예정
#### 맵 제작 및 환경 세팅
- 기본 틀(벽, 기둥, 바닥, 천장, 조명 배치 및 머티리얼 적용) 구성
- Emissive Color로 만 발광체 천장에 배치(조명)
- 포스트프로세스 볼륨 적용 >> Exposure 적용
- Player 카메라에 셰이크 적용(동적인 화면)
- 벽에 Graffiti 부착(간접적으로 탈출 방법 소개)
- 나레이션 및 자막을 적용하고 Data Table을 통해 동기화
- AmbientSound를 통해 BGM 적용
---
### 기타 기능 구현
#### Enemy 발소리 구현
- Walk 애니메이션에서 발이 지면에 닿을 때 발자국 사운드 추가
- 사운드 큐와 어테뉴에이션을 추가하여 사운드의 거리감 구현

#### 시작 화면 추가
- 빈레벨 생성
- 시작 Level의 빈 레벨이 Begin Play 되면 인게임 이미지와 Start 버튼 표출
- Start 버튼 누르면 처음 시작맵으로 이동
---

### 시작 및 엔딩 추가
#### 처음 시작 추가
- Player가 맵에 첫 등장 시 누웠다가 일어나는 애니메이션 적용
#### 첫 시작 맵에 공사장 에셋 적용
#### 최적화를 위해 공사장 맵에 불필요한 Actor 제거

#### 기본 T-Pose 상태인 장식 Enemy(이벤트 없음) 배치 

#### AmbientSound를 배치 및 목소리 적용

#### 화살표 Graffiti를 추가하여 이동 방향 가이드

#### 트리거 박스로 Backroom 이동

#### Backroom 탈출 조건 구현
- ActorSpawner 액터를 둬서 해당 범위 안에 수집품 랜덤 생성
- 해당 수집품을 특정 갯수 구하면 문이 열림 >> 수집품을 Collision하면 위젯에 있는 숫자가 +1 카운트 되고,  해당 수집품은 Destroy
- 문이 열리면 문 앞의 Box Collision 활성화 >> 문 열릴 때 View가 Player에서 문 앞쪽으로 이동하고, 다시 Player View 복귀
- 활성화 된 콜리전에 충돌할 경우 다음 맵 이동

#### Backroom 문 안쪽 Emissive Color 적용

#### 엔딩 맵에서는 맵이 좁아진 만큼 Player 이동속도 절반 감소(게임 템포 조절)

#### 엔딩 설계
- 엔딩 연출 설계 >> 열린 결말
- 집 에셋 적용
- 최종 맵 최적화 >> 불필요한 엑터 제거

#### 엔딩 구현
- Actor Overlap을 통해 집 안의 Light Color를 흰색에서 빨간색으로 변경
- 문 앞 Collision box 충돌 시 노크 소리 구현 
- 수집품 수집 시 문 열림 및 열리는 소리 적용
- 최종 문 앞 Collision Box 충돌 시 3초 뒤 The End? 텍스트 표출 

---
### 문제해결 과정

#### 수집품 모두 수집 시 카메라 View가 문쪽으로 이동할 때 못 도망치는 상황 발생
- OpenDoor 이벤트 발생 시 문 열리는 애니메이션을 화면에 표출하기 위해 카메라 View를 이동
- 해당 이동으로 인해, Player가 자신이 보고 있는 화면을 보지 못하여 Enemy 한테 도망치지 못하는 상황 발생
1. OpenDoor 이벤트가 발생
2. View의 Owner가 Door로 변경
3. Event Dispatcher를 활용하여 모든 Enemy는 Movement 상태를 None으로 변경
4. View의 Owner가 Player로 다시 변경
5. 모든 Enemy의 Movement 상태를 다시 Walk로 변경


#### Don’t Move Enemy의 키 눌림 판정 문제
- 이전 키입력이 밀려서 Don’t move 이벤트 시 키 눌림이 발생
- Don’t move Enemy 충돌 시 0.2초를 delay하여 키 눌림이 밀려서 입력 판정이 되는 것을 방지
※ 테스트 결과 0.2초가 불필요한 delay 시간이 없고, 키 눌림 밀림 현상을
   방지 할 수 있는 최적의 시간이라고 판단.
---
### 프로젝트 회고
#### 잘한점
- 블루 프린트 여러 노드 활용
1. Collision
2. Lerp
3. Was Actor Recently Rendered
4. Create Widget 등등…

- 컨텐츠 설계 경험 습득
1. 공포게임의 필수 조건인 사운드, Jumpscare 구현
2. 에셋 활용 및 배치
3. AI 이동 반경 설계 등등…

#### 개선할 사항
- 블렌더 Rigging 작업 등을 통해 풍부한 애니메이션 추가
- FL Studio 등의 툴로 기존 사운드를 편집을 하여 풍부한 사운드 추가
- 시작 및 엔딩 스토리 추가


