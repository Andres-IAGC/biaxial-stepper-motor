#TECNOLÓGICO​ ​NACIONAL​ ​DE​ ​MÉXICO

#INSTITUTO TECNOLÓGICO DE TIJUANA


# biaxial-stepper-motor



![51aNESyKXJL _AC_UF894,1000_QL80_](https://user-images.githubusercontent.com/71302151/223566455-2b268791-2f77-4bae-96cc-3233d51f3472.jpg)

#Para que se utiliza
se utiliza para controlar el movimiento en dos ejes perpendiculares entre sí. Este tipo de motor es capaz de girar en incrementos precisos, lo que lo hace ideal para aplicaciones que requieren un alto nivel de precisión y control, como en máquinas herramienta CNC, robótica, impresoras 3D y sistemas de posicionamiento.

#Como funciona
Los motores biaxiales stepper motor tienen dos ejes perpendiculares entre sí, lo que significa que cada eje tiene su propia serie de bobinas y se controla de manera independiente. Al controlar la secuencia de activación de las bobinas, se puede controlar la velocidad, la dirección y la precisión del movimiento en ambos ejes.

![image](https://user-images.githubusercontent.com/71302151/226469130-74c18722-b251-4e80-8fc8-c43d0e9fc574.png)

![image](https://scontent.ftij1-3.fna.fbcdn.net/v/t1.15752-9/336063161_765265048446820_5575798665155460983_n.png?_nc_cat=104&ccb=1-7&_nc_sid=ae9488&_nc_ohc=ni4ocz_mm4EAX9qfYOS&_nc_ht=scontent.ftij1-3.fna&oh=03_AdSQfrybJsg7Q4JBVH-u0bf7UwIYLaNXMW3t9KjMwbJVsA&oe=64404D3E)

#Codigo
# Importar los módulos necesarios
import machine # Para controlar los pines GPIO
import utime   # Para agregar retardos en el código

# Definir los pines GPIO que se van a utilizar
coil_A_1_pin = machine.Pin(0, machine.Pin.OUT)
coil_A_2_pin = machine.Pin(1, machine.Pin.OUT)
coil_B_1_pin = machine.Pin(2, machine.Pin.OUT)
coil_B_2_pin = machine.Pin(3, machine.Pin.OUT)


# Definir el patrón de paso para mover el motor en sentido horario
# El primer valor es el estado del pin A1-, el segundo valor es el estado del pin A1+,
# el tercer valor es el estado del pin B1+, y el cuarto valor es el estado del pin B1-
halfstep_seq = [
    [1, 0, 0, 1],
    [0, 0, 1, 1],
    [0, 1, 0, 1],
    [0, 0, 0, 1]
]
# Definir una función para mover el motor 
def motor_step(steps, direction):
    for i in range(steps):
        for halfstep in range(4):
            coil_A_1_pin.value(halfstep_seq[halfstep][0])
            coil_A_2_pin.value(halfstep_seq[halfstep][1])
            coil_B_1_pin.value(halfstep_seq[halfstep][2])
            coil_B_2_pin.value(halfstep_seq[halfstep][3])
            utime.sleep_ms(1)
    if direction == "left":
        halfstep_seq.reverse()
    else:
        pass


# Mover el motor 
motor_step(200, "right")

#Explicacion del codigo
Este código simula dos motores paso a paso conectados al Raspberry Pi Pico en la página de Wokwi. Los motores se controlan mediante la secuencia de pasos definida en la variable seq. Cada elemento de seq representa los valores de los cuatro pines de control del motor en un momento dado. Por ejemplo, seq[0] es [1, 0, 0, 1], lo que significa que el primer y cuarto pines del motor se activan y los otros dos no.

Las funciones forward() y backward() controlan la dirección de rotación de los motores, utilizando la función step() para realizar un paso en cada motor. La función step() toma cuatro argumentos: los valores de los cuatro pines de control del motor y un valor de retardo delay




https://wokwi.com/projects/359761724320927745


