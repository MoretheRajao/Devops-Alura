* Ordenando os logs (Script):

``` 
   sort "${arquivo}.filtrado" -o "${arquivo}.filtrado" 
```

* Removendo duplicatas, a partir do comando Uniq, que deve ser usado após a ordenação (Script):

```
uniq "${arquivo}.filtrado" > "${arquivo}.unico"
```

* Comparando arquivos com diff:

```
 diff myapp-backend.log myapp-backend.log.unico
```

* Contandor de linhas e palavras (Script):

```
num_palavras=$(wc -w < "${arquivo}.unico")
num_linhas=$(wc -l < "${arquivo}.unico")
```
* Armazenando os contadores em 1 arquivo (Script):

```
echo "Arquivo: $nome_arquivo" >> log_stats.txt
echo "Número de linhas: $num_linhas" >> log_stats.txt
echo "Número de palavras: $num_palavras" >> log_stats.txt
echo "______________________" >> log_stats.txt
```

* Extração nome do arquivo com comando basename (Script):

```
nome_arquivo=$(basename "${arquivo}.unico")
```

* Criando diretório dentro do script:
  
```
ARQUIVO_DIR="../myapps/logs-processados"

mkdir -p $ARQUIVO_DIR
```

* Concatenando arquivos com data (script):

```
cat "${arquivo}.unico" >> "${ARQUIVO_DIR}/logs_combinados_$(date +%F).log"
```
* Refatorando Script:
OBS: o código abaixo alterou todos os "textos" log_stats para "log_stats_$(date +%F).txt" dentro do script.

```
sed -i 's/log_stats.txt/"${ARQUIVO_DIR}\/log_stats_$(date +%F).txt"/' monitoramento-logs.sh
```

* Condicionais em scripts:
OBS: o código abaixo adicionou uma "flag" frontend ou backend no inicio de cada log para identificar a origem deles.

```
if [[ "$nome_arquivo" == *frontend* ]]; then
   sed 's/^/[FRONTEND] /' "${arquivo}.unico" >> "${ARQUIVO_DIR}/logs_combinados_$(date +%F).log"

elif [[ "$nome_arquivo" == *backend* ]]; then
   sed 's/^/[BACKEND] /' "${arquivo}.unico" >> "${ARQUIVO_DIR}/logs_combinados_$(date +%F).log"

else
   cat "${arquivo}.unico" >> "${ARQUIVO_DIR}/logs_combinados_$(date +%F).log"
```

* Compactando arquivos (Script):
OBS: czf (Criar zip file) -C para melhor organização do nome (função do tar).

```
tar -czf "${ARQUIVO_DIR}/logs_$(date +%F).tar.gz" -C "$TEMP_DIR" .
```
* Verificando o conteudo compactado:

```
 tar -tzvf logs_2025-11-24.tar.gz
```

* Descompactando:

```
tar -xzvf logs_2025-11-24.tar.gz
```
