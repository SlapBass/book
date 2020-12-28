# El lenguaje de programación Rust

[El lenguaje de programación Rust](title-page.md)

[Prefacio](foreword.md)

[Introducción](ch00-00-introduction.md)

## Empezando

- [Empezando](ch01-00-getting-started.md)

    - [Instalación](ch01-01-installation.md)
    - [¡Hola Mundo!](ch01-02-hello-world.md)
    - [¡Hola, Cargo!](ch01-03-hello-cargo.md)

- [Programación de un juego de adivinanzas](ch02-00-guessing-game-tutorial.md)

- [Conceptos de programación comunes](ch03-00-common-programming-concepts.md)

    - [Variables y mutabilidad](ch03-01-variables-and-mutability.md)
    - [Tipos de datos](ch03-02-data-types.md)
    - [Funciones](ch03-03-how-functions-work.md)
    - [Comentarios](ch03-04-comments.md)
    - [Flujo de control](ch03-05-control-flow.md)

- [Entender la propiedad](ch04-00-understanding-ownership.md)

    - [¿Qué es la propiedad?](ch04-01-what-is-ownership.md)
    - [Referencias y préstamos](ch04-02-references-and-borrowing.md)
    - [El tipo de rebanada](ch04-03-slices.md)

- [Uso de estructuras para estructurar datos relacionados](ch05-00-structs.md)

    - [Definición y creación de instancias de estructuras](ch05-01-defining-structs.md)
    - [Un programa de ejemplo que utiliza estructuras](ch05-02-example-structs.md)
    - [Sintaxis del método](ch05-03-method-syntax.md)

- [Enumeraciones y coincidencia de patrones](ch06-00-enums.md)

    - [Definición de una enumeración](ch06-01-defining-an-enum.md)
    - [El operador de flujo de control de `match`](ch06-02-match.md)
    - [Flujo de control conciso con `if let`](ch06-03-if-let.md)

## Conocimientos básicos sobre el óxido

- [Gestión de proyectos en crecimiento con paquetes, cajas y módulos](ch07-00-managing-growing-projects-with-packages-crates-and-modules.md)

    - [Paquetes y cajas](ch07-01-packages-and-crates.md)
    - [Definición de módulos para controlar el alcance y la privacidad](ch07-02-defining-modules-to-control-scope-and-privacy.md)
    - [Rutas para hacer referencia a un elemento en el árbol del módulo](ch07-03-paths-for-referring-to-an-item-in-the-module-tree.md)
    - [Llevando rutas al alcance con la palabra clave `use`](ch07-04-bringing-paths-into-scope-with-the-use-keyword.md)
    - [Separación de módulos en diferentes archivos](ch07-05-separating-modules-into-different-files.md)

- [Colecciones comunes](ch08-00-common-collections.md)

    - [Almacenamiento de listas de valores con vectores](ch08-01-vectors.md)
    - [Almacenamiento de texto codificado en UTF-8 con cadenas](ch08-02-strings.md)
    - [Almacenamiento de claves con valores asociados en mapas hash](ch08-03-hash-maps.md)

- [Manejo de errores](ch09-00-error-handling.md)

    - [Errores irrecuperables con `panic!`](ch09-01-unrecoverable-errors-with-panic.md)
    - [Errores recuperables con `Result`](ch09-02-recoverable-errors-with-result.md)
    - [¡Al `panic!` o ¡Que no `panic!`](ch09-03-to-panic-or-not-to-panic.md)

- [Tipos genéricos, rasgos y vidas](ch10-00-generics.md)

    - [Tipos de datos genéricos](ch10-01-syntax.md)
    - [Rasgos: definición de comportamiento compartido](ch10-02-traits.md)
    - [Validación de referencias con vidas útiles](ch10-03-lifetime-syntax.md)

- [Escribir pruebas automatizadas](ch11-00-testing.md)

    - [Cómo escribir pruebas](ch11-01-writing-tests.md)
    - [Controlar cómo se ejecutan las pruebas](ch11-02-running-tests.md)
    - [Organización de prueba](ch11-03-test-organization.md)

- [Un proyecto de E / S: creación de un programa de línea de comandos](ch12-00-an-io-project.md)

    - [Aceptación de argumentos de la línea de comandos](ch12-01-accepting-command-line-arguments.md)
    - [Leer un archivo](ch12-02-reading-a-file.md)
    - [Refactorización para mejorar la modularidad y el manejo de errores](ch12-03-improving-error-handling-and-modularity.md)
    - [Desarrollo de la funcionalidad de la biblioteca con desarrollo basado en pruebas](ch12-04-testing-the-librarys-functionality.md)
    - [Trabajar con variables de entorno](ch12-05-working-with-environment-variables.md)
    - [Escribir mensajes de error en error estándar en lugar de salida estándar](ch12-06-writing-to-stderr-instead-of-stdout.md)

