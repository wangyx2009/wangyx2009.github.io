import csv
from snownlp import SnowNLP


fNLs = ['人生大事', '奇迹·笨小孩', '我和我的父辈', '爱情神话', '狙击手', '长津湖']

for fN in fNLs:
    # 读取弹幕
    sentenceLs = []
    with open('电影弹幕/《{}》弹幕.csv'.format(fN), 'r', encoding='utf-8') as f1:
        reader = csv.reader(f1)
        for r in reader:
            sentenceLs.append(r)

    # 获取感情值，感情分析
    sentencesSent = []
    sentenceSent = {}
    for sentence0 in sentenceLs:
        sentence = sentence0[0]
        try:
            sent = SnowNLP(sentence).sentiments
            if sent >= 0.6:
                emotionalAnalysis = '积极'
            elif 0.4 <= sent < 0.6:
                emotionalAnalysis = '中性'
            elif sent < 0.4:
                emotionalAnalysis = '消极'
            sentenceSent[sentence] = [sent, emotionalAnalysis]
        except ZeroDivisionError:
            pass
        except TypeError:
            pass

    # 整理感情值与感情分析
    for sentenceSKey in sentenceSent:
        sentencesS = {'弹幕': sentenceSKey, '感情值': sentenceSent[sentenceSKey][0], '感情分析': sentenceSent[sentenceSKey][1]}
        sentencesSent.append(sentencesS)
    # 保存感情值与感情分析
    with open('电影弹幕感情分析/《{}》弹幕感情分析.csv'.format(fN), 'w', newline='', encoding='utf-8') as f2:
        writer2 = csv.DictWriter(f2, fieldnames=['弹幕', '感情值', '感情分析'])
        writer2.writeheader()
        writer2.writerows(sentencesSent)
