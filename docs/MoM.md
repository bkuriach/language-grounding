
## Meeting Dated: 13-10-2022
1. Improve the image retrieval corresponding to the noun phrases using Multimodal models (ex. ViLT)
2. Manually annotate affordances for 250-500 examples for the evaluation of the pipeline.
3. Pretrain SOTA language models (start with RoBERTa/GPT2) using the affordance information received from the pipeline. E.g. "A boy wearing a Nike shoe. [SEP] Shoe cannot be [MASK]" - predict the MASK (affordance)
4. Evaluate this prtrained model on the reasoning tasks (such as PIQA).

References to read: 
1. https://arxiv.org/pdf/2210.06423.pdf (Foundation transformers)
2. https://arxiv.org/pdf/2007.04245v1.pdf (Understanding Object Affordances Through Verb Usage Patterns)

https://paperswithcode.com/paper/vilt-vision-and-language-transformer-without
## Meeting Dated: 01-09-2022
1. Finish the visual attribute prediction for the candidate images by this weekend (at least for the uncontextualized word embeddings)
2. Taking weighted averages of both sentence and word embeddings is not a very good idea. Think about other Contextualized embeddings (similar to COBE) and improve relevance of the candidate images
3. For each of the top predicted candidate images for a noun_phrase carry forward the confidence score of each of predicted attributes (e.g. round, square etc) to next step (i.e. affordance prediction)
3. For affordance prediction, we can apply markov networks properties (undirected graphical model):

Example -  two objects - ball and chair, 
                  and candidate affordances -  round, square, tall, small
                  0.7 * 0.5: ball, round + chair,tall =  w1
                  0.3 * 0.5: ball, square + chair,tall = w2
                  0.7 * 0.5: ball, round + chair, small = w3
                  0.3 * 0.5: ball, square + chair, small = w4

                 predictions using markov logic
                 y1 = F(w1) = 0.35
                 ......
                 y4 = F(w4) = 0.15
                i.e. each probabilities are independent of each other
                (Ref: Sato's Distribution Semantics - independent random variables)
4. Discuss the paper https://aclanthology.org/2021.findings-emnlp.370.pdf and share a short summary in the chat by next week. Explore the PIQA (PhysicalQA) and plan how we can incorporate the affordance data (we are creating) in SRL (semantic role labelling) and similar tasks by fine tuning a language model. 


## Meeting Dated: 18-08-2022
1. The most appropriate pipeline for affordance prediction could be - 
   collect the set of candidate images for each noun_phrases --> re-rank the images using the context information from the sentences (from which noun_phrases being extracted) --> Use Faster R-CNN for feature extraction (patches/bbox) --> apply ResNet for visual (or other) attributes prediction --> predicting affordances for each noun_phrases
2. Improve the candidate image collection and incorporating sentence information for re-ranking (Daivik & Binil)
3. Use Faster R-CNN for feature extarction and apply ResNet for visual attribute prediction and finally affordance prediction (Daiviki & Sayantan)
4. Think about the tasks such as commonsense reasoning which could be performed using objects and it's corresponding affordances.

## Meeting Dated: 04-08-2022
1. Use 100k visualgenome encoded images for searching for 100 examples of xnli  
2. Filter the images, For each sentence/noun phrases --> corresponding images (2-3)
3. Use the KB to predict the affordance for the noun phrases

## Meeting Dated: 08-07-2022

1. Take 10-15 sample sentences from XNLI data
2. Chunking of sentences using different methods - a> RST parser, b> Syntactic parser, c> entity mentions
3. Using the chunks taken from each of the techniques search for images from imageNet/VisualGenome
4. Manually verify the relevance of the images for each of those techniques and select the best method

Additional Notes: While considering objects for the affordances, take initial seed set of objects from conceptNet/WordNet
Resources: 
https://stanfordnlp.github.io/CoreNLP/demo.html
https://corenlp.run/

## Meeting Dated: 23-06-2022

1. Email the authors about the affordance Knowledge Base
2. - XGLUE is a data constructed from different premises (XNLI, MLNI)... Search in ImageNet, VisualGenome for corresponding images of the samples of XGLUE data. (Given premise as caption, find image)
   - If image available use visual attributes, otherwise use other attributes and utilize KB + MLN to predict top 10 affordances
3. For Human as object, don't consider what human beings can do in general. E.g.  Old man is walking -> Try to predict affordance of 'old man'
4. Skim through the dataset and need to plan to find what are the valid high quality affordances.
5. Map the corresponding candidate objects in English texts to their other versions (Hindi, Spanish etc).. to be used to find multilingual representation of objects
6. To Study:
  - Analysis of Universal Language Models
  - Muril, XLM-R, mBERT  
  - GATO agent
  - The State and Fate of Linguistic Diversity and Inclusion in the NLP World (https://arxiv.org/pdf/2004.09095.pdf)
