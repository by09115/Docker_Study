# Docker

시작하기에 앞서 이 문서는 책 **가장 빨리 만나는 Docker**의 주요 내용을 정리한 것이고, 개인적인 학습 목적으로 작성됨을 미리 밝힙니다.

-----

 Docker는 2013년 3월 Docker, Inc(구 DotCloud)에서 출시한 오픈 소스 컨테이너 프로젝트입니다. 

- Docker의 인기가 가면 갈수록 높아지는 이유

   2010년 이후로 클라우드 서버의 도입이 활발해졌고, 이로써 서버 구입 및 유지보수에 대한 부담이 크게 줄게 되었습니다. 클라우드 환경에서는 가상 서버 생성은 쉬웠지만 많은 가상 서버들에 각각 소프트웨어를 설치하고 관리하는 데에는 많은 노력이 요구되었고, 많은 대책들이 생기기 시작했습니다.

- 해결책
   셸 스크립트로 설치와 설정 자동화를 구현하더라도 중앙 관리가 힘들고, 기능이 부족한데 이는 프로그램 안정성에 직접적인 영향을 끼칩니다. 하지만 **Immutable Infastructure**라는 개념이 등장합니다.

- **Immutable Infastructure**
  호스트 OS와 서비스 운영 환경을 분리하고, 한 번 설정한 운영 환경은 변경하지 않는다(Immutable)는 개념입니다.  서비스 운영 환경을 이미지로 만들어 서버에 배포, 실행하며, 서비스가 업데이트되면 이미지를 새로 생성하여 배포합니다.(서비스 운영 환경 이미지를 한 번 쓰고 버림)

- Immutable Infastructure의 장점

  - 편리한 관리: 이미지를 중앙에서 관리 → 체계적인 배포와 관리 가능
  - 확장: 이미지만 있으면 쉽게 서버 확장 가능
  - 테스트: 어떤 환경이든 이미지만 실행하면 서버와 같은 환경에서 테스트 가능
  - 가벼움: 운영체제 · 서비스 운영 환경 분리로 Lightweight(가볍고), Portable(들고다니기 쉬운) 환경 제공

## 1-1 가상 머신과 Docker

 Docker는 다음처럼 Docker와 여러모로 비슷하다고 할 수 있습니다. 가상 머신에 각종 서버 프로그램 및 DB를 설치하고 개발한 애플리케이션을 실행하고, 이 가상 머신의 이미지를 추출한 뒤 여러 서버에 복사 · 실행하여 여러 서버를 만들 수 있습니다. (Ex: Amazon Web Services, Microsoft Azure, Google Cloud Platform 등)

### > 가상 머신

 하지만 가상머신은 느리다는 단점이 있었고, 이런 단점을 해결하기 위해 **반가상화(Paravirtualization)** 방식이 개발되어 널리 쓰이고 있습니다.

![출처: Intel](https://raw.githubusercontent.com/by09115/Docker_Study/master/Images/paravirtualization.jpg)

전가상화(Full Virtualization) 방식에서의 가상화 이미지는 OS가 포함되어 있어 부피가 매우 크고, 이를 주고받기 위해서 적지 않은 소요시간이 발생합니다.

### > Docker

 반가상화보다 경량화된 Docker는 게스트 OS를 설치하는 대신 Docker 이미지에 각종 라이브러리와 서버 운영에 필요한 프로그램을 설치할 수 있고 OS의 기본 자원은 공유합니다. 이를 통해서 이미지를 경량화할 수 있고, 보관 및 전송을 쉽고 빠르게 할 수 있다는 장점이 있습니다.

### > Docker 설치

 Docker를 설치하는 데에는 그렇게 어렵지 않으므로 생략하고, Docker를 어떻게 사용하는지에 대해 초점을 맞추어 진행하겠습니다.

## Docker 사용

 Docker의 명령어는 주로 `docker <command>` 형식으로 사용할 수 있습니다. (현재 자신이 사용하고 있는 운영체제에 따라 `sudo`와 같이 관리자 권한을 부여해야 합니다.**일부 운영체제 제외**)
저는 주로 백엔드 작업을 할 때 DB를 컨테이너 위에 작동시키거나 여러 서버를 한 컴퓨터에서 구동할 때 등 컨테이너 별 독립성을 갖출 수 있어 자주 사용합니다.

#### 3.1 search 명령

 Docker에서는 **Docker Hub**를 통해 웹에서 여러 이미지를 불러올 수 있습니다. 이미지를 검색하는 방법은 다음과 같습니다.

```
docker search <search>
```

검색된 결과들 중에서는 사용자가 만든 이미지도 있고, 공식직으로 발표된 이미지도 있으니 잘 구별해서 쓰도록 합시다.

#### 3.2 pull 명령

 앞에서 보았던 이미지 목록에서 자신이 원하는 이미지의 이름과 태그를 다음과 같은 명령을 통해서 다운받을 수 있습니다.

```
docker pull <image-name> <tags>
```

 tags에 latest를 입력하면 최신 버전을 내려받을 수 있습니다.

#### 3.3 images 명령

 images 명령을 통해 받은 이미지의 목록을 확인할 수 있습니다.

#### 이 밖에도,,,

 attach, start 등 여러 명령어가 있습니다(추후 추가 예정)
