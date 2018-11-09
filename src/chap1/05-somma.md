# Somma di interi
Prendiamo come esempio una semplice operazione e proviamo a capire come deve essere trasformata
per poter essere eseguita da un processore.

Ipotizziamo che vogliamo sommare due numeri interi. Come dobbiamo fare? Ricordiamoci che il processore può solo leggere e scrivere sulla
memoria, ed effettuare semplici operazioni. Il processore inizia e finisce in uno stato "vuoto", quindi tutto quello che deve fare e tutti i dati che usa devono essere già in memoria prima dell'esecuzione del programma.

Proviamo a scomporre in piccoli passi:
1. leggo dalla memoria il primo addendo, e lo copio in un _registro interno_, ad esempio `regA`
1. leggo dalla memoria il secondo addendo, e lo copio in un altro _registro interno_, ad esempio `regB`
1. leggo dalla memoria l'operazione che devo eseguire, in questo caso somma
1. eseguo l'operazione
1. scrivo il risultato in un registro, per ottimizzare posso riutilizzare il `regA` (così uso solo due registri in totale)
1. copio il contenuto di `regA` in memoria.

OK, sembra che ci siamo. Proviamo a vedere se funziona effettivamente così. Per verificare,
utilizzeremo il linguaggio C perché è quello che ha meno "passaggi" dal codice sorgente al compilato.

```
int main() {
  int a = 12;
  int b = 32;
  int c = a + b;
  return 0;
}
```

Per salvare questo file in locale, utilizzate l'editor `nano`.
```
$ nano
```

 Ricopiate il codice sopra, salvatelo con `ctrl-o` con il nome `main.c`, ed uscite dall'editor con `ctrl-x`.

> Un alternativa più professionale a `nano` è `vim`, lo trovate già installato sulla Raspberry. Un tutorial efficace e divertente per imparare a usare vim è [Vim Adventures](https://vim-adventures.com/).

Ora compiliamo il file con `gcc` e ci facciamo generare l'assembly con l'opzione `-S`:

```
$ gcc -S main.c
```

Otteniamo un output simile al seguente:

```
.arch armv6
.eabi_attribute 28, 1
.eabi_attribute 20, 1
.eabi_attribute 21, 1
.eabi_attribute 23, 3
.eabi_attribute 24, 1
.eabi_attribute 25, 1
.eabi_attribute 26, 2
.eabi_attribute 30, 6
.eabi_attribute 34, 1
.eabi_attribute 18, 4
.file	"main.c"
.text
.align	2
.global	main
.syntax unified
.arm
.fpu vfp
.type	main, %function
main:
@ args = 0, pretend = 0, frame = 16
@ frame_needed = 1, uses_anonymous_args = 0
@ link register save eliminated.
str	fp, [sp, #-4]!
add	fp, sp, #0
sub	sp, sp, #20
mov	r3, #12
str	r3, [fp, #-8]
mov	r3, #32
str	r3, [fp, #-12]
ldr	r2, [fp, #-8]
ldr	r3, [fp, #-12]
add	r3, r2, r3
str	r3, [fp, #-16]
mov	r3, #0
mov	r0, r3
add	sp, fp, #0
@ sp needed
ldr	fp, [sp], #4
bx	lr
.size	main, .-main
.ident	"GCC: (Raspbian 6.3.0-18+rpi1+deb9u1)
```

> Potete eseguire questi passi anche da Android. Dovrete installare prima gli strumenti di sviluppo con il comando `pkg install build-essential`.

La parte che ci interessa è quella all'interno della sezione `main:`.
```
mov	r3, #12
str	r3, [fp, #-8]
mov	r3, #32
str	r3, [fp, #-12]
ldr	r2, [fp, #-8]
ldr	r3, [fp, #-12]
add	r3, r2, r3
str	r3, [fp, #-16]
```
Le operazioni che può eseguire il processore sono quelle più a sinistra:
- `mov`: move, copia un valore costante in un registro
- `str`: store register, copia il valore dal registro alla memoria ad un certo indirizzo
- `ldr`: load register, copia il valore dalla memoria al registro ad un certo indirizzo

Analizziamo il codice assembly nel dettaglio:
- `mov	r3, #12`: assegna il valore `12` al registro `r3`
- `str	r3, [fp, #-8]`: copia il valore del registro `r3` nell'indirizzo di memoria `-8`
- `mov	r3, #32`: assegna il valore `32` al registro `r3`
- `str	r3, [fp, #-8]`: copia il valore del registro `r3` nell'indirizzo di memoria `-12`
- `ldr	r2, [fp, #-8]`: copia il dato all'indirizzo di memoria `-8` nel registro `r2`
- `ldr	r3, [fp, #-12]`: copia il dato all'indirizzo di memoria `-12` nel registro `r3`
- `add	r3, r2, r3`: effettua la somma dei registri `r3` e `r2` ed assegna il risultato a `r3`
- `str	r3, [fp, #-16]`: copia il valore del registro r3 nell'area di memoria `-16`

Concettualmente, è così che funziona un processore: anche le operazioni molto complesse vengono suddivise in piccoli parti
fino ad arrivare ad un risultato molto simile a quello presentato.
