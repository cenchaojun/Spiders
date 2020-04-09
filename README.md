# Spider

**环境说明:**

- `Python3.6`
- `Centos7.5`
- `Scrapy框架` & `简单py爬虫`

**已实现功能:**

1. 爬虫 Scrapy 爬取百度网盘搜索引擎数据
2. 自动将百度网盘资源转存到自己网盘
   1. 支持无提取码 URL
   2. 支持有提取码 URL

**待完成项:**

- 优质代理 IP 池
- 百度网盘自动保存资源 提取码-验证码问题
- 暂不支持保存自己分享的资源
- 代码优化

**文件说明:**

- baiduyun_tools.py 自动转存百度云盘资料
- file 存放自动转存百度云盘 信息
- proxies_tools.py 自动生成代理文件
- Spiders 爬取百度网盘搜索引擎资源
- scrapy_mockplus_template Scrapy爬虫,爬取MockPlus模板(待优化)

## 项目

- Baiduyun
  - 查询 网盘搜索引擎 上百度云盘资源
  - 将云盘资源保存到百度网盘中
- MockPLus
  - 自动获取 MockPlus 精美模板

### 爬虫项目

#### 常用命令

```python
scrapy startproject baidu
# 传递参数
scrapy crawl pansoso1 -a search_text=excel
```

#### 百度网盘网站资源说明

通用参数说明:

- mode 保存模式 append/override 建议 append
- search_text 搜索内容
- page 搜索页数

TODO override 存在 bug 后面覆盖前面的情况

#### 盘搜搜(未完成)

网站资源一般,链接存在加密,存在访问过多时 IP 封锁.

网站链接: 网盘资源 www.pansoso.com

```python
# 项目命令
scrapy crawl pansoso01 -a search_text=excel
scrapy crawl pansoso02
scrapy crawl pansoso03
```

#### 大圣盘((已完成)建议)

说明:

- 大多资源有效,且网站存在资源校验机制.
- 资源分为无提取码和有提取码两种.
- 资源文件都较大,且命名不规范,或非实际所需文件
- 反爬虫机制
  - 延迟加载(提取码 & 提取码是否有效)
    - 解决方法: 使用 selenium(浏览器处理)

网站链接: 网盘资源 www.dashengpan.com

```python
# 项目命令
scrapy crawl dashengpan01 -a mode=append -a search_text=excel -a page=1
```

#### 搜百度盘(已完成)

说明:

- 搜百度盘 网站简单,适合练手
- 但是资源基本(99%)都是无效资源,无过多反爬虫机制.
- 不建议使用此网站

```python
# 项目命令
scrapy crawl sobaidupan01 -a search_text=excel  -a page=1000
scrapy crawl sobaidupan02
```

网站链接: 网盘资源 www.sobaidupan.com

### 百度云资源自动转存项目

**项目详细说明:**

1. 支持功能
   1. 自动将 文件中 URL 保存到百度网盘中
   2. 支持有提取码和无提取码格式
   3. 对资源保存情况有整体说明等
2. TODO 暂不支持
   1. 根据用户名称和密码自动登录获取 Cookie
   2. 部分资源有提取码时仍需要验证码,暂不支持
3. 其他说明:
   1. 使用 Linux 测试,Windows 未测试
   2. 附件说明
      1. `file/badidu_result.txt` 存放百度云资料
      2. `file/success.txt` 存放保存成功的资源
      3. `file/failed.txt` 存放保存失败的资源

**使用样例:**

```bash
# 将网盘资源保存到百度网盘
python baiduyun_tools.py -filename xxxxx -cookie xxxxx -path xxxx

# 输出说明
success.txt 记录成功运行的 URL, 下次运行时不会在运行此中URL
failed.txt 记录失败的URL
```

![参考图片 Spider_baiduyunpan_01](https://raw.githubusercontent.com/fansichao/images/master/markdown/Spider_baiduyunpan_01.png)

## 附件

### 参考链接

- [自动将资源添加到百度网盘中](https://github.com/tengzhangchao/BaiDuPan)
- [Scrapy\_延迟加载](https://zhuanlan.zhihu.com/p/72887277)

### 求赞赏

如果对您有帮助，还请支持我吧！(皮卡 qiu~~)

![支付宝微信_赞赏图片](https://raw.githubusercontent.com/fansichao/images/master/markdown/%E6%94%AF%E4%BB%98%E5%AE%9D%E5%BE%AE%E4%BF%A1_%E8%B5%9E%E8%B5%8F%E5%9B%BE%E7%89%87.png)

### 免责说明

1. 非商业用途.
2. 如有侵犯您的合法权益或违法违规，请提供相关有效书面证明与侵权页面链接联系我们进行删除。感谢您的支持
