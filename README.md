# Super Novas do Tipo Ia
🚀 Neste projeto encontro analiticamente e numericamente constantes cosmológicas do Universo a partir de um banco de dados do redshift de Super Novas do tipo Ia. Para isso foi usado o Monte Carlo da Cadeia de Markov com o fim de determinar a covariância entre diferentes grandezas e de encontrar a máxima verossimilhança de suas respectivas elipses de incertezas.

## Notações e Definições

Aqui neste projeto, utilizarei a mesma notação de Bárbara Ryder em seu livro *Introduction to Cosmology*. Portanto, irei primeiro introduzir aqui brevemente algumas dessas notações.

**1. $H_0$: Constante de Hubble**

* Mede a taxa de expansão do universo no tempo presente.
* É um valor fundamental para determinar a idade do universo e a escala de distâncias cosmológicas.
* Valores atuais estimados:
    * $H_0 = 67,4 km/s/Mpc$ por meio da análise das flutuações de temperatura da radiação cósmica de fundo em micro-ondas (CMB).
    * $H_0 = 71,9 km/s/Mpc$ por meio da observação direta da velocidade de galáxias distantes pelo desvio para o vermelho da luz emitida.

**2. $\Omega_{EE}$:** **Densidade de Energia Escura**

* Fração da densidade crítica atribuída à energia escura, responsável pela expansão acelerada do universo.
* Em nosso Universo as estimativas atuais são em torno de 0,7.

**3. $\Omega_m$: Densidade de Matéria**

* Fração da densidade crítica atribuída à matéria total, incluindo matéria bariônica e matéria escura.
* Em nosso Universo é um valor positivo e menor que 1, com estimativas atuais em torno de 0,3.

**4. $\Omega_k$: Densidade de Curvatura**

* Representa a fração da densidade crítica do universo atribuída à curvatura espacial.
* Valores:
    * $\Omega_k > 0$: Universo fechado, com curvatura positiva que faz com que o universo se contraia após um período de expansão.
        * **Destino:** um "Big Crunch", onde toda a matéria e energia se concentram em um único ponto.
    * $\Omega_k = 0$: Universo plano, com curvatura zero que faz com que o universo se expanda eternamente sem se curvar.
        * **Destino:** um "Big Freeze", onde o universo se torna cada vez mais frio e diluído, com estrelas eventualmente se apagando e a formação de novas estrelas se tornando impossível.
    * $\Omega_k < 0$: Universo aberto, com curvatura negativa que faz com que o universo sofra uma expansão eternamente acelerada.
        * **Destino:**  um "Big Rip", onde a expansão se torna tão forte que as galáxias, estrelas e até mesmo átomos se desintegram.
* As medições cosmológicas atuais indicam que $\Omega_k\approx 0$, sendo o universo é muito provavelmente plano. 
* Relação entre os parâmetros vistos até aqui:
    * $\Omega_k + \Omega_{EE} + \Omega_m = 1$
* Exemplo:
    * Se $\Omega_k = 0$, $\Omega_{EE} = 0,7$ e $\Omega_m = 0,3$, então o universo é plano e a energia escura é a principal componente, seguida pela matéria.

**5. $\Omega_b$: Densidade de Matéria Bariônica**

* Fração da densidade crítica atribuída à matéria bariônica, composta por prótons e nêutrons.
* É uma fração de $\Omega_m$, com estimativa atual de $\Omega_b = 0,049$.

**6. $\Omega_r$: Densidade de Energia de Radiação**

* Fração da densidade crítica atribuída à energia de radiação, incluindo fótons e neutrinos.
* É um valor que diminui com o tempo devido à expansão do universo.

**7. $w$: Parâmetro da Equação de Estado da Energia Escura**

* Descreve a relação entre a pressão e a densidade da energia escura.
* Um valor de $w = -1$ corresponde à energia escura da constante cosmológica $\Lambda$.
* Valores de $w < -1$ indicam uma energia escura "fantasma" com propriedades exóticas.
* Valores de $w > -1$ sugerem uma energia escura dinâmica com propriedades que variam com o tempo.

**Observação:**

* A notação de Bárbara Ryder pode ser diferente de outras notações da literatura utilizadas em cosmologia.
* É importante consultar as definições específicas utilizadas em cada trabalho para evitar ambiguidades.

## Parte 1 - *A distância em diferentes tipos de Universo*

Vamos, no decorrer desta primeira parte, entender o comportamento da distância de luminosidade $D_L$. Para isso deveremos antes compreender como funciona outros tipos de distâncias como a comóvel $D_C$ e a de Hubble $D_H$. No caso da distância comóvel, como ela é obtida por meio de uma integral, iremos comparar os resultados numéricos em vários casos onde a integral possa ser resolvida analiticamente (e.g. Universo vazio, só de matéria, só de constante cosmológica, etc...). Também iremos mostrar a diferença dos resultados numéricos e analíticos em função do redshift até $z=10$.

> **a)** Para começar, vamos criar uma função que calcule a distância de luminosidade. Para encontrá-la é necessário o cálculo de uma integral numérica. Por isso, vamos definí-la antes de encontrá-la.

Para determinar a distância de luminosidade $D_L$ de acordo como o artigo do Hoog, temos que calcular a seguinte expressão:

$$D_L = (1 + z)D_M$$

onde para $\Omega_k > 0$:

$$ D_M = D_H \dfrac{1}{\sqrt{\Omega_k}}\sinh\left[\dfrac{D_C}{D_H}\sqrt{\Omega_k}\right] $$

e para $\Omega_k = 0$:

$$ D_M = D_C$$

e, por fim, para $\Omega_k < 0$:

$$ D_M = D_H \dfrac{1}{\sqrt{\Omega_k}}\sin\left[\dfrac{D_C}{D_H}\sqrt{\Omega_k}\right] $$
    
sendo $D_H$ é a distância de Hubble 

$$D_H = \dfrac{c}{H_0} $$

e $D_C$ é a distância comóvel na direção da linha de visada 

$$ D_C = D_H \displaystyle\int^{z}_{0} \dfrac{dz'}{E(z')} $$

e 

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
> **b)** Iremos agora, antes de prosseguir na nossa análise, comparar o método análitico e a nossa função para um Universo dominado por $\Omega_{EE}$, ou seja, $\Omega_m = 0$, $\Omega_k = 0$ e $\Omega_{EE} = 1$.

Aplicando as formulas dadas no inicio deste trabalho, encontramos que $D_L$ assumirá a seguinte forma:

$$D_L = \dfrac{cz}{H_0}(1 + z)$$


