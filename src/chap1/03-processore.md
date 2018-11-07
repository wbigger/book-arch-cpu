# Il Processore

Cominciamo ad esaminare come lavora un processore più nel dettaglio.

Prima di tutto va compreso che, anche se può fare cose molto complesse,
il processore sa eseguire ad ogni passo solo operazioni _molto semplici_.
Volendo estremizzare, il processore fa fondamentalmente le seguenti cose:
- leggere e scrivere dalla memoria RAM
- fare operazioni logiche su numeri binari, ad esempio AND, OR, NOT, etc.
- fare operazioni aritmetiche su numeri binari, in particolare la somma

Le applicazioni complesse che conosciamo si basano su queste operazioni elementari.
Il vantaggio dei processori è che riescono a fare in un secondo miliardi di queste
operazioni: ad esempio il processore della Raspberry ha un clock di esecuzione di 1.4 GHz,
quindi riesce ad eseguire un miliardo e quattrocento milioni di operazioni in un secondo, più o meno.

> Il cervello funziona in modo molto diverso: ha una frequenza che va da 4 a 40 Hz, ma ad ogni iterazione fa moltissime
operazioni.

Un'altra cosa fondamentale da capire è che il processore capisce _solo numeri binari_.
Non esistono nient'altro che uno e zeri all'interno del processore. Questo è dovuto
al fatto che all'interno ci sono collegamenti elettrici e porte logiche, che possono
per l'appunto avere solo i valori di acceso (passa corrente) o spento (non passa corrente).
Tutto quello che non è binario deve essere convertito per poter essere utilizzato.
E' per questo che è fondamentale conoscere bene l'aritmetica binaria per poter
comprendere come funziona una CPU.

> Per impratichirvi con le porte logiche, vi consiglio di giocare a [Circuit Scramble](https://play.google.com/store/apps/details?id=com.Suborbital.CircuitScramble&hl=it). Per iOS non li conosco,
se avete un'app da proporre fatemi sapere che l'aggiungo qui!
