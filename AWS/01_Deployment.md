# Deployment

## 배포 (Deployment)

나의 로컬 컴퓨터가 아닌 다른 컴퓨터에서 내가 개발한 코드를 돌리는 것이 배포이다. 즉, 개발한 코드를 정상적으로 다른 사람들이 접속해 서비스를 받게 하는 것이다. 즉, 어플리케이션을 cloud service에 설치(install)하는 것이다.

### Cloud

인터넷을 통해 제공되는 서버와 해당 서버에서 실행되는 소프트웨어 및 데이터베이스를 가리킨다.

### Cloud computing

클라우드(인터넷)를 통해 가상화된 컴퓨터의 시스템 리소스를 즉시 제공하는 것을 가리킨다.

## 배포 개발 환경 단계(Environments)

배포를 하기에 앞서, 우리의 코드가 지나가야 할 몇 가지 개발 환경이 존재한다. 각 개발 환경은 개발 중인 코드가 다른 컴퓨터에서도(다른 환경에서도) 정상적으로 동작하기 위한 목적을 가지고서 진행이 된다. 프로젝트가 커지면 아래 소개하는 것보다 더 많은 과정을 거치게 될 것이다.
**1. Development**: 서비스를 개발하는 단계
**2. Integration**: 기존의 베이스 코드와 충돌이 없도록 개발 내용을 수정해서 통합한다. 만일 충돌이 일어난다면 다시 개발단계로 넘어가서 반복한다.
**3. Staging:** 배포 환경과 가장 유사한 단계에서, 다시 한번 테스트를 거치고 서비스를 사용자들에게 배포하기 전에 실제 아무런 문제가 없는지 확인한다.
**4. Production:** 실제 서비스가 운영되는 서버에 서비스를 올린다.

### Environment Challenges

우리의 코드가 로컬이 아닌, 다른 환경에서 정상적으로 돌아가려면, 최소한 이 정도는 지켜줘야 한다.

- Node version
- Dependencies (install npm modules using `--save`)
- Port Number (use enviroment variables to configure ports, `app.listen(process.env.PORT || 1234)`)
- Hostname
- URLs and File Paths (use root-relative URLs instead of absolute ones)
- API Keys

### Deployment Plarforms (Cloud Service)

배포를 위한 플랫폼은 다양하다.

