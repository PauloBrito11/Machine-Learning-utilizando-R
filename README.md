# Machine-Learning-utilizando-R
Técnicas de Machine Learning utilizando R

## Árvores de regressão para decisão

Conjunto de dados utilizado: biblioteca padrão da linguagem R, conjunto "iris".

Criando o modelo utilizando a função rpart (biblioteca "rpart")

```r
modelo = rpart(Sepal.Length ~ Sepal.Width + Petal.Length + Petal.Width + Species, data = iris)
summary(modelo)
```

Estrutura sem texto (não consegui achar uma forma da fonte não ser cortada ):

![image](https://github.com/user-attachments/assets/5f4e0ced-e047-4a74-911f-ad7714cdfa56)

Estrutura "nomeada":

![image](https://github.com/user-attachments/assets/20aa964f-199e-4c7e-8554-bd2ccdefe1b4)

Realizando previsão ("novo conjunto de dados criado"):

```r
predicao = predict(modelo, iris)
head(predicao)
#novo conjunto contendo previsões
```

Resultado:

![image](https://github.com/user-attachments/assets/2f6f4f1b-2702-4d56-9a20-f2a38e3197de)


Comparando a previsão com os resultados reais

```
comparacao = cbind(predicao, iris$Sepal.Length, predicao - iris$Sepal.Length)
head(comparacao)
```

Resultado:

![image](https://github.com/user-attachments/assets/815f6381-fab0-4550-a201-4d036167e0b0)


Verificando métricas de erros:

```r
accuracy(predicao, iris$Sepal.Length)
```

![image](https://github.com/user-attachments/assets/896a7935-1350-4126-a82d-6f8b4d7e7368)


## Árvores de decisão para classificação

Importando conjunto de dados externos

```r
credito = read.csv("Credit.csv")
```

Criando a amostra, com proporções de 70% e 30%, gerados aleatoriamente:

```r
amostra = sample(2, 1000, replace = TRUE, prob = c(0.7, 0.3))
```

Criando o conjunto para teste e conjunto de treino, utilizando a amostra:

```r
creditotreino = credito[amostra == 1, ] #1
creditoteste = credito[amostra == 2, ]  #2

#1 - Cria uma variável que carrega todas as linhas em que o valor "credito é igual a 1", com base na amostra
criada aleatoriamente com a proporção declarada na função

#2 - Cria uma variável que carrega todas as linhas em que o valor "credito é igual a 2", com base na amostra
criada aleatoriamente com a proporção declarada na função
```

Criando método para classificação

```r
arvore = rpart(class ~ ., data = creditotreino, method = "class")
print(arvore)

# Esse método cria uma arvore de previsão da coluna class "class", utilizando a correlação de todas as outras colunas
```

Demonstrando a estrutura da árvore criada:

![image](https://github.com/user-attachments/assets/8eccc71f-81a1-42cb-bf74-4eb10646adac)

Realizando previsão:

```r
teste = predict(arvore, newdata = creditoteste)
head(teste)

# Nesse caso, o conjunto de dados possuíra as probabilidades do cliente ser um bom pagador ou não: "good" ou "bad"
```

Resultando contendo a probabilidade do cliente ser ou não um bom pagador, repare que a soma delas sempre será um, visto que é uma probabilidade:

![image](https://github.com/user-attachments/assets/4d0fbea9-9f49-41ef-b146-2d7e44801b1f)

