---
title: "Impariamo a contare"
date: 2019-05-05T18:35:30+02:00
draft: false
---


# Python perlinguisti parte 2
## impariamo a contare

Il ciclo `for` legge la stringa esattamente come la lista dell'esempio precedente, scorrendo tutti
gli elementi, in questo caso i caratteri (compreso lo spazio).

```python
frase = 'il gatto mangia la pigna'
for carattere in frase:
  print (carattere)
#cosa stampa?
```

Se si vuole dividere "per parola"
bisogna ricorrere al metodo `split()`. Questo metodo non fa altro che dividere il testo in base al separatore specificato.

```python
frase = 'il gatto mangia la pigna'
frase_divisa = frase.split(' ')
for carattere in frase_divisa:
print(carattere)
# cosa stampa ora?
```

In questo caso il separatore in base al quale si effettua lo split è lo spazio, ma si può inserire
qualsiasi carattere alfanumerico o carattere speciale `(\n,\t,,...)`.

Combinando il ciclo for con l'input da tastiera si possono specificare delle condizioni, come ad esempio limitare il numero di caratteri di una stringa inserita in input da parte dell'utente.
Per prima usiamo l'operatore di concatenazione visto prima per stampare accanto alle lettere (o
alle parole) un indice numerico.


### Cosa si può fare col for: il modulo Counter

Come dice il nome, il modulo Counter serve a contare. Risulta estremamente utile per quasisi task di statistica testuale.


```python
# contare elementi in una lista

# per prima cosa si importa il modulo a inizio file
from collections import Counter

# si crea un oggetto Counter
cnt = Counter()
lista = ['A','B','A','C','B','B']
for i in lista:
  cnt[i] += 1
print(cnt)
```

Come si vede dall'output, il programma restituisce una dizionario (contraddistinto da `{}` in cui a ogni elemento presente nella lista è associato il numero di occorrenze. L'uso del ciclo for e di un contatore che si incrementa a ogni iterazione sono sufficienti per creare liste di frequenza
anche di file molto grandi.

### Aprire file e contare le parole

Per contare tutte le parole di un file è sufficiente una linea di codice usando il modulo
Counter.

```python
# importiamo i moduli necessari
import re
from collections import Counter

# il file deve essere nella stessa cartella
# in cui si trova lo script
words = re.findall('\w+',open('nomemiofile.txt').read().lower())
print(Counter(words))
```

### parole più frequenti in un file

L'esempio precedente effettua un conteggio di tutte le parole, ovvero fornisce come output tutte
le parole che appaiono nel testo preso in esame con il relativo numero di occorrenze. Se invece
si vogliono soltanto visualizzare le parole più frequenti di un file è sufficiente una piccola
modifica allo script.

```python
print(Counter(words).most_common( 20 ))
# si specifica il numero di parole che si desiderano in output
```

Come si può notare dall'output, le parole più frequenti molto difficilmente saranno parole semanticamente piene. Al contrario si tratterà di articoli o preposizioni. Se si vuole ottenere un
output più informativo è necessario che il testo sia "ripulito", usando le **stopwords** o una soglia basata sulla lunghezza in caratteri o sulla frequenza.

### scrivere l'output su file

Per scrivere l'output su un file si usa nuovamente il comando `open()` specificando che il file verrà aperto in scrittura `w`.

```python
#scriviamo output su file

c = Counter(words)

#creiamo un nuovo file vuoto da aprire in scrittura
out_file = open('frequenti.txt','w')
#concatena elementi lista
ris = '\n'.join(c)
# scrive su file
print (c, file=out_file)
```

## Nltk

Nltk (acronimo per **Natural Language Toolkit** ) è una libreria python che fornisce moltissimi
stumenti per l'analisi e la manipolazione di dati testuali.
Prima di tutto si crea un nuovo file python e si specifica a inizio file:

Il comando serve a importare il modulo nltk _in toto_. Per leggere testi in locale (quindi testi salvati sul pc) si usando i metodi `open()` e `read()`
A questo punto è buona regola normalizzare il testo convertendo tutto in lettere minuscole, in modo di non avere statistiche falsate nelle analisi successive. Ovviamente la normalizzazione non va operata se la distinzione tra lettere minuscole e maiuscole ha una rilevanza nelle analisi che vogliamo effettuare sul testo.
Per normalizzare si usa la funzione `lower()` che converte tutti i caratteri in minuscolo:

