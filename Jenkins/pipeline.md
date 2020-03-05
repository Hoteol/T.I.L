# 구축하고자 하는 환경
Git 연동이나, Gradle, Maven 빌드 등 기본적인 조건을 제외하고 가장 원했던 조건
- 공통내용을 모듈화하여 공용으로 사용할 수 있는 구조
- 각 단계에 대한 수동 실행이 가능한 구조

--- 

# 구축
## jenkins File
젠킨스는 Pipeline Script를 Admin Web에서 직접 작성하여 저장하는 방법과, Git을 통해 JenkinsFile 을 읽는 방법을 제공합니다.

만들고자 하는 스크립트는, 배포 Flow가 지나치게 다르지 않은 프로젝트에 한하여, 모두 동일한 스크립트를 사용할 수 있도록 구성하여 파라미터 기반으로 실행될 수 있는 스크립트 입니다.

그렇기 때문에 저장소에 대한 수정만으로 모든 프로젝트에 적용할 수 있는 Git을 통해 JenkinsFile 을 읽는 방법을 사용합니다.

groovy 사용이 미숙하여, 코드가 더러운 점은 양해 부탁드립니다. groovy 사용성을 숙지하여 추후 리펙토링할 예정입니다.

---

## Stage
젠킨스 Pipeline Script는 실행에 대한 단위인 node 와 파이프라인을 구성하는 stage가 있습니다. node 와 stage 간에는 먼저 선언되야 하는 것은 없이 작성할 수 있습니다.

``` java
node('', {
  stage('example1', {
    echo ""
  })
})

stage('example2', {
  node('', {
    echo ""
  })
})
```
Pipeline Script는 병렬 실행을 지원하기 때문에 실행 단위를 분리해야할 경우 node를 사용하여 실행 단위를 분리할 수 있고, Pipeline의 단계를 stage로 구성하게 됩니다.

> Flow Check - Parameter Check - Git CheckOut - Test - Build - Deploy - Switch

## Flow
---
각 잡 실행 Pipeline에서 진행할 Stage 를 정의하는 파라미터들입니다.

- USE_TEST : Test 단계 사용 유무
- USE_BUILD : Build 단계 사용 유무
- USE_DEPLOY : Deploy 단계 사용 유무
- USE_SWITCH : Switch 단계 사용 유무

## Module
---
각 프로젝트 Pipeline Job에서 넘겨주어야 할 모듈 정보입니다.

- GRADLE_VERSION : Gradle Version
- JAVA_VERSION : Java Version
- NODE_VERSION : Node Version (Optional)
- SLACK_TOKEN : Slack Token (Optional)

## Git
---
소스 Check Out 을 위한 정보입니다.

- GIT_URL : Git Repository Url
- BRANCH_SELECTOR : 대상 Branch

## Deploy
---
그리고 각 배포 환경에 따라 정의되어야 하는 파라미터들이 있습니다. 아래 파라미터는 제가 배포해야할 환경에 필요한 파라미터로 각 배포 환경에 맞게 구성하시면 됩니다.

- CONFIG_NAME, REMOTE_PATH, TARGET_USER, TARGET_SERVER

