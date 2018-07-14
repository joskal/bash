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
