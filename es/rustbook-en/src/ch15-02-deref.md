## Tratar los punteros inteligentes como referencias regulares con el rasgo de `Deref`

La implementación del rasgo `Deref` permite personalizar el comportamiento del *operador de desreferencia* , `*` (a diferencia del operador de multiplicación o glob). Al implementar `Deref` de tal manera que un puntero inteligente pueda tratarse como una referencia regular, puede escribir código que funcione con referencias y usar ese código también con punteros inteligentes.

Primero veamos cómo funciona el operador de desreferencia con referencias regulares. Luego intentaremos definir un tipo personalizado que se comporte como `Box<T>` , y veremos por qué el operador de desreferencia no funciona como una referencia en nuestro tipo recién definido. Exploraremos cómo implementar el rasgo de `Deref` hace posible que los punteros inteligentes funcionen de manera similar a las referencias. Luego veremos la *función de coerción deref* de Rust y cómo nos permite trabajar con referencias o punteros inteligentes.

> Nota: hay una gran diferencia entre el tipo `MyBox<T>` que estamos a punto de construir y el verdadero `Box<T>` : nuestra versión no almacenará sus datos en el montón. Estamos centrando este ejemplo en `Deref` , por lo que el lugar donde se almacenan los datos es menos importante que el comportamiento de puntero.

### Seguir el puntero al valor con el operador de desreferencia

Una referencia regular es un tipo de puntero, y una forma de pensar en un puntero es como una flecha a un valor almacenado en otro lugar. En el Listado 15-6, creamos una referencia a un valor de `i32` y luego utilizamos el operador de referencia para seguir la referencia a los datos:

<span class="filename">Nombre de archivo: src / main.rs</span>

```rust
fn main() {
    let x = 5;
    let y = &x;

    assert_eq!(5, x);
    assert_eq!(5, *y);
}
```

<span class="caption">Listado 15-6: Uso del operador de referencia para seguir una referencia a un valor <code>i32</code></span>

La variable `x` tiene un valor `i32` , `5` . Ponemos `y` igual a una referencia a `x` . Podemos afirmar que `x` es igual a `5` . Sin embargo, si queremos hacer una afirmación sobre el valor en `y` , tenemos que usar `*y` para seguir la referencia al valor al que apunta (por lo tanto, *desreferencia* ). Una vez que eliminar la referencia `y` , tenemos acceso al valor entero `y` está apuntando a que podemos comparar con `5` .

Si tratamos de escribir `assert_eq!(5, y);` en su lugar, obtendríamos este error de compilación:

```text
error[E0277]: can't compare `{integer}` with `&{integer}`
 --> src/main.rs:6:5
  |
6 |     assert_eq!(5, y);
  |     ^^^^^^^^^^^^^^^^^ no implementation for `{integer} == &{integer}`
  |
  = help: the trait `std::cmp::PartialEq<&{integer}>` is not implemented for
  `{integer}`
```

No se permite comparar un número y una referencia a un número porque son tipos diferentes. Debemos usar el operador de desreferencia para seguir la referencia al valor al que apunta.

### Usando `Box<T>` como una referencia

Podemos reescribir el código en el Listado 15-6 para usar un `Box<T>` lugar de una referencia; el operador de desreferencia funcionará como se muestra en el Listado 15-7:

<span class="filename">Nombre de archivo: src / main.rs</span>

```rust
fn main() {
    let x = 5;
    let y = Box::new(x);

    assert_eq!(5, x);
    assert_eq!(5, *y);
}
```

<span class="caption">Listado 15-7: Uso del operador de desreferencia en un <code>Box<i32></code></span>

La única diferencia entre el Listado 15-7 y el Listado 15-6 es que aquí establecemos `y` como una instancia de un cuadro que apunta al valor en `x` en lugar de una referencia que apunta al valor de `x` . En la última afirmación, podemos usar el operador de desreferencia para seguir el puntero del cuadro de la misma manera que lo hicimos cuando `y` era una referencia. A continuación, exploraremos qué tiene de especial `Box<T>` que nos permite usar el operador de desreferencia definiendo nuestro propio tipo de caja.

