# Javascript Tricky Words

1.  syntax parser 語法解析器
2.  lexical environment 詞彙環境
3.  execution context 執行環境
4.  hositing (提升)
5.  single threaded 單執行緒
6.  synchronous execution 同步執行
7.  invocation 調用 呼叫 函數
8.  parentheses 括弧
9.  invoke 呼叫
10. variable environment 變數環境
11. scope chain 範圍鏈
12. conceptual aside 另一個概念
13. dynamic typing 動態型別
14. primitive types 基本型別
15. symbol 符號
16. operators 預算子, addition operators 加法運算子
17. precedence 優先性
18. associativity 相依性
19. operator precedence 運算子優先性
20. coercion 強制型轉
21. first class functions 一級函數
22. anonymous 匿名
23. expression 表達式
24. ** mutate 改變某項東西
25. immutable 無法改變
26. arguments 參數 (the parameters you pass to function)
27. immediately invoked function expression 立即呼叫的函數表示式 (IIFE)
```
(function (name) {
      console.log(name)
    })("shit")
```
28. prototypal inheritance 原型繼承
29. object-oriented 物件導向
30. classical inheritance 經典繼承
31. verbose 冗長
32. reflection 反射
33. function constructions 函數建構子

## Javascript Tips

1. 所有javascript 的變數一開始都被設定為undefined
2. undefined 不是指值還未定義 還是這是javascript 設定的初始值
3. 到執行階段 那一行程式被執行 真的宣告變數 才能使用let
4. javascript 引擎直到執行堆(execution stack)是空的才會看事件序列(event queue)
5. primitive types:undefined, null,boolean,symbol,string,number
6. operators 運算子都是(function)函數
7. functions are also object, it has is own methods & property
  ```
  let c = 1
  console.log(c, "c")
```
7. JSON 全稱 Javascript Object Notation
8. if  是陳述式 不會返回值 if()可塞進表達式來返回值
9. 傳值：(by value ) 
 ```
  var a =3;
  var b;
  b=a; (因是拷貝值過去 所以該b記憶體位址以不依樣)
  a=2;
  console.log(a,b)
  
```
9. 傳參考：(by reference (all objects (including functions ) ) ) 
   把兩個變數名稱指向同一個記憶體位址
 ```
 var c= {greeting:'hi'};
 var d;
 d=c;
  
```
10. immediately invoked function expression 立即呼叫的函數表示式 (IIFE)
```
(function (name) {
      console.log(name)
    })("shit")
```
> * ()
> * execution context (環境)
> * (for the anonymous function)

19. closure 閉包經典題目  
```
var arr = []
    for (var i = 0; i < 3; i++) {
      arr.push(function () {
        //不是在這裡跑console log 沒有真的執行 只是創造那個物件 因為還沒呼叫 但是for loop會繼續跑
        console.log(i)
      })
    }
```
這很簡單，你要搞清楚 for 迴圈的定義

for (var i = 0; i < 9; i++) {

console.log(i);

}

當今天 i 值跑到 8 時，會判斷 i<9，成立的話作

  console.log(i);  //印出8

再來做 i++(此時 i 是 9 了)

i 值跑到 9 時，會判斷 i<9，不成立所以不做

console.log(i); 

但是此時 i 是 9 了喔

而因為閉包特性，如果你不在當下把函式做呼叫的話就真的過去了

等下方在()呼叫時他在自己的空間找不到 i

所以會往外找，此時找到現在的 i 值是 3

所以就

3

3

3

ex2 settimeout 倒數計時其實也是閉包的一種表達式

```
function sayHiLater() {
      var greeting = "Hi"
      setTimeout(function () {
        console.log("greeting")
      }, 3000)
    }

sayHiLater()
```

set timeout 接受一個函數物件，另一個參數就是停止時間

他在範圍鏈上，閉包裡有這個變數

因為閉包 3秒後還是可以取用到greeting

使用到閉包和函數表達式


20. jQuery also uses function expression and first class functions 

```
$("button").click(function(){

})
```

21. callback 就是我執行你 你結束後執行另一個函數(functions)


22. bind 創造任何你呼叫函數的拷貝 無倫什麼物件 該物件就會是this 變數指向的東西
    不像bind 創造函數的拷貝 call 真的會執行它
    
23. apply 方法接受陣列作為參數 而不是一般的東西 這是唯一跟call apply的差別

24. bind 也可將一個設定好得拷貝 然後帶入特定的預設參數

* function currying

```
var person = {
      firstname: "John",
      lastname: "doe",
      getFullName: function () {
        var fullname = this.firstname + "" + this.lastname
        return fullname
      },
      multiplyFn(a, b) {
        console.log(a, b, "ab")
        return a * b
      },
    }
```


```
 function multiply(a, b) {
      console.log(this, "this")
      return this.multiplyFn(a, b)
      // return a * b
    }
    var multipleByTwo = multiply.bind(person, 2, 4)
    console.log(multipleByTwo())
```

* function borrowing 


```
var person2 = {
      firstname: "Jane",
      lastname: "doe",
    }

    console.log(person.getFullName.apply(person2), "person2")
```

25. inheritance 繼承
>     One object get access to the properties and methods of another     project

 
26. 使用`new` 運算子呼叫這個函數 給被this變數設定好的物件 THIS 變數指向new創造的新的空物件記憶體位置 放了new 關鍵字在前面 會改變this和回傳的東西