- [Heroku](https://www.heroku.com/)
- [Digital Ocean](https://www.digitalocean.com/)
- [**Amazon Web Services (AWS)**](https://aws.amazon.com/ko/)
- [Microsoft Azure](https://azure.microsoft.com/ko-kr/free/search/?&ef_id=EAIaIQobChMI1OKxudCB6wIVg2kqCh1LNgniEAAYASAAEgIIM_D_BwE:G:s&OCID=AID2100068_SEM_EAIaIQobChMI1OKxudCB6wIVg2kqCh1LNgniEAAYASAAEgIIM_D_BwE:G:s&gclid=EAIaIQobChMI1OKxudCB6wIVg2kqCh1LNgniEAAYASAAEgIIM_D_BwE)

# 배포 전략 (Deploy Strategy) with AWS

## 1. SPA 제공 방법

예를 들어 React로 프로젝트를 진행하고서 클라이언트 사이드를 개발한 후에 배포한다고 한다면, 사용자는 모든 개발 파일을 다운받아야 하는 것인가? 그러진 않을 것이다. React에서 개발한 모든 파일은 `build` 해서 `build` 폴더에 모든 개발 코드를 static한 파일로 묶어준다. 즉, 유저가 한 번에 가져갈 수 있게 포장해 주는 것이다.
이렇게 합쳐준 build 파일을 어떻게 유저에게 제공할 수 있을까?

- Node.js와 Express: static file 자체를 서브
- AWS S3: Bulid파일 서브를 위한 cloud 이용

## S3 (Simple Storage Service)

S3를 SPA를 배포하기 위해 활용해 볼 수 있는데, 마치 모바일 앱과 유사한 방식으로 유저가 다운로드할 수 있게 한다. S3에는 버킷이라는 파일을 담을 수 있는 공간이 존재하는데, 이곳에 build 파일을 업로드해놓으면 유저들은 버킷 주소로 접속하여 어플리케이션을 다운로드 받아서 서버와 통신을 하게 된다.

### S3 사용 시 알아두기

- 버킷의 권한을 public으로 변경해야 사용자가 서비스에 접근할 수 있다.
- `npm run build` 혹은 `yarn build`로 정적 파일을 만든다.

### 참고

- [AWS S3](https://aws.amazon.com/ko/s3/)
- [Amazon S3 리소스](https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/dev/s3-arn-format.html)
- [AWS CLI](https://aws.amazon.com/ko/cli/)
- [생활코딩 Simple Storage Service(S3)](https://opentutorials.org/course/608/3006)

## 2. Server application 제공 방법

혼자 서버를 만들어서 개발할 때는 내 마음대로 포트를 설정해서 개발했었다. 이러한 방식은 전혀 배포를 고려하지 않은 방법이고, 또한 다른 사용자를 로컬포트에 접속하게 할 수도 있지만, 외부인이 내 컴퓨터에 그냥 들어오게 하면 안 될 것이다. 그렇기에 개발한 서버를 돌릴 수 있는 컴퓨터를 임대를 해야 할 것이고, 이 역활을 해주는 서비스가 AWS EC2이다.

## EC2 (Elastic Compute Cloud)

EC2는 컴퓨터를 제공해주고, 우리는 아마존 EC2에 예를 들어 Node를 설치해서 그 위에 서버 어플리케이션을 올려서 구동을 할 수 있게 된다. 그리고 사용자는 EC2에 있는 node app에 접속해서 api를 받아 갈 수 있다. EC2는 AWS가 가진 컴퓨터이고, 유저가 원격 접속을 할 수 있다.

### EC2 사용 시 알아두기

- `spem` 키페어를 잘 저장해둬야 나중에 EC2에 접속이 가능하다.
- 터미널의 전역에 `.ssh`로 들어가서 다운받은 `pem` 파일을 `.ssh`로 옮겨준다.
  `~/.ssh$ mv /home/gunwoo/다운로드/test-server-shortly-express.pem ./`
- 이후에 아래를 터미널에서 실행한다. (chmod 400 pemKeyName)
  `chmod 400 test-server-shortly-express.pem`
- 그리고 ssh -i ~/.ssh/<pem 이름> ubuntu@ <EC2 퍼블릭 ip> 로 원격 우분투 서버로 접속한다.
  `ssh -i ~/.ssh/test-server-shortly-express.pem ubuntu@3.34.3.39`
- 접속된 후 nvm, node 등 새롭게 설치해줘야 한다. (새로운 컴퓨터라고 생각하면 된다. git은 기본으로 설치되어 있음) [Easy way to install nvm on Ubuntu 18.04](https://medium.com/@nbanzyme/easy-way-to-install-nvm-on-ubuntu-18-04-2cfb19ee5391)
- **PM2** 패키지를 이용해서 터미널을 꺼도 EC2 서버를 계속 켜둔 상태로 유지 시켜줄 수 있다.
- EC2에서 파일을 수정하고 싶을때는 **VIM**을 사용하거나 **FileZilla**를 사용해볼 수 있다.

### SSH

SSH를 통해 다른 컴퓨터에 원격으로 접속할 수 있다. (Linux & Unix에서)

### 참고

- [AWS EC2](https://aws.amazon.com/ko/ec2/?nc2=h_m1)
- [Tutorial: Creating and managing a Node.js server on AWS, part 1](https://hackernoon.com/tutorial-creating-and-managing-a-node-js-server-on-aws-part-1-d67367ac5171)
- [PM2](https://pm2.keymetrics.io/)
- [FileZilla](https://filezilla-project.org/)

## 3. RDS (Relational Database Servise)

위와 같이 데이터베이스도 내 로컬로 배포할 수 없다. 그렇기에 이곳에서도 클라우드 서비스를 이용해야한다. EC2에서 데이터베이스를 구축할 수도 있지만, AWS RDS라는 서비스가 데이터베이스를 담당할 수 있다. RDS는 데이터베이스에 특화된 컴퓨터다.

### RDS 사용시 알아두기

- RDS에서 사용할 포트를 지정할 때, 기본이 3306이지만 변경해서 지정해주는 것이 좋다.
- 우분투에서 mysql 서버 켤 때: `service mysql start`
- 터미널에서 `mysql -u <RDS master name> --host <RDS endpoint> -P <RDS port> -p`를 실행하고 이후에 RDS 마스터 비밀번호를 입력하면 데이터베이스 접속이 가능하다.
- workbench로도 접속이 가능하다.

### 참고

- [AWS RDS](https://aws.amazon.com/ko/rds/?nc2=h_m1)
- [AWS RDS 사용하기 블로그](https://velog.io/@noyo0123/AWS-RDS-%ED%94%84%EB%A6%AC%ED%8B%B0%EC%96%B4%EB%A1%9C-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0-gek2el89jw)
- [AWS RDS 시작하기 블로그](https://www.holaxprogramming.com/2016/10/22/aws-rds-get-started/)
- [AWS 시작하기 RDS 설치 블로그](https://smujihoon.tistory.com/85)
- [[AWS] RDS Security Groups 변경](https://88240.tistory.com/459)
- [[AWS] RDS MySQL 장단점](http://blog.naver.com/PostView.nhn?blogId=sory1008&logNo=220950167041&categoryNo=0&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView%E3%85%8D%E3%85%8D%E3%85%8D)

# 이슈

- 보안을 위하여 github에 올리지 말아야 할 코드를 `gitignore`로 따로 분류해야 한다.
- 배포할 때와 개발할 때 환경 설정을 달리 가져야 한다. `NODE_ENV` 매우 중요!
- [[AWS] Free-tier로 RDS 사용 중 요금을 지불했어요!](https://velog.io/@arara90/AWS-Free-tier%EB%A1%9C-RDS-%EC%82%AC%EC%9A%A9-%EC%A4%91-%EC%9A%94%EA%B8%88%EC%9D%84-%EC%A7%80%EB%B6%88%ED%96%88%EC%96%B4%EC%9A%94)
- [Elastic IP - youtube video](https://www.youtube.com/embed/mgfpduy5ZAo)
- [React.js 개발자를 위한 SSR 앱 개발 및 배포하기 - youtube video](https://www.youtube.com/watch?v=Lh5CrFJQSz4&t=4s)

### SSL (Secure Socket Layer)

SSL(Secure Socket Layer) 프로토콜은 웹서버와 브라우저 사이의 보안을 위해 만들어졌고, 서버와 클라이언트의 인증을 하는 데 사용된다.

- [SSL](https://www.instantssl.com/compare-tsl-ssl-certificates)
- [AWS Certificate Manager](https://aws.amazon.com/ko/certificate-manager/)
- [SSL Certificates HOWTO](https://wiki.kldp.org/HOWTO/html/SSL-Certificates-HOWTO/x70.html)
- [SSL 이란? 블로그1](https://captcha.tistory.com/51)
- [SSL 이란? 웹사이트 보안을 위한 SSL에 대한 정리 블로그2](https://jins-dev.tistory.com/entry/SSL-%EC%9D%B4%EB%9E%80-SSL-%EC%97%90-%EB%8C%80%ED%95%9C-%EC%A0%95%EB%A6%AC)

### Route53

[Route53](https://aws.amazon.com/ko/route53/)는 도메인 관리를 수월하게 해준다. - DNS : Domain Name Service

### CloudFront

[CloudFront](https://aws.amazon.com/ko/cloudfront/)를 이용하면, S3 bucket에 SSL을 적용하고, 보안 및 퍼포먼스를 강화 할 수 있다. - CDN : Content Delivery Service

### ELB

[AWS Elastic Load Balancer](https://aws.amazon.com/ko/elasticloadbalancing/?nc=sn&loc=0)를 이용하면 EC2에 SSL을 적용할 수 있다.

### CI/CD system

[CI/CD system](https://www.redhat.com/en/topics/devops/what-is-ci-cd): CI란 지속적인 통합을 통해, 품질을 유지하는 활동을 말하고 CD란 지속적인 배포를 가리키는 것으로 배포 자동화라고 볼 수 있다.

- AWS 서비스의 [code build](https://aws.amazon.com/ko/codebuild/?nc2=h_m1)과 [code deploy](https://aws.amazon.com/ko/codedeploy/?nc2=h_m1)
- [Jenkins](https://www.jenkins.io/)
- [CircleCI](https://circleci.com/)
- [CI/CD 란? 블로그](https://itholic.github.io/qa-cicd/)

### Docker

[Docker](https://www.docker.com/)란 리눅스 컨테이너 기반으로 하는 오픈소스 가상화 플랫폼이다. 도커를 이용하면 독립적인 배포환경을 구축할 수 있다.

- [Docker가 뭐고 왜 쓰는 건가요? - 얄팍한 코딩사전](https://www.youtube.com/watch?v=tPjpcsgxgWc)
- [Docker 가 왜 좋은지 - 노마드코더](https://www.youtube.com/watch?v=chnCcGCTyBg)
- [초보를 위한 도커 안내서 - 도커란 무엇인가?](https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html)
- [Docker의 개념 및 핵심 설명](https://khj93.tistory.com/entry/Docker-Docker-%EA%B0%9C%EB%85%90)
- [Docker란 무엇일까요? - RedHat](https://www.redhat.com/ko/topics/containers/what-is-docker)
- [When and Why to Use Docker](https://www.linode.com/docs/applications/containers/when-and-why-to-use-docker/)

# 참고

- [[AWS] 4.EC2(Elastic Compute Cloud)란? 블로그1](https://goddaehee.tistory.com/179)
- [S3/EC2/RDS 구축 과정 블로그](https://velog.io/@naseriansuzie/imcourseTIL25)
- [아마존 웹 서비스를 다루는 기술](http://pyrasis.com/aws.html)
- [컴파일, 빌드, 배포의 개념 및 차이](https://itholic.github.io/qa-compile-build-deploy/)
