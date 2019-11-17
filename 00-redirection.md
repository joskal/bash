# Redireccionamiento
## File Descriptor.
Un File Descriptor es una zona a la que el comando envía su salida.
```bash
0:  stdin     standar input
1:  stdout    standar output
2:  stderr    standar error
```

Para redigir la salida estándar (stdout) si no se da ningún error.
```bash
cat fichero 1> resultado
```
Podemos omitir el número de stdout.
```bash
cat fichero > resultado
```
