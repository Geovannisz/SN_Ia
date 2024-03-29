Autor: [@Geovannisz](https://github.com/Geovannisz/)

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

<div align="center">

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/9737f944-1776-493a-98d2-847c5806cd1c)

</div>

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

<div align="center">

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/8b8777a4-5faa-4fe5-9a4f-fdafd61f6b30)

</div>

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

<div align="center">

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/f151414f-311d-454f-a1fb-60b3550b10d2)

</div>

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

<div align="center">

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/c132f319-acc3-4b23-bca2-a8f331ae38e3)

</div>

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

<div align="center">

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/2317c1f3-dcdd-4ce2-89bc-9c8242db32f2)

</div>

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

<div align="center">

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/384091a3-8d43-4b01-9928-64be19c536e3)

</div>

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

<div align="center">

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/a4a20027-4386-4365-a738-60f804742b29)

</div>

### (g) - Magnitude Aparente em Diferentes Universos

> **g)** Ignorando as correções K e por extinção, vamos calcular a magnitude aparente de um objeto em $z=1$, com magnitude absoluta $M=-19,05$ nos casos abaixo:

<div align="center">

| Tipo de Universo       | $\Omega_m$ | $\Omega_{EE}$ | $w$    |
|          :---:         |    :---:   |     :---:     |  :---: |
| Einstein-de-Sitter     | $1.0$      | $0.0$         |        |
| Geometria Aberta       | $0.3$      | $0.0$         |        |
| "Padrão" (o nosso)     | $0.3$      | $0.7$         | $-1.0$ |
| $\Omega_{EE}$ Dinâmica | $0.3$      | $0.7$         | $-0.8$ |
| $\Omega_{EE}$ Exótica  | $0.3$      | $0.7$         | $-1.2$ |

</div>

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

<div align="center">

|	      | redshift	| modulo_de_distancia |	erro_do_mod_dist |
| :---: |   :---:   |        :---:        |       :---:      |
| **0** |	0.028488  |	     35.339320      |	    0.223906     |
| **1** |	0.050043  |	     36.669580      |    	0.166829     |
| **2** |	0.052926  |	     36.804163      |	    0.155756     |
| **3** |	0.070086  |	     37.428796      |    	0.158467     |
| **4** |	0.062668  |	     37.467377      |    	0.156099     |

</div>

Vamos definir $\chi^2$, para isso, deve-se lembrar que ele é dado por:

$$\chi^2 = \displaystyle\sum_i\dfrac{[\mu_i(z_i) - \mu(z_i,\Omega_M,\Omega_{EE},w)]^2}{\sigma_{\mu_i}^2}$$

Então, criaremos uma função que calcula $\chi^2$:

```python
def chi2(modelo, obs, inc):
  return ((modelo - obs)/inc)**2
```

Agora, vejamos qual o valor de $\Omega_{EE}$ minimiza o $\chi^2$. Para isso, antes devemos calcular os valores de $\chi$ para cada valor de $\Omega_{EE}$ no intervalo de $0$ a $1$:

```python
c = 3e5 # velocidade da luz em km/s
H0 = 70 # constante de hubble em km/(s*Mpc)
dh = c/H0 # distância de hubble em Mpc
w = -1

#Calcula a curva
def curva(x, omega_m, omega_ee, w):
  d_L = dist(x, omega_m, omega_ee, w)
  return (5*np.log10(d_L) + 25)

x = []
y = []
erro = []
for i in range(len(dados)):
  x.append(dados["redshift"][i])
  y.append(dados["modulo_de_distancia"][i])
  erro.append(dados["erro_do_mod_dist"][i])

omega_ee = np.linspace(float(0.001), float(1), 999)
omega_m = []
for i in range(0, len(omega_ee)):
    omega_mi = 1 - omega_ee[i]
    omega_m.append(omega_mi)

# Cálculo dos chi^2:

chi = []
for i in range(0, len(omega_ee)):
  om_mi = omega_m[i]
  om_eei = omega_ee[i]
  chi_i = 0
  for j in range(0, len(x)):
    xj = x[j]
    yj = y[j]
    erroj = erro[j]
    mod = curva(xj, om_mi, om_eei, -1)
    chi_i += chi2(mod, yj, erro)[0]
  chi.append(chi_i)

omega_ee_min = omega_ee[chi.index(min(chi))]
print("chi^2 mínimo:", min(chi))
print("Omega_EE que minimiza o chi^2:", omega_ee_min)
```
Esse código deverá lhe imprimir os valores:

