---
title: PyTorch
Date Created: 2024-10-26
Last Updated: 2025-09-28
tags:
  - CS2109S
  - PyTorch
---
# PyTorch
---
We usually use <span style='color:var(--mk-color-purple)'>PyTorch</span> to build a neural network.

Here are some <span style='color:var(--mk-color-orange)'>basic function</span> provided in the <span style='color:var(--mk-color-purple)'>PyTorch</span> package.
**Containers**
- Module - `torch.nn.module`
- Sequential - `torch.nn.sequential`

**Linear Layers**
- Single layer NN with no activation - `torch.nn.Linear`

**Non-linear activation functions**
- ReLU - `torch.nn.ReLU`
- Sigmoid - `torch.nn.Sigmoid`
- Softmax - `torch.nn.Softmax`

**Loss functions**
- MSE - `torch.nn.MSELoss`
- Binary Cross entropy - `torch.nn.BCELoss`
- Cross entropy - `torch.nn.CrossEntropyLoss`

**Optimizers**
- Stochastic gradient descent - `torch.nn.SGD`
- Adam - `torch.nn.Adam`

The <span style='color:var(--mk-color-teal)'>Adam</span> optimiser is <span style='color:var(--mk-color-green)'>better</span> in a sense that it is <span style='color:var(--mk-color-yellow)'>less sensitive to the learning rate</span>.

**Important functions**
- Set all gradients to 0 - `optimizer.zero_grad()` (*We need to set a variable with one of the optimizers*)
- Update the weights after 1 step - `optimizer.step()`

**Example of modeling this NN**
![[PyTorch Modeling Example.png|center]]

```Python
class NNRegressor(torch.nn.Module):
	def __init__(self, inputSize, hiddenSize):
		super().__init__()
		# First we need to get the linear "box"
		# Hiddeen size is the number of neurons in that layer which is also the output size
		self.linear1 = torch.nn.Linear(input_size, hidden_size, bias=False)
		self.linear2 = torch.nn.Linear(hidden_size, 1, bias=False)
		# This is for the ReLU activation function
		self.relu = torch.nn.ReLU()
	
	# Make a predicition
	def forwardPropagation(self, x):
		# Pass the input and output as per normal in to the different components
		f1 = self.linear1(x)
		a1 = self.relu(f1)
		f2 = self.linear2(a1)
		return f2

model1 = NNRegressor(2,8) # 2 features, 8 hidden neurons
# This is the same as doing it with a class
model2 = torch.nn.Sequential(
			torch.nn.Linear(2,8),
			torch.nn.ReLU(),
			torch.nn.Linear(8,1)
		)
```

Then how can we <span style='color:var(--mk-color-orange)'>optimise</span> it:
```Python
model = NeuralNetRegressor(2,8)

loss_function = torch.nn.MSELoss()
# mode.parameters() retrieves all the weights in the model
optimizer = torch.optim.SGD(model.parameters(), lr = 0.01)

for epoch in range(num_epochs):
	y_pred = model(x)
	loss = loss_function(y_pred, y)
	# If we do not set to 0 then we will accumulate the weight modification over each epoch
	optimizer.zero_grad()
	# Carry out backwards propagation
	loss.backward() 
	# Update the weights, this line in important if not it will not update
	optimizer.step()
```
