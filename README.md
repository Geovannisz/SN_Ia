# Super Novas do Tipo Ia
🚀 Neste projeto encontro analiticamente e numericamente constantes cosmológicas do Universo a partir de um banco de dados do redshift de Super Novas do tipo Ia. Para isso foi usado o Monte Carlo da Cadeia de Markov com o fim de determinar a covariância entre diferentes grandezas e de encontrar a máxima verossimilhança de suas respectivas elipses de incertezas.

## Sumário
* [***Super Novas do Tipo Ia***](#super-novas-do-tipo-ia)
   * [**Notações e Definições**](#notações-e-definições)
      * [1. *Constante de Hubble*](#1-h_0--constante-de-hubble)
      * [2. *Densidade de Energia Escura*](#2-omega_ee--densidade-de-energia-escura)
      * [3. *Densidade de Matéria*](#3-omega_m--densidade-de-matéria)
      * [4. *Densidade de Curvatura*](#4-omega_k--densidade-de-curvatura)
      * [5. *Densidade de Matéria Bariônica*](#5-omega_b--densidade-de-matéria-bariônica)
      * [6. *Densidade de Energia de Radiação*](#6-omega_r--densidade-de-energia-de-radiação)
      * [7. *Parâmetro da Equação de Estado da Energia Escura*](#7-w--parâmetro-da-equação-de-estado-da-energia-escura)
  * [**A Distância em Diferentes Tipos de Universo**](#parte-1---a-distância-em-diferentes-tipos-de-universo)
      * [(a) - *Distâncias Cosmológicas*](#a---distâncias-cosmológicas)
      * [(b) - *Distâncias em Universo de Energia Escura*](#b---d_l-em-um-universo-de-omega_ee)
      * [(c) - *Distâncias em Universo de Matéria*](#c---d_l-em-um-universo-de-omega_m)
      * [(d) - *Distâncias em Universo Fechado*](#d---d_l-em-um-universo-de-omega_k)
      * [(e) - *Comparação das Distâncias nos Universos*](#e---omega_ee-omega_m-e-benchmark)
      * [(f) - *Modo Alternativo de Medir Distâncias*](#f---outra-maneira-de-encontrar-d_l)
      * [(g) - *Magnitude Aparente em Diferentes Universos*](#g---magnitude-aparente-em-diferentes-universos)
  * [**O Redshift de Super Novas do Tipo Ia**](#parte-2---o-redshift-de-super-novas-do-tipo-ia)
      * [(a) - *Calculando a Densidade de Energia Escura*](#a---calculando-a-densidade-de-energia-escura)
      * [(b) - *Elipses de Covariância de Matéria e Energia Escura*](#b---elipses-de-covariância-de-matéria-e-energia-escura)
      * [(c) - *Covariância de Matéria e Energia Escura em um Universo Aberto*](#c---covariância-de-matéria-e-energia-escura-em-um-universo-aberto)
      * [(d) - *Covariância entre Matéria e Pressão da Energia Escura*](#d---covariância-entre-matéria-e-pressão-da-energia-escura)

## Notações e Definições

Aqui neste projeto, utilizarei a mesma notação de Bárbara Ryder em seu livro [*Introduction to Cosmology*](https://amzn.to/4a62Awl). Portanto, irei primeiro introduzir aqui brevemente algumas dessas notações.

### **1. $H_0$ : Constante de Hubble**

* Mede a taxa de expansão do universo no tempo presente.
* É um valor fundamental para determinar a idade do universo e a escala de distâncias cosmológicas.
* Valores atuais estimados:
    * $H_0 = 67,4~km\cdot s^{-1}\cdot Mpc^{-1}$ por meio da análise das flutuações de temperatura da radiação cósmica de fundo em micro-ondas (CMB).
    * $H_0 = 71,9~km\cdot s^{-1}\cdot Mpc^{-1}$ por meio da observação direta da velocidade de galáxias distantes pelo desvio para o vermelho da luz emitida.

### **2. $\Omega_{EE}$ : Densidade de Energia Escura**

* Fração da densidade crítica atribuída à energia escura, responsável pela expansão acelerada do universo.
* Em nosso Universo as estimativas atuais são em torno de 0,69.

### **3. $\Omega_m$ : Densidade de Matéria**

* Fração da densidade crítica atribuída à matéria total, incluindo matéria bariônica e matéria escura.
* Em nosso Universo é um valor positivo e menor que 1, com estimativas atuais em torno de 0,31.

### **4. $\Omega_k$ : Densidade de Curvatura**

* Representa a fração da densidade crítica do universo atribuída à curvatura espacial.
* Valores:
    * $\Omega_k > 0$ : Universo fechado, com curvatura positiva que faz com que o universo se contraia após um período de expansão.
        * **Destino:** um "Big Crunch", onde toda a matéria e energia se concentram em um único ponto.
    * $\Omega_k = 0$ : Universo plano, com curvatura zero que faz com que o universo se expanda eternamente sem se curvar.
        * **Destino:** um "Big Freeze", onde o universo se torna cada vez mais frio e diluído, com estrelas eventualmente se apagando e a formação de novas estrelas se tornando impossível.
    * $\Omega_k < 0$ : Universo aberto, com curvatura negativa que faz com que o universo sofra uma expansão eternamente acelerada.
        * **Destino:**  um "Big Rip", onde a expansão se torna tão forte que as galáxias, estrelas e até mesmo átomos se desintegram.
* As medições cosmológicas atuais indicam que $\Omega_k\approx 0$, sendo o universo é muito provavelmente plano. 
* Relação entre os parâmetros vistos até aqui:
    * $\Omega_k + \Omega_{EE} + \Omega_m = 1$
* Exemplo:
    * Se $\Omega_k = 0$, $\Omega_{EE} = 0,7$ e $\Omega_m = 0,3$, então o universo é plano e a energia escura é a principal componente, seguida pela matéria.

### **5. $\Omega_b$ : Densidade de Matéria Bariônica**

* Fração da densidade crítica atribuída à matéria bariônica, composta por prótons e nêutrons.
* É uma fração de $\Omega_m$, com estimativa atual de $\Omega_b = 0,049$.

### **6. $\Omega_r$ : Densidade de Energia de Radiação**

* Fração da densidade crítica atribuída à energia de radiação, incluindo fótons e neutrinos.
* É um valor que diminui com o tempo devido à expansão do universo.

### **7. $w$ : Parâmetro da Equação de Estado da Energia Escura**

* Descreve a relação entre a pressão e a densidade da energia escura.
* Um valor de $w = -1$ corresponde à energia escura da constante cosmológica $\Lambda$.
* Valores de $w < -1$ indicam uma energia escura "fantasma" com propriedades exóticas.
* Valores de $w > -1$ sugerem uma energia escura dinâmica com propriedades que variam com o tempo.

## Parte 1 - *A distância em diferentes tipos de Universo*

Vamos, no decorrer desta primeira parte, entender o comportamento da distância de luminosidade $D_L$. Para isso deveremos antes compreender como funciona outros tipos de distâncias como a comóvel $D_C$ e a de Hubble $D_H$. No caso da distância comóvel, como ela é obtida por meio de uma integral, iremos comparar os resultados numéricos em vários casos onde a integral possa ser resolvida analiticamente (e.g. Universo vazio, só de matéria, só de constante cosmológica, etc...). Também iremos mostrar a diferença dos resultados numéricos e analíticos em função do redshift até $z=10$.

### (a) - Distâncias Cosmológicas

> **a)** Para começar, vamos criar uma função que calcule a distância de luminosidade. Para encontrá-la é necessário o cálculo de uma integral numérica. Por isso, vamos definí-la antes de encontrá-la.

Para determinar a distância de luminosidade $D_L$, temos que calcular a seguinte expressão:

$$D_L = (1 + z)D_M$$

onde 

```math
\begin{align}
    D_M = \begin{dcases*}
      D_H \dfrac{1}{\sqrt{\Omega_k}}\sinh\left[\dfrac{D_C}{D_H}\sqrt{\Omega_k}\right] & para $\Omega_k > 0$\\
      D_C & para $\Omega_k = 0$\\
      D_H \dfrac{1}{\sqrt{\Omega_k}}\sin\left[\dfrac{D_C}{D_H}\sqrt{\Omega_k}\right] & para $\Omega_k < 0$
    \end{dcases*}
\end{align}
```
    
sendo $D_H$ é a distância de Hubble 

$$D_H = \dfrac{c}{H_0} $$

e $D_C$ é a distância comóvel na direção da linha de visada 

$$ D_C = D_H \displaystyle\int^{z}_{0} \dfrac{dz'}{E(z')} $$

sendo 

$$ E(z) = \sqrt{\Omega_M (1 + z)^3 + \Omega_k (1 + z)^2 +\Omega_{EE}(1+z)^{3(1+w)}} $$

Antes, vamos importar as bibliotecas que serão usadas no decorrer do código:

```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from astropy.cosmology import LambdaCDM
from scipy import integrate
```

Escolhemos a regra do trapézio como método de integração para integrar $\displaystyle\int^{z}_{0} = \dfrac{dz'}{E(z')}$:

```python
def ez(z, omega_m, omega_ee, omega_k, w):
    return np.sqrt(omega_m*(1+z)**3+omega_k*(1+z)**2+omega_ee*(1+z)**(3*(1+w)))

def integral(z, H, omega_m, omega_ee, omega_k, w):
    integral = 0
    soma = 0
    i = z/100000
    h = z/100000

    while i < z:
        soma += 1/ez(i,omega_m,omega_ee,omega_k, w)
        i += h

    integral = h*(0.5*ez(0,omega_m,omega_ee,omega_k, w) + soma + 0.5*ez(z,omega_m,omega_ee,omega_k, w))
    return integral
```

Função para calcular a $D_L$:

```python
def dist(z, H, omega_m, omega_ee, w):

    omega_k = 1 - omega_m - omega_ee

    c = 3*10**5 # km/s
    dh = c/H
    dc = dh*integral(z, H, omega_m, omega_ee, omega_k, w)
    if omega_k == 0:
        dm = dc
    elif omega_k > 0:
        dm = (dh/np.sqrt(omega_k))*np.sinh(np.sqrt(omega_k)*dc/dh)
    else:
        dm = (dh/np.sqrt(-omega_k))*np.sin(np.sqrt(-omega_k)*dc/dh)

    dl = (1+z)*dm

    mod_dist = 5*np.log10(dl*100000)

    return dl, mod_dist
```

Caso você queira testar para diferentes entradas:

```python
z = float(input('Digite o valor de z: '))
H = float(input('Digite o valor de H: '))
omega_m = float(input('Digite o valor de omega_m: '))
omega_ee = float(input('Digite o valor de omega_ee: '))
w = float(input('Digite o valor de w: '))

l = dist(z, H, omega_m, omega_ee, w)
print("Distância de Luminosidade = %.2f" %l[0], "Mpc")
print("Módulo de Distância = %.2f" %l[1], "Mpc")
print("Distância Comóvel = %.2f" %l[2], "Mpc")
print("Distância de Hubble = %.2f" %l[3], "Mpc")
```

Alguns possíveis valores aleatórios para teste podem ser:

```python
z = 1
H = 70
omega_m = 0
omega_ee = 1
w = -1

l = dist(z, H, omega_m, omega_ee, w)
print("Distância de Luminosidade = %.2f" %l[0], "Mpc")
print("Módulo de Distância = %.2f" %l[1], "Mpc")
print("Distância Comóvel = %.2f" %l[2], "Mpc")
print("Distância de Hubble = %.2f" %l[3], "Mpc")
```

Você deve esperar o seguinte resultado ao executar esse código:

```
Distância de Luminosidade = 8571.51 Mpc
Módulo de Distância = 44.67 Mpc
Distância Comóvel = 4285.76 Mpc
Distância de Hubble = 4285.71 Mpc
```

Vamos fazer um teste usando a função *(luminosity_distance(z) do pacote astropy)* para comparar o valor real com o valor obtido em um Universo Dominado por $\Omega_{EE}$:

```python
z = 1
H = 70
omega_m = 0
omega_ee = 1
w = -1

l = dist(z, H, omega_m, omega_ee, w)
print("d_l = %.2f" %l[0],'Mpc')

cosmo = LambdaCDM(H0=70, Om0=0, Ode0=1)
D_lambdaCDM = str(cosmo.luminosity_distance(z))
D_lambdaCDM = float(D_lambdaCDM[:9])
Erro = ((l[0] - D_lambdaCDM)/D_lambdaCDM)*100
print("Erro percentual = %.3f" %Erro, "porcento")
```

Esse código imprime no terminal:

```
Distância de Luminosidade obtida   = 8571.51 Mpc
Distância de Luminosidade esperada = 8565.50 Mpc
Erro = 0.070 %
```

### (b) - $D_L$ em um Universo de $\Omega_{EE}$

> **b)** Iremos agora, antes de prosseguir na nossa análise, comparar o resultado do método análitico e da nossa função para um Universo dominado por $\Omega_{EE}$, ou seja, $\Omega_m = 0$, $\Omega_k = 0$ e $\Omega_{EE} = 1$.

Aplicando as formulas dadas no inicio deste trabalho, encontramos que $D_L$ assumirá a seguinte forma:

$$D_L = \dfrac{cz}{H_0}(1 + z)$$

Portanto, vamos criar uma função que a define:

```python
def d_LEE(z, c, H):
   d_L = ((c*z)/H)*(1 + z)
   return d_L
```

Agora podemos plotar um gráfico do método analítico e numérico junto com uma respectiva curva de erro entre ambos. Segue o código para tal:

```python
z = np.arange(0.01, 10, 0.1)

c = 3*10**5 # km/s
H = 70
dh = c/H
omega_m = 0
omega_ee = 1
w = -1

eixo_y_EE = np.array([])
eixo_y_d_LEE = np.array([])

for a in z:
   l = dist(a, H, omega_m, omega_ee, w)
   eixo_y_EE  = np.append(eixo_y_EE, (H/c)*l[0])
   D_l = d_LEE(a, c, H)
   eixo_y_d_LEE  = np.append(eixo_y_d_LEE, (H/c)*D_l)

erro = eixo_y_EE - eixo_y_d_LEE

plt.style.use(matplotx.styles.dracula)
plt.subplot(2, 1, 1)
plt.plot(z, eixo_y_EE, linestyle='dashdot', linewidth=2, color='white', label = 'Numérico')
plt.plot(z, eixo_y_d_LEE, linestyle='-', color='red', label = 'Analítico')
plt.title('$\\Omega_{EE} = 1$')
plt.ylabel('$\\frac{D_{L}H_{0}}{c}$', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.xlim(0, 10)
plt.legend()
plt.subplot(2, 1, 2)
plt.plot(z, erro, linestyle='-', color='yellow', label = 'erro')
plt.ylabel('Erro', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.xlim(0, 10)
plt.legend()
```

O gráfico obtido é o seguinte:

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/9737f944-1776-493a-98d2-847c5806cd1c)

Nele podemos ver que nosso método numérico se aproxima bastante do real.

### (c) - $D_L$ em um Universo de $\Omega_{m}$

> **c)** Vamos agora comparar o resultado do método análitico e da nossa função para um Universo dominado por $\Omega_{m}$, ou seja, $\Omega_m = 1$, $\Omega_k = 0$ e $\Omega_{EE} = 0$.

Aplicando as formulas dadas no inicio desta parte encontramos que $D_L$ assumirá a seguinte forma:

$$D_L = \dfrac{c(1+z)^2}{H_0}\left(2 - \frac{2}{\sqrt{1 + z}}\right)$$

Portanto, vamos criar uma função que a define:

```python
def d_Lm(z, c, H):
   d_L = ((c*((1+z)**2))/H)*(2 - (2/(np.sqrt(1+z))))
   return d_L
```

Agora podemos plotar um gráfico do método analítico e numérico junto com uma respectiva curva de erro entre ambos. Segue o código para tal:

```python
z = np.arange(0.01, 10, 0.1)

c = 3*10**5 # km/s
H = 70
dh = c/H
omega_m = 1
omega_ee = 0
w = 0

eixo_y_m = np.array([])
eixo_y_d_Lm = np.array([])

for a in z:
   l = dist(a, H, omega_m, omega_ee, w)
   eixo_y_m  = np.append(eixo_y_m, (H/c)*l[0])
   D_L = d_Lm(a, c, H)
   eixo_y_d_Lm  = np.append(eixo_y_d_Lm, (H/c)*D_L)

erro = eixo_y_m - eixo_y_d_Lm

plt.style.use(matplotx.styles.dracula)
plt.subplot(2, 1, 1)
plt.plot(z, eixo_y_m, linestyle='dashdot', linewidth=2, color='white', label = 'Numérico')
plt.plot(z, eixo_y_d_Lm, linestyle='-', color='red', label = 'Analítico')
plt.title('$\\Omega_{m} = 1$')
plt.ylabel('$\\frac{D_{L}H_{0}}{c}$', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.ylim(0,16)
plt.xlim(0, 10)
plt.legend()
plt.subplot(2, 1, 2)
plt.plot(z, erro, linestyle='-', color='yellow', label = 'erro')
plt.ylabel('Erro', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.xlim(0, 10)
plt.legend()
```

O gráfico obtido é o seguinte:

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/8b8777a4-5faa-4fe5-9a4f-fdafd61f6b30)

Nele podemos ver que nosso método analítico se distancia exponencialmente do numérico a medida que aumenta o valor de $z$.

### (d) - $D_L$ em um Universo de $\Omega_{k}$

> **d)** Iremos agora, antes de prosseguir na nossa análise, comparar o método análitico e a nossa função para um Universo dominado por $\Omega_{k}$, ou seja, $\Omega_k = 0$, $\Omega_k = 1$ e $\Omega_{EE} = 0$.

Aplicando as formulas dadas no inicio desta página encontramos que $D_L$ assumirá a seguinte forma:

$$D_L = \dfrac{c(1+z)}{H_0}\ln(1+z)$$

Portanto, vamos criar uma função que a define:

```python
def d_Lk(z, c, H):
   d_L = ((c*((1+z)))/H) * np.log(1 + z)
   return d_L
```

Agora podemos plotar um gráfico do método analítico e numérico junto com uma respectiva curva de erro entre ambos. Segue o código para tal:

```python
z = np.arange(0.01, 10, 0.1)

c = 3*10**5 # km/s
H = 70
dh = c/H
omega_m = 0
omega_ee = 0
w = -1

eixo_y_k = np.array([])
eixo_y_d_Lk = np.array([])

for a in z:
   l = dist(a, H, omega_m, omega_ee, w)
   eixo_y_k  = np.append(eixo_y_k, (H/c)*l[0])
   D_L = d_Lk(a, c, H)
   eixo_y_d_Lk  = np.append(eixo_y_d_Lk, (H/c)*D_L)

erro = eixo_y_k - eixo_y_d_Lk

plt.style.use(matplotx.styles.dracula)
plt.subplot(2, 1, 1)
plt.plot(z, eixo_y_k, linestyle='dashdot', linewidth=2, color='white', label = 'Numérico')
plt.plot(z, eixo_y_d_Lk, linestyle='-', color='red', label = 'Analítico')
plt.title('$\\Omega_{EE} = 1$')
plt.ylabel('$\\frac{D_{L}H_{0}}{c}$', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.xlim(0, 10)
plt.legend()
plt.subplot(2, 1, 2)
plt.plot(z, erro, linestyle='-', color='yellow', label = 'erro')
plt.ylabel('Erro', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.xlim(0, 10)
plt.legend()
```

O gráfico obtido é o seguinte:

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/f151414f-311d-454f-a1fb-60b3550b10d2)

Nele podemos ver que nosso método analítico se distancia exponencialmente do numérico a medida que aumenta o valor de $z$, no entanto se distancia menos do que o anterior.

### (e) - $\Omega_{EE}$, $\Omega_m$ e Benchmark

> **e)** Nós iremos agora reproduzir a figura apresentada como Figura 6.2 no [livro de cosmologia de Bárbara Ryder](https://amzn.to/4a62Awl):

Primeiro obteremos o gráfico do Universo dominado pelo parâmetro de energia escura:

$$\Omega_m = 0,\; \Omega_{EE} = 1\;\mathrm{e}\; w = -1$$

```python
z = np.arange(0.01, 6, 0.05)

c = 3*10**5 # km/s
H = 70
dh = c/H

eixo_y_EE = np.array([])

for a in z:
   l = dist(a, H, 0, 1, -1)
   eixo_y_EE  = np.append(eixo_y_EE, (H/c)*l[0])
```

Posteriormente do Universo dominado pela matéria:

$$\Omega_m = 1,\; \Omega_{EE} = 0\;\mathrm{e}\; w = 0$$

```python
z = np.arange(0.01, 6, 0.05)

c = 3*10**5 # km/s
H = 70
dh = c/H

eixo_y_m = np.array([])

for a in z:
   l = dist(a, H, 1, 0, 0)
   eixo_y_m  = np.append(eixo_y_m, (H/c)*l[0])
```

Por fim, do Benchmark:

$$\Omega_m = 0.31,\; \Omega_{EE} = 0.69\;\mathrm{e}\; w = -1$$

```python
z = np.arange(0.01, 6, 0.05)

c = 3*10**5 # km/s
H = 70
dh = c/H

eixo_y_bench = np.array([])

for a in z:
   l = dist(a, H, 0.31, 0.69, -1)
   eixo_y_bench  = np.append(eixo_y_bench, (H/c)*l[0])
```

Podemos finalmente plotar tal gráfico com o seguinte código:

```python
plt.style.use(matplotx.styles.dracula)
plt.plot(z, eixo_y_EE, linestyle='dashdot', label = 'Somente $\\Omega_{EE}$')
plt.plot(z, eixo_y_m, linestyle='--', label = 'Somente Matéria')
plt.plot(z, eixo_y_bench, linestyle='-', color='white', label = 'Benchmark')
plt.ylabel('$\\frac{D_{L}H_{0}}{c}$', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.ylim(0,16)
plt.xlim(0,6)
plt.legend()
```

E, assim, obteremos o gráfico abaixo, que é o da figura em questão do livro.

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/c132f319-acc3-4b23-bca2-a8f331ae38e3)

### (f) - Outra Maneira de Encontrar $D_L$

> **f)** Agora vamos testar a precisão da equação abaixo (da equação 6.31 do [livro de cosmologia de Bárbara Ryder](https://amzn.to/4a62Awl)), para os três casos da figura acima e o mesmo intervalo de redshift.

$$D_L ≈ \dfrac{c}{H_0}(1 + \dfrac{1-q_0}{2}z)$$

onde

$$q_0 = \Omega_m = \Omega_{EE}$$

Portando, vamos definir a função $D_L$:

```python
def d_L(z, omega_m, omega_ee, dh):
   q0 = 0.5*omega_m - omega_ee
   d_L = dh * z * ((1 + ((1 - q0)/2))*z)
   return d_L
```

Em um Universo dominado por $\Omega_{EE}$:  

$$\Omega_m = 0,\; \Omega_{EE} = 1\;\mathrm{e}\; w = -1$$

```python
z = np.arange(0.01, 10, 0.1)
c = 3*10**5 # km/s
H = 70 #km/(s*Mpc)
omega_m = 0
omega_ee = 1
w = -1
dh = c/H

eixo_y_d_L = np.array([])
eixo_y_EE = np.array([])

for a in z:
   l = dist(a, H, omega_m, omega_ee, w)
   eixo_y_EE  = np.append(eixo_y_EE, (H/c)*l[0])
   D_l = d_L(a, omega_m, omega_ee, dh)
   eixo_y_d_L  = np.append(eixo_y_d_L, (H/c)*D_l)

erro = eixo_y_d_L - eixo_y_EE

plt.style.use(matplotx.styles.dracula)
plt.subplot(2, 1, 1)
plt.plot(z, eixo_y_EE, linestyle='dashdot', color='white', label = 'Numérico')
plt.plot(z, eixo_y_d_L, linestyle='-', color='red', label = 'Analítico')
plt.title('$\\Omega_{EE} = 1$')
plt.ylabel('$\\frac{D_{L}H_{0}}{c}$', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.xlim(0, 10)
plt.legend()
plt.subplot(2, 1, 2)
plt.plot(z, erro, linestyle='-', color='yellow', label = 'erro')
plt.ylabel('Erro', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.xlim(0, 10)
plt.legend()
```

Segue gráfico que obtemos para $\Omega_{EE} = 1$:

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/2317c1f3-dcdd-4ce2-89bc-9c8242db32f2)

Agora, para um Universo dominado por $\Omega_{m}$:  

$$\Omega_m = 1, \;\Omega_{EE} = 0\; \mathrm{e}\; w = 0$$

```python
z = np.arange(0.01, 10, 0.1)
c = 3*10**5 # km/s
H = 70 #km/(s*Mpc)
omega_m = 1
omega_ee = 0
w = 0
dh = c/H

eixo_y_d_L = np.array([])
eixo_y_m = np.array([])

for a in z:
   l = dist(a, H, 1, 0, 0)
   eixo_y_m  = np.append(eixo_y_m, (H/c)*l[0])
   D_l = d_L(a, omega_m, omega_ee, dh)
   eixo_y_d_L  = np.append(eixo_y_d_L, (H/c)*D_l)

erro = eixo_y_d_L - eixo_y_m

plt.style.use(matplotx.styles.dracula)
plt.subplot(2, 1, 1)
plt.plot(z, eixo_y_d_L, linestyle='-', color='red', label = 'Analítico')
plt.plot(z, eixo_y_m, linestyle='dashdot', color='white', label = 'Numérico')
plt.title('$\\Omega_m = 1$')
plt.ylabel('$\\frac{D_{L}H_{0}}{c}$', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.xlim(0, 10)
plt.legend()
plt.subplot(2, 1, 2)
plt.plot(z, erro, linestyle='-', color='yellow', label = 'erro')
plt.ylabel('Erro', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.xlim(0, 10)
plt.legend()
```

Segue gráfico que obtemos para $\Omega_m = 1$:

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/384091a3-8d43-4b01-9928-64be19c536e3)

Por fim, para um Universo Vazio com:

$$\Omega_{k} = 1, \;\Omega_m = 1, \;\Omega_{EE} = 0\; \mathrm{e}\; w = 0$$

```python
z = np.arange(0.01, 10, 0.1)
c = 3*10**5 # km/s
H = 70 #km/(s*Mpc)
omega_m = 0
omega_ee = 0
w = 0
dh = c/H

eixo_y_d_L = np.array([])
eixo_y_bench = np.array([])
for a in z:
  l = dist(a, H, 0.31, 0.69, -1)
  eixo_y_bench  = np.append(eixo_y_bench, (H/c)*l[0])
  l = d_L(a, omega_m, omega_ee, dh)
  eixo_y_d_L  = np.append(eixo_y_d_L, (H/c)*l)

erro = eixo_y_d_L - eixo_y_bench

plt.style.use(matplotx.styles.dracula)
plt.subplot(2, 1, 1)
plt.plot(z, eixo_y_d_L, linestyle='-', color='red', label = 'Analítico')
plt.plot(z, eixo_y_bench, linestyle='dashdot', color='white', label = 'Numérico')
plt.title('$\\Omega_k = 1$')
plt.ylabel('$\\frac{D_{L}H_{0}}{c}$', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.xlim(0, 10)
plt.legend()
plt.subplot(2, 1, 2)
plt.plot(z, erro, linestyle='-', color='yellow', label = 'erro')
plt.ylabel('Erro', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.xlim(0, 10)
plt.legend()
```

Com isso obtemos para $\Omega_k = 1$:

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/a4a20027-4386-4365-a738-60f804742b29)

### (g) - Magnitude Aparente em Diferentes Universos

> **g)** Ignorando as correções K e por extinção, vamos calcular a magnitude aparente de um objeto em $z=1$, com magnitude absoluta $M=-19,05$ nos casos abaixo:

| Tipo de Universo       | $\Omega_m$ | $\Omega_{EE}$ | $w$    |
|          :---:         |    :---:   |     :---:     |  :---: |
| Einstein-de-Sitter     | $1.0$      | $0.0$         |        |
| Geometria Aberta       | $0.3$      | $0.0$         |        |
| "Padrão" (o nosso)     | $0.3$      | $0.7$         | $-1.0$ |
| $\Omega_{EE}$ Dinâmica | $0.3$      | $0.7$         | $-0.8$ |
| $\Omega_{EE}$ Exótica  | $0.3$      | $0.7$         | $-1.2$ |

A função `dist(z,H,omega_m,omega_ee,w)` criada anteriormente nos retorna o valor da distância de luminosidade e também o valor do módulo da distância $\mu$. Lembrando que $\mu = m - M$, onde $M$ é a magnitude absoluta e $m$ é a magnitude aparente, dado que $M = -19,05$, pode-se encontrar o valor de $m$.

```python
M = -19.05

# modelo Einstein de Sitter
mi1 = dist(1,70,1,0,0)[1]
m1 = mi1 + M

# modelo Aberto
mi2 = dist(1,70,0.3,0,0)[1]
m2 = mi2 + M

# modelo Padrão
mi3 = dist(1,70,0.3,0.7,-1)[1]
m3 = mi3 + M

# modelo 4
mi4 = dist(1,70,0.3,0.7,-0.8)[1]
m4 = mi4 + M

# modelo 5
mi5 = dist(1,70,0.3,0.7,-1.2)[1]
m5 = mi5 + M

print(" No modelo Einstein-de-Sitter:      m = %.2f" %m1,
      "\n No modelo de Geometria Aberta:     m = %.2f" %m2,
      "\n No modelo \"Padrão\" (o nosso):      m = %.2f" %m3,
      "\n No modelo Energia Escura Dinâmica: m = %.2f" %m4,
      "\n No modelo Energia Escura Exótica:  m = %.2f" %m5
      )
```

Esse código nos imprimirá a magnitude aparente para cada tipo de Universo:

```
 No modelo Einstein-de-Sitter:      m = 24.45 
 No modelo de Geometria Aberta:     m = 24.80 
 No modelo "Padrão" (o nosso):      m = 25.05 
 No modelo Energia Escura Dinâmica: m = 24.96 
 No modelo Energia Escura Exótica:  m = 25.13
```

## Parte 2 - *O Redshift de Super Novas do Tipo Ia*

De agora em diante, usaremos os [dados](dados.csv) coletados do Redshift de Supernovas do tipo Ia na nossa análise.

### (a) - Calculando a Densidade de Energia Escura

> **a)** Vamos calcular o melhor valor (máxima verossimilhança) e os intervalos de $68,3$%, $95,4$% e $99,7$% ($1$, $2$, $3$ “$\sigma$” de uma distribuição Normal) para o $\Omega_{EE}$, supondo $w=-1$ e um Universo Plano.  Além disso, sabendo que a probabilidade $P(\Omega_{EE}) ∝ e^{-\chi^2}$, também vamos calcular a probabilidade desses dados indicarem que a densidade da energia escura é maior do que $0.5$:

$$\dfrac{\displaystyle\int_{0.5}^{+\infty} P(\Omega_{EE})d\Omega_{EE}}{\displaystyle\int_{-\infty}^{+\infty} P(\Omega_{EE})d\Omega_{EE}}$$

Em problemas unidimensionais, com este, $\Delta\chi = 1.0, 4.0, 9.0$ para (1, 2, 3 “$\sigma$”).

Primeiro vamos importar nossos [dados](dados.csv) no código:

```python
url = 'https://raw.githubusercontent.com/Geovannisz/SN_Ia/main/dados.csv'
dados = pd.read_csv("https://raw.githubusercontent.com/Geovannisz/SN_Ia/main/dados.csv", delimiter= " ")
dados.head()
```

O linha `dados.head()` imprimiria as 5 primeiras linhas dos [dados](dados.csv):

|	      | redshift	| modulo_de_distancia |	erro_do_mod_dist |
| :---: |   :---:   |        :---:        |       :---:      |
| **0** |	0.028488  |	     35.339320      |	    0.223906     |
| **1** |	0.050043  |	     36.669580      |    	0.166829     |
| **2** |	0.052926  |	     36.804163      |	    0.155756     |
| **3** |	0.070086  |	     37.428796      |    	0.158467     |
| **4** |	0.062668  |	     37.467377      |    	0.156099     |

Vamos definir $\chi^2$, para isso, deve-se lembrar que ele é dado por:

$$\chi^2 = \displaystyle\sum_i\dfrac{[\mu_i(z_i) - \mu(z_i,\Omega_M,\Omega_{EE},w)]^2}{\sigma_{\mu_i}^2}$$

Então, criaremos uma função que calcula $\chi^2$:

```python
def chi2(modelo, obs, inc):
  return ((modelo - obs)/inc)**2
```

Continua...

### (b) - Elipses de Covariância de Matéria e Energia Escura









### (c) - Covariância de Matéria e Energia Escura em um Universo Aberto








### (d) - Covariância entre Matéria e Pressão da Energia Escura





