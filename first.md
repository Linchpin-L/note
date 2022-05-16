1 cookie的工作流程：
  客户端访问服务器，服务器调用response.addCookie()方法，产生响应时，会产生set-cookie响应头，将cookie文本发送给客户端，客户端会将cookie文本保存起来，当客户端再次请求服务器时，会产生cookie请求头，将之前服务器发送的cookie信息，再发送给服务器，服务器就可以根据cookie信息跟踪客户端的状态。
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
2 三种提取字符串的方法
(1) slice(start, end)
  slice() 提取字符串的某个部分并在新字符串中返回被提取的部分。
该方法设置两个参数：起始索引（开始位置），终止索引（结束位置）。
 eg:
 var str = "Apple, Banana, Mango";
 var res = str.slice(7,13);
 结果是：
 Banana

(2) substring(start, end)
  substring() 类似于 slice()。
  不同之处在于 substring() **无法接受负的索引**。
 eg:
 var str = "Apple, Banana, Mango";
 var res = str.substring(7,13);
 结果是：
 Banana
(3) substr(start, length)
  substr() 类似于 slice()。
  不同之处在于第二个参数**规定被提取部分的长度**。
 eg:
 var str = "Apple, Banana, Mango";
 var res = str.substr(7,6);
 结果是：
 Banana
3 vue生命周期 
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
4 html字符实体
链接：https://www.w3school.com.cn/html/html_entities.asp
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
  ￠分（cent）	&cent;	&#162;
  £	镑（pound）	&pound;	&#163;
  ¥	元（yen）	&yen;	&#165;
  €	欧元（euro）	&euro;	&#8364;
  §	小节	&sect;	&#167;
  ©	版权（copyright）	&copy;	&#169;
  ®	注册商标	&reg;	&#174;
  ™	商标	&trade;	&#8482;
  ×	乘号	&times;	&#215;
  ÷	除号	&divide;	&#247;
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

5 input复选框选中<label></label>中的内容也可以选中
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
  
6 摘抄的方法
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
7 html表单
html表单用于搜索不同类型的用户输入
html表单元素是指不同类型的input元素、复选框、单选按钮、提交按钮等等
类型：
text 定义常规文本输入
radio 定义单选按钮输入（选择多个选择之一）
submit 定义提交按钮（提交表单）
8 git rebase命令
git rebase 命令在另一个分支的基础上重新应用，用于把一个分支的修改合并到当前分支
https://www.yiibai.com/git/git_rebase.html

 