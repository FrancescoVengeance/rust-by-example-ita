# Commenti

Ogni programma ha bisogno dei commenti e Rust ne supporta di diversi formati

* *Commenti standard* i quali sono ignorati dal compilatore:
  * `// Commento in-line valido fine a fine riga.`
  * `/* Blocco di commento che termina con il delimiter . */`
* *Documentazione* mostrate in formato HTML [documentazione][docs]:
  * `/// Genera documentazione per l'elemento seguente.`
  * `//! Genera documentazione per l'elemento che lo contiene.`

```rust,editable
fn main() {
    // Questo è un esempio di commento in-line
    // Ci sono due slash all'inizio della riga.
    // E niente scritto dopo i due slash è interpretato dal compilatore.

    // println!("Hello, world!");

    // Eseguilo. Vedi? Adesso rieseguilo eliminando i due slash.

    /*
     * Questo è un altro tipo di commento, un blocco di commento. In generale,
     * i commenti in-line sono i più utilizzati. Ma i blocco di commento
     * è molto utile per disabilitare all'instante molte rige di codice.
     * /* Blocchi di commento possono essere /* innestati, */ */ quindi basta
     * digitare un paio di caratteri per commentare tutto in questa funzione main().
     * /*/*/* Prova! */*/*/
     */

    /*
    Nota: La colonna di `*` è solo per stile ma in realtà non ce n'è bisogno.
    */

    // È possibile manipolare le espressioni più facilmente con i commenti in blocco
    // rispetto a quelli in-line. Prova a eliminare i delimitatori dei commenti
    // per modificare il risultato:
    let x = 5 + /* 90 + */ 5;
    println!("Is `x` 10 or 100? x = {}", x);
}
```

### Vedi anche:

[Documentare una libreria][docs]

[docs]: ../meta/doc.md
