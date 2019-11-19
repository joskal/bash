# Redireccionamiento
## File Descriptor.
Un File Descriptor es una zona donde el comando envía una salida (`stdout`,  `stderr`) o recibe una entrada (`stdin`).

`0:stdin`     standard input<br>
`1:stdout`    standard output<br>
`2:stderr`    standard error<br>

La salida estándar `stdout` se produce cuando un comando se ejecuta sin errores. En caso contrario, se produce la salida `stderr`. 
Las salidas se pueden redireccionar hacia o desde un archivo mediante los operadores de redirección.
<table>
  <thead>
    <tr>
      <th>Operador</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tr>
    <td> 1> <br> > <br> 1>> <br> >> </td>
    <td>Redirecciona <code>stdout</code> a un archivo. Si existe, lo sobreescribe; si no, lo crea.<br>
      Podemos omitir el número de stdout, ya que por defecto es 1.<br>
    <code>ls -l > listado.txt </code> <br>
      Para concatenar la salida con el contenido del fichero, es decir, añadiendo la salida al final del archivo sin perder el anterior contenido, usaremos <code> >> </code>.<br>
      <code>date >> fechas.txt </code><br>
      <code>ps -ef >> procesos.txt  </code>
    </td>
  </tr>
  <tr>
    <td> 2> <br> 2>> </td>
    <td>Redirecciona <code>stderr</code> (salida de errores) a un archivo.<br>
      En este ejemplo, si se produce algún mensaje de error lo envía a <code>error.txt</code><br>
    <code>cp file1 file2 2> error.txt </code> <br>
      Si queremos concatenar la salida <code>stderr</code> al archivo:<br>
      <code>cp file1 file2 2>> error.txt </code>
    </td>
  </tr>
</table>  


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