```
chi^2 mínimo: 818.3044978119215
Omega_EE que minimiza o chi^2: 0.5765761523046092
```

Se plotarmos o gráfico de como $\chi^2$ varia em função de $\Omega_{EE}$, poderemos observar melhor o quanto $\chi^2$ pode ser minimizado.

```python
plt.style.use(matplotx.styles.dracula)
plt.plot(omega_ee, chi)
plt.xlabel('$\\Omega_{EE}$')
plt.ylabel('$\\chi^{2}$')
plt.title("Variação do $\\chi^{2}$ com $\\Omega_{EE}$")
plt.xlim(0,1)
plt.grid()
plt.show()
```

O gráfico mostrado deve ser:

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/b86debd1-7a2c-4689-b52f-3930c8cc2e0f)

Admitindo esse valor de $\Omega_{EE}$ onde $\chi^2$ é mínimo, podemos ajustar uma função que minimiza o quadrado da distância de cada ponto dos valores dos [dados](dados.csv). Portanto, devemos fazer o que se segue:

```python
w = -1
omega_ee = omega_ee_min

mod_dist = []
for i in range(0,len(x),1):
    model_i = curva(x[i], 1 - omega_ee_min, omega_ee_min, w)
    mod_dist.append(model_i)

a = sorted(x)
b = sorted(mod_dist)

plt.style.use(matplotx.styles.dracula)
plt.plot(a,b,color="r",label = "Ajuste")
plt.scatter(x,y,s=5,label = "Dados")
plt.grid()
plt.ylabel('$\\mu$', fontsize=16)
plt.xlabel('z', fontsize=16)
plt.title("Variação do $\\mu$ com z")
plt.ylim(35,max(y))
plt.xlim(0,max(x))
plt.legend()
```

O gráfico resultante será o que é exibido a seguir:

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/d3d19cdc-a728-4ad2-a773-305d2dafaece)

Por fim, calcularemos qual a probabilidade de $\Omega_{EE}>0,5$.

```python
def prob_dens(chi):
  pdf = np.exp(-chi/float(1.239777))
  return pdf

omega_ee = np.linspace(float(0.001), float(1), 999)
pdf = []
for i in range(0, len(omega_ee)):
  pdf.append(prob_dens(chi[i]))

# Fazer a integral pelo método dos retângulos pra facilitar
n = len(omega_ee)

# Vetor com as distâncias entre os pontos:
h = []

for i in range(1, n, 1):
	h_i = omega_ee[i] - omega_ee[i-1]
	h.append(h_i)

# Integral do numerador:
int_1 = 0
for i in range(0, n-1, 1):
  if omega_ee[i] >= 0.5:
    int_1 += h[i]*(pdf[i])

# Integral do denominador:

int_2 = 0
for i in range(0, n-1, 1):
  int_2 += h[i] * (pdf[i])

plt.style.use(matplotx.styles.dracula)
plt.plot(omega_ee, pdf)
plt.xlabel("$\\Omega_{EE}$")
plt.ylabel("Densidade de probabilidade")
plt.xlim(0,1)
plt.xticks([i/10 for i in range(11)])
plt.yticks([])
plt.show()

print("A probabilidade de Omega_EE ser maior que 0.5 é:", (int_1/int_2))
```

Esse código deve lhe exibir o seguinte:

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/49300bd3-a149-434d-9cbe-37a0c533e535)

```
A probabilidade de Omega_EE ser maior que 0.5 é: 0.9999999952214428
```

Desse modo, vemos que é pouco possível que $\Omega_{EE}$ seja maior que $0,5$.

### (b) - Elipses de Covariância de Matéria e Energia Escura

