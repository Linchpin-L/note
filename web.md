## 对数据进行的 base64 的编码以及解码
### 1.  对于没有 UTF-8 字符集的数据
```c
	window.btoa("需要编码的数据"); // 编码
	window.atob("需要解码的数据"); // 解码
```
### 2. 对于包含 UTF-8 字符集的数据、
如果需要编码的数据中 包含 utf-8那么直接使用上述的方法 会报错

```c
Failed to execute 'btoa' on 'Window': The string to be encoded contains characters outside of the Latin1 range
```

需要使用下面的方法进行进一步的处理

```c
	window.btoa(unescape(encodeURIComponent("需要编码的数据"))) // 编码
	decodeURIComponent(escape(window.atob("需要解码的数据"))); // 解码
```


## 在这里开始整理 web 开发相关的知识点
## 一、http状态码
    (一)1XX:接到请求，继续处理;
    (二)2XX: 请求成功;
    (三)3XX: 请求重定向;
        301 请求被永久重定向到另一个地址
        302 请求被临时重定向到另一个地址
        304 Not Modified 资源未修改，从本地取缓存
        307 重定向中保持原来的post数据，防止数据库丢失
    (四)4XX: 客户端请求错误;
        404 没有找到请求的文件;
        403 客户端访问错误;
    (五)5XX: 服务端出现问题;

## 二、位运算符

 1.逻辑位运算符(&,|,^,~)
 
    十进制转二进制:
					       1: 0000 0001;
					       2: 0000 0010;
					       3: 0000 0011;
					       4: 0000 0100;
      **与运算(&): 只有1&1 = 1; 其他情况均为0**
      	  例： 1&2=0 (0000 0000); 1&3=1 (0000 0001); 2&3=10(二进制) => 2(十进制); (0000 0010)
      **或运算(|):只有0|0 = 0；其他情况均为1**
    	  例： 1|2=11(二进制) => 3(十进制) (0000 0011); 
      **异或运算(^): 只有0^1=1，其他情况均为0**
    	  例： 1^2=11(二进制) => 3(十进制) （0000 0011); 2^3=1(0000 0001)
      **取反(~): 用于对一个二进制数计算**
	      ~1：1111 1110 
	      ~0： 1111 1111 值为-1（有符号为-1，无符号为无穷大）
      而在数据中使用字节，则是为了避免浪费；1个字节最小为8位；每一位可以用来存储一种情况：
        例如：1234 5678 (事件8：表示性别：0、1;事件7：表示地址：0、1；……)
        与运算则是用来判断，结果只有两种情况，0或1；判断谁就和它所在的那一位转换成十进制数相与
        比如：判断事件5，则让事件5的值和8相与，得出结果；
             判断事件4，则让事件4的值和16相与，得出结果；
             ……以此类推

2.位移位运算（<< ,>>）

	   左移位运算(<<)
	     3<<2: 3 => 0000 0011 左移2： 0000 1100（将高位的两个移除，其余左移；低位空出的补0），结果为：12
	     右移位运算(>>)
	     5>>2：5 => 0000 0101 右移2： 0000 0001 （将低位移除两位，其余右移，高位补0）， 结果为：1

