# AWS 클라우드 소개

## 클라우드란 무엇인가?

기존의 온프레미스 환경에 대해서 먼저 살펴볼 필요가 있다. 기존 시스템에서는 회사에서 비지니스에 필요한 모든 물리적인 하드웨어를 구축해야 했다.
클라우드는 여러 리소스를 인터넷을 통해 IT리소스, 스토리지, 데이터베이스, 서버 등을 임대하는 서비스이다.
클라우트 컴퓨팅을 사용하면 인프라를 하드웨어가 아닌 소프트웨어로 간주하고 사용할 수 있다.
이렇게 함으로 클릭 몇번만으로 스토리지 용량, 서버 등을 동적으로 축소 혹은 넓힐 수 있다.

## AWS 클라우드 컴퓨팅의 여섯가지 이점

1. 자본 비용을 가변 비용으로 대체: 필요한 리소스를 필요한 만큼 사용가능하고, 확장 가능하다.
2. 규모의 경제로 얻게 되는 이점:
3. 용량 추정 불필요: fast fail
4. 속도 및 대응력 향상: 기존 복작하게 구축해야 했던 것을 서비스로 사용할 수 있다.
5. 데이터 센터 운영 및 유지 관리에 비용 투자 불필요: IT인프라, 건물, 관리 인력
6. 몇 분 만에 전 세계에 배포

## AWS 핵심 인프라 및 서비스

- 보안
  방화벽, ACL. 관리자 => 보안그룹, 네트워크ACL, AWS IAM
- 네트워킹
  라우터, 네트워크 파이프라인, 스위치 => Elastic Load Balancing, Amazon VPC
- 서버
  온프레미스 서버 => AMI -> Amazon EC2 인스턴스
- 스토리지 및 데이터베이스
  DAS, SAN, NAS, RDBMS => Amazon EBS, Amazon EFS, Amazon S3, Amazon RDS

## 클라우드 작동 방식

- AWS는 네트워크로 연결된 하드웨어를 소유하고 유지 관리한다.

## 클라우드 배포 모델

- 온프레미스: 또는 프라이빗이라 불린다. 회사 소유의 데이터 센터에 모든 물리적인 인프라를 위치시킨다. 일반적으로 가상화 방식을 사용하여, 클라우드 환경을 모방하는 것이 요즘의 트렌드이다.
- 하이브리드: 기존의 온프레미스와 클라우드 방식을 함께 사용하는 모델이다. 기존의 것과 클라우드를 같이 운영하기 위함이다.
- 클라우드: 클라우드 올인이라고도 불린다. 클라우드 상에서 모든 애플리케이션을 배포한다. 확장성, 뛰어난 보안, 관리의 용이성 등의 이점을 누릴 수 있다.

## AWS 글로벌 인프라

- AWS 리전: AWS가 서비스하는 지리적인 위치이다. 현재 총 25개의 리전이 있다.
- 가용 영역: 데이터 센터의 클러스터를 의미한다. Availability Zone, AZ 라고도 한다. 하나의 리전은 최소 2개 이상의 가용 영역으로 구분되어 있다. 가용 영역의 위치는 보안상의 이유를 공개되어 있지 않다. 한 가용 영역은 다른 가용 영역의 장애로 부터 격리되어 있기 때문에 여려 AZ에 분리해서 배포하면 더욱더 안전하다.

## 리전 선택의 기준

1. 데이터 거버넌스를 고려해야 한다. 예) 중국에서 서비스 하기 위해선 반드시 중국에 지정되어야 한다.
2. 지연: 엔드유저에 더 가까운 리전을 선택하면 더 빠르다.
3. 비용: 6000개가 넘는 서비스를 AWS가 제공하고 있는데, 모든 리전에서 제공하는 것은 아니고, 리전마다 가격이 다르다.

## 엣지 로케이션란

최종사용자에게 더 짧은 지연시간으로 서비스를 제공하는 AWS의 추가적인 시설물이다. 전 세계에 인구가 밀집한 지역에 200여개가 넘는 곳에 엣지 로케이션 POP를 제공하고 있다. 이 엣지 로케이션에서는 DNS 서비스인 Amazon Route 53과 CDN 서비스인 Amazon CloudFront등을 이용할 수 있다.

## AWS 엣지 인프라

- AWS Outposts
- AWS Local Zones
- AWS Wavelength: 매우 짧은 지연, 5G 기능

## AWS와 상호 작용하는 3가지 방법

- AWS Management Console: 사용하기 쉬운 그래픽 인터페이스
- AWS 명령줄 인터페이스 (AWS CLI): 개별 명령을 사용하여 서비스에 엑세스
- 소프트웨어 개발 키트 (SDK): 코드에서 서비스에 액세스

