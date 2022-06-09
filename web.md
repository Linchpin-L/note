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
		200: 服务器成功返回请求的数据
		201: 新建或修改数据成功
		202: 一个请求已经进入后台排队（异步任务）
    (三)3XX: 请求重定向;
        301 请求被永久重定向到另一个地址
        302 请求被临时重定向到另一个地址
        304 Not Modified 资源未修改，从本地取缓存
        307 重定向中保持原来的post数据，防止数据库丢失
    (四)4XX: 客户端请求错误;
        401 用户没有权限（用户名或密码错误）;
        403 用户得到授权但访问被禁止
        404 没有找到请求的文件;
        406 请求的格式不可得
        410 请求资源被删除		
        422 创建对象时发生一个验证错误
    (五)5XX: 服务端出现问题;
        500 服务器发生错误，请检查服务器		
        502 网关错误
        503 服务不可用，服务暂时过载或维护		
        504 网关超时

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
4. ref属性

   	ref 被用来给元素或者子组件注册引用信息（id的替代者）
   	应用在html标签上获取的是真实的DOM元素，应用在组件标签上获取的是组件实例对象vc
   	使用方法：
   	       <h1 ref="xxx"></h1> 或者 <school ref="xxx"></school>
   	       获取：this.$refs.xxx
5. props 配置项

       让组件接收外部传过来的数据
        接收数据方式：
           （1）只接收：props:['name','age']
           （2）限制类型：props:{name:String, age:Number}
           （3）限制类型、限制必要性、指定默认值
   		        props: {
   		   		  name: {
   		      		  type: String,	 // 类型
   		      		  required: true,// 必要性
   		      		  default: 'cess'// 默认值
   		          }
   		        }
   	  props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告；若确实需要修改，可以赋值props中的内容到data中，然后去修改data中的数据

6. 编程式路由导航

   	 this.$router.push({}) 内传的对象与<router-link>中的to相同,向history栈添加一个记录，点击后退会返回到上一个页面；
   	 this.$router.replace({}) 跳转到不同的url,但是这个方法不会向history里添加新纪录，点击返回，会跳转到上上一个页面，上一个记录是不存在的；
   	 this.$router.forward() 前进
   	 this.$router.back() 后退
   	 this.$router.go(n) n为正数前进，为负数后退

7. 缓存路由组件

        让不展示的路由组件保持挂载，不被销毁，当我们重新切回来时，还保持着之前的数据，比如，在文本框中输入数据，然后切换到其他页面，再切换到之前的文本框界面，则文本框的数据仍然保存着。
        <keep-alive include="News"> <router-view></router-view></keep-alive> // 缓存一个路由组件
        <keep-alive :include="['News','Message']"> <router-view></router-view></keep-alive> // 缓存多个路由组件
        <keep-alive></keep-alive> // 全部缓存


8.  正则表达式的使用：

	    常用的方法：
	     let str = '123abc456ef' // 需要处理的字符串
	     let regEx = /[a-z]+/
	    （1）查询matches: 用规则匹配整个字符串，只要有一处不符合规则，就匹配结束，返回false ;
	    （2）切割split: 将字符串分割成字符串数组	    
	    （3）替换replaceAll：直接使用，全局匹配，不需要加g修饰符
	           replace: 使用时需要加上g修饰符，否则只会替换第一个
	            例：let res =  str.replace(/regEx/g,"0")
	            console.log(res) //打印结果：12304560
	    （4）search: 检索与正则表达式相匹配的值，返回的是索引或者-1；仅返回一个匹配值的索引，不能全局匹配
	               例：let res = str.search(regEx)
	               console.log(res) //打印结果：  
	    （5）match: 通过字符串查找只能返回第一次匹配到的元素；如果使用了g修饰符，则返回的是字符串中出现的指定字符的所有值的集合，不会有index,input等属性;如果匹配不到，返回null
	               例：let res = str.match(regEx)
	               console.log（res）//打印结果：["abc",index: 3,input: "123abc456ef",groups: undefind]
	               如果使用了g修饰符，则返回如下数组：
	                 ["abc","ef"]
	    （6）test: 用于检测一个字符串是否匹配指定内容，匹配返回true，不匹配返回false
	              例：let res = regEx.test(str)
	               console.log(res) // 打印结果：true
	    （7）exec: 用于检索正则表达式中的匹配，若匹配到返回数组，否则返回null


## 五、overflow
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

## 六、其他常用的操作
### 1. 使用 canvas 合成两张图片
代码

