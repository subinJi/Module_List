# Overwatch_Ranker_Crawling

## main.py
```python3
import hero  # 옵치 영웅 이름, 포지션 가져옴
import driver  # webdriver 설정
import opgg

driver = driver.set_option()

heroes = hero.get_list(driver)
ranker_id = opgg.ranker_info(driver)

print(len(ranker_id))
print(ranker_id)
```

<br>

## driver.py
```python3
from selenium import webdriver


def set_option():
    options = webdriver.ChromeOptions()
    options.add_argument('headless')
    options.add_argument('window-size=1920x1080')
    options.add_argument('disable-gpu')
    options.add_argument('lang=ko_KR')

    driver = webdriver.Chrome(executable_path='c:/chromedriver.exe', options=options)
    # driver.implicitly_wait(3)

    return driver
```

<br>

## hero.py
```python3
import requests
from bs4 import BeautifulSoup


def get_list(driver):
    url = "https://playoverwatch.com/ko-kr/heroes/"
    hero_list = {"TANK": [], "DAMAGE": [], "SUPPORT": []}

    # 크롤링 시작
    html = requests.get(url).text
    soup = BeautifulSoup(html, 'html.parser')

    hero_div = soup.find_all('div', class_='hero-portrait-detailed-container')

    for hero in hero_div:
        hero_position = hero.get('data-groups')[2:-2]
        hero_name = hero.find('span', class_='portrait-title').text
        hero_list[hero_position].append(hero_name)

    return hero_list
```

<br>

## opgg.py
```python3
from bs4 import BeautifulSoup
import requests


def ranker_detail(user_id):
    url = f"https://overwatch.op.gg/detail/overview/{user_id}"
    html = requests.get(url).text
    soup = BeautifulSoup(html, 'html.parser')

    if soup.find('div', class_="profile-not-found") is not None:  # 프로필 비공개일 때
        pass
    else:
        hero_list = soup.find_all('td', class_="ContentCell-Hero")
        print(hero_list)


def ranker_info(driver):
    page_num = 1
    id_list = []
    while True:
        url = f'https://overwatch.op.gg/leaderboards?platform=pc&role_id=1&page={page_num}'
        driver.get(url)
        soup = BeautifulSoup(driver.page_source, 'html.parser')

        tbody = soup.find('table', class_='LeaderBoardsTable').tbody
        lst = tbody.find_all('tr')
        for tr in lst:
            # 유저 고유번호
            user_id = tr.get('data-uid')
            # 유저 닉네임
            user_nickname = tr.find('td', class_="ContentCell-Player").a.b.text
            # 유저 레벨
            user_level = tr.find('td', class_="ContentCell-Player").a.em.text.split(" ")[1]
            # 랭겜 점수
            rank_score = int(tr.find('td', class_='ContentCell-SkillRating').text.strip())

            ranker_detail(user_id)

            if rank_score < 4000:
                print(f'{page_num}페이지 크롤링 완료')
                return id_list
            id_list.append(tr.get('data-uid'))
        print(f'{page_num}페이지 크롤링 완료')
        page_num += 1
```
