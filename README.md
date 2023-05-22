# __PROYECTO: MONTACARGA__


![Alt text](../Img/Captura%20de%20pantalla%202023-05-21%20a%20la(s)%2020.10.34.png)
![Alt text](../Img/Captura%20de%20pantalla%202023-05-21%20a%20la(s)%2021.23.24.png)


## __Funcionalidad__. 

El montacargas posee 3 pulsadores, uno para subir, uno para bajar y otro para parar, un segmento display de 7 leds, un led rojor y un led verde. El montacargas subira hasta el ultimo piso, numero 9 en este caso (indicado por el dispplay 7 segmentos), una vez arriba podra bajar gasta el piso numero 0, o planta baja. El montacarga parara en cualquiera de estos pisos segun lo indique el usuario oprimiendo el boton de parar. Los leds verde y rojo indicaran si el ascensor se encuentra en movimiento o este se encuetra parado encendiendo la luz verde si se encuentra en movimiento y la roja si esta parado.

###  __Alumno:__
- Joaquin Quiroga

## __Funciones__
El proyecto posee 7 funciones importantes.

1. __Funcion `validarContador`__

Esta función toma un parámetro `contador` y devuelve un valor entero para indicar si el `contador` es par o impar.

```
int validarContador(int contador)
{
  if(contador % 2 == 0)
  {
    return 1;
  }
  else
  {
    return 0;
  }
}
```
__La función devuelve un entero:__
- `1` si el `contador` es par.
- `0` si el `contador` es impar.

__Parametros.__
- `contador`: Un número entero que se desea validar.


2. __Funcion `validarCambioDeEstado`__

Esta función toma tres parámetros: `estado`, `siguienteEstado` y `contadorDeCambio`. Comprueba si el estado actual es diferente al siguiente estado y si el estado actual es `LOW`. En caso afirmativo, incrementa el valor del `contadorDeCambio` en 1 y lo devuelve.

```
int validarCambioDeEstado(int estado, int siguienteEstado, int contadorDeCambio)
{
  if (estado != siguienteEstado && estado == LOW)
  {
    contadorDeCambio += 1;
  }
  
  return contadorDeCambio;
}
```
__Valor de retorno.__

- La función devuelve un entero que representa el nuevo valor de `contadorDeCambio`.


__Parametros.__

- `estado`: Un número entero que representa el estado actual.

- `siguienteEstado`: Un número entero que representa el siguiente estado.

- `contadorDeCambio`: Un número entero que registra el número de cambios de estado.

3. __Funcion `subirPiso_bajarPiso`__

Esta función toma varios parámetros: `piso`, `a`, `b`, `c`, `d`, `e`, `f`, `g` y `subir_bajar`. Dependiendo del valor de `subir_bajar`, incrementa o decrementa el valor de `piso`. Luego, invoca la función `contadorSegmento` con el nuevo valor de `piso`, imprime el valor actual de `piso` en la salida serial y finalmente devuelve el nuevo valor de `piso`.

```
int subirPiso_bajarPiso(int piso,int a, int b,int c,int d,int e,int f,int g,int subir_bajar)
{
  if(subir_bajar == 1)
  {
    piso++;
  }
  else
  {
    piso--;
  }
  
  contadorSegmento(piso,A,B,C,D,E,F,G);
  Serial.print("Piso:");
  Serial.println(piso);
  
  return piso;
}
```

__Valor de retorno.__
- La función devuelve un entero que representa el nuevo valor de `piso`.

__Parametros.__

- `piso`: Un número entero que representa el piso actual.
- `a`, `b`, `c`, `d`, `e`, `f`, `g`: Parámetros adicionales que no se utilizan en esta función, pero se pasan a la función `contadorSegmento`.
- `subir_bajar`: Un número entero que indica si se debe subir o bajar de piso. 
  - Si `subir_bajar` es igual a `1`, se incrementa el valor de `piso`.
  - Si `subir_bajar` es diferente de `1`, se decrementa el valor de `piso`.


4. __Funcion `contadorSegmento`__

Esta función toma varios parámetros: `numero`, `a`, `b`, `c`, `d`, `e`, `f`, `g`. Dependiendo del valor de `numero`, se encienden los segmentos deseados en base a un conjunto de reglas. La función `encenderSegmentosDeseados` se invoca con los parámetros `a`, `b`, `c`, `d`, `e`, `f`, `g` junto con los valores correspondientes para encender los segmentos específicos.
La funcion no retorna nada.