> **b)** Calcularemos agora o melhor valor (máxima verossimilhança) e os intervalos de $68,3$%, $95,4$% e $99,7$% ($1$, $2$, $3$ “$\sigma$” de uma distribuição Normal) para $\Omega_M$ e $\Omega_{EE}$ , supondo $w=-1$.

Começaremos importanto e separando os valores do redshift, do módulo da distância e seu respectivo erro dos [dados](dados.csv).

```python
z = dados["redshift"]
mod_dist = dados["modulo_de_distancia"]
erro = dados["erro_do_mod_dist"]
```

Criaremos algumas funções semelhantes às que criamos anteriormente apenas para que elas não sejam mudadas.

```python
#Calcula m_model_i
def m_modeli(z, omega_m, omega_ee, w):
  d_L = dist(z, omega_m, omega_ee, w)
  return (5*np.log10(d_L) + 25)

#Calcula chi2
def chi_quad(m_i, m_mod_i, s_i):
  return ((m_i - m_mod_i)/s_i)**2
```

Definidas as funções, façamos o código que será necessário para, posteriormente, plotar a densidade covariante de probabilidades onde o valor de $\chi^2$ mínimo depende da máxima verossimilhança entre $\Omega_{EE}$ e $\Omega_m$.

```python
c = 3e5 # velocidade da luz em km/s
H0 = 70 # constante de hubble em km/(s*Mpc)
dh = c/H0 # distância de hubble em Mpc
w = -1

Omega_EE_max = float(1)
Omega_EE_min = float(0)
Omega_m_max = float(1)
Omega_m_min = float(0)
n = 100 #numero de pontos do vetor

omega_m = np.linspace(Omega_m_min, Omega_m_max, n)
omega_ee = np.linspace(Omega_EE_min, Omega_EE_max, n)
OMEGA_M, OMEGA_EE = np.meshgrid(omega_m, omega_ee)

chi = []
chi_min = 1000000000
omega_m_min = omega_m[0]
omega_ee_min = omega_ee[0]

for j in range(len(OMEGA_M)):
  linha_chi = []

  for k in range(len(OMEGA_M[j])):
    chi_i = 0

    for i in range(len(z)):
      m_mod_ijk = m_modeli(z[i], OMEGA_M[j][k], OMEGA_EE[j][k], w)
      m_i = mod_dist[i]
      chi_i += chi_quad(m_i, m_mod_ijk, erro[i])

    linha_chi.append(chi_i)

    if chi_i < chi_min:
      indice_chi_min_j = j
      indice_chi_min_k = k
      chi_min = chi_i
      omega_m_min = OMEGA_M[j][k]
      omega_ee_min = OMEGA_EE[j][k]

  chi.append(linha_chi)

chi = np.array(chi)

int_conf = [2.3, 6.17, 11.8] #Deltas chi^2
level_elip = [chi_min, chi_min + int_conf[0], chi_min + int_conf[1], chi_min + int_conf[2]] #intervalos de confiança
```

O primeiro gráfico que podemos plotar é um gráfico de calor de $\Omega_{EE}$ e $\Omega_m$ em função de $\chi^2$, segue o código e seu respectivo resultado:

```python
plt.style.use(matplotx.styles.dracula)
plt.pcolormesh(OMEGA_M, OMEGA_EE, chi, cmap=plt.get_cmap('gist_heat'))
plt.colorbar()
plt.contour(OMEGA_M, OMEGA_EE, chi, 10, colors='green')
plt.xlabel("$\\Omega_{M}$")
plt.ylabel("$\\Omega_{EE}$")
plt.title("$\\chi^2$")
plt.show()
```

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/dbaa8c83-47b2-4b56-b0a0-639bdd5c3160)

Uma variação do gráfico anterior, onde analisamos o $\log\chi^2$ ao invés de $\chi^2$, também pode ser feita. Segue o código que faz isso e seu respectivo resultado:

```python
plt.style.use(matplotx.styles.dracula)
plt.pcolormesh(OMEGA_M, OMEGA_EE, chi, cmap=plt.get_cmap('gist_heat'))
plt.colorbar()
plt.contour(OMEGA_M, OMEGA_EE, chi, 10, colors='green')
plt.xlabel("$\\Omega_{M}$")
plt.ylabel("$\\Omega_{EE}$")
plt.title("$\\chi^2$")
plt.show()
```

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/6acc59b9-5102-4f9c-bb16-2b2337b394d2)

