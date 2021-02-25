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
<script type="text/javascript" src="jquery-1.11.1.min.js"></script>
<script type="text/javascript">    
var $1111 = $.noConflict(true);
</script>
```

noConflictの引数にtrueを指定し、jQueryオブジェクトを別名に書き換えます。  
上記の場合、1.11.1のjQueryオブジェクトが「$1111」として、1.2.6のjQueryオブジェクトが「$」「jQuery」として使用できます。  
ちなみに、$1111は任意のため、$「****」部分は好きな文字で大丈夫。

## 共存した状態でのプラグインの使用方法
プラグインが1.11.1のバージョンでしか使えない場合は、下記のようにプラグイン本体のjavascriptを囲います。

```Javascript
(function($){
    // プラグイン本体のjavascript
})($1111)
```

こうすることで、プラグイン本体内の「$」は「$1111」として認識します。  

### 実例
```Javascript
(function($){
    // ↓元々のscript
    $(function() {
      var href = "https://sigotora.jp/index.cfm";
      $('#srh_ken_param,#sfw,.srh_jobtype_child_param').on('change', function() {
        var srh_ken_param = $('#srh_ken_param').val();
        var sfw = $('#sfw').val();
        var srh_jobtype_child_param = $('.srh_jobtype_child_param:checked').map(function() {
                      return $(this).val();
                    }).get();
        $('#test').prop('href', href + "?fuseaction=job.joblist&srh_jobtype_param=5&srh_ken_param=" + srh_ken_param + "&sfw=" + sfw + "&srh_jobtype_child_param=" + srh_jobtype_child_param);
      });
    });
    // ↑元々のscript
})($1111)
```
