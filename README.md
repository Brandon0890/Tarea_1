# Tarea_1
import random

Y = 0
B = 1
x1 = 0
x2 = 0
wx1 = 0
wx2 = 0
wxB = 0
sum = 0

print("Tarea 1 _____Perceptron simple____")

x1 = float(input("Por favor ingresa el primer valor (x1): "))
x2 = float(input("Por favor ingresa el segundo valor (x2): "))

wx1 = random.uniform(-1, 1)
wx2 = random.uniform(-1, 1)
wxB = random.uniform(-1, 1)

B = B * wxB
sum = (x1 * wx1) + (x2 * wx2) + B


if (sum >= 0):
  Y = 1
else:
  Y = 0

print("°°°°LISTO ESTOS SON TUS RESULTADOS°°°°")
print("Resultado de la Sumatoria: ", sum)
print("Resultado de la Salida(Y): ", Y)
