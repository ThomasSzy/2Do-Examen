#Segundo Parcial

![LOGO TINKERCAD](https://i.ibb.co/K08W9N9/Arduino-Tinkercad.jpg)

## Nombre y Apellido:
* Thomas Szymuda


## Primer Parcial Imagen

![IMAGEN DEL PROYECTO](https://i.im.ge/2023/06/26/02xHyP.Thomas-Szymuda-2do-Examen.png)

## DESCRIPCIÓN

Este parcial trata sobre un alerta de incendios <br/>
Tambien tiene unos leds de emerjencias agregados al momento de detectar mucha temperatura<br/>

## FUNCIÓN PRINCIPAL

La función principal se encarga de detectar las temperaturas y decir en que estapa del año se encuentra<br/>
Tambien tiene unos leds los cuales titilan en alerta si detectan mucha temperatura, y dice alerta en el LCD <br/>
Luego tenemos un servo que gira al momento de detectar temperatura alta<br/>
//Thomas Szymuda 1D
//Segundo Parcial
void loop()
{
  if (prendido_apagado)
  {
    int lectura_sensor = analogRead(sensor_temperatura);
    //Temperatura a numero entero
    float temperatura_ambiente = (lectura_sensor * 5.0 / 1024.0 - 0.5) * 100.0;
	
    //Configuracion del lcd columna x fila y printeo de temperatura
    lcd.setCursor(0, 0);
    lcd.print("Temperatura: ");
    lcd.print(temperatura_ambiente);
    delay(500);

    //Estaciones
    detectar_estacion(temperatura_ambiente);

    //Temperatura
    if (temperatura_ambiente > 60)
    {
      mover_servo();
      ALERTA(led_roja,led_amarilla);
    }
    else
    {
      frenar_servo();
    }
	//Funcionalidad al precionar boton
    if (IrReceiver.decode()) 
    {
      Serial.println(IrReceiver.decodedIRData.decodedRawData, HEX);
      IrReceiver.resume();
      switch (IrReceiver.decodedIRData.decodedRawData)
      {
        //Numero de pin presionado pasado a numero
        case 4278238976:
          prendido_apagado = false;
        //Inicializamos el LCD sin texto
          lcd.setCursor(0, 0);
          lcd.print("                ");
          lcd.setCursor(0, 1);
          lcd.print("                ");
          break;
      }
      delay(50);
      //Reanuda Señales
      irrecv.resume();
    }
  }
  else
  {
    if (IrReceiver.decode()) 
    {
        Serial.println(IrReceiver.decodedIRData.decodedRawData, HEX);
        IrReceiver.resume();
        switch (IrReceiver.decodedIRData.decodedRawData)
        {
            case 4278238976:
              prendido_apagado = true;
              break;
        }
        delay(50);
        irrecv.resume();
    }
  }
}


## LINK AL PROYECTO

* [proyecto](https://www.tinkercad.com/things/3OqKFXLHK63-neat-migelo-tumelo/editel?sharecode=35iUkX6Nvwl1Q3nP32ijyF-pohKsQrJKgRG5jeW5BJY)
