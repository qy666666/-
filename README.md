scroll-view:
<scroll-view class="wrap" bindscrolltoupper="scrolltupper" bindscrolltolower="scrolllower" upper-threshold="100" lower-threshold="50" scroll-into-view="{{location}}" scroll-y="true" scroll="true">
  <view id="a" class='a'>a</view>
  <view id="b" class='b'>b</view>
  <view id="c" class='c'>c</view>
</scroll-view>
通过scroll-view可实现视图的滚动滑动，a,b,c,在wxss中可以设置初始属性，
.a{
  background-color: red;
}
.b{
  background-color: green;
}
.c{
  background-color: blue;
}
scroll-y or scroll-x可以控制对上下或左右的滑动。
wrap：对视图的初始话：
.wrap{
  width: 400rpx;
  height: 400rpx;
  border: 1px solid red;
  text-align: center;
}
bindscrolltoupper="scrolltupper" bindscrolltolower="scrolllower"
bindscrolltoupper和--lower对到顶或到底的一个事件的判断。
<button  hover-class="active" bindtap='tapq'>切换</button>
class为基础属性hover-class为触发后属性，
.active{
  color:red;
}
此时点击后字体颜色由默认改为设定颜色（red）;
<slider bindchange='interview' show-value min='2000' max='5000'></slider>
slider中设置可拖动的长度
<swiper indicator-dots='true' autoplay='{{autoplay}}' interval='{{inter}}'duration='500' current='2'
bindchange='swiperchange'>
  <block>
  <swiper-item wx:for="{{imgUrls}}">
    <image src='{{item}}' width="355" height="150"></image>
    我是文字
  </swiper-item>
  </block>
</swiper>
<slider bindchange='interview' show-value min='2000' max='5000'></slider>
<button bindtap='changeanto'>切换antoplay</button>



imgUrls: [
      'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
      'http://img06.tooopen.com/images/20160818/tooopen_sy_175866434296.jpg',
      'http://img06.tooopen.com/images/20160818/tooopen_sy_175833047715.jpg'
    ],
如果在 bindchange 的事件回调函数中使用 setData 改变 current 值，则有可能导致 setData 被不停地调用，因而通常情况下请在改变 current 值前检测 source 字段来判断是否是由于用户触摸引起。


<icon type='success' size='50' color='green'></icon>
设置一个简单的图案。
<view wx:for="{{iconType}}">
  <block >
    <icon type='{{item}}' size='40'></icon>
  </block>
</view>

iconType: [
      'success', 'success_no_circle', 'info', 'warn', 'waiting', 'cancel', 'download', 'search', 'clear'
    ],
通过一个简单的for循环得出多种图案。

<input placeholder="输入用户名" placeholder-class='outher-placeholder' maxlength='10' auto-focus='true' bindinput='inputFn' bindfocus='focusFn'></input>
实现数字和文字的输入，maxlength定义输入的最大长度。

picker:选择器
<view class='settion'>选择城市</view>
<picker bindchange='bindpickerchange' value='{{index}}' range='{{citys}}'>
  <view>当前选择:{{citys[index]}}</view>
</picker>
<view class='settion'>选择时间：</view>
<picker value="{{time}}" start="09:01" end="21:01" mode="time" bindchange='bindtimechange'>
  <view>当前选择{{time}}</view>
</picker>
<view class='settion'>选择日期：</view>
<picker mode="date" value='{{date}}' start="2019-01-30" end='2020-10-21' bindchange='binddatachange'>
  <view>当前选择：{{date}}</view>
</picker>

citys:['北京','上海','广州','深圳'],
time:"09:01",
index：0,
date:"2019-01-30",
这个里先给定初始时间，日期，城市。

复选框：
<checkbox-group bindchange="checkChange">
    <label class="checkbox" wx:for="{{country}}">
      <checkbox value="{{item.name}}" checked="{{item.checked}}">{{item.value}}</checkbox>
    </label>
</checkbox-group>

country: [
      { name: 'USA', value: '美国' },
      { name: 'CHN', value: '中国', checked: 'true' },
      { name: 'BRA', value: '巴西' },
      { name: 'JPN', value: '日本' },
      { name: 'ENG', value: '英国' },
      { name: 'TUR', value: '法国' },
    ],
通过选择确定要选的的城市。

<!--单选框-->
<radio-group bindchange='bindradiochange'>
  <label class="checkbox" wx:for="{{country}}">
      <checkbox value="{{item.name}}" checked="{{item.checked}}">{{item.value}}</checkbox>
  </label>
</radio-group>
复选框能同时选择多个，而单选框只能选择一个。

<!--滑动选择器-->
<slider show-value='true' min='0' max='100' step='5' bindchange='bindradiochange' value='10'></slider>
<!--开关选择器-->
<switch  class='switch' checked='true' type='checkbox' bindchange='bindswitchchange'></switch>
<!--多行文本-->
<textarea class='textarea' placeholder='输入：' placeholder-class='textareaholder'auto-height='true' bindlinechange='bindtextlinechange'></textarea>
<button bindtap='showaction'>显示操作菜单</button>
<button bindtap='showmode'>显示模拟弹窗</button>
<button bindtap='showToast'>显示消息提示框</button>
<navigator url='../test/test' >跳转到首页</navigator>

showmode:function(){
    wx.showModal({
      title: '提示',
      content: '我是一个模态窗',
      showCancel:false,
      cancelText:"继续",
      confirmText:"继续确定",
      success:function(res){
        console.log(res.tapindex);
      }
    })

  },
  showToast:function(){
    wx.showToast({
      title:"删除成功",
      icon:"success",
      duration:10000,
      success:function(){
        console.log("显示成功");
      }
    });
   wx.request({
     url: api,
     data:{},
     header:{
       'Content-Type':'application/json'
     },
     success:function(res){
       console.log(res.data);
       wx.hideToast();
     }
   });
  },
  showaction:function(){
    wx.showActionSheet({
      itemList: ['A','B','C'],
      success:function(res){
        if(!res.cancel){
          console.log(res.tapIndex);
        }
      }
    })
  },
textarea与input类似。
