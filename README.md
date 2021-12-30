# R training

Notas y apuntes de R mientras voy aprendiendo. Puede que lo elimine en el futuro

## Ayuda

#### ?

Consulta información sobre una función

```R
# ?FUN
?gsub
```

#### str()

Obtener información estructurada de una variable

```R
# str(object, ...)
str(vars)
```

## Funciones para imprimir por consola

#### print()

Imprime por pantalla

```R
# print(X, ...)
print('hola')
```

#### paste()

Concatena valores (y convierte a strings)

```R
# paste (..., sep = " ", collapse = NULL, recycle0 = FALSE)
paste('hola', 'mundo')
```

## Comparación de valores

#### identical()

Compara dos valores

```R
# identical(x, y, ...)
identical(1, 2) # FALSE
identical(c("a","b"), sort(c('b', 'a'))) # TRUE
```

#### is.list()

Comprueba si un valor es una lista

```R
# is.list(x)
is.list(list(1, 2, 3)) # TRUE
is.list(c(1, 2, 3)) # FALSE
```


## Utilidades matemáticas

#### abs()

Valor absoluto

```R
# abs(x)
abs(-20) # 20
abs(c(-1, -2, 3)) # 1 2 3
```

#### round()

Redondear valores

```R
# round(x, digits = 0)
round(1.39, 1) # 1.3
round(c(1.1, 2.5, 3.9)) # 1 2 4
```

#### ceiling()

Redondear valores al entero superior

```R
# ceiling(x)
ceiling(1.4) # 2
ceiling(c(1.4, 2.0)) # 2 2
```

#### floor()

Redondear valores al entero inferior

```R
# floor(x)
floor(1.8) # 1
floor(c(1.4, 2.9)) # 1 2
```

#### sum()

Sumar valores

```R
# sum(..., na.rm = FALSE)
sum(1, 4, 5) # 10
sum(c(1, 4, 5)) # 10
```

#### mean()

Calcular media (average)

```R
# mean(x, ...)
mean(c(2, 4, 6)) # 4
```

## Funciones para estructuras de datos

#### seq()

Generar secuencia de datos

```R
# seq(from = 1, to = 1, by = ((to - from)/(length.out - 1)), ...)
seq(1, 5) # 1 2 3 4 5
seq(5, 1, -2) # 5 3 1
```

#### rep()

Replica los valores de x (vector o lista normalmente)

```R
# rep(x, times = 1, length.out = NA, each = 1)
rep(23, 3) # 23 23 23
rep(c(1, 2, 3), times=2) # 1 2 3 1 2 3
rep(c(1, 2, 3), each=2) # 1 1 2 2 3 3
```

#### sort()

Ordena los valores de x

```R
# sort(x, decreasing = FALSE, ...)
sort(c(3,1,2)) # 1 2 3
sort(c(3,1,2), decreasing=TRUE) # 3 2 1
sort(c('lorem', 'ipsum', 'dolor')) # "dolor" "ipsum" "lorem"
```

#### unlist()

Convierte una lista a un vector

```R
# unlist(x, recursive = TRUE, use.names = TRUE)
unlist(list(1, 2, 3)) # 1 2 3
unlist(list(1, 2, 'a')) # "1" "2" "a"
```

#### append()

Añade elementos a un vector

```R
# append(x, values, after = length(x))
append(c(1, 2), 3) # 1 2 3
append(c(1, 2), c(3, 4)) # 1 2 3 4
```

#### rev()

Invierte el orden del elemento

```R
# rev(x)
rev(c(1, 2, 3)) # 3 2 1
```

## Expresiones regulares

#### grep()

Devuelve las posiciones del vector/lista que hacen match

```R
# grep(pattern, x, ignore.case = FALSE, value = FALSE, ...)
grep('a', c("gato", "perro", "caballo")) # 1 3
```

#### grepl()

Devuelve un vector lógico con los matchs

```R
# grepl(pattern, x, ignore.case = FALSE, ...)
grepl('a', c("gato", "perro", "caballo")) # TRUE FALSE TRUE
```

#### sub()

Substituye strings con expresiones regulares (solo primer match de cada item)

```R
# sub(pattern, replacement, x, ignore.case = FALSE, ...)
sub('a', 'A', c("gato", "perro", "caballo")) # "gAto" "perro" "cAballo"
```

#### gsub()

Substituye strings con expresiones regulares (global)

```R
# gsub(pattern, replacement, x, ignore.case = FALSE, ...)
gsub('a', 'A', c("gato", "perro", "caballo")) # "gAto" "perro" "cAbAllo"
```

## Fecha y tiempo

#### Sys.time()

Devuelve la fecha y hora del sistema

```R
Sys.time() # "2021-12-30 15:03:32 CET"
```

#### Sys.Date()

Devuelve la fecha del sistema

```R
Sys.Date() # "2021-12-30"
```

#### as.Date()

Genera fecha con el string introducido

```R
# as.Date(x, format, ...)
as.Date('2021-11-30') # "2021-11-30"
as.Date('30-12-2021', '%d-%m-%Y') # "2021-11-30"
```

#### as.POSIXct

Genera fecha y hora con string introducido

```R
# as.POSIXct(x, tz = "", ...)
as.POSIXct('2021-12-30 12:12:60') "2021-12-30 12:13:00 CET"
```
> Módulos útiles para trabajar con fechas: `lubridate`, `zoo`, `xts`

## lapply, sapply y vapply

Funciones para aplicar sobre iterables

#### lapply()

Aplica una función a un iterable y devuelve una **lista**

```R
# lapply(X, FUN, ...)
low_pioners <- lapply(pioneers, tolower)
```

#### sapply()

Aplica una función a un iterable y devuelve una lista/vector **simplificado**

```R
# sapply(X, FUN, ..., simplify = TRUE, USE.NAMES = TRUE)
sapply(pioneers, function(x) { nchar(x) + 1 })
```

#### vapply()

Aplica una función a un iterable y devuelve un **vector** con formato definido

```R
# vapply(X, FUN, FUN.VALUE, ..., USE.NAMES = TRUE)
vapply(temp, basics, FUN.VALUE=numeric(3))
```
> `numeric(3)`: el resultado de cada iteración de `temp` es un vector numérico de longitud 3. También existe `character()` o `logical()`