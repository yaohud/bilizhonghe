# bilizhonghe
BilibiliAPI 合集 含个人、视频、直播等信息
https://api.bilibili.com/x/web-interface/view?bvid=BV号

获取视频AV号（内含视频基本信息，若此BV对应视频属于系列视频，API会列出所有系列视频）



https://api.bilibili.com/x/space/acc/info?mid=UID

UP主信息（名称、性别、头像、描述、个人认证信息、大会员状态、直播间地址、预览图、标题、房间号、观看人数、直播间状态[开启/关闭]等）



https://api.bilibili.com/x/space/channel/index?mid=UID

UP主首页展示频道视频



https://api.bilibili.com/x/space/nAVnum?mid=UID

UP主视频、频道总数（请求被拦截）



https://api.bilibili.com/x/relation/stat?vmid=UID

UP主粉丝数、关注数



https://api.bilibili.com/x/space/upstat?mid=UID

UP主总播放数、总专栏浏览数



https://api.bilibili.com/x/space/top/arc?vmid=UID

UP主置顶视频



https://api.bilibili.com/x/space/arc/search?mid=UID&pn=页码&ps=单页数据量&index=分类

分类为数字 1为全部类型 其余未知
此API相当于"投稿"选项卡内的分页获取视频数据（此处有总视频数）



https://api.bilibili.com/x/ugcpay-rank/elec/month/up?up_mid=UID

UP主充电信息（月充电人数、月充电用户、总充电人数）



https://api.bilibili.com/x/space/notice?mid=UID



UP主页公告信息

https://api.bilibili.com/x/space/acc/tags?mid=UID



UP主标签

https://api.live.bilibili.com/xlive/web-room/v1/index/getRoomBaseInfo?uids=UID&;req_biz=video

UP主直播间信息（同上，另含背景图、直播分类等）



http://api.live.bilibili.com/ajax/msg?roomid=直播房间ID

获取直播间评论/弹幕（若需实时评论，循环调用此API过滤重复）

https://api.bilibili.com/x/web-interface/archive/relation?bvid=视频BV

这个API可以获取你对此视频进行的操作（是否观看过、点赞、踩、投币数、收藏）但需要Cookie
（还有一个aid参数 不知道有什么用 这里我删了）

https://api.bilibili.com/x/web-interface/dynamic/region?ps=单页数据量&rid=不知道是什么(默认1)

获取首页视频（具体我也不知道rid该填什么）

https://api.bilibili.com/x/web-interface/ranking/region?rid=1&day=3&original=0

获取首页排行榜（参数未知）

https://api.bilibili.com/pgc/web/timeline/v2?season_type=1&day_before=1&day_after=5

获取首页番剧信息latest为最新番剧（内有预览图、标题、更新至第N话、更新时间等）
timeline为时间线，可以获取期当天更新的番剧信息，同上

https://api.bilibili.com/pgc/web/rank/list?season_type=1&day=3

番剧排行榜（含番剧播出类型[独家/会员/限免等]、番剧预览图、番剧名称、弹幕数、追番数、观看数等）

首页特别推荐

https://api.bilibili.com/pgc/operation/api/slideshow?position_id=104

（修改position_id数据不同，该参数为推荐内容位置[首页有很多推荐板块，这个参数各有不同，自己开F12寻找吧]）

话题获取(GET Cookie)
https://app.bilibili.com/x/topic/web/dynamic/rcmd?source=Web&;;page_size=1

获取UP主动态(GET)
第一次访问这个:https://api.vc.bilibili.com/dynamic_svr/v1/dynamic_svr/space_history?host_uid=对象uid

想要访问下一页请获取JSON.data.next_offset的值(每一次访问都会有) 是一串数字不是请用科学计数法计算

然后访问:https://api.vc.bilibili.com/dynamic_svr/v1/dynamic_svr/space_history?host_uid=686584029&;;offset_dynamic_id=JSON.data.next_offset的值

点赞视频(POST Cookie)
https://api.bilibili.com/x/web-interface/archive/like1

提交数据:   aid=目标视频的av号&like=1&csrf=自己csf

(aid为目标视频的av号非bv号,csf为自己的csf一般在cookie中找到)

发送评论(POST Cookie)
https://api.bilibili.com/x/v2/reply/add

提交数据:    oid=视频的av号&type=1&message=发言内容且要utf8编码&plat=1&ordering=heat&jsonp=jsonp&csrf=自己csf

