#import library yang digunakan
import requests
import pandas as pd
from bs4 import BeautifulSoup

#membuat koneksi dengan wikipedia
url = 'https://id.wikipedia.org/wiki/Demografi_Indonesia'
r = requests.get(url)
soup = BeautifulSoup(r.text, 'html.parser')

#mencari table yang akan diambil
table = soup.find('table', {'class' : 'wikitable sortable'})

#mendapatkan header
header = [th.text.rstrip() for th in table.findAll('th')]

#mendapatkan isi columns
cl1 = []
cl2 = []
cl3 = []
cl4 = []
cl5 = []
cl6 = []
cl7 = []
cl8 = []
cl9 = []

for i in table.findAll('tr'):
    cell = i.findAll('td')
    if len(cell) == 9 :
        cl1.append(cell[0].find(text = True))
        cl2.append(cell[1].find('a').text)
        cl3.append(cell[2].find(text = True))
        cl4.append(cell[3].find(text = True))
        cl5.append(cell[4].find(text = True))
        cl6.append(cell[5].find(text = True))
        cl7.append(cell[6].find(text = True))
        cl8.append(cell[7].find(text = True))
        cl9.append(cell[8].find(text = True))

#dictionary sementara
d = dict([(x,0) for x in header])

#membuat dataframe dari data yang sudah diambil
df_data = pd.DataFrame(d)
df_data = df_data.drop(['Lambang','Kode ISO[4]', 'Status khusus'],axis = 1)
df_data = df_data.rename(columns = {'Populasi[5]':'Populasi', 'Luas (km²)[6]':'Luas km'})

#menyimpan menjadi csv
df_data.to_csv("Indonesia_Demography_by_Province.csv", index = False, header = True)
