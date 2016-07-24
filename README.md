KoalaNLP v0.9
==============

[![Join the chat at https://gitter.im/nearbydelta/KoalaNLP](https://badges.gitter.im/nearbydelta/KoalaNLP.svg)](https://gitter.im/nearbydelta/KoalaNLP?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
(구) KoreanAnalyzer

[![Gitter](https://badges.gitter.im/nearbydelta/KoalaNLP.svg)](https://gitter.im/nearbydelta/KoalaNLP?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

# 소개
한국어 형태소 및 구문 분석기의 모음입니다.

이 프로젝트는 __서로 다른 형태의 형태소 분석기를__ 모아,
__동일한 인터페이스__ 아래에서 사용할 수 있도록 하는 것이 목적입니다.
* Hannanum: KAIST의 [한나눔 형태소 분석기](http://kldp.net/projects/hannanum/)와 [NLP_HUB 구문분석기](http://semanticweb.kaist.ac.kr/home/index.php/NLP_HUB)
* KKMA: 서울대의 [꼬꼬마 형태소/구문 분석기](http://kkma.snu.ac.kr/documents/index.jsp)
* Komoran: Shineware의 [코모란 v2.4](http://shineware.tistory.com/entry/KOMORAN-ver-24)
* Twitter: Twitter의 [한국어 분석기](https://github.com/twitter/twitter-korean-text)
* Eunjeon: 은전한닢 프로젝트의 [SEunjeon(S은전)](https://bitbucket.org/eunjeon/seunjeon)

KoalaNLP의 Contributor가 되고 싶으시다면, 언제든지 Issue에 등록해주십시오.
또한, 추가하고자 하는 새로운 프로젝트가 있으시면, Issue에 등록해주십시오.

# SBT/Maven

## Packages
각 형태소 분석기는 별도의 패키지로 Maven Central에 등재되어 있습니다.
* `koalanlp-core` : 통합 인터페이스의 정의가 등재된 중심 묶음입니다.
* `koalanlp-hannanum` : 한나눔 분석기 패키지입니다. <sup>주1</sup>
* `koalanlp-kkma` : 꼬꼬마 분석기 패키지입니다. <sup>주1</sup>
* `koalanlp-komoran` : 코모란 분석기 패키지입니다. <sup>주1</sup>
* `koalanlp-twitter` : 트위터 분석기 패키지입니다.
* `koalanlp-eunjeon` : 은전한닢 분석기 패키지입니다.

> <sup>주1</sup> 꼬꼬마, 한나눔, 코모란 분석기는 타 분석기와 달리 Maven repository에 등재되어 있지 않아, 원래는 수동으로 직접 추가하셔야 합니다.
> 이 점이 불편하다는 것을 알기에, KoalaNLP는 assembly 형태로 해당 패키지를 포함하여 배포하고 있습니다. 포함된 패키지를 사용하려면, `assembly` classifier를 사용하십시오.
> "assembly" classifier가 지정되지 않으면, 각 분석기 라이브러리가 빠진 채로 dependency가 참조됩니다.

## Dependency 추가하기
KoalaNLP는 Scala 2.11.8에서 컴파일 되었으며, Scala 2.11+과 Java 8+을 지원합니다.
~~현재 최신 버전은 __0.9__입니다.~~
> Maven Repository 생성을 대기중이며, 2016년 7월 27일 이전에 승인될 것 같습니다.

SBT를 사용하시는 경우, 다음과 같이 추가하시면 됩니다.
```scala
libraryDependencies += "kr.bydelta" %% "koalanlp-twitter" % "0.9"	//트위터 분석기의 경우
libraryDependencies += "kr.bydelta" %% "koalanlp-eunjeon" % "0.9"	//은전한닢 분석기의 경우

libraryDependencies += "kr.bydelta" %% "koalanlp-kkma" % "0.9" classifier "assembly"	//꼬꼬마 분석기의 경우
libraryDependencies += "kr.bydelta" %% "koalanlp-komoran" % "0.9" classifier "assembly"	//코모란 분석기의 경우
libraryDependencies += "kr.bydelta" %% "koalanlp-hannanum" % "0.9" classifier "assembly"	//한나눔 분석기의 경우
```

Maven을 사용하시는 경우, 다음과 같습니다.
```xml
<dependency>
  <groupId>kr.bydelta</groupId>
  <artifactId>koalanlp-{TAGGER.PACK}_2.11</artifactId>
  <version>0.9</version>
</dependency>
```

Classifier를 추가하실 경우, `<artifactId>`다음 행에 다음 코드를 추가하세요.
```xml
  <classifier>assembly</classifier>
```

# 사용방법
사용방법은 Scala를 기준으로 작성합니다.
Java Wrapper가 추가되는 대로, 자바기준 구현을 올리겠습니다.

아래에 대부분의 사항에 대해 기술하겠지만, 상세한 사항은 ~~[ScalaDoc](http://nearbydelta.github.io/KoalaNLP/api/#kr.bydelta.koala)을 참고하십시오.~~
> Doc이 제대로 작성되어 있지 않아, 아직은 Access가 안됩니다.

## 문장 분리
품사 태깅을 거치지 않은 문장 분리는, 한나눔과 트위터 분석기만 지원됩니다. 타 패키지의 경우 문장 분리 작업이 품사 태깅 이후에 이루어집니다.
> * 긴 문단의 경우, 문장 분리를 한나눔 또는 트위터로 작업한 다음 각 문장별로 태깅하는 것을 권합니다.
> * 한나눔이 트위터보다 문장분리가 정확하지만, 반대로 무겁습니다.

```scala
/* 패키지 명: 한나눔(hnn), 트위터(twt) */
// 예시에서는 트위터 문장 분리기 활용
import kr.bydelta.koala.twt.SentenceSplitter

val sentSplit = new SentenceSplitter
val paragraph = "누군가가 말했다. Python에는 KoNLPy가 있다. Scala는 KoalaNLP가 있었다."
val sentences: Seq[String] = sentSplit.sentences(paragraph)
```

Implicit method 형태의 작업은 추후 지원 예정입니다.

## 단순 품사 분석
모든 패키지가 품사 분석을 지원합니다.

> * 형태소 분석의 결과는 세종 말뭉치의 지침에 따라 통합되었으며, 통합 태그와 각 분석기 태그의 비교표는 [여기](https://docs.google.com/spreadsheets/d/1OGM4JDdLk6URuegFKXg1huuKWynhg_EQnZYgTmG4h0s/edit?usp=sharing)에서 보실 수 있습니다.

```scala
/* 패키지 명: 한나눔(hnn), 코모란(kmr), 꼬꼬마(kkma), 은전한닢(eunjeon), 트위터(twt) */
// 예시에서는 은전한닢 분석기 활용
import kr.bydelta.koala.eunjeon.Tagger

val tagger = new Tagger

/* 단일 문장 분석 */
val sentence = "이것은 코알라 통합 품사분석기에서 은전한닢 분석기를 돌린 결과입니다."
val analyzed: Sentence = tagger.tagSentence(sentence)

/* 문단 분석 */
val paragraph = "누군가가 말했다. Python에는 KoNLPy가 있다. Scala는 KoalaNLP가 있었다."
val sentences: Seq[Sentence] = tagger.tagParagraph(paragraph)
```

> __Note:__ 
> * 은전한닢과 코모란 라이브러리는 문장분리기(Sentence splitter)를 지원하지 않아, Koala가 품사 분석 결과를 토대로 Heuristic을 사용하여 문장을 분리합니다. 때문에, 그 정확성이 떨어질 수 있습니다.
> * 트위터의 경우 품사 태깅을 세부적으로 진행하지 않아, 통합 변경 과정에서 임의로 대응되므로(예: Noun → NNG), 통합 태그가 실제와 다를 수 있으나, 큰 무리는 없습니다.

## 단순 구문 분석
의존 구문 분석은 한나눔과 꼬꼬마가 지원합니다. (타 패키지는 지원하지 않습니다)

> * 구문 분석의 결과는 세종 말뭉치의 지침에 따라 통합되었으며, 통합 태그와 각 분석기 태그의 비교표는 [여기](https://docs.google.com/spreadsheets/d/1OGM4JDdLk6URuegFKXg1huuKWynhg_EQnZYgTmG4h0s/edit?usp=sharing)에서 보실 수 있습니다.

```scala
/* 패키지 명: 한나눔(hnn), 꼬꼬마(kkma) */
// 예시에서는 꼬꼬마 구문 분석기 활용
import kr.bydelta.koala.kkma.Parser

val parser = new Parser
val sentence = "이것은 코알라 통합 품사분석기에서 은전한닢 분석기를 돌린 결과입니다."
val analyzed: Sentence = parser.parse(sentence)
```

## 사용자 정의 사전
모든 품사 분석기는 사용자 정의 사전을 등록할 수 있습니다. 단, 트위터 분석기의 경우 명사만 가능합니다.

> * 사전에 등재되어도, 일부 라이브러리의 경우, 신규 추가된 단어의 우선순위가 낮아 적용되지 않을 수도 있습니다.

```scala
/* 패키지 명: 한나눔(hnn), 코모란(kmr), 꼬꼬마(kkma), 은전한닢(eunjeon), 트위터(twt) */
// 예시에서는 한나눔 사전에 추가
import kr.bydelta.koala.hnn.Dictionary
import kr.bydelta.koala.POSTag

Dictionary.addUserDictionary(
  "설빙" -> POSTag.NNP, /* 고유명사 '설빙' 추가 */
  "구글하" -> POSTag.VV /* 동사 '구글하다' 추가 */
)
```

## 여러 패키지의 사용
통합 인터페이스는 여러 패키지간의 호환이 가능하게 설계되어 있습니다. 이론적으로는 타 패키지의 품사 분석 결과를 토대로 구문 분석이 가능합니다.
> __Experimental__
> * 본 분석의 결과는 검증되지 않았으며, 잘못된 분석에 대해서 KoalaNLP는 책임지지 않습니다.
> * 신조어 등으로 인해 한나눔이나 꼬꼬마에서 품사 분석이 제대로 수행되지 않을 경우를 위한 기능입니다.
> * 사용자 정의 사전은 `Tagger`와 `Parser`의 대상이 되는 패키지에 모두에 추가하여야 합니다.

```scala
/* 패키지 명: 한나눔(hnn), 코모란(kmr), 꼬꼬마(kkma), 은전한닢(eunjeon), 트위터(twt) */
// 예시에서는 트위터 문장분석기, 은전한닢 품사 분석, 꼬꼬마 구문 분석을 진행함.
import kr.bydelta.koala.twt.SentenceSplitter
import kr.bydelta.koala.eunjeon.Tagger
import kr.bydelta.koala.kkma.Parser

val splitter = new SentenceSplitter
val tagger = new Tagger
val parser = new Parser

val paragraph = "누군가가 말했다. Python에는 KoNLPy가 있다. Scala는 KoalaNLP가 있었다."
val sentences = splitter.sentenceOf(paragraph)
val tagged = sentences.map(tagger.tagSentence)
val parsed = tagged.map(parser.parse)
```

## 자료 구조
### Class `Morpheme` (형태소)
* String `morpheme` 형태소 
* String `rawTag` 품사 분석을 진행한 분석기에서 부여한 품사 (통합 전)
* koala.POSTag `tag` 통합 품사 
* koala.Processor `processor` 품사 분석을 진행한 패키지
* Boolean `isNoun`, `isVerb`, `isModifier`, `isJosa` 명사/동사/관형사/조사 여부
* Boolean `hasTag(tag:String)` 통합 품사가 tag로 제시한 해당 통합 품사의 하위 분류인지 확인
* Boolean `hasRawTag(tag:String)` 원본 품사가 tag로 제시한 품사의 하위 분류인지 확인

### Class `Word` (어절)
Word는 `Iterable[Morpheme]`을 상속합니다.
* String `originalWord` 원본 어절 또는 복원된 어절
* Seq[Morpheme] `morphemes` 어절에 포함된 형태소들
* Seq[Word] `dependents` 현재 어절이 지배소(Dominant)인 의존소(Dependent) 목록. 즉, 현재 어절에 의존하는 어절의 목록.
* String `rawTag` 의존구문분석의 원본 결과. 현재 어절이 지배소와 가지는 관계. 즉, 현재 어절이 상위 어절과 가지는 관계의 이름.
* koala.FunctionalTag `tag` 의존구문분석의 통합 결과.
* Int `numOfMeaningful` 명사, 동사, 관형사 형태소의 수
* Boolean `matches(seq: Seq[String])` 주어진 품사 목록을 순서대로 가지고 있는지 검사함.
* Boolean `existsMorpheme(tag: String)` 주어진 품사를 가지고 있는지 검사함.
* Morpheme `apply(index: Int)`, Option[Morpheme] `get(index: Int)` 주어진 위치의 형태소를 가져옴.
* Morpheme `apply(tag: String)`, Option[Morpheme] `get(tag: String)` 주어진 품사의 형태소를 가져옴.
* Morpheme `getNextOf(m: Morpheme)`, `getPrevOf(m: Morpheme)` 주어진 형태소의 다음 또는 이전 위치의 형태소를 가져옴.

### Class `Sentence` (문장)
Sentence는 `Iterable[Word]`를 상속합니다.
* Seq[Word] `words` 문장 내의 단어들
* Word `rootWord` 의존구문분석에서 Root(뿌리)가 되는 단어, 즉, 핵심어.
* Sentence `++(other: Sentence)` 문장을 이어붙여 새 문장을 구성함.
* Boolean `matches(seq: Seq[Seq[String]])` 주어진 품사 목록의 단어 목록을 순서대로 가지고 있는지 검사함.
* Seq[Word] `nouns`, `verbs`, `adjectives` 문장 내 명사, 동사, 관형사를 포함한 단어들
* Word `apply(index: Int)`, Option[Word] `get(index: Int)` 주어진 위치의 단어를 가져옴.
* String `originalString(delimiter: String = " ")` 띄어쓰기를 교정한 원본 문장을 구성하여 돌려줌.

# License 조항
이 프로젝트 자체(KoalaNLP-core)와 인터페이스 통합을 위한 코드는  *GPL v3*을 따르며,
각 분석기의 License와 저작권은 각 프로젝트에서 지정한 바를 따릅니다.
* Hannanum: GPL v3
* KKMA: GPL v2 (GPL v2를 따르지 않더라도, 상업적 이용시 별도 협의 가능)
* Komoran: GPL v2, 역컴파일 불가, 비상업적 용도 사용 가능, 상업적 용도 사용시 별도 협의 (3년미만의 10명 이하 사업장 자유)
* Twitter: Apache License 2.0
* Eunjeon: Apache License 2.0


# 결과 비교
실제 사용 성능을 보여드리기 위해서, 네이버 뉴스에서 임의로 문장을 선택하였습니다.

## 일반 문장
아래 문장은 **국토부**라는 단어 이외에는 일반적으로 큰 문제가 없는 문장입니다.
> 국토부는 시장 상황과 맞지 않는 일률적인 규제를 탄력적으로 적용할 수 있도록 법 개정을 추진하는 것이라고 설명하지만, 투기 세력에 기대는 부동산 부양책이라는 비판이 일고 있다.

### 은전한닢
```text
국토/NNG  부/NNG는/JX  시장/NNG  상황/NNG과/JKB  맞/VV지/EC  않/VX는/ETM  일률/NNG적/XSN이/VCPᆫ/ETM  규제/NNG를/JKO  탄력/NNG적/XSN으로/JKB  적용/NNG하/XSVᆯ/ETM  수/NNB  있/VV도록/EC  법/NNG  개정/NNG을/JKO  추진/NNG하/XSV는/ETM  것/NNB이/VCP  라고/EC  설명/NNG하/XSV지만/EC  ,/SP  투기/NNG  세력/NNG에/JKB  기대/VV는/ETM  부동/NNG산/NNG  부양/NNG책/NNG이/VCP  라는/ETM  비판/NNG이/JKS  일/VV고/EC  있/VX다/EF  ./SF
```
은전한닢은 **국토부**의 국토와 부, **부동산**의 부동과 산, **부양책**의 부양과 책을 별개로 인식하였고, **것이 라고**, **부양책이 라는**과 같이, 띄어쓰기를 하였으며, 문장의 종결부호나 구분부호(**./SF ,/SP**)를 띄어쓰기 하였습니다. 품사 부착에는 큰 문제가 없어보입니다.

### 한나눔
```text
국토/NNG부/NNG는/JX  시장/NNG  상황/NNG과/JC  맞/VV지/EC  않/VX는/ETM  일률/NNG적/NNG이/VCPㄴ/ETM  규제/NNG를/JKO  탄력/NNG적/NNG으로/JKB  적용/NNG하/XSVㄹ/ETM  수/NNB  있/VX도록/EC  법/NNG  개정/NNG을/JKO  추진/NNG하/XSV는/ETM  것/NNB이/VCP라/EF고/JKQ  설명/NNG하/XSV지/EC말/VXㄴ/ETM,/SP  투/NNB이/VCP기/ETN  세력/NNG에/JKB  기대/VV는/ETM  부동산/NNG  부양책/NNG이/VCP라/EF는/ETM  비판/NNG이/JKC  일/VV고/EC  있/VX다/EF  ./SF
```
한나눔은 **국토부**의 국토와 부를 별개로 인식하였고, 문장 종결 부호(**./SF**)를 띄어 쓰기 하였습니다. **투기**라는 단어를 의존명사 **투** + 긍정지정사 **이-** + **명사형 전성어미** -기로 인식, "~라고 말하는 투기"의 투기로 인식하였습니다. 동사와 그 변형의 분석에 가장 자세합니다.

### 꼬꼬마
```text
국토/NNG  부/NNG는/JX  시장/NNG  상황/NNG과/JKB  맞/VV지/EC  않/VX는/ETM  일률적/NNG이/VCPㄴ/ETM  규제/NNG를/JKO  탄력/NNG적/XSN으로/JKB  적용/NNG하/XSVㄹ/ETM  수/NNM  있/VV도록/EC  법/NNG  개정/NNG을/JKO  추진/NNG하/XSV는/ETM  것/NNM이/VCP라고/EC  설명/NNG하/XSV지만/EC,/SP  투기/NNG  세력/NNG에/JKB  기대/VV는/ETM  부동산/NNG  부양책/NNG이/VCP라는/ETM  비판/NNG이/JKS  일/VV고/EC  있/VX다/EF./SF
```
꼬꼬마는 **국토부**의 국토와 부를 별개로 인식하였고, 일반 의존명사 "수", "것"을 단위성 의존명사 **NNM**으로 잘못 인식하였습니다.

### 코모란
```text
국토/NNG부/NNG는/JX  시장/NNG  상황/NNG과/JC  맞/VV지/EC  않/VX는/ETM  일률/NNG적/XSN이/VCPㄴ/ETM  규제/NNG를/JKO  탄력/NNG적/XSN으로/JKB  적용/NNG하/XSVㄹ/ETM  수/NNB  있/VV도록/EC  법/NNG  개정/NNG을/JKO  추진/NNG하/XSV는/ETM  것/NNB이/VCP라고/EC  설명/NNG하/XSV지만/EC,/SP  투기/NNG  세력/NNG에/JKB  기대/NNG는/JX  부동산/NNG  부양책/NNG이/VCP라는/ETM  비판/NNG이/JKS  일/NNB이/VCP고/EC  있/VX다/EF./SF
```
코모란은 **국토부**의 국토와 부를 별개로 인식하였고, 문장의 종결부호나 구분부호(**./SF ,/SP**)를 앞선 단어에 붙여 쓰기 하였습니다. "의견 따위가 나타나고"라는 뜻의 **일고**를 의존명사 일 + 긍정 지정사 이- + 접속조사 -고 와 분석, "~하는 일이고"의 "일이고"로 잘못 분석하였습니다.

### 트위터
```text
국토부/NNP  는/JX   /SY  시장/NNG   /SY  상황/NNG  과/JX   /SY  맞지/VV   /SY  않는/VV   /SY  일률/NNG  적/XSO  인/JX   /SY  규제/NNG  를/JX   /SY  탄력/NNG  적/XSO  으로/JX   /SY  적용할/VV   /SY  수/NNG   /SY  있도/VA  록/EF   /SY  법/NNG   /SY  개정/NNG  을/JX   /SY  추진하는/VV   /SY  것/NNG  이라고/JX   /SY  설명하지/VV  만/EF  ,/SF   /SY  투기/NNG   /SY  세력/NNG  에/JX   /SY  기대는/VV   /SY  부동산/NNG   /SY  부양책/NNG  이라는/JX   /SY  비판/NNG  이/JX   /SY  일/NNG  고/JX   /SY  있다/VA  ./SF
```
트위터 분석기는 가장 넓은 범위로 분석, 품사 내부의 세부 구분이 나타나지 않으며, 어절 단위의 묶음을 지원하지 않습니다. 또한, 공백을 하나의 문자로 인식하는 것을 보실 수 있습니다.

## 문장 분리 성능 (따옴표 안에 여러 문장이 인용될 때)
아래 문장은 겹따옴표("") 사이에 3개의 문장이 포함되어, 문장 분리에 까다로운 문장입니다. 문장 분리만을 보기 위해서, 어절, 형태소 구분은 유지하지만, 품사 구분은 생략합니다.

> 집 앞에서 고추를 말리던 이숙희(가명·75) 할머니의 얼굴에는 웃음기가 없었다. "나라가 취로사업이라도 만들어주지 않으면 일이 없어. 섬이라서 어디 다른 데 나가서 일할 수도 없고." 가난에 익숙해진 연평도 사람들은 '정당'과 '은혜'라는 말을 즐겨 썼다.

### 은전한닢 (Koala 구현)
```text
집  앞+에서  고추+를  말리+던  이숙희  (  가명  ·  75  )  할머니+의  얼굴+에+는  웃음+기+가  없+었+다  .
"  나라+가  취로  사업+이  라도  만들+어  주+지  않+으면  일+이  없+어  .  섬+이  라서  어디  다른  데  나가+서  일+하+ᆯ  수+도  없+고  .  "  가난+에  익숙+하+아+지+ᆫ  연평+도  사람+들+은  '  정당  '  과  '  은혜  '  이+라는  말+을  즐기+어  쓰+었+다  .
```
정상 분리입니다. 따옴표가 끝나는 부분에서 문제가 발생하지만, 이는 처리할 수 없는 부분입니다. ("~하였다."라고 말했다)라는 문장을 분리할 수 없기 때문입니다.

### 한나눔
```text
집  앞+에서  고추+를  말+ㄹ+리+이+던  이숙희  (  가명  ·  75  )  할머니+의  얼굴+에+는  웃음+기+가  없+었+다  .
"+나라+가  취로사업+이+라+도  만들+어+주+지  않+으면  일+이  없+어  .
서+ㅁ+이+라서  어디  다른  데  나가+아  일+할  수+도  없+고  .+"
가난+에  익숙해지+ㄴ  연평도  사람+들+은  '+정당+'과  '+은혜+'+라는  말+을  즐기+어  쓰+었+다  .
```
한나눔은 문장부호를 단어에 붙여쓰는 경향과, 동사를 우선하여 인식하려는 경향으로 인해서, 따옴표 안의 문장이 분리되었습니다. 다만 홑따옴표로 강조된 단어는 한 어절로 바르게 인식되었습니다.

### 꼬꼬마
```text
집  앞+에서  고추+를  말리+더+ㄴ  이  숙희  (  가명  ·  75  )  할머니+의  얼굴+에+는  웃음기+가  없+었+다+.
"  나라+가  취로  사업+이+라도  만들+어  주+지  않+으면  일+이  없+어+.  섬+이+라서  어디  다른  데  나가+서  일하+ㄹ  수+도  없+고+.+"  가난+에  익숙  해지+ㄴ  연평도  사람+들+은  '  정당+'  과  '  은혜+'  이+라는  말+을  즐기+어  쓰+었+다+.
```
꼬꼬마는 정상적으로 분리되었습니다.

### 코모란 (Koala 구현)
```text
집  앞+에서  고추+를  말리+던  이+숙희+(+가명+·+75+)  할머니+의  얼굴+에+는  웃음기+가  없+었+다+.
"+나라+가  취로사업이라도  만들+어+주+지  않+으면  일+이  없+어+.  섬+이+라서  어디  다른  데  나가+아서  일+하+ㄹ  수+도  없+시+고+.+"  가난+에  익숙+하+아+지+ㄴ  연평도  사람+들+은  '+정당+'+과  '+은혜+'+이+라는  말+을  즐기+어  쓰+었+다+.
```
정상적으로 분리되었습니다.

### 트위터
공백 문자는 _로 표시합니다.
```text
집  _   앞  에서  _  고추  를  _  말리  던  _  이숙희  (  가명  ·  75  )  _  할머니  의  _  얼굴  에는  _  웃음  기  가  _  없었  다  .
"  나라  가  _  취  로  사업  이라도  _  만들어  주  지  _  않으  면  _  일이  _  없어  .
섬  이라서  _  어디  _  다른  _  데  _  나가서  _  일할  _  수도  _  없고  ."
가난  에  _  익숙해진  _  연평도  _  사람  들  은  _  '  정당  '  과  _  '  은혜  '  라는  _  말  을  _  즐겨  _  썼  다  .
```
트위터 분석기는 겹따옴표 내의 문장을 인용문으로 인식하지 않았습니다.

## 사전에 없는 단어 1
아래는 사전에 없을 법한 단어인 **포켓몬**과 **와이파이존**이 있고, 지명인 **속초**가 등장하는 문장입니다.

> 포털의 '속초' 연관 검색어로 '포켓몬 고'가 올랐고, 속초시청이 관광객의 편의를 위해 예전에 만들었던 무료 와이파이존 지도는 순식간에 인기 게시물이 됐다.

### 은전한닢
```text
포털/NNP의/JKG  '/SY  속초/NNP  '/SY  연관/NNG  검색/NNG어/NNG로/JKB  '/SY  포켓몬/NNP  고/NNG  '/SY  가/JKS  오르/VV았/EP고/EC  ,/SP  속초/NNG  시청/NNG이/JKS  관광/NNG객/NNG의/JKG  편의/NNG를/JKO  위하/VV아/EC  예전/NNG에/JKB  만들/VV었/EP던/ETM  무료/NNG  와이파이/NNP  존/NNP  지도/NNG는/JX  순식/NNG간/NNG에/JKB  인기/NNG  게시/NNG물/NNG이/JKS  되/VV었/EP다/EF  ./SF
```
속초, 포켓몬, 와이파이존 모두 명사구 또는 복합명사구로 정상 인식되었습니다.

### 한나눔
```text
포털/NNG의/JKG  '/SS속/NNM초/XSN'/SS  연관/NNG  검색/NNG어로/NNG  '포켓몬/NNG  고/MM'/SS가/JKC  오르/VV아/EP고/EC,/SP  속초시청/NNG이/JKC  관광객/NNG의/JKG  편의/NNG를/JKO  위하/VV어/EC  예전/NNG에/JKB  만들/VV었/EP던/ETM  무료/NNG  와이파이존/NNG  지/NNB도/JX는/JX  순식간/NNG에/JKB  인기/NNG  게시/NNG물/NNG이/JKC  되/VV었/EP다/EF  ./SF
```
속초는 분리되었으나, 속초시청은 하나로 인식되었으며, 포켓몬과 와이파이존은 명사로 인식되었습니다.

### 꼬꼬마
```text
포털/NNG의/JKG  '/SS  속/NNG  초/NNM'/SS  연관/NNG  검색어/NNG로/JKB  '/SS  포켓/NNG  몬/MAG  고/NNG'/SS  가/VV아/EC  오르/VV았/EP고/EC,/SP  속초시/NNP청/XSN이/JKS  관광객/NNG의/JKG  편의/NNG를/JKO  위하/VV어/EC  예전/NNG에/JKB  만들/VV었/EP더/EPㄴ/ETM  무료/NNG  와이/NNG  파이/NNG  존/NNP  지도/NNG는/JX  순식간/NNG에/JKB  인기/NNG  게시물/NNG이/JKC  되/VV었/EP다/EF./SF
```
속초는 속, 초로 어절이 분리되었으며, 속초시청은 속초시+청(명사파생 접미사)으로 분리되었으며, 포켓몬은 포켓, 몬(관형사)으로 어절이 분리되고, 와이파이존은 와이, 파이, 존으로 분리되었습니다.

### 코모란
```text
포털/NNG의/JKG  '/SS속초/NNP'/SS  연관/NNG  검색어/NNG로/JKB  '포켓몬/UE  고/NNG'/SS가/JKS  오르/VV았/EP고/EC,/SP  속초/NNP시청/NNG이/JKS  관광객/NNG의/JKG  편의/NNG를/JKO  위하/VV아/EC  예전/NNG에/JKB  만들/VV었/EP던/ETM  무료/NNG  와이/NNG파이/NNG존/NNG  지도/NNG는/JX  순식간/NNG에/JKB  인기/NNG  게시물/NNG이/JKS  되/VV었/EP다/EF./SF
```
속초, 속초시청(속초+시청)은 정상 인식되었고, 포켓몬은 알 수 없는 단어로 정상 인식 되었지만, 와이파이존은 와이+파이+존으로 인식되었습니다.

### 트위터
```text
포털/NNP  의/JX   /SY  '/SF  속초/NNG  '/SF   /SY  연관/NNG   /SY  검색어/NNG  로/JX   /SY  '/SF  포켓몬/NNG   /SY  고/NNG  '/SF  가/VV   /SY  올랐/VV  고/EF  ,/SF   /SY  속초/NNP  시청/NNG  이/JX   /SY  관광객/NNG  의/JX   /SY  편의/NNG  를/JX   /SY  위해/NNG   /SY  예전/NNG  에/JX   /SY  만들었/VV  던/EF   /SY  무료/NNG   /SY  와이파이존/NNG   /SY  지도/NNG  는/JX   /SY  순식간/NNG  에/JX   /SY  인기/NNG   /SY  게시/NNG  물이/NNG   /SY  됐/VV  다/EF  ./SF
```
속초, 속초 시청, 포켓몬, 와이파이존 모두 정상 인식되었습니다.

## 사전에 없는 단어 2
아래 문장에서는 **사드**, **월스트리트 저널**이 문제가 될 수 있는 단어입니다.
> 미국 국방부가 미국 미사일방어망(MD)의 핵심 무기체계인 사드(THAAD)를 한국에 배치하는 방안을 검토하고 있다고 <월스트리트 저널>이 28일(현지시각) 보도했다.

### 은전한닢
```text
미국/NNP  국방/NNG부/NNG가/JKS  미국/NNP  미사일/NNG  방어/NNG망/NNG  (/SS  MD/SL  )/SS  의/JKG  핵심/NNG  무기/NNG  체계/NNG이/VCPᆫ/ETM  사드/NNP  (/SS  THAAD/SL  )/SS  를/JKO  한국/NNP에/JKB  배치/NNG하/XSV는/ETM  방안/NNG을/JKO  검토/NNG하/XSV고/EC  있/VX다고/EC  </SY  월/NNG스트리트/NNP  저널/NNG  >/SY  이/JKS  28/SN  일/NNM  (/SS  현지/NNG  시각/NNG  )/SS  보도/NNG하/XSV았/EP다/EF  ./SF
```
사드는 정상인식되었으나, 월스트리트(월+스트리트) 저널은 일부 오류가 있습니다.

### 한나눔
```text
미국/NNG  국방부/NNG가/JKS  미국/NNG  미사일/NNG방어망/NNG  (/SS  MD/SL  )/SS  의/NNG  핵심/NNG  무기체계/NNG이/VCPㄴ/ETM  사드/NNG  (/SS  THAAD/SL  )/SS  를/NNG  한국/NNG에/JKB  배치/NNG하/XSV는/ETM  방안/NNG을/JKO  검토/NNG하고/JC  있/VX다/EF고/JKQ  </SS  월스트리트/NNG  저널/NNG  >/SS  이/MM  28/NR일/NNM  (/SS  현지시각/NNG  )/SS  보도/NNG하/XSV었/EP다/EF  ./SF
```
사드, 월스트리트 저널 모두 정상 인식되었습니다.

### 꼬꼬마
```text
미국/NNP  국방부/NNG가/JKS  미국/NNP  미사일/NNG  방어망/NNG  (/SS  MD/SL  )/SS  의/NNG  핵심/NNG  무기/NNG체계/NNG이/VCPㄴ/ETM  사드/UN  (/SS  THAAD/SL  )/SS  를/JKO  한국/NNP에/JKB  배치/NNG하/XSV는/ETM  방안/NNG을/JKO  검토/NNG하/XSV고/EC  있/VX다고/EF
</SS  월/NNG  스트리트/NNG  저널/NNG  >/SS  이/MM  28/NR일/NNM  (/SS  현지/NNG  시각/NNG  )/SS  보도/NNG하/XSV었/EP다/EF./SF
```
사드는 명사로 추정되는 알 수 없는 단어로 정상 처리되었지만, 월스트리트 저널은 월, 스트리트, 저널로 분리되어 인식되었습니다.

### 코모란
```text
미국/NNP  국방부/NNG가/JKS  미국/NNP  미사일/NNG방어망/NNG(/SSMD/SL)/SS의/JKG  핵심/NNG  무기/NNG체계/NNG이/VCPㄴ/ETM  사/NNG드/NNG(/SSTHAAD/SL)/SS를/JKO  한국/NNP에/JKB  배치/NNG하/XSV는/ETM  방안/NNG을/JKO  검토/NNG하/XSV고/EC  있/VV다고/EC  </SS월스트리트/NNP  저널/NNG>/SS이/MM  28/SN일/NNB(/SS현지/NNG시각/NNG)/SS  보도/NNG하/XSV았/EP다/EF./SF
```
사드는 사+드로 분리되어 인식되었고, 월스트리트 저널은 정상 인식되었습니다.

### 트위터
```text
미국/NNG   /SY  국방부/NNG  가/JX   /SY  미국/NNG   /SY  미사일방어/NNP  망/NNG  (/SF  MD/SY  )/SF  의/NNG   /SY  핵심/NNG   /SY  무기체계/NNP  인/JX   /SY  사드/NNG  (/SF  THAAD/SY  )/SF  를/NNG   /SY  한국/NNG  에/JX   /SY  배치/NNG  하는/VV   /SY  방안/NNG  을/JX   /SY  검토/NNG  하고/JX   /SY  있다/VA  고/EF   /SY  </SF  월스트리트/NNG   /SY  저/MM  널/NNG  >/SF  이/NNG   /SY  28일/NR  (/SF  현지/NNP  시각/NNG  )/SF   /SY  보도했/VV  다/EF  ./SF
```

사드는 정상 인식되었지만, 월스트리트 저널은 월스트리트, 저, 널로 인식되었습니다.
