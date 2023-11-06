# Experiment-6---Implementation-of-Semantic-Analysis

## Aim : Construct a python program to read a text from a file.Identify the verbs from the text file and provide synonyms for all verbs using Natutal Language Processing 

## Algorithm:
1.Import the necessary libraries: nltk and wordnet.
2.Define a function get_verbs(sentence) to identify verbs in a given sentence using part-of-speech tagging.
3.Define a function get_synonyms(word) to get synonyms for a given word using the WordNet corpus.
4.Define a function read_text_file(file_path) to read text from a file and return the content as a string.
5.In the main program:
  Set the file_path variable to the path of the input text file.
  Read the text from the file using the read_text_file() function.
  Tokenize the text into sentences using the sent_tokenize() function from the nltk library.
  Initialize an empty list all_verbs to store all identified verbs.
  Initialize an empty dictionary synonyms_dict to store the synonyms for each verb.
  Iterate over each sentence:
  Call the get_verbs() function to identify verbs in the sentence.
  Append the identified verbs to the all_verbs list.
  For each verb, call the get_synonyms() function to get its synonyms and store them in the synonyms_dict dictionary.
  Print the verbs and their synonyms.
6.Execute the main program.

## Program:
```
Developed by: Sivabalan S
Register number: 212222240100
```
```
import nltk
nltk.download('wordnet')
nltk.download('punkt')
nltk.download('averaged_perceptron_tagger')
from nltk.tokenize import word_tokenize, sent_tokenize
from nltk.corpus import wordnet as wn
from nltk.tag import pos_tag


def read_text_file(file_path):
    with open(file_path, 'r') as file:
        text = file.read()
    return text

file_path = 'text_file.txt'  # Replace with the path to your text file
text = read_text_file(file_path)

def get_verbs(text):
    tokens = word_tokenize(text)
    tagged_tokens = pos_tag(tokens)
    verbs = [word for word, pos in tagged_tokens if pos.startswith('VB')]
    return verbs

verbs = get_verbs(text)
def get_synonyms_antonyms(verb):
    synonyms = []
    antonyms = []

    for synset in wn.synsets(verb, pos=wn.VERB):
        for lemma in synset.lemmas():
            synonyms.append(lemma.name())
            if lemma.antonyms():
                antonyms.append(lemma.antonyms()[0].name())

    return set(synonyms), set(antonyms)

verb_synonyms_antonyms = {}
for verb in verbs:
    synonyms, antonyms = get_synonyms_antonyms(verb)
    verb_synonyms_antonyms[verb] = {'synonyms': synonyms, 'antonyms': antonyms}

for verb, data in verb_synonyms_antonyms.items():
    print(f"Verb: {verb}")
    print(f"Synonyms: {', '.join(data['synonyms'])}")
    print(f"Antonyms: {', '.join(data['antonyms']) if data['antonyms'] else 'No antonyms found.'}")
    print()
```

## Output:
![243279035-e1234a46-4a7c-4fea-8a6f-6fef43c18767](https://github.com/sivabalan28/Experiment-6---Implementation-of-Semantic-Analysis/assets/113497347/c51fffd5-cae3-45fa-abe0-78c6912f4d75)

## Result
Thus, we have successfully implemented a program for Natural Language Processing.
