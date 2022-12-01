from xml.dom.minidom import parse
import xml.dom.minidom
import pandas as pd
danmus = []

for x in range(1, 24):
    DOMTree = xml.dom.minidom.parse(f'./zx-{x//10}{x%10}.xml')
    collection = DOMTree.documentElement
    entrys = collection.getElementsByTagName('entry')
    for entry in entrys:
        t1 = entry.getElementsByTagName('content')
        if len(t1) > 0:
            t2 = t1[0].childNodes
            if len(t2) > 0:
                danmu = t2[0].data
                danmus.append(danmu)
    print(x, "done")
# print(danmus)
df = pd.DataFrame({
    '弹幕': danmus
})
df.to_csv('./danmu.csv',
          encoding='utf-8-sig', index=False)
