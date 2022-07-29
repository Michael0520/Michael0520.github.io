---
title: Styled-component 元件管理
description: React 以輕量化 Library 自居，因此 React 在樣式刻畫、狀態管理、網頁互動上充滿靈活、自由的樣貌，相同的問題，有各式各樣的解決方案！
date: 2020-12-21
categories:
- JavaScript
- React
tags: 
- JavaScript
- React
---

> 參加 Web 實驗室 React 讀書會所做的筆記
# Styled-component 元件管理
React 以輕量化 Library 自居，因此 React 在樣式刻畫、狀態管理、網頁互動上充滿靈活、自由的樣貌，相同的問題，有各式各樣的解決方案！

> 前言
> 
>如何根據狀態(state)來動態改變 Web 的 CSS 樣式呢？大家透過各自的經驗及想法提出了許多不同的方案，包含：Styled Components, CSS module, Styled JS, Emotion, JSS, Glamor, Radium, Aphrodite 等...。在 CSS 2019 當中，CSS in JS 篇章裡 Styled Components 在 關注度、感興趣程度及滿意度 綜合評比中獲得非常不錯的總體評價。
---
styled-components 能在 JSX 當中 基於已刻畫好的元件中，透過 template literals ，在其中撰寫 CSS 樣式。使我們可以更專注、聚焦在每個元件之下，為使用者提供更好的體驗及視覺呈現。

### styled-components 的特點

1. `Automatic critical CSS: styled-components` 持續追蹤頁面上顯示的元件，並在其中注入樣式，完全自動化，可讓開發者 代碼分割(code splitting)，同時替使用者提供更好的體驗。（不載入未使用的冗余程式碼，提升載入速度）

2. `No class name bugs: styled-components` 自動替你的樣式，產生 class 名稱，不必再擔心命名的衝撞、想不到名字的窘境、拼錯字、重複使用等...。

3. `Easier deletion of CSS:` 傳統的程式碼在檔案之前，很難辨別某個 class name 在哪些地方被使用過了， styled-components 使元件結構與樣式的關聯，顯而易見，每份樣式都專注對應在某個元件上。假如這個元件沒被使用、想刪除了，這個樣式很容易跟著被一起刪除。

4. `Simple dynamic styling:` 當你需要根據某個 props 或是 global theme 來動態改變樣式時，styled-components 使這件事變得容易，不用手動管理無數的 css classes。

5. `Painless maintenance:` 不用再跨檔案去尋找你的樣式與結構，你可以在同一份檔案之中，替你的元件上結構及樣式。在維護上，就算未來你的 codebase 變更大了，也不會變得能以掌控。

6. `Automatic vendor prefixin:` 依照當前的標準來撰寫你的 CSS，讓 styled-components 替你完成其他任務，不用再思考不同瀏覽器間的前綴字，可以更專注在開發樣式上。
`
-webkit- (Chrome, Safari, iOS Safari / iOS WebView, Android)
-moz- (Firefox)
-ms- (Edge, Internet Explorer)
-o- (Opera, Opera Mini)
CSS Vendor Prefixes
`

---
1. 直接在 styled 預設提供的 HTML 元件，寫入 css 樣式

```javascript=
const Button = styled.button`
  background: blue;
  color: white;
  &:hover {
    background: gray;
    color: black;
  }
`;

render(<Button> 點我！</Button>);
```

2. 透過 props 動態改變 styled-components 的元件
```javascript=
const Button = styled.button<{ primary?: boolean }>`
  background: ${props => (props.primary ? 'pink' : 'blue')};
  color: ${props => (props.primary ? 'white' : 'green')};
  &:hover {
    background: gray;
    color: black;
  }
`;

render(
  <div>
    <Button> 點我！</Button>
    <Button primary> 點我！</Button>
  </div>
);
```

3. 基於某個 styled-components 之上，創造新的元件


```javascript=
const Button = styled.button`
  background: blue;
  color: white;
  &:hover {
    background: gray;
    color: black;
  }
`;
const CoolButton = styled(Button)`
  background: yellow;
  color: pink;
  &:hover {
    background: pink;
    color: yellow;
  }
`;

render(
  <div>
    <Button> 點我！</Button>
    <CoolButton> 點我！</CoolButton>
  </div>
);
```

如此可知，我們便可以修改某些其他人寫好的 styled-components 了

如 MATERIAL-UI, Ant Design 等等，
目前都有支援 styled-components 互動了
```javascript=
import Button from '@material-ui/core/Button';
const ChillButton = styled(Button)`
  font-weight: 900;
  text-transform: inherit;
`;
render(
  <ChillButton variant="contained" color="primary">
    Yoyoyo 點我！
  </ChillButton>
);
```
題外話，與有支援的第三方套件互動？！(以 MATERIAL-UI 為例) 期待其他大大分享如 Ant Design 等相關經驗。

有時候，我們會需要修改、覆寫到第三方套件預設的樣式，難不成要用到兇殘的 !important？

```javascript=
import Button from '@material-ui/core/Button';
const ChillButton = styled(Button)`
  color: blue !important;
  font-weight: 900;
  text-transform: inherit;
`;
render(
  <ChillButton variant="contained" color="primary">
    Yoyoyo 點我！
  </ChillButton>
);
```


也許你還有其他種解法，就是 MATERIAL-UI 提供改變注入樣式的優先順序的方法

```javascript=
import { StylesProvider } from '@material-ui/core/styles';
render(
  <StylesProvider injectFirst>
    <App />
  </StylesProvider>
);
```


4. 如何與其他無支援 styled-components 的元件互動及修改樣式呢？ （含其他第三方、自己的元件）

透過綁定 className 使 styled-components 能注入樣式，此範例來自官網 styling-any-component

```javascript=
// from official document https://styled-components.com/docs/basics#styling-any-component
// This could be react-router-dom's Link for example
const Link = ({ className, children }) => (
  <a className={className}>{children}</a>
);

const StyledLink = styled(Link)`
  color: palevioletred;
  font-weight: bold;
`;

render(
  <div>
    <Link>Unstyled, boring Link</Link>
    <br />
    <StyledLink>Styled, exciting Link</StyledLink>
  </div>
);
```

## **進階**

5. 參考其他元件，在元件樣式中使用 css 選擇器，選取其子元件

```javascript=
註解：& 代表 當下的這個元件，於是我們可以使用 &:hover,& > ${SomeComponent}

const StyledTitle = styled.h2`
  font-weight: 800;
  font-size: 20px;
`;
const StyledSection = styled.div`
  display: flex;
  align-items: center;
  & > ${StyledTitle} {
    margin-right: 20px;
    padding: 50px;
  }
`;
render(
  <StyledSection>
    <StyledTitle>You're the best!</StyledTitle>
  </StyledSection>
);
```

6. 參考其他元件，在元件樣式偵測上面，父元件的狀態

Icon 包在 Button 底下，有時我們會希望當 Button 被 hover 到時，Icon 的樣式也能一起動態改變樣式

參考文獻：
<React. 7 tricks to work with Styled Components>
<Official Doc [Referring to other components]>

```javascript=
const Button = styled.button<{ primary?: boolean }>`
  background: ${props => (props.primary ? 'pink' : 'blue')};
  color: ${props => (props.primary ? 'white' : 'green')};
  &:hover {
    background: gray;
    color: black;
  }
`;
const Icon = styled.i`
  color: white;
  background-color: orange;
  font-size: 1.5 rem;
  ${Button}:hover & {
    color: black;
  }
`;
render(
  <Button>
    Click me<Icon>icon </Icon>
  </Button>
);
```