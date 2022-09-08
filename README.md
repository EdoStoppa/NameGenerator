# NameGenerator
  The idea for this project is pretty simple: create an application that, given a starting letter, can generate a number of names that starts with the given letter. To achieve that, an LSTM network was trained using 2000 common American names. The results are quite satisfactory, with names that are close enough to real names (for example Alessan, Alexandriah, Farroy)

## Dataset
  The dataset consists in the 2000 most common names in the US (1000 male names, and 1000 female names). Unfortunately, the first letter distribution is not optimal, but   it is to be expected given what we are actually sampling.
  <div align="center">
    <img src="https://github.com/EdoStoppa/EdoStoppa/blob/main/imgs/NameGenerator/letter_freq.png?raw=true" alt="Frequency of First Letters" width="600" height="350">
  <div />
  <div align="left"><div />
  This, even if may seems a major problem, doesn't break the generation for the less frequent letters. Obviously, the less frequent first letters generate stranger names than the more frequent ones, but they are still acceptable.
  
## Model
  The model is composed by 2 LSTM layers, and two fully connected layers. In particular, for the LSTM layer in PyTorch we use these parameters:
  ```
  INPUT_SIZE = 27
  HIDDEN_SIZE = 216
  NUM_LAYERS = 2
  ```
  The first fully connected layer has dimensions `(in: 216, out: 108)`, while the second layer has dimension `(in: 108, out: 27)`. The activation function used is the RELU, to avoid the problem of the vanishing gradient
    
## Hyperparameters
  There aren't a lot of hyperparameters, the only ones that I used are
  ```
  LEARNING_RATE = 0.005
  GAMMA = 0.95
  NUM_EPOCHS = 200
  ```
  Where `GAMMA` is the mutiplicative factor for which the learning rate is decrease in the `StepLR` scheduler.
  
## Results
  After 200 epochs the loss is about 0.42, that is an acceptable value. Here it's shown the curve
  <div align="center">
    <img src="https://github.com/EdoStoppa/EdoStoppa/blob/main/imgs/NameGenerator/loss.png?raw=true" alt="Loss" width="500" height="300">
  <div />
  <div align="left"><div />
  The names generated are satisfactory, and we can consider this project a success.<br />
  Here are some examples of names:
    
  ```
  alexa          anablee        anas           alexandriah    alessan
  farroyi        frarandol      frances        finnegan       fishel 
  ```
