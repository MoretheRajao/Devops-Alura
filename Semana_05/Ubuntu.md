* Ordenando os logs:

``` 
   sort "${arquivo}.filtrado" -o "${arquivo}.filtrado" 
```

*Removendo duplicatas, a partir do comando Uniq, que deve ser usado após a ordenação:

```
uniq "${arquivo}.filtrado" > "${arquivo}.unico"
```

*Comparando arquivos com diff:

```
 diff myapp-backend.log myapp-backend.log.unico
```

*Contandor de linhas e palavras:

```
num_palavras=$(wc -w < "${arquivo}.unico")
num_linhas=$(wc -l < "${arquivo}.unico")
```
