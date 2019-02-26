# JS 陣列(Array)使用說明
## 自有屬性:
* constructor (回傳此變數屬性)
    ```javascript
    var g = 10;
    var names = ['Zack', 'Peter', 'Mary'];
    console.log(names.constructor);  // [Function: Array]
    console.log(g.constructor);  // [Function: Number]
    ```
* length (回傳此陣列變數的元素個數)
    ```javascript
    var names = ['Zack', 'Peter', 'Mary'];
    console.log(names.length);  //  3
    ```
* prototype (可對於當下變數的屬性自定義函式)
    ```javascript
    Array.prototype.myUcase = function () {
    return this.length;
    };
    console.log(names.myUcase());  //  3  
    ```
## 可用方法:
* concat(array1,array2...) (使兩個或**以上**陣列合而為一)

    括號裡面放要接在當下陣列後方的陣列變數名稱。

	>**注意** : 使用方法後並不會改變原先的陣列
    ```javascript
    var names  = ['Zack', 'Peter', 'Mary'];
    var fruits = ['banana', 'kiwi', 'apple'];
    console.log(names.concat(fruits));    //  [ 'Zack', 'Peter', 'Mary', 'banana', 'kiwi', 'apple' ]
    console.log(names);    //  ['Zack', 'Peter', 'Mary']
    console.log(fruits);    //  ['banana', 'kiwi', 'apple'] 
    ```
* copyWithin(R_target, O_default_0, O_default_array_length ) (複製陣列元素)
  
	(覆蓋原本陣列的那個 index, 從哪個 index 開始, 從哪個 index 結束)

	>**注意** : 使用方法後會改變原先的陣列，ES6新增。
	```javascript
    var names  = ['Zack', 'Peter', 'Mary'];
	names.copyWithin(1,0);
	consoel.log(names);  //  [ 'Zack', 'Zack', 'Peter' ]
    ```