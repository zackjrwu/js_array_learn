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

    >**注意** : 使用方法後不會改變原先的陣列，若陣列沒有值回傳 true ???? 
    ```javascript
        var ages = [18, 19, 29, 26, 21, 24];
        function Adult(age) {
            return age >= 18;
        }
        console.log(ages.every(Adult));  //  true
    ```

* arrayName.some(functionName) (利用函式來確認陣列內容有一個符合規則)

    如果陣列有一個符合則回傳 **true**，全部不對回傳 **false**

    >**注意** : 使用方法後不會改變原先的陣列，若陣列沒有值回傳 **false**。
    ```javascript
        var ages = [18, 9, 2, 6, 1, 4];
        function Adult(age) {
            return age >= 18;
        }
        console.log(ages.some(Adult));  //  true
    ```


* filter(functionName) (利用函式來確認陣列內容符合規則)

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
        console.log(ggyy);  //  [ 29, 26 ] 
    ```

* fill(string_number_var...) (取代陣列所有元素)

    將陣列原有的元素全部替換成括號裡面的資訊
    
    >**注意** : ES6語法，IE11與以下都不支援
    ```javascript
        var fruits = ['apple', 'banana', 'orange', 'kiwi'];
        fruits.fill('kiwi');
        console.log(fruits);  //  [ 'kiwi', 'kiwi', 'kiwi', 'kiwi' ]
    ```

* find(functionName) (找尋陣列的元素)

    找尋陣列所有元素中第一個符合函式規則的元素並回傳，一樣IE11與以下不支援 ~~TMD~~
    
    >**注意** : ES6語法，若空陣列不執行，若陣列沒有元素符合回傳 **undefined**，不改變原始陣列。
    ```javascript
        var ages = [18, 19, 29, 26, 21, 24];
        function Adult(age) {
            return age >= 20;
        }
        var ans = ages.find(Adult);
        console.log(ans);  //  29
    ```

* findIndex(functionName) (找尋陣列中的元素)
    
    找尋陣列所有元素中第一個符合函式規則的元素並回傳他在此陣列中的 **index**，一樣IE11與以下不支援 ~~TMD~~

    >**注意** : ES6語法，若空陣列不執行，若陣列沒有元素符合回傳 **-1**，不改變原始陣列。
    ```javascript
        var ages = [18, 19, 29, 26, 21, 24];
        function Adult(age) {
            return age >= 20;
        }
        var ans = ages.findIndex(Adult);
        console.log(ans);  //  2
    ```

* forEach(functionName) (使陣列執行函式)

    使陣列裡的每個元素都執行一次所給的函式

    >**注意** : 只是單單純陳的執行函式而已，並不回傳任何東西，當陣列沒東西不會執行。
    ```javascript
        var ages = [18, 11, 29, 7, 21, 24];
        var ageCheck = [];
        function isFullAge(age, index) {
            if (age >= 18) {
                ageCheck.push(index + ': ' + age);
            } else
                ageCheck.push(index + ': No');
        }
        ages.forEach(isFullAge);
        console.log(ageCheck);  //  [ '0: 18', '1: No', '2: 29', '3: No', '4: 21', '5: 24' ]
        //  另一個常使用的表示法
        ages.forEach(function (val, index) {
            if (val >= 18)
                console.log(`第${index+1}位成年者是${val}歲`);
            else
                console.log(`第${index+1}位不成年者是${val}歲`);
        });
        /*  第1位成年者是18歲
            第2位不成年者是11歲
            第3位成年者是29歲
            第4位不成年者是7歲
            第5位成年者是21歲
            第6位成年者是24歲  */
    ```
* map(functionName) (讓陣列每個值都使用一次函式)

    把陣列裡的所有元素都使用括號中的函式

    >**注意** : map() 與 forEach() 極為相似，差異是在**回傳**的陣列與否
    
    >**注意** : 當陣列沒有任何元素時不執行函式，函式不改變原有的陣列
    ```javascript
    var ages = [19, 27, 34, 5, 21];
    function addOne(age) {
    return age + 1;
    }
    console.log(ages.map(addOne));  //  [ 20, 28, 35, 6, 22 ]
    ```

* Array.from(string) (把一個字串變成陣列)

    括號中放一個字串或是儲存字串的變數，會把它打散照順序分別儲存到一個陣列中，回傳陣列
    
    >**注意** : ES6語法，IE11與以下都不支援。
    ```javascript
        var strings = 'My name is shit!';
        var arrayFromString = Array.from('happy');
        var arrayFromString2 = Array.from(strings);
        console.log(arrayFromString);  //  [ 'h', 'a', 'p', 'p', 'y' ]
        console.log(arrayFromString.length);  //  5
        console.log(arrayFromString2);  //  [ 'M', 'y', ' ', 'n', 'a', 'm', 'e', ' ', 'i', 's', ' ', 's', 'h', 'i', 't', '!' ]
        console.log(arrayFromString2.length);  //  16
    ```

* join() (把陣列的元素全部組合成一個字串)

    括號中可填字串間格的符號，預設是使用逗點

    ```javascript
        var array = ['miki', 9, 'Joe', 'Zack'];
        console.log(array.join());  //  miki,9,Joe,Zack
        console.log(array.join('|'));  //  miki|9|Joe|Zack
    ```

*  toString() (把陣列或是物件轉成一個字串)
    
    >**注意** : 不會改變原使陣列，型態也會從陣列變成字串
    ```javascript
        var ages = [14, 7, 9, 55, 43, 22, 100, 25];
        var ans = ages.toString();
        console.log(ans);  //  14,7,9,55,43,22,100,25
        console.log(ans.constructor);  //  [Function: String]
        console.log(ages.constructor);  //  [Function: Array]
    ```

* includes() (查找有無在陣列中)

    找尋括號中的值有沒有在陣列中，回傳 **true** 或 **false**
    
    >**注意** : ES7語法，大小寫是敏感的。
    ```javascript
        var array = ['miki', 9, 'Joe', 'Zack'];
        console.log(array.includes(9));  //  true
        console.log(array.includes('9'));  //  false
        console.log(array.includes('Miki'));  //  false
        console.log(array.includes('Joe'));  //  true
    ```

* indexOf() (查找有無在陣列中)

    找尋括號中的值有沒有在陣列中，回傳 **index** 如果不在則回傳 **-1**

    ```javascript
        var array = ['miki', 9, 'Joe', 'Zack'];
        console.log(array.indexOf(9));  //  1
        console.log(array.indexOf('Zack'));  //  3
        console.log(array.indexOf('zack'));  //  -1
    ``` 

* Array.isArray(variable) (判斷是否為陣列)

    判斷括號中的變數是否為陣列，回傳 **true** 或 **false**
    
    ```javascript
        var array = ['miki', 9, 'Joe', 'Zack'];
        var gg = 'bb';
        console.log(Array.isArray(array));  //  true
        console.log(Array.isArray(gg));  //  false
    ```

* arrayName.lastIndexOf(string) (顯示出他的索引)

    判斷括號中的字串在陣列中的索引，從**後面算過來**
    
    >**注意** : 只會顯示出第一個找到的，如果沒有回傳 **-1**
    ```javascript
        var names = ['Miki', 'Zack', 'Ben', 'Mary', 'Zack'];
        console.log(names.lastIndexOf('Zack'));  //  4
        console.log(names.lastIndexOf('Benson'));  //  -1
    ```
* arrayName.pop() (彈出陣列中的最後一個元素)

    把陣列中的最後一個元素取出，原始陣列的最後一個元素就此消失

    ```javascript
        var ages = [19, 27, 34, 5, 21];
        console.log(ages.pop());  //  21
        console.log(ages);  //  [ 19, 27, 34, 5 ]
    ```

* arrayName.shift() (彈出陣列中的第一個元素)

    把陣列中的第一個元素取出，原始陣列的第一個元素就此消失

    >**注意** : 和 pop()極為相似，差異在彈出**第一個**或**最後一個**元素
    ```javascript
        var ages = [19, 27, 34, 5, 21];
        console.log(ages.shift());  //  19
        console.log(ages);  //  [ 27, 34, 5, 21 ]
    ```

* arrayName.push() (推入元素到陣列的最後方)

    >**注意** : 會改變原始的陣列內容
    ```javascript
        var ages = [14, 7, 9, 55, 43, 22, 100, 25];
        ages.push(22);
        console.log(ages);  //  [ 14, 7, 9, 55, 43, 22, 100, 25, 22 ]
    ```

* arrayName.unshift() (推入元素到陣列的最前方)

    >**注意** : 會改變原始的陣列內容
    ```javascript
        var ages = [14, 7, 9, 55, 43, 22, 100, 25];
        ages.unshift(22);
        console.log(ages);  //  [ 22,14, 7, 9, 55, 43, 22, 100, 25 ]
    ```

* arrayName.reduce() (將陣列裡的元素都加總起來)

    這個的好處是在做加總時不用使用到外面的變處做重複存取，**左到右**

    >**注意** : 注意此函數的前兩個參數，第一個是 index 0 的值，第二個是 index 1 的值
    ```javascript
        var ages = [19, 27, 34, 5, 21];
        var ans = ages.reduce(function (total, cur) {
            console.log(total);
            console.log(cur);
            return total += cur;
        });
        console.log(ans);
        //       19             27             46        34 80 5 85 21 106
        // total += ages[0]   ages[1]    total += ages[1]......
    ```

* arrayName.reduceRight() (將陣列裡的元素都加總起來)

    這個的好處是在做加總時不用使用到外面的變處做重複存取，**右到左**

    >**注意** : 注意此函數的前兩個參數，第一個是 index **最後一個** 的值，**第二個是 最後一個減 1** 的值
    ```javascript
        var ages = [19, 27, 34, 5, 21];
        var ans = ages.reduceRight(function (total, cur) {
            console.log(total);
            console.log(cur);
            return total += cur;
        });
        console.log(ans);
        //          21                               5                      26        34 60 27 87 19 106
        // total += ages[最後一個元素]   ages[最後一個元素前 1 個]    total += ages[1]......
    ```

* arrayName.reverse() (把陣列元素的順序從尾到頭顛倒排序放置)

    >**注意** : 這個操作會改變到原始的陣列內容
    ```javascript
        var ages = [19, 27, 34, 5, 21];
        ges.reverse();
        console.log(ages);  //  [ 21, 5, 34, 27, 19 ]
    ```

* arrayName.slice(想要切割的第一個元素 index, 到最後一個切個元素 index (不包括))
  
    >**注意** : 這個操作**不改變**到原始的陣列內容
    ```javascript
        var ages = [19, 27, 34, 5, 21];
        console.log(ages.slice(1, 4));  //  [ 27, 34, 5 ]
        console.log(ages);  //  [ 19, 27, 34, 5, 21 ]
    ```

* arrayName.splice(想要從第幾個元素 index 開始切 (包括), 包括自己要切幾個)
  
    >**注意** : 這個操作**改變**到原始的陣列內容
    ```javascript
        var ages = [19, 27, 34, 5, 21];
        console.log(ages.splice(1, 2));  //  [ 27, 34 ]
        console.log(ages);  //  [ 19, 5, 21 ]
    ```
* arrayName.sort(small,big) (排序字串，做些操作可以排數字)

    >**注意** : 會改變原始的陣列順序
    ```javascript
        var ages = [14, 7, 9, 55, 43, 22, 100, 25];
        //  由於是根據文字排序，所以不做一些操作會壞掉
        console.log(ages.sort());  //  [ 100, 14, 22, 25, 43, 55, 7, 9 ]
        //  小排到大
        ages.sort(function (small, big) {
            return small - big;
        });
        console.log(ages);  //  [ 7, 9, 14, 22, 25, 43, 55, 100 ]  
        console.log(ages[0]);  //  7
        //  大排到小
        ages.sort(function (small, big) {
            return big - small;
        });
        console.log(ages);  //  [ 100, 55, 43, 25, 22, 14, 9, 7 ]
        console.log(ages[0]);  //  100
    ```
  

