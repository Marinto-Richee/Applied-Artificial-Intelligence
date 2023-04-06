# Implementation of Hidden Markov Model

## AIM
Construct a Python code to find the sequence of hidden states by the known sequence of obsevances using Hidden Markov Model. Consider two hidden states Sunny and Rainy with observable states, happy and sad.

## ALGORITHM
* Step 1: Define the transition matrix, which specifies the probability of transitioning from one hidden state to another.
* Step 2: Define the emission matrix, which specifies the probability of observing each possible observation given each hidden state.
* Step 3: Define the initial probabilities, which specify the probability of starting in each possible hidden state.
* Step 4: Define the observed sequence, which is the sequence of observations that we want to analyze.
* Step 5: Initialize the alpha matrix with zeros, where each row represents a time step and each column represents a possible hidden state.
* Step 6: Calculate the first row of the alpha matrix by multiplying the initial probabilities by the emission probabilities for the first observation.
* Step 7: Loop through the rest of the observed sequence and calculate the rest of the alpha matrix by multiplying the emission probabilities by the sum of the product of the previous row of the alpha matrix and the corresponding row of the transition matrix.
* Step 8: Calculate the probability of the observed sequence by summing the last row of the alpha matrix.
* Step 9: Find the most likely sequence of hidden states by selecting the hidden state with the highest probability at each time step based on the alpha matrix.

<br><br><br><br><br><br>
##  PROGRAM
```python3
import numpy as np
transition_matrix=np.array([[0.7,0.3],
                            [0.4,0.6]])
emission_matrix=np.array([[0.1,0.9],
                          [0.8,0.2]])
initial_probabilities=np.array([0.5,0.5])
observed_sequence=np.array([1,1,1,0,0,1])
alpha=np.zeros((len(observed_sequence),len(initial_probabilities)))
alpha[0,:]=initial_probabilities*emission_matrix[:,observed_sequence[0]]
     

for t in range(1,len(observed_sequence)):
  for j in range(len(initial_probabilities)):
    alpha[t,j]=emission_matrix[j,observed_sequence[t]]*np.sum(alpha[t-1,:]*transition_matrix[:,j])
probability=np.sum(alpha[-1,:])
print("The probability of the observed sequence is: ",probability)

most_likely_sequence=[]
for t in range(len(observed_sequence)):
  if alpha[t,0] > alpha[t,1]:
    most_likely_sequence.append("sunny")
  else:
    most_likely_sequence.append("rainy")

print("The most likely sequence of weather states is: ",most_likely_sequence)
```

## OUTPUT
![image](https://user-images.githubusercontent.com/65499285/230396164-fd6f1e16-47be-470e-b0c1-cabd1c87f5d1.png)

## RESULT
Thus, the Hidden Markov Model to identify the sequence of Hidden states is executed successfully.
