    # array

    不管是在面试中还是在笔试中，我们都会被经常问到关于javascript数组的一些算法，比方说数组去重、数组求交集、数组扰乱等等。

    今天抽点时间把javascript中的一些常用的数组算法做一下总结，以方便大家面试笔试或者日常开发过程中用到。其中部分算法来自网络，这里做了下汇总整理。文章末尾我会把参考的来源附上去，如果直接看算法比较枯燥的可以到参考文献里去看，讲解的非常不错。

    一、数组去重

    方法1:

    //利用数组的indexOf方法
    function unique (arr) {
      var result = []; 
      for (var i = 0; i < arr.length; i++)
      {
        if (result.indexOf(arr[i]) == -1) result.push(arr[i]);
      }
      return result;
    }
    方法2：

    //利用hash表,可能会出现字符串和数字一样的话出错，如var a = [1, 2, 3, 4, '3', 5],会返回[1, 2, 3, 4, 5]
    function unique (arr)
    {
        var hash = {},result = []; 
        for(var i = 0; i < arr.length; i++)
        {
            if (!hash[arr[i]]) 
            {
                hash[arr[i]] = true; 
                result.push(arr[i]); 
            }
        }
        return result;
    }
    方法3：

    //排序后比较相邻，如果一样则放弃，否则加入到result。会出现与方法2一样的问题，如果数组中存在1,1,'1'这样的情况，则会排错
    function unique (arr) {
        arr.sort();
        var result=[arr[0]];
        for(var i = 1; i < arr.length; i++){
            if( arr[i] !== arr[i-1]) {
                result.push(arr[i]);
            }
        }
        return result;
    }
    方法4：

    //最简单但是效率最低的算法,也不会出现方法2和方法3出现的bug
    function unique (arr) {
        if(arr.length == 0) return;
        var result = [arr[0]], isRepeate;
        for( var i = 0, j = arr.length; i < j; i++ ){
            isRepeate = false;
            for( var k = 0, h = result.length; k < h; k++){
                if(result[k] === arr[i]){
                    isRepeate = true;
                    break;
                }
                if(k == h) break;
            }
            if( !isRepeate ) result.push(arr[i]);
        }
        return result;
    }
    方法5：

    //此方法充分利用了递归和indexOf方法，感谢网友@真爱像深蓝
    var unique = function (arr, newArr) {
         var num;

         if (-1 == arr.indexOf(num = arr.shift())) newArr.push(num);

         arr.length && unique(arr, newArr);
    }
    二、数组顺序扰乱

    方法1：

    //每次随机抽一个数并移动到新数组中
    function shuffle(array) {
        var copy = [],
            n = array.length,
            i;
        // 如果还剩有元素则继续。。。
        while (n) {
            // 随机抽取一个元素
            i = Math.floor(Math.random() * array.length);
            // 如果这个元素之前没有被选中过。。
            if (i in array) {
                copy.push(array[i]);
                delete array[i];
                n--;
            }
        }
    方法2：

    //跟方法1类似，只不过通过splice来去掉原数组已选项
    function shuffle(array) {
        var copy = [],
            n = array.length,
            i;
        // 如果还剩有元素。。
        while (n) {
            // 随机选取一个元素
            i = Math.floor(Math.random() * n--);
            // 移动到新数组中
            copy.push(array.splice(i, 1)[0]);
        }
        return copy;
    }
    方法3：

    //前面随机抽数依次跟末尾的数交换，后面依次前移，即：第一次前n个数随机抽一个跟第n个交换，第二次前n-1个数跟第n-1个交换，依次类推。
    function shuffle(array) {
        var m = array.length,
            t, i;
        // 如果还剩有元素…
        while (m) {
            // 随机选取一个元素…
            i = Math.floor(Math.random() * m--);
            // 与当前元素进行交换
            t = array[m];
            array[m] = array[i];
            array[i] = t;
        }
        return array;
    }
    三、数组判断

    方法1：

    1 //自带的isArray方法
    2 var array6 = [];
    3 Array.isArray(array6 );//true
    方法2：

    1 //利用instanceof运算符
    2 var array5 = [];
    3 array5 instanceof Array;//true
    方法3：

    1 //利用toString的返回值
    2 function isArray(o) {
    3     return Object.prototype.toString.call(o) === ‘[object Array]‘;
    4 }
    四、数组求交集

    方法1：

    1 //利用filter和数组自带的indexOf方法
    2 array1.filter(function(n) {
    3     return array2.indexOf(n) != -1
    4 });
    五、数组求并集

    方法1：

    //方法原理：连接两个数组并去重
    function arrayUnique(array) {
        var a = array.concat();
        for(var i=0; i<a.length; ++i) {
            for(var j=i+1; j<a.length; ++j) {
                if(a[i] === a[j])
                    a.splice(j--, 1);

     - 列表项

            }
        }

        return a;
    };
    六、数组求差集

    方法1：

    1 //利用filter和indexOf方法
    2 Array.prototype.diff = function(a) {
    3     return this.filter(function(i) {return a.indexOf(i) < 0;});
    4 };
    暂时汇总了这点儿，有待后续补充。欢迎大家补充。

    参考：

    高效率去掉js数组中重复项
    js数组去重
    由乱序播放说开了去-数组的打乱算法Fisher–Yates Shuffle
    How to randomize (shuffle) a JavaScript array?
    Simplest code for array intersection in javascript


    作者： IT程序狮 

    链接：https://www.imooc.com/article/3219

    来源：慕课网

