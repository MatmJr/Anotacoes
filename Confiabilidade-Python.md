# Confiabilidade

Confiabilidade é a probabilidade de que um item execute uma função exigida por um determinado período de tempo, sob certas condições operacionais. Em outras palavras, é a probabilidade de não falha ao longo do tempo. A confiabilidade representa um componente significativo da qualidade de um produto no domínio do tempo. Os clientes esperam que os produtos durem um determinado período de tempo antes de serem reabastecidos após a falha. Se o tempo funcional de um produto não atender aos requisitos do cliente, alterações devem ser feitas em suas especificações de design durante a fabricação.
$$
R(t)=Pr(T \geq t)
$$
A confiabilidade se concentra no tempo em que um produto continua funcional depois de se tornar operacional (ou seja, o ciclo de vida do produto). A confiabilidade pode ser vista como a qualidade no domínio do tempo. Sua fórmula é representada como:
$$
R(t) = Pr(T \geq t) = 1 - F(t) = \int_{t}^{\infty}f(t)dt
$$
onde f(t) é a função densidade de probabilidade de uma variável aleatória dada.

Existem várias etapas necessárias para calcular a confiabilidade de um sistema em um período específico:

- Obtenha tempos de falha - Defina um tamanho de amostra e obtenha o tempo até a falha da componente estudada.
- Identifique a distribuição que melhor se ajusta aos dados - Crie um histograma para os dados coletados, ajuste múltiplas distribuições de probabilidade e identifique aquela que melhor descreve os dados. 
- Obtenha os parâmetros de distribuição - Obtenha a localização, escala e parâmetros adicionais para a distribuição selecionada para determinar sua função de densidade de probabilidade.
- Obtenha probabilidades - Obtenha a probabilidade de falha antes de um tempo t usando a função de densidade cumulativa e a confiabilidade após um tempo t usando a função de sobrevivência.

## Exemplos em Python: 

<b>1 - Scipy</b>:

fonte: https://towardsdatascience.com/reliability-analysis-with-python-862c95e5c65a

```python
import matplotlib.pyplot as plt
%matplotlib inline
import scipy
import scipy.stats
import warnings
warnings.filterwarnings("ignore")

# Criando um dataset
size = 1000
x = scipy.arange(size)
y = scipy.stats.beta.rvs(6, 2, size=size, random_state=40)*50 

# Especificações do Histograma
plt.figure(figsize=(20,10))
h = plt.hist(y, bins=range(51))


# Lista das Distribuições
dist_names = ['alpha', 'beta', 'expon', 'gamma', 'norm', 'rayleigh']

# Fit the distributions to the data and plot their probability density functions
for dist_name in dist_names:
dist = getattr(scipy.stats, dist_name)
param = dist.fit(y)
pdf_fitted = dist.pdf(x, *param[:-2], loc=param[-2], scale=param[-1])*size
plt.plot(pdf_fitted, label=dist_name)
plt.xlim(0,50)
plt.legend(loc='upper left')
plt.title("Failure Times Distribution")
plt.xlabel("Failure Time")
plt.ylabel("Frequency")
plt.show()
```

No exemplo acima temos seis distribuições diferentes ajustadas aos dados: distribuições alfa, beta, exponencial, gama, normal e Rayleigh. 

Para obter os parâmetros da melhor distribuição:

```python
# Determinar a distribuição com o melhor Fit
dist = getattr(scipy.stats, 'beta')

# Fit a distribuição ao dados
param = dist.fit(y)

# Parâmetros da Distribuição (e.g. 'a', 'b' for beta distribution)
args = param[:-2]

# Localização dos parâmetros
loc = param[-2]

# Parâmetros de Escala
scale = param[-1]
```

Para obter as probabilidades: 

```python
# Probability of failure before time t
print("Probability of failure before time 40:", round(scipy.stats.beta.cdf(40, *args, loc=loc, scale=scale)*100,2),"%")
# Probability of failure before time 40: 57.32 %

# Reliability estimation after time t
print("Reliability Estimation at time 40:", round(scipy.stats.beta.sf(40, *args, loc=loc, scale=scale)*100,2),"%")
# Reliability Estimation at time 40: 42.68 %
```

De acordo com os resultados, é mais provável que o produto não dure pelo menos 40 semanas como esperado, uma vez que sua probabilidade de falha antes da semana 40 é de 57,32% (ou seja, sua probabilidade de continuar funcional após a semana 40 é de 42,68%).

<b> 2 - distfit </b>

fonte: https://erdogant.github.io/distfit/pages/html/Performance.html

Para medir a qualidade do ajuste das funções de densidade, a lib distfit usa a métrica RSS (Residual Sum of Squares). 

O RSS (https://www.investopedia.com/terms/r/residual-sum-of-squares.asp) é uma técnica estatística usada para medir a quantidade de variância em um conjunto de dados que não é explicada pelo próprio modelo de regressão. Em vez disso, estima a variação nos resíduos, ou termo de erro. 

<b> IMPORTANTE: </b>

- O RSS mede o nível de variância no termo de erro, ou resíduos, de um modelo de regressão.
- Quanto menor a soma residual dos quadrados, melhor seu modelo se ajusta aos dados; quanto maior for a soma residual dos quadrados, pior será o ajuste do modelo aos dados.
- Um valor zero significa que seu modelo é um ajuste perfeito.

- Em termos gerais, a soma dos quadrados é uma técnica estatística usada na análise de regressão para determinar a dispersão dos pontos de dados. Em uma análise de regressão, o objetivo é determinar o quão bem uma série de dados pode ser ajustada a uma função que pode ajudar a explicar como a série de dados foi gerada. A soma dos quadrados é usada como uma forma matemática de encontrar a função que melhor se ajusta (varia menos) a partir dos dados. 

- O RSS mede a quantidade de erro restante entre a função de regressão e o conjunto de dados após a execução do modelo. Uma figura RSS menor representa uma função de regressão. 

- O RSS, também conhecido como a soma dos resíduos quadrados, essencialmente determina o quão bem um modelo de regressão explica ou representa os dados no modelo. 

As pontuações de qualidade do ajuste são armazenadas em dist.summary. Neste exemplo, não especificaremos nenhuma distribuição, mas apenas forneceremos os dados empíricos ao modelo.

```python
X = data_frame

dist = distfit()
dist.fit_transform(X)
print(dist.summary)
```

A biblioteca vai fazer um ranqueamento de acordo com a pontuação do escore RSS, várias distrbuições podem ter pontuações próximas. Um gráfico de resumo dos pdfs avaliados é dado por:

```python
dist.plot_summary()
```

Se o número de amostras for muito baixo, pode ser difícil obter um bom ajuste em seus dados. Uma solução é brincar com o tamanho das classes, por exemplo. Outra maneira é suavizar o histograma com o parâmetro smooth. O padrão é definido como Nenhum. Vamos avaliar o efeito deste parâmetro.

```python
# Generate data
X = np.random.normal(0, 2, 100)

# Ajuste sem suavizar 
model = distfit()
model.fit_transform(X)
model.plot()

# Ajuste suavizando
model = distfit(smooth=10)
model.fit_transform(X)
model.plot()
```

A suavização tende a ser eficaz em amostras pequenas  (menores que 5000 amostras). Observe que esse número pode ser diferente entre os conjuntos de dados.