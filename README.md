# Lord-of-the-Rings-Training
 Deep learning to create a model that can generate text that could theoretically be in the Lord of the Rings 

## Neural Networks and Deep Learning

### DEFINITIONS

1. Natural Language Processing (NLP)
    1. Natural language Processing manipulates human languages, this can be as simple as detecting repeated words or more complicated like in the case of this project of generating human-like text based on previous works.
2. Neural Networks
    1. A Neural Network is a series of algorithms that recognises underlying patterns and relationships within a set of data. Neural networks are a type of machine learning but the technique is often refered to as deep learning. A neural network can contain many nodes that are densely connected. An individual node or neuron may be conecced to several nodes in the layer beneath it and several in the layer above it. 
3. Seq-2-Seq models
    1. Sequence to Sequence (Seq-2-Seq) is about converting sequences from one domain into a sequence in another domain. For example, language translation works really well as a seq-2-seq model. These models are often used anytime we want to generate task. Typically we would use a recurrent neural network (RNN) to work with seq-2-seq. 
4. Attention
    1. Attension mechanisms are a type of input for Neural Networks that allows the network to focus on specific aspects of a complex imput. When an input is very complex, this can be broken down into manageble chunks that can then be paid attention to. This happens until the whole dataset is categorised. These models and mechanisms require continuous reinforcement to be effective. Attention mechanisms are common in both computer vision and Neural Machine Translation. 
5. Transformers
    1. A transformer in NLP is an architecture that solves solves sequence-to-sequence tasks for long-range dependency instead of attention based seq-2-seq models. 



<br><br>
### Transformers and language modelling
<center>
<br>
You can read about the origin and proposal of these archetictures in the paper <a href="https://arxiv.org/abs/1706.03762">Attention Is All You Need</a>. The novel architecture allows for long-range dependency unlike seq-2-seq models which have challenges with this and parallelization. These issues are addressed by transformers. The limitation of Transformers is that Attention can only be used on fixed lengths. A text has to be split into a certain number of segments before it can be fed into the system. This chunking can cause context fragmentation. Meaning can be lost if a sentence is split in two, or some other boundary.  
<br>
<img src="https://cdn.analyticsvidhya.com/wp-content/uploads/2019/06/Screenshot-from-2019-06-17-19-53-10.png">
<br> <i>Figure 1: Transformer Architecture</i></center>
<br><br>

Transformers in the case of Language Modelling has been around since 2018 <a href ="https://arxiv.org/abs/1808.04444">(Al-Rfou 2018)</a>. Transformers are particularly successful in text generation where the long-term context matters for the readability and improvement of AI-text. It allows the text to become more Human. This computation however is quite intensive. For this project a NVIDIA GTX-1080 was used, and I think it would be remiss to try this without a GPU.  

The HuggingFace transformer package was used for this project which can be found here https://github.com/huggingface/transformers and installed using
> pip install transformers

For this project we ended up using the GPT-2 transformer from OpenAI. 

## Observations and outcomes
You can view my testing of the model in the jupyter notebook 'testing.ipynb'. The model seemed to be able to group characters that do appear commonly together well. Scenes with Legolas often contained Aragorn and Gimli, and scenes with Frodo often contained Sam and Gandalf. There was a clear acknowledgement of Sauron and Saruman being the villains throughout the story, unless they were involved in the prompt and then it was a little bit harder -- Including one paragraph where Sauron is escorting Frodo!

I started with a small prompt, and used the following settings. Temperature - 1 Top_P = 0.9 length = 500

### Test One
Input

> Aragon looked at the cloaked figure.

Generated text
<blockquote>
He was no longer cloaked but in a brown woolen cloak; and the edge of his sword hung with the Elven-cloak above the belt. 'Away now!' cried Aragorn. 'Up into the glade! Follow me! It will be glad to hear the rumour that Boromir perished there.' They found in the hollow beneath Amon Hen that was where Boromir had fallen; but the elf-cloak that he wore had been broken, and lay lost in the dell. When at last they had passed the dell they found that he had been clothed again, and carried. A garment of mail was embroidered upon the garment and wrapped in grey cloths, and was driven into the folds about the waist. Above his tunic he bore a helm, a quiver of elven-string; and beneath it was a robe of fair cloth of fine linen, the hue of which had been chosen by him, but it was in the gold of Rivendell that it was wrought. To his left he wore a mail shirt of green and white, and beneath it he was clad in a grey shirt of mail and with green shields. From his belt a spear was he wore a silver rapier. Aragorn leaped to his feet. 'Away!' he cried. 'This is the spear of Boromir, son of Arathorn!
You can see that the text does read like it could be in Tolkien's work, but there are some definite mistakes to the human eye. Boromir being the son of Arathorn is a large one, or that he was no longer cloaked but in a cloak. Interestingly though, throughout the text Boromir does remain dead which I think is good, although possibly because he is dead for 2/3rds of the text.</blockquote>

From there I decided to mess with the temperature and P values to see how much to iron out.

When temperature and or p reached < 0.6, the repitition in the text was very high.
<center> <img src="https://i.ytimg.com/vi/h8ciZV9zk-A/maxresdefault.jpg"> </center>
### Increasing Repetition penalty

Using the same prompt with a lower temperature and p_value but a repetition_penalty of 1.2 the following text was generated

<blockquote> 
 `He is a wizard,' he said, 'and a great lord of men.'
     `A mighty king!' cried Legolas; and Gimli was amazed to see the old man in such a high place among the Riders: so tall and fair, yet so young and yet so old! He seemed like an older brother than the others that stood before him or followed after his lead into battle-field upon either side – but he had no helm nor sword. His face bore a keen and commanding look as if he were a judge of men's worth. And yet he spoke in a kindly voice with clear voices for the most part, and was not proud or angry. He smiled, though he did show signs also now more clearly then ever when he spoke softly to the others about their own affairs under sunlit sky."

 
"He has come to the Last Battle," I say again," said Aragon stern and gravely "not to tell you that he will not be here. But he comes to you, Gimli sonof Glóin. For he knows that you are in peril, and he desires peace, even if you do what may seem wise. So do all men who go to war, and you have done what your friends would ask".
 But I am not yet ready", answered Gandli. _I must go now. The Lord Denethor commands me._ What he means by this we cannot guess, but he says: _The Ring shall remain here, until the end_. I fear that he means _until_ the End. But I know that he does much else. We need it, and we can use its power. Now he turned away from them and went out of sight.

"So I heard it myself!" said Legolas. "_It is a command of Saur-ard that I should give to all my kindred. I wish therefore only one thing: first take back Rohan, where it belongs. That way we might have peace and quiet. But we could still help the Enemy. It seems plain enough to us that the Ring itself is the keystone which he seeks. He knows that it came there, and that we knew it, and made sure arrangements with Saruman. But he would find it hard indeed justifiably hostile to the Ring, if he knew that it was not his own.
 </blockquote>
 
 There is some punctuation errors, but what I did find very interesting was the generation of "Saur-ard" as a name, and also the use of captalisation of 'the End' in the sentence  "_The Ring shall remain here, until the end_. I fear that he means _until_ the End." As i think this has a very significant weight to it as a piece of literature that I don't think is necessarily easy for a computer to understand. 
