# Supresión de sonido
#### Glosario
- Buddeado: Que esta encendido cuando debería estar apagado
- CCE box: Una caja de shulker que reemplaza un atril
- Crash: Interrupción inesperada del juego.
- Kick: Expulsar a un jugador de un servidor
- Setup: conjunto de componentes y su disposición para un propósito específico.
- shadow items: hacer shadow items es tener un objeto enlazado a dos espacios distintos de inventario
- Tile entity: Bloque que almacena  información, como un cofre, una shulker o un sensor de sculk.

## Abstracto
La supresión de sonido es un nuevo tipo de supresión como OOM (Out Of Memory), ClastCast (Supresión de shulker) y SackOverflow (Supresión anterior a 1.18) que usa la técnica del cambio de tile entity para crear un tile entity en un estado ilegal que se puede usar para la supresión.
#### Créditos:
- Descubridores originales
    - JKM
    - Metacinabar
- Hacer una versión mas utilizable
    - Igna778
- Personas de Investigación y Desarrollo
    - Lame
    - Savva
    - Void
    - Ruthro
```ad-help
title: ¿Necesitas ayuda?
Video de la supresion de sonido: https://youtu.be/77M8Adnxmsw?si=f-hon2OtKevtEUhx

Canal Youtube:https://youtube.com/@igna778
Comunidad de Discord: https://discord.gg/rsuTZer7RT
```
## En el lado práctico
La mayor aplicación practica para este método es convertirse en un peligro de crasheo si se usa de forma incorrecta, así que siempre tiene que ser tratado con precaución.
### El setup
#### Construcción
Consiste en un sculk calibrado conectado a un supresor y un observador con un block de notas y una puerta adyacente a la alfombra puesta encima del sensor de sculk. Todo está configurado de la siguiente manera:

```ad-warning
title: Estado de la puerta
Es importante resaltar que en el setup de aqui la puerta esta en estado de apagado y debe estar puesto exactamente asi
```

  

![[Pasted image 20240806104831.png|350]]

  

![[Pasted image 20240806105705.png|350]]

  

La línea de railes mostrada, la cual es una línea de railes buddeada debe estar conectada a un supresor de actualizaciones, el cual si estas en la 1.20 y tienes una CCE Box deberías usar eso para el setup, de otra manera tu tendrías que ir con el setup de OOM mas reciente (en este momento la Supresión de bolas de nieve (snowball supresión))

```ad-info
title: 1.19
La supresion de sonido en 1.19 no es realmente estable, a que no hay manera de controlar los canales de sonidos, deberias de intentar conseguir una CCE box y despues actualizarlo cuando estes en la 1.20

```
### Usarlo
Para usar el setup solo tienes que estar enfrente del la puerta mientras se abre y se cierra e intentar romper la parte de abajo de la puerta con una azada de diamante, cuando se abra, instantáneamente romperás el sensor de sculk calibrado y activaras la supresión.

Después de eso reemplaza la puerta con un comparador y pon un atril  **con un libro que tenga 15 paginas**

![[Pasted image 20240806105705.png|350]]

![[Pasted image 20240806111136.png|350]]

```ad-tip
title: consejo

Whait a few minutes until you are sure the server has finish processing the suppresion. Especialy if you are using OOM.

Espera unos minutos hasta que estes seguro de que el servidor ha terminado de procesar la supresion. Especialmente si estas usando OOM (Out Of Memory)

```

```ad-danger
title: Extrema precaucion en el siguiente paso

Si el siguiente paso se hace de manera incorrecta podrias crashear constantemente el juego. ¡¡TEN CUIDADO!!

```
Coge un cofre y mira al comparador, así te aseguras de que la parte de atrás es activada por el comparador. Pon el cofre donde estaba el sensor de sculk calibrado.

![[Pasted image 20240806111756.png]]
### Romperlo
```ad-danger
title: Extrema precaucion en el siguiente paso

Si el siguiente paso se hace de manera incorrecta podrias crashear constantemente el juego. ¡¡TEN CUIDADO!!

```

Si planeas no volver a usar el setup rompe el cofre antes que cualquier otro componente. **Romper el comparador o el atril hará que probablemente crashes constantemente tu juego**.
## Canales de sonido
La supresión de sonido tiene 15 canales de sonido pero Solo he encontrado útiles los siguientes, si encuentras algo mas y consideras que este documento debería de ser actualizado por favor, contacta a Igna778 por discord
```ad-warning
title: Acciones que no son del jugador

Recuerda que las acciones que no son del jugador podrian crashear el server, cosas como usar cohetes o creepers explotando podrian apagar el server
```
##### 1 Movimiento en cualquier forma
- exploit de kickeo
    - Kickea cualquier jugador que haga sonido mientras se mueva
