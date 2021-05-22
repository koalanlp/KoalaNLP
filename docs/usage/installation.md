--------

[목차로 이동](./index.md)

--------

# 설치

- [Java, Kotlin, Scala의 경우](#java-kotlin-scala)
- [NodeJS의 경우](#nodejs)
- [Python3의 경우](#python-3)

## Java, Kotlin, Scala
### Java 패키지 목록

다음과 같은 하위 패키지가 있습니다.

| 패키지명            | 설명                                                                 |  버전    | License (원본)     |
| ------------------ | ------------------------------------------------------------------ | ------- | ------------ |
| `koalanlp-core`    | 통합 인터페이스의 정의가 등재된 중심 묶음입니다.                            | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-core.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-core) | MIT |
| `koalanlp-scala`   | Scala를 위한 편의기능 (Implicit conversion 등)                         | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-scala_2.13.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-scala) | MIT |
| `koalanlp-server`  | HTTP 서비스 구성을 위한 패키지입니다.                                    | (2.x 개발중) | MIT |
| `koalanlp-kmr`     | 코모란 Wrapper / 분석범위: 형태소                                       | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-kmr.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-kmr)         | Apache 2.0 |
| `koalanlp-eunjeon` | 은전한닢 Wrapper / 분석범위: 형태소                                     | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-eunjeon.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-eunjeon) | Apache 2.0 |
| `koalanlp-arirang` | 아리랑 Wrapper / 분석범위: 형태소 <sup>2-1</sup>                        | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-arirang.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-arirang) | Apache 2.0 |
| `koalanlp-rhino`   | RHINO Wrapper / 분석범위: 형태소 <sup>2-1</sup>                        | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-rhino.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-rhino)     | GPL v3 |
| `koalanlp-daon`    | Daon Wrapper / 분석범위: 형태소 <sup>2-1</sup>                         | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-daon.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-daon)       | MIT(별도 지정 없음) |
| `koalanlp-khaiii`  | Kakao Khaiii Wrapper / 분석범위: 형태소 <sup>2-3</sup>                 | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-khaiii.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-khaiii)       | Apache 2.0 |
| `koalanlp-utagger` | 울산대 UTagger Wrapper / 분석범위: 형태소 <sup>2-4</sup>                 | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-utagger.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-utagger)       | 교육/연구용 무료, 상업용 별도협약 |
| `koalanlp-okt`     | Open Korean Text Wrapper / 분석범위: 문장분리, 형태소                    | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-okt.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-okt)        | Apache 2.0  |
| `koalanlp-kkma`    | 꼬꼬마 Wrapper / 분석범위: 형태소, 의존구문 <sup>2-1</sup>                | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-kkma.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-kkma)       | GPL v2    |
| `koalanlp-hnn`     | 한나눔 Wrapper / 분석범위: 문장분리, 형태소, 구문분석, 의존구문 <sup>2-1</sup>| [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-hnn.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-hnn)        | GPL v3    |
| `koalanlp-etri`    | ETRI Open API Wrapper / 분석범위: 형태소, 구문분석, 의존구문, 개체명, 의미역 | [![Version](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-etri.svg?style=flat-square&label=r)](http://search.maven.org/search?q=koalanlp-etri)      | MIT<sup>2-2</sup> |

> <sup>주2-1</sup> 꼬꼬마, 한나눔, 아리랑, RHINO 분석기는 타 분석기와 달리 Maven repository에 등재되어 있지 않아, 원래는 수동으로 직접 추가하셔야 합니다.
> 이 점이 불편하다는 것을 알기에, KoalaNLP는 assembly 형태로 해당 패키지를 포함하여 배포하고 있습니다. 포함된 패키지를 사용하려면, `assembly` classifier를 사용하십시오.
> "assembly" classifier가 지정되지 않으면, 각 분석기 라이브러리가 빠진 채로 dependency가 참조됩니다.
>
> <sup>주2-2</sup> ETRI의 경우 Open API를 접근하기 위한 코드 부분은 KoalaNLP의 License 정책에 귀속되지만, Open API 접근 이후의 사용권에 관한 조항은 ETRI에서 별도로 정한 바를 따릅니다.
> 따라서, ETRI의 사용권 조항에 동의하시고 키를 발급하셔야 하며, 다음 위치에서 발급을 신청할 수 있습니다: [키 발급 신청](http://aiopen.etri.re.kr/key_main.php)
>
> <sup>주2-3</sup> Khaiii 분석기의 경우는 Java가 아닌 C++로 구현되어 사용 전 분석기의 설치가 필요합니다. Python3.6 및 CMake 3.10+만 설치되어 있다면 설치 자체가 복잡한 편은 아니니 [여기](https://github.com/kakao/khaiii/wiki/빌드-및-설치)를 참조하여 설치해보세요. 참고로, KoalaNLP가 Travis CI에서 패키지를 자동 테스트하기 위해 구현된 bash script는 [여기](https://github.com/koalanlp/koalanlp/blob/master/khaiii/install.sh)에 있습니다.
>
> <sup>주2-4</sup> UTagger 분석기의 경우에도 C/C++로 구현되어, 사용 전 분석기의 설치가 필요합니다. 윈도우와 리눅스(우분투, CentOS)용 라이브러리 파일만 제공되며, 설치 방법은 [여기](https://koalanlp.github.io/usage/Install-UTagger.md)를 참조하십시오.

## Gradle
```groovy
ext.koala_version = '2.1.4'

repositories {
    mavenCentral()
    jcenter()
    maven { url "https://jitpack.io" } // 코모란의 경우에만 추가.
}

dependencies{
    // 코모란의 경우
    implementation "kr.bydelta:koalanlp-kmr:${ext.koala_version}" 
    // 은전한닢 프로젝트(Mecab-ko)의 경우
    implementation "kr.bydelta:koalanlp-eunjeon:${ext.koala_version}"
    // 아리랑의 경우
    implementation "kr.bydelta:koalanlp-arirang:${ext.koala_version}:assembly"
    // RHINO의 경우 
    implementation "kr.bydelta:koalanlp-rhino:${ext.koala_version}:assembly"
    // Daon의 경우
    implementation "kr.bydelta:koalanlp-daon:${ext.koala_version}:assembly"
    // OpenKoreanText의 경우
    implementation "kr.bydelta:koalanlp-okt:${ext.koala_version}" 
    // 꼬꼬마의 경우
    implementation "kr.bydelta:koalanlp-kkma:${ext.koala_version}:assembly"
    // 한나눔의 경우
    implementation "kr.bydelta:koalanlp-hnn:${ext.koala_version}:assembly" 
    // ETRI Open API의 경우
    implementation "kr.bydelta:koalanlp-etri:${ext.koala_version}"
    // Khaiii의 경우 (Khaiii C++ 별도 설치 필요)
    implementation "kr.bydelta:koalanlp-khaiii:${ext.koala_version}"
    // REST Server Service의 경우 (준비중)
    implementation "kr.bydelta:koalanlp-server:${ext.koala_version}"
}
```

## SBT
(버전은 Latest Release 기준입니다. SNAPSHOT을 사용하시려면, `latest.integration`을 사용하세요.)
```sbtshell
val koalaScalaVer = "2.1.0"
val koalaVer = "2.1.4"

// Implicit method 사용시 Scala support 추가
libraryDependencies += "kr.bydelta" %% "koalanlp-scala" % koalaScalaVer

// 코모란 분석기의 경우
resolvers += "jitpack" at "https://jitpack.io/"
libraryDependencies += "kr.bydelta" % "koalanlp-kmr" % koalaVer

// 은전한닢 분석기의 경우
libraryDependencies += "kr.bydelta" % "koalanlp-eunjeon" % koalaVer

// 아리랑 분석기의 경우
libraryDependencies += "kr.bydelta" % "koalanlp-arirang" % koalaVer classifier "assembly"

// RHINO 분석기의 경우
libraryDependencies += "kr.bydelta" % "koalanlp-rhino" % koalaVer classifier "assembly"

// Daon 분석기의 경우
libraryDependencies += "kr.bydelta" % "koalanlp-daon" % koalaVer classifier "assembly"

// Open Korean Text 분석기의 경우
libraryDependencies += "kr.bydelta" % "koalanlp-okt" % koalaVer

// 꼬꼬마 분석기의 경우
libraryDependencies += "kr.bydelta" % "koalanlp-kkma" % koalaVer classifier "assembly"

// 한나눔 분석기의 경우
libraryDependencies += "kr.bydelta" % "koalanlp-hannanum" % koalaVer classifier "assembly"

// ETRI 분석기의 경우
resolvers += Resolver.JCenterRepository
libraryDependencies += "kr.bydelta" % "koalanlp-etri" % koalaVer

// Khaiii 분석기의 경우 (Khaiii C++ 별도 설치 필요)
resolvers += Resolver.JCenterRepository
libraryDependencies += "kr.bydelta" % "koalanlp-khaiii" % koalaVer

// UTagger 분석기의 경우 (UTagger C++ 별도 설치 필요)
resolvers += Resolver.JCenterRepository
libraryDependencies += "kr.bydelta" % "koalanlp-utagger" % koalaVer
```

## Maven
Maven을 사용하시는 경우, 다음과 같습니다. `${TAGGER_PACK}`위치에는 원하는 품사분석기의 패키지를 써주시고, `${TAGGER_VER}`위치에는 품사분석기의 버전을 써주세요.
```xml
<dependency>
  <groupId>kr.bydelta</groupId>
  <artifactId>koalanlp-${TAGGER.PACK}</artifactId>
  <version>${TAGGER_VER}</version>
</dependency>
```

Classifier를 추가하실 경우, `<artifactId>`다음 행에 다음 코드를 추가하세요.
```xml
  <classifier>assembly</classifier>
```

예를 들어서, 꼬꼬마 분석기(koalanlp-kkma) 버전 2.1.3을 추가하고자 한다면, 아래와 같습니다.
```xml
<dependency>
  <groupId>kr.bydelta</groupId>
  <artifactId>koalanlp-kkma</artifactId>
  <classifier>assembly</classifier>
  <version>2.1.3</version>
</dependency>
```

## NodeJS
우선 Java 8 및 NodeJS 8 이상을 설치하고, `JAVA_HOME`을 환경변수에 등록해주십시오.
그런 다음, 아래와 같이 설치하십시오. (현재 nodejs-koalanlp 버전은 [![NPM Version](https://img.shields.io/npm/v/koalanlp.svg?style=flat-square)](https://github.com/koalanlp/nodejs-koalanlp)입니다.)

```bash
$ npm install koalanlp --save 
```

### 지원 API 유형
각 형태소 분석기는 별도의 패키지로 나뉘어 있습니다. 패키지 이름은 `koalanlp.API`에 상수로 정의되어 있습니다.

| 패키지명            | 설명                                                                 |  사용 가능 버전    | License (원본)     |
| ------------------ | ------------------------------------------------------------------ | ---------------- | ----------------- |
| API.KMR          | 코모란 Wrapper, 분석범위: 형태소                                       | [![Ver-KMR](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-kmr.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-kmr%22)         | Apache 2.0 |
| API.EUNJEON      | 은전한닢 Wrapper, 분석범위: 형태소                                     | [![Ver-EJN](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-eunjeon.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-eunjeon%22) | Apache 2.0 |
| API.ARIRANG      | 아리랑 Wrapper, 분석범위: 형태소                                       | [![Ver-ARR](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-arirang.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-arirang%22) | Apache 2.0 |
| API.RHINO        | RHINO Wrapper, 분석범위: 형태소                                       | [![Ver-RHI](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-rhino.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-rhino%22)     | GPL v3 |
| API.DAON         | Daon Wrapper, 분석범위: 형태소                                        | [![Ver-DAN](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-daon.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-daon%22)       | MIT(별도 지정 없음) |
| API.KHAIII       | Khaiii Wrapper, 분석범위: 형태소 <sup>주2-3</sup>                      | [![Ver-KHA](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-khaiii.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-khaiii%22)       | Apache 2.0 |
| API.OKT          | Open Korean Text Wrapper, 분석범위: 문장분리, 형태소                    | [![Ver-OKT](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-okt.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-okt%22)        | Apache 2.0  |
| API.KKMA         | 꼬꼬마 Wrapper, 분석범위: 형태소, 의존구문                               | [![Ver-KKM](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-kkma.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-kkma%22)       | GPL v2    |
| API.HNN          | 한나눔 Wrapper, 분석범위: 문장분리, 형태소, 구문분석, 의존구문               | [![Ver-HNN](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-hnn.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-hnn%22)        | GPL v3    |
| API.ETRI         | ETRI Open API Wrapper, 분석범위: 형태소, 구문분석, 의존구문, 개체명, 의미역 | [![Ver-ETR](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-etri.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-etri%22)      | MIT<sup>2-2</sup> |

> <sup>주2-2</sup> ETRI의 경우 Open API를 접근하기 위한 코드 부분은 KoalaNLP의 License 정책에 귀속되지만, Open API 접근 이후의 사용권에 관한 조항은 ETRI에서 별도로 정한 바를 따릅니다.
> 따라서, ETRI의 사용권 조항에 동의하시고 키를 발급하셔야 하며, 다음 위치에서 발급을 신청할 수 있습니다: [키 발급 신청](http://aiopen.etri.re.kr/key_main.php)
>
> <sup>주2-3</sup> Khaiii 분석기의 경우는 Java가 아닌 C++로 구현되어 사용 전 분석기의 설치가 필요합니다. Python3.6 및 CMake 3.10+만 설치되어 있다면 설치 자체가 복잡한 편은 아니니 [여기](https://github.com/kakao/khaiii/blob/v0.1/doc/setup.md)를 참조하여 설치해보세요. (단, v0.1에서는 빌드시 'python3' 호출시 'python3.6'이 연결되어야 합니다.) 참고로, KoalaNLP가 Travis CI에서 패키지를 자동 테스트하기 위해 구현된 bash script는 [여기](https://github.com/koalanlp/koalanlp/blob/master/khaiii/install.sh)에 있습니다.

### 초기화
초기화 과정에서 KoalaNLP는 필요한 Java Library를 자동으로 다운로드하여 설치합니다. 설치에는 시간이 다소 소요됩니다.
때문에, 프로그램 실행시 최초 1회에 한하여 초기화 작업이 필요합니다.

* 아래 코드는 ES8과 호환되는 CommonJS (NodeJS > 8) 기준으로 작성되어 있습니다.
* 초기화 코드는 Asynchronous call만 지원합니다. 아래는 Async/Await 방식으로 작성되어 있습니다.

```javascript
const {initialize} = require('koalanlp/Util');

async function someAsyncFunction(){
    // 꼬꼬마와 은전한닢 분석기의 2.0.4 버전을 참조합니다.
    await initialize({
      packages: {KKMA:'2.0.4', EUNJEON:'2.0.4'},
      javaOptions: ["-Xmx4g"],
      verbose: true,
    });
    
    // 초기화 다음 작업...
}

someAsyncFunction().then(
    () => console.log('Finished'),
    (error) => console.error('Error', error)
);

```

* 첫번째 인자는 초기화 option입니다.
  * `packages` 인자는 Python 프로그램에서 사용할 모든 패키지의 버전을 정의합니다. (상단 표 참고)
  * `javaOptions` 인자는 JVM을 실행하기 위한 option string의 array입니다.
  * `verbose`는 초기화 과정을 표시할지를 결정하는 인자입니다. `true`이면 초기화 과정이 표시되며, 기본값은 true입니다.
* 아래 문서는 초기화 과정이 모두 완료되었다고 보고 진행합니다.
* API 참고: [initialize](https://koalanlp.github.io/nodejs-support/module-koalanlp_Util.html#.initialize)

## Python 3
우선 Java 8 이상을 설치하고, `JAVA_HOME`을 환경변수에 등록해주십시오.
그런 다음, 아래와 같이 설치하십시오. (현재 python-koalanlp 버전은 [![PyPI](https://img.shields.io/pypi/v/koalanlp.svg?style=flat-square)](https://github.com/koalanlp/python-support)입니다.)

```bash
$ pip install koalanlp
```

### Packages
각 형태소 분석기는 별도의 패키지로 나뉘어 있습니다.

| 패키지명            | 설명                                                                 |  사용 가능 버전    | License (원본)     |
| ------------------ | ------------------------------------------------------------------ | ---------------- | ----------------- |
| API.KMR          | 코모란 Wrapper, 분석범위: 형태소                                       | [![Ver-KMR](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-kmr.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-kmr%22)         | Apache 2.0 |
| API.EUNJEON      | 은전한닢 Wrapper, 분석범위: 형태소                                     | [![Ver-EJN](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-eunjeon.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-eunjeon%22) | Apache 2.0 |
| API.ARIRANG      | 아리랑 Wrapper, 분석범위: 형태소                                       | [![Ver-ARR](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-arirang.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-arirang%22) | Apache 2.0 |
| API.RHINO        | RHINO Wrapper, 분석범위: 형태소                                       | [![Ver-RHI](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-rhino.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-rhino%22)     | GPL v3 |
| API.DAON         | Daon Wrapper, 분석범위: 형태소                                        | [![Ver-DAN](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-daon.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-daon%22)       | MIT(별도 지정 없음) |
| API.KHAIII       | Khaiii Wrapper, 분석범위: 형태소 <sup>주2-3</sup>                                      | [![Ver-KHA](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-khaiii.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-khaiii%22)       | Apache 2.0 |
| API.UTAGGER      | 울산대 UTagger Wrapper / 분석범위: 형태소 <sup>2-4</sup>                                | [![Ver-UTA](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-utagger.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-utagger%22)       | 교육/연구용 무료, 상업용 별도협약 |
| API.OKT          | Open Korean Text Wrapper, 분석범위: 문장분리, 형태소                    | [![Ver-OKT](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-okt.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-okt%22)        | Apache 2.0  |
| API.KKMA         | 꼬꼬마 Wrapper, 분석범위: 형태소, 의존구문                               | [![Ver-KKM](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-kkma.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-kkma%22)       | GPL v2    |
| API.HNN          | 한나눔 Wrapper, 분석범위: 문장분리, 형태소, 구문분석, 의존구문               | [![Ver-HNN](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-hnn.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-hnn%22)        | GPL v3    |
| API.ETRI         | ETRI Open API Wrapper, 분석범위: 형태소, 구문분석, 의존구문, 개체명, 의미역 | [![Ver-ETR](https://img.shields.io/maven-central/v/kr.bydelta/koalanlp-etri.svg?style=flat-square&label=r)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22koalanlp-etri%22)      | MIT<sup>2-2</sup> |
| API.KSS          | KSS Wrapper, 분석범위: 문장분리                                          | 버전무관                                                                                                                                                                              | BSD 3 |
| API.KIWI         | Kiwi Wrapper, 분석범위: 형태소                                          | 버전무관                                                                                                                                                                              | LGPL v2.1              |

> <sup>주2-2</sup> ETRI의 경우 Open API를 접근하기 위한 코드 부분은 KoalaNLP의 License 정책에 귀속되지만, Open API 접근 이후의 사용권에 관한 조항은 ETRI에서 별도로 정한 바를 따릅니다.
> 따라서, ETRI의 사용권 조항에 동의하시고 키를 발급하셔야 하며, 다음 위치에서 발급을 신청할 수 있습니다: [키 발급 신청](http://aiopen.etri.re.kr/key_main.php)
>
> <sup>주2-3</sup> Khaiii 분석기의 경우는 Java가 아닌 C++로 구현되어 사용 전 분석기의 설치가 필요합니다. Python3.6 및 CMake 3.10+만 설치되어 있다면 설치 자체가 복잡한 편은 아니니 [여기](https://github.com/kakao/khaiii/blob/v0.1/doc/setup.md)를 참조하여 설치해보세요. (단, v0.1에서는 빌드시 'python3' 호출시 'python3.6'이 연결되어야 합니다.) 참고로, KoalaNLP가 Travis CI에서 패키지를 자동 테스트하기 위해 구현된 bash script는 [여기](https://github.com/koalanlp/koalanlp/blob/master/khaiii/install.sh)에 있습니다.
>
> <sup>주2-4</sup> UTagger 분석기의 경우에도 C/C++로 구현되어, 사용 전 분석기의 설치가 필요합니다. 윈도우와 리눅스(우분투, CentOS)용 라이브러리 파일만 제공되며, 설치 방법은 [여기](https://koalanlp.github.io/usage/Install-UTagger.md)를 참조하십시오. UTagger 분석기는 교육 연구용은 무료로 배포되며, 상업용은 별도 협약이 필요합니다.

### 초기화 & 사용종료
초기화 과정에서 KoalaNLP는 필요한 Java Library를 자동으로 다운로드하여 설치합니다. 설치에는 시간이 다소 소요됩니다.
때문에, 프로그램 실행시 최초 1회에 한하여 초기화 작업이 필요합니다.

* 사용이 종료된 이후에는 `finalize()`를 실행하여 KoalaNLP가 사용중인 관련 프로그램을 종료하는 것을 권합니다.

```python
from koalanlp.Util import initialize, finalize

# 꼬꼬마와 ETRI 분석기의 2.0.4 버전을 참조합니다.
initialize(java_options="-Xmx4g", KKMA="2.0.4", ETRI="2.0.4")

# 사용이 끝나면 아래와 같이 사용을 종료합니다.
finalize()
```

* `java_options` 인자는 JVM을 실행하기 위한 option string입니다.
* 이후 인자들은 keyword argument들로, 상단 표를 참고하여 지정하실 수 있습니다. (항상 최신 버전을 사용하려면 `="LATEST"`를 사용하면 됩니다.)
* 나머지 문서는 초기화 과정이 모두 완료되었다고 보고 진행합니다.
* API 참고: [initialize](https://koalanlp.github.io/python-support/html/koalanlp.html#koalanlp.Util.initialize)

--------

[목차로 이동](./index.md)

--------