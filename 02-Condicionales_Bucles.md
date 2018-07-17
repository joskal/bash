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
| \\< | Less Than |
| \\> | Greather Than |
| -z | Zero Byte. Empty |
| -n | Not Empty |

```bash
$ vim operators-string.sh
  1 #!bin/bash
  2 pais=${1}
  3 if [ "$pais" == "spain" ]; then
  4   echo "==: pais is spain"
  5 fi
  6
  7 if [ "$pais" != "spain" ]; then
  8   echo "==: pais is not spain"
  9 fi
 10
 11 if [ "$pais" \< "italia" ]; then
 12  echo "<: pais comes before italia"
 13 fi
 14
 15 if [ "$pais" \> "italia" ]; then
 16  echo ">: pais comes after italia"
 17 fi
 18
 19 if [ -n "$pais" ]; then
 20  echo "-n: pais is not null"
 21 fi
 22
 23 if [ -z "$pais" ]; then
 24  echo "-z: pais is null"
 25 fi
 
$ operators-string.sh spain
==: pais is spain
>: spain comes after italia
-n: pais is not null
```