```c
drawAndShareImage(bgsrc, src) {
    // 创建一张画布
    let canvas = document.createElement('canvas');
    // 设置画布的宽和高
    canvas.width = 400;
    canvas.height = 400;
    // 设置画布的绘制环境 2d 绘制
    let context = canvas.getContext('2d');
    // 绘制一个矩形
    context.rect(0, 0, canvas.width, canvas.height);
    // 声明一个 image 对象
    let bgImg = new Image();
    // 设置这个 image 的 src 属性
    bgImg.src = bgsrc;    // 背景图的url
    // Anonymous 如果使用这个值的话就会在请求中的 header 中带上 Orgin 属性
    // 但请求不会带上 cookie 和其他的一些认证信息
    bgImg.crossOrigin = 'Anonymous';
    bgImg.onload = () => {
        // 向画布上绘制图片
        context.drawImage(bgImg, 0, 0, 200, 200);
        let img = new Image();
        img.src = src;    // 需要合进去的图片url
        img.crossOrigin = 'Anonymous';
        img.onload = () => {
            context.drawImage(img, 75, 75, 50, 50);
            let base64 = canvas.toDataURL('image/png');
            console.log(base64); // 这个就是合成后的图片链接
        }
    }
}
```

### 2. vue 使用 qrcode 把链接生成二维码图片
1. 安装qrcode
```c
npm install --save qrcode
```
2. 引入
```c
import qrcode from 'qrcode'
```
3. 使用

```c
let url = await qrcode.toDataURL('需要转化的 url');  // 返回 promise
```

