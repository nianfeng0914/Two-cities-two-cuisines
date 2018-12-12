# Two cities, two cuisines
All the original code (.ipynb) for our group case
## Group Members

LIU Gang    	55454180

NIAN Feng    	55459506

TAO Siyu 		  55418296

WANG Man 		  55289586

## Introduction
- Majority of Chinese cannot tell the difference between Sichuan Cuisine and Hunan Cuisine in terms of flavor.
- If a Sichuan restaurant want to expand market in Changsha
  - How can you develop a differentiation strategy to make yourself outstanding
  - Natives tend to believe local cuisine more delicious than others

## Our research questions
- Which has the quantitative superiority in Sichuan and Chengdu respectively?
- Which has higher grades in taste, service and environment in Sichuan and Chengdu respectively?
- Which owns higher proportion in various popular business districts?
- Is there any other hidden reasons we can get from data, to explain why Chuan cuisine wins more popularity?

## Data source
The number of Sichuan restaurants in Chengdu [URL](https://www.dianping.com/search/keyword/8/0_川菜)

Ranked by popularity and the respective score for taste，environment，service [URL](http://www.dianping.com/search/keyword/8/10_川菜/o2p1)

The amount of Hunan restaurant in Chengdu [URL](https://www.dianping.com/search/keyword/8/0_湘菜)

Ranked by popularity and the respective score for taste，environment，service [URL](http://www.dianping.com/search/keyword/8/10_湘菜/o2p1)

The number of Sichuan restaurants in Chengdu [URL](https://www.dianping.com/search/keyword/8/0_川菜)

Ranked by popularity and the respective score for taste，environment，service [URL](http://www.dianping.com/search/keyword/8/10_川菜/o2p1)

The amount of Hunan restaurant in Chengdu [URL](https://www.dianping.com/search/keyword/8/0_湘菜)

Ranked by popularity and the respective score for taste，environment，service [URL](http://www.dianping.com/search/keyword/8/10_湘菜/o2p1)

## Our original codes to crawl the scores for example
```Python
headers = {'Host': 'www.dianping.com',
    'Referer': 'http://www.dianping.com/shop/22711693',
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.95 Safari/535.19',
    'Accept-Encoding': 'gzip'}
titles=[]
kouweis=[]
fuwus=[]
huanjings=[]

pages=[str(i) for i in range(1,51)]
for page in pages:
    source = requests.get('http://www.dianping.com/search/keyword/344/10_川菜/o2p'+page,headers=headers) 
    soup=bs.BeautifulSoup(source.content , features='html.parser')
    sleep(randint(8,15))
    
    containers=soup.find_all('div',class_='txt')
    for container in containers:
        for title in container.find_all('h4'):
            titles.append(title.text.strip())

print(titles)
####################################
for row in soup.find_all('span',class_='comment-list'):
        
    kouwei=row.select('span:nth-of-type(1)')
        
    for i in kouwei:
        kouwei2=i.get_text()
        kouweis.append(kouwei2)            

print(kouweis)
###################################
for row in soup.find_all('span',class_='comment-list'):
        
    fuwu=row.select('span:nth-of-type(3)')
        
    for i in fuwu:
        fuwu2=i.get_text()
        fuwus.append(fuwu2)
print(fuwus)
####################################
for row in soup.find_all('span',class_='comment-list'):
        
    huanjing=row.select('span:nth-of-type(2)')
        
    for i in huanjing:
        huanjing2=i.get_text()
        huanjings.append(huanjing2)
print(huanjings)
###################################
data_4={
    '名字':titles,
    '口味':kouweis,
    '環境':huanjings,
    '服務':fuwus
}
pd_changshachuancai=pd.DataFrame.from_dict(data_4,orient='index').transpose()
print(pd_changshachuancai.info())
```

