# Neural-Image-Captioning
Implementation of Encoder decoder model to generate description for Images
In this project there are few concepts such as,
1. Encoder-Decoder
2. Attention
3. ResNet and LSTM
4. BLEU score

### Objective
The purpose behind to work on this project is to develope an model which will take a input as a Image and describe that image like how humans do or how they think when they see something.
This type of model comes under the category of sequence to sequence model, because our input is image which is the sequence of poixel and generated output is the text, i.e. sequence of text.
I hope you got basic idea about the repository, let's dive into content

##### Data
The data used for this is Flickr8k dataset, consist of 8000 images. Flickr30k and COCO datasets are also avilable but to handle those rquires the bigger compute power.

### Encoder-Decoder architecture
Encoder-Decoder architecture consist of two subunits, Encoder and decoder. The encoder one which reads our inputs and learns through those inputs and this learning we transfer to decoder as learned parameter. so now after sending this parameter to the decoder our decoder started to generate the ouput one by one. At every decoding step the decoder take the parameter upto that step and embedding of the previously generated word and generate next word.
After one itearation it calculate the loss(cross entropy loss) and sum them. Use this loss and calculate loss gradient w.r.t to parameters. Based on gradient it changes the parameter and train it. Repeat this process until model getting train.
As our input is images which we can say the sequence of pixels so to extract features from them we have to use Convolutional Neural Network. While using CNN i.e. scratch model we can use some pretrained CNNs such as ResNet or VGG or AlexNet of any other that you wanted. Here I used the ResNet101(101 layer) because of it's residual connection which provide him to avoid vanishing gradient problem and good learning over the input.
To decode this learning of input parameters and generate the caption LSTM would be the good choice over RNN. The architecture of LSTM consist of three gates INPUT, OUTPUT, and FORGET gate this gates make LSTM to learn specific word which summarize our previous step sentence/caption to generate next word and avoid longterm dependecies on our previous data and vanishing gradient problem. 

### Attention Mechanism
The paper 'Attention All You Need' came with an interesting idea, the idea is that instead of learning whole input at once while generating whole single caption we can modify our encoder which can provide you the input learning at every step so you can focus on relevant pixels and generate the meaningful caption.
In attention mechanism, instead of taking average over all pixel we calculate the weighted average over the pixel. This modification tells our model at every decoding step to focus on particular pixel which is suitable to generate the word at that decoding step. And same process repeats and trained our model

### BLEU score (Bilingual Evaluation Understudy)
This metric from NLTK library used to evaluate the performance of our model. The main idea behind this metric is it calculate the score by matching the our generated output from decoder to reference one. This score lies between the 0 to 1. perfect match BLEU=1


