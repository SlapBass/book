## Apéndice B: Operadores y símbolos

Este apéndice contiene un glosario de la sintaxis de Rust, incluidos los operadores y otros símbolos que aparecen por sí mismos o en el contexto de rutas, genéricos, límites de rasgos, macros, atributos, comentarios, tuplas y corchetes.

### Operadores

La Tabla B-1 contiene los operadores en Rust, un ejemplo de cómo aparecería el operador en contexto, una breve explicación y si ese operador se puede sobrecargar. Si un operador se puede sobrecargar, se enumera el rasgo relevante que se utilizará para sobrecargar ese operador.

<span class="caption">Tabla B-1: Operadores</span>

Operador | Ejemplo | Explicación | ¿Sobrecargar?
--- | --- | --- | ---
`!` | `ident!(...)` , `ident!{...}` , `ident![...]` | Expansión macro |
`!` | `!expr` | Complemento lógico o bit a bit | `Not`
`!=` | `var != expr` | Comparación de no calidad | `PartialEq`
`%` | `expr % expr` | Resto aritmético | `Rem`
`%=` | `var %= expr` | Resto aritmético y asignación | `RemAssign`
`&` | `&expr` , `&mut expr` | Pedir prestado |
`&` | `&type` , `&mut type` , `&'a type` , `&'a mut type` | Tipo de puntero prestado |
`&` | `expr & expr` | Y bit a bit | `BitAnd`
`&=` | `var &= expr` | AND bit a bit y asignación | `BitAndAssign`
`&&` | `expr && expr` | Y lógico |
`*` | `expr * expr` | Multiplicación aritmética | `Mul`
`*=` | `var *= expr` | Multiplicación y asignación aritmética | `MulAssign`
`*` | `*expr` | Desreferencia |
`*` | `*const type` , `*mut type` | Puntero sin procesar |
`+` | `trait + trait` , `'a + trait` | Restricción de tipo compuesto |
`+` | `expr + expr` | Suma aritmética | `Add`
`+=` | `var += expr` | Sumas y asignaciones aritméticas | `AddAssign`
`,` | `expr, expr` | Separador de argumentos y elementos |
`-` | `- expr` | Negación aritmética | `Neg`
`-` | `expr - expr` | Resta aritmética | `Sub`
`-=` | `var -= expr` | Resta y asignación aritmética | `SubAssign`
`->` | `fn(...) -> type` , <code>|...| -&gt; type</code> | Función y tipo de retorno de cierre |
`.` | `expr.ident` | Acceso miembros |
`..` | `..` , `expr..` , `..expr` , `expr..expr` | Literal de rango exclusivo derecho |
`..=` | `..=expr` , `expr..=expr` | Literal de rango con inclusión derecha |
`..` | `..expr` | Sintaxis de actualización literal de estructura |
`..` | `variant(x, ..)` , `struct_type { x, .. }` | Encuadernación con patrón "Y el resto" |
`...` | `expr...expr` | En un patrón: patrón de rango inclusivo |
`/` | `expr / expr` | División aritmética | `Div`
`/=` | `var /= expr` | División y asignación aritmética | `DivAssign`
`:` | `pat: type` , `ident: type` | Restricciones |
`:` | `ident: expr` | Inicializador de campo de estructura |
`:` | `'a: loop {...}` | Etiqueta de lazo |
`;` | `expr;` | Terminador de estado de cuenta y artículo |
`;` | `[...; len]` | Parte de la sintaxis de matriz de tamaño fijo |
`<<` | `expr << expr` | Shift izquierdo | `Shl`
`<<=` | `var <<= expr` | Desplazamiento a la izquierda y asignación | `ShlAssign`
`<` | `expr < expr` | Menos que comparación | `PartialOrd`
`<=` | `expr <= expr` | Menor o igual a la comparación | `PartialOrd`
`=` | `var = expr` , `ident = type` | Cesión / equivalencia |
`==` | `expr == expr` | Comparación de igualdad | `PartialEq`
`=>` | `pat => expr` | Parte de la sintaxis de Match Arm |
`>` | `expr > expr` | Mayor que la comparación | `PartialOrd`
`>=` | `expr >= expr` | Mayor o igual que la comparación | `PartialOrd`
`>>` | `expr >> expr` | Giro a la derecha | `Shr`
`>>=` | `var >>= expr` | Desplazamiento a la derecha y asignación | `ShrAssign`
`@` | `ident @ pat` | Encuadernación de patrón |
`^` | `expr ^ expr` | OR exclusivo bit a bit | `BitXor`
`^=` | `var ^= expr` | OR exclusivo bit a bit y asignación | `BitXorAssign`
<code>|</code> | <code>pat | pat</code> | Alternativas de patrón |
<code>|</code> | <code>expr | expr</code> | O bit a bit | `BitOr`
<code>|=</code> | <code>var |= expr</code> | O bit a bit y asignación | `BitOrAssign`
<code>||</code> | <code>expr || expr</code> | OR lógico |
`?` | `expr?` | Propagación de errores |

