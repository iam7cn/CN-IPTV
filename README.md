# OTT-IPTV
移动魔百盒直播源生成m3u8播放列表
使用方法
  苏州移动IPTV抓包 获取频道列表接口地址和基础URL
  
  从下面网址中    
  http://looktvepg.jsa.bcs.ottcn.com:8080/ysten-lvoms-epg/epg/getChannelIndexs.shtml?deviceGroupId=1697
  
 可以看到
 "channel1":{"uuid":"HD-8000k-1080P-cctv1","channelName":"CCTV-1","channelIcon":"http://images.center.bcs.ottcn.com:8080/images/ysten/images/ysten/TV/HD-8000k-1080P-cctv1/CCTV-1JSXB.png"}
 的结构需要转换成  http://183.207.248.71:80/cntv/live1/channelName/uuid  的方式就可以播放了
 
 },
 },\N
 
 
 "channel[0-9]{0,9}":{"uuid":"(.*?)","channelName":"(.*?)","channelIcon":"http://images(.*?).png"}
 
 \2,http://183.207.248.71:80/cntv/live1/\2/\1
