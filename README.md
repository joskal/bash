# Bash shelll programming
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
```bash
vim holamundo.sh
  1 #!/bin/bash
  2 echo "Hola mundo"
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
  1 #!/bin/bash
  2 USERNAME="joskal"
  3 echo $USERNAME
```
### Referenciar una variable con $ o ${}
Es lo mismo referenciar una variable con **$** que con **${}**. La diferencia es que con **${}** podemos concatenar el contenido de la variable con otra expresión.
```bash
vim var1.sh
  1 #!/bin/bash
  2 nombre="coche"
  3 echo "\$nombre: $nombre"
  4 echo "\${nombre}: ${nombre}cito"

./var1.sh
$nombre: coche
${nombre}: cochecito
```

### Quoting
En los scripts podemos emplear tanto comillas dobles como simples, aunque hay diferencias entre ellas. En las comillas dobles podemos expandir el contenido de una variable, mientras que en las simples no. Tanto en las dobles como en las simples se respetan los espacios que intercalemos entre palabras.
```bash
vim quoting.sh
  1 #!/bin/bash
  2 nombre="John Doe"
  3 var1='$nombre'
  4 var2="$nombre"
  5
  6 echo '$nombre=$nombre'
  7 echo "\$nombre=$nombre"
  8
  9 echo "var1=" $var1
 10 echo "var2=" $var2
 11
 12 echo "This will not expand \$dollar"
 13 echo 'This will not expand $dollar'

$./quoting.sh
$nombre=$nombre
$nombre=John Doe
var1= $nombre
var2= John Doe
This will not expand $dollar
This will not expand $dollar
```
**Quoting Vs Not-Quoting ("$VAR" vs $VAR)**<br>
Cuando referenciamos una variable entre comillas dobles, el contenido será considerado como una sola cadena de texto. Y cuando no, interpretará como una cadena cada palabra del contenido.

```bash
vim quoting.sh
  1 #!/bin/bash
  2 provincias="Alicante Cadiz Sevilla"
  3 echo 'con "quoting"'
  4 for i in "$provincias"
  5 do
  6   echo $i
  7 done
  8 echo "---------------------------"
  9 echo "sin quoting"
 10 for i in $provincias
 11 do
 12   echo $i
 13 done
 
$ ./quoting.sh
con "quoting"
Alicante Cadiz Sevilla
---------------------------
sin quoting
Alicante
Cadiz
Sevilla
```
### Declare (declaración de variables)
Normalmente no necesitamos declarar el tipo de una variable. No obstante bash nos permite declarar variables de tipo entero, de sólo lectura, arrays, arrays asociativos y de tipo export. Las variables sin declarar pueden tomar cambiar el tipo sin devolver error a lo largo de la ejecución.
* **declare -i total**      #tipo entero
* **declare -r casa=roja**  #tipo solo lectura
* **declare -x global=mundo** #tipo global. Estará activo incluso cuando termine el script.
* **declare -a** #tipo array.
* **declare -A** #tipo array asociativo.

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
  1 IFS="-#"
  2 echo "Nombre del script: $0"
  3 echo "Parámetro 1: $1"
  4 echo "Parámetro 2: $2"
  5 echo "Parámetro 3: $3"
  6 echo "Todos los parámetros: $@"
  7 echo "Todos los parámetros: $*"
  8 echo "Número de parámetros: $#"

$ ./args.sh uno dos tres cuatro
Nombre de script: ./args.sh
Parámetro 1: uno
Parámetro 2: dos
Parámetro 3: tres
Todos los parámetros: uno dos tres cuatro
Todos los parámetros: uno-dos-tres-cuatro
Número de parámetros: 4
```

**Rango de parámetros**<br>
Además de referenciar cada argumento por su posición (**$1, $2, $3...**), también podemos referenciar un rango de parámetros posicionales de esta forma: **${@:$start:$count}**.

```bash
vim ./rango.sh
  1 #!/bin/bash
  2 echo "Rango de parámetros"
  3 echo "-------------------"
  4 echo "\$@        = $@"
  5 echo "\${@:2}    = ${@:2}"
  6 echo "\${@:2:3}  = ${@:2:3}"
  7 echo "\${@:-4}   = ${@:-4}"
  8 echo "\${@:-4:3} = ${@:-4:3}"
 
$ ./rango.sh 1 2 3 4 5 6
Rango de parámetros
-------------------
$@        = 1 2 3 4 5 6 7 8 9
${@:2}    = 2 3 4 5 6 7 8 9
${@:2:3}  = 2 3 4
${@:-4}   = 1 2 3 4 5 6 7 8 9
${@:-4:3} = 1 2 3 4 5 6 7 8 9
```

**shift**<br>
Este comando mueve **n** veces hacia la izquierda todos los parámetros posicionales. Si omitimos **n** lo moverá uno.
```bash
$ vim ./shift.sh
  1 #!/bin/bash
  2 # Mover hacia la izquierda los argumentos dos posiciones
  3 echo "Número de parámetros (antes de shift): $#"
  4 echo "Parámetros: $@"
  5 shift 2
  6 echo "Número de parámetros (después de shift): $#"
  7 echo "Parámetros: $@"
  8 echo "Parámetro 1: $1"
  9 echo "Parámetro 2: $2"
 10 echo "Parámetro 3: $3"
 
$ sh ./shift.sh 1 2 3 4 5 6 7 8 9
Número de parámetros (antes de shift): 9
Parámetros: 1 2 3 4 5 6 7 8 9
Número de parámetros (después de shift): 7
Parámetros: 3 4 5 6 7 8 9
Parámetro 1: 3
Parámetro 2: 4
Parámetro 3: 5
```

## Expresiones aritméticas
Podemos almacenar numeros en variables, pero a la hora de operar con ellos debemos recurrir a los comandos **let** y **expr**. También podemos calcular una expresión encerrándola entre paréntesis dobles **((expr))**
