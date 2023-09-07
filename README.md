import matplotlib.pyplot as plt


class SimplePerceptron:
    def __init__(self, learning_rate=0.01, epochs=100):
        self.learning_rate = learning_rate
        self.epochs = epochs
        self.weights = None
        self.bias = 0.0

    def activation_function(self, x):
        return 1 if x > 0 else 0

    def train(self, X, y):
        num_samples = len(X)
        num_features = len(X[0])
        self.weights = [0.0] * num_features

        for _ in range(self.epochs):
            for i in range(num_samples):
                x_i = X[i]
                linear_output = sum([x_i[j] * self.weights[j] for j in range(num_features)]) + self.bias
                y_predicted = self.activation_function(linear_output)
                
                # Actualización de pesos y bias
                update = self.learning_rate * (y[i] - y_predicted)
                for j in range(num_features):
                    self.weights[j] += update * x_i[j]
                self.bias += update

    def predict(self, X):
        predictions = []
        for x_i in X:
            linear_output = sum([x_i[j] * self.weights[j] for j in range(len(self.weights))]) + self.bias
            predictions.append(self.activation_function(linear_output))
        return predictions

def read_data(filename):
    with open(filename, 'r') as file:
        lines = file.readlines()
        X = []
        y = []
        for line in lines:
            data = [float(i) for i in line.strip().split(',')]
            X.append(data[:-1])
            y.append(int(data[-1]))
        return X, y

def plot_data(X, y, weights, bias):
    plt.figure()

    # Plot data points
    for i, x in enumerate(X):
        if y[i] == 1:
            plt.scatter(x[0], x[1], marker='o', color='g', label='Positive')
        else:
            plt.scatter(x[0], x[1], marker='x', color='r', label='Negative')

    # Plot decision boundary
    x_values = [-2, 2]
    y_values = [-(weights[0]*x+bias)/weights[1] for x in x_values]
    plt.plot(x_values, y_values, '-m')

    plt.xlabel('X1')
    plt.ylabel('X2')
    plt.title('Data Points and Decision Boundary')
    plt.grid(True)
    plt.show()
    


if __name__ == "__main__":
    # Lectura de datos
    training_filename = input("Ingrese el nombre del archivo de entrenamiento: ")
    X_train, y_train = read_data(training_filename)

    # Parámetros del perceptrón
    learning_rate = float(input("Ingrese la tasa de aprendizaje: "))
    epochs = int(input("Ingrese el número máximo de épocas: "))

    # Entrenamiento del perceptrón
    perceptron = SimplePerceptron(learning_rate=learning_rate, epochs=epochs)
    perceptron.train(X_train, y_train)

    # Test
    test_filename = input("Ingrese el nombre del archivo de prueba: ")
    X_test, _ = read_data(test_filename)
    predictions = perceptron.predict(X_test)

    print("Predicciones:", predictions)
    
    plot_data(X_train, y_train, perceptron.weights, perceptron.bias)
