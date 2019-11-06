# Neural network
Artificial neural network for Python. Features online backpropagtion learning using gradient descent, momentum, the sigmoid and hyperbolic tangent activation function.

## About
The library allows you to build and train multi-layer neural networks. You first define the structure for the network. The number of input, output, layers and hidden nodes. The network is then constructed. Interconnection strengths are represented using an adjacency matrix and initialised to small random values.  Traning data is then presented to the network incrementally. The neural network uses an online backpropagation training algorithm that uses gradient descent to descend the error curve to adjust interconnection strengths. The aim of the training algorithm is to adjust the interconnection strengths in order to reduce the global error. The global error for the network is calculated using the mean sqaured error. 

You can provide a learning rate and momentum parameter.  The learning rate will affect the speed at which the neural network converges to an optimal solution. The momentum parameter will help gradient descent to avoid converging to a non optimal solution on the error curve called local minima.  The correct size for the momentum parameter will help to find the global minima but too large a value will prevent the neural network from ever converging to a solution.

Trained neural networks can be saved to file and loaded back for later activation.

## Installation
```bash
$  pip install neuralnetwork
```
## Examples
### Training XOR function on three layer neural network with two inputs and one output
```
from neuralnetwork.FeedForward import FeedForward
from neuralnetwork.Sigmoid import Sigmoid
from neuralnetwork.Backpropagation import Backpropagation

sigmoid = Sigmoid()

networkLayer = [2,2,1]

feedForward = FeedForward(networkLayer, sigmoid)

backpropagation = Backpropagation(feedForward,0.7,0.3)

trainingSet = [
    [0,0,0],
    [0,1,1],
    [1,0,1],
    [1,1,0]
]

while True:
    backpropagation.initialise()
    result = backpropagation.train(trainingSet)

    if(result):
        break

feedForward.activate([0,0])
outputs = feedForward.getOutputs()
print(outputs[0])

feedForward.activate([0,1])
outputs = feedForward.getOutputs()
print(outputs[0])

feedForward.activate([1,0])
outputs = feedForward.getOutputs()
print(outputs[0])

feedForward.activate([1,1])
outputs = feedForward.getOutputs()
print(outputs[0])
```

### Training XOR function on three layer neural network using Hyperbolic Tangent
```
from neuralnetwork.FeedForward import FeedForward
from neuralnetwork.HyperbolicTangent import HyperbolicTanget
from neuralnetwork.Backpropagation import Backpropagation

hyperbolicTangent = HyperbolicTangent()

networkLayer = [2,2,1]

feedForward = FeedForward(networkLayer, hyperbolicTangent)

backpropagation = Backpropagation(feedForward,0.7,0.3,0.001)

trainingSet = [
                    [-1,-1,-1],
                    [-1,1,1],
                    [1,-1,1],
                    [1,1,-1]
                ];

while True:
    backpropagation.initialise()
    result = backpropagation.train(trainingSet)

    if(result):
        break

feedForward.activate([-1,-1])
outputs = feedForward.getOutputs()
print(outputs[0])

feedForward.activate([-1,1])
outputs = feedForward.getOutputs()
print(outputs[0])

feedForward.activate([1,-1])
outputs = feedForward.getOutputs()
print(outputs[0])

feedForward.activate([1,1])
outputs = feedForward.getOutputs()
print(outputs[0])
```

### Saving trained neural network to file
```
from neuralnetwork.FeedForward import FeedForward
from neuralnetwork.Sigmoid import Sigmoid
from neuralnetwork.Backpropagation import Backpropagation

sigmoid = Sigmoid()

networkLayer = [2,2,1]

feedForward = FeedForward(networkLayer, sigmoid)

backpropagation = Backpropagation(feedForward,0.7,0.3)

trainingSet = [
    [0,0,0],
    [0,1,1],
    [1,0,1],
    [1,1,0]
]

while True:
    backpropagation.initialise()
    result = backpropagation.train(trainingSet)

    if(result):
        break

feedForward.save('./network.txt')
```

### Load trained neural network from file
```
from neuralnetwork.FeedForward import FeedForward
from neuralnetwork.Sigmoid import Sigmoid
from neuralnetwork.Backpropagation import Backpropagation

feedForward = FeedForward.load('./network.txt')

feedForward.activate([0,0])
outputs = feedForward.getOutputs()
print(outputs[0])

feedForward.activate([0,1])
outputs = feedForward.getOutputs()
print(outputs[0])

feedForward.activate([1,0])
outputs = feedForward.getOutputs()
print(outputs[0])

feedForward.activate([1,1])
outputs = feedForward.getOutputs()
print(outputs[0])
```
