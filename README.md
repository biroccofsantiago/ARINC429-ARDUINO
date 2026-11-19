# Firmware Arduino ARINC 429

Este sketch está adaptado al formato de `ARINC429-Completo`.

## Comunicación y validaciones

- Serie a **9600 baudios**; recibe ocho dígitos hexadecimales ASCII por línea,
  terminados en `\n` (por ejemplo, `1234ABCD`).
- Verifica longitud y caracteres hexadecimales, paridad impar, etiqueta
  registrada y límites del instrumento.
- Interpreta el dato como BNR firmado de 19 bits y lo multiplica por la
  resolución configurada.
- Presenta instrumento, valor y unidad en un LCD 16x2 I²C.
- Emite cada palabra MSB primero: pulso HIGH de 5 ms en D13 para un bit 1, o
  en D12 para un bit 0; luego ambas salidas quedan LOW.

## Configuración incluida

El ejemplo del proyecto define **Altitud**, etiqueta octal `203`, resolución
`0.5`, rango de `-1000` a `20000 ft`. La tabla `instruments[]` del sketch debe
coincidir con los instrumentos configurados en la aplicación.

## Hardware y carga

Sketch: `ARINC429_Arduino.ino`. Placa tipo Uno/Nano, LCD I²C 16x2 en dirección
`0x27`, biblioteca `LiquidCrystal_I2C`. En Arduino IDE seleccioná la placa y
el puerto serie correspondiente antes de cargarlo.

D12 y D13 son salidas lógicas de demostración; no son una interfaz eléctrica
ARINC 429. Para conectarlas a un bus real se necesita el transceptor adecuado.
