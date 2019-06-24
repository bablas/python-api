
# WeatherPy
----

### Analysis
* As expected, the weather becomes significantly warmer as one approaches the equator (0 Deg. Latitude). More interestingly, however, is the fact that the southern hemisphere tends to be warmer this time of year than the northern hemisphere. This may be due to the tilt of the earth.
* There is no strong relationship between latitude and cloudiness. However, it is interesting to see that a strong band of cities sits at 0, 80, and 100% cloudiness.
* There is no strong relationship between latitude and wind speed. However, in northern hemispheres there is a flurry of cities with over 20 mph of wind.

---

#### Note
* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.


```python
# Dependencies and Setup
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import requests
import time

# Import API key
# import api_keys
# print(api_keys)

# Incorporated citipy to determine city based on latitude and longitude
from citipy import citipy

# Output File (CSV)
output_data_file = "output_data/cities.csv"

# Range of latitudes and longitudes
lat_range = (-90, 90)
lng_range = (-180, 180)
```

## Generate Cities List

### Perform API Calls
* Perform a weather check on each city using a series of successive API calls.
* Include a print log of each city as it'sbeing processed (with the city number and city name).



```python
# List for holding lat_lngs and cities
lat_lngs = []
cities = []

# Create a set of random lat and lng combinations
lats = np.random.uniform(low=-90.000, high=90.000, size=1500)
lngs = np.random.uniform(low=-180.000, high=180.000, size=1500)
lat_lngs = zip(lats, lngs)

# Identify nearest city for each lat, lng combination
for lat_lng in lat_lngs:
    city = citipy.nearest_city(lat_lng[0], lat_lng[1]).city_name

    # If the city is unique, then add it to a our cities list
    if city not in cities:
        cities.append(city)

# Print the city count to confirm sufficient count
len(cities)
cities
```




    ['jamestown',
     'kashan',
     'bengkulu',
     'cherskiy',
     'punta arenas',
     'kosh-agach',
     'bluff',
     'saint george',
     'broome',
     'rikitea',
     'butaritari',
     'ribeira grande',
     'marsa matruh',
     'ushuaia',
     'amderma',
     'bredasdorp',
     'nizhneyansk',
     'san luis',
     'hamilton',
     'tiksi',
     'narsaq',
     'busselton',
     'katsuura',
     'georgetown',
     'abu samrah',
     'yumen',
     'port alfred',
     'longyearbyen',
     'kiisa',
     'leningradskiy',
     'arlit',
     'marzuq',
     'illoqqortoormiut',
     'brodokalmak',
     'saskylakh',
     'asau',
     'eenhana',
     'lorengau',
     'tasiilaq',
     'cape town',
     'pisco',
     'mizdah',
     'morrisburg',
     'hasaki',
     'barentsburg',
     'swan hill',
     'warqla',
     'meulaboh',
     'yuancheng',
     'nikolskoye',
     'ures',
     'rengo',
     'taganak',
     'qeshm',
     'cabo san lucas',
     'aksarka',
     'nabire',
     'ojuelos de jalisco',
     'sorland',
     'batie',
     'atuona',
     'albany',
     'alamogordo',
     'khatanga',
     'flinders',
     'omboue',
     'norman wells',
     'nanortalik',
     'yellowknife',
     'ometepec',
     'puerto ayora',
     'kainantu',
     'vaini',
     'taolanaro',
     'saint anthony',
     'hilo',
     'harlingen',
     'poum',
     'toliary',
     'kodiak',
     'tura',
     'thompson',
     'severobaykalsk',
     'ilmatsalu',
     'shediac',
     'coquimbo',
     'truckee',
     'shaoguan',
     'cam ranh',
     'zephyrhills',
     'takapau',
     'mataura',
     'aklavik',
     'touros',
     'fukue',
     'hithadhoo',
     'nemuro',
     'samusu',
     'yerbogachen',
     'attawapiskat',
     'gamba',
     'ocampo',
     'cuamba',
     'ancud',
     'port elizabeth',
     'muros',
     'vilhena',
     'herat',
     'srednekolymsk',
     'manzil salim',
     'anadyr',
     'kapaa',
     'tevaitoa',
     'victoria',
     'yulara',
     'morganton',
     'mahebourg',
     'dikson',
     'ballina',
     'tucupita',
     'ambulu',
     'berlevag',
     'havoysund',
     'pevek',
     'lebu',
     'iqaluit',
     'mount gambier',
     'souillac',
     'tuggurt',
     'peterhead',
     'esperance',
     'pompeia',
     'namibe',
     'guane',
     'chokurdakh',
     'madona',
     'cidreira',
     'arraias',
     'bambous virieux',
     'port blair',
     'airai',
     'sentyabrskiy',
     'coihaique',
     'santa catalina',
     'clyde river',
     'hailar',
     'qabis',
     'salvador',
     'dubrovnik',
     'ambilobe',
     'mys shmidta',
     'arraial do cabo',
     'vila velha',
     'geraldton',
     'necochea',
     'bagnan',
     'caapucu',
     'kaeo',
     'warrington',
     'paradwip',
     'vaitupu',
     'youkounkoun',
     'ust-ordynskiy',
     'auki',
     'mar del plata',
     'togur',
     'yatou',
     'hami',
     'areosa',
     'new norfolk',
     'oranjemund',
     'sumbe',
     'te anau',
     'prescott',
     'pangnirtung',
     'hobart',
     'tuktoyaktuk',
     'dukstas',
     'baiao',
     'smithers',
     'troitskoye',
     'timmins',
     'ligayan',
     'berbera',
     'maniitsoq',
     'dzaoudzi',
     'gornoye loo',
     'grindavik',
     'paka',
     'hermanus',
     'bodden town',
     'carnarvon',
     'melchor de mencos',
     'torbay',
     'qaanaaq',
     'willowmore',
     'alotau',
     'chuy',
     'kalengwa',
     'vrede',
     'salalah',
     'kamenskoye',
     'belushya guba',
     'ordynskoye',
     'vangaindrano',
     'dunedin',
     'kyshtovka',
     'praia da vitoria',
     'raudeberg',
     'luderitz',
     'mrirt',
     'shaygino',
     'ponta do sol',
     'ilulissat',
     'laguna',
     'lagoa',
     'east london',
     'nishihara',
     'sunland park',
     'asnaes',
     'palmer',
     'zlobin',
     'phan rang',
     'barreirinhas',
     'hobyo',
     'sakakah',
     'upernavik',
     'sao joao da barra',
     'mirnyy',
     'mega',
     'barrow',
     'saint-philippe',
     'tawang',
     'jinchengjiang',
     'naifaru',
     'fairbanks',
     'alofi',
     'college',
     'rorvik',
     'moyale',
     'cambridge',
     'jalu',
     'kumluca',
     'gat',
     'lardos',
     'prince rupert',
     'hualmay',
     'provideniya',
     'olafsvik',
     'sao filipe',
     'curumani',
     'waterboro',
     'manokwari',
     'turukhansk',
     'san cristobal',
     'klaksvik',
     'dingle',
     'limbang',
     'guerrero negro',
     'texarkana',
     'constitucion',
     'bethel',
     'san policarpo',
     'innisfail',
     'lokosovo',
     'liverpool',
     'samalaeulu',
     'castro',
     'camacha',
     'makakilo city',
     'iquitos',
     'kavieng',
     'saleaula',
     'kaspiysk',
     'westport',
     'saint-joseph',
     'kingston',
     'itambacuri',
     'suntar',
     'evensk',
     'santa maria do para',
     'michigan city',
     'ahipara',
     'cacoal',
     'nestorion',
     'avarua',
     'baykit',
     'karamay',
     'beringovskiy',
     'saint-leu',
     'puerto quijarro',
     'huallanca',
     'quimper',
     'yokadouma',
     'adrar',
     'speightstown',
     'nome',
     'labuhan',
     'naze',
     'paamiut',
     'zhuhai',
     'almaznyy',
     'mongo',
     'xuddur',
     'boyolangu',
     'comodoro rivadavia',
     'prado',
     'saldanha',
     'tual',
     'margate',
     'novyy buyan',
     'dosso',
     'mandalgovi',
     'palabuhanratu',
     'bilibino',
     'mount isa',
     'bada',
     'opuwo',
     'lompoc',
     'road town',
     'atambua',
     'cao bang',
     'rawlins',
     'concordia',
     'bathsheba',
     'harper',
     'tarudant',
     'fuling',
     'matara',
     'aksu',
     'lata',
     'zyryanka',
     'buraydah',
     'krasnyy chikoy',
     'mawlaik',
     'great yarmouth',
     'wiwili',
     'moron',
     'sur',
     'narasannapeta',
     'kalmunai',
     'colac',
     'avera',
     'finnsnes',
     'tezu',
     'sattahip',
     'porto novo',
     'renqiu',
     'miyako',
     'iracoubo',
     'sillamae',
     'sembakung',
     'codrington',
     'helmsdale',
     'teguise',
     'bang saphan',
     'nelson bay',
     'guhagar',
     'flin flon',
     'namatanai',
     'florianopolis',
     'barra patuca',
     'linapacan',
     'kiruna',
     'hirara',
     'kloulklubed',
     'dolbeau',
     'kaitangata',
     'mpika',
     'bintulu',
     'shingu',
     'san patricio',
     'itarema',
     'vardo',
     'goalpara',
     'faanui',
     'otavi',
     'magui',
     'omaruru',
     'hollola',
     'franklin',
     'san juan',
     'thunder bay',
     'grand gaube',
     'roma',
     'selenginsk',
     'buala',
     'inhambane',
     'tuatapere',
     'buta',
     'dzilam gonzalez',
     'whitehorse',
     'milin',
     'puerto madryn',
     'bazarnyy karabulak',
     'chernyshevskiy',
     'kenai',
     'akyab',
     'fevralsk',
     'cururupu',
     'lar',
     'kemijarvi',
     'arman',
     'ixtapa',
     'ostrovnoy',
     'belyy yar',
     'junin',
     'chimbote',
     'pacific grove',
     'payo',
     'nakamura',
     'lipari',
     'khorramabad',
     'nampula',
     'dubbo',
     'burica',
     'vorselaar',
     'vostok',
     'larsnes',
     'lavrentiya',
     'beyneu',
     'spearfish',
     'axim',
     'wadi',
     'wellington',
     'port moresby',
     'vestmannaeyjar',
     'severo-kurilsk',
     'sahibganj',
     'sakyla',
     'araraquara',
     'ust-maya',
     'riyadh',
     'vao',
     'san jeronimo',
     'bonthe',
     'vila franca do campo',
     'caravelas',
     'bud',
     'batagay-alyta',
     'kimbe',
     'preobrazheniye',
     'new milford',
     'puerto del rosario',
     'chicama',
     'gambela',
     'outjo',
     'paita',
     'sesheke',
     'aksha',
     'santa isabel',
     'nhulunbuy',
     'ust-nera',
     'xining',
     'craig',
     'usinsk',
     'veraval',
     'motygino',
     'los llanos de aridane',
     'yeppoon',
     'raga',
     'leh',
     'verkhnyaya inta',
     'ciudad bolivar',
     'undory',
     'machilipatnam',
     'rongcheng',
     'jiazi',
     'cayenne',
     'inirida',
     'mul',
     'hue',
     'batagay',
     'merauke',
     'tsihombe',
     'jind',
     'barinitas',
     'beihai',
     'lamu',
     'northam',
     'sault sainte marie',
     'simbahan',
     'gheraseni',
     'pousat',
     'markova',
     'novyy redant',
     'bourges',
     'irpa irpa',
     'half moon bay',
     'betioky',
     'amalapuram',
     'skjervoy',
     'padang',
     'tulum',
     'gorlice',
     'peniche',
     'kudahuvadhoo',
     'kondopoga',
     'kelo',
     'mamedkala',
     'acapulco',
     'solnechnyy',
     'pimenta bueno',
     'rio gallegos',
     'terra roxa',
     'oni',
     'eureka',
     'muroto',
     'kahului',
     'verkhnetulomskiy',
     'boguchany',
     'lixourion',
     'komsomolskiy',
     'abrau-dyurso',
     'korla',
     'umzimvubu',
     'tashla',
     'carupano',
     'trang',
     'great bend',
     'the valley',
     'henties bay',
     'aflu',
     'ilhabela',
     'odweyne',
     'gebze',
     'saginaw',
     'viedma',
     'kokopo',
     'husavik',
     'manta',
     'qandala',
     'egvekinot',
     'manawar',
     'marystown',
     'sar-e pul',
     'soubre',
     'sitka',
     'otane',
     'bilma',
     'khani',
     'mackay',
     'rawson',
     'duz',
     'rabo de peixe',
     'tessalit',
     'pitkyaranta',
     'kangra',
     'tautira',
     'leninsk',
     'port keats',
     'panjakent',
     'liwale',
     'prainha',
     'ghanaur',
     'kobryn',
     'camabatela',
     'linhares',
     'freetown',
     'along',
     'jutai',
     'canhotinho',
     'mahanoro',
     'port hardy',
     'vestmanna',
     'lethem',
     'toamasina',
     'hawkesbury',
     'camana',
     'palu',
     'moose factory',
     'nienburg',
     'velika gorica',
     'camacupa',
     'grand centre',
     'grand river south east',
     'mouzakion']