```python
import nltk

f = open('davinci.txt','r')
miofile = f.read()
```

Ottenuto il file normalizzato è necessario operare un’ulteriore trasformazione per rendere i dati
processabili con i metodi di nltk. Il file va infatti trasformato in un oggetto `Text` (un tipo di oggetto “interno” di nltk che consente di effettuare tutte le operazioni viste sopra da shell interattiva). Per trasformare il file in oggetto Text si effettuano le seguenti operazioni:

Se si effettua controllo con il comando type se tutto è andato a buon fine la shell python ci informerà che si tratta di un oggetto di tipo `nltk.text.Text`.

```
<class 'nltk.text.Text'>
```
Dunque il nostro file locale è stato “convertito” in un oggetto sul quale possono essere eseguiti
tutti i metodi di nltk. Senza questa trasformazione qualsiasi operazione sarà impossibile.
Adesso è possibile effettuare le analisi testuali di base, come contare da quanti **token** è
composto il testo. Per contare il numero di token si usa il metodo len():

```
numero token 173694
```
La prima line conta il numero di token da cui è composto il testo (ricordiamo che in questo
momento per token si intende qualsiasi carattere separato da spazio o diviso da un segno di
punteggiatura). La seconda linea semplicemente stampa a video il numero di token seguito dalla
stringa numero token per rendere il risultato più leggibile.
Per calcolare il vocabolario del testo, ovvero il numero di **type** , e contarli, si usano i metodi
set() e len():

```
numero parole-tipo 14359
```
Il comando set() “crea” l’insieme delle parole-tipo e col comando len() - analogamente a

quanto visto prima - effettua il conteggio che viene successivamente stampato a video.

```
miofilenorm = miofile.lower()
```
```
miotesto = nltk.wordpunct_tokenize(miofilenorm)
miotesto = nltk.Text(miotesto)
```
```
print (type(miotesto))
```
```
tokens = len(miotesto)
print ('numero token ',tokens)
```
```
vocab = set(miotesto)
# il numero dei type è di fatto il vocabolario di un testo
tipi = len(vocab)
print ('numero parole-tipo ',tipi)
```
##### 1 1 2 1 1 2 1 2 3 4


Una volta che sappiamo calcolare il numero di token e il numero di type, è facile iniziare ad
ottenere delle metriche informative sul testo, la più semplice è la **type-token-ratio (TTR)**. La
TTR mira a fornire informazioni in merito alla ricchezza lessicale mettendo in rapporto il numero
di token (quindi le parole totali che compongono il testo) con il numero di type (quindi le parole
uniche).

Per calcolare la ricchezza lessicale è sufficiente dividere il numero di token per il numero di type,
essendo entrambi stati calcolati precedentemente.

```
ricchezza lessciale: 0.
```
Un'altra misura molto semplice da calcolare è l' **inverse type-token-ratio** , ovvero il rapporto
inverso tra numero di token e numero di parole-tipo. Questo rapporto indica quante volte in
media è stata usata ogni parola del testo:

```
ricchezza lessicale inversa: 12.
```
Se vogliamo invece ottenere la percentuale con cui una determinata parola è usata è sufficiente
un semplice calcolo:

##### 0.

Ovviamente per dare risultati validi sarà sempre necessario iniziare importando il modulo
nltk, pertanto il codice completo per calcolare i token, le parole-tipo e le misure di ricchezza

lessicale sarà il seguente:

```
#type-token-ratio
ttr = tipi/tokens
#stampa la type-token-ratio
print ('ricchezza lessciale: ',ttr)
```
```
#inverse type-token-ratio
ittr = tokens/tipi
print ('ricchezza lessicale inversa: ',ittr)
```
```
parola = 'parigi'
occorrenze = miotesto.count(parola)
percentuale = 100 *occorrenze/tokens
print (percentuale)
```
##### 1 2 3 4 1 2 3 1 2 3 4


import nltk