O último gráfico que podemos plotar é um gráfico semelhante ao primeiro mas agora com elipses de incertezas desenhadas nele. Segue o código e seu respectivo resultado:

```python
plt.style.use(matplotx.styles.dracula)
plt.pcolormesh(OMEGA_M, OMEGA_EE, chi, cmap=plt.get_cmap('gist_heat'))
plt.colorbar()
plt.contour(OMEGA_M, OMEGA_EE, chi, 10, colors='green')
plt.xlabel("$\\Omega_{M}$")
plt.ylabel("$\\Omega_{EE}$")
plt.title("$\\chi^2$")
plt.show()
```

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/5ee7cfda-2b2e-492e-a115-fc9ebf5f4891)

Escolhendo os valores de $\Omega_{EE}$ e $\Omega_m$ que minimizam $\chi^2$, podemos fazer um novo ajuste dos [dados](dados.csv).

```
# Definindo os novos limites para z
z_extended = np.linspace(-0.03, 1.45, len(z))

# Comparação entre modelo e dados
model_extended = []
for i in range(len(z_extended)):
    model_i = m_modeli(z_extended[i], omega_m_min, omega_ee_min, -1)
    model_extended.append(model_i)

redshift_extended = sorted(z_extended)
modeldist_extended = sorted(model_extended)

plt.style.use(matplotx.styles.dracula)
plt.plot(z, mod_dist, linestyle="", marker='.', label = "Dados")
plt.plot(redshift_extended, modeldist_extended, linewidth=2, color='r', label = "Modelo")
plt.legend()
plt.title("Modelo versus Dados")
plt.ylabel("Módulo de distância")
plt.xlabel("Redshift")
plt.xlim(-0.03,1.45)
plt.ylim(33.5,45.5)
plt.grid()
plt.show()

print("chi^2_min: %.2f" %chi_min)
print("Omega_m do chi_min: %.2f" %omega_m_min)
print("Omega_ee de chi_min: %.2f" %omega_ee_min)
```

Esse cógido deve retornar:

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/6e0daead-3c3e-4c2e-8497-4bc49f61d0c7)

```
chi^2_min: 562.24
Omega_m do chi_min: 0.57
Omega_ee de chi_min: 0.63
```

Agora, se quisermos ver explicitamente como $\chi^2$ varia em função de $\Omega_m$ podemos gerar um gráfico dessa variação:

```python
plt.style.use(matplotx.styles.dracula)
plt.plot(omega_m, chi[indice_chi_min_j])
plt.xlabel('$\\Omega_{M}$')
plt.ylabel('$\\chi^{2}$')
plt.xlim(0,1)
plt.title("$\\chi^{2}$ versus $\\Omega_{M}$")
plt.grid()
plt.show()
```

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/50cd340a-82fd-4fa0-ad01-fbe2b3041eb1)

Por fim, se quisermos ver explicitamente como $\chi^2$ varia em função de $\Omega_m$ podemos gerar um gráfico dessa variação:

```python
plt.style.use(matplotx.styles.dracula)
plt.plot(omega_ee, chi[indice_chi_min_j])
plt.xlabel('$\\Omega_{EE}$')
plt.ylabel('$\\chi^{2}$')
plt.xlim(0,1)
plt.title("$\\chi^{2}$ versus $\\Omega_{EE}$")
plt.grid()
plt.show()
```

