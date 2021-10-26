---
title: Around the globe
description: Descrizione di Around the globe
paragraph: [
    Uno script per il calcolo dell'azimut tra due punti della superfice terrestre.,
"Se vuoi sapere in che direzione girarti per guardare verso Tokyo o NewYork o qualunque altra città del mondo, questo è lo strumento che fa per te!"
        ]
img: 
    src: https://img.freepik.com/free-vector/globalization-concept-blue-lines-around-blue-globe_104327-79.jpg?size=626&ext=jpg&ga=GA1.2.1656752755.1627689600
    alt: Around the globe
tag: [
    Programmazione,
    Matematica
]
---

# Around the globe

<cMedia type="img" s="https://img.freepik.com/free-vector/globalization-concept-blue-lines-around-blue-globe_104327-79.jpg?size=626&ext=jpg&ga=GA1.2.1656752755.1627689600" a="Around the globe" provider="other"></cMedia>

## Introduzione
 
 Questo semplice script nasce da un esigenza reale di un mio amico: un giorno mi disse di voler creare un palo di **crocevia con dei cartelli che indicassero le città più importanti nel mondo**.
 Aveva quindi la necessità di sapere l'azimut con il quale angolare i cartelli di modo che fossero direzionati correttamente.
 Nello scrivere il codice si sono poi aggiunte altre piccole funzioni che danno quel tocco di originalità all'algoritmo. Ma partiamo dalle basi.


## Le basi di partenza

Lo scopo principale era quello di ottenere a partire dalle coordinate geografiche di due punti, l'azimut tra di essi.
[L'azimut](https://it.wikipedia.org/wiki/Azimut) è infatti l'angolo che si viene a formare tra la linea immaginaria che congiunge i due punti, e il meridiano passante per il punto iniziale.

<cMedia type="img" s="/v1635210809/Articoli/Around%20the%20globe/Azimut.jpg" c="Esempio di azimut tra due persone"></cMedia>

Utilizzando concetti base di Analisi e Geometria 2, è possibile visualizzare la superficie del [geoide terrestre](https://it.wikipedia.org/wiki/Geoide) attraverso un semplice sistema di 3 equazioni goniometriche.
A partire da una qualsiasi coppia latitudine - longitudine, ovvero coordinate polari, sono facilmente ricavabili le coordinate cartesiane, ovvero la terna dei valori x-y-z, del punto considerato.
**Sfruttando quindi le coordinate cartesiane è poi facile adoperare operazioni con vettori e piani**, essendo di fatto il sistema appena parametrizzato uno spazio euclideo formato dalla terna elemenatre dei versori I-J-K.

In particolare, per rappresentare al meglio il geoide terrestre, ho deciso di sfruttare l'ellissoide di Hayford, uno dei primi [ellissoidi di riferimento](https://it.wikipedia.org/wiki/Ellissoide_di_riferimento).

<cMedia type="img" s="/v1635210809/Articoli/Around%20the%20globe/Ellissoide_Matlab.png" c="L'ellissoide di Hayford rappresentato in Matlab"></cMedia>

## La matematica dietro l'algoritmo

Per il calcolo dell'azimut vengono sfruttati concetti base di Analisi e Geometria 1 applicati allo spazio tridimensionale.
Sfruttando la parametrizzazione euclidea, sappiamo essere possibili sia il prodotto scalare che il prodotto vettoriale ed è quindi naturale risolvere il problema in questi termini.


Ricordando che il nostro obbiettivo è **l'angolo definito come 'NORD - Osservatore - Oggetto osservato'**, rappresentandone un esempio applicato ad una sfera 3D, si ottiene la situazione descritta nell'immagine sotto.

<cMedia type="img" s="/v1635210809/Articoli/Around%20the%20globe/Azimut_matlab.png" a=""></cMedia>

Ma allora osservando che le linee che collegano 'NORD - Osservatore' e 'Osservatore - Oggetto osservato', non sono altro che le intersezioni di due piani cartesiani con la sfera, allora appare chiaro che **l'azimut cercato è di fatto l'angolo formato tra questi due piani: il primo passante per i tre punti 'NORD - Osservatore - Centro della sfera', mentre il secondo passante per i tre punti 'Osservatore - Oggetto osservato - Centro della sfera'**.


Sapendo poi che ogni piano cartesiano è individuato tramire un vettore normale al piano stesso, e che l'angolo tra due vettori è ricavabile per via trigonometrica, allora l'azimut cercato ha valore:

<cMedia type="img" s="/v1635210809/Articoli/Around%20the%20globe/Formula_finale_azimut.png" c="Formula finale per il calcolo dell'azimut (p1/p2 = vettori normali ai due piani cartesiani)"></cMedia>

Per avere una comprensione più chiara e gloabale del problema e della sua soluzione, è forse utile osservare il tutto in maniera più interattiva grazie all'uso di GeoGebra.

<cMedia type="frame" s="https://www.geogebra.org/3d/snm5rqfd?embed" a="File di GeoGebra"></cMedia>

[Link al file online di GeoGebra](https://www.geogebra.org/3d/snm5rqfd)


## L'algoritmo

L'implementazione a livello di algoritmo di tutta la matematica spiegata sopra, avviene per mezzo di **JavaScript** e in particolare della libreria **Math.js**.
La libreria offre infatti una vasta scelta di operatori e funzioni matematiche a partire dalle basilari di trigonometria fino ad operazioni con vettori e matrici e non solo.


Dopo aver salvato i dati di latitudine e longitudine in un array, ne esegue la conversione da gradi a radianti di modo da facilitare l'uso di funzioni trigonometriche essenziali per ricavare poi le coordinate cartesiane dei punti.

<cMedia type="img" s="/v1635210809/Articoli/Around%20the%20globe/Algoritmo_coordinate_cartesiane.png" c="L'algoritmo per il cambio di parametrizzazione"></cMedia>

Successivamente l'algoritmo elabora i vettori normali ai due piani cartesiani necessari per il calcolo dell'azimut.
Per fare ciò calcola, come sottrazione di coordinate dei tre punti di riferimento, due vettori che appartengono al piano e, con l'utilizzo del prodotto vettoriale su quest'ultimi, **calcola il vettore normale al piano cartesiano**.
L'operazione viene poi ripetuta anche per il secondo piano cartesiano e **infine viene calcolato l'angolo formato tra i due vettori normali ai piani**, ottenendo così l'azimut ricercato.

<cMedia type="img" s="/v1635210809/Articoli/Around%20the%20globe/Algoritmo_vettore_piano.png" c="Vettore normale al piano - Calcolo dell'angolo tra vettori"></cMedia>

## Testalo e divertiti!

Il programmino è ovviamente online e di libero utilizzo.
Contiene come detto nell'introduzione molte altre funzioni divertenti ed interessanti come il calcolo delle distanze o altro ancora.<br>
Se vuoi dare uno sguardo al codice lo trovi su GitHub a questo <a href="#">link</a>, altrimenti se vuoi direttamente provare il programma naviga nella sezione:

<a href="/portale/around_the_globe" class="button">App > Portale > Around_the_globe</a>

**Non ti sei mai chiesto con quale inclinazione scavare un tunnel fino a Tokyo?** E per quanto dovresti scavare? Il programma ha tutte le risposte alle tue domande! Buon utilizzo!