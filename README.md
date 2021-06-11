## Hexo 主题 Tree

一个简洁的主题，主要功能是 “树状导航” + “树状目录”，可选配“评论”和“阅读量”功能。

有问题欢迎及时联系，issues、邮件都行

Demo：https://wujun234.github.io/

[![img](https://github.com/wujun234/hexo-theme-tree/raw/master/source/Tree.png)](https://github.com/wujun234/hexo-theme-tree/blob/master/source/Tree.png)

## 使用说明

### 1 下载主题

下载主题到 `hexo` 根目录中 `themes` 目录下

```
git clone https://github.com/JiangJiaWei520/hexo-theme-tree.git  themes/tree
```

修改 `hexo` 根目录的 `_config.yml`

```
theme: tree
```

### 2 配置主题

如果要使用 `valine` 的评论及阅读量功能，需要在 `themes/tree` 路径下的 `_config.yml` 文件中，填写自己申请的 `leancloud` 账户下面的 `appID` 和 `appKey`

```
valine:
    appID: 
    appKey: 
```

若不需使用，则设置

```
valine:
    enableComment: false 
    enableCounter: false
```

### 3 导航栏和图标

- 导航栏：当前没有配置化，需要修改`themes/tree/layout/_partial` 路径下的 `header.ejs` 文件
- 图标：替换`themes/tree/source` 路径下的`favicon.ico` 文件

### 4 about 页

在 `source`路径下，与`_posts`文件夹平行，建立一个`about`页

执行

```
hexo new page --path about/index "About"
```

参考：https://hexo.io/zh-cn/docs/commands.html#new

### 5 文章树、目录树

页面左侧的文章树是根据 source 文件夹里的文章和文件夹生成的，目录树是根据文章中的标题生成的

## 其他

### 推荐插件

推荐安装 [Markdown-it](https://github.com/markdown-it/markdown-it) 插件渲染 `Markdown`

替换之后注意将 _config.yml 中 hexo 默认的 Markdown 配置改一下

```
highlight:
  enable: false
  line_number: false
  auto_detect: false
  tab_replace: ''
```

### 访问管理

我自己用的是百度统计 [https://tongji.baidu.com](https://tongji.baidu.com/) ，很简单，注册后在 'head' 里加一个 '<script>' 块就行了



### 注意：

- **hexo 的 CNAME 文件** 需要放在source 目录下，每次运行hexo clean会清除public 目录，hexo g重新生成，hexo d发布到远程服务器。

1、准确来说 CNAME 文件是放在 hexo 项目下的 source 目录，你再运行下

```text
hexo generade
```

然后你再去 public 目录中看看就明白了

BTW，为了达到更有说服力的验证，最好在开始前先运行下

```text
hexo clean
```

这样会先删除 public 目录

- **hexo 的 README.md等文件**

  [原文]: (https://www.dazhuanlan.com/2020/03/20/5e73a3d07ebbc/)

  文件添加在 **Hexo**目录下的**source**根目录下创建**README.md**文件。并编辑保存。

  - **防止README.md被渲染**

  编辑**Hexo**目录的_config.yml文件中的“skip_render”参数。
  eg：

  ```
  skip_render: [README.md]
  ```

  保存并退出。

  - **完成**

  试着命令部署，再去你的 Git仓库看看是否存在README.md文件。

  ```
  $ Hexo clean && hexo g && hexo d
  ```

- **插入网站运行时间代码**

  ```
  样例 1:
  <span>
  本站已运行
  </span>
  <span id="span_dt_dt">
  </span>
  <script>
  /*建站时间*/
  function show_date_time() {
  window.setTimeout("show_date_time()", 1e3);
  var BirthDay = new Date("2018/03/01"),
  today = new Date,
  timeold = today.getTime() - BirthDay.getTime(),
  msPerDay = 864e5,
  e_daysold = timeold / msPerDay,
  daysold = Math.floor(e_daysold),
  e_hrsold = 24 * (e_daysold - daysold),
  hrsold = Math.floor(e_hrsold),
  e_minsold = 60 * (e_hrsold - hrsold),
  minsold = Math.floor(60 * (e_hrsold - hrsold)),
  seconds = Math.floor(60 * (e_minsold - minsold));
  span_dt_dt.innerHTML = daysold + "天" + hrsold + "小时" + minsold + "分" + seconds + "秒";
  }
  show_date_time();
  </script>
  ```
  ```
  样例 2：
  当前系统时间
  <span id="nowTime"></span>
  <script type="text/javascript">
  //获取系统时间
  var newDate = '';
  getLangDate();
  //值小于10时，在前面补0
  function dateFilter(date){
  if(date < 10){return "0"+date;}
  return date;
  }
  function getLangDate(){
  var dateObj = new Date(); //表示当前系统时间的Date对象
  var year = dateObj.getFullYear(); //当前系统时间的完整年份值
  var month = dateObj.getMonth()+1; //当前系统时间的月份值
  var date = dateObj.getDate(); //当前系统时间的月份中的日
  var day = dateObj.getDay(); //当前系统时间中的星期值
  var weeks = ["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];
  var week = weeks[day]; //根据星期值，从数组中获取对应的星期字符串
  var hour = dateObj.getHours(); //当前系统时间的小时值
  var minute = dateObj.getMinutes(); //当前系统时间的分钟值
  var second = dateObj.getSeconds(); //当前系统时间的秒钟值
  var timeValue = "" +((hour >= 12) ? (hour >= 18) ? "晚上" : "下午" : "上午" ); //当前时间属于上午、晚上还是下午
  newDate = dateFilter(year)+"年"+dateFilter(month)+"月"+dateFilter(date)+"日 "+" "+dateFilter(hour)+":"+dateFilter(minute)+":"+dateFilter(second);
  document.getElementById("nowTime").innerHTML = timeValue+"好！当前时间为： "+newDate+"　"+week;
  setTimeout("getLangDate()",1000);
  }
  </script>
  ```
  ```
  样例 3：
  function showtime(times) { //传入时间的参数
  var time_1 = new Date(times).getTime();
  var time_2 = new Date().getTime();
  var time_3;
  var time_distance;
  //计算时间差
  if (time_1 > time_2) {
  time_distance = time_1 - time_2;
  } else {
  time_distance = time_2 - time_1;
  }
  if (time_distance > 0) {
  // 天时分秒换算
  var int_day = Math.floor(time_distance / 86400000);
  time_distance -= int_day * 86400000;
  var int_hour = Math.floor(time_distance / 3600000);
  time_distance -= int_hour * 3600000;
  var int_minute = Math.floor(time_distance / 60000);
  time_distance -= int_minute * 60000;
  var int_second = Math.floor(time_distance / 1000);
  // 时分秒为单数时、前面加零
  if (int_day < 10) {
  int_day = "0" + int_day;
  }
  if (int_hour < 10) {
  int_hour = "0" + int_hour;
  }
  if (int_minute < 10) {
  int_minute = "0" + int_minute;
  }
  ```