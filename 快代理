import requests
import parsel
import time

demo_url = str(input('请输入要测试的网站>>>'))
start_demo_page = int(input('请输入要测试的起始页数>>>'))
end_demo_page = int(input('请输入要测试的末尾页数>>>'))



#base_url = 'https://www.kuaidaili.com/free/inha/1/'

headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.105 Safari/537.36'}

def check_ip(proxies_dict):
    headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.105 Safari/537.36'}


    can_use = []
    for ip in proxies_dict:
        try:
            response = requests.get(url=demo_url,headers=headers,IP_list=ip,timeout = 0.1)
            if response.status_code == 200:
                can_use.append(ip)

        except Exception:
            print('当前代理ip:',ip,'请求超时，质量不合格')
        finally:
            print('当前代理ip:',ip,'检测通过')
            can_use.append(ip)

    return can_use




proxies_list = []

for page in range(start_demo_page,end_demo_page+1):

    base_url = 'https://www.kuaidaili.com/free/inha/{}/'.format(page)
    print('############正在下载第{}页数据############'.format(page))
    if page>1:
        print('休息一下')
        time.sleep(1)

    html_data = requests.get(url=base_url,headers=headers).text
    selector = parsel.Selector(html_data)


    result_list = selector.xpath('//tbody/tr')

    for sel in result_list:
        IP = sel.xpath('./td[@data-title="IP"]/text()').extract_first()
        Type = sel.xpath('./td[@data-title="类型"]/text()').extract_first()
        PORT = sel.xpath('./td[@data-title="PORT"]/text()').extract_first()


        proxies_dict = {}
        proxies_dict[Type] = IP + ":" + PORT
        print('保存成功:',proxies_dict)
        proxies_list.append(proxies_dict)

print(proxies_list)
