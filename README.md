## 一、前言

春节就快要到了，在这里先祝愿大家，2022年，如虎添翼万事圆！吉祥如意平安年，开心快乐幸福年，喜气冲天幸运年，财源滚滚发财年，万事大吉顺心年，美满团圆喜庆年，愿君新年事事顺利，岁岁平安，年年如意！

## 二、效果展示

### 1.春节计时

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d65a2cc39cd84fe68dd3fcc906cfed43~tplv-k3u1fbpfcp-zoom-1.image)
> -   春节计时的位置在中间偏上先设置一个大体的框架，代码获取到现在的时间显示，与过年设定好的时间进行比对，求解出具体还剩下的时分秒。


### 2.虎年摆件

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f243e16ae9e54e818377b3c564608879~tplv-k3u1fbpfcp-zoom-1.image)

> -   两个虎年动态摆件，左边是一只大吉大利的老虎，右边是一只心想事成的老虎，祝大家在新的一年里面，无论遇到任何事情都会大吉大利、心想事成。

### 3.背景音乐

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/06bf1b83294d4fd28a4081a9642365cd~tplv-k3u1fbpfcp-zoom-1.image)


> -   背景音乐是李谷一老师的难忘今宵（过年气氛就来了），点击右上角按钮即可以播放音乐

### 4.全局效果

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c0e86ffe68ba45eea90f97cf8e8a90c5~tplv-k3u1fbpfcp-zoom-1.image)

>- 总体布局还是中间上方是一个灯笼，下面是距离春节的倒计时，最下面是两个小老虎，点击老虎中间的按钮就可以观看烟花。


### 5.烟花祝福

## ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f2a603838f6048678ebf0ff56b65be81~tplv-k3u1fbpfcp-zoom-1.image)
> -   点击底部的提前观看烟花就会跳转新的页面，生成烟花祝福
> -   等到春节的那一刻，也会跳转到这一个页面

## 三、代码讲解

### html

```html
<!DOCTYPE html>
<html lang="zh">

<head>
  <meta charset="UTF-8">
  <meta name="viewport"
    content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no">
  <meta http-equiv="X-UA-Compatible' content='ie=edge,chrome=1">
  <link rel="stylesheet" href="./css/index.css?ver=1.0">
  <link rel="icon" href="./img/fz.png">
  <title>：知心宝贝祝你2022好运连连🎁</title>
</head>

<body>
  <!-- 初始页 -->
  <div class="index">
    <div class="lantern"></div>
    <div class="time">
      距离春节：
      <span class="hour">--</span> ://小时
      <span class="min">--</span> ://分钟
      <span class="second">--</span>//秒数
    </div>
    <div class="text"></div>
    <div class="fence">
      <div class="p1"></div>
      <div class="p2">提前看烟花</div>//点击按钮提前观看烟花
      <div class="p3"></div>
    </div>
  </div>
  <!-- 烟花场景 -->
  <div class="fire">//进入烟花的场景
    <canvas></canvas>
  </div>
  <!-- 烟花音效 -->
  <div class="fireSound">//设置不同的烟花音效
    <audio src="http://www.imooc.com/newyear/static/fire_sound.mp3" autoplay muted loop></audio>
    <audio src="http://www.imooc.com/newyear/static/fire_sound.mp3" autoplay muted loop></audio>
    <audio src="http://www.imooc.com/newyear/static/fire_sound.mp3" autoplay muted loop></audio>
  </div>
  <!-- 背景音乐 -->
  <div class="music run">
    <audio src="music/李谷一 - 难忘今宵.mp3" loop></audio>//李谷一老师的歌曲
  </div>
  <script src="./js/index.js?ver=1.0"></script>
</body>
</html>
```

### JS倒计时

