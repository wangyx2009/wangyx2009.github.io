#pip install wordcloud
import PIL.Image as image
from wordcloud import WordCloud as cloud
import matplotlib.pyplot as plt
import numpy as np
import os

film,name = 'Changjin Lake.txt','长津湖'
file=os.path.abspath('data\\'+'circle1.png')
with open(file='data//'+film,mode='r') as word:
    txt = word.readlines()

txt2,other = str(),False
for i in txt:
    if not(i in "都的了啦是这我们他你也人啊就是那么个"):
        txt2=txt2+i
mask = np.array(image.open(file))
clou = cloud(background_color='#FFFFFF',font_path='msyhl.ttc',\
    height=5000,width=5000,
            collocations=False,mask=mask)
clou.generate(txt2)
plt.axis("off")
clou.background_color='white'
clou.to_file("{}.png".format(name))
