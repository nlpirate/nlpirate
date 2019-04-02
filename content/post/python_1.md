---
title: "Python Perlinguisti"
date: 2019-04-02T18:35:30+02:00
draft: false
---


# Python per linguisti
## una (piccola piccola) introduzione

il primo programma: `helloworld.py`

Precisazione: nell'apprendimento di un qualsiasi linguaggio di programmazione, il primo programma è sempre quello che stampa a video la stringa "hello world!" (o "ciao mondo" nella lingua dove il si suona), come a sancire il nostro primo vagito di benvenuto al mondo in quella nuova lingua che - nel nostro caso - è il linguaggio python.


```python
#questo è un commento in python

print('Hello World!')
```

    Hello World!
il comando `print()` stampa (a video) la stringa `Hello World!` che - in quanto stringa di testo - è racchiusa tra apici singoli o doppi. Tutto ciò che si vuole stampare deve essere racchiuso tra parentesi tonde.

### Istruzioni
1. aprire IDLE
2. creare un nuovo file
3. scrivere l'istruzione
4. salvare il file come `hello.py`
5. eseguire il programma con F5

### Come funziona il programma?
l'interprete python "legge" riga per riga le istruzioni del codice sorgente e le "traduce" producendo un output. In questo caso l'unico comando che diamo è `print  ('stringa di testo')`

## Le variabili
Una variabile è un nome che si riferisce a un valore. Tramite il comando di **assegnazione** si creano nuove variabili e si assegna loro un valore


```python
#comando di assegnazione
messaggio = 'ciao a tutti'
stringa = 'pigna'
numero = 25
pi = 3.14159
```


```python
### ESERCIZIO 1
### queste istrizuoni non producono nessun output
### scrivere il programma es_1.py che stampa in sequenza le variabili elencate
```

Si può subito notare che le stringhe, come detto sopra, vanno sempre racchiuse tra apici, mentre i numeri no. È importante qui introdurre il concetto di **tipo**. Python semplifica molto la vita del programmatore dal momento che - contrariamente alla maggior parte dei linguaggi - non bisogna specificare il tipo di variabile che stiamo creando. I tipi che ci interessano al momento sono:
1. `int` = numero intero (integer)
2. `float` = numero decimale
3. `str` = stringa di testo (string)


Se ci interessa sapere i tipi delle variabili create sopra si usa il comando `type()`


```python
print (type(pi))
```

    <class 'float'>
Ovviamente per il trattamento di dati testuali si lavora principalmente su stringhe, ma è importante conoscere i tipi soprattutto per sapere come si concatenano tipi diversi.


```python
# quando si vogliono concatenare oggetti di tipo diverso si usa la virgola
print ('il tipo di ',pi,' è ',type(pi))
```

    il tipo di  3.14159  è  <class 'float'>
Se si concatenano stringhe si usa l'operatore `+`


```python
#variabili
parola1 = 'ciao'
parola2 = 'mondo'
```


```python
#concateniamo stringhe
print (parola1+parola2)
```

    ciaomondo



```python
#aggiungiamo lo spazio (che è una stringa)
print (parola1+' '+parola2)
```

    ciao mondo



```python
#concateniamo stringhe e variabili
frase = 'il gatto mangia la'
ris = frase+' pigna'
print (ris)
```

    il gatto mangia la pigna


È buona norma assegnare alle variabili nomi significativi:


```python
messaggio_auguri = 'tanti auguri'   #ok
var11201231891   = 'tanti auguri'   #bleah
# per il compilatore non c'è differenza, ma per gli umani si
```

I nomi assegnati alle variabili devono iniziare per lettera (convenzionalmente minuscola), **non possono iniziare con un carattere numerico e non possono contenere spazi bianchi**, altrimenti il compilatore restituirà un messaggio di errore. Se i nomi sono composti da più parole si usa il simbolo underscore o la notazione a cammello LINK:


```python
auguri_natale    = 'buon natale'    #underscore OK
21Auguri         = 'buon natale'    #errore di sintassi
tanti auguri     = 'buon natale'   #errore di sintasi
auguriNatale     = 'buon natale'   #CamelCase OK
```

#### Sovrascrittura
Attenzione: il nome di ciascuna variabile è univoco, se una variabile viene rinominata essa viene sovrascritta in modo irreversibile


```python
parola = 'cane'
parola = 'gatto'
print (parola)
# non cè modo di recuperare la stringa della prima assegnazione
```

### il comando condizionale ` if `
verifica se una condizione è vera o meno ed esegue dei comandi


```python
#se la condizione è vera stampa 'ok'

if 5 > 2:
    print ('ok')
```

    ok


La sintassi del comando condizionale è così composta:


```python
if condzione:
    comando da eseguire se la condizione è verificata
```