(oid也是目标视频的av号,message为要评论内容,需要经过utf8编码后才可正常显示,csf上文有

读取私信(GET Cookie)
https://api.vc.bilibili.com/svr_sync/v1/svr_sync/fetch_session_msgs?talker_id=私聊对象uid&session_type=1

(talker_id为会话对象uid,session_type为会话类型经过测试只有1有返回)

发送私信(POST Cookie)

https://api.vc.bilibili.com/svr_sync/v1/svr_sync/fetch_session_msgs?talker_id=私聊对象uid&session_type=1

(talker_id为会话对象uid,session_type为会话类型经过测试只有1有返回)

向指定文章/视频投币(POST Cookie)
https://api.bilibili.com/x/web-interface/coin/add

当为专栏/视频投币时提交:  csrf=自己的csrf&aid=专栏/视频的id(为请求网址里的cv/av 1时请填视频av 请填专栏av(cv))&upid=up的uid(可以随便填)&multiply=(投币数量目前为一,因为专栏上限一个币)&avtype=(1为点赞视频,2为点赞专栏)

向指定文章/视频投币(POST 返回json 需cookie)
https://api.bilibili.com/x/web-interface/coin/add

当为专栏/视频投币时提交:  csrf=自己的csrf&aid=专栏/视频的id(为请求网址里的cv/av 1时请填视频av 请填专栏av(cv))&upid=up的uid(可以随便填)&multiply=(投币数量目前为一,因为专栏上限一个币)&avtype=(1为点赞视频,2为点赞专栏)

{"code":34005,"message":"超过投币上限啦~","ttl":1,"data":{"like":false}}
                返回如上(ps:为了这个api我花费了15个硬币……)

 取/关注(POST 返回json 需cookie)
https://api.bilibili.com/x/relation/modify

提交数据: fid=关注的人uid&act=(模式,1为关注2为取关)&csrf=(您的csrf)

{"code":0,"message":"0","ttl":1}

收藏稿件(文章)(POST 返回json 需cookie)
https://api.bilibili.com/x/article/favorites/add

提交信息:  csrf=您的csrf&id=文章的cv(不带cv)

{"code":0,"message":"0","ttl":1}

取消收藏稿件(文章)(POST 返回json 需cookie)
https://api.bilibili.com/x/article/favorites/del

提交信息:  csrf=您的csrf&id=文章的cv(不带cv)

{"code":0,"message":"0","ttl":1}

读取视频可以储存的收藏文件夹列表(GET 返回json 需cookie)
https://api.bilibili.com/x/v3/fav/folder/created/list-all?type=2&rid=视频av&up_mid=您的uid

{"code":0,"message":"0","ttl":1,"data":{"count":5,"list":[{"id":1111887905,"fid":11118879,"mid":1311590005,"attr":131,"title":"***","fav_state":0,"media_count":4}],"season":null}}

收藏稿件(视频)(POST 返回json 需cookie)
https://api.bilibili.com/x/v3/fav/resource/deal

提交信息:  rid=视频av&type=2&add_media_ids=收藏夹代号(上条api周边获取)&csrf=您的csrf

{"code":0,"message":"0","ttl":1,"data":{"prompt":true}}

取消收藏稿件(视频)(POST 返回json 需cookie)
https://api.bilibili.com/x/v3/fav/resource/deal

提交信息:  rid=视频av&type=2&del_media_ids=收藏夹代号(上条api中获取)&csrf=您的csrf

{"code":0,"message":"0","ttl":1,"data":{"prompt":true}}

接收直播弹幕(POST 返回json 无需cookie)
https://api.live.bilibili.com/xlive/web-room/v1/dM/gethistory?roomid=房间id

获取自己历史记录 来自uid:176936889(GET 返回json 需cookie)
http://api.bilibili.com/x/v2/history?pn=页码

搜索内容(GET 返回json 无需cookie)
https://api.bilibili.com/x/web-interface/search/all/v2?page=页码&keyword=搜索内容(utf8编码)

获取热门动态(GET 返回json 无需cookie)
https://api.vc.bilibili.com/dynamic_svr/v1/dynamic_svr/unlogin_dynamics?fake_uid=随机数

fake_uid为随机数,不同的随机数返回不同(同一随机数不同时间也一样返回不同),但不填那都一样

获取小黑屋内容(GET 返回json 无需cookie)
https://api.bilibili.com/x/credit/blocked/list?otype=第几页&pn=第几个&ps=显示项目数目

otype为显示第几页,pn为显示第几页的哪一个,ps为输出几个结果

直播间弹幕(POST 返回Json 需Cookie)
https://api.live.bilibili.com/msg/send

提交信息:msg=要发送的内容(utf8编码)&roomid=直播间id&csrf=您的csrf&csrf_token=您的csrf&rnd=123467890(十位随机数,都可以)&color=16777215(颜色代码)&fontsize=25(字体大小)

获取推荐视频(GET 返回Json 需要/不需要Cookie)
https://api.bilibili.com/x/web-interface/index/top/rcmd?version=1&ps=显示个数

获取"综合热门"视频 (GET 返回Json 无需Cookie)
https://api.bilibili.com/x/web-interface/popular?ps=显示个数&pn=页码

获取"每周必看"视频 (GET 返回Json 无需Cookie)
https://api.bilibili.com/x/web-interface/popular/series/one?number=期数(第几期)

获取"入站必刷"视频 (GET 返回Json 无需Cookie)
https://api.bilibili.com/x/web-interface/popular/precious?page_size=显示个数&pn=页码

获取"排行榜·全部"视频 (GET 返回Json 无需Cookie)
https://api.bilibili.com/x/web-interface/ranking/v2?rid=0&type=all(其他的太诡异找不到) 作者：可爱的小喵咪Cat https://www.bilibili.com/read/cv12357091 出处：bilibili
