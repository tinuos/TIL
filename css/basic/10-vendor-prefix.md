# CSS - 벤더 프리픽스 개념

- 벤더 프리픽스에 대해 학습

---

## Vendor prefix

| 브라우저 | 벤더 프리픽스 |
| :---: | :---: |
| IE or Edge | `-ms-` |
| Chrome | `-webkit-`|
| Firefox | `-moz-`|
| Safari | `-webkit-`|
| Opera | `-o-`|
| iOS Safari | `-webkit-`|
| Android Browser | `-webkit-`|
| Chrome for Android | `-webkit-`|

- vendor : 판매자 / prefix : 접두사
- 여기서 벤더는 브라우저 회사를 말하며 프리픽스는 속성명 앞에 붙는 단어를 의미한다.
- 브라우저가 제공하는 기능으로 실험적인 속성이나 CSS3 표준 확장 이전의 기능을 제공하기 위해 사용된다.

> poiemaweb에서 소개한 [Prefix Free 라이브러리](https://projects.verou.me/prefixfree/)와 같이 벤더 프리픽스 관련 도구 등을 이용하여 불필요한 사용을 자제할 수 있다고 한다. 추가적으로 속성 사용 시 Can I use 사이트나 MDN 에서 브라우저 별로 적용 가능한 지 확인하기

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-vendor-prefix)