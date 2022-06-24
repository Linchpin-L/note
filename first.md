###1 cookie的工作流程：
```c
客户端访问服务器，服务器调用response.addCookie()方法，产生响应时，会产生set-cookie响应头，将cookie文本发送给客户端，客户端会将cookie文本保存起来，当客户端再次请求服务器时，会产生cookie请求头，将之前服务器发送的cookie信息，再发送给服务器，服务器就可以根据cookie信息跟踪客户端的状态。
```
    eg:从cookie中获取userId
    export const $getUserId = () => {
     if (document.cookie && document.cookie !== '') {
    let cookies = document.cookie.split(';');
    for (let i = 0; i < cookies.length; i++) {
      let cookie = decodeURIComponent(cookies[i]).trim().split("=");
      if (cookie.length === 3 && cookie[0] === 'ZM') {
        return cookie[2]
      }
    }
    }
     return null
    }
trim()移除字符串两侧的空白字符
###2 三种提取字符串的方法
```c
1. slice(start, end)
  slice() 提取字符串的某个部分并在新字符串中返回被提取的部分。
该方法设置两个参数：起始索引（开始位置），终止索引（结束位置）。
 eg:
 var str = "Apple, Banana, Mango";
 var res = str.slice(7,13);
 结果是：
 Banana

2. substring(start, end)
  substring() 类似于 slice()。
  不同之处在于 substring() **无法接受负的索引**。
 eg:
 var str = "Apple, Banana, Mango";
 var res = str.substring(7,13);
 结果是：
 Banana
3. substr(start, length)
  substr() 类似于 slice()。
  不同之处在于第二个参数**规定被提取部分的长度**。
 eg:
 var str = "Apple, Banana, Mango";
 var res = str.substr(7,6);
 结果是：
 Banana
```
###3 vue生命周期
    beforeCreate( 创建前 )
    在实例初始化之后，数据观测和事件配置之前被调用，此时组件的选项对象还未创建，el 和 data 并未初始化，因此无法访问methods， data， computed等上的方法和数据。
    created ( 创建后 ）
    实例已经创建完成之后被调用，在这一步，实例已完成以下配置：数据观测、属性和方法的运算，watch/event事件回调，完成了data 数据的初始化，el没有。 然而，挂在阶段还没有开始, $el属性目前不可见，这是一个常用的生命周期，因为你可以调用methods中的方法，改变data中的数据，并且修改可以通过vue的响应式绑定体现在页面上，，获取computed中的计算属性等等，通常我们可以在这里对实例进行预处理，也有一些童鞋喜欢在这里发ajax请求，值得注意的是，这个周期中是没有什么方法来对实例化过程进行拦截的，因此假如有某些数据必须获取才允许进入页面的话，并不适合在这个方法发请求，建议在组件路由钩子beforeRouteEnter中完成
    beforeMount
    挂载开始之前被调用，相关的render函数首次被调用（虚拟DOM），实例已完成以下的配置： 编译模板，把data里面的数据和模板生成html，完成了el和data 初始化，注意此时还没有挂在html到页面上。
    mounted
    挂载完成，也就是模板中的HTML渲染到HTML页面中，此时一般可以做一些ajax操作，mounted只会执行一次。
    beforeUpdate
    在数据更新之前被调用，发生在虚拟DOM重新渲染和打补丁之前，可以在该钩子中进一步地更改状态，不会触发附加地重渲染过程
    updated（更新后）
    在由于数据更改导致地虚拟DOM重新渲染和打补丁只会调用，调用时，组件DOM已经更新，所以可以执行依赖于DOM的操作，然后在大多是情况下，应该避免在此期间更改状态，因为这可能会导致更新无限循环，该钩子在服务器端渲染期间不被调用
    beforeDestroy（销毁前）
    在实例销毁之前调用，实例仍然完全可用，这一步还可以用this来获取实例，一般在这一步做一些重置的操作，比如清除掉组件中的定时器 和 监听的dom事件
    destroyed（销毁后）
    在实例销毁之后调用，调用后，所以的事件监听器会被移出，所有的子实例也会被销毁，该钩子在服务器端渲染期间不被调用
###4 html字符实体
[html字符实体更多请看链接](https://www.w3school.com.cn/html/html_entities.asp)
```c
  html中的预留字符必须被替换为字符实体
  在html当中不能使用小于号（<）和大于号（>），因为浏览器会误认为他们是标签
  如果希望正确地显示预留字符，我们必须在html源代码中使用字符实体
  html中有用的字符实体
  **html**实体名称对大小写敏感
  显示结果	描述	实体名称	实体编号
   	空格 	&nbsp; &#160;
  <	小于号	&lt;	&#60;
  >	大于号	&gt;	&#62;
  &	和号  	&amp;	&#38;
  "	引号	    &quot;	&#34;
  '	撇号 	&apos; (IE不支持)	&#39;
const matchList  = {
  '&lt;': '<',
  '&gt;': '>',
  '&amp;': '&',
  '&#34;': '"',
  '&quot;': '"',
  '&#39;': "'",
  '&nbsp;': " ",
}
// 字符过滤器
let regStr = '(' + Object.keys(matchList).toString() + ')'
// ↑ ------------【*提取匹配列表key值*】.【组数转字符串】
regStr = regStr.replace(/,/g, ')|(')
// ↑ 通过匹配将其更新为正则的字符串类型
const regExp = new RegExp(regStr, 'g')
return text.replace(regExp, match => matchList[match])
// ↑ ------ 替换方法 (正则, 当前key => 返回当前被匹配的key值)
```
###5 input复选框选中的内容也可以选中
```c
<div v-for="(item, i) in selected" :key="i">
 <input type=checkbox v-model="item.active" :id="`form${item.id}`">
 <label :for="`form${item.id}`">{{item.title}}</label>
</div>
需要for一下 但要是数组性的渲染 需要转为动态的
**data中声明一下**

 selected: [{
                 title: '删除选项的前两个字符',
                 active: false,
                 id: 1,
               },
               {
                 title: '恢复转义字符（如 $nbsp; 到 空格）',
                 active: false,
                 id: 2
               },
               {
                 title: '移除题干和选项的html标签',
                 active: false,
                 id: 3
               }
    ],
  ```
###6 摘抄的方法
```c
// 删除 html 标签
let deleteHtmlTag = (content) => {
    try {
        return content.replace(/<.*?>/ig, '')
    } catch (e) {
        return content
    }
}

// 删除选项上多余的东西
let deleteOptionRed = (content) => {
    const arr = ['A.', 'B.', 'C.', 'D.', 'E.', 'F.', 'G.', 'H.', 'I.', 'J.', 'K.', 'L.', 'M.', 'N.']
    for (let i in arr) {
        if (content.indexOf(arr[i]) !== -1) {
            return content.replace(arr[i], '')
        }
    }
}
  // 删除选项A.B.C.D.E.
    deleteOptionRed (content) {
      let temp = content.substring(0,2)
      for (let i in arr) {
        if (arr[i]===temp) {
          return content.slice(2)
        }
      }
      return content
    },
// 过滤选项上多余的转义字符
let htmlFilter = (text) => {
    // 抽离成可配置的匹配列表
    const matchList  = {
        '&lt;': '<',
        '&gt;': '>',
        '&amp;': '&',
        '&#34;': '"',
        '&quot;': '"',
        '&#39;': "'",
        '&nbsp;': "",
    }
    // 字符过滤器
    let regStr = '(' + Object.keys(matchList).toString() + ')'
    // ↑ ------------【*提取匹配列表key值*】.【组数转字符串】
    regStr = regStr.replace(/,/g, ')|(')
    // ↑ 通过匹配将其更新为正则的字符串类型
    const regExp = new RegExp(regStr, 'g')
    // ↑ ------- 字符串 转 正则 方法
    return text.replace(regExp, match => matchList[match])
    // ↑ ------ 替换方法 (正则, 当前key => 返回当前被匹配的key值)
}
```
###7 html表单
```c
html表单用于搜索不同类型的用户输入
html表单元素是指不同类型的input元素、复选框、单选按钮、提交按钮等等
类型：
text 定义常规文本输入
radio 定义单选按钮输入（选择多个选择之一）
submit 定义提交按钮（提交表单）
```
###8 git rebase命令
```c
git rebase 命令在另一个分支的基础上重新应用，用于把一个分支的修改合并到当前分支
```
[git rebase命令](https://www.yiibai.com/git/git_rebase.html)
###9 Number.isSafeInteger 方法使用
```c
    Number.isSafeInteger 方法确定所提供的值是否为安全整数。
安全整数是指：
    可以精确地表示为 IEEE-754 双精度数，并且
    其 IEEE-754 表示不能是对任何其他整数进行四舍五入以适合 IEEE-754 表示的结果。
    508/2000 
    例如，2 ^ 53-1是一个安全的整数: 它可以被精确表示，并且在任何 ieee-754四舍五入模式下都不会有其他整数舍入。
    相比之下，2 ^ 53不是一个安全的整数: 它可以在 ieee-754中精确表示，但是整数2 ^ 53 + 1不能直接在 ieee-754中表示，
    而是在四舍五入和四舍五入下四舍五入到2 ^ 53。
    安全整数由-(2 ^ 53-1)至2 ^ 53-1(± 9007199254740991)或 ± 9,007,199,254,740,991)的所有整数组成。
 javaScript:
    对于整数，根据ECMAScript标准的要求(地址)，JavaScript能表示并进行精确算术运算的整数范围为：
    正负2的53次方，也即从最小值-9007199254740992到最大值+9007199254740992之间的范围；
    对于超过这个范围的整数，JavaScript依旧可以进行运算，但却不保证运算结果的精度。
    值得注意的是，对于整数的位运算（比如移位等操作），JavaScript仅支持32位整型数，也即从-2147483648到+2147483647之间的整数。
    当整数值超出-9007199254740992到9007199254740992的范围时，不用运算也会发生偏差;
 Math.pow(底数x,指数y)
    math.pow(2,53) = 2的53次方
    1.如果底数 x 为负数并且指数 y 不是整数，将会返回NaN。
    2.如果底数 x 是 0，指数 y 是负数，将会返回Infinity (无穷)。
    3.如果返回值太大，将会返回Infinity (无穷)。
```
###10 数组的增删改查
```c
js 数组的添加和删除
      js中数组元素常用添加方法是直接添加、push方法以及unshift方法
      删除方法则是delete、pop、shift及修改方法为一身的则是splice
1、添加：
　　　(1)直接添加通常都是这样
　　　　var arr=[];arr[0]="first";arr[1]="second";
　　　(2)push
　　　　push方法就是将要添加的元素添加到数组的**末尾**，数组长度+1
　　　　var arr=["first","second"];　　//arr.length=2
　　　　arr.push("last");//　　arr→["first","second","last"]　　　　arr.length=3
　　　(3)unshift
　　　　unshift方法就是将要添加的元素添加到**数组头部**，并将其他元素一次移到更高的索引处
　　　　var arr=["first","second"];　　//arr.length=2
　　　　arr.unshift("last");//　　arr→["last","first","second"]　　　　arr.length=3
2、删除
　　  (1)delete
　   　var arr=["first","second","last"];
　　  delete arr[0];//arr→[undefined,"second","last"],arr.length=3;
　   　**并未完全达到删除目的**
　　  (2)pop
　   　pop方法是与push对应的，**删除最后一个元素**，数组长度-1
　　  var arr=["first","second","last"];
　　  arr.pop();//arr→["first","second"],arr.length=2;
　   　(3)shift
　   　与unshift对应，删除第一个元素，数组长度-1，其他元素索引均-1
3、splice
　   　splice方法是修改方法，具有添加和删除功能
　　  splice()的前两参数指定了需要删除的数组元素，紧随其后任意多个参数指定需要插入到数组的元素，
        以至于splice可以实现添加、删除和修改功能。实际上不是修改，只是先删除一个元素再把后面插入的元素插入到那个位置。
　　  _添加：_
　　  var arr=[1,2,3,4,5];
　　  arr.splice(2,0,"change");//arr→[1,2,"change",3,4,5]
　　  参数2代表索引值，参数0代表要改变的元素个数，最后一个参数代表要添加或者替换进去的元素。
　   　_删除_
　   　arr.splice(2,1);//arr→[1,2,4,5]　　当然，也可以删除多个，修改第二个参数即可
```
###11小图标链接
[小图标](https://fontawesome.dashgame.com/)
###12
 