### Definiendo nuestro propio puntero inteligente

Construyamos un puntero inteligente similar al tipo `Box<T>` proporcionado por la biblioteca estándar para experimentar cómo los punteros inteligentes se comportan de manera diferente a las referencias de forma predeterminada. Luego veremos cómo agregar la capacidad de usar el operador de desreferencia.

El tipo `Box<T>` se define en última instancia como una estructura de tupla con un elemento, por lo que el Listado 15-8 define un tipo `MyBox<T>` de la misma manera. También definiremos una `new` función para que coincida con la `new` función definida en el `Box<T>` .

<span class="filename">Nombre de archivo: src / main.rs</span>

```rust
struct MyBox<T>(T);

impl<T> MyBox<T> {
    fn new(x: T) -> MyBox<T> {
        MyBox(x)
    }
}
```

<span class="caption">Listado 15-8: Definición de un tipo <code>MyBox<T></code></span>

Definimos una estructura llamada `MyBox` y declaramos un parámetro genérico `T` , porque queremos que nuestro tipo contenga valores de cualquier tipo. El tipo `MyBox` es una estructura de tupla con un elemento de tipo `T` La función `MyBox::new` toma un parámetro de tipo `T` y devuelve una instancia de `MyBox` que contiene el valor pasado.

Intentemos agregar la función `main` en el Listado 15-7 al Listado 15-8 y cambiarla para usar el tipo `MyBox<T>` que hemos definido en lugar de `Box<T>` . El código en el Listado 15-9 no se compilará porque Rust no sabe cómo desreferenciar `MyBox` .

<span class="filename">Nombre de archivo: src / main.rs</span>

```rust,ignore,does_not_compile
fn main() {
    let x = 5;
    let y = MyBox::new(x);

    assert_eq!(5, x);
    assert_eq!(5, *y);
}
```

<span class="caption">Listado 15-9: Intentando usar <code>MyBox<T></code> de la misma manera que usamos referencias y <code>Box<T></code></span>

Aquí está el error de compilación resultante:

```text
error[E0614]: type `MyBox<{integer}>` cannot be dereferenced
  --> src/main.rs:14:19
   |
14 |     assert_eq!(5, *y);
   |                   ^^
```

Nuestro tipo `MyBox<T>` no puede ser desreferenciado porque no hemos implementado esa capacidad en nuestro tipo. Para habilitar la desreferenciación con el operador `*` , implementamos el rasgo `Deref` .

### Tratar un tipo como una referencia implementando el rasgo de `Deref`

Como se discutió en el Capítulo 10, para implementar un rasgo, necesitamos proporcionar implementaciones para los métodos requeridos del rasgo. El `Deref` rasgo, proporcionado por la biblioteca estándar, nos exige poner en práctica un método llamado `deref` que toma prestado `self` y devuelve una referencia a los datos internos. El Listado 15-10 contiene una implementación de `Deref` para agregar a la definición de `MyBox` :

<span class="filename">Nombre de archivo: src / main.rs</span>

```rust
use std::ops::Deref;

# struct MyBox<T>(T);
impl<T> Deref for MyBox<T> {
    type Target = T;

    fn deref(&self) -> &T {
        &self.0
    }
}
```

<span class="caption">Listado 15-10: Implementando <code>Deref</code> en <code>MyBox<T></code></span>

El `type Target = T;` La sintaxis define un tipo asociado para el rasgo de `Deref` a utilizar. Los tipos asociados son una forma ligeramente diferente de declarar un parámetro genérico, pero no necesita preocuparse por ellos por ahora; los cubriremos con más detalle en el Capítulo 19.

We fill in the body of the `deref` method with `&self.0` so `deref` returns a reference to the value we want to access with the `*` operator. The `main` function in Listing 15-9 that calls `*` on the `MyBox<T>` value now compiles, and the assertions pass!

