# MySQL_Tool
Ferramenta para extração de dados do database MySQL

## Método 1
### **REQUER:**
- Instalação do MySQL (8.0) (é recomendado realizar a instalação padrão);
- Instalação do Python (3.9.19)

Este método é preferível para aqueles que já tem familiaridade com um IDE como o VSCode.
Depois das instalações, é recomendado utilizar o ambiente virtual (mysql_venv) já incluído nos arquivos, para utilizar a versão correta das bibliotecas.

![alt](https://github.com/Yurnerosk/MySQL_Tool/blob/main/images/image_1.png)

O arquivo é um Jupyter Notebook, [baixar_por_data.ipynb](https://github.com/Yurnerosk/MySQL_Tool/blob/main/baixar_por_data.ipynb).

A função que é responsável pela coleta e download de dados possui os parâmetros:

- nome_tabela: Nome da tabela de dados. (Não do database!) **(obrigatório)**
- mes: Mês que deseja filtrar. **(obrigatório)**
- ano: Ano que deseja filtrar. **(obrigatório)**
- colunas: Lista de colunas que deseja coletar. Caso queira todas elas, não use este parâmetro.
- limite: Número de linhas por arquivo csv. Default: 10000 linhas.
- caminho_csv: Caso queira um caminho específico para o arquivo gerado, use este parâmetro. Caso contrário, não use o parâmetro, e o arquivo será gerado na mesma pasta em que o código se situa.

Observação: No código já existe um loop para que os arquivos sejam gerados até que o período especificado seja completamente coberto, e também itera sobre outros meses caso seja necessário.


## Método 2
### **REQUER:**
- Instalação do MySQL (8.0) (é recomendado realizar a instalação padrão);

Este método não requer Python, mas pode ser um pouco mais lento por causa do programa.

Vá em _Database_ e _Connect to Database_.

![alt](https://github.com/Yurnerosk/MySQL_Tool/blob/main/images/image_2.png)

Clique em _File_, _New Query Tab_, e insira o código em SQL que deseja utilizar. A seguir, um template:

```
USE MY_DATABASE;
SELECT DATETIME_, COLUMN_A, COLUMN_B FROM TABLE_DATA
            WHERE MONTH(DATETIME_COLUMN) = 6 AND YEAR(DATETIME_COLUMN)
            = 2024 ORDER BY `TIMESTAMP_COLUMN`
            LIMIT 100;
```

Isso irá criar uma tabela de 100 linhas com os campos Datetime_, Column_A e Column_B, do mês 06, do ano 2024, ordenada em ordem crescente pela coluna Timestamp_Column. 

Por fim, para exportar o arquivo csv gerado, clique no ícone mais próximo da tabela, e ele será exportado para onde quiser.


Caso seja necessário separar o arquivo em mais partições, é possível fazer um offset e fazer com que a tabela pule as linhas anteriores e pegue o que esteja faltando. No exemplo a seguir, serão puladas as 100 primeiras linhas que já foram exportadas, e o código irá pegar as próximas 100.

```
USE MY_DATABASE;
SELECT DATETIME_, COLUMN_A, COLUMN_B FROM TABLE_DATA
            WHERE MONTH(DATETIME_COLUMN) = 6 AND YEAR(DATETIME_COLUMN)
            = 2024 ORDER BY `TIMESTAMP_COLUMN`
            LIMIT 100 OFFSET 100;
```