```
#importa il file
f = open('davinci.txt','r')
miofile = f.read()
```
```
#normalizza il file
miofilenorm = miofile.lower()
```
```
#trasforma il file in oggetto Text
miotesto = nltk.wordpunct_tokenize(miofilenorm)
miotesto = nltk.Text(miotesto)
```
```
#calcola tokens e types
tokens = len(miotesto)
print ('numero token: ',tokens)
```
```
print ('-------')
# separatore per rendere più leggibile l'output
```
```
vocab = set(miotesto)
tipi = len(vocab)
print ('numero parole-tipo: ',tipi)
```
```
print ('-------')
```
```
#misure ricchezza lessicale
ttr = tipi/tokens
print ('ricchezza lessciale: ',ttr)
```
```
print ('-------')
```
```
ittr = tokens/tipi
print ('ricchezza lessicale inversa: ',ittr)
```
```
print ('-------')
```
```
#percentuale d'uso di una parola
parola = 'parigi'
occorrenze = miotesto.count(parola)
percentuale = 100 *occorrenze/tokens
print (parola,"è usata",percentuale,"volte in percentuale")
```



```
numero token: 173694
-------
numero parole-tipo: 14359
-------
ricchezza lessciale: 0.
-------
ricchezza lessicale inversa: 12.
-------
parigi è usata 0.048360910566858956 volte in percentuale
```
È possibile visualizzare le **collocazioni** , ovvero le parole all'interno del loro contesto, con un
buffer di n parole prima e dopo. Per fare ciò è sufficiente usare il metodo concordance().

```
parola da visualizzare: parigi
Displaying 25 of 84 matches:
he mai. prologo museo del louvre , parigi ore 22. 46 il famoso curatore del
odino. l ' università americana di parigi è lieta di presentare una serata
co
lio per chiamarla prima di lasciare parigi , martedì prossimo? grazie .» e
ri
delle luci. buon sonno al ritz di parigi. alzò la testa e fissò lo
specchio
hine dell ' università americana di parigi « il nostro ospite di questa sera
n
ella settimana , silas era ospite a parigi , ma da molti anni godeva della
ben
pensi. la chiave di volta è qui a parigi .» « parigi? incredibile. sembra
chiave di volta è qui a parigi .» « parigi? incredibile. sembra persino
trop...
```
## Distribuzioni di frequenza

Per creare una distribuzione di frequenza in nltk si usa il comando nltk.FreqDist().

##### ### ESERCIZIO 11

```
### riscrivere il programma ma calcolando la percentuale di uso
### di una parola scelta dall'utente
```
```
# input utente
parola = input('parola da visualizzare: ')
```
```
#collocazioni
conc = miotesto.concordance(parola)
print (conc)
```
##### 1 2 3 1 2 3 4 5 6


La distribuzione di frequenza, anche se parzialmente filtrata si configura sempre come una
legge di potenza, ovvero con una distribuzione cosiddetta a coda lunga , c'è un altissimo numero
di parole con frequenze estremamente basse e un insieme di parole molto molto ridotto che
occorrono un numero altissimo di volte. Le parole con frequenza più altra sono quelle dette
semanticamente vuote, ovvero tutte le parti del discorso
Dalla distribuzione di frequenza che si ottiene si nota come venga rispettata la Legge di Zipf e
come all'interno delle 30 parole più frequenti che vengono stampate a video ci siano pochissime
parole semanticamente piene: per la maggior parte si tratta di articoli, preposizioni, segni di
punteggiatura. Infatti, se vogliamo vedere quali sono le parole più frequenti senza stampare il
grafico della distribuzione di frequenza basta dare il comando:

```
[('.', 8635), (',', 7392), ('di', 4987), ('la', 3782), ("'", 3711), ('il',
3616), ('«', 3475), ('e', 3041), ('che', 2960), ('un', 2451), ('a', 2388),
('era', 1746), ('non', 1724), ('.»', 1678), ('si', 1675), ('l', 1626), ('in',
1573), ('una', 1425), ('per', 1422), ('langdon', 1336), ('aveva', 1328),
('"', 1284), ('del', 1216), ('le', 1166), ('è', 1144), ('sophie', 1023),
('con', 1001), ('della', 993), ('i', 904), ('da', 790)]
```
Occorre dunque "ripulire" il testo, filtrando tutti gli elementi non informativi che creano solo
rumore. Uno dei modi più semplici è quello di usare le **stopwords**. Le stopwords sono parole
estremamente comuni e semanticamente vuote inserite in una lista. Nel nostro codice andiamo
a specificare che nella distribuzione di frequenza devono esserci elementi solo se non
appartengono all'insieme delle stopwords. Esiste una lista di stopwords per l'italiano già

