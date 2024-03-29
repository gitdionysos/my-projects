# Dashboard RH (People Analytics)

#### Os indicadores que precisamos

* Total de Colaboradores /OK
* Total de Lay-off /OK
* Taxa de Turnover /OK
* Headcount atual /A fazer
* Total em reais da Folha Salarial /A fazer
* Distribuição de gênero /OK
* Quantidade de colaboradores por faixa etária /OK
* Colaboradores por departamento e nível de cargo /A fazer
* Salário médio por departamento /A fazer

#### Precisamos dos seguintes dados

* ID /OK
* Nome /OK
* Gênero /OK
* Idade /OK
* Faixa Etária /OK
* Unidade/Local /A fazer
* Departamento /OK
* Salário /OK
* Nível /OK
* Desligamento /OK

#### Transformação da tabela

##### Coluna de Salário

Transformei a tabela na linguagem DAX, pois não tinha a coluna salário, para conseguir trabalhar com os dados. Usei a seguinte expressão no arquivo alterado dentro do Excel:

```
Salary = IF([SalarySlab]="Upto 5k",RANDBETWEEN(2000,5000),(IF([SalarySlab]="5k-10k",RANDBETWEEN(5000,10000),(IF([SalarySlab]="10k-15k",RANDBETWEEN(10000,15000),RANDBETWEEN(15000,20000))))))
```

Usei a função IF porque possuíamos apenas parte da informação da média do salário e, junto à função RANDBETWEEN, aleatorizei entre os valores.

Edit: Provável reformulaçao do cálculo para a melhor compreensao

Tentei fazer no Power BI, usando o Power Query, mas nao obtive um bom resultado, apenas quatro valores foram gerados no aleatório e distribuídos, enquanto no Excel todos os valores foram distribuídos separadamente, acredito que para poupar memória pela quantidade de linhas   o Power BI resolveu utiizar dessa abordagem

```
if [SalarySlab]="Upto 5k" then Number.RandomBetween(2000,5000) else (if [SalarySlab]="5k-10k" then Number.RandomBetween(5000,10000) else ( if [SalarySlab]="10k-15k" then Number.RandomBetween(10000,15000) else Number.RandomBetween(15000,20000)))
```

Dado as diferenças irei utilizar o modelo de linguagem DAX (primeiro), para o levantamento da coluna no Excel

##### Criação da Tabela de Calendário

Tabela de data criada diretamente no Power BI, não é uma abodagem comum, mas na falta de uma data padrão na tabela resolvi inserir a data brasileira, de 1º de janeiro até 31 de dezembro e coloquei como padrao entre as tabelas

#### Visuais

##### Total de Colaboradores

Tipo - Numero Inteiro

Usei o Count da coluna "Emp ID" para retornar o valor total ou contagem de todos os colaboradores

##### Total de Lay-off

Tipo - Número Inteiro

Usei a mesma expressão de Count para retornar o valor total da coluna "Lay-off", mas coloquei um filtro para que apenas se o valor da célula na coluna for "Yes"

##### Taxa de TurnOver

###### Criação de Medida de TurnOver

Tipo - Número Inteiro

Na criação de medida usei uma fórmula no proprio DAX do Power BI, fiz a contagem de variantes da coluna de Lay-off "Yes" e "No", coloquei outra variante onde fiz a divisão no cálculo padrão de turnover, e retornei o valor dividindo por 100, para gerar o valor em porcentagem

```
VAR Yes =
    CALCULATE(
     COUNTA('HR_Analytics'[Lay-off]),
        'HR_Analytics'[Lay-off] IN { "Yes" }
 )VAR No =
    CALCULATE(
     COUNTA('HR_Analytics'[Lay-off]),
        'HR_Analytics'[Lay-off] IN { "No" }
 )
VAR LayoffTotal =
     CALCULATE(
        DIVIDE(No - Yes, Yes)
    )
RETURN
    DIVIDE(LayoffTotal, 100)
```

Apartir dai coloquei em destaque como numero fixo inteiro

##### Distribuicao de Gênero

Tipo - Grafico Pizza

Coloquei na contagem dos gêneros e filtragem da coluna "Gender" presentes na tabela, foram apresentados apenas dois gêneros na tabela referida

##### Quantidade de Colaboradores por Faixa Etária

Tipo- Grafico Pizza

No gráfico pizza acrescentei a coluna "AgeGroup" para contagem e filtragem
