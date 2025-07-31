
# Laboratorio MinRank: Ataque a un "Rainbow" Reducido

Este laboratorio está enfocado en el criptoanálisis y explotación de un esquema de firma multivariada simplificado (Rainbow reducido) utilizando un ataque **MinRank** sobre $\mathbb{F}_2$. A lo largo del ejercicio, se construye el esquema vulnerable y se demuestra cómo comprometer su integridad mediante la falsificación de firmas válidas.

---

## 🧬 ¿Qué es un esquema de firma Rainbow?

Rainbow es un esquema de firma post-cuántico multivariado basado en el problema de resolver sistemas de polinomios cuadráticos sobre campos finitos, típicamente $\mathbb{F}_2$. La idea básica se apoya en la dificultad de resolver sistemas de ecuaciones cuadráticas multivariadas (**MQ Problem**), considerado NP-difícil incluso para computadoras cuánticas.

---

## 🔐 ¿Por qué es vulnerable?

La clave pública de Rainbow expone polinomios cuadráticos que cumplen una estructura especial: están construidos a partir de una matriz central cuya combinación lineal puede tener rango reducido. Esto permite aplicar un **ataque MinRank**, que busca una combinación de matrices cuadráticas tal que su rango sea menor o igual a un umbral definido.

El atacante busca una combinación:

$$
C = \sum_{i=1}^{m} \alpha_i M_i \quad \text{con } \operatorname{rank}(C) \leq r
$$

Donde cada $M_i$ es una matriz cuadrática que representa un polinomio de la clave pública.

Una vez encontrada esta combinación, se pueden falsificar firmas resolviendo:

$$
P_i(x) = 0 \quad \forall i \in [1, m]
$$


---

# 📁 Estructura del proyecto

```
minrank-lab/
├── lab.py                     <- Generación de instancia vulnerable
├── attack/
│   ├── reconstructor.py       <- Carga y reconstrucción de polinomios públicos
│   ├── forge_signature.py     <- Falsificación de firma
│   └── verify_signature.py    <- Verificación de firma
├── keys/
│   ├── rainbow_public_key.pkl <- Clave pública serializada
│   └── forged/                <- Firma falsificada
│       └── forged_signature.pkl
```

---

# 🧪 Pasos del laboratorio

### 1. Generar una instancia vulnerable
Ejecuta el script principal que genera la clave pública y realiza el ataque MinRank:

```
sage lab.py
```

Esto guardará los polinomios y la solución MinRank en el directorio `keys/` y `attack/output/`.

### 2. Falsificar la firma

Usamos la solución obtenida para buscar una firma válida que anule todos los polinomios:

```
sage attack/forge_signature.py
```

Se guardará un archivo en `keys/forged/forged_signature.pkl`.

### 3. Verificar la firma

Comprueba si la firma falsificada es válida:

```
sage attack/verify_signature.py
```

---

# 📌 Créditos

Desarrollado por Mauro Carrillo (@Pr00fOf3xpl0it) como parte de sus laboratorios avanzados de criptoanálisis post-cuántico ofensivo.