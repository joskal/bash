# Comandos condicionales y bucles
## test command
El comando test verifica que se está cumpliendo la condición.
```bash
test
```
Antes de pasar a los comandos condicionales conviene conocer los operadores de comparación numéricos y de cadena.
## Operadores de comparación numéricos
Para comparar números usaremos los siguientes operadores:

| Operator | Description         |
| -------- | ------------- |
| -eq       | Equal to            |
| -ne       | Not Equal to        |
| -gt       | Greather Than       |
| -ge       | Greather than or Equal To |
| -lt       | Less Than |
| -le       |Less than or Equal to |

```bash
$ vim operators-number.sh
#!/bin/bash
#Number comparison
n=${1}

if [ $n -eq 100 ]; then
  echo "-eq: n is equal to 100"
fi

if [ $n -ne 100 ]; then
  echo "-ne: n is NOT equal to 100"
fi

if [ $n -lt 100 ]; then
  echo "-lt: n is less than 100"
fi

if [ $n -gt 100 ]; then
  echo "-gt: n is greater than 100"
fi

if [ $n -le 100 ]; then
  echo "-le: n is less than or equal to 100"
fi

if [ $n -ge 100 ]; then
 echo "-le: n is greater than or equal to 100"
fi
```

```bash
$ ./operators-number.sh 100
-eq: n is equal to 100
-le: n is less than or equal to 100
-le: n is greater than or equal to 100
```

## Operadores de comparación de cadena.

| Operator | Description |
| -- | -- |
| = | Equal to |
| == | Equal to |
| != | Not Equal to |
| \\< | Less Than |
| \\> | Greather Than |
| -z | Zero Byte. Empty |
| -n | Not Empty |

```bash
$ vim operators-string.sh
#!bin/bash
pais=${1}
if [ "$pais" == "spain" ]; then
   echo "==: pais is spain"
fi

if [ "$pais" != "spain" ]; then
  echo "==: pais is not spain"
fi

if [ "$pais" \< "italia" ]; then
  echo "<: pais comes before italia"
fi

if [ "$pais" \> "italia" ]; then
  echo ">: pais comes after italia"
fi

if [ -n "$pais" ]; then
  echo "-n: pais is not null"
fi

if [ -z "$pais" ]; then
  echo "-z: pais is null"
fi
```

```bash
$ operators-string.sh spain
==: pais is spain
>: spain comes after italia
-n: pais is not null
```

Podemos comprobar el valor que devuelven los operadores de comparación haciendo lo siguiente:
```bash
$ [ 1 -eq 1 ]; echo $?
0
$ [ 1 -eq 2 ]; echo $?
1
$ test 1 -eq 1; echo $?
0
$ [ "jose" == "joss" ]; echo $?
1
$ [ "jose" == "jose" ]; echo $?
0
$ [ 3 -gt 2 ]; echo $?
0
```
Como podemos comprobar el resultado verdadero devuelve 0.
