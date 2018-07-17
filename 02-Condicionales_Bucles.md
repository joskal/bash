# Comandos condicionales y bucles
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
  1 #!/bin/bash
  2 #Number comparison
  3 n=${1}
  4
  5 if [ $n -eq 100 ]; then
  6  echo "-eq: n is equal to 100"
  7 fi
  8
  9 if [ $n -ne 100 ]; then
 10  echo "-ne: n is NOT equal to 100"
 11 fi
 12
 13 if [ $n -lt 100 ]; then
 14      echo "-lt: n is less than 100"
 15 fi
 16
 17 if [ $n -gt 100 ]; then
 18  echo "-gt: n is greater than 100"
 19 fi
 20
 21 if [ $n -le 100 ]; then
 22  echo "-le: n is less than or equal to 100"
 23 fi
 24
 25 if [ $n -ge 100 ]; then
 26  echo "-le: n is greater than or equal to 100"
 27 fi

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
| < | Less Than |
| > | Greather Than |
| -z | Zero Byte. Empty |
| -n | Not Empty |
