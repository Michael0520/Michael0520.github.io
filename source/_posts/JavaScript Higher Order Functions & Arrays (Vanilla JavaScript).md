---
title: JavaScript Higher Order Functions & Arrays (Vanilla JavaScript)
description: 紀錄實作 For 迴圈應用
date: 2021-03-01
categories:
- JavaScript
tags: 
- JavaScript
---


# JavaScript Higher Order Functions & Arrays (Vanilla JavaScript)

###### tags: `JS`


# 事前準備:

待會要處理的資料

```javascript=
const companies= [
  {name: "Company One", category: "Finance", start: 1981, end: 2004},
  {name: "Company Two", category: "Retail", start: 1992, end: 2008},
  {name: "Company Three", category: "Auto", start: 1999, end: 2007},
  {name: "Company Four", category: "Retail", start: 1989, end: 2010},
  {name: "Company Five", category: "Technology", start: 2009, end: 2014},
  {name: "Company Six", category: "Finance", start: 1987, end: 2010},
  {name: "Company Seven", category: "Auto", start: 1986, end: 1996},
  {name: "Company Eight", category: "Technology", start: 2011, end: 2016},
  {name: "Company Nine", category: "Retail", start: 1981, end: 1989}
];

const ages = [33, 12, 20, 16, 5, 54, 21, 44, 61, 13, 15, 45, 25, 64, 32];
```

# forEach 逐個印出

## 使用for作範例

