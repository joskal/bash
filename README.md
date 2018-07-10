# bash
Para empezar a crear código en bash, la primera línea de nuestro código ha de empezar por esta secuencia de caracteres **#!** (conocida como **shebang**) seguido del nombre del intérprete que vamos a usar. Los intérpretes pueden ser:
```bash
#!/bin/sh — Execute the file using sh, the Bourne shell, or a compatible shell
#!/bin/csh — Execute the file using csh, the C shell, or a compatible shell
#!/usr/bin/perl -T — Execute using Perl with the option for taint checks
#!/usr/bin/php — Execute the file using the PHP command line interpreter
#!/usr/bin/python -O — Execute using Python with optimizations to code
#!/usr/bin/ruby — Execute using Ruby
```
En nuestro caso usaremos **bash**
```bash
#!/bin/bash
```
