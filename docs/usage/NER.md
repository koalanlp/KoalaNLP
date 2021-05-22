--------

[목차로 이동](./index.md)

--------

## 목차 

- [개관](#개체명-인식하기)
- [Kotlin](#kotlin)
- [Scala](#scala)
- [Java](#java)
- [NodeJS](#javascript)
- [Python 3](#python-3)

## 개체명 인식하기

문장 또는 문단을 분석해서 각 문장 속에서 사람이나 장소 등을 나타내는 개체명을 묶어낼 수 있습니다. ETRI 분석기만 의존구조 분석을 지원합니다.

결과물은 Sentence 객체에 포함된 Entity의 List가 됩니다.
- [Java, Scala, Kotlin의 Sentence](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.data/-sentence/index.html),
  [Entity](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.data/-entity/index.html)
- [NodeJS의 Sentence](https://koalanlp.github.io/nodejs-support/module-koalanlp_data.Sentence.html),
  [Entity](https://koalanlp.github.io/nodejs-support/module-koalanlp_data.Entity.html)
- [Python의 Sentence](https://koalanlp.github.io/python-support/html/koalanlp.html#koalanlp.data.Sentence),
  [Entity](https://koalanlp.github.io/python-support/html/koalanlp.html#koalanlp.data.Entity)

아래 분석 예시는 **'텍스트 문단'** 을 기준으로 분석한 결과들입니다. 
이미 타 분석기에서 분석된 `Sentence` 객체나, `Sentence`의 List인 경우에도 같은 방식으로 호출이 가능합니다. 

## 참고
**개체명 인식**은 문장에서 인물, 장소, 기관, 대상 등을 인식하는 기술입니다.

예) '철저한 진상 조사를 촉구하는 국제사회의 목소리가 커지고 있는 가운데, 트럼프 미국 대통령은 되레 사우디를 감싸고 나섰습니다.'에서, 다음을 인식하는 기술입니다.
* '트럼프': 인물
* '미국' : 국가
* '대통령' : 직위
* '사우디' : 국가

### Kotlin
Reference: [CanRecognizeEntity](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.proc/-can-recognize-entity/index.html),
ETRI [EntityRecognizer](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.etri/-entity-recognizer/index.html)

```kotlin
import kr.bydelta.koala.etri.EntityRecognizer

val API_KEY = /** ETRI에서 발급받은 키 **/
val recognizer = EntityRecognizer(API_KEY)

val parsed = recognizer.analyze("이 문단을 분석합니다. 문단 구분은 자동으로 합니다.") 
// 또는 recognizer(...), recognizer.invoke(...)

// 첫번째 문장의 개체명들을 출력합니다.
parsed[0].getEntities().forEach{ entity ->
    println(entity)
}
```

#### Scala
Reference: [CanRecognizeEntity](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.proc/-can-recognize-entity/index.html),
           ETRI [EntityRecognizer](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.etri/-entity-recognizer/index.html)

* [koalanlp-scala](https://koalanlp.github.io/scala-support)가 dependency로 포함되었다고 가정합니다.

```scala
import kr.bydelta.koala.etri.EntityRecognizer
import kr.bydelta.koala.Implicits._

val API_KEY = /** ETRI에서 발급받은 키 **/
val recognizer = new EntityRecognizer(API_KEY)

val parsed = recognizer.analyze("이 문단을 분석합니다. 문단 구분은 자동으로 합니다.") 
// 또는 recognizer(...), recognizer.invoke(...)

// 첫번째 문장의 개체명들을 출력합니다.
parsed[0].getEntities().forEach{ entity =>
    println(entity)
}
```

#### Java
Reference: [CanRecognizeEntity](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.proc/-can-recognize-entity/index.html),
           ETRI [EntityRecognizer](https://koalanlp.github.io/koalanlp/api/koalanlp/kr.bydelta.koala.etri/-entity-recognizer/index.html)

```java
import kr.bydelta.koala.etri.EntityRecognizer;
import kr.bydelta.koala.data.Sentence;
import kr.bydelta.koala.data.Entity;

String API_KEY = /** ETRI에서 발급받은 키 **/
EntityRecognizer recognizer = new EntityRecognizer(API_KEY);

List<Sentence> parsed = recognizer.analyze("이 문단을 분석합니다. 문단 구분은 자동으로 합니다.") 
// 또는 recognizer.invoke(...)

// 첫번째 문장의 개체명들을 출력합니다.
for(Entity entity : parsed[0].getEntities()) {
    println(entity);
}
```

#### JavaScript
Reference: [EntityRecognizer](https://koalanlp.github.io/nodejs-support/module-koalanlp_proc.EntityRecognizer.html)

* 아래 코드는 ES8과 호환되는 CommonJS (NodeJS > 8) 기준으로 작성되어 있습니다.

##### Async/Await

```javascript
const {EntityRecognizer} = require('koalanlp/proc');
const {ETRI} = require('koalanlp/API');

const API_KEY =; ??/** ETRI에서 발급받은 키 **/

async function someAsyncFunction(){
    // ....
    
    let recognizer = new EntityRecognizer(ETRI, {etriKey: API_KEY});
    let result = await recognizer("이 문단을 분석합니다. 문단 구분은 자동으로 합니다.");
    // 또는 recognizer.analyze(...)

    /* Result는 Sentence[] 타입입니다. */
    // 첫번째 문장의 개체명들을 출력합니다.
    for(const entity of parsed[0].getEntities()){
        console.log(entity.toString());
    }
        
    // ...
}

someAsyncFunction().then(
    () => console.log('After function finished'),
    (error) => console.error('Error occurred!', error)
);
```

##### Promise

```javascript
const {EntityRecognizer} = require('koalanlp/proc');
const {ETRI} = require('koalanlp/API');

const API_KEY =; ??/** ETRI에서 발급받은 키 **/

let recognizer = new EntityRecognizer(ETRI, {etriKey: API_KEY});
recognizer("이 문단을 분석합니다. 문단 구분은 자동으로 합니다.")  // 또는 recognizer.analyze(...)
    .then((result) => {
        /* Result는 Sentence[] 타입입니다. */
        // 첫번째 문장의 개체명들을 출력합니다.
        for(const entity of parsed[0].getEntities()){
            console.log(entity.toString());
        }
    }, (error) => console.error('Error occurred!', error));
```

##### Synchronous Call

```javascript
const {EntityRecognizer} = require('koalanlp/proc');
const {ETRI} = require('koalanlp/API');

const API_KEY =; ??/** ETRI에서 발급받은 키 **/

// ....

let recognizer = new EntityRecognizer(ETRI, {etriKey: API_KEY});
let result = recognizer.analyzeSync("이 문단을 분석합니다. 문단 구분은 자동으로 합니다.");

/* Result는 Sentence[] 타입입니다. */
// 첫번째 문장의 개체명들을 출력합니다.
for(const entity of parsed[0].getEntities()){
    console.log(entity.toString());
}
    
// ...
```

#### Python 3
Reference: [EntityRecognizer](https://koalanlp.github.io/python-support/html/koalanlp.html#koalanlp.proc.EntityRecognizer)

```python
from koalanlp import API
from koalanlp.proc import EntityRecognizer

recognizer = EntityRecognizer(API.ETRI, etri_key=API_KEY)

parsed = recognizer("이 문단을 분석합니다. 문단 구분은 자동으로 합니다.")
# 또는 recognizer.analyze(...), recognizer.invoke(...)

# 첫번째 문장의 개체명들을 출력합니다.
for entity in parsed[0].getEntities():
    print(entity)
```

--------

[목차로 이동](./index.md)

--------
