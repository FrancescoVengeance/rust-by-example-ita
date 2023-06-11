# Hello World

Questo è il codice di un programma Rust che stampa `Hello World!`:

```rust,editable
// Questo è un commento ed è ignorato dal compilatore.
// Puoi testare questo codice cliccando sul pulsante "Run" ->
// o se preferisci le shortcut puoi premere "Ctrl + Enter"

// Questo codice è modificabile, sentiti libero di farlo!
// Puoi sempre ritornare indietro premendo il tasto "Reset" ->

// Questa è la funzione main.
fn main() {

    // Stampa il testo in console.
    println!("Hello World!");
}
```

`println!` è una [*macro*][macros] che stampa il testo in console

Un file binario può essere generato utilizzando il compilatore: `rustc`.

```bash
$ rustc hello.rs
```

`rustc` restituirà un file binario chiamato `hello` che potrà essere eseguito.

```bash
$ ./hello
Hello World!
```

### Esercizio

Premi il pulsante 'Run' , come mostrato sopra, per vedere l'output. Dopo, aggiungi una nuova riga
con un altra macro `println!` per mostrare avere come risultato:

```text
Hello World!
I'm a Rustacean!
```

[macros]: macros.md