### Símbolos de no operador

La siguiente lista contiene todas las no letras que no funcionan como operadores; es decir, no se comportan como una función o llamada a un método.

La Tabla B-2 muestra los símbolos que aparecen por sí mismos y son válidos en una variedad de ubicaciones.

<span class="caption">Tabla B-2: Sintaxis autónoma</span>

Símbolo | Explicación
--- | ---
`'ident` | Etiqueta de ciclo o vida útil con nombre
`...u8` , `...i32` , `...f64` , `...usize` , etc. | Literal numérico de tipo específico
`"..."` | Literal de cadena
`r"..."` , `r#"..."#` , `r##"..."##` , etc. | Literal de cadena sin formato, caracteres de escape no procesados
`b"..."` | Literal de cadena de bytes; construye un `[u8]` lugar de una cadena
`br"..."` , `br#"..."#` , `br##"..."##` , etc. | Literal de cadena de bytes sin formato, combinación de literal de cadena de bytes y sin formato
`'...'` | Carácter literal
`b'...'` | Literal de bytes ASCII
<code>|...| expr</code> | Cierre
`!` | Tipo de fondo siempre vacío para funciones divergentes
`_` | Enlace de patrón "ignorado"; también se usa para hacer legibles los literales enteros

La Tabla B-3 muestra los símbolos que aparecen en el contexto de una ruta a través de la jerarquía del módulo hasta un elemento.

<span class="caption">Tabla B-3: Sintaxis relacionada con la ruta</span>

Símbolo | Explicación
--- | ---
`ident::ident` | Ruta del espacio de nombres
`::path` | Ruta relativa a la raíz de la caja (es decir, una ruta explícitamente absoluta)
`self::path` | Ruta relativa al módulo actual (es decir, una ruta explícitamente relativa).
`super::path` | Ruta relativa al padre del módulo actual
`type::ident` , `<type as trait>::ident` | Constantes, funciones y tipos asociados
`<type>::...` | Elemento asociado para un tipo que no se puede nombrar directamente (por ejemplo, `<&T>::...` , `<[T]>::...` , etc.)
`trait::method(...)` | Eliminación de ambigüedades de una llamada de método nombrando el rasgo que la define
`type::method(...)` | Eliminación de ambigüedades de una llamada a un método nombrando el tipo para el que está definido
`<type as trait>::method(...)` | Eliminación de ambigüedades de una llamada a un método nombrando el rasgo y el tipo

La Tabla B-4 muestra los símbolos que aparecen en el contexto del uso de parámetros de tipo genérico.

<span class="caption">Tabla B-4: Genéricos</span>

