# 🚇 지하철 노선도 미션

## 📌생각하기
3주차 미션도 노션에 생각, 계획 등을 정리하면서 진행했습니다. 링크에 들어가서 맨 마지막 항목인 `'🎈느낀점'`만 보시면 됩니다!

↓↓ 노션 링크 ↓↓

[https://www.notion.so/Week3-b61a21d55cb942c7b637568c9f726b37]

<br/>

## 🔨모듈 분리
```
📁 docs
└ README.md

📁 src
├ 📁 ui
│	├ init-ui.js
│	├ station-ui.js
│	├ line-ui.js
│   ├ 📁 section
│	│	├ section-selection-ui.js
│	│	├ section-management-ui.js
│	│	└ section-management-table-ui.js
│	└ map-ui.js
│
├ 📁 util
│	├ station.js
│	├ line.js
│	├ section.js
│	└ storageAccess.js
│
├ index.js
└ constants.js

📄 index.html
```
- 웹에 표시되는 'ui'와 관련된 파일과 작동과 관련된 'util' 파일을 분리하였다.
- 예를 들어 '역 목록'에서 역을 하나 삭제한다고 할 때 화면에 보이는 표에서 행이 하나 사라지는 것은 'ui'로, localStorage에서 해당 역이 사라지는 것은 'util'로 배치하였다.
- 따라서 유효성을 검사하는 함수는 util에 있다.
- localStorage를 DB라고 생각하고, DB에 접근하기 위한 함수를 starageAccess.js에 따로 모아두었다.
- 저번주와 마찬가지로 이후에 변동 가능하거나 상수 취급이 가능한 요소는 모두 'constatns.js'에 정리하였다.

<br/>

## 🚀 기능 요구사항

**⭐: 예외사항**

### 메뉴 관련 기능
- 메뉴 버튼을 누르면 해당 페이지가 로드된다.
### 지하철 역 관련 기능
- 지하철 역을 등록하고 삭제할 수 있다. 
- (단, 노선에 등록된 역은 삭제할 수 없다) ⭐
- 중복된 지하철 역 이름이 등록될 수 없다. ⭐
- 지하철 역은 2글자 이상이어야 한다. ⭐
- 지하철 역의 목록을 조회할 수 있다.

### 지하철 노선 관련 기능
- 지하철 노선을 등록하고 삭제할 수 있다.
- 중복된 지하철 노선 이름이 등록될 수 없다. ⭐
- 노선 등록 시 상행 종점역과 하행 종점역을 입력받는다.
- 지하철 노선의 목록을 조회할 수 있다.

### 지하철 구간 추가 기능
- 지하철 노선에 구간을 추가하는 기능은 노선에 역을 추가하는 기능이라고도 할 수 있다.
  - 역과 역사이를 구간이라 하고 이 구간들의 모음이 노선이다.  
- 하나의 역은 여러개의 노선에 추가될 수 있다.
- 역과 역 사이에 새로운 역이 추가 될 수 있다.
- 노선에서 갈래길은 생길 수 없다. ⭐
- 추가하려는 역의 index가 out of range가 아니다. ⭐

### 지하철 구간 삭제 기능
- 노선에 등록된 역을 제거할 수 있다.
- 종점을 제거할 경우 다음 역이 종점이 된다.
- 노선에 포함된 역이 두개 이하일 때는 역을 제거할 수 없다.⭐

### 지하철 노선에 등록된 역 조회 기능
- 노선의 상행 종점부터 하행 종점까지 연결된 순서대로 역 목록을 조회할 수 있다.

<br/>

## ✅ 프로그래밍 요구사항

### 메뉴 버튼
- 역 관리 button 태그는 `#station-manager-button` id값을 가진다.
- 노선 관리 button 태그는 `#line-manager-button` id값을 가진다.
- 구간 관리 button 태그는 `#section-manager-button` id값을 가진다.
- 지하철 노선도 출력 관리 button 태그는 `#map-print-manager-button` id값을 가진다.

### 지하철 역 관련 기능
- 지하철 역을 입력하는 input 태그는 `#station-name-input` id값을 가진다.
- 지하철 역을 추가하는 button 태그는 `#station-add-button` id값을 가진다.
- 지하철 역을 삭제하는 button 태그는 `.station-delete-button` class값을 가진다.

### 지하철 노선 관련 기능
- 지하철 노선의 이름을 입력하는 input 태그는 `#line-name-input` id값을 가진다.
- 지하철 노선의 상행 종점을 선택하는 select 태그는 `#line-start-station-selector` id값을 가진다.
- 지하철 노선의 하행 종점을 선택하는 select 태그는 `#line-end-station-selector` id값을 가진다.
- 지하철 노선을 추가하는 button 태그는 `#line-add-button` id값을 가진다.
- 지하철 노선을 삭제하는 button 태그는 `.line-delete-button` class값을 가진다.

### 지하철 구간 추가 기능
- 지하철 노선을 선택하는 button 태그는 `.section-line-menu-button` class값을 가진다.
- 지하철 구간을 설정할 역 select 태그는 `#section-station-selector` id값을 가진다.
- 지하철 구간의 순서를 입력하는 input 태그는 `#section-order-input` id값을 가진다.
- 지하철 구간을 등록하는 button 태그는 `#section-add-button` id값을 가진다.
- 지하철 구간을 제거하는 button 태그는 `.section-delete-button` class값을 가진다.

### 지하철 노선도 출력 기능
- 지하철 노선도 출력 버튼을 누르면 `<div class="map"></div>` 태그를 만들고 해당 태그 내부에 노선도를 출력한다.

<br/>

## 🎈 추가 고려사항

### 2주차 피드백 반영사항
- **기능 구현 목록을 재검토한다 -** 함수 목록을 먼저 완성하고 그대로 구현하는 게 좋은 방법인 줄 알았는데, 2주차 피드백을 보니 그게 아니라는 것을 알게 되었다. '함수 목록'을 삭제하고 전체적인 구조를 전달하려 했다. 예외사항은 눈에 띄게 따로 표시하였다.
- **상수를 활용한다 -** 결과 메세지와 같은 'string'값은 상수화할 생각은 했는데, 이동/정지 기준처럼 눈에 안 띄는 int값은 상수화할 생각은 못 했다. 이번에는 잊지 않고 '역 이름 길이' 기준을 상수화했다. 이후 로직을 변경할 때 훨씬 수월할 것 같다.
- **Boolean을 return하는 경우 간결하게 한다 -** 몰랐던 사실이다.. 예외사항을 처리하는 isValid 함수를 되도록이면 return 한 줄로 구현했다.
- **불필요한 변수를 줄이기 위해 노력한다 -** 초보자의 입장에서는 새 변수를 계속해서 만들게 되는 것 같아서.. let이나 const를 사용하더라도 새 변수를 최대한 적게 선언하려 했다. var을 금지시킨 이유를 알 것 같았다.
- **비지니스 로직과 UI로직을 분리해라 -** 3주차 과제는 '비즈니스 & 로직'을 기준으로 파일을 분리해보았다!
- **git을 통해 관리할 자원에 대해서도 고려한다 -** ㅠㅠ eslint 관련 파일은 커밋하지 않았다.

### 개인적으로 고려한 사항
- 예외사항을 'isValid' 류의 함수로만 관리하였다. 예를 들어 이름이 중복되는지 검사하는 hasNameOnList, 길이가 적절한지 검사하는 isLengthOutOfRange를 따로 만들고, 이런 예외사항을 한꺼번에 검사하는 최종(?)함수 isNameValid에 모두 담았다.
- 나의 코드를 처음 보는 사람도 이해하기 쉽게 하려고 노력하였다. 또 코드가 너무 복잡해지면 내가 쓴 코드임에도 버그를 찾을 때 시간이 너무 오래 걸렸기 때문이다. 내 능력 하에서 다른 사람이 봤을 때 수정이 쉬울 수 있도록 작성하였다.
    - 예컨대 모듈을 최대한 직관적으로 분리하고 각 파일의 길이가 너무 길어지지 않도록 했다.
    - 또한 'constants.js'에 분리해 둔 상수도 직관적으로 이름을 붙이려 했다. 예를 들어 '역 이름 길이 제한'은 'STATION.VALIDNAMELENGTH' 로 접근할 수 있다.
- 문제가 생기면 함수가 한 가지 기능만을 하는지 & "정말 제대로" 작동하는지 확인 후 수정했다.
    - 완벽하고 간결한 함수는 머리가 너무 복잡해지는 것을 막아주었다.

### 저번 주차에 비해 발전한 사항
- 한 파일의 길이가 줄어들었다. 파일 하나에 너무 많은 함수가 포함되어있으면 코드를 파악하기 힘들다.
    - '3. 구간 관리'에 해당하는 파일이 너무 길어져서 selection, managment, table 로 분리해서 관리했다.