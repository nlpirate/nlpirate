---
title: "Impariamo a contare"
date: 2019-05-06T18:35:30+02:00
draft: true
---


# Testi dal web ed Espressioni Regolari

```
from urllib import request
#orlando furioso
url = 'https://www.gutenberg.org/files/3747/3747-0.txt'
response = request.urlopen(url)
raw = response.read().decode('utf8')
```
```
print (type(raw))
```
##### 1 2 1 2 3 4 5 1 2 3 4 5 1


<class 'str'>

##### 1644985

​The Project Gutenberg EBook of Orlando Furioso, by Ludovico Ariosto

<class 'nltk.text.Text'>

['u', 'e', 'a', 'i', 'a', 'i', 'i', 'i', 'e', 'i', 'a', 'i', 'o', 'o']

['Ippolito', 'vincito', 'uscito', 'subito', 'ardito', 'subito', 'subito',
'tacito', 'rito', 'incognito', 'istordito', 'perdito', 'tacito', 'strepito',
'guernito', 'subito', 'credito', 'stordito', 'impedito', 'udito', 'subito',
'subito', 'rito', 'tacito', 'forbito', 'Rito', 'rito', 'lito', 'rito',
'debito', 'adito', 'tradito', 'uscito', 'subito', 'rito', 'tradito', 'adito',
'insolito', 'statuito', 'merito', 'subito', 'rito', 'tenito', 'esercito',
'inclito', 'Ippolito', 'esercito', 'abito', 'Ippolito', 'Ippolito',
'Ippolito', 'dito', 'abito', 'rito', 'dito', 'nutrito', 'gemito', 'tenito',
'debito',...

```
print (len(raw))
```
```
print (raw[: 70 ])
```
```
#trasformiamo il file in un oggetto di tipo Text
webtext = nltk.wordpunct_tokenize(raw)
webtext = nltk.Text(webtext)
print (type(webtext))
```
```
### Espressioni regolai
import re
word = 'supercalifragilistichespiralidoso'
print (re.findall(r'[aeiou]',word))
```
```
print (re.findall(r'\w+ito',raw))
```


#scriviamo risultati su un file
output_file = open('output.txt','w')
aut = re.findall(r'\w+ito',raw)
aut = ''.join(aut)
print(aut, file=output_file)