이 작업을 자동화할 수 있다.

# AWS 클라우드 핵심 서비스 소개1

## 컴퓨팅

### Amazon Elastic Compute Cloud (Amazon EC2)

- 크기 조정 가능한 컴퓨팅 용량: 원하는 유형 및 사이즈로 변경 가능하다.
- 컴퓨팅 리소스 완전 제어: 기존 온프레미스에서 했던 실행 환경을 모두 제공한다.
- 새로운 서버 인스턴스 확보 및 부팅 시간 단축: 실제 사용한 만큼만 비용을 지불하면 된다.

가상머신과 물리적 서버를 비교하게 되면, AWS에서는 서버, DB, 스토리지등을 탄력적으로 조절할 수 있지만, 물리 서버에서는 용량을 추가하고 하는 것이 쉽지 않아 오버프로비저닝 하게 된다. AWS EC2가 가상머신이다.
AWS 클라우드에서 EC2 인스턴스는 일회용 리소스로 취급된다. EC2 인스턴스를 프로비저닝하고 EC2 인스턴스에 데이터를 저장하지 않는다. 모든 정보는 외부에 저장해 EC2 인스턴스를 일종의 Stateless하게 관리할 수도 있다. 이렇게 관리하게 되면, EC2 인스턴스는 기능한 하게되므로 인프라를 탄력적으로 확장 및 축소 가능하다. 또한 EC2 인스턴스의 부하를 CloudWatch 라는 모니터링 서비스로 모니터링하고 데이터를 기반으로 인스턴스를 확장, 스케일 업 또는 다운, 스케일 아웃 또는 인을 할 수 있도록 결정할 수 있다.
AWS 환경에서는 신기술 도입이나 아키텍처 변경 등 다양한 환경을 테스트해 볼 수 있다.

EC2 인스턴스는 Amazon Machine Image(AMI)를 기준으로 인스턴스화 된다. 운영체제, 앱서버, 앱과 같이 필요한 소프트웨어 및 AMI 시작 권한, 시작될 때 인스턴스에 연결할 볼륨을 지정하는 블록디바이스 매핑 등이 구성된 템플릿이다.

AMI에서 원하는 만큼의 인스턴스를 추가 또는 종료 할 수 있다. 그리고 정지시 비용이 지불되지 않는다.
AMI를 다운하는 방법은 4가지가 있다:

1. AWS에서 제공하는 AMI,
2. 마켓플레이스에서 제공하는 AMI가 있다: 스마트폰의 앱스토어와 같이 AMI에 솔루션과 같은 소프트웨어를 통합해 이를 판매할 수 있다.
3. 사용자가 자체적으로 구성한 AMI를 생성해 이를 사용할 수 있다.
4. 커뮤니티에서 올라오는 AMI를 사용할 수 있다.

### Amazon EC2의 이점

- 필요한 인프라 용량을 정하지 않아도 된다. 탄력성이 있다. => 클라우드 컴퓨팅의 장점
- 제어가 매우 쉽다. 중단, 시작, 재시작, 인스턴스 유형 제어 등등.
- 다양한 AWS 서비스와 쉽게 통합할 수 있다.
- 99.99%의 가용성.
- Amazon VPC 안에서 여러 단계의 보안을 누릴 수 있다.
- 합리적인 비용. 컴퓨팅 자원을 효율적으로 사용할 수 있다.
- 오토스케일링
- 사용하기 쉬은 접근성. 추상화된 방법을 제공함으로 쉽게 사용가능하다.

### Amazon EC2 인스턴스 패밀리 타입 및 이름

- 범용 인스턴스 패밀리: 트래픽이 적은 웹 사이트와 웹 앱. 소형 및 중형 데이터베이스
- 컴퓨팅 최적화 인스턴스 패밀리: 고성능 웹 서버, 동영상 인코딩
- 메모리 최적화: 고성능 데이터베이스, 분산 메모리 캐시
- 스토리지 최적화: 데이터 웨어하우징, 로그 또는 데이터 처리 앱
- 액셀러레이티드 컴퓨팅 : 3D시각화, 기계학습

### Amazon EC2 요금

초당 결제 (Amazon Linux 및 Ubuntu 전용)
시간당 결제 (다른 모든 OS)

- 온디맨드 인스턴스
- 예약 인스턴스
- Savings Plans: 예약 인스턴스와 비슷하지만, 유동성이 좋다.
- 스팟 인스턴스: 온디멘드보타 90% 저렴한 가격. 예측이 쉽다.
