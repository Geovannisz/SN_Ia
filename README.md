# Super Novas do Tipo Ia
🚀 Neste projeto encontro analiticamente e numericamente constantes cosmológicas do Universo a partir de um banco de dados do redshift de Super Novas do tipo Ia. Para isso foi usado o Monte Carlo da Cadeia de Markov com o fim de determinar a covariância entre diferentes grandezas e de encontrar a máxima verossimilhança de suas respectivas elipses de incertezas.

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

Esse código imprimiria no terminal:

```
Distância de Luminosidade obtida   = 8571.51 Mpc
Distância de Luminosidade esperada = 8565.50 Mpc
Erro = 0.070 %
```


