---
title: "Testi dal web"
date: 2019-05-14T15:35:30+02:00
draft: false
---


## Testi dal web

### Il modulo urllib

Questo modulo serve per importare file dal web direttamente dal vostro editor/shell/app e lavorarci.
Il primo passo è quello di importare il modulo con il seguente comando:


```python
import urllib.request

```

Il secondo passo è quello di trovare un file su cui lavorare. Per comodità useremo i file txt in utf-8 disponibili gratuitamente sulla pagina del [Progetto Gutemberg](https://www.gutenberg.org/browse/languages/it).

il file in txt scelto verrà assegnato a una variabile (in questo caso chiamata `url`) ma si può scrivere direttamente omettendo la variabile oppure utilizzare `input` e inserire il link una volta lanciato lo script.


```python
#l'aeroplano del papa (Marinetti)
url = 'http://www.gutenberg.org/cache/epub/17838/pg17838.txt'
```

Adesso facciamo in modo che il modulo apra e legga il file e successivamente lo stampi a video.


```python
response = request.urlopen(url)
mytextfromweb = response.read().decode('utf8')

print(mytextfromweb)
```

Se tutto è andato a buon fine verrà visualizzato un estratto del file importato (o l'intero file). Si nota subito che il file è ancora "sporco", ovvero sono presenti tag html (se abbiamo scelto questo formato) oppure tag che indicano i ritorni a capo e cose simili (`\b\r` o cose simili).

Pertanto il file va ripulito prima di poter effettuare qualsiasi operazione.

- Se il testo è un txt e si riscontrano problemi di codifica è sufficiente modificare la riga precedente:



```python
mytextfromweb = response.read().decode('utf8')
```

- se il testo è in html o xml e sono presenti tag da eliminare, ci sono innumerevoli modi per farlo.

Un metodo comune è quello di usare le espressioni regolari. Data la ristrettezza temporale a nostra disposizione e il non molto interesse da parte vostra, si è scelto di usare per comodità un modulo pronto, in particolare `BeautifulSoup`.


```python
from bs4 import BeautifulSoup

soup = BeautifulSoup(mytextfromweb,"html5lib")
mytextfromweb = soup.get_text(strip=True)
print (mytextfromweb)
```

### Ora mettiamo insieme questo e NLTK

Per prima cosa trasformiamo il testo in una sequenza di token.
Il comando successivo tokenizza senza usare nltk.



```python
import nltk

tokens = [t for t in mytextfromweb.split()]
```


```python
print(tokens)
```

La tokenizzazione può essere fatta anche usando Nltk. Come visto precedentemente, si trasforma il file in un oggetto nltk e successivamente si usando le funzioni già presenti nella libreria.

Contiamo ora la frequenza delle parole e stampiamola a video (è possibile anche usare il codice della lezione precedente).


```python
freq = nltk.FreqDist(tokens)
for key,val in freq.items():
    print (str(key) + ':' + str(val))
```


```python
freq.plot(20,cumulative=False)
```

Come visto nella lezione precedente, è possibile migliorare facilmente questa distribuzione di frequenza inserendo delle soglie sulla lunghezza delle parole e sulla frequenza.
