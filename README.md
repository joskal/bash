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
Cuando referenciamos una variable entre comillas (**quoting**), el contenido será considerado como una palabra.
