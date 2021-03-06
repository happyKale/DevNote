> 이 글은 엘리님의 '드림코딩 by엘리' 유튜브 채널에 있는 [CI/CD 5분 개념 정리 (현업에서 쓰는 개발 프로세스)](https://www.youtube.com/watch?v=0Emq5FypiMM&t=126s) 영상을 정리한 것입니다.

<br/>

#### 요즘같이 변화가 빠른 시대에 빠르게 시장과 고객의 요구사항을 반영해서 제품을 출시, 업데이트할 것인가는 큰 과제이다. 이를 위해 많은 회사에서 CI/CD를 개발 프로세스로 사용한다.

<br/>

## 🧩👨‍🚀🚀 CI/CD
어플리케이션 개발 단계부터 배포 단계까지 모든 단계들을 자동화를 통해서 좀 더 효율적이고 빠르게 사용자에게 배포할 수 있도록 만드는 것을 말한다.
<br/><br/><br/>

## 🧩 CI ( Continuous Integration 지속적인 통합 )
: 버그 수정이나 새로 만드는 기능들이 메인 Repository에 주기적으로 빌드되고 테스트가 되어서 머지되는 것.
<br/><br/>

### ✨ CI의 2가지 포인트
####  1. 개발자들은 그들의 코드 변경사항을 메인 Repository에 주기적으로 빈번하게 머지해야 한다.
- 같은 파일을 2명의 개발자가 각각 작성하고 있다면 오랜기간 수정을 하고나서 머지를 할 경우 서로 다른 코드를 어떻게 통합해야할지 방법을 찾기가 쉽지 않다.
  새로운 기능을 개발하기 위해 코드를 작성하는 것보다 머지 충돌을 해결하기 위해서 더 많은 시간을 사용해야할 것이다.
- 버그를 수정하거나 새로운 기능을 구현할 때는 어떻게하면 작은 단위로 나누어서 메인 repository에 반영하거나 사용자에게 배포할 수 있을지
  최대한 작은 단위로 나누어서 개발하고 통합해나가는 것이 중요하다.
#### 2. 통합을 위한 단계 ( 빌드, 테스트, 머지 )의 자동화
- 주기적으로 머지된 코드의 변경사항이 자동으로 빌드가 되어서 코드 변경사항 이후에도 빌드가 성공적으로 되었는지 확인할 수 있어야한다.
- 새로 추가된 코드의 변경사항 뿐만 아니라 기존의 시스템에 다른 버그를 초래하지는 않았는지 자동으로 테스트까지 되어야 한다.
- 순서
  1. 개발자들이 하루에도 몇 번씩 주기적으로 코드의 변경사항을 메인 repository에 머지한다. ( 머지하기 전에 코드리뷰를 통해서 코드가 적절한지 판단한다. )
  2. 머지가 되었으면 자동으로 팀에서 만든 CI 스크립트를 통해서 추가된 코드와 함께 repository가 빌드가 된다.
  3. 빌드가 잘 되었으면 팀에서 작성한 유닛 테스트, integration 테스트 등등 여러가지 테스트들도 스크립트를 통해서 실행된다.
<br/><br/><br/>
### ✨ CI의 장점
- 주기적인 머지를 통해서 머지 충돌을 줄일 수 있기 때문에 개발 생산성이 향상된다.
- 머지되는 모든 코드들은 자동으로 빌드되고 테스트 되기 떄문에 코드의 문제점을 빠르게 확인할 수 있다.
- 버그 수정이 용이하다. 주기적으로 머지를 하기 위해서 코드의 변경사항이 작기 때문에 문제를 수정할 때에도 작은 단위의 문제를 확인할 수 있기 때문이다.
#### 이런 것들을 통해서 코드의 퀄리티가 향상된다.
CI를 잘 운영하기 위해서는 모든 개발자들이 자신이 작성한 코드에 대해서 유닛 테스트를 꼭 포함해야하기 때문이다. 
CI를 사용한다면 우리 프로젝트의 대부분의 소스코드들이 자동으로 테스트가 될 수 있도록 만들기 때문에 좀 더 안정성있는 제품을 개발할 수 있다.

<br/><br/><br/>


## 👨‍🚀 CD ( Continuous Delivery 지속적인 제공 )
## 🚀 CD ( Continuous Deployment 지속적인 배포 )
: 마지막 배포 단계에서 어떻게하면 자동화해서 배포를 만들 수 있을지 고민하는 단계이다.<br/>
지속적인 제공/ 지속적인 배포 서로 연관이 있고 섞어서 사용하는 경우가 있기 때문에 비슷하다고 보면 된다.
<br/><br/>

### ✨ 진행 순서
1. CI( 지속적인 통합 )을 통해서 주기적으로 머지된 코드의 변경사항들이 자동으로 빌드가 되고 테스트가 되었다면
2. Prepare Release 배포할 준비 과정을 거친다. 준비된 release가 정상인지 확인하는 과정을 거친다.
3. - 사용자에게 배포해도 되겠다는 결정을 내리면 <strong> 수동적으로 배포하는 단계를 👨‍🚀 Continuous Delivery </strong>라고 한다.
   - release가 준비 되자마자 사용자에게 배포할 수 있도록 <strong> 모든 과정을 자동화 해놓은 것을 🚀 Continuous Deployment </strong>라고 한다.

<br/>

##### 회사마다 어느 정도의 자동화를 하는지 다르기 때문에 차이가 있다. CI/CD는 완벽히 분리된 것이 아니라 대부분의 회사에서 CI와 CD를 거쳐서 배포를 하기 때문에 CI/CD 라고 묶어서 부르곤 한다.
<br/><br/><br/>

## 🌈 전체적인 CI/CD 과정
1. 작은 단위로 기능을 나누어서 주기적으로 메인 저장소에 머지를 한다.
2. 자동으로 빌드를 한다.
3. 자동으로 테스트 과정을 거친다.
4. release 준비를 한다.
5. 수동 or 자동으로 최종 배포를 한다.

<br/><br/><br/>


## 🧰 CI/CD를 위한 툴들
- Jenkins
- Buildkite
- Github Actions
- Bitbucket pipelines
- Gitlab CI/CD

<br/><br/><br/>


