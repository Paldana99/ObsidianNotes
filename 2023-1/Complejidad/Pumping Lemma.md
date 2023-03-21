> [!note] Nota
> **NO SIRVE** para demostrar que un lenguaje es regular

Si $l$ es un lenguaje regular, entonces $l$ tiene un largo de **bombeo (pumping) P** tal que $\forall$ string $S$ donde $\mid S\mid \geq \mid P\mid$ se puede dividir en 3 partes $S=xyz$ de modo que las siguientes condiciones son verdaderas:
1. $xy^{i}z\in\mathcal{L} \quad \forall i\geq 0$
2. $\mid y\mid>0$
3. $\mid xy\mid\leq P$

## Como usarlo -> Por contradicción

1. Asumimos que $\mathcal{L}$ es regular
2. Tiene un largo de Bombo $P$
3. Todo string mas largo $P$ puede ser bombeado
4. Encontramos $S$
5. Dividimos en $xyz$
6. Mostramos que $xy^{i}z \not\in \mathcal{L}$ para algún i
7. Tomamos todas las formas posibles de div $S$
8. Mostramos que no se pueden cumplir las 3 condiciones al mismo tiempo -> contradicción