### 3. HTML 中的 link 标签解析
link 标签  是用来链接到外部样式文件的一个标签
|属性| 值 | 描述 |
|--|--|--|
| href | URL | 定义链接文档的位置`
| hreflang| 	language_code | 定义被链接文档中文本的语言
| media| media_query| 规定被链接文档将显示在什么设备上。
| rel| [介绍](https://www.runoob.com/tags/att-link-rel.html) | 必需。定义当前文档与被链接文档之间的关系。rel 是 relationship的英文缩写。
| sizes| HeightxWidth any | 定义了链接属性大小，只对属性 rel="icon" 起作用。
| type| MIME_type | 规定被链接文档的 MIME 类型。
#### （1）记录一次 ssr 项目中为啥引入 css 样式在 ios 中不生效
原代码
```c
link: [
      { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' },
      { rel: 'stylesheet', type: '', href: '/lib/css/bootstrap.min.css'},
      { rel: 'stylesheet', type: '', href: '/lib/css/viewer.min.css'},
    ],
```
这样引入 css 文件 css 文件不生效

	原因：
	因为没有设置 type='text/css'，现在的一些主流浏览器默认会把这些引入的 css 文件加上 type/css， 这就导致 可能在谷歌浏览器上面不加入这个属性， 也能造成 css 文件能够加载成功， 但是这种方式在 ios 苹果手机上面可能失效， 这时要想解决这种情况我们就需要手动加上这个属性

更改完成之后：

```c
link: [
      { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' },
      { rel: 'stylesheet', type: 'text/css', href: '/lib/css/bootstrap.min.css'},
      { rel: 'stylesheet', type: 'text/css', href: '/lib/css/viewer.min.css'},
    ],
```
#### （2）接口传值形式：formData,JSON,   From URL Encode格式的区别

	    （1） formData对应的contentType 的值为：multipart/form-data，不需要单独设置contentType的值，将数据格式改为formData格式即可。
	              formData格式提交的数据为：a=1&b=2&c=3
	           即可以上传文件，也可以上传键值对，它是以键值对的形式上传，因此可以上传多个文件;文件流格式
	    （2）JSON对应的contentType的值为：  application/json，需要手动设置content-type的值；
	           JSON格式提交的数据为：{"a":1,"b":2,"c":3}
	    （3）From URL Encode格式formData,对应的content-type: application/x-www-form-urlencoded,需要手动配置，并且使用
	             qs.stringfy(data)将data转换成url格式，才能正常使用；
	             form表单数据被编码为key/value格式发送到服务器（表单默认的提交数据的格式）

### 4. validate表单验证
#### （1）validate表单验证的作用
	作用就是对输入的数据，立即进行校验，查看是否复合要求
	eg: 用required判断某个输入框是否属于必填字段、判断输入框中的最大输入长度等。
#### （2）使用validate验证：
	a. 使用 validate 需要先引入 jquery.validate.js
	b. 页面加载后对表单进行验证 $("#表单id名").validate({}）
	c. 在validate中的rules中编写验证规则
	 	1. 一个输入框只有一个校验器的时候，可以用字段的name属性:“校验器”；
		2. 输入框需要有多个校验器的时候，可以用字段的name属性:{校验器:值,校验器:值}
	d. 在validate中的messages中编写提示信息
	e. 在validate中的submitHandler中编写验证通过执行的内容
#### （3）验证规则：
| 校验类型 | 取值 | 描述 |
|--|--|--|
|required|true/false|必填字段|
|email|“@”或者”email”|邮件地址|
|url||路径|
|date|数字|日期|
|dateISO|字符串|日期（YYYY-MM-dd）|
|number||数字（负数，小数）|
|digits||整数|
|minlength|数字|最小长度|
|maxlength|数字|最大长度|
|rangelength|[minL,maxL]|长度范围|
|min||最小值|
|max||最大值|
|range|[min,max]|值范围|
|equalTo|jQuery表达式|两个值相同|
|remote|url路径|ajax校验|
#### （4）操作符说明
| 标记 | 标记说明|
|--|--|
| , | 多操作符分割 |
| I | 或操作 |
| -	| 跳过字段验证 |
#### （5）常用标记说明
| 标记 | 标记说明 | 例 |
|--|--|--|
| required | 必填 |	Field或Struct validate:"required" |
| omitempty |	空时忽略 | 	Field或Struct validate:"omitempty" |
| len |	长度 | Field validate:"len=0" |
| eq | 等于 | Field validate:"eq=0" |
| gt | 大于 | Field validate:"gt=0" |
| gte | 大于等于 | Field validate:"gte=0" |
| lt | 小于 | Field validate:"lt=0" |
| lte | 小于等于 | Field validate:"lte=0" |
| eqfield | 同一结构体字段相等 | Field validate:"eqfield=Field2" |
| nefield | 同一结构体字段不相等 | Field validate:"nefield=Field2" |
| gtfield | 大于同一结构体字段 | Field validate:"gtfield=Field2" |
| gtefield | 大于等于同一结构体字段 | Field validate:"gtefield=Field2" |
| ltfield | 小于同一结构体字段 | Field validate:"ltfield=Field2" |
| ltefield | 小于等于同一结构体字段 | Field validate:"ltefield=Field2" |
| eqcsfield | 跨不同结构体字段相等 | Struct1.Field validate:"eqcsfield=Struct2.Field2" |
| necsfield | 跨不同结构体字段不相等 | Struct1.Field validate:"necsfield=Struct2.Field2" |
| gtcsfield | 大于跨不同结构体字段 | Struct1.Field validate:"gtcsfield=Struct2.Field2" |
| gtecsfield | 大于等于跨不同结构体字段 | Struct1.Field validate:"gtecsfield=Struct2.Field2" |
| ltcsfield | 小于跨不同结构体字段 | Struct1.Field validate:"ltcsfield=Struct2.Field2" |
| ltecsfield | 小于等于跨不同结构体字段 | Struct1.Field validate:"ltecsfield=Struct2.Field2" |
| min | 最小值 | Field validate:"min=1" |
| max | 最大值 | Field validate:"max=2" |
| structonly | 仅验证结构体，不验证任何结构体字段 | Struct validate:"structonly" |
| nostructlevel | 不运行任何结构级别的验证 | Struct validate:"nostructlevel" |
| dive | 向下延伸验证，多层向下需要多个dive标记 | [][]string validate:"gt=0,dive,len=1,dive,required" | 
| dive Keys & EndKeys | 与dive同时使用，用于对map对象的键的和值的验证，keys为键，endkeys为值 | map[string]string validate:"gt=0,dive,keys,eq=1|eq=2,endkeys,required" |
| required_with | 其他字段其中一个不为空且当前字段不为空 | Field validate:"required_with=Field1 Field2" |
| required_with_all | 其他所有字段不为空且当前字段不为空 | Field validate:"required_with_all=Field1 Field2" |
| required_without | 其他字段其中一个为空且当前字段不为空 | Field `validate:"required_without=Field1 Field2" |
| required_without_all | 其他所有字段为空且当前字段不为空 | Field validate:"required_without_all=Field1 | Field2" |
| isdefault | 是默认值 | Field validate:"isdefault=0"oneof其中之一Field validate:"oneof=5 7 9"
| containsfield | 字段包含另一个字段 | Field validate:"containsfield=Field2" |
| excludesfield | 字段不包含另一个字段 | Field validate:"excludesfield=Field2" |
| unique | 是否唯一，通常用于切片或结构体 | Field validate:"unique" |
| alphanum | 字符串值是否只包含 ASCII 字母数字字符 | Field validate:"alphanum" |
| alphaunicode | 字符串值是否只包含 unicode 字符 | Field validate:"alphaunicode" |
| alphanumunicode | 字符串值是否只包含 unicode 字母数字字符 | Field validate:"alphanumunicode" |
| numeric | 字符串值是否包含基本的数值 | Field validate:"numeric" |
| hexadecimal | 字符串值是否包含有效的十六进制 | Field validate:"hexadecimal" |
| hexcolor | 字符串值是否包含有效的十六进制颜色 | Field validate:"hexcolor" |
| lowercase | 符串值是否只包含小写字符 | Field validate:"lowercase" |
| uppercase | 符串值是否只包含大写字符 | Field validate:"uppercase" |
| email | 字符串值包含一个有效的电子邮件 | Field validate:"email" |
| json | 字符串值是否为有效的 JSON | Field validate:"json" |
| file | 符串值是否包含有效的文件路径，以及该文件是否存在于计算机上 | Field validate:"file" |
| url | 符串值是否包含有效的 url | Field validate:"url" |
| uri | 符串值是否包含有效的 uri | Field validate:"uri" |
| base64 | 字符串值是否包含有效的 base64值 | Field validate:"base64" |
| contains | 字符串值包含子字符串值 | Field validate:"contains=@" |
| containsany | 字符串值包含子字符串值中的任何字符 | Field validate:"containsany=abc" |
| containsrune | 字符串值包含提供的特殊符号值 | Field validate:"containsrune=☢" |
| excludes | 字符串值不包含子字符串值 | Field validate:"excludes=@" |
| excludesall | 字符串值不包含任何子字符串值 | Field validate:"excludesall=abc" |
| excludesrune | 字符串值不包含提供的特殊符号值 | Field validate:"containsrune=☢" |
| startswith | 字符串以提供的字符串值开始 | Field validate:"startswith=abc" |
| endswith | 字符串以提供的字符串值结束 | Field validate:"endswith=abc" |
| ip | 字符串值是否包含有效的 IP 地址 | Field validate:"ip" |
| ipv4 | 字符串值是否包含有效的 ipv4地址 | Field validate:"ipv4" |
| datetime | 字符串值是否包含有效的 日期 | Field validate:"datetime" |
#### （6）validator默认校验规则
	a. required:true 必输字段
	b. remote:"check.php" 使用ajax方法调用check.php验证输入值
	c. email:true 必须输入正确格式的电子邮件
	d. url:true 必须输入正确格式的网址
	e. date:true 必须输入正确格式的日期
	f. dateISO:true 必须输入正确格式的日期(ISO)，例如：2009-06-23，1998/01/22 只验证格式，不验证有效性
	g. number:true 必须输入合法的数字(负数，小数)
	h. digits:true 必须输入整数
	i. creditcard: 必须输入合法的信用卡号
	j. equalTo:"#field" 输入值必须和#field相同
	k. accept: 输入拥有合法后缀名的字符串（上传文件的后缀）
	l. maxlength:5 输入长度最多是5的字符串(汉字算一个字符)
	m. minlength:10 输入长度最小是10的字符串(汉字算一个字符)
	n. rangelength:[5,10] 输入长度必须介于 5 和 10 之间的字符串")(汉字算一个字符)
	o. range:[5,10] 输入值必须介于 5 和 10 之间
	p. max:5 输入值不能大于5
	q. min:10 输入值不能小于10

### 5. 时间选择器和时间戳

#### （1）时间选择器：
	<input type="date"/>
	可以选择当前日期
#### （2）时间戳：
	获取当前的时间戳：new Date().getTime()
	获取昨天的时间戳：new Date().getTime() - 24*60*60*1000
	获取昨天的十位的时间戳：parseInt((new Date().getTime() - 24*60*60*1000)/1000)

### 6. 模板字符串
	模板字符串使用反引号 (` `) 来代替普通字符串中的用双引号和单引号。模板字符串可以包含特定语法（${expression}）的占位符。占位符中的表达式和周围的文本会一起传递给一个默认函数，该函数负责将所有的部分连接起来，如果一个模板字符串由表达式开头，则该字符串被称为带标签的模板字符串，该表达式通常是一个函数，它会在模板字符串处理后被调用，在输出最终结果前，你都可以通过该函数来对模板字符串进行操作处理。在模版字符串内使用反引号（`）时，需要在它前面加转义符（\）。