```js
let timer1 = setInterval(() => {
    let nowTime = new Date(),//获取目前的时间
      future = new Date("2022/02/01 00:00"),//设置好过春节的时间
      // 时间差
      times = future - nowTime,
      // 时 分 秒
      h = Math.floor(times / (3600 * 1000)),//计算相差的小时数
      m = (Math.floor(times % (3600 * 1000) / (60 * 1000)) + '').padStart(2, 0),//计算分钟数
      s = (Math.floor(times % (60 * 1000) / 1000) + "").padStart(2, 0);//计算秒数
    hour.innerText = h
    min.innerText = m
    second.innerText = s

    if (s == "00" && h == "00" && m == "00") {//如果当前的时间和春节相等，触发烟花特效
      page1.style.display = "none"
      page2.style.display = "block"
      clearInterval(timer1)
      // 初始烟花界面
      initFire()
    }
  }, 1000)
```


### JS烟花

```js
function initFire() {
    // 爆炸声音
    for (let i = 0; i < fireAudio.length; i++) {
      fireAudio[i].currentTime = i
    }
    // 获取宽高
    let width = window.innerWidth,
      height = window.innerHeight
    // 设置宽高
    canvas.width = width
    canvas.height = height
    // 运动小球
    let balls = [],
      timer2 = null,
      count = 0,
      ballAll = 5,
      // 祝福词个数
      textAll = 5,
      // 祝福词坐标
      textPos = [
        { x: width / 4, y: height / 4 + 30 },
        { x: width / 4 * 3, y: height / 4 - 30 },
        { x: width / 2, y: height / 2 },
        { x: width / 4, y: height / 4 * 3 },
        { x: width / 4 * 3, y: height / 4 * 3 + 50 },
      ],
      // 爆炸数组
      fires = [],
      // 图片粒子点数组
      points1 = getImgInfo(imgArr[0], 4),
      points2 = [],
      textFires = []
    for (let i = 1; i < imgArr.length; i++) {
      points2.push(getImgInfo(imgArr[i], 2))
    }
```

### Css样式

```css
.index .fence .p1 {//对于左边小老虎的特效
  position: absolute;
  left: 0px;//左侧位置
  bottom: 0;
  z-index: 5;
  width: 280px;
  height: 300px;
  background: url(../img/kouzuo.png) bottom no-repeat;//设置图片在整个页面中的位置
  background-size: 100%;
  transform-origin: center bottom;//底部
  animation: 2s ease-in-out -1s infinite turn;
}
.index .fence .p3 {//对于右边小老虎的特效
  position: absolute;
  right: -60px;//右侧位置
  bottom: -70px;
  z-index: 10;
  width: 280px;
  height: 300px;
  background: url(../img/kouyou.png) no-repeat;//设置图片在整个页面中的位置
  background-size: 100%;
  transform-origin: center bottom;//底部
  animation: 2s ease-in-out infinite turn;
}
```

## 四、Github Pages

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/406f941ea58e42e1b66cdda9ba2ea876~tplv-k3u1fbpfcp-zoom-1.image)

Github Pages为每一个账户提供了专属域名，可以把自己提交到仓库的项目生成一个可执行站点，后面有机会我再详细介绍使用教程。

上面的春节代码只是简单列举了一些，大家如果想体验直接点击用Github Pages生成的链接：[春节](https://bosombaby.github.io/ "春节")，或者自己依靠Github Pages上传这个项目文件，搞一个专属于自己的网页。

点击链接之后，就会跳转到上面效果图的界面，国内访问可能会有一点卡顿，等待一会就可以。

## 五、附录

   这个代码是参考Github的牛年新春页面写的：[牛年贺春](https://github.com/KailoveQ/New-Year-Card "牛年贺春")

   我给改成了虎年新春：[虎年新春](https://github.com/bosombaby/bosombaby.github.io "虎年新春")，大家想要源码直接上Github上面下载不同两个年份的贺春页面体验一下就可以了。

 趁着钟声还未响，趁着鞭炮还未鸣，趁着春节还未至，趁着虎年刚开始，趁着人还未喝醉。先把我美好的祝愿送到你的手机，在这里祝愿大家虎年吉祥如意，合家欢乐。