##### 4 Planear con elytras o interacciones unicas de mob
- **Kickeo por volar**
    - Si vuelas con elytras serás kickeado
- **Shadow Items**
    - Puedes crear shadow items con soportes de armaduras si tiene manos
##### 5 Desmontar un mob o equiparse
- **Shadow Items**
    -Puedes crear shadow items de objetos de armadura
##### 7 Mobs y jugadores siendo dañados
- **Cancelación de animación de daño**
    - Cancela la animación de daño
##### 9 Bloques 'desactivándose'
- **Puede ser usado para crear pequeñas supresiones**
    - Usando bloques de notas o trampillas tu puedes crear un supresor normal.
##### 10 Bloques 'activándose'
- **Puede ser usado para crear pequeñas supresiones**
    - Usando bloques de notas o trampillas tu puedes crear un supresor normal.
##### 12 Bloques siendo destruidos menos la lana
- **Bloques indestructibles**
    - Indestructible Hace que cualquier bloque en rango (excepto la lana y bloques que se rompen de manera custom como la puertas)
##### 13 Poner bloques
- **Duplicación**
    - Puedes duplicar cualquier bloque que pongas

```ad-note
title: Otros canales
Almenos lo que he encontrado incialmente los otros canales solo kickean / crashean el servidor, otros pueden ser utiles en situaciones muy especificas pero no van a ser registradas en este documente
```
## Dentro del código

```ad-info
title: Mapeo de codigo

Todos los caminos de código, clases, métodos y otros nombres se toman de los mapeos de Yarn del juego.
```

Este exploit es posible gracias a la parte `blockstate` de obtener una propiedad que no existe en el `blockstate`. Las clases relevantes para este exploit son: `CalibratedSculkSensorBlockEntity`, `State` y `Vibrations`.
#### Jerarquía de llamadas
Cuando se crea un evento del juego (vibración), el juego busca escuchadores para transmitir esa información. En este caso, el `CalibratedSculkSensorBlockEntity` es uno de esos escuchas y se ejecuta el código que determina si el evento del juego (vibración) debe ser aceptado.

```java

    public boolean listen(ServerWorld world, RegistryEntry<GameEvent> event, GameEvent.Emitter emitter, Vec3d emitterPos) {  

    ListenerData listenerData = this.receiver.getVibrationListenerData();  

    Callback callback = this.receiver.getVibrationCallback();  

    if (listenerData.getVibration() != null) {  

        return false;  

    }  

    if (!callback.canAccept(event, emitter)) {  

        return false;  

    }  

    Optional<Vec3d> optional = callback.getPositionSource().getPos(world);  

    if (optional.isEmpty()) {  

        return false;  

    }  

    Vec3d vec3d = optional.get();  

    if (!callback.accepts(world, BlockPos.ofFloored(emitterPos), event, emitter)) {  

        return false;  

    }  

    if (VibrationListener.isOccluded(world, emitterPos, vec3d)) {  

        return false;  

    }  

    this.listen(world, listenerData, event, emitter, emitterPos, vec3d);  

    return true;}

```

La primera llamada `accepts` es donde el crasheo sucede.

```java

public boolean accepts(ServerWorld world, BlockPos pos, RegistryEntry<GameEvent> event, @Nullable GameEvent.Emitter emitter) {  

    int i = this.getCalibrationFrequency(world, this.pos, CalibratedSculkSensorBlockEntity.this.getCachedState());  

    if (i != 0 && Vibrations.getFrequency(event) != i) {  

        return false;  

    }  

    return super.accepts(world, pos, event, emitter);  

}

```

Si el `blockstate` no tiene una propiedad de dirección, se producirá un crash en el `getCalibrationFrequency` antes de realizar la verificación del canal de vibración; de lo contrario, verificará si la vibración corresponde a la frecuencia establecida por la energía de Redstone y, si es así, más tarde se producirá un crash en la parte `super.accepts` del código
## Crédito del documento
Gracias a todos los que han contribuido a este documento
#### Creador
- Igna778
#### Colaboradores
- krispyking24
- infernal
- rca
