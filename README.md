# Lord-of-the-Rings-Training
 Deep learning to create a model that can generate text that could theoretically be in the Lord of the Rings 

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
