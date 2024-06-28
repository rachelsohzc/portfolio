+++
title = "Simple stock prediction with ANN"
description = ""
type = ["posts","post"]
tags = [
    "AI/ML",
    "LSTM",
    "Data Analysis",
    "Neural Networks",
]
date = "2022-05-04"
categories = [
    "Data Analysis",
    "AI/ML",
]
+++

[THIS IS AN ONGOING PROJECT](https://github.com/rachelsohzc/Simple-stock-prediction-with-ANN)

The task of predicting stock market prices is challenging. That’s what drove me to do this project. Due to high volatility, investors use a combination of technical and fundamental analysis to help them better decisions about their equity market decisions. A newly popular technical methods is using artificial neural networks (ANN). Therefore, this project aims to find out which ANN model has the best performance.

Some main concepts and code from this project can be found below:

### Sliding Window concept

Since we’re dealing with the stock market, dates are important in the data. To make the most of the data, I transformed it with a sliding window before using it to train the models. An example of a sliding window: The data consists of records 1,2,3,4,5,6. I then convert this data into the following:

| Input      | Output |
| ----------- | ----------- |
| 1, 2      | 3       |
| 2, 3   | 4        |
| 3, 4   | 5        |
| 4, 5   | 6        |

### Multi-layer perceptron (MLP) model

The MLP model is the simplest of all models used. I used this model as a baseline for comparisons later on.

```
{{ class MLP(nn.Module):
def __init__(self, num_inputs, num_outputs, num_hiddens):
    super(MLP, self).__init__()
    self.hidden = nn.Linear(num_input, num_hidden) 
    nn.init.kaiming_uniform_(self.hidden.weight) 
    self.activation = nn.ReLU()
    self.out = nn.Linear(num_hidden, num_output)

def forward(self, X):
    X = self.hidden(X)
    X = self.activation(X)
    X = self.out(X)
    return X }}
```

### Recurrent neural network (RNN) model

Recurrent neural networks was another one of my model choices because it takes information from the previous input to influence the next output/node. This feedforward characteristic was promising.

```
{{ class RNN(nn.Module):
def __init__(self, num_inputs, num_hiddens, num_layers, num_outputs):
    super(RNN, self).__init__()
    self.num_hiddens = num_hiddens 
    self.num_layers = num_layers 
    self.rnn = nn.RNN(num_inputs, num_hiddens, num_layers, batch_first = True) 
    self.fc = nn.Linear(num_hiddens, num_outputs) 
    
def forward(self, X):
    h0 = torch.zeros(self.num_layers, X.size(0), self.num_hiddens).requires_grad_()
    out, h_state = self.rnn(X, h0.detach())
    out = self.fc(out[:, -1, :]) 
    return out }}
```

### Long-short term memory (LSTM) model

LSTMs model are a built-on version of an RNN model. Although they have been known to perform better for things like speech, handwriting etc, it’s also well-known for forecasting well as it tends to remember only important bits of information, and omits irrelevant data.

```
{{ class LSTM(nn.Module):
def __init__(self, input_dim, hidden_dim, num_layers, output_dim):
    super(LSTM, self).__init__()
    self.hidden_dim = hidden_dim 
    self.num_layers = num_layers 
    self.lstm = nn.LSTM(input_dim, hidden_dim, num_layers, batch_first=True) 
    self.fc = nn.Linear(hidden_dim, output_dim) 

def forward(self, x):
    h_0 = torch.zeros(self.num_layers, x.size(0), self.hidden_dim).requires_grad_()
    c_0 = torch.zeros(self.num_layers, x.size(0), self.hidden_dim).requires_grad_()
    out, (hn, cn) = self.lstm(x, (h_0.detach(), c_0.detach())) 
    out = self.fc(out[:, -1, :]) 
    return out }}
```

View the full project repository **[here](https://github.com/rachelsohzc/Simple-stock-prediction-with-ANN)**