```python
len(cities)
```




    577




```python
api_key = "dd2619e7db70a5d08a9a581d2b95028c"

url = "http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=" + api_key

cityname = []
clouds = []
country = []
dt = []
humidity = []
temp_max = []
lat = []
lon = []
wind_speed = []


print(f"Beginning Data Retrieval")
print(f"-------------------------------")


for city in cities:  
    try: 
        city_url = url + "&q=" + city
#         print(city_url)
        response = requests.get(city_url).json() 
        city = (response["name"])   
        cityname.append(response["name"])
        clouds.append(response["clouds"]["all"])
        country.append(response["sys"]["country"])
        dt.append(response["dt"])
        humidity.append(response["main"]["humidity"])
        temp_max.append(response["main"]["temp_max"])
        lat.append(response["coord"]["lat"])
        lon.append(response["coord"]["lon"])
        wind_speed.append(response["wind"]["speed"])
        
        print(f"Processing Record | {city}")
    except:
        print("City not found. Skiped")
    continue
    

print(f"-------------------------------")   
print(f"Processing Ended")
```

    Beginning Data Retrieval
    -------------------------------
    Processing Record | Jamestown
    Processing Record | Kashan
    City not found. Skiped
    Processing Record | Cherskiy
    Processing Record | Punta Arenas
    Processing Record | Kosh-Agach
    Processing Record | Bluff
    Processing Record | Saint George
    Processing Record | Broome
    Processing Record | Rikitea
    Processing Record | Butaritari
    Processing Record | Ribeira Grande
    Processing Record | Marsa Matruh
    Processing Record | Ushuaia
    City not found. Skiped
    Processing Record | Bredasdorp
    City not found. Skiped
    Processing Record | San Luis
    Processing Record | Hamilton
    Processing Record | Tiksi
    Processing Record | Narsaq
    Processing Record | Busselton
    Processing Record | Katsuura
    Processing Record | Georgetown
    Processing Record | Abu Samrah
    Processing Record | Yumen
    Processing Record | Port Alfred
    Processing Record | Longyearbyen
    Processing Record | Kiisa
    Processing Record | Leningradskiy
    Processing Record | Arlit
    Processing Record | Marzuq
    City not found. Skiped
    Processing Record | Brodokalmak
    Processing Record | Saskylakh
    City not found. Skiped
    Processing Record | Eenhana
    Processing Record | Lorengau
    Processing Record | Tasiilaq
    Processing Record | Cape Town
    Processing Record | Pisco
    Processing Record | Mizdah
    Processing Record | Morrisburg
    Processing Record | Hasaki
    City not found. Skiped
    Processing Record | Swan Hill
    City not found. Skiped
    Processing Record | Meulaboh
    City not found. Skiped
    Processing Record | Nikolskoye
    Processing Record | Ures
    Processing Record | Rengo
    Processing Record | Taganak
    Processing Record | Qeshm
    Processing Record | Cabo San Lucas
    Processing Record | Aksarka
    Processing Record | Nabire
    Processing Record | Ojuelos de Jalisco
    Processing Record | Sorland
    Processing Record | Batie
    Processing Record | Atuona
    Processing Record | Albany
    Processing Record | Alamogordo
    Processing Record | Khatanga
    Processing Record | Flinders
    Processing Record | Omboue
    Processing Record | Norman Wells
    Processing Record | Nanortalik
    Processing Record | Yellowknife
    Processing Record | Ometepec
    Processing Record | Puerto Ayora
    Processing Record | Kainantu
    Processing Record | Vaini
    City not found. Skiped
    Processing Record | Saint Anthony
    Processing Record | Hilo
    Processing Record | Harlingen
    Processing Record | Poum
    City not found. Skiped
    Processing Record | Kodiak
    Processing Record | Tura
    Processing Record | Thompson
    Processing Record | Severobaykalsk
    Processing Record | Ilmatsalu
    Processing Record | Shediac
    Processing Record | Coquimbo
    Processing Record | Truckee
    Processing Record | Shaoguan
    Processing Record | Cam Ranh
    Processing Record | Zephyrhills
    Processing Record | Takapau
    Processing Record | Mataura
    Processing Record | Aklavik
    Processing Record | Touros
    Processing Record | Fukue
    Processing Record | Hithadhoo
    Processing Record | Nemuro
    City not found. Skiped
    Processing Record | Yerbogachen
    City not found. Skiped
    Processing Record | Gamba
    Processing Record | Ocampo
    Processing Record | Cuamba
    Processing Record | Ancud
    Processing Record | Port Elizabeth
    Processing Record | Muros
    Processing Record | Vilhena
    Processing Record | Herat
    Processing Record | Srednekolymsk
    Processing Record | Manzil Salim
    Processing Record | Anadyr
    Processing Record | Kapaa
    Processing Record | Tevaitoa
    Processing Record | Victoria
    Processing Record | Yulara
    Processing Record | Morganton
    Processing Record | Mahebourg
    Processing Record | Dikson
    Processing Record | Ballina
    Processing Record | Tucupita
    Processing Record | Ambulu
    Processing Record | Berlevag
    Processing Record | Havoysund
    Processing Record | Pevek
    Processing Record | Lebu
    Processing Record | Iqaluit
    Processing Record | Mount Gambier
    Processing Record | Souillac
    City not found. Skiped
    Processing Record | Peterhead
    Processing Record | Esperance
    Processing Record | Pompeia
    Processing Record | Namibe
    Processing Record | Guane
    Processing Record | Chokurdakh
    Processing Record | Madona
    Processing Record | Cidreira
    Processing Record | Arraias
    Processing Record | Bambous Virieux
    Processing Record | Port Blair
    Processing Record | Airai
    City not found. Skiped
    Processing Record | Coihaique
    Processing Record | Santa Catalina
    Processing Record | Clyde River
    Processing Record | Hailar
    City not found. Skiped
    Processing Record | Salvador
    Processing Record | Dubrovnik
    Processing Record | Ambilobe
    City not found. Skiped
    Processing Record | Arraial do Cabo
    Processing Record | Vila Velha
    Processing Record | Geraldton
    Processing Record | Necochea
    Processing Record | Bagnan
    Processing Record | Caapucu
    Processing Record | Kaeo
    Processing Record | Warrington
    City not found. Skiped
    City not found. Skiped
    Processing Record | Youkounkoun
    Processing Record | Ust-Ordynskiy
    Processing Record | Auki
    Processing Record | Mar del Plata
    Processing Record | Togur
    Processing Record | Yatou
    Processing Record | Hami
    Processing Record | Areosa
    Processing Record | New Norfolk
    Processing Record | Oranjemund
    Processing Record | Sumbe
    Processing Record | Te Anau
    Processing Record | Prescott
    Processing Record | Pangnirtung
    Processing Record | Hobart
    Processing Record | Tuktoyaktuk
    Processing Record | Dukstas
    Processing Record | Baiao
    Processing Record | Smithers
    Processing Record | Troitskoye
    Processing Record | Timmins
    Processing Record | Ligayan
    City not found. Skiped
    Processing Record | Maniitsoq
    Processing Record | Dzaoudzi
    Processing Record | Gornoye Loo
    Processing Record | Grindavik
    Processing Record | Paka
    Processing Record | Hermanus
    Processing Record | Bodden Town
    Processing Record | Carnarvon
    Processing Record | Melchor de Mencos
    Processing Record | Torbay
    Processing Record | Qaanaaq
    Processing Record | Willowmore
    City not found. Skiped
    Processing Record | Chuy
    Processing Record | Kalengwa
    Processing Record | Vrede
    Processing Record | Salalah
    City not found. Skiped
    City not found. Skiped
    Processing Record | Ordynskoye
    Processing Record | Vangaindrano
    Processing Record | Dunedin
    Processing Record | Kyshtovka
    Processing Record | Praia da Vitoria
    Processing Record | Raudeberg
    Processing Record | Luderitz
    City not found. Skiped
    Processing Record | Shaygino
    Processing Record | Ponta do Sol
    Processing Record | Ilulissat
    Processing Record | Laguna
    Processing Record | Lagoa
    Processing Record | East London
    Processing Record | Nishihara
    Processing Record | Sunland Park
    Processing Record | Asnaes
    Processing Record | Palmer
    Processing Record | Zlobin
    City not found. Skiped
    Processing Record | Barreirinhas
    Processing Record | Hobyo
    City not found. Skiped
    Processing Record | Upernavik
    Processing Record | Sao Joao da Barra
    Processing Record | Mirnyy
    Processing Record | Mega
    Processing Record | Barrow
    Processing Record | Saint-Philippe
    Processing Record | Tawang
    City not found. Skiped
    Processing Record | Naifaru
    Processing Record | Fairbanks
    Processing Record | Alofi
    Processing Record | College
    Processing Record | Rorvik
    Processing Record | Moyale
    Processing Record | Cambridge
    Processing Record | Jalu
    Processing Record | Kumluca
    Processing Record | Gat
    Processing Record | Lardos
    Processing Record | Prince Rupert
    Processing Record | Hualmay
    Processing Record | Provideniya
    City not found. Skiped
    Processing Record | Sao Filipe
    Processing Record | Curumani
    Processing Record | Waterboro
    Processing Record | Manokwari
    Processing Record | Turukhansk
    Processing Record | San Cristobal
    Processing Record | Klaksvik
    Processing Record | Dingle
    Processing Record | Limbang
    Processing Record | Guerrero Negro
    Processing Record | Texarkana
    Processing Record | Constitucion
    Processing Record | Bethel
    Processing Record | San Policarpo
    Processing Record | Innisfail
    Processing Record | Lokosovo
    Processing Record | Liverpool
    City not found. Skiped
    Processing Record | Castro
    Processing Record | Camacha
    Processing Record | Makakilo City
    Processing Record | Iquitos
    Processing Record | Kavieng
    City not found. Skiped
    Processing Record | Kaspiysk
    Processing Record | Westport
    Processing Record | Saint-Joseph
    Processing Record | Kingston
    Processing Record | Itambacuri
    Processing Record | Suntar
    Processing Record | Evensk
    Processing Record | Santa Maria do Para
    Processing Record | Michigan City
    Processing Record | Ahipara
    Processing Record | Cacoal
    City not found. Skiped
    Processing Record | Avarua
    Processing Record | Baykit
    City not found. Skiped
    Processing Record | Beringovskiy
    Processing Record | Saint-Leu
    Processing Record | Puerto Quijarro
    Processing Record | Huallanca
    Processing Record | Quimper
    Processing Record | Yokadouma
    Processing Record | Adrar
    Processing Record | Speightstown
    Processing Record | Nome
    Processing Record | Labuhan
    Processing Record | Naze
    Processing Record | Paamiut
    Processing Record | Zhuhai
    Processing Record | Almaznyy
    Processing Record | Mongo
    Processing Record | Xuddur
    Processing Record | Boyolangu
    Processing Record | Comodoro Rivadavia
    Processing Record | Prado
    Processing Record | Saldanha
    Processing Record | Tual
    Processing Record | Margate
    Processing Record | Novyy Buyan
    Processing Record | Dosso
    Processing Record | Mandalgovi
    City not found. Skiped
    Processing Record | Bilibino
    Processing Record | Mount Isa
    Processing Record | Bada
    Processing Record | Opuwo
    Processing Record | Lompoc
    Processing Record | Road Town
    Processing Record | Atambua
    Processing Record | Cao Bang
    Processing Record | Rawlins
    Processing Record | Concordia
    Processing Record | Bathsheba
    Processing Record | Harper
    City not found. Skiped
    Processing Record | Fuling
    Processing Record | Matara
    Processing Record | Aksu
    Processing Record | Lata
    Processing Record | Zyryanka
    Processing Record | Buraydah
    Processing Record | Krasnyy Chikoy
    Processing Record | Mawlaik
    Processing Record | Great Yarmouth
    Processing Record | Wiwili
    Processing Record | Moron
    Processing Record | Sur
    Processing Record | Narasannapeta
    Processing Record | Kalmunai
    Processing Record | Colac
    Processing Record | Avera
    Processing Record | Finnsnes
    Processing Record | Tezu
    Processing Record | Sattahip
    Processing Record | Porto Novo
    Processing Record | Renqiu
    Processing Record | Miyako
    Processing Record | Iracoubo
    Processing Record | Sillamae
    Processing Record | Sembakung
    Processing Record | Codrington
    Processing Record | Helmsdale
    Processing Record | Teguise
    Processing Record | Bang Saphan
    Processing Record | Nelson Bay
    Processing Record | Guhagar
    Processing Record | Flin Flon
    Processing Record | Namatanai
    Processing Record | Florianopolis
    Processing Record | Barra Patuca
    City not found. Skiped
    Processing Record | Kiruna
    Processing Record | Hirara
    Processing Record | Kloulklubed
    City not found. Skiped
    Processing Record | Kaitangata
    Processing Record | Mpika
    Processing Record | Bintulu
    Processing Record | Shingu
    Processing Record | San Patricio
    Processing Record | Itarema
    Processing Record | Vardo
    Processing Record | Goalpara
    Processing Record | Faanui
    Processing Record | Otavi
    City not found. Skiped
    Processing Record | Omaruru
    Processing Record | Hollola
    Processing Record | Franklin
    Processing Record | San Juan
    Processing Record | Thunder Bay
    Processing Record | Grand Gaube
    Processing Record | Rome
    Processing Record | Selenginsk
    Processing Record | Buala
    Processing Record | Inhambane
    Processing Record | Tuatapere
    Processing Record | Buta
    Processing Record | Dzilam Gonzalez
    Processing Record | Whitehorse
    Processing Record | Milin
    Processing Record | Puerto Madryn
    Processing Record | Bazarnyy Karabulak
    Processing Record | Chernyshevskiy
    Processing Record | Kenai
    City not found. Skiped
    City not found. Skiped
    Processing Record | Cururupu
    Processing Record | Lar
    City not found. Skiped
    Processing Record | Arman
    Processing Record | Ixtapa
    Processing Record | Ostrovnoy
    Processing Record | Belyy Yar
    Processing Record | Junin
    Processing Record | Chimbote
    Processing Record | Pacific Grove
    Processing Record | Payo
    Processing Record | Nakamura
    Processing Record | Lipari
    Processing Record | Khorramabad
    Processing Record | Nampula
    Processing Record | Dubbo
    City not found. Skiped
    Processing Record | Vorselaar
    Processing Record | Vostok
    Processing Record | Larsnes
    Processing Record | Lavrentiya
    Processing Record | Beyneu
    Processing Record | Spearfish
    Processing Record | Axim
    Processing Record | Wadi
    Processing Record | Wellington
    Processing Record | Port Moresby
    Processing Record | Vestmannaeyjar
    Processing Record | Severo-Kurilsk
    Processing Record | Sahibganj
    Processing Record | Sakyla
    Processing Record | Araraquara
    Processing Record | Ust-Maya
    Processing Record | Riyadh
    Processing Record | Vao
    Processing Record | San Jeronimo
    Processing Record | Bonthe
    Processing Record | Vila Franca do Campo
    Processing Record | Caravelas
    Processing Record | Bud
    Processing Record | Batagay-Alyta
    Processing Record | Kimbe
    Processing Record | Preobrazheniye
    Processing Record | New Milford
    Processing Record | Puerto del Rosario
    Processing Record | Chicama
    Processing Record | Gambela
    Processing Record | Outjo
    Processing Record | Paita
    Processing Record | Sesheke
    Processing Record | Aksha
    Processing Record | Santa Isabel
    Processing Record | Nhulunbuy
    Processing Record | Ust-Nera
    Processing Record | Xining
    Processing Record | Craig
    Processing Record | Usinsk
    Processing Record | Veraval
    Processing Record | Motygino
    Processing Record | Los Llanos de Aridane
    Processing Record | Yeppoon
    City not found. Skiped
    Processing Record | Leh
    Processing Record | Verkhnyaya Inta
    Processing Record | Ciudad Bolivar
    Processing Record | Undory
    Processing Record | Machilipatnam
    Processing Record | Rongcheng
    Processing Record | Jiazi
    Processing Record | Cayenne
    Processing Record | Inirida
    Processing Record | Mul
    Processing Record | Hue
    Processing Record | Batagay
    Processing Record | Merauke
    City not found. Skiped
    Processing Record | Jind
    Processing Record | Barinitas
    Processing Record | Beihai
    Processing Record | Lamu
    Processing Record | Northam
    Processing Record | Sault Sainte Marie
    Processing Record | Simbahan
    City not found. Skiped
    City not found. Skiped
    Processing Record | Markova
    City not found. Skiped
    Processing Record | Bourges
    Processing Record | Irpa Irpa
    Processing Record | Half Moon Bay
    City not found. Skiped
    Processing Record | Amalapuram
    Processing Record | Skjervoy
    Processing Record | Padang
    Processing Record | Tulum
    Processing Record | Gorlice
    Processing Record | Peniche
    Processing Record | Kudahuvadhoo
    Processing Record | Kondopoga
    City not found. Skiped
    Processing Record | Mamedkala
    Processing Record | Acapulco
    Processing Record | Solnechnyy
    Processing Record | Pimenta Bueno
    Processing Record | Rio Gallegos
    Processing Record | Terra Roxa
    Processing Record | Oni
    Processing Record | Eureka
    Processing Record | Muroto
    Processing Record | Kahului
    Processing Record | Verkhnetulomskiy
    Processing Record | Boguchany
    Processing Record | Lixourion
    Processing Record | Komsomolskiy
    Processing Record | Abrau-Dyurso
    City not found. Skiped
    City not found. Skiped
    Processing Record | Tashla
    Processing Record | Carupano
    Processing Record | Trang
    Processing Record | Great Bend
    Processing Record | The Valley
    Processing Record | Henties Bay
    City not found. Skiped
    Processing Record | Ilhabela
    City not found. Skiped
    Processing Record | Gebze
    Processing Record | Saginaw
    Processing Record | Viedma
    Processing Record | Kokopo
    Processing Record | Husavik
    Processing Record | Manta
    Processing Record | Qandala
    Processing Record | Egvekinot
    Processing Record | Manawar
    Processing Record | Marystown
    Processing Record | Sar-e Pul
    Processing Record | Soubre
    Processing Record | Sitka
    Processing Record | Otane
    Processing Record | Bilma
    Processing Record | Khani
    Processing Record | Mackay
    Processing Record | Rawson
    City not found. Skiped
    Processing Record | Rabo de Peixe
    Processing Record | Tessalit
    Processing Record | Pitkyaranta
    Processing Record | Kangra
    Processing Record | Tautira
    Processing Record | Leninsk
    Processing Record | Port Keats
    Processing Record | Panjakent
    Processing Record | Liwale
    Processing Record | Prainha
    Processing Record | Ghanaur
    Processing Record | Kobryn
    Processing Record | Camabatela
    Processing Record | Linhares
    Processing Record | Freetown
    Processing Record | Along
    Processing Record | Jutai
    Processing Record | Canhotinho
    Processing Record | Mahanoro
    Processing Record | Port Hardy
    Processing Record | Vestmanna
    Processing Record | Lethem
    Processing Record | Toamasina
    Processing Record | Hawkesbury
    City not found. Skiped
    Processing Record | Palu
    Processing Record | Moose Factory
    Processing Record | Nienburg
    Processing Record | Velika Gorica
    Processing Record | Camacupa
    City not found. Skiped
    City not found. Skiped
    City not found. Skiped
    Processing Ended
    -------------------------------


