# Analise das vendas de uma pizzaria
Feita no Excel e SQL

### Sumário

- Análise com o objetivo de saber os sabores, tamanhos e dias que mais vendem.

### Metas 

- Aumentar o faturamento e conseguir vender em dias de baixa procura.

### Dataset

![Captura de tela 2024-05-21 214043](https://github.com/chernayavdova/venda.pizza/assets/86575159/2ee7079c-e0a8-4f8b-9e14-f5bda48b9778)

- O dataset contém as seguintes informações:
  - 11 colunas e 49.621 linhas
 
### Metodologia
  - Fiz algumas queries no SQL para obter informações relevantes e precisas, depois utilizei o Excel para a criação de KPIs e dashboard.

### SQL
  - Visão total das queries
  
  ![Captura de tela 2024-05-21 215125](https://github.com/chernayavdova/venda.pizza/assets/86575159/bad5d477-2d0e-436d-ad79-5593a2250b8d)

  ### Queries detalhadas 

  #### Valor total das vendas
  - select SUM(total_price) AS Total_Revenue FROM pizza_sales
    
![Captura de tela 2024-05-21 221111](https://github.com/chernayavdova/venda.pizza/assets/86575159/d1b87cab-9257-4c62-88ef-fbd57641d3e7)

  #### Média do valor dos pedidos 
  - select SUM(total_price) / COUNT(distinct order_id) as Avg_Order_Value from pizza_sales

![Captura de tela 2024-05-21 221120](https://github.com/chernayavdova/venda.pizza/assets/86575159/edbc2c12-bcb8-4579-bf4c-26e10ac537c3)

  #### Quantidade de total pizzas vendidas
  - select SUM(quantity) as Total_pizza_sold from pizza_sales

![Captura de tela 2024-05-21 221127](https://github.com/chernayavdova/venda.pizza/assets/86575159/a57758d3-7a8b-4396-8f8e-e001e62edc32)

  #### Quantidade de pedidos
  - select COUNT(DISTINCT order_id) as Total_Orders from pizza_sales
    
![Captura de tela 2024-05-21 221133](https://github.com/chernayavdova/venda.pizza/assets/86575159/80c33afa-c648-4840-82d9-5251b353e8be)

  #### Média de pizzas por pedido
  - select cast(CAST(sum(quantity) as decimal(10,2)) / 
    CAST(count(distinct order_id) as decimal(10,2)) as decimal(10,2)) AS  Avg_Pizza_Per_Order from pizza_sales

![Captura de tela 2024-05-21 221140](https://github.com/chernayavdova/venda.pizza/assets/86575159/ad9e973b-2006-4b1b-9a7f-dbffcac3c717)

  #### Pedidos diários
  - select DATENAME(DW, order_date) as order_day, COUNT(distinct order_id) as total_orders from pizza_sales
    group by datename(DW, order_date)

![Captura de tela 2024-05-21 222057](https://github.com/chernayavdova/venda.pizza/assets/86575159/c4450bbe-5b2d-4a00-8c07-c8aa9f78dea4)

  #### Horários dos pedidos
  - select DATEPART(hour, order_time) as order_hours, COUNT(distinct order_id) as Total_Orders from pizza_sales
    group by DATEPART(hour, order_time)
    order by datepart(hour, order_time)

![Captura de tela 2024-05-21 221156](https://github.com/chernayavdova/venda.pizza/assets/86575159/0233ef0d-d8ff-4181-97ce-c49cc50cd006)

  #### % de vendas das categorias
  - select pizza_category, cast(sum(total_price) AS DECIMAL(10,2)) as Total_Sales, 
    CAST(sum(total_price) * 100 / (select sum(total_price) from pizza_sales) AS decimal(10,2)) as PCT
    from pizza_sales
    group by pizza_category

![Captura de tela 2024-05-21 221200](https://github.com/chernayavdova/venda.pizza/assets/86575159/3d1fe783-853d-4fa6-bb90-1cb1fd6dcd44)

  #### % de vendas dos tamanhos das pizzas
  - select pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as Total_Sales,
    CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
    from pizza_sales
    group by pizza_size
    order by pizza_size

![Captura de tela 2024-05-21 221214](https://github.com/chernayavdova/venda.pizza/assets/86575159/54f1f622-ea7a-4e0e-a593-db25e6e3495c)

  #### Quantidade de pizza vendidas por categoria
  - select pizza_category, SUM(quantity) as Total_Quantity_Sold
    from pizza_sales 
    where MONTH(order_date) = 2
    group by pizza_category
    order by Total_Quantity_Sold DESC

![Captura de tela 2024-05-21 221219](https://github.com/chernayavdova/venda.pizza/assets/86575159/2d8dab7e-00e2-4c00-b629-d70fb8f9768d)

  #### As 5 pizzas mais vendidas
  - select top 5 pizza_name, SUM(quantity) as Total_Pizza_Sold
    from pizza_sales
    group by pizza_name
    order by Total_Pizza_Sold DESC

![Captura de tela 2024-05-21 221223](https://github.com/chernayavdova/venda.pizza/assets/86575159/dc5736c7-659e-402f-99a4-b809de515b4f)

  #### As 5 pizzas menos vendidas
  -select top 5 pizza_name, Sum(quantity) as Total_Pizza_Sold
  from pizza_sales
  group by pizza_name
  order by Total_Pizza_Sold ASC

![Captura de tela 2024-05-21 221228](https://github.com/chernayavdova/venda.pizza/assets/86575159/452dbff0-b134-4f95-8450-670c304bca79)

### Excel
