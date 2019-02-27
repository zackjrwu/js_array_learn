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
* every(functionName) (利用函式來確認陣列內容都符合規則)

    如果陣列全部符合則回傳 **true**，有一個不對就回傳 **false**

    >**注意** : 使用方法後不會改變原先的陣列，若陣列沒有值不會執行。
    ```javascript
        var ages = [18, 19, 29, 26, 21, 24];
        function Adult(age) {
            return age >= 18;
        }
        console.log(ages.every(Adult));  //  true
    ```
* filter(functionName) (利用函式來確認陣列內容都符合規則)

    回傳一個**陣列**，裡面有符合函式規則的元素

    >**注意** : 如果沒有任何一個元素通過則會回傳一個空陣列
    ```javascript
        var ages = [18, 19, 29, 26, 21, 24];
        function Adult(age) {
            return age >= 20;
        }
        console.log(ages.filter(Adult));  //  [ 29, 26, 21, 24 ]
        var ggyy = ages.filter(function (age, index, arr) {
            return age >= 25;
        });
        console.log(ggyy);  //  [ 29, 26 ] is ok
    ```
    