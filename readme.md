# Descripción

Este proyecto simula una alarma de incendios atraves del uso de distintos componentes electronicos los cuales son : un servomotor,lcd 16x2,sensor tmp,control remoto y sensor IR.
El sensor tmp es el encargado de medir la temperatura y pasarle estos parametros a los demas componentes para que definan su funcionamiento.

## Proyecto : Alarma de incendio.


![visual](img\alarmaArduino.png)
## Funciones principales.


### "DeterminarEstacion"
Recibe un parametro de tipo float y en base a un rango de este mismo devuelve un str con las estaciones del año.

```C++
String determinarEstacion(float temperatura)
{
  if (temperatura >= 22.0 && temperatura <= 59.0)
  {
    return "Verano";
  }
  else if (temperatura >= 15.0 && temperatura < 22.0)
  {
    return "Otonio";
  }
  else if (temperatura >= 5.0 && temperatura < 15.0)
  {
    return "Primavera";
  }
  else if (temperatura >= -40.0 && temperatura < 5.0)
  {
    return "Invierno";
  }
  else if (temperatura > 70.0 && temperatura <= 125.0)
  {
    return "ALARMA";
  }

  return "";
}
```

### "activarServo"
Es el encargado de evaluar la temperatura y activar el servo en caso de que cumpla las condiciones establecidas.
Ademas printea en el LCD si la alarma esta desactivada.
```C++
void activarServo(float temperatura,bool boton)
{
  if (temperatura >= 60.0 && boton == false )
  {
    prenderServo();
    parpadeoLedRojo();
    digitalWrite(LED_VERDE,LOW);
  }
  else if (temperatura >= 60.0 && boton == true)
  {
    lcd.setCursor(0,1);
    servo1.write(0);
    digitalWrite(LED_ROJO,LOW);
    digitalWrite(LED_VERDE,HIGH);
    
    lcd.print("Alarma Off");
  }
}
```

### "prendeServo()"

Esta funcion es la que activa el servo,printea en el LCD si la alarma esta activa y le da el angulo de rotacion al mismo.
```C++
void prenderServo(){
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("ALARMA ACTIVADA");
    for (int angulo = 0; angulo <= 180; angulo++) {
      servo1.write(angulo);  
      delay(15);  
    }
    for (int angulo = 180; angulo >= 0; angulo--) {
      servo1.write(angulo);  
      delay(15);  
  }
}
```

### "parpadeoLedRojo()"
Se encarga de prender y apagar un led en un ritmo especifico.
```C++
void parpadeoLedRojo()
{
  digitalWrite(LED_ROJO, HIGH);  
  delay(500);                  
  digitalWrite(LED_ROJO, LOW);   
  delay(500);   
} 
```
## Link al proyecto 🤗.
* [Alarma de incendio ⏰](https://www.tinkercad.com/things/iD6aWTVq75a-juanas-martin-adrian-2do-parcial-practico-spd/editel?sharecode=_wAGJURQDfbk7mEMUJhGgWImyC0HZlg79BOtmoUX8Y4)


## Fuentes utilizadas📚.
* [Tutorial de Markdown](https://www.youtube.com/watch?v=oxaH9CFpeEE&t=205s)

* [Guia Servomotor](https://naylampmechatronics.com/blog/33_tutorial-uso-de-servomotores-con-arduino.html)

* [Uso de control remoto y sensor IR](https://www.youtube.com/watch?v=gPmsGyOuowI&t=1279s)

* [Uso de LCD 16x2](https://www.youtube.com/watch?v=JEZiHQY-JPI)
