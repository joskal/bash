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
  <tr>
    <td> 0< <br> < </td>
    <td>
      Redirecciona <code>stdin</code> desde un archivo. El archivo es la entrada del comando.<br>
      En el ejemplo siguiente se adjunta el fichero <code>presupuesto.txt</code> al email que se va a enviar.<br>
      <code>mail -s "asunto a tratar" joskal@gmail.com < presupuesto.txt</code>
    </td>
  </tr>
  <tr>
    <td>
      <<
    </td>
    <td>
      HEREDOC o HereDoc.<br>
      Consiste en un bloque de texto que puede ser redireccionado a un comando o archivo de una manera interactiva.<br>
      Funciona indicando una palabra como delimitador que cierra el bloque de texto. El usuario va introduciendo el texto y 
      cuando introduce una línea nueva con la palabra delimitadora, termina ya la introducción de texto.<br>
      <code> $>  wc << fin </code><br>
      <code> > alfa </code><br>
      <code> > beta gamma </code><br>
      <code> > fin </code> </code><br>
      En este caso, la palabra que cierra el bloque de texto es <code>fin</code>
    </td>
  </tr>
  <tr>
    <td>
      <<<
    </td>
    <td>
      HERESTRING<br>
      A este operador no se le envía un bloque de texto con un delimitador, sino que se le redirecciona una cadena alfanumérica.<br>
      <code>$> sed 's/hola/HOLA/' <<< "hola mundo"</code><br>
        <code>HOLA mundo</code><br>
        <br>
        <code> $> bc <<< 3*3</code><br>
          <code>9</code>
    </td>
  </tr>
  <tr>
    <td> | </td>
    <td>
      Pipe<br>
      <code> | </code> Es un tipo de redireccionamiento por el cual se indica que la salida de un comando es la entrada del otro.<br>
      <code> ls ./ | grep pruebas </code>
    </td>
  </tr>
  <tr>
    <td> tee </td>
    <td>
      Comando que en conjunción con <code> | </code> redirecciona la salida a la terminal y a un archivo al mismo tiempo. <br>
      <code> ps -ef | tee procesos.txt </code><br>
      Con <code> tee -a </code> concatena al final del fichero. 
    </td>
  </tr>
  <tr>
    <td> &&<br>|| </td>
    <td>
      Ejecutar el comando2 solo si se ejecuta el comando1:
      <code>$ comando1 && comando2</code><br>
      Ejecutar el comando2 solo si no se ejecuta el comando1:
      <code>$ comando1 || comando2</code><br> <br>
      <code>ls -l pepe && echo "Este mensaje aparecerá únicamente si pepe existe"</code><br>
      <code>ls -l pepe || echo "Este mensaje aparecerá en caso de que pepe no exista"</code><br><br>
      Obviamente se pueden utilizar ambos operadores a la vez.<br>
      <code>ls -l jose && echo "El fichero existe" || echo "El fichero no existe"</code>
    </td>
  </tr>
</table>  

Podemos anular tanto la salida estándar `stdout` como `stderr` redireccionándola a `/dev/null`
```bash
ls -l welcome.txt >/dev/null 2>/dev/null && echo "El fichero existe" || echo "El fichero no existe"
```
