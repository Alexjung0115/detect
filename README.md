<h1>디지랩 챌린지 기술로 바꾸는 세상 해커톤 in 제주</h1>

<h2>주제: CCTV기반 주취자 행동 감지 및 음주운전 조기 포착</h2>

총 3가지 형식의 모델로 주취자 식별을 진행한다

모델 1. Detection모델
Class: Car, Open Driver-seat, Car-Door Open, Person
을 통해 사람이 자동차에 접근하였을 때, 운전석으로 향하는지, 혹은 다른 방향으로 항하는지 확인 가능하다.


모델 2. Yolo Track & Pose Estimation
Tracking 모델을 통해 각 사람마다 ID를 부여하고, Tracking에 의해  생성된 Bbox를 기준으로 포즈 측정을 진행한다. 
이 때 포즈 측정을 더 자세하게 진행하기 위해, 각 프레임 중 각 주체의 BBOx를 제외한 부분을  색상을 검정색으로 칠해 더 자세하게 식별하도록 한다.
각 프레임과 각 주체마다 포즈 측정을 진행 한 뒤, 하나의 csv 파일에 저장한다.


모델 3. LSTM
모델2를 통해 수집된 csv 파일을 기반으로 Sequence length를 90으로 지정한 뒤 연속적인 값에 대해 값을 정하기 위해 LSTM을 통해 진행된다.

위 모델 3개를 통해 주취자 식별 및 음주운전 조기 포착을 진행하는데, 우선 LSTM을 통해 주취자를 식별 후 주취자가 움직일때마다 빨간색으로 주취자를 Bbox를 그린다.,  모델 1으로 포착한 자동차와 거리가 가까워지면 자동차의 라벨을 Intoxicated person car로 변경한다. 그 뒤, 총 3개의 Class인 Intoxciated car ,open driver-seat, drunken person이 겹치게 되면 분홍색으로 화면색상을 전환하여 위험성을 부여하고, 탑승 후 자동차의 Center값의 위치가 변한다면 화면 색깔을 빨간색으로 변환하여 경고를 준다.


모델을 작동시키기 위해 위 깃허브를 다운로드 받은 후, main.py를 통해 모델을 실행시키면 됩니다.


욜로 모델 다운로드 받기 위해서 아래의 드라이브를 통해 다운받아야 합니다. 

1. 욜로 10 Xlarge
   
  https://drive.google.com/file/d/1B7k7i9CIquFpnnEZigEpRNejrcJ6hFxc/view?usp=sharing
  
2. 욜로 8 large
   
  https://drive.google.com/file/d/1SmdWKzg9xhvwNPjjC-D9puSyNi35Jjmz/view?usp=sharing
