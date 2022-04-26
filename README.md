mport re
import requests
from urllib.parse import unquote, urlencode
import time
from selenium import webdriver
#抓包地址 要的内容是什么
#通过开发者工具可以找到
#获取的地址是已经编码过的
#发送请求
#用户信息

url = 'https://book.qidian.com/info/1033512662/#Catalog'
requests.get(url)
headers = {
    'cookie': 'douyin.com; ttwid=1%7C-KMrOhTUYAmtKrY37g0yg0YIDJbT8puStBYizylZwOc%7C1650635265%7C9f9dea74b438e8c1375ff0746983a140322dafa75261fad8cf2d6debd12a4f2d; _tea_utm_cache_6383=undefined; passport_csrf_token=62bcdb4a62e4165d9125d6a2240c9b3b; passport_csrf_token_default=62bcdb4a62e4165d9125d6a2240c9b3b; s_v_web_id=verify_l2ahmb74_A1sifWMg_RiGh_4LLp_B3TU_LHqmJWT0UWCn; _tea_utm_cache_1300=undefined; ttcid=b2a01c0bdbe94a85a163f7544c73ba0f26; THEME_STAY_TIME=299532; IS_HIDE_THEME_CHANGE=1; _tea_utm_cache_2285=undefined; pwa_guide_count=3; douyin.com; strategyABtestKey=1650805286.719; AVATAR_FULL_LOGIN_GUIDE_TIMESTAMP=1650805286644; AVATAR_FULL_LOGIN_GUIDE_COUNT=1; odin_tt=71875ff938fa859ad3bfc189a8b62dbeb4825c44747053e95a8c55232a772e85370e2af25dfd6770bc4adeeeae049873ae422b0ee75e1d0b92bc64d7a6634ad8; __ac_nonce=062655167000f6c3ca763; __ac_signature=_02B4Z6wo00f01ZLXIpwAAIDBEtXY3Dmte82S9yYAAAbRXv5NofTAvn0gQ.r08I2ijz9PdjBczDozjYSUx6GiqUCsd2Id.2t8Oc9Qpx4xsRQoOtTzfdLgbBsOXREVusgaf.YsK760zEKX9rE7ba; msToken=vYo7xOay7rpHE6iKNOF5Q1H0sy8PxG7J0_djF0II2-rF2ob250iEtTlYk9LiYHkPbI-RTzn7ow3hUfgU3Kmp3Ya8nSZ-7nQ7Eg6BZoIVOQM32W4GUqnnIUDoIYvIRzwA; home_can_add_dy_2_desktop=1; tt_scid=u43esc.I6Rc6PrEb6.YGjYWqXhBUeQOSa7wggEVb1jBT30DlRcsYTNc-HbPN72v433cc; msToken=piL6w8ENr5RXvzwKdbLhBy84f0YKQCWxHOVqfKMihyucWoFfgibED9q6RBnYPUGP73EdnoJTHa8WDSg9CbXyz7rvrsrCtPjvkVt0bothd_iQQSwT6y_AqQsFPjAdcZpW',
    'referer':'https://book.qidian.com',
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.60 Safari/537.36'
         }
list_html = requests.get(url, headers=headers).text
info_list = re.findall('<h2 class="book_name"><a href="(.*?)".*?">(.*?)</a></h2>',list_html,re.S)
print(info_list)
for link,titile in info_list:
    link = 'https:' + link
    response = requests.get(link, headers=headers)
    html_data = response.text
    text = re.findall('<div class="read-content j_readContent" id=".*?">(.*?)</div>',html_data,re.S)[0]
    #对已有的数据进行处理
    text = text.replace('<p>','\n')
with open('只有噪音.txt',mode = 'a',encoding='utf-8') as f:
    f.write(text)
print(text)
