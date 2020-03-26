# javascript ) The Observers

###### 자바스크립트 기본 내장 옵저버!



## 옵저버 패턴

###### 모든 객체들의 신속한 동기화를 위해 데이터를 보유한 주체(subject)를 여러 객체들이 감시(observe)하는 방식으로 모든 요소들이 동시에, 즉각적으로 변해야한다.

###### => 엑셀에서 스프레드시트의 값을 바꿀 때마다 표와 차트등에 변화가 전달



## JS Observers

1. ### IntersectionObserver 

   ###### 루트 영역(뷰포트와 대상 객체의 겹침을 감시)

   ###### 성능개선에 사용

   

2. ### ResizeObserver

   ###### 객체의 너비, 높이의 변화를 감시

   ###### 섬세한 애니메이션을 필요로 할 때 유용하게 사용 (최신 크롬환경에서만 작동...)

   

3. ### MutationObserver

   ###### 객체의 속성 변경을 감시

   ###### DOM 객체의  '속성' 영역을 감시 (호환성 좋음)

   

4. ### PerformanceObserver

   ###### 프로세스 성능 모니터링

   ###### 호환성이 낮음 / 다른툴 => Perfume.js 

   

5. ### ReportingObserver

   ###### 웹 사이트의 표준 및 정책 준수 현황을  감시

   ###### 아직 지원하는 브라우저가거의 없음



(참고 : [MDN Web APIs](https://developer.mozilla.org/en-US/docs/Web/API))

출처 : [huskyhoochu.com](https://www.huskyhoochu.com/js-observers/)