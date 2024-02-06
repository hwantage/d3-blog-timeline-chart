
## d3-blog-timeline-chart

![image](https://github.com/hwantage/d3-blog-timeline-chart/assets/82494320/ac2a071e-e9db-4036-9f71-c8ad82e8ecc6)

휴고 블로그의 sitemap 정보를 읽어들여 타임라인 차트로 생성하도록 하기위해 제작하였습니다.
포스트와 포스트 사이의 시간 간격과 포스트가 언제 작성되었는지 상대 날짜로 확인이 가능합니다. 블로그 포스팅을 열심히 하라는 무언의 압박이...

[live demo](https://hwantage.github.io/d3-blog-timeline-chart/timeline.html)

[blog showcase](https://hwantage.github.io/posts/)

데이터는 다음과 같이 작성합니다.
```javascript
var timelineData = [
  {
    id: "0",
    permalink: "https://hwantage.github.io/posts/hugo/",
    title: "HUGO를 이용한 정적 사이트 생성 및 github pages를 이용한 블로그 운영 방법",
    category: "[Front-end]",
    date: "2024-01-12 13:14:52"
  },
  {
    id: "1",
    permalink: "https://hwantage.github.io/posts/nvm/",
    title: "nvm을 이용한 node.js의 버전 관리 방법",
    description: "NVM(Node Version Manager)를 이용한 node  버전 관리 방법",
    category: "[Front-end]",
    date: "2024-01-12 13:14:52"
  },
  {
    id: "2",
    permalink: "https://hwantage.github.io/posts/npm-publish/",
    title: "CSS-Deduplication part 3 (postcss 플러그인을 npmjs.org에 배포)",
    description: "postcss 플러그인을 npmjs에 배포하기",
    category: "[Front-end]",
    date: "2024-01-14 10:32:14"
  }
]
```

### Usage
```javascript
var timeline = HTimelineChart.makeChart("timelineWrapper", {
        ChartType: "TimeLine",
        ChartTitle: "Post Timeline", // 챠트 상단 타이틀 설정
        TimeSkipInterval: 0, // milliseconds (1시간=3600000)
        TimeSkipTickInterval: 200, // TimeSkipTick 간격
        TickInterval: 200, // 노드사이 간격
        DateFormatType: "before", // normal/after/before
        ChartData: timelineData,
        Onload: function (chart) {
          console.log("chart create.", chart);
        },
        NodeClick: function (node, nodeData) {
          console.log(node);
          console.log(nodeData);
          window.open(nodeData["permalink"], "_blank");
        },
      });

      timeline.scrollToTarget(timelineData.length - 1); // 챠트 포커스(스크롤) 이동
```

### Options
`ChartType` : TimeLine 고정값. 추후 type 확장 가능성 있음.

`ChartTitle` : 차트 상단 타이틀

`TimeSkipInterval` : milliseconds 인터벌(1시간=3600000), 노드 사이에 시간 차이를 ... 으로 표기하는데 인터벌 시간 이내이면 ... 을 표기하지 않음

`TimeSkipTickInterval` : px 단위 설정. 인터벌 시간 이상인 경우의 노드 사이 간격

`TickInterval` : px 단위 설정. 인터벌 시간 이내인 경우의 노드 사이 간격

`DateFormatType` : normal(시간으로 표기)/after(시작 시간부터 이후 날짜 단위로 표기)/before(현재 날짜부터 이전 날짜 단위로 표기)

`ChartData` : 차트를 위한 데이터 

`Onload` : 차트 로그 완료 이벤트 콜백

`NodeClick` : 노드 클릭 이벤트 콜백

### Method
`scrollToTarget` : id 값의 노드로 포커스 이동

### License 
MIT
