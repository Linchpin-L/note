一、浅拷贝与深拷贝
   (一)只针对Object和Array这种数据类型
   (二)区别:
       浅拷贝只复制指向对象的指针，不复制对象本身，旧对象与新对象共存；javaScript对象存储，存储地址，会导致新旧对象指向同一地址；
       深拷贝则是会另外创造一个一摸一样的对象，且与旧对象不共存，因此修改新对象，不会影响旧对象；
       简单来说，A复制B，B改变，A也改变是浅拷贝；否则是深拷贝；
   (三)实现方法：
      1.浅拷贝
      (1)for…in 循环第一层
         for (let i in copyObj) {
           obj[i] = copyObj[i];
         }
      (2)Object.assign(目标对象, 源对象) 返回值：目标对象
         let copyObj = Object.assign({},obj);
      (3)可以直接使用'=' 赋值
      (4)Array.protottype.concat()
         let new_array = old_array.concat(value1[, value2[, ...[, valueN]]])
      (5)Array.protottype.slice()
         let new_array = old_array.slice(0)
      2.深拷贝
      (1) 递归拷贝
      (2) JSON
          将javascript值转为JSON字符串
          let jsonText = JSON.stringify(obj)
          console.log(jsonText);//{"a":1,"b":2}
          把JSON字符串转为javascript值
          let copyObj = JSON.parse(jsonText)
      (3) 函数库lodash的_.cloneDeep方法
          .cloneDeep方法：
            var objects = [{ 'a': 1 }, { 'b': 2 }];
            var deep = _.cloneDeep(objects);
            console.log(deep[0] === objects[0]);
            // => false

二、JS阻止冒泡方法
   问题：当点击div下面包含的按钮时，会触发div事件，造成不太好的使用感，使用阻止冒泡可以解决该情况：
   解决方法：在button的@click.stop=……即可

三、当使用formDiff对比优化时,设置ID不变，但ID又是必传项，可采用如下方法封装接口：
    export const $方法名 = (wordID,data,openID = 0) => new Promise((resolve, reject) => {
      data.WordID = wordID
      $http({
        url: `${$BASE_URL2}/adm/media/image/open/${openID}/word`,
        method: "put",
        data
      }, res => {
        resolve(res)
      }, err => {
        reject(err)
      })
    })

四、可选链操作符(?.)
   允许读取位于连接对象链深处的属性的值，而不必明确验证链中的每个引用是否有效。
   在引用为(null或者undefined)的情况下不会引起错误

五、重复点击，重复走请求的优化方法:
    给数组新添加一个属性,用来存储点击走请求获取到的数据,然后判断这个属性是否为空或者undefind(判断可使用可选链操作符?.)。
    是,则发送请求; 否,不走请求

六、受JavaScript 的限制 (以及废弃 Object.observe),Vue不能检测到对象属性的添加或删除,造成视图不更新的情况,因此需要手动添加或删除:
   (一)最常用的方法: 利用this.$set(this.object,key,value)
        例:this.$set(this.chapter[i], 'sectionList', res.data)
   (二)利用Object.assign({},this.obj)
        例:this.obj.this.chapter[i] = "sectionList";
          this.obj = Object.assign({},this.obj)
   (三)this.obj = Object.assign({ },this.obj,{"this.chapter[i]","sectionList"})
      this.someObject = Object.assign({}, this.someObject, { a: 1, b: 2 }) 赋值多个







