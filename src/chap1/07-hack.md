# Hack & Security

Come qualsiasi altro componente di un sistema, fisico o software, anche i processori hanno delle vulnerabilità che devono essere conosciute.

Le vulnerabilità dei processori hanno fatto notizia all'inizio di quest'anno
con la divulgazione di due criticità che coinvolgono moltissimi processori attualmente in commericio: Meltdown e Spectre.

Meltdown e Spectre sono chiamati _side-channel attacks_ perché sfruttano l'implementazione fisica di alcuni algoritmi, e si contrappongono principalmente ai _brute force attacks_ che invece si basano, come dice il nome, su attacchi a "forza bruta".

Meltdown e Spectre si basano su alcune strategie di ottimizzazione del processore. Come abbiamo detto all'inizio di questo capitolo, il numero di operazioni al secondo che può fare un processore equivale più o meno alla sua frequenza, ad esempio 1.2 GHz. Oltre una certa frequenza di esecuzione non si può andare, per motivi fisici e quantistici. Per aumentare le prestazioni si usano quindi altri metodi, in particolare:
- _out-of-order processing_: le istruzioni vengono riordinate per cercare di eseguirne il più possibile ad ogni ciclo
- _branch prediction_: il corpo all'interno dei condizionali (es. `if`) viene eseguito prima di fare il controllo della condizione stessa, sempre per cercare di fare più operazioni ad ogni ciclo e non lasciare mai il processore sotto-utilizzato.

Non tutti i processori usano queste strategie: ad esempio i Cortex-A7 e Cortex-A53 non le usano e non sono quindi vulnerabili a Meltdown e Spectre.

> Per appofondimenti su questo tema, si consiglia caldamente la lettura di [questo post](https://www.raspberrypi.org/blog/why-raspberry-pi-isnt-vulnerable-to-spectre-or-meltdown/).