Sin el rasgo de `Deref` , el compilador solo puede eliminar referencias `&` referencias. El `deref` método da el compilador la capacidad de tomar un valor de cualquier tipo que implementa `Deref` y llamar a la `deref` método para obtener una `&` de referencia que se sabe cómo eliminar la referencia.

Cuando ingresamos `*y` en el Listado 15-9, Rust detrás de escena ejecutó este código:

```rust,ignore
*(y.deref())
```

Rust sustituye al operador `*` con una llamada al método `deref` y luego una simple referencia para que no tengamos que pensar si necesitamos o no llamar al método `deref` . Esta característica Rust nos permite escribir código que funciona de manera idéntica si tenemos una referencia regular o un tipo que implementa `Deref` .

The reason the `deref` method returns a reference to a value, and that the plain dereference outside the parentheses in `*(y.deref())` is still necessary, is the ownership system. If the `deref` method returned the value directly instead of a reference to the value, the value would be moved out of `self`. We don’t want to take ownership of the inner value inside `MyBox<T>` in this case or in most cases where we use the dereference operator.

Tenga en cuenta que el operador `*` se reemplaza con una llamada al método `deref` y luego una llamada al operador `*` solo una vez, cada vez que usamos un `*` en nuestro código. Debido a que la sustitución del operador `*` no se repite infinitamente, terminamos con datos del tipo `i32` , ¡que coinciden con los `5` en `assert_eq!` en el Listado 15-9.

### Coerciones implícitas de Deref con funciones y métodos

*La coerción de Deref* es una conveniencia que Rust realiza en argumentos de funciones y métodos. La coerción de Deref convierte una referencia a un tipo que implementa `Deref` en una referencia a un tipo en el que `Deref` puede convertir el tipo original. La coerción de Deref ocurre automáticamente cuando pasamos una referencia al valor de un tipo particular como argumento a una función o método que no coincide con el tipo de parámetro en la definición de función o método. Una secuencia de llamadas al método `deref` convierte el tipo que proporcionamos en el tipo que necesita el parámetro.

La coerción de Deref se agregó a Rust para que los programadores que escriben llamadas a funciones y métodos no necesiten agregar tantas referencias explícitas y desreferencias con `&` y `*` . La función de coerción deref también nos permite escribir más código que puede funcionar para referencias o punteros inteligentes.

Para ver la coerción de deref en acción, usemos el tipo `MyBox<T>` que definimos en el Listado 15-8, así como la implementación de `Deref` que agregamos en el Listado 15-10. El listado 15-11 muestra la definición de una función que tiene un parámetro de corte de cadena:

<span class="filename">Nombre de archivo: src / main.rs</span>

```rust
fn hello(name: &str) {
    println!("Hello, {}!", name);
}
```

<span class="caption">Listado 15-11: Una función de <code>hello</code> que tiene el <code>name</code> del parámetro de tipo <code>&str</code></span>

Podemos llamar a la función `hello` con un corte de cadena como argumento, como `hello("Rust");` por ejemplo. La coerción de Deref hace posible llamar a `hello` con una referencia a un valor de tipo `MyBox<String>` , como se muestra en el Listado 15-12:

<span class="filename">Nombre de archivo: src / main.rs</span>

```rust
# use std::ops::Deref;
#
# struct MyBox<T>(T);
#
# impl<T> MyBox<T> {
#     fn new(x: T) -> MyBox<T> {
#         MyBox(x)
#     }
# }
#
# impl<T> Deref for MyBox<T> {
#     type Target = T;
#
#     fn deref(&self) -> &T {
#         &self.0
#     }
# }
#
# fn hello(name: &str) {
#     println!("Hello, {}!", name);
# }
#
fn main() {
    let m = MyBox::new(String::from("Rust"));
    hello(&m);
}
```

<span class="caption">Listado 15-12: Llamando <code>hello</code> con una referencia a un valor <code>MyBox<String></code> , que funciona debido a la coerción deref</span>

