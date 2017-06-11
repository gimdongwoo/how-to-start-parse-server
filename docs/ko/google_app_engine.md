# GCP App Engine에서 Parse-server 실행

> [참고] 원본 문서: [GCP](https://cloud.google.com/nodejs/resources/frameworks/parse-server#download_app).

Google Cloud Platform에서 Parse-server 앱을 실행하여, 쉽게 개발을 시작 할 수 있습니다. 또한 생성하는 앱이 Google의 모든 제품에 필요한 동일한 인프라에서 실행되기 때문에 수백 또는 수천 개의 사용자가 있는지 여부에 관계없이 모든 사용자에게 서비스를 제공하도록 확장 할 수 있습니다.
이 튜토리얼은 간단한 Parse-server 애플리케이션을 빠르게 배포 할 수 있게 한다. 이 튜토리얼에서는 여러분이 Node.js 프로그래밍에 익숙하고 Node.js 개발을 위해 이미 환경을 준비했다고 가정합니다.


## 시작하기 전에

완료 할 때마다 각 단계를 확인하십시오.

### Google Cloud Platform 콘솔에서 프로젝트를 만듭니다.
프로젝트를 아직 만들지 않았다면 지금 만듭니다. 프로젝트를 사용하면 배포, 액세스 제어, 청구 및 서비스를 포함하여 앱의 모든 Google Cloud Platform 리소스를 관리 할 수 있습니다.

1. [Cloud Platform 콘솔](https://console.cloud.google.com/)을 엽니다.
2. 상단의 드롭 다운 메뉴에서 프로젝트 만들기를 선택하십시오.
3. 고급 옵션 표시를 클릭하십시오. App Engine 위치에서 미국 위치를 선택하십시오.
4. 프로젝트 이름을 지정하십시오.
5. 프로젝트 ID와 프로젝트 이름을 기록해 둡니다. 프로젝트 ID는 명령 및 구성에 사용됩니다.

### 귀하의 프로젝트에 대한 청구를 활성화하십시오.
프로젝트에 대해 [결제 사용](https://console.cloud.google.com/project/_/settings?_ga=1.22855806.496551942.1491453407)을 아직 설정하지 않은 경우 지금 결제방법을 설정하십시오. 청구 기능을 설정해야 인스턴스 실행 및 데이터 저장과 같은 청구 가능한 리소스를 어플리케이션에서 사용 할 수 있습니다.

### Google Cloud SDK를 설치하십시오.
Google Cloud SDK를 아직 설치하지 않았다면 [Google Cloud SDK 설치 및 초기화](https://cloud.google.com/sdk/docs/)를 참조하십시오. SDK에는 Google Cloud Platform에서 리소스를 만들고 관리 할 수있는 도구와 라이브러리가 포함되어 있습니다.


## 앱 다운로드 및 실행

Node.js로 작성되고 Parse-server를 사용하는 간단한 Hello World 앱을 사용하면 Cloud Platform에 앱을 빠르게 배포 할 수 있습니다. 준비 항목을 완료 한 후에는 Parse-server 샘플 응용 프로그램을 다운로드하여 배포 할 수 있습니다. 다음 섹션에서는 Parse-server 응용 프로그램을 실행하는 과정을 안내합니다.
배포 된 앱은 [여기](http://parse-dot-nodejs-docs-samples.appspot.com/)에서 볼 수 있습니다.

### Parse-server 응용 프로그램 복제

Parse-server 샘플 앱의 코드는 GitHub의 [GoogleCloudPlatform/nodejs-docs-samples](https://github.com/GoogleCloudPlatform/nodejs-docs-samples/tree/master/appengine/parse-server) 저장소에 있습니다. 아직 로컬 컴퓨터에 리포지토리를 복사하지 않은 경우 :

```
git clone https://github.com/GoogleCloudPlatform/nodejs-docs-samples.git
```

샘플 코드가 들어있는 디렉토리로 이동하십시오.

```
cd nodejs-docs-samples
```

Parse-server 샘플 앱은 appengine 폴더에 있습니다.

```
cd appengine/parse-server
```

또는 [샘플](https://github.com/GoogleCloudPlatform/nodejs-docs-samples/archive/master.zip)을 다운로드 하여 압축을 풀어 사용할 수도 있습니다.

### MongoDB 데이터베이스 만들기

새로운 MongoDB 데이터베이스를 생성하기위한 옵션은 여러 가지가 있습니다. 예 :

- [MongoDB 사전 설치](https://cloud.google.com/launcher/?q=mongodb)를 사용하여 Google Compute Engine 가상 시스템을 만듭니다.
- [mLab](https://mlab.com/google/)을 사용하여 Google Cloud Platform Central 1 (us-central1) 지역에서 무료 MongoDB 배포를 만드십시오. 현재 다른 지역을 선택할 수 없습니다.
- [MongoDB Atlas](https://www.mongodb.com/cloud)를 사용하여 Amazon Web Service N. Virginia (us-east-1) 지역에 무료 MongoDB 배치를 작성하십시오. 현재 다른 지역을 선택할 수 없습니다.

### 환경 변수 설정

앱을 로컬에서 실행하려면 config.json 파일에서 몇 가지 환경 변수를 설정해야합니다.

- DATABASE_URI - 데이터베이스의 MongoDB URI.
- APP_ID - 파스 서버가 실행될 앱의 ID입니다.
- MASTER_KEY - ACL 보안을 겹쳐 쓰는 데 사용할 마스터 키.
- SERVER_URL - 앱의 URL (예 : http://localhost:8080/parse)

### 로컬 컴퓨터에서 앱 실행

1. 의존성 설치 :

```
npm install
```

2. 시작 스크립트를 실행하십시오.

```
npm start
```

3. 웹 브라우저에 다음 주소를 입력하십시오.

```
http://localhost:8080
```

페이지에 표시된 샘플 앱에서 Hello World 메시지를 볼 수 있습니다. 이 페이지는 당신의 컴퓨터에서 실행중인 Parse-server 웹 서버에서 제공합니다.

다음 단계로 넘어가려면 Ctrl + C를 눌러 로컬 웹 서버를 중지하십시오.


## Google Cloud Platform에서 Parse-server 실행하기

다음 다이어그램에서는 Cloud Platform에 앱을 배포하는 프로세스를 보여줍니다.

![](https://cloud.google.com/languages/images/hello-world-app-structure.png)

App Engine의 유연한 환경은 애플리케이션의 부하를 처리하도록 자동으로 확장 할 수 있는 컨테이너에서 애플리케이션을 실행합니다. 이 아키텍처는 Compute Engine과 Docker를 사용하여 구성되어 있습니다. 자세한 내용은 [App Engine flexible environment](https://cloud.google.com/appengine/docs/flexible/)를 참조하십시오.

### Google Cloud Platform에서의 앱 배포

샘플을 입력하십시오 다음 명령을 입력하십시오.

```
gcloud app deploy
```

앱 업데이트가 완료되었음을 알리는 메시지가 표시 될 때까지 기다리십시오.

### 클라우드에서 실행되는 앱보기

웹 브라우저에 다음 주소를 입력하십시오.

```
https://<your-project-id>.appspot.com
```

이번에는 Hello World 메시지를 표시하는 페이지가 App Engine의 유연한 환경에서 실행되는 웹 서버에 의해 전달됩니다.

앱을 업데이트하는 경우 처음으로 앱을 배포 할 때 사용한 것과 동일한 명령을 입력하여 업데이트 된 버전을 배포 할 수 있습니다. 새로운 배포에서는 앱의 [새 버전](https://console.cloud.google.com/project/_/appengine/versions)을 만들고 기본 버전으로 승격합니다. 이전 버전의 앱은 VM 인스턴스에 종속되어 유지됩니다. 이러한 앱 버전과 VM 인스턴스는 모두 비용 청구 가능한 리소스라는 점에 유의하십시오. VM 인스턴스 삭제 또는 중지에 대한 자세한 내용은 [인스턴스 정리](https://cloud.google.com/nodejs/getting-started/delete-tutorial-resources)를 참조하십시오.

편의를 위해 npm 스크립트를 사용하여 gcloud 명령을 실행할 수 있습니다. ``package.json`` 파일에 다음 행을 추가하십시오 :

```json
"scripts": {
  "start": "node server.js",
  "deploy": "gcloud app deploy  --project <your-project-id>"
}
```

이제이 명령을 실행하여 응용 프로그램을 배포 할 수 있습니다.

```
npm run deploy
```

## 설정

App Engine의 유연한 환경에서 실행되는 모든 앱은 app.yaml 파일을 사용하여 배포 구성을 설정해야합니다.

```
// appengine/parse-server/app.yaml
runtime: nodejs
env: flex
```

[GITHUB에서 보기](https://github.com/GoogleCloudPlatform/nodejs-docs-samples/blob/master/appengine/parse-server/app.yaml)

이 최소한의 app.yaml 파일은 nodejs와 유연한 환경을 가진 런타임으로 설정되어 있습니다. app.yaml에서 지정할 수있는 수 많은 구성 값이 있고, 리소스, 크기 조정 및 기타 설정 등을 사용자 정의 할 수 있습니다. 유연한 환경의 구성 설정에 대한 자세한 내용은 [App Engine flexible environment](https://cloud.google.com/appengine/docs/flexible/)를 참조하십시오.