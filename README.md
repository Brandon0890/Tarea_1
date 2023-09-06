# Tarea_1
Import random

X1 = 0
X2 = 0
B = 1
WX1 = O
WX2 = 0
WXB = 0
Y = 0
Sumatoria = 0

Print("Perceptron simple")

X1 = float(input("Ingrsa X1: "))
X2 = float(input("Ingrsa X2: "))

WX1 = random.uniform(-1, 1)
WX2 = random.uniform(-1, 1)
WXB = random.uniform(-1, 1)

B = B * WXB

Sumatoria = (X1 * WX1) + (X2 * WX2) + B

if (sumatoria >= 0):
  Y = 1
else:
  Y = 0

print("Resultado Sumatoria: ", Sumatoria)
print("Resultado Salida(Y): ", Y)
