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

