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
➡️ Verificando a conectividade de uma aplicação:

✴️ http/2 200 = foi bem sucedida a conexão
✴️ -s do curl é para suprimir o texto e deixar somente o que "filtrei"
```
if  curl -s --head https://www.alura.com.br/ | grep "HTTP/2 200" > /dev/null; then
        echo "$(date): Conexao com a Alura bem-sucedida." >> $LOG_DIR/monitoramento_rede.txt
else
        echo "$(date): Falha ao conectar com a Alura." >> $LOG_DIR/monitoramento_rede.txt
fi
```
➡️ Usando função (Script):

```
function monitorar_rede() {
        .
        .
        .
}

monitorar_rede
```
➡️ Verificando disco (Script):

✴️ "du -sh" é utilizado para verificar o uso de disco de diretórios especificos.
✴️ "function executar_monitoramento" é utilizando para melhorar a organização no uso de multiplas funções.

```
function monitorar_disco() {
        echo "$(date)" >> $LOG_DIR/monitoramento_disco.txt
        df -h | grep -v "snapfuse" | awk '$5+0 > 50 {print $1 "esta com " $5 " de uso."}' >> $LOG_DIR/monitoramento_disco.txt
        echo "Uso de disco no diretorio principal:" >> $LOG_DIR/monitoramento_disco.txt
        du -sh /root >> $LOG_DIR/monitoramento_disco.txt

}


function executar_monitoramento() {
        monitorar_disco
}

executar_monitoramento

```

➡️ Verificando hardware (Script):

```
function monitorar_hardware() {
        echo "$(date)" >> $LOG_DIR/monitoramento_hardware.txt
        free -h | grep Mem | awk '{print "Memoria RAM Total: " $2 ", Usada: " $3 ", Livre: " $4}' >> $LOG_DIR/monitoramento_hardware.txt
        top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print "Uso da CPU: " 100 - $1 "%"}' >> $LOG_DIR/monitoramento_hardware.txt
        echo "Operacoes de leitura e escrita:" >> $LOG_DIR/monitoramento_hardware.txt
        iostat | grep -E "Device|^sda|^sdb|^sdc" | awk '{print $1, $2, $3, $4}' >> $LOG_DIR/monitoramento_hardware.txt
}

function executar_monitoramento() {
       monitorar_hardware
}

executar_monitoramento
```


