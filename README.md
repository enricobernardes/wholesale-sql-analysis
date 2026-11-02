# Análise de clientes de um distribuidor atacadista com SQL

Usei SQL para responder 3 perguntas que um diretor comercial faria sobre os clientes de um distribuidor: onde está o dinheiro, quem são os clientes que mais pesam e se a empresa depende de poucos deles.

**Resposta curta:** o dinheiro está em produtos frescos e mercearia; o cliente de varejo vale mais que o de restaurante e hotel; e nenhum cliente sozinho ameaça o negócio.

## Problema
Um distribuidor precisa saber onde está o faturamento, quem são os clientes que mais pesam e quão dependente o negócio é de poucos clientes, para direcionar estoque, logística e esforço comercial.

## Dados
- [Wholesale Customers (Kaggle)](https://www.kaggle.com/datasets/smitisinghal/wholesale-customers-data), originalmente do repositório UCI
- 440 clientes de um distribuidor em Portugal, com o valor comprado no ano em 6 categorias

**Dicionário de dados**

| Coluna | Significado |
|---|---|
| `Channel` / `canal` | 1 = Horeca (Hotéis, Restaurantes e Cafés), 2 = Varejo (mercados e lojas) |
| `Region` / `regiao` | 1 = Lisboa, 2 = Porto, 3 = Outras |
| `Fresh`, `Milk`, `Grocery`, `Frozen`, `Detergents_Paper`, `Delicassen` | Valor comprado no ano em cada categoria (frescos, laticínios, mercearia, congelados, limpeza/papel, delicatessen) |

## Abordagem
1. CSV carregado num banco SQLite pelo Python (Google Colab)
2. Colunas `canal` e `regiao` criadas com nomes no lugar dos códigos; os códigos originais foram mantidos
3. Cada pergunta de negócio respondida com uma query e uma leitura curta do resultado
4. Resultados conferidos entre si (por exemplo, a soma dos portes bate com o faturamento total)

**Técnicas de SQL:** GROUP BY, agregações (COUNT, SUM, AVG), WHERE com várias condições, CASE WHEN (classificação e contagem condicional), subquery e window functions (RANK e % dentro do grupo com OVER/PARTITION BY).

## Resultados

| Pergunta | Resultado |
|---|---|
| Clientes por canal | Horeca 298, Varejo 142 |
| Faturamento por categoria | Fresh 36% e Grocery 24% (60% juntos) |
| Média de Grocery por cliente | Varejo compra 4,1x mais que o Horeca |
| Top 10 clientes | 2,3% da base, 10,6% do faturamento; o maior é 1,4% |
| Varejo em Lisboa | 14 de 18 clientes compram mais de 10 mil em Grocery |
| Porte | Médio: 52% dos clientes e 51% do faturamento; Grande: 15% e 36% |
| Fresh acima da média | 158 clientes (36%); a média é puxada por poucos clientes muito grandes |
| Ranking e % dentro do canal | Nenhum cliente passa de 3,6% do Fresh do seu canal |

## Conclusão
O canal com mais clientes não é o que mais pesa por cliente: o Varejo compra muito mais Grocery por cliente, e essa categoria merece atenção de estoque e variedade. O faturamento está espalhado em centenas de clientes, sem dependência de um só, com os clientes Médios sustentando metade do negócio. Para metas por cliente, a média não é uma boa referência, porque poucos clientes grandes a puxam para cima.

## Próximos passos
- Dashboard em Power BI com as mesmas perguntas
- Incluir margem por categoria, se disponível, para comparar faturamento com lucro

## Tecnologias
SQL (SQLite) · Python · Pandas · Google Colab

## Como rodar
1. Baixe o CSV do link acima
2. Abra `wholesale_sql_analysis.ipynb` no Google Colab e envie o CSV pelo ícone de pasta
3. Execute todas as células (Ambiente de execução → Executar tudo)

## Projeto relacionado
[Segmentação de clientes com K-Means](https://github.com/enricobernardes/wholesale-customer-segmentation), feita com o mesmo dataset

---
*Sintaxe com apoio de guias pessoais e IA; análise e conclusões são minhas.*