### Convert Raw Data to DataFrame
* Export the city data into a .csv.
* Display the DataFrame


```python
weatherdict = {
    "City": cityname,
    "Cloudiness":clouds, 
    "Country":country,
    "Date":dt, 
    "Humidity": humidity,
    "Lat":lat, 
    "Lon":lon, 
    "Max Temp": temp_max,
    "Wind Speed":wind_speed
} 


weatherdict_df = pd.DataFrame(weatherdict)


weatherdict_df.count()
```




    City          521
    Cloudiness    521
    Country       521
    Date          521
    Humidity      521
    Lat           521
    Lon           521
    Max Temp      521
    Wind Speed    521
    dtype: int64




```python
weather_data.to_csv('weather_data.csv')
weather_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Cloudiness</th>
      <th>Country</th>
      <th>Date</th>
      <th>Humidity</th>
      <th>Lat</th>
      <th>Lng</th>
      <th>Max Temp</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Thompson</td>
      <td>40</td>
      <td>CA</td>
      <td>1560443204</td>
      <td>42</td>
      <td>55.74</td>
      <td>-97.86</td>
      <td>66.20</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Geraldton</td>
      <td>75</td>
      <td>CA</td>
      <td>1560443205</td>
      <td>48</td>
      <td>49.72</td>
      <td>-86.95</td>
      <td>60.80</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Butaritari</td>
      <td>100</td>
      <td>KI</td>
      <td>1560443206</td>
      <td>81</td>
      <td>3.07</td>
      <td>172.79</td>
      <td>84.12</td>
      <td>17.02</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Tuatapere</td>
      <td>100</td>
      <td>NZ</td>
      <td>1560443207</td>
      <td>95</td>
      <td>-46.13</td>
      <td>167.69</td>
      <td>42.01</td>
      <td>4.36</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Carnarvon</td>
      <td>0</td>
      <td>ZA</td>
      <td>1560443208</td>
      <td>23</td>
      <td>-30.97</td>
      <td>22.13</td>
      <td>52.62</td>
      <td>7.20</td>
    </tr>
  </tbody>
</table>
</div>



### Plotting the Data
* Use proper labeling of the plots using plot titles (including date of analysis) and axes labels.
* Save the plotted figures as .pngs.

#### Latitude vs. Temperature Plot


```python
plt.scatter(weather_data["Lat"], weather_data["Max Temp"], marker="o", s=30)

