Bitcoin: A Peer-to-Peer Electronic Cash System

Uso de Block Chain para compartir la informacion. 

Toda la plata es una cadena originada en la Trabasaccion 1. Una transaccion puede tener tantos inputs y outputs como queramos. Los outputs siempre se gastan completos.

Se crea un bloque firmado con todas las transacciones validas. Si se quiere enviar una transaccion se envia a los nodos vecinos, si se recibe una igual (se propaga la informacion en la red)

Se forma un bloque con las transacciones y luego se propaga. Al recibir un nuevo bloque se verifica correcto y se propaga.

El bloque generado se considera valido si el hash parte con 20 0's. 
![[Pasted image 20230703152555.png]]


Si hay dos bloques generado al mismo tiempo, se trabaja en ambos, y luego se selecciona el con cadena mas larga.

## Bloque

![[Pasted image 20230703152806.png]]

### Header:
![[Pasted image 20230703152828.png]]

Ocupamos arboles de Merkle para verificar que una transaccion es parte de un bloque.

### Transacciones