```
void contadorSegmento(int numero,int a,int b,int c,int d,int e,int f,int g)
{
  switch(numero)
  {
    case 0:
    	encenderSegmentosDeseados(a,b,c,d,e,f,g,1,1,1,1,1,0,1);
   	  break;
    case 1:
    	encenderSegmentosDeseados(a,b,c,d,e,f,g,0,1,1,0,0,0,0);
   	  break;
    case 2:
    	encenderSegmentosDeseados(a,b,c,d,e,f,g,1, 1, 0, 1, 1, 1, 0);
      break;
    case 3:
   	 	encenderSegmentosDeseados(a,b,c,d,e,f,g,1, 1, 1, 1, 0, 1, 0);
      break;
    case 4:
    	encenderSegmentosDeseados(a,b,c,d,e,f,g,0, 1, 1, 0, 0, 1, 1);
      break;
    case 5:
    	encenderSegmentosDeseados(a,b,c,d,e,f,g,1, 0, 1, 1, 0, 1, 1);
      break;
    case 6:
    	encenderSegmentosDeseados(a,b,c,d,e,f,g,1, 0, 1, 1, 1, 1, 1);
      break;
    case 7:
    	encenderSegmentosDeseados(a,b,c,d,e,f,g,1, 1, 1, 0, 0, 0, 0);
      break;
    case 8:
    	encenderSegmentosDeseados(a,b,c,d,e,f,g,1, 1, 1, 1, 1, 1, 1);
      break;
    case 9:
    	encenderSegmentosDeseados(a,b,c,d,e,f,g,1, 1, 1, 1, 0, 1, 1);
      break;
  } 
}
```
__Parametros.__
- `numero`: Un número entero que representa el dígito para el cual se desean encender los segmentos.
- `a`, `b`, `c`, `d`, `e`, `f`, `g`: Parámetros adicionales que se pasan a la función `encenderSegmentosDeseados`.

5. __Funcion `encenderSegmentosDeseados`__

Esta función toma varios parámetros: `a`, `b`, `c`, `d`, `e`, `f`, `g`, `prender_a`, `prender_b`, `prender_c`, `prender_d`, `prender_e`, `prender_f`, `prender_g`. Utiliza los valores de los parámetros para encender o apagar los segmentos correspondientes en un arreglo de LEDs.
```
void encenderSegmentosDeseados(int a,int b,int c,int d,int e, int f,int g,int prender_a,int prender_b,int prender_c,int prender_d,int prender_e,int prender_f,int prender_g)
{ 
  int arrayLed[] = {a,b,c,d,e,f,g};
  int arrayEstadoLed[] = {prender_a,prender_b,prender_c,prender_d,prender_e,prender_f,prender_g};
 
  for(int i = 0; i<7;i++)
  {
    digitalWrite(arrayLed[i],arrayEstadoLed[i]);
  }
  
}
```
__Funcionamiento.__

La función crea dos arreglos: `arrayLed` y `arrayEstadoLed`. `arrayLed` contiene los valores de los pines o controladores de los LEDs correspondientes a los segmentos, mientras que `arrayEstadoLed` contiene los valores para encender o apagar los segmentos específicos.

Luego, se recorre un bucle `for` que itera sobre los elementos de los arreglos `arrayLed` y `arrayEstadoLed`. En cada iteración, se utiliza la función `digitalWrite` para encender o apagar el LED correspondiente según el estado indicado en `arrayEstadoLed`.

__Parametros.__
- `a`, `b`, `c`, `d`, `e`, `f`, `g`: Parámetros que representan los pines o controladores de los LEDs correspondientes a los segmentos del display.
- `prender_a`, `prender_b`, `prender_c`, `prender_d`, `prender_e`, `prender_f`, `prender_g`: Parámetros booleanos que indican si se debe encender (`1`) o apagar (`0`) cada segmento respectivamente.

6. __Funcion `encenderLed`__

Esta función toma un parámetro `led`, que representa el pin o controlador del LED que se desea encender.
```
void encenderLed(int led)
{
  digitalWrite(led, HIGH);
}
```
__Parametros.__
- `led`: Un número entero que representa el pin o controlador del LED que se desea encender.

__Funcionalidad.__

La función utiliza la función `digitalWrite` para establecer el estado del pin `led` como `HIGH`, lo que enciende el LED conectado a ese pin.

7. __Funcion `apagarLed`__

Esta función toma un parámetro `led`, que representa el pin o controlador del LED que se desea apagar.
```
void apagarLed(int led)
{
  digitalWrite(led, LOW);
}
```

__Parametros.__
- `led`: Un número entero que representa el pin o controlador del LED que se desea apagar.

__Funcionalidad.__

La función utiliza la función `digitalWrite` para establecer el estado del pin `led` como `LOW`, lo que apaga el LED conectado a ese pin.




##  __Componentes__.

- 2 Leds.
- 3 Pulsadores.
- 1 Display de 7 segmentos.