Aquí estamos llamando a la función `hello` con el argumento `&m` , que es una referencia a un valor `MyBox<String>` . Debido a que implementamos el rasgo `Deref` en `MyBox<T>` en el Listado 15-10, Rust puede convertir `&MyBox<String>` en `&String` llamando a `deref` . La biblioteca estándar proporciona una implementación de `Deref` en `String` que devuelve un segmento de cadena, y esto se encuentra en la documentación de la API para `Deref` . Rust llama a `deref` nuevamente para convertir el `&String` en `&str` , que coincide con la definición de la función `hello` .

Si Rust no implementó la coerción deref, tendríamos que escribir el código en el Listado 15-13 en lugar del código en el Listado 15-12 para llamar a `hello` con un valor de tipo `&MyBox<String>` .

<span class="filename">Nombre de archivo: src / main.rs</span>

```rust
# use std::ops::Deref;
#
# struct MyBox<T>(T);
#
# impl<T> MyBox<T> {
#     fn new(x: T) -> MyBox<T> {
#         MyBox(x)
#     }
# }
#
# impl<T> Deref for MyBox<T> {
#     type Target = T;
#
#     fn deref(&self) -> &T {
#         &self.0
#     }
# }
#
# fn hello(name: &str) {
#     println!("Hello, {}!", name);
# }
#
fn main() {
    let m = MyBox::new(String::from("Rust"));
    hello(&(*m)[..]);
}
```

<span class="caption">Listado 15-13: El código que tendríamos que escribir si Rust no tuviera coerción</span>

El `(*m)` elimina la referencia de `MyBox<String>` en una `String` . Luego, `&` y `[..]` toman una porción de cadena de la `String` que es igual a la cadena completa para que coincida con la firma de `hello` . El código sin coacciones deref es más difícil de leer, escribir y comprender con todos estos símbolos involucrados. La coerción de Deref le permite a Rust manejar estas conversiones automáticamente.

Cuando el rasgo de `Deref` se define para los tipos involucrados, Rust analizará los tipos y usará `Deref::deref` tantas veces como sea necesario para obtener una referencia que coincida con el tipo de parámetro. El número de veces que `Deref::deref` debe insertarse se resuelve en el momento de la compilación, por lo que no hay penalización en tiempo de ejecución por aprovechar la coerción de deref.

### Cómo interactúa Deref Coercion con la mutabilidad

De manera similar a cómo usa el rasgo `Deref` para anular el operador `*` en referencias inmutables, puede usar el rasgo `DerefMut` para anular el operador `*` en referencias mutables.

Rust hace una deserción de la coerción cuando encuentra tipos e implementaciones de rasgos en tres casos:

- De `&T` a `&U` cuando `T: Deref<Target=U>`
- De `&mut T` a `&mut U` cuando `T: DerefMut<Target=U>`
- De `&mut T` a `&U` cuando `T: Deref<Target=U>`

Los dos primeros casos son iguales excepto por la mutabilidad. El primer caso indica que si tiene un `&T` , y `T` implementa `Deref` en algún tipo `U` , puede obtener un `&U` transparente. El segundo caso establece que ocurre la misma coerción de deref para las referencias mutables.

El tercer caso es más complicado: Rust también obligará a una referencia mutable a una inmutable. Pero lo contrario *no* es posible: las referencias inmutables nunca obligarán a referencias mutables. Debido a las reglas de endeudamiento, si tiene una referencia mutable, esa referencia mutable debe ser la única referencia a esos datos (de lo contrario, el programa no se compilaría). Convertir una referencia mutable en una referencia inmutable nunca romperá las reglas de préstamo. La conversión de una referencia inmutable en una referencia mutable requeriría que solo haya una referencia inmutable a esos datos, y las reglas de préstamo no lo garantizan. Por lo tanto, Rust no puede suponer que es posible convertir una referencia inmutable en una referencia mutable.
