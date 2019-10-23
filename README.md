# 複数のバージョンのjQueryを共存させる方法

## 読み込んだjQueryの優先順位

```Javascript
<script type="text/javascript" src="jquery-1.2.6.min.js"></script>
<script type="text/javascript" src="jquery-1.11.1.min.js."></script>
```

この場合、1.11.1バージョンが優先される。

## 複数のバージョンを共存させる方法
最後に読み込んだバージョンが優先されるので、「noConflict()」を使い、複数のバージョンでも機能するようにします。

```Javascript
<script type="text/javascript" src="jquery-1.2.6.min.js"></script>
<script type="text/javascript" src="jquery-1.11.1.min.js."></script>
<script type="text/javascript">    
var $1111 = $.noConflict(true);
</script>
```
