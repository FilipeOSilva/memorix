## IPTables 
```
echo -e "\n\n=========\n\n" > logIptables.log && \
echo -e "iptables -L \n\n" >> logIptables.log && \
iptables -L >> logIptables.log && \
echo -e "\n\n=========\n\n" >> logIptables.log && \
echo -e "iptables -tnat -L \n\n" >> logIptables.log && \
iptables -tnat -L >> logIptables.log && \
echo -e "\n\n=========\n\n" >> logIptables.log && \
echo -e "iptables -tmangle -L \n\n" >> logIptables.log && \
iptables -tmangle -L >> logIptables.log && \
echo -e "\n\n=========\n\n" >> logIptables.log && \
echo -e "iptables -traw -L \n\n" >> logIptables.log && \
iptables -traw -L >> logIptables.log
```
## EBTables
```
echo -e "\n\n=========\n\n" > logEBtables.log && \
echo -e "ebtables -L \n\n" >> logEBtables.log && \
ebtables -L >> logEBtables.log && \
echo -e "\n\n=========\n\n" >> logEBtables.log && \
echo -e "ebtables -tnat -L \n\n" >> logEBtables.log && \
ebtables -tnat -L >> logEBtables.log && \
echo -e "\n\n=========\n\n" >> logEBtables.log && \
echo -e "ebtables -tbroute -L \n\n" >> logEBtables.log && \
ebtables -tbroute -L >> logEBtables.log
```
## Limpando os contadores IPTables e EBTables
```
iptables -Z && \
iptables -tnat -Z && \
iptables -tmangle -Z && \
iptables -traw -Z && \
ebtables -Z && \
ebtables -tnat -Z && \
ebtables -tbroute -Z
```
## Pegando os contadores do IPTables
```
echo -e "\n\n=========\n\n" > logIptablesCount.log && \
echo -e "iptables -L -v \n\n" >> logIptablesCount.log && \
iptables -L -v >> logIptablesCount.log && \
echo -e "\n\n=========\n\n" >> logIptablesCount.log && \
echo -e "iptables -tnat -L -v \n\n" >> logIptablesCount.log && \
iptables -tnat -L -v >> logIptablesCount.log && \
echo -e "\n\n=========\n\n" >> logIptablesCount.log && \
echo -e "iptables -tmangle -L -v \n\n" >> logIptablesCount.log && \
iptables -tmangle -L -v >> logIptablesCount.log && \
echo -e "\n\n=========\n\n" >> logIptablesCount.log && \
echo -e "iptables -traw -L -v \n\n" >> logIptablesCount.log && \
iptables -traw -L -v >> logIptablesCount.log && \
```
## Pegando os contadores do EPTables
```
echo -e "\n\n=========\n\n" > logEBtablesCount.log && \
echo -e "ebtables -L --Lc \n\n" >> logEBtablesCount.log && \
ebtables -L --Lc >> logEBtablesCount.log && \
echo -e "\n\n=========\n\n" >> logEBtablesCount.log && \
echo -e "ebtables -tnat -L --Lc \n\n" >> logEBtablesCount.log && \
ebtables -tnat -L --Lc >> logEBtablesCount.log && \
echo -e "\n\n=========\n\n" >> logEBtablesCount.log && \
echo -e "ebtables -tbroute -L --Lc \n\n" >> logEBtablesCount.log && \
ebtables -tbroute -L --Lc >> logEBtablesCount.log
```
## Regras para criação de IPTables
```
echo -e "\n\n=========\n\n" > logIptablesCreate.log && \
echo -e "iptables -S \n\n" >> logIptablesCreate.log && \
iptables -S >> logIptablesCreate.log && \
echo -e "\n\n=========\n\n" >> logIptablesCreate.log && \
echo -e "iptables -tnat -S \n\n" >> logIptablesCreate.log && \
iptables -tnat -S >> logIptablesCreate.log && \
echo -e "\n\n=========\n\n" >> logIptablesCreate.log && \
echo -e "iptables -tmangle -S \n\n" >> logIptablesCreate.log && \
iptables -tmangle -S >> logIptablesCreate.log && \
echo -e "\n\n=========\n\n" >> logIptablesCreate.log && \
echo -e "iptables -traw -S \n\n" >> logIptablesCreate.log && \
iptables -traw -S >> logIptablesCreate.log
```
