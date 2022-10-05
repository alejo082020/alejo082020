import machine,esp32,time
from machine import Pin
T0 = machine.TouchPad(machine.Pin(4))
T0.config(600)
T1 = machine.TouchPad(machine.Pin(15))
T1.config(600)
led1 =Pin(23,Pin.OUT)
led2 =Pin(21,Pin.OUT)

def touch1():
    if T0.read()<90:
       led2.value(1)
    else:
       led2.value(0)
def touch2():
    if T1.read()<90:
       led1.value(1)
    else:
       led1.value(0)
while True:
    touch1 ()
    print("touch 1: ",T1.read())
    touch2 ()
    print("touch 2: ",T0.read())
    time.sleep(0.2)
    
from machine import Pin, ADC, PWM
from utime import sleep_ms

def mapear(valor_sensor, minimo_entrada, maximo_entrada, minimo_salida, maximo_salida):
  valor_mapeado = (valor_sensor - minimo_entrada) * (maximo_salida - minimo_salida) / (maximo_entrada - minimo_entrada) + minimo_salida
  return valor_mapeado
#--------------------------- [OBJETOS]---------------------------------------
bombillor  = PWM(Pin (26),1000)
bombillog  = PWM(Pin (25),1000)
bombillob  = PWM(Pin (33),1000)
potr = ADC(Pin(13))
potg = ADC(Pin(12))
potb = ADC(Pin(14))

  


while True:
  print(f"rojo:{potr.read()}\t verde:{potg.read()} \t azul:{potb.read()}")
  bombillor.duty( int (potr.read()/4))
  bombillog.duty( int (potg.read()/4))
  bombillob.duty( int (potb.read()/4))
  # bombillo.duty( int (pot.read/4))
  # bombillo.duty_ns( pot.read()*16)
  sleep_ms(30)
  
  
from machine import Pin
import utime
import esp32

led=Pin(21,Pin.OUT)
led1=Pin(23,Pin.OUT)
esp32.hall_sensor()

while(True):
    print(esp32.hall_sensor())
    if(esp32.hall_sensor()<0):
        led1.on()
    else:
        led.off()
    
    print(esp32.hall_sensor())
    if(esp32.hall_sensor()>0):
        led1.on()
    else:
        led1.off()
        
import machine,esp32, time
from machine import Pin
led=Pin(27,Pin.OUT)
T0 = machine.TouchPad(machine.Pin(4))
T0.config(600)
T1 = machine.TouchPad(machine.Pin(2))

while True:
    print(T0.read())
    led.value(T0)      
    time.sleep(0.2)        
        
        
