➡️ Criando script de monitoramento de servidor:

```
vim monitoramento-sistema.sh
```
✴️ Habilitar a permissão de execução do script

```
sudo chmod +x monitoramento-sistema.sh
```
✴️ Script

```
#!/bin/bash

LOG_DIR="monitoramento_sistema"

mkdir -p $LOG_DIR

grep -E "fail(ed)?|error|denied|unauthorized" /var/log/syslog | awk '{print $1, $2, $3, $4, $5, $6, $7}' > $LOG_DIR/monitoramento_logs_sistma.txt
```
➡️ Verificando conectividade com a internet (Script)

```
if ping -c 1 8.8.8.8 > /dev/null; then
        echo "$(date): Conectividade ativa." >> $LOG_DIR/monitoramento_rede.txt
else
        echo "$(date): Sem conexão com a internet." >> $LOG_DIR/monitoramento_rede.txt
fi
```
