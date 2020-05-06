步骤
如果想从AutoApiSecret项目直接升级

可以把本项目代码下载，然后把里面部分文件更新进AutoApiSecret:

把 AutoApiSecret 的 1.py 删除，再把本项目的1.py 上传上去

把 update.py 上传到 AutoApiSecret

把 .github/workflow/AutoupdateToken.yml 上传到 AutoApiSecret 的 .github/workflow/ 文件夹下

把 AutoApiSecret 的.github/workflow/autoapi.yml 删除，再把本项目的 .github/workflow/AutoApiSR.yml 上传上去

如果是以前从未接触AutoApi系列项目的

第一步，先大致浏览原教程，了解如何获取应用id、机密、refresh_token 3样东西，以方便接下来的操作。

第二步，登陆/新建github账号，回到本项目页面，点击右上角fork本项目的代码到你自己的账号，然后你账号下会出现一个一模一样的项目，接下来的操作均在你的这个项目下进行。（看不到图片/图裂请科学上网）

image

根据原教程获取应用id、机密、refresh_token（自己复制保存，注意区分id机密，别弄混了）

然后在线编辑你项目里的1.txt，将整个refresh_token覆盖粘贴进去（里面是我的数据，先删掉或者覆盖掉）。（千万不要改1.py）

refresh_token位置如图下。复制refresh_token紧接着的双引号里的内容（红竖线框起来的），不要把双引号复制进去。复制进1.txt后，留意结尾不要留空格或者空行

image

第三步，依次点击上栏Setting > Secrets > Add a new secret，新建两个secret如图：CONFIG_ID、CONFIG_KEY。

内容分别如下: ( 把你的应用id改成你的应用id , 你的应用机密改成你的机密，单引号不要动 )

CONFIG_ID

id=r'你的应用id'
CONFIG_KEY

secret=r'你的应用机密'
image

最终格式应该是类似这样的：

image

第四步，进入你的个人设置页面(右上角头像 Settings，不是仓库里的 Settings)，选择 Developer settings > Personal access tokens > Generate new token,

image image

设置名字为GITHUB_TOKEN , 然后勾选 repo , admin:repo_hook , workflow 等选项，最后点击Generate token即可。

image image image

第五步，点击右上角星星/star立马调用一次，再点击上面的Action就能看到每次的运行日志，看看运行状况

（必需点进去Test Api看下，api有没有调用到位，有没有出错。外面的Auto Api打勾只能说明运行是正常的，我们还需要确认10个api调用成功了，就像图里的一样。如果少了几个api，要么是注册应用的时候赋予api权限没弄好；要么是没登录激活onedrive，登录激活一下）

image

第六步，没出错的话，就搞定啦！！再看看下面的定时次数要不要修改，不打算改就忽略。

然后第二天回来确认下是否自动运行了（ation里是否多出来几个）,是的话就不用管了，完结。

我设定的每6小时自动运行一次，每次调用3轮（点击右上角星星/star也可以立马调用一次），你们自行斟酌修改（我也不知道保持活跃要调用多少次、多久）：

定时自动启动修改地方：（在.github/workflow/autoapi.yml文件里，自行百度cron定时任务格式，最短每5分钟一次）
image

每次轮数修改地方：（在1.py最后面）
image

题外话
Api调用 你们可以自己去graph浏览器看一下，学着自己修改要调用什么api(最重要的是调用outlook、onedrive) https://developer.microsoft.com/zh-CN/graph/graph-explorer/preview

GithubAction介绍
提供的虚拟环境：

· 2-core CPU · 7 GB RAM 内存 · 14 GB SSD 硬盘空间

使用限制：

每个仓库只能同时支持20个 workflow 并行。
每小时可以调用1000次 GitHub API 。
每个 job 最多可以执行6个小时。
免费版的用户最大支持20个 job 并发执行，macOS 最大只支持5个。
私有仓库每月累计使用时间为2000分钟，超过后$ 0.008/分钟，公共仓库则无限制。
（我们这里用的公共仓库，按理，你们可以设定无限循环调用，然后6小时启动一次，保证24小时全天候调用）

最后的最后，再次感谢黑幕/paran大佬

————wangziyingwen/酷安id-卷腿毛菌

