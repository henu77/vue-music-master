# vue-music

## 下载依赖

```
npm install
```

### 启动项目

```
npm run serve
```

### 打包项目

```
npm run build
```

### 后台 GitHub 地址

https://github.com/Binaryify/NeteaseCloudMusicApi
开发时对应版本：4.0.23
若出现问题则选择最新版本

### 预览地址

[仿网易云音乐预览地址 ](http://47.102.159.133/)
### uni-app版

[uni-app版仓库 ](https://gitee.com/crazybox521/uni-music)

### 目前完成功能

- 歌曲播放器：播放、拖动进度、音量调整、下载、播放列表，歌曲页歌词滚动、评论
- 发现页：推荐、歌单、歌手、排行榜、最新音乐（新歌速递、新碟上架（本周新碟））
- 登录：手机号密码登录，二维码登录，验证码登录，退出登录
- 歌曲列表：喜欢音乐，专辑入口，歌手入口，当前播放音乐行
- 各详情页
  - 歌单详情页：歌曲列表、歌单页搜索、加载完整歌单、收藏、评论
  - 专辑详情页：歌曲列表、搜索、收藏、评论、专辑详情
  - 歌手详情页：专辑列表、歌手描述、MV、相似歌手
  - 视频详情页：视频播放（使用原生 video 及控件播放）、相似视频推荐、 MV 播放、MV 推荐，点赞、收藏、评论、关注创作者
  - 用户详情页：基本信息、地区（仅支持国内地区）、创建的歌单、收藏的歌单、更新个人信息和头像
- 搜索：歌曲、歌手、歌单、用户、MV、专辑搜索、热搜榜、搜索建议、搜索结果快捷入口
- 评论（需要登录）：点赞、回复、评论、评论分页、及页码跳转和回复跳转输入框的动画
- 视频（需要登录）：视频列表、MV 列表、全部 MV 页、MV 排行页
- 我的收藏（需要登录）：收藏的专辑、MV、歌手及筛选功能
- 最近播放（本地存储，不是云端的播放记录）
- 私人 FM（需要登录）：播放、垃圾桶，喜欢、评论、歌词滚动(这里表现不太与网易云一样，如果想要一致需要改很多)
- 全部页面移动端适配
- 路由懒加载及代码分块，添加未登录情况下导航守卫，路由 props 解耦合
- 使用 Vuex 管理登录状态、当前歌曲列表及歌曲状态、其余多组件状态
- 分享的接口为分享到网易云动态，因还没有做动态部分，所有分享是无效的，收藏全部歌曲按网易云的表现是收藏到某个创建的歌单或者创建新歌单，暂未加入

### BUG or UPDATE

- 添加对歌单加载完整歌曲的限制（使用过程中遇到了个 6000 单曲的歌单，使用 trackIds 请求对应歌曲会造成 431 错误）
- 添加对最近播放歌曲数量的限制 11/19
- 解决添加导航守卫后，刷新丢失登录状态，在重新获取完登录状态就错误导航的 bug 11/20
- 添加视频播放时停止歌曲播放
- 解决歌手详情页相似歌手 tab 下切换歌手无法更新数据的状况
- 添加歌词滚动的 js 动画
- 添加路由视图切换的动画
- 添加歌手详情页 Tab 切换加载数据的动画以及为空时的提示
- 添加@根目录,并将 API 按功能模块化，便于管理
- 遇到了作用域具名插槽后备内容打包后不生效的问题，其在开发环境表现正常，暂未解决，只能用到都使用，而不是利用后备内容
- 遇到了超出 JS 最大安全数字的问题，暂未解决（在获取搜索建议时得到的歌曲信息中的图片是 NULL，但是图片 ID 有，只不过超出安全数不准确），可以自己定义 axios 处理数据的方式（axios 默认直接 JSON.parse）,有相关的插件
- 解决歌曲页面评论区点击用户跳转用户路由，但是播放界面不关闭的 bug，以及用户页面不随 id 变化的 bug,删除播放组件重复逻辑
- 移动端 outline 没有圆角，更换为 border
- 将专辑列表、歌单列表、歌手列表整合为一个组件
- 将仅渲染的数据冻结，优化性能
- 将视频详情和 MV 详情页整合为一个组件
- 大部分子页面均使用同一个滚动条，监听路由地址，重置滚动条，以及更换歌曲时重置歌曲播放页滚动条
- 修复评论内容长数字不换行的 bug
- 解决歌曲进度往前拉，歌词激活行不变的 bug；改变了歌词滚动判断的当前时间来源（之前是 audio 实时播放时间，现在是前者经过处理的提交到 vuex 的当前时间，可能会稍有延迟或提前）；抽离歌词组件（私人 FM 需要复用）
- chrome对媒体标签有限制，必须用户有交互才能自动播放
- 添加编辑创建的歌单信息，使用VueCropper插件实现裁剪图片
- 添加个人信息包括头像的裁剪更改，未加入地区，将图片裁剪及处理为blob对象封装成一个组件（歌单封面和个人头像）
- 取消使用Nprogress
- 歌手页取消使用ELTABS，改用项目中的TabMenu；修改封装的axios请求的get方法，改变处理错误的方式，使其能被async/await接收
- 部分插件cdn加载有些慢，导致第一次加载白屏时间过长
- 解决退出登录不退回首页的bug,部分页面图片懒加载
- 新增了部分图片懒加载，去除部分不合理的骨架，更改了组件使用的规范性
- 以及更改vue3 + ts版本重构中发现的bug
- 修复线上预览地址不能正常预览功能的问题