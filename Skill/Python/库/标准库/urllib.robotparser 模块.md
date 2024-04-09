##### urllib.robotparser 模块
```python
# 解析类
class urllib.robotparser.RobotFileParser(url='')

# 实例方法
set_url(url)
	# 设置指向 robots.txt 文件的 URL。
read()
	# 读取 robots.txt URL 并将其输入解析器。
parse(lines)
	# 解析行参数。
can_fetch(useragent, url)
	# 如果允许 useragent 按照被解析 robots.txt 文件中的规则来获取 url 则返回 True。
```
##### 示例
```python
from urllib.robotparser import RobotFileParser

# 创建 RobotFileParser 对象并指定 robots.txt 的 URL
robot_parser = RobotFileParser()
robot_parser.set_url("https://www.example.com/robots.txt")

# 读取并解析 robots.txt 文件
robot_parser.read()

# 检查 User-Agent 是否允许访问特定的 URL
user_agent = "MyBot"
url = "https://www.example.com/page.html"

if robot_parser.can_fetch(user_agent, url):
    print(f"{user_agent} is allowed to access {url}")
else:
    print(f"{user_agent} is not allowed to access {url}")

```