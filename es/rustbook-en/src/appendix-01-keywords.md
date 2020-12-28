## Apéndice A: Palabras clave

The following list contains keywords that are reserved for current or future use by the Rust language. As such, they cannot be used as identifiers (except as raw identifiers as we’ll discuss in the “[Raw Identifiers]<!-- ignore -->” section), including names of functions, variables, parameters, struct fields, modules, crates, constants, macros, static values, attributes, types, traits, or lifetimes.

### Palabras clave actualmente en uso

Las siguientes palabras clave tienen actualmente la funcionalidad descrita.

- `as` : realizar fundición primitiva, eliminar la ambigüedad del rasgo específico que contiene un elemento o cambiar el nombre de los elementos en `use` y declaraciones de `extern crate`
- `break` - salir de un bucle inmediatamente
- `const` : define elementos constantes o punteros crudos constantes
- `continue` : continúa con la siguiente iteración del ciclo
- `crate` : vincule una caja externa o una macro variable que represente la caja en la que se define la macro
- `dyn` : envío dinámico a un objeto de rasgo
- `else` - alternativa para `if` y `if let` flujo de control se construya
- `enum` - define una enumeración
- `extern` : vincular una caja, función o variable externa
- `false` - Booleano falso literal
- `fn` - define una función o el tipo de puntero de función
- `for` : recorre los elementos de un iterador, implementa un rasgo o especifica una vida útil de mayor rango
- `if` - rama basada en el resultado de una expresión condicional
- `impl` - implementar funcionalidad inherente o característica
- `in` - parte de la sintaxis del bucle `for`
- `let` - enlazar una variable
- `loop` - bucle incondicionalmente
- `match` - hacer coincidir un valor con los patrones
- `mod` - define un módulo
- `move` - hacer que un cierre tome posesión de todas sus capturas
- `mut` - denota mutabilidad en referencias, punteros sin formato o enlaces de patrones
- `pub` : denota visibilidad pública en campos de estructura, bloques `impl` o módulos
- `ref` - enlazar por referencia
- `return` - retorno de la función
- `Self` : un alias de tipo para el tipo que implementa un rasgo
- `self` - método objeto o módulo actual
- `static` : variable global o vida útil que dura toda la ejecución del programa
- `struct` - define una estructura
- `super` - módulo padre del módulo actual
- `trait` - define un rasgo
- `true` : verdadero literal booleano
- `type` : define un alias de tipo o un tipo asociado
- `unsafe` : indica código, funciones, rasgos o implementaciones inseguros
- `use` - traer símbolos al alcance
- `where` - denota cláusulas que restringen un tipo
- `while` - bucle condicionalmente basado en el resultado de una expresión

### Palabras clave reservadas para uso futuro

Las siguientes palabras clave no tienen ninguna funcionalidad, pero Rust las reserva para un posible uso futuro.

- `abstract`
- `async`
- `await`
- `become`
- `box`
- `do`
- `final`
- `macro`
- `override`
- `priv`
- `try`
- `typeof`
- `unsized`
- `virtual`
- `yield`

### Identificadores sin procesar

*Los identificadores sin formato* son la sintaxis que le permite usar palabras clave donde normalmente no se permitirían. Utiliza un identificador sin formato prefijando una palabra clave con `r#` .

Por ejemplo, la `match` es una palabra clave. Si intenta compilar la siguiente función que usa `match` como su nombre:

<span class="filename">Nombre de archivo: src / main.rs</span>

```rust,ignore,does_not_compile
fn match(needle: &amp;str, haystack: &amp;str) -&gt; bool {
    haystack.contains(needle)
}
```

obtendrá este error:

```text
error: expected identifier, found keyword `match`
 --&gt; src/main.rs:4:4
  |
4 | fn match(needle: &amp;str, haystack: &amp;str) -&gt; bool {
  |    ^^^^^ expected identifier, found keyword
```

El error muestra que no puede utilizar la `match` palabras clave como identificador de función. Para usar la `match` como nombre de función, debe usar la sintaxis de identificador sin formato, como esta:

<span class="filename">Nombre de archivo: src / main.rs</span>

```rust
fn r#match(needle: &amp;str, haystack: &amp;str) -&gt; bool {
    haystack.contains(needle)
}

fn main() {
    assert!(r#match("foo", "foobar"));
}
```

Este código se compilará sin errores. Tenga en cuenta el prefijo `r#` en el nombre de la función en su definición, así como dónde se llama a la función en `main` .

Los identificadores sin formato le permiten usar cualquier palabra que elija como identificador, incluso si esa palabra es una palabra clave reservada. Además, los identificadores en bruto le permiten usar bibliotecas escritas en una edición de Rust diferente a la que usa su caja. Por ejemplo, `try` no es una palabra clave en la edición de 2015, pero sí en la edición de 2018. Si depende de una biblioteca que está escrita con la edición 2015 y tiene una función de `try` , necesitará usar la sintaxis de identificador sin formato, `r#try` en este caso, para llamar a esa función desde su código de edición 2018. Ver [Apéndice E]<!-- ignorar --> para obtener más información sobre las ediciones.


[Raw Identifiers]: #raw-identifiers
[Apéndice E]: appendix-05-editions.html