![image](https://github.com/Geovannisz/SN_Ia/assets/82838501/f686d1fb-15a1-4747-985b-06b3976e7e08)

Concluindo a nossa análise, podemos encontrar os valores dos extremos nos intervalos pelo seguinte código:

```python
# Encontra os valores extremos dos intervalos
def encont_inter(chi, OMEGA_M, OMEGA_EE):
  int_omega_m_68 = [-2, 2]
  int_omega_m_95 = [-2, 2]
  int_omega_m_99 = [-2, 2]

  int_omega_ee_68 = [-2, 2]
  int_omega_ee_95 = [-2, 2]
  int_omega_ee_99 = [-2, 2]

  int_con = [2.3, 6.17, 11.8] # Deltas chi^2

  for i in range(len(chi)):

    for j in range(len(chi[0])):

      if (chi[i][j] < (chi_min + int_con[0])):

        if OMEGA_M[i][j] > int_omega_m_68[0]:
          int_omega_m_68[0] = OMEGA_M[i][j]

        elif OMEGA_M[i][j] < int_omega_m_68[1]:
          int_omega_m_68[1] = OMEGA_M[i][j]

        if OMEGA_EE[i][j] > int_omega_ee_68[0]:
          int_omega_ee_68[0] = OMEGA_EE[i][j]

        elif OMEGA_EE[i][j] < int_omega_ee_68[1]:
          int_omega_ee_68[1] = OMEGA_EE[i][j]

      elif (chi[i][j] < (chi_min + int_con[1])):

        if OMEGA_M[i][j] > int_omega_m_95[0]:
          int_omega_m_95[0] = OMEGA_M[i][j]

        elif OMEGA_M[i][j] < int_omega_m_95[1]:
          int_omega_m_95[1] = OMEGA_M[i][j]

        if OMEGA_EE[i][j] > int_omega_ee_95[0]:
          int_omega_ee_95[0] = OMEGA_EE[i][j]

        elif OMEGA_EE[i][j] < int_omega_ee_95[1]:
          int_omega_ee_95[1] = OMEGA_EE[i][j]

      elif (chi[i][j] < (chi_min + int_con[2])):

        if OMEGA_M[i][j] > int_omega_m_99[0]:
          int_omega_m_99[0] = OMEGA_M[i][j]

        elif OMEGA_M[i][j] < int_omega_m_99[1]:
          int_omega_m_99[1] = OMEGA_M[i][j]

        if OMEGA_EE[i][j] > int_omega_ee_99[0]:
          int_omega_ee_99[0] = OMEGA_EE[i][j]

        elif OMEGA_EE[i][j] < int_omega_ee_99[1]:
          int_omega_ee_99[1] = OMEGA_EE[i][j]

  return int_omega_m_68, int_omega_m_95, int_omega_m_99, int_omega_ee_68, int_omega_ee_95, int_omega_ee_99
```

Assim, finalmente, podemos imprimir os intervalos de confianças das elipses.

```python
intervalos = encont_inter(chi, OMEGA_M, OMEGA_EE)

int_omega_m_68 = intervalos[0]
int_omega_m_95 = intervalos[1]
int_omega_m_99 = intervalos[2]
int_omega_ee_68 = intervalos[3]
int_omega_ee_95 = intervalos[4]
int_omega_ee_99 = intervalos[5]

print("Intervalo de confiança de 68: Omega_M = [%.2f, %.2f], Omega_EE = [%.2f, %.2f]" %(int_omega_m_68[1], int_omega_m_68[0], int_omega_ee_68[1], int_omega_ee_68[0]))
print("Intervalo de confiança de 95: Omega_M = [%.2f, %.2f], Omega_EE = [%.2f, %.2f]" %(int_omega_m_95[1], int_omega_m_95[0], int_omega_ee_95[1], int_omega_ee_95[0]))
print("Intervalo de confiança de 99: Omega_M = [%.2f, %.2f], Omega_EE = [%.2f, %.2f]" %(int_omega_m_99[1], int_omega_m_99[0], int_omega_ee_99[1], int_omega_ee_99[0]))
```

Isso deve imprimir:

```
Intervalo de confiança de 68: Omega_M = [0.26, 0.92], Omega_EE = [0.38, 0.90]
Intervalo de confiança de 95: Omega_M = [0.07, 1.00], Omega_EE = [0.23, 1.00]
Intervalo de confiança de 99: Omega_M = [0.00, 1.00], Omega_EE = [0.13, 1.00]
```

### (c) - Covariância de Matéria e Energia Escura em um Universo Aberto








### (d) - Covariância entre Matéria e Pressão da Energia Escura





