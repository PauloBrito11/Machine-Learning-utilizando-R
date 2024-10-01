# Machine-Learning-utilizando-R
Técnicas de Machine Learning utilizando R

## Árvores de regressão para decisão

Conjunto de dados utilizado: biblioteca padrão da linguagem R, conjunto "iris".

Criando o modelo utilizando a função rpart (biblioteca "rpart")

```r
modelo = rpart(Sepal.Length ~ Sepal.Width + Petal.Length + Petal.Width + Species, data = iris)
summary(modelo)
```

Estrutura sem texto:

![image](https://github.com/user-attachments/assets/5f4e0ced-e047-4a74-911f-ad7714cdfa56)

Estrutura "nomeada":

![image](https://github.com/user-attachments/assets/20aa964f-199e-4c7e-8554-bd2ccdefe1b4)

Realizando previsão:

```r
predicao = predict(modelo, iris)
head(predicao)
```

Comparando a previsão com os resultados reais

```
comparacao = cbind(predicao, iris$Sepal.Length, predicao - iris$Sepal.Length)
head(comparacao)
```

Verificando métricas de erros:

```r
accuracy(predicao, iris$Sepal.Length)
```

![image](https://github.com/user-attachments/assets/896a7935-1350-4126-a82d-6f8b4d7e7368)
