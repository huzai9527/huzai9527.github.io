---
title: python爬取最新更新的小说并发送到你的邮箱
date: 2018-11-17 15:07:29
tags: python
---
## 数据获取---Spider()
### 找目标网站，该网站是你看小说的网站，分析该网站的结构方便你对内容的抓取
  ![1.png](https://i.loli.net/2018/11/17/5befc2f9dd2a9.png)
  这里我获取最新章节的时间、标题以及标题的连接
  ![2.png](https://i.loli.net/2018/11/17/5befc38daf280.png)
  这里获取内容
### 编写spider方法，确定他的返回值，这里我返回的是一个list，包括更新的时间、标题、内容
- 方法中需要导入的包 **requests** **bs4** **re** 
``` bash
def spider():
    list = []
    response = requests.get('https://www.xbiquge6.com/13_13134/')
    response.encoding = ('utf-8')
    html = response.text
    html = BeautifulSoup(html, 'html.parser')
    time = html.select('div#info p:nth-of-type(3)').__getitem__(0).text[5:]
    title = html.select('div#info p:nth-of-type(4) a[href]').__getitem__(0).text
    href = html.select('div#info p:nth-of-type(4) a[href]').__getitem__(0)
    # print(title)
    pattern = re.compile(r'href="(.+?)"')
    href = re.findall(pattern, href.__str__()).__getitem__(0)
    href = "https://www.xbiquge6.com" + href
    response = requests.get(href)
    response.encoding = ('utf-8')
    html = BeautifulSoup(response.text, 'html.parser')
    content = html.select('div#content')
    # print(content)
    list.append(title)
    list.append(content)
    list.append(time)
    return list
```
## 邮件发送---smtp()
### 首先先在你的邮箱中设置打开smtp服务
比如我的QQ邮箱，先进入邮箱->点击设置->点击账户->下滑找到smtp服务->点击开启服务->生成授权码（就是你在smtp方法中用到的password）
![PCO_6AO93%@2W$B}[GFGHI0 (1).png](https://i.loli.net/2018/11/17/5befc49990bec.png)
### 编写smtp方法，向我的邮箱发送小说，确定返回值是bool类型，成功为True，失败为False
```bash
def mail():
    list = spider();
    ret = True
    try:
        mail_msg = list.__getitem__(1).__str__()
        msg = MIMEText(mail_msg, 'html', 'utf-8')
        msg['From'] = formataddr(['huzai', my_sender])
        msg['To'] = formataddr(['huzai', receiver])
        msg['Subject'] = list.__getitem__(0)
        server = smtplib.SMTP_SSL('smtp.qq.com', 465)
        server.login(my_sender, my_pwd)
        server.sendmail(my_sender, [receiver], msg.as_string())
        server.quit()
    except Exception:
        ret = False
    return ret
```

## 上传脚本到服务器
### 使用xftp将写好的smtp.py上传到你的云服务器上
![3.png](https://i.loli.net/2018/11/17/5befc6acf033d.png)
直接拖进去就行
### 这里注意保证你的服务器上的python版本和你本机一致，且需要的包已经安装
- 如果你的服务器上的版本是2.*的可以运行下面代码安装python3
```bash
sudo apt-get remove python
sudo apt-get install python3
sudo apt autoremove
```
### 用xshell进入服务器试着运行
![TIM图片20181117155505.png](https://i.loli.net/2018/11/17/5befc966d6b17.png)
## 在服务器端设置定时执行
### 确保你安装了crontab（ubuntu默认安装）
cron命名解析：执行的时间 + 执行的用户 + 执行的命令 
![4.png](https://i.loli.net/2018/11/17/5befc8af89fb3.png)
### 查看原有的cron
```bash
cat /etc/crontab
```
![TIM图片20181117155728.png](https://i.loli.net/2018/11/17/5befc9f6040d2.png)
### 编辑你的程序
```bash
sudo nano /etc/crontab
```
编写你的命令，每天14:58给我发送邮件，这里根据你看的小说的更新时间设置，一天几更在大约什么时间等等
```bash
58 14 * * * root python3 smtp.py
```
编辑好了再次查看cron是否已经写入，我这里已经写入
![TIM图片20181117160221.png](https://i.loli.net/2018/11/17/5befcb198cbae.png)
重启crontab服务
```bash
service cron restart
```
## 静静的等待14:58的到来，查看邮箱
- 邮件收到了最新更新的哦
![TIM图片20181117160515.png](https://i.loli.net/2018/11/17/5befcbd7281ec.png)