plt.title("City Latitude vs. Max Temperature")
plt.ylabel("Max. Temperature (F)")
plt.xlabel("Latitude")
plt.grid(True)

plt.savefig("Latitude_vs_Temperature_Plot.png")
plt.show()
```


![png](output_12_0.png)


#### Latitude vs. Humidity Plot


```python
plt.scatter(weather_data["Lat"], weather_data["Humidity"], marker="o", s=30)

plt.title("City Latitude vs. Humidity")
plt.ylabel("Humidity (%)")
plt.xlabel("Latitude")
plt.grid(True)

plt.savefig("Latitude_vs_Humidity_Plot.png")
plt.show()
```


![png](output_14_0.png)


#### Latitude vs. Cloudiness Plot


```python
plt.scatter(weather_data["Lat"], weather_data["Cloudiness"], marker="o", s=30)

plt.title("City Latitude vs. Cloudiness")
plt.ylabel("Cloudiness (%)")
plt.xlabel("Latitude")
plt.grid(True)

plt.savefig("Latitude_vs_Cloudiness_Plot.png")
plt.show()
```


![png](output_16_0.png)


#### Latitude vs. Wind Speed Plot


```python
plt.scatter(weather_data["Lat"], weather_data["Wind Speed"], marker="o", s=30)

plt.title("City Latitude vs. Wind Speed")
plt.ylabel("Wind Speed (mph)")
plt.xlabel("Latitude")
plt.grid(True)

plt.savefig("Latitude_vs_Wind_Speed_Plot.png")
plt.show()
```


![png](output_18_0.png)



```python

```