```
fd = nltk.FreqDist(miotesto)
```
```
#creare il grafico per le 30 parole più frequenti
fd.plot( 30 )
```
```
print(fd.most_common( 30 ))
```
##### 1

##### 1

##### 2

##### 1


presente in nltk, oppure è possibile specificarne una propria da un file esterno.
Per utilizzare le stopwords di nltk è sufficiente a inizio file specificare:

Qualora il programma lanciato restituisse un messaggio di errore non trovando il modulo, allora
bisognerà installare il pacchetto nltk.data. Da shell digitare:

Una volta installati i corpora di nltk, nel codice è sufficiente specificare:

L'output è lievemente migliorato ma contiene ancora molto rumore, come i segni di
punteggiatura, eviidentemente non presenti nella lista stopwords di nltk. Per migliorare il

risultato si può utilizzare un altro metodo, basato sulla lunghezza della parole. Si stabilisce una
soglia e si specifica che la distribuzione di frequenza contemplerà soltanto le parole più lunghe
di n caratteri, secondo il criterio che le parole molto corte sono molto probabilmente articoli,
segni di punteggiatura o preposizioni.

```
from nltk.corpus import stopwords
```
```
#>>> nltk.download()
```
```
sw = stopwords.words('italian')
# crea una variabile con le stopwords per l'italiano
```
```
unstopped_words = [w for w in miotesto if w not in sw]
fd_unstopped_words = nltk.FreqDist(unstopped_words)
```
```
fd_unstopped_words.plot( 30 )
```
```
long_words = [w for w in miotesto if len(w)> 7 ]
fd_long_words = nltk.FreqDist(long_words)
```
##### 1 1 1 2 3 4 5 1 1 2


in questo caso con una soglia pari a 7 notiamo un sensibile miglioramento. Per avere un output
ancora più raffinato si può combinare questo filtro basato sulla lunghezza con uno basato sulla
frequenza. Ovvero includerò nella distribuzione soltanto le parole lunghe almeno _n_ caratteri e
che occorrono almeno _x_ volte nel mio testo.

```
fd_long_words.plot( 30 )
```
```
filtered_words = [w for w in miotesto if len(w)> 7 and fd[w]> 7 ]
fd_filtered_words = nltk.FreqDist(filtered_words)
fd_filtered_words.plot( 30 )
```
##### 1

##### 1

##### 2

##### 3


Valutando l'output si nota come con pochi semplici passaggi si riesce a passare da un risultato
quasi inutilizzabile a un output molto informativo per quanto riguarda il contenuto del testo.
Infatti se si va a stampare la lista di frequenza si nota una netta differenza tra il primo output.

```
[('saunière', 243), ('priorato', 170), ('aringarosa', 154), ('qualcosa',
143), ('leonardo', 127), ('pavimento', 126), ('messaggio', 114), ('capitano',
92), ('studioso', 91), ('documenti', 89), ('maddalena', 82), ('cofanetto',
73), ('qualcuno', 73), ('cavaliere', 70), ('sicurezza', 69), ('francese',
68), ('templari', 67), ('immediatamente', 61), ('sembrava', 61), ('telefono',
60), ('occhiata', 59), ('galleria', 59), ('lasciato', 58), ('direzione', 55),
('impressione', 54), ('corridoio', 52), ('sorpresa', 51), ('sangreal', 50),
('riusciva', 50), ('espressione', 50)]
```
```
abbastanza -> 22
abituato -> 9
accompagnato -> 9
aeroplano -> 13
aeroporto -> 29
affresco -> 14
aggiunse -> 12
aggrottò -> 28
alfabeto -> 13
allontanarsi -> 19
allontanava -> 16
...
```
## Testi dal web

```
#parole più frequenti in lista filtrata
print(fd_filtered_words.most_common( 30 ))
```
```
#scriviamo questa distribuzione di frequenza su un file
out_distfreq = open('df.txt','w')
for w in sorted(fd_filtered_words):
print (w, '->', fd_filtered_words[w], end='\n')
print(w, '->', fd_filtered_words[w], end='\n', file=out_distfreq)
```
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
aut = '\n'.join(aut)
print(aut, file=output_file)
