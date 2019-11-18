# Redireccionamiento
## File Descriptor.
Un File Descriptor es una zona a la que el comando envía una salida (`stdout`,  `stderr`) o recibe una entrada (`stdin`).

`0:stdin`     standar input<br>
`1:stdout`    standar output<br>
`2:stderr`    standar error<br>


Para redigir la salida estándar `stdout` a un fichero, si no se da ningún error:
```bash
cat listado 1> fichero.txt
```
Podemos omitir el número de stdout, ya que por defecto es 1.
```bash
cat listado > fichero
```
Si el fichero `listado` no existe, devolverá el error estándar `stderr`, el cual se puede redireccionar con `2>`
```bash
cat listado 2> error.txt
```
Agregar la fecha al final de fichero.txt
```bash
date >> fecha.txt
```
Se puede silenciar la salida de cualquier comando direccionándola a /dev/null

```bash
cat fichero.txt > /dev/null
```
Si el fichero.txt no existe devolverá un error, el cual también se puede silenciar.
```bash
cat fichero.txt 2> /dev/null
```
Los redireccionamientos `stdout` y `stderr` se pueden usar en el mismo comando. 
```bash
cat fichero.txt > main.txt 2> errors.txt
```