Símbolo | Explicación
--- | ---
`path<...>` | Especifica parámetros para el tipo genérico en un tipo (por ejemplo, `Vec<u8>` )
`path::<...>` , `method::<...>` | Especifica parámetros para el tipo, función o método genérico en una expresión; a menudo denominado pez turbio (p. ej., `"42".parse::<i32>()` )
`fn ident<...> ...` | Definir función genérica
`struct ident<...> ...` | Definir estructura genérica
`enum ident<...> ...` | Definir enumeración genérica
`impl<...> ...` | Definir implementación genérica
`for<...> type` | Límites de por vida de mayor rango
`type<ident=type>` | Un tipo genérico donde uno o más tipos asociados tienen asignaciones específicas (p. Ej., `Iterator<Item=T>` )

La Tabla B-5 muestra los símbolos que aparecen en el contexto de la restricción de parámetros de tipo genérico con límites de rasgos.

<span class="caption">Tabla B-5: Restricciones vinculadas a rasgos</span>

Símbolo | Explicación
--- | ---
`T: U` | Parámetro genérico `T` restringido a tipos que implementan `U`
`T: 'a` | El tipo genérico `T` debe sobrevivir a la vida útil `'a` (lo que significa que el tipo no puede contener transitivamente ninguna referencia con vidas más cortas que `'a` )
`T : 'static` | El tipo genérico `T` no contiene referencias prestadas distintas de las `'static`
`'b: 'a` | La vida útil genérica `'b` debe sobrevivir a la vida útil `'a`
`T: ?Sized` | Permitir que el parámetro de tipo genérico sea un tipo de tamaño dinámico
`'a + trait` , `trait + trait` | Restricción de tipo compuesto

La Tabla B-6 muestra los símbolos que aparecen en el contexto de llamar o definir macros y especificar atributos en un elemento.

<span class="caption">Tabla B-6: Macros y atributos</span>

Símbolo | Explicación
--- | ---
`#[meta]` | Atributo externo
`#![meta]` | Atributo interno
`$ident` | Sustitución de macros
`$ident:kind` | Captura de macros
`$(…)…` | Repetición macro

La Tabla B-7 muestra los símbolos que generan comentarios.

<span class="caption">Tabla B-7: Comentarios</span>

Símbolo | Explicación
--- | ---
`//` | Comentario de línea
`//!` | Comentario de documento de línea interna
`///` | Comentario de documento de línea exterior
`/*...*/` | Bloquear comentario
`/*!...*/` | Comentario de documento de bloque interno
`/**...*/` | Comentario de documento de bloque externo

La Tabla B-8 muestra los símbolos que aparecen en el contexto del uso de tuplas.

<span class="caption">Tabla B-8: Tuplas</span>

Símbolo | Explicación
--- | ---
`()` | Tupla vacía (también conocida como unidad), tanto literal como de tipo
`(expr)` | Expresión entre paréntesis
`(expr,)` | Expresión de tupla de un solo elemento
`(type,)` | Tipo de tupla de un solo elemento
`(expr, ...)` | Expresión de tupla
`(type, ...)` | Tipo de tupla
`expr(expr, ...)` | Expresión de llamada a función; también se usa para inicializar `struct` tupla y variantes de `enum` tuplas
`ident!(...)` , `ident!{...}` , `ident![...]` | Invocación de macros
`expr.0` , `expr.1` , etc. | Indexación de tuplas

La Tabla B-9 muestra los contextos en los que se utilizan llaves.

<span class="caption">Tabla B-9: Corchetes rizados</span>

Contexto | Explicación
--- | ---
`{...}` | Expresión de bloque
`Type {...}` | `struct` literal

La Tabla B-10 muestra los contextos en los que se utilizan corchetes.

<span class="caption">Tabla B-10: Corchetes</span>

Contexto | Explicación
--- | ---
`[...]` | Array literal
`[expr; len]` | Array literal que contiene copias `len` de `expr`
`[type; len]` | Tipo de matriz que contiene instancias de `type` `len`
`expr[expr]` | Indexación de colecciones. Overloadable ( `Index` , `IndexMut` )
`expr[..]` , `expr[a..]` , `expr[..b]` , `expr[a..b]` | Collection indexing pretending to be collection slicing, using `Range`, `RangeFrom`, `RangeTo`, or `RangeFull` as the “index”
