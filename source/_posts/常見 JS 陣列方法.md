---
tags: 2022 React 新手讀書會
---

# 常見 JS 陣列方法

在寫 React 時很常使用陣列方法來進行渲染、判斷等等，因此在真正開始進入到 React 之前，先來練習一下常見的陣列方法吧！

### `.forEach()`

forEach() 方法會將陣列內的每個元素，皆傳入並執行一次。
**不會建立新的陣列以及回傳任何數值**

```javascript
const array1 = ["apple", "banana", "berry"];

array1.forEach((element) => console.log(element));

// 結果為 "apple"
// 結果為 "banana"
// 結果為 "berry"
```

### `.map()`

map() 方法會建立一個新的陣列，其新陣列的內容是原陣列的每一個元素經由運算後回傳的結果。

```javascript
const array1 = [1, 3, 5, 7];
const map1 = array1.map((x) => x * 5);

console.log(map1);
// 結果為 Array [5, 15, 25, 35]
```

### `.filter()`

filter() 方法會建立一個經函式篩選後，符合條件之結果的新陣列。

```javascript
const employeeList = [
  { name: "John", age: 30 },
  { name: "Betty", age: 28 },
  { name: "Candy", age: 25 },
];

const result = employeeList.filter((employee) => employee.age < 30);

console.log(result);
// 結果為 [{name: "Betty", age: 28}, {name: "Candy", age: 25}]
```

### 練習一：使用 `.map` 讓大家的 money 都乘以 5 倍

```javascript
const newMoneyList = moneyList.map((item) => ({
  ...item,
  money: item.money * 5,
}));
console.log("newMoneyList: ", newMoneyList);

// 結果為 [{"name":"John","money":500},{"name":"Tony","money":1500},{"name":"Carter","money":250}]
```

### 練習二：使用 `.filter` 篩選出 newMoneyList 中 money 大於 1000 的資料

```javascript
let filterMoneyList = newMoneyList.filter((item) => {
  return item.money > 1000;
});
console.log("filterMoneyList", filterMoneyList);
// 結果為 [{"name":"Tony","money":1500}]
```