```javascript=
 for (let i = 0; i < companies.length; i++) {
     console.log(companies[i]);
 }
```
印出結果:
![](https://i.imgur.com/ebpS8lu.png)


## forEach


* 是一個比較好的方法來跑array的迴圈相較於一般的for迴圈並且不會return東西回來
* 是個比較優雅的方式處理資料

```javascript=

//這邊做的印出每一個物件
companies.forEach(function (company) {
    console.log(company);
})

//當然也可以取用裡面的資料

companies.forEach(function (company) {
    console.log(company.name);
})
```

印出結果:
跟for跑出來的結果一模一樣，但比較淺顯易懂就是使用了一個forEach方法省去了很多複雜的條件
![](https://i.imgur.com/ebpS8lu.png)

取用裡面的name資料印出的結果
![](https://i.imgur.com/6NB9sFX.png)


# filter 篩選功能


## 練習一:

篩選 ages 這個array裡面大於等於21歲的人
![](https://i.imgur.com/YhViXk1.png)



## 使用for作範例


```javascript=
let canDrink = [];

for (let i = 0; i < ages.length; i++) {
    if (ages[i] >= 21) {
        canDrink.push(ages[i]); //使用push把符合條件的人推進去
    }
}
console.log(canDrink);
```

印出結果:
![](https://i.imgur.com/WgyScBp.png)


## filter

```javascript=
const canDrink = ages.filter(function (age) {
    if (age >= 21) {
        return true;
    }

})

console.log(canDrink);
```

甚至使用ES6語法的箭頭函式可以更簡潔:

```javascript=
const canDrink = ages.filter(age => age >= 21);


console.log(canDrink);
```

印出結果:
一樣不需要處理條件式且比較簡潔也不需要而外多使用其他的方法
![](https://i.imgur.com/WgyScBp.png)


## 練習二:

抓出companies資料裡面含有'Retail內容的物件

## 使用ES5的寫法


```javascript=
const retailCompanies = companies.filter(function (company) {
    if (company.category === 'Retail') {
        return true;
    }
});

console.log(retailCompanies);
```

## ES6箭頭函式的寫法

```javascript=
const retailCompanies = companies.filter(company => company.category === 'Retail')


console.log(retailCompanies);
```


印出結果會一樣:
![](https://i.imgur.com/4M3q9Oj.png)


## 練習三:

篩選公司成立時間在1980年代

主要篩選companies 的start區塊作時間上的判斷

```javascript=
const eightiesCompanies = companies.filter(company => (company.start >= 1980 && company.start < 1990))

console.log(eightiesCompanies)
```

印出結果:

![](https://i.imgur.com/x1PBpe5.png)


## 練習四:

篩選出所有成立超過或是等於十年的公司

```javascript=
const lastedTenYears = companies.filter(company => (company.end - company.start >= 10));


console.log(lastedTenYears);
```

印出結果:
![](https://i.imgur.com/zuEWelh.png)



# map 印出資料(新的array)並且操作他們

除了篩選資料之外我們還可以創造新的array從現存的array中
並且對新的array做各種操作


## 練習一:

把所有的公司名稱取出來並放入一個新的array

```javascript=
const companyNames = companies.map(function (company) {
    return company.name
})

console.log(companyNames);
```

印出結果:

一個全新的array包含了公司名稱
![](https://i.imgur.com/gKHMYRC.png)


## 練習二:

可以操作map取得的新array:

放入公司名稱跟年份組成新的arra

```javascript=
const testMap = companies.map(company => `${company.name}[${company.start} - ${company.end}]`)

console.log(testMap);
```

![](https://i.imgur.com/CQ5MNjw.png)



## 練習三:

對map的新array做數字上面的處理

把數字開平方

把數字乘2

把數字開平方後乘2

```javascript=
const agesSquare = ages.map(age => Math.sqrt(age));


console.log(agesSquare);



const agesTimesTwo = ages.map(age => age * 2);

console.log(agesTimesTwo);



// 甚至可以把它們做串接處理
const agesMap = ages
    .map(age => Math.sqrt(age))
    .map(age => age * 2);



console.log(agesMap);

```
印出結果:

開平方
![](https://i.imgur.com/t0Gbuob.png)

乘2
![](https://i.imgur.com/qTnAnZK.png)

開平方後乘2
![](https://i.imgur.com/Siwzx2V.png)


# sort 

如果我們不對sort做任何處理的話會這樣安排:

```javascript=
const sortedAges = ages.sort();

console.log(sortedAges);
```

看似是由大到小但是有個小問題在於其實只比較了第一個數字然後再比較第二位所以5竟然排在那麼下面顯然不太合理(對一般使用的情況下)
![](https://i.imgur.com/qXvWpx0.png)


## 一般我們會這樣處理sort:

讓順序由大排到小

```javascript=
const sortedAges = ages.sort((a,b) => a-b);

console.log(sortedAges);
```


由小排到大

```javascript=
const sortedAges = ages.sort((a,b) => b-a);

console.log(sortedAges);
```






## 練習一:
分類公司藉著他們的開始年分 最早排到最晚

一次比較兩個公司如果a>b 則顯示-1排前面

```javascript=
const sortedCompanies = companies.sort((a, b) => (a.start > b.start ? 1 : -1));

console.log(sortedCompanies);
```

印出的結果:
![](https://i.imgur.com/5OueGVc.png)




# reduce

作加總，記得寫法reduce(參數1,參數2){function(){},0}後面的0要記得寫


## 練習一:
加總ages所有的數字和

## 使用for範例

```javascript=
let ageSum = 0;
for (let i = 0; i < ages.length; i++) {
    ageSum += ages[i];
}

console.log(ageSum);
```

得出加總的數字為:460

## 使用reduce

## Es5語法:

```javascript=
const ageSum = ages.reduce(function (total, age) {
    return total + age;
}, 0);


console.log(ageSum);
```

得出加總的數字為:460

## ES6語法:

```javascript=
const ageSum = ages.reduce((total, age) => total + age, 0);


console.log(ageSum);
```

得出加總的數字為:460


## 練習二:

加總所有公司的存在年分

把公司的end年份減去start年份就是存在時間並且做加上total就好瞜

```javascript=
const totalYears = companies.reduce(function (total, company) {
    return total + (company.end - company.start);
}, 0);
console.log(totalYears);


//使用ES6的簡化寫法

const totalYears = companies.reduce((total, company) =>
    total + (company.end - company.start), 0);

console.log(totalYears);

```

得出結果: 119




# 串接使用全部方法

不是很實用但是他們可以這樣串接使用


```javascript=
const combined = ages
    .map(age => age * 2)
    .filter(age => age >= 40)
    .sort((a, b) => a - b)
    .reduce((a, b) => a + b, 0);

console.log(combined);
```

由大到小排列:
![](https://i.imgur.com/1zQSVkn.png)


得到加總結果結果是798