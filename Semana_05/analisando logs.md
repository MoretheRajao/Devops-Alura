➡️ Visualização paginada de arquivos de texto longos:

```
less /var/log/syslog
```
➡️ Acessar informações gerais (syslog):

✴️ Sair do tail [Ctrl+c]
```
tail -f /var/log/syslog
```

➡️ Acessar informações de autenticações e autorizações (auth.log):
✴️ Sair do less [q]
```
sudo less /var/log/auth.log
```

➡️ Filtrando dados com expressões regulares (Regex):
✴️ Filtrando todos os dados de "fail(ed)?|error|denied|unauthorized"
```
grep -E "fail(ed)?|error|denied|unauthorized" /var/log/syslog
```

➡️Formatando logs com awk:
✴️ inserção do | para redirecionar a saída comando grep para o awk tratar e trazer apenas as colunas que preciso.

```
grep -E "fail(ed)?|error|denied|unauthorized" /var/log/syslog | awk '{print $1, $2, $3, $4, $5, $6, $7}'
```
✴️Salvando resultado do grep em um arquivo
```
grep -E "fail(ed)?|error|denied|unauthorized" /var/log/syslog | awk '{print $1, $2, $3, $4, $5, $6, $7}' > monitoramento_logs_sistma.txt
```
