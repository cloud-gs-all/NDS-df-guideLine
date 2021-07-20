# NDS-df-guideLine

QuickLab 진행 후에 On-premise 환경에서 GCP와 연동한 ETL 작업

## 다운로드 Pycharm or VsCode

`Pycharm`은 통합 개발 환경(IDE)으로 python 개발을 목적으로 설치하게 됩니다.

`vscode`를 사용해도 괜찮습니다.

[Pycharm Download](https://www.jetbrains.com/pycharm/download/) 에서 설치할 수 있습니다.

## Git Clone

```javascript
$ git clone https://github.com/cloud-gs-all/NDS-df-guideLine.git
```

git clone을 수행하고 프로젝트를 `vscode` 나 `Pycharm` 에서 `import`를 진행합니다.

clone 시 프로젝트 `Directory` 구조는 아래와 같습니다.

`public` : README에 포함될 `.gif` 파일 모음

`schema` : dataflow 실행 시 `bigQuery` 데이터를 인입하기 위해 참고하는 스키마 정보

`LICENSE` : apache-beam open source에 대한 라이센스

`nds-df-v0.1.py` : dataflow 소스 코드, python으로 작성되어 있습니다.

`README.md` : 현재 보고 있는 파일

`requirements.txt` : `nds-df-v0.1.py`를 동작시키기 위한 python의 패키지 목록

```
|-- project
|  `-- public
|  `-- schema
|     `-- mv_sa_tran_online.json
|  `-- LICENSE
|  `-- nds-df-v0.1.py
|  `-- README.md
|  `-- requirements.txt
|--
```

## Google Cloud SDK

사전에 `Google Cloud SDK` 가 설치 되어있어야 합니다.

`gcloud init` 으로 `google cloud platform` 과 연결합니다.

```
$ gcloud init
```

[관련 Docs](https://cloud.google.com/sdk/docs/install?hl=ko)

## IAM 설정

IAM role에 이용하고 계신 email에 Role이 `Computer Admin` 권한 이상이라면 `dataflow` 동작 시키는데 어려움이 없습니다.

정석적인 방법으로는 `Service Account` 를 만들고 `Dataflow Worker` 권한을 준 뒤에 `JSON` 파일로 다운 받고 환경설정을 셋팅 하시면 됩니다.

MAC 의 경우에 아래와 같이 작성합니다

```
$ vi ~./zshrc 혹은 vi ~/.bashrc
```

```
export GOOGLE_APPLICATION_CREDENTIALS=[Service Account File Path]
```

[관련 Docs](https://cloud.google.com/docs/authentication/getting-started)

## nds-df-v0.1.py 실행

python 실행하는데 필요한 패키지를 설치합니다.

```
$ pip install -r requirements.txt
```

`nds-df-v0.1.py` 소스코드를 살펴보면 `add_argument` 로 등록된 `project`, `bucket`, `dataSet` 을 python 파일을 실행시켜 줄 때 `parameter` 로 넘겨주어야 합니다.

```
$ python3 nds-df-v0.1.py -p [project-name] -b [bucket-name] -d [bigQuery-dataSet]
```

실행이 완료되면 `Google Cloud Platform`으로 이동해서 `dataflow` 에서 동작하고 있는지 확인합니다.

## dataflow 소스코드 작성

`dataflow`를 실행시키기 위해서는 `apache-beam`을 기반으로 하고 있기 때문에 `apache-beam` 공식 문서를 보며 개발을 진행하셔야 합니다.

세 가지 언어 `python`, `java`, `Go` 를 지원합니다.

소스 코드가 간결하고 이해하기 쉬운 `python`으로 작성하는것을 추천 드립니다.

[Apache Beam Docs](https://beam.apache.org/documentation/runners/dataflow/)

[Apache Beam Programming Guide](https://beam.apache.org/documentation/programming-guide/)

[Apache Beam SDK Docs for Python](https://beam.apache.org/releases/pydoc/2.13.0/index.html)
