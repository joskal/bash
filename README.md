# bash
Para empezar a crear código en bash, la primera línea de nuestro código ha de empezar por esta secuencia de caracteres **#!** (conocida como **shebang**) seguido del nombre del intérprete que vamos a usar. Los intérpretes pueden ser:
```bash
#!/bin/sh — Execute the file using sh, the Bourne shell, or a compatible shell
#!/bin/bash — Bourne Again Shell
#!/bin/csh — Execute the file using csh, the C shell, or a compatible shell
#!/usr/bin/perl -T — Execute using Perl with the option for taint checks
#!/usr/bin/php — Execute the file using the PHP command line interpreter
#!/usr/bin/python -O — Execute using Python with optimizations to code
#!/usr/bin/ruby — Execute using Ruby
```
Podemos obtener una lista de shells disponibles en nuestro sistema mirando en el archivo **/etc/shells**
```bash
$ cat /etc/shells
/bin/bash
/bin/csh
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
/usr/local/bin/bash
```
## Hola mundo
vim holamundo.sh
```bash
#!/bin/bash
echo "hola mundo"
```
Para ejecutar el script:
```bash
$ sh ./holamundo.sh
hola mundo
```
También podemos asignar permisos de ejecución al archivo.
```bash
$ chmod 755 ./holamundo.sh
$ holamundo.sh
hola mundo
```
## Variables
Las variables en bash son implícitas(no necesita declararse el tipo) y case sensitive. Para asignarle un valor basta con poner un nombre a la variable (sin espacios en el signo **=**); pero al invocarla hay que anteponerle el signo **$** al nombre.
```bash
#!/bin/bash
USERNAME='joskal'
echo $USERNAME
```
### Referenciar una variable con $ o ${}
Es lo mismo referenciar una variable con **$** que con **${}**. La diferencia es que con **${}** podemos concatenar el contenido de la variable con otra expresión.
```bash
#!/bin/bash
#con $
USERNAME='Jose'
echo $USERNAME

$ Jose
```
```bash
#!/bin/bash
#con ${}
USERNAME='Coche'
echo ${USERNAME}cito

$ Cochecito
```

### Quoting Vs Not-Quoting ("$VAR" vs $VAR)
Cuando referenciamos una variable entre comillas (**quoting**), el contenido será considerado como una sola cadena de texto. Y cuando no, interpretará como una cadena cada palabra del contenido.

```bash
#!/bin/bash
#con quoting
provincias="Alicante Cadiz Sevilla"
for i in "$provincias"
do
  echo $i
done

$ #Mostrará sólo un resultado.
$ Alicante Cadiz Sevilla
```

```bash
#!/bin/bash
#sin quoting
provincias="Alicante Cadiz Sevilla"
for i in $provincias
do
  echo $i
done

$ #Mostrará tres resultados.
$ Alicante 
$ Cadiz 
$ Sevilla
```

## Parámetros posicionales y especiales.
**Parámetros posicionales**<br>
Los argumentos que pasemos a un script son interpretados como **parámetros posicionales**. Podemos referenciarlos tanto con **$** como con **${}**.
* **$1** - parámetro 1
* **$2** - parámetro 2
* **${3}** - parámetro 3 
* **${4}** - parámetro 4
* **$5** - parámetro 5
<br>......<br>
* **$9** - parámetro 9
* **${10}** - parámetro 10
<br>......<br>

**Parámetros especiales**<br>
Si queremos saber cuantos parámetros posicionales hemos pasado al script, así como el nombre del mismo y otros detalles, recurriremos a los **parámetros especiales** (**$0, $\*, $@, $#**)
* **$0** Devuelve el nombre del script que se está ejecutando.
* **$#** Devuelve el número de argumentos (parámetros posicionales) que le hemos dado al script.
* **$@** Devuelve todos los argumentos en una sola cadena.
* **$\*** Idem al anterior, con la excepción de que si se usa entrecomillado, **"$\*"** es convertido a **"${1}x${2}x${3}x..."**, donde **x** es el primer carácter de la variable **IFS** (Internal Field Separator) que es utilizada como separador de palabras en una cadena de texto.

```bash
$ vim args.sh
IFS="-#"
echo "Nombre del script: $0"
echo "Parámetro 1: $1"
echo "Parámetro 2: $2"
echo "Parámetro 3: $3"
echo "Todos los parámetros: $@"
echo "Todos los parámetros: $*"
echo "Número de parámetros: $#"

$ ./args.sh uno dos tres cuatro
Nombre de script: ./args.sh
Parámetro 1: uno
Parámetro 2: dos
Parámetro 3: tres
Todos los parámetros: uno dos tres cuatro
Todos los parámetros: uno-dos-tres-cuatro
Número de parámetros: 4
```
