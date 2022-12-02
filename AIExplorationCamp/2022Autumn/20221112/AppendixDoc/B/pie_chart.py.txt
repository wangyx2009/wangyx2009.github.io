import matplotlib.pyplot as plt
import matplotlib

film,name = 'data/Changjin Lake(t).txt','长津湖'
with open(file=film,mode='r',encoding='utf-8') as word:
    happy_sad = word.readlines()

for i in happy_sad:
    try:
        happy_sad.append(i.split(',')[2])
    except:
        pass
middle,down,up = int(),int(),int()
for i in happy_sad:
    if i=='消极\n':
        down+=1
    elif i=='中性\n':
        middle+=1
    elif i=='积极\n':
        up+=1
plt.pie(x=[down,middle,up],labels=['消极','中性','积极'],autopct='%0.1f%%')
matplotlib.rcParams['font.sans-serif']=['Microsoft Yahei']
plt.title("{}弹幕感情分析".format(name))
plt.show()