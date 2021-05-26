# Emojional
Inspired by the current lack of existing emoji embedding models and their limited understanding of the nature of the evolving emotional content of the emoji, I have created novel emoji embeddings using their emotional content from their dictionary meanings. The subsequent emoji embeddings **are more accurate than the state-of-the-art embeddings by up to 4%** when tested on the task of sentiment analysis. 

As these embeddings were also trained on keywords, the subsequent embeddings are durable and can be used in different natural language tasks such as emotion, cyberbully and sarcasm detection successfully. The current embedding file contains all emojis as of [v13.1](https://unicode.org/emoji/charts/full-emoji-list.html) from Unicode.org (1816 emojis). The emoji embedding file will be updated when new emojis are added. 

## Creating the Dataset

I scraped the key emotive words from the online dictionaries [Emojipedia](https://emojipedia.org) and [Emojis.Wiki](https://emojis.wiki) and created a new dataset. 

The data looks like this:
🔮	crystal ball	future	magic	mysterious

### Change Dataset Format

In order for the model to train the data, the data needs to look like this:

* crystal ball	🔮	True
* magic	🔮	True
* mysterious	🔮	True

To achieve this I created a change dataset format script which also shuffles the data.

### Negative Sampling

To make quality embeddings, I needed to create negative samples.

* ripe fruits🔮	False
* dirt	🔮	False
* approval	🔮	False

## Test Train Dev Split

In the original paper the authors used a training folder which contained the datasets train.txt, test.txt and dev.txt in a 91.8% train, 4.1% test, 4.1% develop split, and a testing folder which contained 20 identical true samples in train.txt, test.txt and dev.txt. 

My full dataset consisted of 12205 true samples and 1000 of false samples. I also used the same 91.8% train, 4.1% test, 4.1% develop split.

### My Data Folder

#### Training Folder

* Train.txt consists of 11205 true samples.
* Test.txt consists of 500 true samples and 500 false samples.
* Dev.txt consists of 500 true samples and 500 false samples which are different from then test.txt.

Training folder uses all true samples available spread over the three datasets
The training folder also uses a total of 500 negative samples

#### Testing Folder

* Train.txt uses 20 true samples
* Test.txt uses 20 true samples
* Develop.txt uses 20 true samples

The folders can be found here.

## Training

I used a [PyTorch implementation of emoji2vec](https://github.com/pwiercinski/emoji2vec_pytorch). The original implementation of emoji2vec can be found [here](https://github.com/uclnlp/emoji2vec). 

### Training your own dataset
The train test and dev files have been replaced in both training and testing folders. The file ‘phrase_embeddings.pkl’ in the ‘pre-trained’ folder (if it exists) needs to be deleted as this will allow a new dictionary to be created from the new dataset. I ran the file ‘presentation.ipynb’ to train the embeddings.

## Testing
I used emoji2vec's original testing script and updated to current Python standards here.

### Results
I have evaluated the emoji embeddings on a list of emotive words, emoji similarity and analogies.
I compared my emoji embeddings to the state-of-the-art emoji embeddings on a Twitter sentiment analysis. Beating all other embeddings using Random Forests. 


## Mapping to Emotions and Key Words


### Homour

### Plutchicks Wheel of Emotion

### Similarities

### Analogy
## Visulization

### Visualizing Embeddings in 2D spaces
![download](https://user-images.githubusercontent.com/53048127/117536197-93685700-aff1-11eb-80ae-6bc98a5a8bb4.png)

## Using the Emoji Embeddings

To use the embedding you need to download the emojional.bin file and include the following code within your model.
```python
import gensim

e2v = gensim.models.KeyedVectors.load_word2vec_format("emojional.bin", binary=True)
```

## References

