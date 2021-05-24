# OTT-IPTV

## 以下方法仅提供思路，具体看当地运营商运营方式。文章发布时间可能存在失效请自行辨认

移动魔百盒直播源生成m3u8播放列表
使用方法
  苏州移动IPTV抓包 获取频道列表接口地址和基础URL
  
  从下面网址中    
 ```
 http://looktvepg.jsa.bcs.ottcn.com:8080/ysten-lvoms-epg/epg/getChannelIndexs.shtml?deviceGroupId=1697
 ```
  
 可以看到
 ``` 
 "channel1":{"uuid":"HD-8000k-1080P-cctv1","channelName":"CCTV-1","channelIcon":"http://images.center.bcs.ottcn.com:8080/images/ysten/images/ysten/TV/HD-8000k-1080P-cctv1/CCTV-1JSXB.png"}
 ```
 的结构需要转换成  
 
 http://183.207.248.71:80/cntv/live1/channelName/uuid  的方式就可以播放了
 
 
 使用notepad++  正则表达式把各个频道替换下播放地址就OK了 
 
如果有服务器可以用php代理，  https://raw.githubusercontent.com/iam7cn/OTT-IPTV/master/jstv.txt 就是我自己用php代理出来的


PHP代码

```
<?php
if(!$_GET['code']){
    echo "404 error";
    exit();
}
$code=$_GET["code"];
$info=file_get_contents("http://looktvepg.jsa.bcs.ottcn.com:8080/ysten-lvoms-epg/epg/getChannelIndexs.shtml?deviceGroupId=1697");
preg_match('/"'.$code.'":{"uuid":"(.*?)","channelName":"(.*?)",/i',$info,$m);
$url = 'http://183.207.248.71:80/cntv/live1/'.$m[2].'/'.$m[1].'';
$playurl = iconv('UTF-8', 'GBK//TRANSLIT', $url);
header('location:'.urldecode($playurl));
?>
```



