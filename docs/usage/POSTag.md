--------

[목차로 이동](./index.md)

--------

## 목차 

- [개관](#품사-분석하기)
- [Kotlin](#kotlin)
- [Scala](#scala)
- [Java](#java)
- [NodeJS](#javascript)
- [Python 3](#python-3)

## 품사 분석하기

문장 또는 문단을 분석해서 품사를 부착할 수 있습니다. 모든 분석기 API가 품사 분석을 지원합니다.

결과물은 Sentence 객체가 됩니다.
- [Java, Scala, Kotlin의 Sentence](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.data/-sentence/index.html)
- [NodeJS의 Sentence](https://koalanlp.github.io/nodejs-support/module-koalanlp_data.Sentence.html)
- [Python의 Sentence](https://koalanlp.github.io/python-support/html/koalanlp.html#koalanlp.data.Sentence)

아래 분석 예시는 **'문단'** 을 기준으로 분석한 결과들입니다. 문장 1개를 분석하고 싶은 경우 `tag` 대신에 `tagSentence`를 사용하면 됩니다. 

### 참고
**형태소**는 의미를 가지는 요소로서는 더 이상 분석할 수 없는 가장 작은 말의 단위로 정의됩니다.

**형태소 분석**은 문장을 형태소의 단위로 나누는 작업을 의미합니다.

예) '문장을 형태소로 나눠봅시다'의 경우, 아래와 같이 대략적으로 형태소를 나눌 수 있습니다.
* 문장/일반명사, -을/조사,
* 형태소/일반명사, -로/조사,
* 나누-(다)/동사, -어-/어미, 보-(다)/동사, -ㅂ시다/어미

### Kotlin
Reference: [CanTag](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.proc/-can-tag/index.html) 및 
이를 상속한 class들.

```kotlin
import kr.bydelta.koala.eunjeon.Tagger
// 또는 eunjeon 대신 다른 분석기 가능: arirang, daon, etri, eunjeon, hnn, kkma, kmr, okt, rhino 

val tagger = Tagger()
// (1) 코모란 분석기는 경량 분석기를 사용하는 옵션이 있습니다. 예: Tagger(useLightTagger = true)
// (2) ETRI 분석기의 경우 API 키를 필수적으로 전달해야 합니다. 예: Tagger(API_KEY)
// (3) Khaiii 분석기의 경우 Khaiii 리소스 폴더를 필수적으로 전달해야 합니다. 예: Tagger(resourcePath)
// (4) UTagger 분석기의 경우 사용 전 아래와 같이 UTagger 초기화 절차가 필요합니다.
// import kr.bydelta.koala.utagger.UTagger
// UTagger.setPath(libraryPath, configPath)  // (라이브러리 파일 위치와 설정파일 위치 지정)

val taggedParagraph = tagger.tag("문단을 분석합니다. 자동으로 분리되어 목록을 만듭니다.")
// 또는 tagger(...), tagger.invoke(...)

// 분석 결과는 Sentence 클래스의 List입니다.
println(taggedParagraph[0].singleLineString()) // "문단을 분석합니다."의 품사분석 결과 출력
```

#### Scala
Reference: [CanTag](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.proc/-can-tag/index.html) 및 
이를 상속한 클래스들.

* [koalanlp-scala](https://koalanlp.github.io/scala-support)가 dependency로 포함되었다고 가정합니다.

```scala
import kr.bydelta.koala.eunjeon.Tagger
import kr.bydelta.koala.Implicits._
// 또는 eunjeon 대신 다른 분석기 가능: arirang, daon, etri, eunjeon, hnn, kkma, kmr, okt, rhino 

val tagger = new Tagger()
// (1) 코모란 분석기는 경량 분석기를 사용하는 옵션이 있습니다. 예: new Tagger(useLightTagger = true)
// (2) ETRI 분석기의 경우 API 키를 필수적으로 전달해야 합니다. 예: new Tagger(API_KEY)
// (3) Khaiii 분석기의 경우 Khaiii 리소스 폴더를 필수적으로 전달해야 합니다. 예: new Tagger(resourcePath)
// (4) UTagger 분석기의 경우 사용 전 아래와 같이 UTagger 초기화 절차가 필요합니다.
// import kr.bydelta.koala.utagger.UTagger
// UTagger.setPath(libraryPath, configPath)  // (라이브러리 파일 위치와 설정파일 위치 지정)

val taggedParagraph = tagger("문단을 분석합니다. 자동으로 분리되어 목록을 만듭니다.")
// 또는 tagger(...), tagger.invoke(...)

// 분석 결과는 Sentence 클래스의 List입니다.
println(taggedParagraph(0).singleLineString()) // "문단을 분석합니다."의 품사분석 결과 출력

```

#### Java
Reference: [CanTag](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.proc/-can-tag/index.html) 및 
이를 상속한 class들.

```java
import kr.bydelta.koala.eunjeon.Tagger;
import kr.bydelta.koala.data.Sentence;
// 또는 eunjeon 대신 다른 분석기 가능: arirang, daon, etri, eunjeon, hnn, kkma, kmr, okt, rhino 

Tagger tagger = new Tagger();
// (1) 코모란 분석기는 경량 분석기를 사용하는 옵션이 있습니다. 예: new Tagger(useLightTagger = true);
// (2) ETRI 분석기의 경우 API 키를 필수적으로 전달해야 합니다. 예: new Tagger(API_KEY);
// (3) Khaiii 분석기의 경우 Khaiii 리소스 폴더를 필수적으로 전달해야 합니다. 예: new Tagger(resourcePath);
// (4) UTagger 분석기의 경우 사용 전 아래와 같이 UTagger 초기화 절차가 필요합니다.
// import kr.bydelta.koala.utagger.UTagger;
// UTagger.setPath(libraryPath, configPath);  // (라이브러리 파일 위치와 설정파일 위치 지정)

// 문단을 분석해서 문장들로 얻기 (각 API가 문단 분리를 지원하지 않아도, KoalaNLP가 자동으로 구분합니다)
List<Sentence> taggedParagraph = tagger.tag("문단을 분석합니다. 자동으로 분리되어 목록을 만듭니다.");
// 또는 tagger.invoke(...)

// 분석 결과는 Sentence 클래스의 List입니다.
println(taggedParagraph.get(0).singleLineString()) // "문단을 분석합니다."의 품사분석 결과 출력
```

#### JavaScript
Reference: [Tagger](https://koalanlp.github.io/nodejs-support/module-koalanlp_proc.Tagger.html)

* 아래 코드는 ES8과 호환되는 CommonJS (NodeJS > 8) 기준으로 작성되어 있습니다.

##### Async/Await

```javascript
const {Tagger} = require('koalanlp/proc');
const {EUNJEON} = require('koalanlp/API');

async function someAsyncFunction(){
    // ....
    
    let tagger = new Tagger(EUNJEON);
    // (1) 코모란 분석기는 경량 분석기를 사용하는 옵션이 있습니다. 예: new Tagger(KMR, {kmrLight:true});
    // (2) ETRI 분석기의 경우 API 키를 필수적으로 전달해야 합니다. 예: new Tagger(ETRI, {etriKey: API_KEY});
    // (3) Khaiii 분석기의 경우 Khaiii 리소스 폴더를 필수적으로 전달해야 합니다. 예: new Tagger(KHAIII, {khaResource: resourcePath});
    // (4) UTagger 분석기의 경우 사용 전 아래와 같이 UTagger 초기화 절차가 필요합니다.
    // const {utagger} = require('koalanlp/proc');
    // UTagger.setPath(libraryPath, configPath);  // (라이브러리 파일 위치와 설정파일 위치 지정)

    let result = await tagger("문단을 분석합니다. 자동으로 분리되어 목록을 만듭니다.");
    // 또는 tagger.tag(...) 

    /* Result는 string[] 타입입니다. */
    console.log(result[0].singleLineString()); // "문단을 분석합니다."의 품사분석 결과 출력
        
    // ...
}

someAsyncFunction().then(
    () => console.log('After function finished'),
    (error) => console.error('Error occurred!', error)
);
```

##### Promise

```javascript
const {Tagger} = require('koalanlp/proc');
const {EUNJEON} = require('koalanlp/API');

let tagger = new Tagger(EUNJEON);
// (1) 코모란 분석기는 경량 분석기를 사용하는 옵션이 있습니다. 예: new Tagger(KMR, {kmrLight:true});
// (2) ETRI 분석기의 경우 API 키를 필수적으로 전달해야 합니다. 예: new Tagger(ETRI, {etriKey: API_KEY});
// (3) Khaiii 분석기의 경우 Khaiii 리소스 폴더를 필수적으로 전달해야 합니다. 예: new Tagger(KHAIII, {khaResource: resourcePath});
// (4) UTagger 분석기의 경우 사용 전 아래와 같이 UTagger 초기화 절차가 필요합니다.
// const {utagger} = require('koalanlp/proc');
// UTagger.setPath(libraryPath, configPath);  // (라이브러리 파일 위치와 설정파일 위치 지정)

tagger("문단을 분석합니다. 자동으로 분리되어 목록을 만듭니다.")  // 또는 tagger.tag(...)
    .then((result) => {
        /* Result는 string[] 타입입니다. */
        console.log(result[0].singleLineString()); // "문단을 분석합니다."의 품사분석 결과 출력
    }, (error) => console.error('Error occurred!', error));
```

##### Synchronous Call

```javascript
const {Tagger} = require('koalanlp/proc');
const {EUNJEON} = require('koalanlp/API');

// ....

let tagger = new Tagger(EUNJEON);
// (1) 코모란 분석기는 경량 분석기를 사용하는 옵션이 있습니다. 예: new Tagger(KMR, {kmrLight:true});
// (2) ETRI 분석기의 경우 API 키를 필수적으로 전달해야 합니다. 예: new Tagger(ETRI, {etriKey: API_KEY});
// (3) Khaiii 분석기의 경우 Khaiii 리소스 폴더를 필수적으로 전달해야 합니다. 예: new Tagger(KHAIII, {khaResource: resourcePath});
// (4) UTagger 분석기의 경우 사용 전 아래와 같이 UTagger 초기화 절차가 필요합니다.
// const {utagger} = require('koalanlp/proc');
// UTagger.setPath(libraryPath, configPath);  // (라이브러리 파일 위치와 설정파일 위치 지정)

let result = await tagger.tagSync("문단을 분석합니다. 자동으로 분리되어 목록을 만듭니다."); 

/* Result는 string[] 타입입니다. */
console.log(result[0].singleLineString()); // "문단을 분석합니다."의 품사분석 결과 출력
    
// ...
```

#### Python 3
Reference: [Tagger](https://koalanlp.github.io/python-support/html/koalanlp.html#koalanlp.proc.Tagger)

```python
from koalanlp import API
from koalanlp.proc import Tagger

tagger = Tagger(API.EUNJEON)
# (1) 코모란 분석기는 경량 분석기를 사용하는 옵션이 있습니다. 예: Tagger(kmr_light=True)
# (2) ETRI 분석기의 경우 API 키를 필수적으로 전달해야 합니다. 예: Tagger(etri_key=API_KEY)
# (3) Khaiii 분석기의 경우 Khaiii 리소스 폴더를 필수적으로 전달해야 합니다. 예: Tagger(khaiii_resource=some_path)
# (4) UTagger 분석기의 경우 사용 전 아래와 같이 UTagger 초기화 절차가 필요합니다.
# from koalanlp.proc import UTagger
# UTagger.setPath(library_path, config_path)  // (라이브러리 파일 위치와 설정파일 위치 지정)

# 문단을 분석해서 문장들로 얻기 (각 API가 문단 분리를 지원하지 않아도, KoalaNLP가 자동으로 구분합니다)
taggedParagraph = tagger("문단을 분석합니다. 자동으로 분리되어 목록을 만듭니다.")
# 또는 tagger.tag(...), tagger.invoke(...)

print(taggedParagraph[0].singleLineString()) # "문단을 분석합니다."의 품사분석 결과 출력
```

--------

[목차로 이동](./index.md)

--------
