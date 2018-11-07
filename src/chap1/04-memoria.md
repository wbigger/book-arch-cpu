# La memoria

Il secondo componente fondamentale dei computer è la _memoria_.

Prima di tutto una precisazione: quando ora parliamo di memoria, intendiamo un tipo specifico chiamato
_memoria primaria_: generalmente è costituita dalla RAM, ovvero _Random Access Memory_, memoria ad accesso casuale.

<div>
<p align="center">
<img title="RAM" src='./assets/ram.png' width='50%'>
</p>
<p align="center">
<em>Diversi tipi di RAM. Fonte: wikipedia</em>
</p>
</div>

La caratteristica principale è che, come dice il nome, si può accedere a qualsiasi parte di questo tipo di memoria
semplicemente conoscendone la posizione, che è rappresentato da un numero intero. Questo numero viene anche detto _indirizzo_.
Al contrario, altri tipi di memoria come l'hard-disk, devono essere acceduti in maniera _sequenziale_: per poter accedere ad una certa porzione di memoria, bisogna prima _scorrere_ parte della memoria precedente: questo la rende ovviamente molto più lenta.

Possiamo immaginare la RAM come un lunghissimo nastro, diviso in caselle, proprio come il nastro della macchina di Turing.

<div>
<p align="center">
<img title="Turing machine" src='./assets/turing-machine.jpg' width='70%'>
</p>
<p align="center">
<em>Un esempio di macchina di Turing. Fonte: wikipedia</em>
</p>
</div>

Come dicevamo, la caratteristica di questa memoria è che si può accedere a qualsiasi casella, basta saperne l'indirizzo. Per convenzione e comodità, si usano i numeri esaedecimali per indicare l'indirizzo.

Torniamo al caso della nostra Raspberry. Per sapere la dimensione della memoria, possiamo usare il seguente comando da terminale.
```
$ cat /proc/meminfo
MemTotal:         949580 kB
MemFree:          335800 kB
MemAvailable:     698964 kB
Buffers:          196460 kB
Cached:           218844 kB
SwapCached:            0 kB
Active:           282936 kB
Inactive:         290512 kB
...
```

> Potete eseguire lo stesso comando anche sul vostro dispositivo Android.

L'output del comando è molto lungo, ho omesso la parte finale per brevità. Il dato che ci interessa in particolare è il primo: memoria totale pari a 949580 kB. Per convertirlo in byte, dobbiamo sapere quanto vale un `kB`: normalmente il prefisso `k` sta per kilo e significa 1000, ma in questo caso il kernel (che gestisce `/proc/meminfo`) usa una convenzione sua e vale 1024 :(.

Calcoliamo il numero totale di byte della memoria, e convertiamolo in esadecimale:
```
949580 kB = 949580 * 1024 = 972369920 (in base 10) = 0x39F53000 (in base 16)
```

Quindi, noi avremo un "nastro" di memoria RAM a cui possiamo accedere usando un indirizzo da 0x00000000 a 0x39F53000.

<p align="center">
<img title="RAM as a tape" src='./assets/ram-tape.png' width='90%'>
</p>