## 三、JS知识
 1. return
 
	    函数都是有返回值的，如果有return，返回return后面的值，如果没有return,返回undefind；并且，return只能返回一个值，多个用逗号隔开的值，默认返回最后一个。
	   
 2. arguments

		可以用来获取传递了多少个参数，它是函数的一个内置对象，展示形式是一个伪数组（特点：具有length属性；按数据索引存储；不具有数组方法）

 3. Math对象

		   Math.floor() 向下取整
		   Math.ceil() 向上取整
		   Math.round() 四舍五入，就近取整，-3.5，取整结果为 -3；3.5,取整结果为4
		   Math.abs() 绝对值
		   Math.max() Math.min() 求最大、小值
		  
 4. 判断对象类型

		   instanceof ： obj instanceof Array // 返回值为true/false
		   Array. isArray(): Array.isArray(obj)   //判断是否为数组 ,返回值为true/false
		   
 5.  数组
	 
		  添加删除：
	 
			  obj.push(): 末尾添加一个或多个元素； 返回新的长度
			  obj.unshift(): 开头添加一个或多个元素；返回新的长度
			  pop(): 删除数组最后一个元素；返回删除的元素值
			  shift(): 删除数组第一个元素；返回第一个元素
			  
		  排序：
	 
	          sort(): 对数组元素进行排序；返回新数组
				  例： arr.sort(function(a,b) { 
	                     return b - a;  //降序的排列
	                     return a - b; //升序
			 			}
			  reverse(): 颠倒数组中的元素顺序；返回新数组
				  
		  数组去重：
	 
			   遍历旧数组，元素放入新数组，利用indexOf方法判断，新数组中是否存在该元素，返回值为-1，代表不存在，放入
			   方法： 新数组.indexOf(数组元素)
			       
		  数组转成字符串：
	 
			   toString(): 逗号分隔每一项，返回一个字符串
			   join('分隔符'): 用分隔符将每一项分隔
			   
		  连接两个数组或多个数组
	 
			   concat(): 不影响原数组，返回新数组
			   语法：array1.concat(array2, array3, ..., arrayX)
			   
 6. 字符串
 
		   concat(): 拼接字符串;
		   substr(star,length): length代表取得个数；
		   slice(start,end): 截取位置；
		   substring(start，end): 基本和slice相同，但不接受负； 
		   replace(被替换字符，要替换为的字符串): 只会替换字符串中遇到的第一个字符
		   **将字符串转换成数组**
		       split('分隔符‘) // 数组转换成字符串用join
		       
 7. DOM：文档对象模型

		 获取页面元素的方法：
		      通过ID：doucument.getElementByld('id名');
		      通过标签名：doucument.getElementsByTagName('标签名');返回带有指定标签名的对象集合；
		      通过类名：document.getElementsByClassName('类名'); （H5新增）
		      通过指定选择器，返回第一个元素对象：document.querySelector('选择器'); 
		        例：document.querySelector(’#box');
		      通过指定选择器，返回所有元素对象：document.querySelectorAll('选择器');
		      
		自定义属性：
		    获取自定义的属性：element.getAttribute('属性')
		    设置内置属性值：element.属性 = ‘值’
		    主要设置自定义属性： element.setAttribute('属性'，‘值’)；
		    移除属性：element.removeAttribute('属性')；

 8. BOM：浏览器对象模型
		
		  window对象的常见事件：
		       window.onload：窗口页面加载事件，它是等页面全部加载完成（包括图片和样式），才会触发；一个页面只能写一个，写多个的话，只执行最后一个；
		       document.addEventListener('DOMContentLoaded',function(){})：窗口页面加载，仅当DOM加载完成就会触发，一个页面可以使用多次；适用于图片多的页面
		       
		  调整窗口大小事件：
		       window.onresize = function() {}
		       window.addEventListener('resize',function(){}); // 只要窗口发生变化，就会触发该事件，通常用来完成响应式布局
		       
		  设置定时器
		     window.setTimeout(调用函数,[延迟的毫秒数]); // 延迟毫秒数默认为0
		     window.setInterval(回调函数,[间隔的毫秒数]);
		     
		  清除定时器 
		     window.clearTimeout(timeoutID)  //用于停止setTimeout设置的定时器
		     window.clearInterval ( ) //用于停止setInterval设置的定时器
          location对象属性
	          location.href 跳转页面
	          location.search 返回参数
          location对象方法
         	  location.assign() 重定向页面
         	  location.replace() 替换当前页面，且不能退回之前的页面
         	  location.reload() 重新加载页面，相当于强制刷新
          navigator对象：包含有关浏览器的信息
              userAgent属性：可以返回由客户机发送服务器的user-agent头部的值，进而判断用户是pc端登录还是移动端登录
          history对象：与浏览器中访问过的URL历史记录，进行交互
              back(): 后退
              forward(): 前进
              go(参数)：前进、后退都可；前进时，参数为1；后退为-1

## 四、Vue
1.事件修饰符

    prevent: 组织默认事件
    stop: 阻止事件冒泡
    once: 事件只触发一次
    capture: 使用事件的捕获模式
    self: 只有event.target是当前操作的元素时才触发事件
    passive: 事件的默认行为立即执行，无需等待事件回调执行完毕
    还可以连续使用：@click.prevent.stop = "showInfo"

2.绑定样式：

    ：class="xxx",xxx可以是字符串、数组、对象
    ：style="{fontSize: xxx}"
    字符串写法适用于：类名不确定，要动态获取
    数组写法适用于： 要绑定多个样式，个数不确定，名字也不确定
    对象写法是用于： 要绑定多个样式，个数确定，名字也确定，但不确定用不用

3.vue-cli 本地存储

    浏览器通过window.sessionStrorage和window.localStorage属性实现本地存储机制
    setItem('key','value') 该方法接收一个键和值作为参数，会把键值对添加到存储中，若键名存在，则更新其对应的值
    getItem('key') 该方法接收一个键名作为参数，返回键值；如果获取不到key,会返回null
    removeItem('key') 该方法接受一个键名作为参数，并把该键名从存储中删除
    clear() 该方法会清空存储中的所有数据
   
    sessionStorage: 存储的内容会随着浏览窗口关闭而消失
    LocalStorage: 存储的内容，需要手动清除才会消失


## overflow
CSS属性 overflow 定义当一个元素的内容太大而无法适应 块级格式化上下文 时候该做什么
#### 1. 属性
**overflow: visible** 默认值。内容不会被修剪，会呈现在元素框之外
**overflow: hidden** 内容会被修剪，并且其余内容不可见
**overflow: scroll** 内容会被修剪，浏览器会显示滚动条以便查看其余内容
**overflow: auto** 由浏览器定夺，如果内容被修剪，就会显示滚动条
**overflow: inherit** 规定从父元素继承overflow属性的值

#### 2. 扩展
**overflow-x overflow-y** 就是针对于元素的 x 轴和 y 轴 可以单独进行设置

[MDN overflow ](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow)
