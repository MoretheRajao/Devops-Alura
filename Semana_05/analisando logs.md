* Visualização paginada de arquivos de texto longos:

```
less /var/log/syslog
```
* Acessar informações gerais (syslog):

OBS: Sair do tail [Ctrl+c]
```
tail -f /var/log/syslog
```

* Acessar informações de autenticações e autorizações (auth.log):

OBS: Sair do less [q]
```
sudo less /var/log/auth.log
```
