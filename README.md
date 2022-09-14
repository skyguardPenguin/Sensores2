
# Sensores

## NLSF595 SPI Tri-Color LED Driver
![image](https://user-images.githubusercontent.com/44510625/190011100-4909f3a7-1a49-4abb-a50b-5dd43e50017a.png)

Sirve para conectar LED RGB que consumen mucha energía a su microcontrolador. Una sola unidad puede controlar dos LED RGB, y una cadena de dos unidades puede controlar hasta cinco LED RGB.

**Distribución de pines**


![image](https://user-images.githubusercontent.com/44510625/190014335-3ead1590-12e0-4d67-97f9-0e85f03a0d2f.png)



**Funcionalidad de pines**

| Pin     | Description                                           |
|---------|-------------------------------------------------------|
| SI      | Serial Input                                          |
| RCK     | Storage (latch) pin                                   |
| OE      | Output enable, active low. Connect to GND if not used |
| QA...QH | Parallel output                                       |
| SQH     | Serial output*                                        |
| SCLR    | Reset(clear), active low. Connect to VCC if not used  |
| GND     | Ground                                                |
| VCC     | Supply voltage                                        |

## Photoresistor (LDR) Sensor

![image](https://user-images.githubusercontent.com/44510625/190018879-b3f6fd18-5487-4093-b091-eec62ccbbd7e.png)


Un fotorresistor o fotorresistencia es un componente electrónico cuya resistencia se modifica, con el aumento de intensidad de luz incidente. Puede también ser llamado fotoconductor, célula fotoeléctrica o resistor dependiente de la luz, cuyas siglas, LDR, se originan de su nombre en inglés light-dependent resistor. Su cuerpo está formado por una célula fotorreceptora y dos patillas. En la siguiente imagen se muestra su símbolo eléctrico.

**¿Qué es la fotoresistencia o LDR?**

El LDR por sus siglas en inglés (Light Dependent Resistor) o fotoresistor es una resistencia eléctrica la cual varía su valor en función de la cantidad de luz que incide sobre su superficie. Cuanto mayor sea la intensidad de luz que incide en la superficie del LDR o fotoresistor menor será su resistencia y en cuanto menor sea la luz que incida sobre éste mayor será su resistencia.

**¿Cómo funciona una LDR o fotoresistencia?**

Cuando el LDR(fotoresistor) no está expuesto a radiaciones luminosas, los electrones están firmemente unidos en los átomos que lo conforman, pero cuando sobre él inciden radiaciones luminosas, esta energía libera electrones con lo cual el material se hace más conductor, y de esta manera disminuye su resistencia. Las resistencias LDR solamente reducen su resistencia con una radiación luminosa situada dentro de una determinada banda de longitudes de onda.
