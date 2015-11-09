---
layout: post
title: Python正则表达式
date: 2015-11-06 15:09:20
tags:
category: Python
comments: true
---

2015-11-03

##一、re.search()

使用正则表达式<<ed$>>查找以ed结尾的词汇。使用函数re.search(p, s) 检查字符串s中是否有模式p。

```
import re
import nltk
In[12]: wsj = sorted(set(nltk.corpus.treebank.word()))
In[13]: ws = [w for w in wsj if re.search('ed$', w)]

In[15]: ws[:10]
Out[15]: 
[u'62%-owned',u'Absorbed',u'Advanced',u'Alfred', u'Allied', u'Annualized', u'Arbitrage-related',
 u'Asked',u'Atlanta-based', u'Bermuda-based']
```
通配符“.”可以用来匹配任何单个字符。假设有一个8个字母组成的字谜，j是第三个字母，t是第六个字母。每个空白单元格用句点隔开。

```
In[16]: ws = [w for w in wsj if re.search('^..j..t..$', w)]
In[18]: ws
Out[18]: [u'adjusted', u'rejected']
```
匹配除元音字母之外的所有字母

```
[^aeiouAEIOU]
```

?:
如果要使用括号来指定连接的范围，又不想选择要输出字符串，必须添加“?:”。

```
In[20]: re.findall(r'^.*(?:ing|ly|ed|ies)$', 'processing')
Out[20]: ['processing']
```

演示如何使用符号：\，{}，() 和 |

```
In[20]: ws = [w for w in wsj if re.search('^[0-9]+\.[0-9]+$', w)]
In[21]: ws[:5]
Out[21]: [u'0.0085', u'0.05', u'0.1', u'0.16', u'0.2']

In[22]: ws = [w for w in wsj if re.search('^[A-Z]+\$$', w)]
In[23]: ws
Out[23]: [u'C$', u'US$']

In[24]: ws = [w for w in wsj if re.search('^[0-9]{4}$', w)]
In[26]: ws[:5]
Out[26]: [u'1614', u'1637', u'1787', u'1901', u'1903']

In[27]: ws = [w for w in wsj if re.search('(ed|ing)$', w)]
In[28]: ws[:5]
Out[28]: [u'62%-owned', u'Absorbed', u'According', u'Adopting', u'Advanced']
```

##分词

```
In[13]: raw = """'When I'M a Duchess,' she said to herself, (not in a very hopeful tone
... though), 'I won't have any pepper in my kitchen AT ALL. Soup does very
... well without--Maybe it's always pepper that makes people
... hot-tempered,'..."""
In[16]: re.split(r' ', raw)
Out[16]: 
["'When",
 "I'M",
 'a',
 "Duchess,'",...]
In[17]: re.split('[ \t\n]', raw)
Out[17]: 
["'When",
 "I'M",
 'a',
 "Duchess,'",...]
```


