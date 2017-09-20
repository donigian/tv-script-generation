# TV Script Generation

In this project, I will generate your my [Simpsons](https://en.wikipedia.org/wiki/The_Simpsons) TV scripts using RNNs.  You'll be using part of the [Simpsons dataset](https://www.kaggle.com/wcukierski/the-simpsons-by-the-data) of scripts from 27 seasons.  The Neural Network I'll build will generate a new TV script for a scene at [Moe's Tavern](https://simpsonswiki.com/wiki/Moe's_Tavern).


### Dataset Stats
```
Roughly the number of unique words: 11492
Number of scenes: 262
Average number of sentences in each scene: 15.248091603053435
Number of lines: 4257
Average number of words in each line: 11.50434578341555
```

## Implement Preprocessing Functions
The first thing to do to any dataset is preprocessing. I'll implement the following preprocessing functions below:

+ Lookup Table
+ Tokenize Punctuation

## Tokenize Punctuation
I'll be splitting the script into a word array using spaces as delimiters. However, punctuations like periods and exclamation marks make it hard for the neural network to distinguish between the word "bye" and "bye!".

## Build the Neural Network
build the components necessary to build a RNN by implementing the following functions below:

+ **get_inputs**: implements the get_inputs() function to create TF Placeholders for the Neural Network. It should create the following placeholders:
	+ Input text placeholder named "input" using the TF 	+ Placeholder name parameter.
   + Targets placeholder
	+ Learning Rate placeholder
+ **get_init_cell**: Stack one or more BasicLSTMCells in a MultiRNNCell.
	+ The Rnn size should be set using rnn_size
	+ Initalize Cell State using the MultiRNNCell's zero_state() function
	+ Apply the name "initial_state" to the initial state using tf.identity()
+ **get_embed**: Apply embedding to input_data using TensorFlow. Return the embedded sequence.
+ **build_rnn**: Created a RNN Cell in the get_init_cell() function. Time to use the cell to create a RNN.
	+ Build the RNN using the tf.nn.dynamic_rnn()
	+ Apply the name "final_state" to the final state using tf.identity()
+ **build_nn**: 
	+ Apply embedding to input_data using your get_embed(input_data, vocab_size, embed_dim) function.
	+ Build RNN using cell and your build_rnn(cell, inputs) function.
	+ Apply a fully connected layer with a linear activation and vocab_size as the number of outputs.
+ **get_batches**: Return batches of input and target

## Hyperparameters
```
# Number of Epochs
num_epochs = 64
# Batch Size
batch_size = 512
# RNN Size
rnn_size = 1024
# Embedding Dimension Size
embed_dim = None
# Sequence Length
seq_length = 15
# Learning Rate
learning_rate = 0.01
# Show stats for every n number of batches
show_every_n_batches = 100
```

## Train
Train the neural network on the preprocessed data.

```
Epoch   0 Batch    0/8   train_loss = 8.822
Epoch  12 Batch    4/8   train_loss = 5.250
Epoch  25 Batch    0/8   train_loss = 3.771
Epoch  37 Batch    4/8   train_loss = 2.949
Epoch  50 Batch    0/8   train_loss = 1.947
Epoch  62 Batch    4/8   train_loss = 1.258
Model Trained and Saved
```

## Sample Output from Generated TV Script
```
moe_szyslak:
?(upbeat) why can should you always any luck.
lisa_simpson: i hope some song. you know my first man lisa. it's squeezin' the beginning. you've got beer from my new daddy.
detective_homer_simpson: say it. my answer what do you be loaded nine 'cause he ever!


moe_szyslak: all they miss you've.
fritz: really?
moe_szyslak: see? don't you know how to come up.
moe_szyslak:(impressed wide, the soon out.
homer_simpson:(sings) you could sacrifice my dad.
moe_szyslak: oh, why i'm nice for my new kids. you're the south of didn't.
homer_simpson:(trying to scream.
moe_szyslak: and i!
moe_szyslak: it's your prime on love in tv.
lenny_leonard: homer, lessee now...

c'mon, that kind of mister.
chief_wiggum:(sobs) i didn't let me so many bigger shoes fat... it's just that one into a world-class long.


homer_simpson: i'd like to really drunk from gettin' some man
```