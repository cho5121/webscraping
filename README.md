# webscraping
import requests
from bs4 import BeautifulSoup
import csv

# 한글요청 header
headers = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) \
    AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.89 \
        Safari/537.36","Accept-Language":"ko-KR,ko"}

# soup 개체
url = "https://euler.synap.co.kr/prob_list.php"
res = requests.get(url, headers=headers)
res.raise_for_status()
soup = BeautifulSoup(res.text, "lxml")
res.raise_for_status()

filename = "temp1.csv"
f = open(filename, "w", encoding="utf-8-sig", newline="")
writer = csv.writer(f)


# print(len(res.text))  # 가져오는지 확인
# # print(res.text)

table = soup.find("table", attrs={"class":"grid"})
trs = table.find_all("tr")
for index, tr in enumerate(trs):   #enumerate를 사용하면 해당값의 해당값의 index를 알 수 있다.
    if index > 0: # 제목 의미없어 제거
        tds = tr.find_all("td")
        # sequence = tds[0].text.strip()
        # 설명 = tds[1].get_text().strip()
        # solv_num = tds[2].get_text().strip()
        # latest = tds[3].text.strip()
        # or
        data = [td.get_text().strip() for td in tds]

        print(data)
        writer.writerow(data)

        



   
