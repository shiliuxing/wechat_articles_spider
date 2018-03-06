# 微信公众号文章爬虫

实现思路:

1. 从微信公众号平台获取微信公众所有文章的url

2. 登录微信PC端获取文章的阅读数、评论等信息

具体可以参考我的博客: [微信公众号爬虫](http://blog.csdn.net/wnma3mz/article/details/78570580)

## 第三方包

- `requests`: 爬取内容

## API实例

### 支持两种爬虫方式

下面登录方式选用其一即可

1. 账号密码爬虫，输入账号密码后，扫描二维码登录。自动获取cookie和token。此方法需要安装`matplotlib`和`PIL`用于显示二维码图片

2. cookie、token爬虫，手动复制cookie和token。具体cookie和token获取方式见[说明文档](https://github.com/wnma3mz/wechat_articles_spider/blob/master/get_cookie_token.md)

### 支持三种存储方式

1. txt存储（不建议）

2. sqlite3存储。自带模块，不需要额外安装

3. mongo存储。需要安装`pymongo`。暂未完成

```python
# 导入模块
from wechatarticles import OfficialWeChat
from wechatarticles import LoginWeChat

"""
初始化一些参数
username: 用户账号
password: 用户密码
cookie: 登录后获取的cookie
token: 登录后获取的token
nickname: 需要爬取的公众号
"""
username = username
password = password
cookie = yourcookie
token = token
nickname = nickname

# 实例化爬取对象

# 账号密码自动获取cookie和token
test = OfficialWeChat(username=usernmae, password=password)
# 手动输入账号密码
test = OfficialWeChat(cookie=cookie, token=token)

# 获取公众号文章总数
articles_sum = test.totalNums(nickname)
# 实例化爬取对象
test = OfficialWeChat(token, cookie)
# 获取公众号文章总数
articles_sum = test.totalNums(nickname)
# 获取公众号部分文章信息
artiacle_data = test.get_articles(nickname, begin="10", count="5")
# 获取公众号的一些信息
officical_info = test.get_official_info(nickname)
# 保存数据为txt格式
test.save_txt("test.txt", artiacle_data)
# 保存数据为sqlite3
test.save_sqlite("test.db", "test", artiacle_data)
```

```python
# 输出
print("articles_sum:", articles_sum)
print("artcles_data:")
pprint(artiacle_data)
print("officical_info:")
pprint(officical_info)
```

## TO-DO

1. 支持cookie的保留

2. 模拟登录微信PC端

3. 支持存储数据到mongo中
