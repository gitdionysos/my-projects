# Dashboard RH (People Analytics)

#### Os indicadores que precisamos

* Total de admissões
* Total de demissões
* Taxa de Turnover
* Headcount atual
* Total em reais da Folha Salarial
* Distribuição de gênero
* Quantidade de colaboradores por faixa etária
* Colaboradores por departamento e nível de cargo
* Admissões por período
* Salário médio por departamento

#### Precisamos dos seguintes dados

* ID
* Nome
* Data de admissão
* Gênero
* Idade
* Faixa Etária
* Etnia
* Unidade
* Departamento
* Salário
* Nível
* Desligamento
* Data de Desligamento

#### Transformação da tabela

##### Tabela de Salário

Transformei a tabela de exemplo com o Power Pivot, que não tinha salário, para conseguir trabalhar com os dados. Usei a seguinte expressão no arquivo alterado dentro do Excel:

```
IF([SalarySlab]="Upto 5k";RANDBETWEEN(2000;5000);(IF([SalarySlab]="5k-10k";RANDBETWEEN(5000,10000);(IF([SalarySlab]="10k-15k";RANDBETWEEN(10000;15000);RANDBETWEEN(15000;20000)
```

Usei a função IF porque possuíamos apenas parte da informação da média do salário e, junto à função RANDBETWEEN, aleatorizei entre os valores.

(OBS: Vou estudar para verificar o sistema de pesos dentro dessa função e tornar mais complexo o sistema de salário, por exemplo, aumentar alguns dependendo da escolaridade ou idade.)

Edit: Provável reformulaçao do cálculo para a melhor compreensao

##### Tabela de Data de demissão

- Analisar média ponderada
  - Porcentagem de corte de funcionário, de modo que nao altere o porte da organizaçao
  - Obs: verificar possóveis pesos de corte de cada setor e possíveis influencias
- Verificar variáveis
  - Analise de cada fator (coluna) da tabela que influencia a demissao de cada funcionário
  - pesquisa de baixa no setor
- formular algorítimo para cálculo
  - Estabelecer um algorítimo completo para a criaçao da nova coluna