Tutto ciò che viene dopo i due punti è il comando e viene indentato a sinistra rispetto al comando `if`per specificare che viene eseguito soltanto se la condizione stabilita nell'`if`viene soddisfatta.


```python
#le la lettera 'a' è contenuta nella stringa 'casa' allora stampa la stringa 'ok'
if 'a' in 'casa':
    print ('ok')
```

    ok



```python
#stessa cosa ma con valori booleani True/False
if 'a' in 'casa':
    print (True)
```

    True



```python
#stringhe su stringhe
if 'hobbit' in 'in un buco sotto terra viveva uno hobbit':
    print ('ok')
```

    ok



```python
### ESERCIZIO 1.1
### scrivere il programma es_1.1.py che verifica se una stringa è contenuta in un'altra
### e restituisce ok se la condizione viene verificata

### ESERCIZIO 1.2
### scrivere il programma es_1.2.py che modifica il precedente usando delle variabili per le stringhe

### ESERCIZIO 1.3
### scrivere il programma es_1.3.py che modifica il precedente stampando:
### "la variabile nomevariabile è contenuta nella stringa nomestringa" usando l'operatore di concatenazione
```

Cosa succede se la condizione non è vera?


```python
if 'q' in 'casa':
    print (True)
```

Se non viene specificata un'istruzione alternativa, il programma non stampa nulla.
L'esecuzione alternativa è data con il comando `else` e segue la medesima sintassi di `if `


```python
# se la condizione non è verificata
# esegui il comando alternativo

if 'q' in 'casa':
    print (True)
else:
    print (False)
```

    False



```python
### ESERCIZIO 1.4
### dato il seguente programma

if 'termostato' in 'la casa spiccava il volo sotto un turbinio scosceso di verdi pascoli':
    print True

### scrivere es_1.4.py che modifica il programma specificando un'istruzione condizionale

### ESERCIZIO 1.5
### scrivere es_1.5.py che modifica es_1.4.py usando delle variabili

### ESERCIZIO 1.6
### scrivere il programma es_1.6.py che:
### - controlla se la lettera 'b' è presente nella stringa 'cane'
### - se la condizione si verifica stampi il messaggio 'ok'
### - se la condizione non si verifica stampi 'la lettera b non è contenuta nella parola cane'
```

## Input da tastiera
il comando `input()` permette all'utente di inserire una stringa di testo


```python
# l'utente deve scrivere qualcosa per continuare l'esecuzione dello script
parola = input('')
```


```python
print (parola)
```


```python
#aggiungiamo un messaggio per rendere più comprensibile l'input
nome = input('scrivi il tuo nome: ')
print ('ciao '+nome)
```

    scrivi il tuo nome: pippo
    ciao pippo

###

### `prompt` e ` if `



```python
#controlla se il numero inserito dall'utente è maggiore di 4
lettera = input('scrivi una lettera: ')
if lettera in 'gatto':
    print (True)
else:
    print (False)
```

    scrivi una lettera: 122132
    False



```python
### ESERCIZIO 1.7
### scrivere il programma es_1.7.py che modifica il codice in modo che stampi
### - 'la lettera <lettera inserita dall'utente> è contenuta nella parola casa se la condzione è vera'
### - 'non dire gatto se non lo hai nel sacco' se la condizione è falsa

### ESERCIZIO 1.8
### scrivere il programma es_1.8.py  che controlli se una stringa inserita dall'utente è contenuta
### in un'altra stringa inserita dall'utente e abbia un'istruzione alternativa in caso la condizione non sia vera
```

## Comandi iterativi: il ciclo `for`
il comando `for` scorre gli elementi uno per uno


```python
#crea una lista di 6 elementi
lista = [0,1,2,3,4,5]

#scorri tutti gli elementi della lista e stampa
for i in lista:
    print (i)
```

    0
    1
    2
    3
    4
    5


ora proviamo con le stringhe


```python
frase = 'il gatto mangia la pigna'
for carattere in frase:
    print (carattere)  #cosa stampa?
```

    i
    l

    g
    a
    t
    t
    o

    m
    a
    n
    g
    i
    a

    l
    a

    p
    i
    g
    n
    a

Il ciclo `for` legge la stringa esattamente come la lista dell'esempio precedente, scorrendo tutti gli elementi, in questo caso i caratteri (compreso lo spazio). Se si vuole dividere "per parola" bisogna ricorrere al metodo `split()`. Questo metodo non fa altro che dividere il testo in base al separatore specificato.

```python
frase = 'il gatto mangia la pigna'
frase_divisa = frase.split(' ')
for carattere in frase_divisa:
    print carattere
# cosa stampa ora?
```

Combinando il ciclo `for` e l'input da tastiera si possono specificare delle condizioni, come ad esempio limitare il numero di caratteri di una stringa inserita in input da parte dell'utente
