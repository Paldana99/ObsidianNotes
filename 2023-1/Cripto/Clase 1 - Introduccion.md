## Cifrado

Si uno quiere enviar un mensaje por un canal publico, donde cualquiera puede tener acceso -> mejor no enviar el mensaje. 
Para esto enviamos un mensaje encriptado, donde Alice envía a Bob el mensaje cifrado (C), y Bob pueda convertirlo en **mensaje** pero Eve no pueda hacerlo. 

![[Pasted image 20230307104135.png]]

Para que esto funcione, B debe conocer un **algoritmo** para obtener M en base a C, pero E no puede saber ese algoritmo. 

Definimos una familia de algoritmos para descifrar. Donde B conoce dentro de la familia cual es el correcto. Para esto necesitamos muchos algoritmos dentro de una familia. Algo como $2^{128}$.

Para reconocerlos fácilmente, los parametrizamos:

![[Pasted image 20230307105014.png]]

Dado k, cualquiera puede obtener el mensaje. Pero A debe ser capaz de cifrar mensajes que lego son descifrable con $Dec_k$
Si A y B comparten k (una llave) es simétrico. Se puede usar asimétrico, para iniciar un canal simétrico y hacerlo mas eficiente.

## Autentificar

Ahora queremos saber que el mensaje fue bien escrito por A y no por E. Para esto se envia un Tag (t) , el cual indica que fue enviado por A y no fue modificado.

Si Eve, no modifica el mensaje entonces t no cambia

![[Pasted image 20230307105804.png]]

Pero si el mensaje esta modificado Bob debe poder saber que el tag y el mensaje no corresponden.

![[Pasted image 20230307105914.png]]


Igual que para el cifrado, utilizamos muchos algoritmos existentes y los parametrizamos.

![[Pasted image 20230307110243.png]]

De esta forma gracias al k y un mensaje vemos si el tag corresponde al enviado. B debe ser capaz  de verificar tag que son generados con MACk

## Principio de Kerckhoffs

> La seguridad de un sistema criptográfico **no** debe depender de que los algoritmos de cifrado y descifrado sean secretos, solo debe depender de que las claves sean secretos.

- Es más fácil mantener el secreto de una clave que de un algoritmo
- Si la seguridad se ve comprometida es más fácil cambiar una clave cambiar una clave que todo un algoritmo
- Es mejor usar algoritmos públicos que hayan sido ampliamente verificados.

## Principios de la criptografía moderna

- Hay que definir formalmente los sistemas criptográficos, y nociones de seguridad usados.
- Los supuestos detrás del funcionamiento, tengan una formulación precisa y sean conocidos.
- Es importante construir **demostraciones formales de seguridad** (basadas en las definiciones y supuestos)
