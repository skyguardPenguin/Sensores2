
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

**Código**

***code.py***
```
import time
import board
import digitalio
import shiftOut

data = digitalio.DigitalInOut(board.GP21)
clock = digitalio.DigitalInOut(board.GP28)
latch = digitalio.DigitalInOut(board.GP26)

clock.direction = digitalio.Direction.OUTPUT
latch.direction = digitalio.Direction.OUTPUT
data.direction = digitalio.Direction.OUTPUT



while(True):
    shiftOut.shiftOut(data,clock,latch,1,0)
    time.sleep(.5)
    shiftOut.shiftOut(data,clock,latch,1,1)
    time.sleep(.5)    
    shiftOut.shiftOut(data,clock,latch,1,2)
    time.sleep(.5)

```
***shiftOut.py***
```
#función extraída de: https://github.com/grampastever/shiftout

def shiftOut(dataPin, clockPin, latchPin, bitOrder, val):
    #bit map of digital number to 7-seg display pinout where the bit order is 'abcdefgh'
    #which also maps to the output pins of the 74HC595 as 'QaQbQcQdQeQfQgQh'
    bit_map = ['11011011', '10110111', '01001011']
    
    #convert the digital val to a corresponding binary string representation of that
    #number as it applies to the 7-segment display
    bin_num = bit_map[val]
    
#shift out per the pre-selected bit order
        
    if bitOrder == 0:  #MSB first
     
        #shift out bin_num MSB first
        for i in range(0, 8):
            a = bin_num[i:i+1]

            #"typecast" string value to integer
            if a == '0':
                dataPin.value= False
            elif a == '1':
                dataPin.value =True
            
            clockPin.value =False
            clockPin.value= True
            
        #display data from the serial register of the74HC595
        latchPin.value= True 
        latch.value= False

    elif bitOrder == 1: #LSB first
    
        #shift out bin_num LSB first
        for i in range(8, 0, -1):
            a = bin_num[i-1:i]
            
            if a == '0':
                dataPin.value = False
            elif a == '1':
                dataPin.value = True
                
            clockPin.value = True
            clockPin.value = False
    
        #display data from the serial register of the74HC595
        latchPin.value = True
        latchPin.value = False
    
    else:
        
        #trap bit order error
        print("Bit order error. Must be either 0 = MSB first or 1 = LSB first")
        print("press cntl-c to end")
        while True:
            a = 0  #just a useless variable assignement to keep the while loop going
```

**Ejemplo**

![image](https://i.imgur.com/yZdZAsf.gif)
## Photoresistor (LDR) Sensor

![image](https://user-images.githubusercontent.com/44510625/190018879-b3f6fd18-5487-4093-b091-eec62ccbbd7e.png)



Un fotorresistor o fotorresistencia es un componente electrónico cuya resistencia se modifica, con el aumento de intensidad de luz incidente. Puede también ser llamado fotoconductor, célula fotoeléctrica o resistor dependiente de la luz, cuyas siglas, LDR, se originan de su nombre en inglés light-dependent resistor. Su cuerpo está formado por una célula fotorreceptora y dos patillas. En la siguiente imagen se muestra su símbolo eléctrico.

**¿Qué es la fotoresistencia o LDR?**

El LDR por sus siglas en inglés (Light Dependent Resistor) o fotoresistor es una resistencia eléctrica la cual varía su valor en función de la cantidad de luz que incide sobre su superficie. Cuanto mayor sea la intensidad de luz que incide en la superficie del LDR o fotoresistor menor será su resistencia y en cuanto menor sea la luz que incida sobre éste mayor será su resistencia.

**¿Cómo funciona una LDR o fotoresistencia?**

Cuando el LDR(fotoresistor) no está expuesto a radiaciones luminosas, los electrones están firmemente unidos en los átomos que lo conforman, pero cuando sobre él inciden radiaciones luminosas, esta energía libera electrones con lo cual el material se hace más conductor, y de esta manera disminuye su resistencia. Las resistencias LDR solamente reducen su resistencia con una radiación luminosa situada dentro de una determinada banda de longitudes de onda.


**Código**
```
import time
import board
import analogio

GAMMA = 0.7
RL10 = 50

photoresistor = analogio.AnalogIn(board.GP26)

while True:
    analogValue = photoresistor.value/(65536/1024)

    voltage = analogValue / 1024. * 5
    resistance = 2000 * voltage / (1 - voltage / 5)
    lux = pow(RL10 * 1e3 * pow(10, GAMMA) / resistance, (1 / GAMMA))
    print(round(lux,1))
    time.sleep(2)
```

![image](https://i.imgur.com/HINIPJ3.gif)
