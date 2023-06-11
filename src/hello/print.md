# Stampare testo formattato

La stampa è gestita da una serie di  [`macro`][macros] definite nel modulo
[`std::fmt`][fmt] alcune delle quali sono:

* `format!`: scrive testo formattato su una [`Stringa`][string]
* `print!`: simile `format!` ma stampa il testo in console (io::stdout).
* `println!`: come `print!` ma stampa e va a capo.
* `eprint!`: lo stesso di `print!`, ma il testo viene stampato sulla standard error
  (io::stderr).
* `eprintln!`: come `eprint!` ma stampa e va a capo.

Tutti i testi vengono analizzati nello stesso modo. 
Inoltre, Rust controlla la correttezza della formattazione durante la compilazione.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // In generale, le parentesi graffe `{}` vengono automaticamente sostituite con gli argomenti specificati. 
    // Gli argomenti passati alla macro vengono convertiti in stringhe.
    println!("{} days", 31);

    // Gli argomenti possono anche essere posizionali. Specificando un indice all'interno di {}
    // si determina quale argomento in quella determinata posizione verrà sostituito
    // Gli indici degli argomenti partono da 0 immediatamente dopo la stringa di formattazione.
    println!("{0}, this is {1}. {1}, this is {0}", "Alice", "Bob");

    // Gli argomenti possono anche essere nominali
    println!("{subject} {verb} {object}",
             object="the lazy dog",
             subject="the quick brown fox",
             verb="jumps over");

    // È possibile richiamare diversi tipi di formattazione specificando il carattere di formattazione corrispondente
    // dopo il carattere `:`.
    println!("Base 10:               {}",   69420); // 69420
    println!("Base 2 (binary):       {:b}", 69420); // 10000111100101100
    println!("Base 8 (octal):        {:o}", 69420); // 207454
    println!("Base 16 (hexadecimal): {:x}", 69420); // 10f2c
    println!("Base 16 (hexadecimal): {:X}", 69420); // 10F2C

    // È possibile allineare a destra il testo con una larghezza specificata. Questo stamperà
    // Questo stamperà "    1". (Quattro spazi e un "1", per una larghezza totale di 5.)
    println!("{number:>5}", number=1);

    // È possibile aggiungere zeri aggiuntivi per completare i numeri
    println!("{number:0>5}", number=1); // 00001
    // E' possibile allineare a sinistra invertendo il segno. Ciò produrrà l'output "10000".
    println!("{number:0<5}", number=1); // 10000

    // È possibile utilizzare gli argomenti nominali nel formato specificatore aggiungendo un `$`.
    println!("{number:0>width$}", number=1, width=5);

    // Rust controlla anche che il numero corretto di argomenti venga utilizzato.
    println!("My name is {0}, {1} {0}", "Bond");
    // FIXME ^ Aggiungi l'argomento mancante: "James"

    // Solo i tipi che implementano `fmt::Display` possono essere formattati con `{}`.
    // I tipi definiti dall'utente non implementano `fmt::Display` automaticamente.

    #[allow(dead_code)] // disabilita il `dead_code` che solleva un warning per i moduli importati ma non utilizzati
    struct Structure(i32);

    // Questo non compilerà perché `Structure` non implementa `fmt::Display`.
    // println!("This struct `{}` won't print...", Structure(3));
    // TODO ^ prova ad eliminare il commento su questa riga

    // Per Rust 1.58 e versioni successive, puoi catturare direttamente l'argomento da una variabile circostante.
    // Proprio come nell'esempio precedente, ciò produrrà l'output desiderato.
    // "    1", 4 spazi vuoti e un "1".
    let number: f64 = 1.0;
    let width: usize = 5;
    println!("{number:>width$}");
}
```

[`std::fmt`][fmt] contiene diversi [`trait`][traits] che regolano la formattazione del testo.
Di seguito sono elencate le forme di base di due strumenti importanti:

* `fmt::Debug`: Utilizza il marcatore `{:?}`. Formatta il testo per scopi di debug.
* `fmt::Display`: Utilizza il marcatore `{}`. Formatta il testo in modo più elegante e user-friendly.

In questo caso, abbiamo usato `fmt::Display` perché la libreria std fornisce implementazioni per questi tipi.
Per stampare il testo per i tipi personalizzati, sono necessari altri passaggi.

Implementare il trait `fmt::Display` significa ereditare anche l'implementazione del trait
[`ToString`] che permette di [convertire] il tipo in una [`Stringa`][string].

Alla *riga 46*, `#[allow(dead_code)]` è un [attributo] che si applica solo al modulo in cui è contenuto.

### Esercizi

* Correggere il problema nel codice precedente (vedere FIXME) in modo che venga eseguito senza errori.
* Prova a togliere il commento dalla riga che tenta di formattare la struct `Structure`
  (vedere TODO)
* Aggiungere una chiamata macro `println!` che stampa: `Pi è approssimativamente 3,142` controllando
  il numero di cifre decimali visualizzate. Ai fini di questo esercizio, utilizzare
  `let pi = 3,141592` come stima del pi greco. (Suggerimento: potrebbe essere necessario controllare il parametro
  [`std::fmt`][fmt] per impostare il numero di decimali da visualizzare.)

### Vedi anche:

[`std::fmt`][fmt], [`macros`][macros], [`struct`][structs], [`traits`][traits], e [`dead_code`][dead_code]

[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../macros.md
[string]: ../std/str.md
[structs]: ../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[convertire]: ../conversion/string.md
[attributo]: ../attribute.md
[dead_code]: ../attribute/unused.md