## Pensando en Rust

- [Características del lenguaje funcional: iteradores y cierres](ch13-00-functional-features.md)

    - [Cierres: funciones anónimas que pueden capturar su entorno](ch13-01-closures.md)
    - [Procesamiento de una serie de elementos con iteradores](ch13-02-iterators.md)
    - [Mejorando nuestro proyecto de E / S](ch13-03-improving-our-io-project.md)
    - [Comparación del rendimiento: bucles frente a iteradores](ch13-04-performance.md)

- [Más sobre Cargo y Crates.io](ch14-00-more-about-cargo.md)

    - [Personalización de compilaciones con perfiles de versión](ch14-01-release-profiles.md)
    - [Publicar una caja en Crates.io](ch14-02-publishing-to-crates-io.md)
    - [Espacios de trabajo de carga](ch14-03-cargo-workspaces.md)
    - [Instalación de binarios desde Crates.io con `cargo install`](ch14-04-installing-binaries.md)
    - [Extensión de carga con comandos personalizados](ch14-05-extending-cargo.md)

- [Punteros inteligentes](ch15-00-smart-pointers.md)

    - [Uso de `Box<T>` para apuntar a datos en el montón](ch15-01-box.md)
    - [Tratar los punteros inteligentes como referencias regulares con el rasgo `Deref`](ch15-02-deref.md)
    - [Ejecutar código en limpieza con el rasgo de `Drop`](ch15-03-drop.md)
    - [`Rc<T>` , el puntero inteligente contado de referencia](ch15-04-rc.md)
    - [`RefCell<T>` y el patrón de mutabilidad interior](ch15-05-interior-mutability.md)
    - [Los ciclos de referencia pueden perder memoria](ch15-06-reference-cycles.md)

- [Concurrencia intrépida](ch16-00-concurrency.md)

    - [Uso de subprocesos para ejecutar código simultáneamente](ch16-01-threads.md)
    - [Uso de la transferencia de mensajes para transferir datos entre hilos](ch16-02-message-passing.md)
    - [Concurrencia de estado compartido](ch16-03-shared-state.md)
    - [Concurrencia extensible con los rasgos de `Sync` y `Send`](ch16-04-extensible-concurrency-sync-and-send.md)

- [Funciones de programación orientadas a objetos de Rust](ch17-00-oop.md)

    - [Características de los lenguajes orientados a objetos](ch17-01-what-is-oo.md)
    - [Uso de objetos de rasgo que permiten valores de diferentes tipos](ch17-02-trait-objects.md)
    - [Implementación de un patrón de diseño orientado a objetos](ch17-03-oo-design-patterns.md)

## Temas avanzados

- [Patrones y emparejamiento](ch18-00-patterns.md)

    - [Se pueden usar todos los patrones de lugares](ch18-01-all-the-places-for-patterns.md)
    - [Refutabilidad: si un patrón puede no coincidir](ch18-02-refutability.md)
    - [Sintaxis del patrón](ch18-03-pattern-syntax.md)

- [Características avanzadas](ch19-00-advanced-features.md)

    - [Óxido inseguro](ch19-01-unsafe-rust.md)
    - [Rasgos avanzados](ch19-03-advanced-traits.md)
    - [Tipos avanzados](ch19-04-advanced-types.md)
    - [Funciones y cierres avanzados](ch19-05-advanced-functions-and-closures.md)
    - [Macros](ch19-06-macros.md)

- [Proyecto final: Construcción de un servidor web multiproceso](ch20-00-final-project-a-web-server.md)

    - [Creación de un servidor web de un solo subproceso](ch20-01-single-threaded.md)
    - [Convirtiendo nuestro servidor de un solo subproceso en un servidor multiproceso](ch20-02-multithreaded.md)
    - [Cierre y limpieza agraciados](ch20-03-graceful-shutdown-and-cleanup.md)

- [Apéndice](appendix-00.md)

    - [A - Palabras clave](appendix-01-keywords.md)
    - [B - Operadores y símbolos](appendix-02-operators.md)
    - [C - Rasgos derivables](appendix-03-derivable-traits.md)
    - [D - Herramientas de desarrollo útiles](appendix-04-useful-development-tools.md)
    - [E - Ediciones](appendix-05-editions.md)
    - [F - Traducciones del libro](appendix-06-translation.md)
    - [G - Cómo se fabrica el óxido y "óxido nocturno"](appendix-07-nightly-rust.md)
