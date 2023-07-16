# Temporal Relation Annotation Guidelines

*Yingying Chen*

Temporal dependency annotation aims to construct timelines of the ordering of events in the text. Our guideline is based on the paraphrasing approach (Bethard, et al. 2012) outlined below.

We annotate 5 temporal relations: `before`, `after`, `contains`, `contained`, and `overlap`. The relations `before` and `after`, and the relations `contains` and `contained` are inverses, so it is often possible to annotate a sentence in more than one equivalent way. The following definitions are adapted slightly from the UMR guidelines https://github.com/umr4nlp/umr-guidelines/blob/master/guidelines.md:
 

We also include document-creation-time `DCT` as the root node for each notation.  


| Role         | How to read | Annotation | Definition |Common Clauses |
|--------------|------------|------------|------------|------------|
| `before` | B is before A      |B before --> A or A after --> B |B is totally before A  (B finished before A started)      | past tense; perfect tense |
| `after`      | B is after A      |B after --> A or A before --> B |B is totally after A (B started after B had finished)      | future tense |
| `contains`      | B contains A  |B contains --> A or A contained --> B |the time of B properly contains the time of A (B started before A started and finished after A finished)  | present tense |
| `contained`      | B is contained in A  |B contained --> A or A contains --> B |the time of B is properly contained in the time of A (B started after A started and finished before A finished)   | |
| `overlap`      | B and A overlap   |A overlap B = B overlap A|the time of B and A overlap   | at the same time; while; when... |


## 1.Annotation Tool: Inception

**Temporal Labels (2):** DCT (d), Event (e)

**Temporal Relations (5):**  after (a), before (b), contains (c), contained (n), overlap (o)

1) Select the space at the very beginning of the paragraph and press "shift" button at the same time to create a `DCT` tag. 

* Typically, one text has one `DCT`. If a Reddit post has some follow-ups written such as as "edit/update", there could be more than one `DCT`. For example, in this case there are three `DCT`s. Remember to use the 'after' relation to link one `DCT` after another. 

> [DCT] ...the main passage... [edit]: guys, i don’t know why... [edit pt. 2]: i don’t understand ...  [edit 3]: I am not asking her...

**Relation Identification:**  
	
	[DCT] <-- after [DCT1 edit]: <-- after [DCT2 edit pt. 2]: <-- after [DCT3 edit 3]:


2) Select the appropriate text span to create an `Event` tag.

3) Link the `DCT` and `Event` or link `Event` and `Event`. Mind the direction of the arrow and choose the appropriate relation!


## 2.Three-Step Annotation

1) **Event Identification:** Choose the appropriate text span as an "Event" or "DCT".

2) **Pair Identification:** Consider whether an event is related to the DCT or to another event. Pair identification is normally linear and intuitive, except when the sentence contains a dependent clause. (see 4.10)

3) **Relation Identification:** Create the appropriate relation between the DCT and event, or between an event and an event.


## 3.Definition of "event"

In most cases, an event is the main predicate (the verb) in a sentence. An event can have occured in the past, in present, or in the future. But we only annotate events which have occured or will occur.


## 4.Core Rules

In the following instructions, the square brackets [] indicate a text span as an event. [DCT] for document creation time often appears at the beginning of the text.

### 4.1 How to annotate an "event"?
1. **Copula + noun/verb/adj./prep.** should be annotated as a single event because the copula is marked for tense which indicates the temporal order. 
    - copula + noun
      - It has [been a month]
      - It [is the only class] he takes.
      - It [is a piece of apple].
    - copula + gerund
      - I [am doing] my homework.
    - copula + adjective
      - He [was sad] because he did not get a full mark.
      - She [is always good].
    - copula + preposition
      - Tony [is in front of] you. 
      - Tony [is always in front of] you.
      - Tony [is always standing] in front of you.
    - existential construction (there be + X + verb-ing + Prep.)
      - There [are children swimming] in the lake. 
        - Children [are swimming] in the lake.
      - There [are birds in] the garden.
        - Birds [are in] the garden.
2. **To what extent should prepositions be annotated?**
    - We don't annotate infinitive "to" or locative prepositions.
      - We [went] to the supermarket yesterday.
      - He [is standing] on the table.
    - In other cases, we include preposition in a phrasal expression.
      - They [got on] the bus.
      - I [care about] you.
      - She [was thinking of] becoming a zoologist.
3. **What about sentences in parentheses?** 
Content in parenthesis is used for explannations. Some of them are meaningful and contain event(s), some are not.
    - If an event is included, annotate it.
        - We didn't have plans for spring break (this [happened] like two weeks before it).
4. **Colloquial expressions** 
    - If "be like" express the equivalent meaning as the verb "say", we can annotate them as events. 
      - She['s like] "now we need to go to Boston." = She [says] "now we need to go to Boston."
    - For the expression "feel like" with nominal complements, we annotate "feel like" because it means "want".
      - I [feel like] a burger. = I [want] a burger.


### 4.2 No speech
We don't annotate reported events because it is often unclear when the event described by direct or indirect speech is meant to have taken place.
> It (the voice) said : "If you please -- draw me a sheep !" (https://amr.isi.edu/download/amr-bank-struct-v1.6.txt)

**Event Identification:**  
It (the voice) [said] : "If you please -- draw me a sheep !" 

**Relation Identification:** 

	DCT <-- before [said]

We don't annotate the content after the speech verb. Speech verbs include but are not limited to "say", "claim", "argue".
> I am saying that the school was a sham taking advantage of minority children…

**Event Identification:**  
I [am saying] that the school was a sham taking advantage of minority children…

**Relation Identification:** 

	DCT <-- contains [am saying]

### 4.3 No hypothetical
Conditionals are a clear case in which events are hypothetical.
> If it rains, the grass will be wet.
	
**Event Identification:**  
If it rains, the grass will be wet.

**Relation Identification:**  

	N/A

When we see the following verbs, they are also expressed in a hypothetical situation that we don't annotate. "Hope", "want", "wish", and "feel" are all annotated, but the verbs that come after them are not annotated.
    - I [hope] to make some great progress.
    - He [wants] to achieve a higher score in annotation.
    - She [wished] her mother would call her.
    - I [felt] that the midterm was so hard.
    - It [seems] that this is the evidence.

We should be careful about the hypothetical adverbs including "seemingly", "apparently" especially when the context expresses uncertainty.
   - Apparently, bad things were taking place.
   
### 4.4 No modal
Modal auxiliaries should not be considered because they indicate a possibility rather than certainty. Keywords include but not limited to "might", "can", "must", "have to". We don't annotate verbal complements to modals.

> You should go to the school right now.

**Event Identification:**  
You should go to the school right now.

**Relation Identification:**  

	N/A

In the following example, we only annotate the predicate "think".

> It might be difficult to admit, but I think the dog has ran away.
	
**Event Identification:**  
It might be difficult to admit, but I [think] the dog has ran away.

**Relation Identification:**  

	DCT <-- contains [think]


### 4.5 No negated events
If an event is negated, it means it didn't happen. As such, we do not annotate negated expressions. 

In this example, the completion of the plans is negated and is irrelevant for the temporal ordering of the main events in the text.

> He left the project in 1966. His plans for the interior of the building were not completed. (https://aclanthology.org/D18-1371.pdf)

**Event Identification:**  
He [left] the project in 1966. His plans for the interior of the building were not completed. 

**Relation Identification:**  

	DCT <-- before [left]


Some words such as "barely", "hardly", "little" seem negative, but they do not always negate the event. For instance, in the following sentence, the author did in fact pass the exam.

> I barely passed the exam.

**Event Identification:**  
I barely [passed] the exam

**Relation Identification:**  

	DCT <-- before [passed]

Bear in mind that having a negation doesn't mean we have to give up annotating the whole sentence. 
    - I don’t like this because it [looks] bad.
    - I [like] this because it does not look bad.


### 4.6 No question
We do not annotate events in questions.

> Did he go to bed on time?

**Event Identification:**  
Did he go to bed on time?

**Relation Identification:**  
	
	N/A

### 4.7 No imperatives
An imperative is used to make a command. We do not annotate imperatives because it is uncertain whether the event happens or not.

> Play this game with me!

**Event Identification:**  
Play this game with me!

**Relation Identification:**  
	
	N/A

### 4.8 No exclamatives, swear words
In Reddit texts, it is common to see expressions that are unique to social media posts. For clarity, we make some rules to not annotate the following types of expression.

1. exclamatives
     - Thank you!
       - Thank you for [telling] me the truth!
2. swear words
    - Fuck my life. (this event obviously does not happen)


### 4.9 Paraphrasing rule
Select words that best paraphrase the meaning in phrasal events.

1. Aspectual verbs include but are not limited to "begin", "start", "stop", "remain", "end up", "proceed", "continue", "finish", "keep". We only annotate the verbs or adjectives that come after the aspectual verbs.
    - start [doing] my homework
    - stop to [rest]
    - the reason remains [mysterious]
    - end up [marrying] his childhood friend
    - proceed to [read]
    - continue [working] 
    - finish [planting] the seed
    - keep [raising] his questions
    - keep [alight]

2. Paraphrasing rule for other expressions
    - a dog who used to [snap at] other people (we don't annotate "used to")
    - he managed to [scramble on] to dry ground from a backwater (we don't annotate "managed to")
    - he got [called] yesterday (we don't annotate "got" in this context)
    - she gets [better] now (we don't annotate "gets" in this context)
    - He did his best to reach them by [jumping]. (we don't annotate "did" here)
    - this experience makes me [realize] ("realize" is more appropriate to be considered as an event than "make" in this context)

3. **Be Careful!**
The above rules are just for your references. They do not mean you should skip these keywords. Everything should be based on context and your judgement. For example,
    - She let herself [hang down] by her hind legs from a peg.
    - The mother [let] her children play Nintendo Switch after their assignments are done. (we annotate "let" but not "choose" here because "let" indicates permission here and events that come after might not occur)
 
### 4.10 Pair identification rule
Typically, we follow the reading order (from left to right) to annotate words. But when it comes to a complex sentence that consists of a main clause and a dependent clase, we need to be careful about the order of annotation.

> "[DCT] Before I [realized] this scam, I firmly [believed] it without any doubt. I [am confused] now."

**Main clause:** "I firmly believed it without any doubt."  
**Dependent clause:** "Before I realized this scam."

**(WRONG VERSION✖️)** Before we have this pair identification rule, we may link the events in this way:

	[DCT] <-- before [realized] <-- before [believed] <-- after [am confused]

**(CORRECT VERSION✔️)** But after we have this pair identification, we can do better in making sense of the logic of the timeline. The relation should be annotated in this way:

	[DCT] <-- before [believed], 
	[realized] <-- before [believed], 
	[believed] <-- after [am confused]

The difference is that now there is no relation between [realized] and [DCT].


### 4.11 Before & After
1. The relations `before` and `after` are used to annotate simple temporal precedence and subeqeunce relations between two events. 

> Tottenham will win a trophy this year.

**Event Identification:**  
Tottenham will [win] a trophy this year.

**Relation Identification:**  

	DCT <-- after [win]


2. The following example should be read as the dinining happened after the going which happened before the document creation time.

> Yesterday, I went to the museum, then had dinner with my friends. (https://aclanthology.org/2020.emnlp-main.432.pdf)

**Event Identification:**  
Yesterday, I [went] to the museum, then [had] dinner with my friends.

**Relation Identification:**  

	DCT <-- before [went]  
	[went] <-- after [had]


3. Likewise, the following sentence describes three events, with each preceding the next.

> I woke up at 6 A.M. yesterday, ate breakfast and then went to school by bus. (https://aclanthology.org/O08-4003.pdf)

**Event Identification:**  
I [woke up] at 6 A.M. yesterday, [ate] breakfast and then [went] to school by bus.

**Relation Identification:** 

	DCT <-- before [woke up]  
	[woke up] <-- after [ate]  
	[ate] <-- after [went]

					
4. In general, we use `before` to annotate sentences containing the perfect. This is demonstrated in the following example. Notice also that in this example, the document creation time is set in the future in "2051", rather than the present. It is rare for the document creation time to be in the future, but quite common for it to be set in the past.

> The year is 2051 . All cancers have been cured , all world issues have been solved...

**Event Identification:**  
The year [is 2051] . All cancers have [been cured] , all world issues have [been solved]...

**Relation Identification:**  

	DCT <-- contains [is 2051]  
	DCT <-- before [been cured]  
	DCT <-- before [been solved]
	
	
### 4.12 Contains & Contained
1. It is common to see present tense statives or progressives. In both cases, you should use `contains` to relate these to the document creation time.

> People are anxious, the world is heating up, and the icecaps are melting.

**Event Identification:**  
People [are anxious], the world [is heating up], and the icecaps [are melting].

**Relation Identification:**  

	DCT <-- contains [are anxious]  
	DCT <-- contains [is heating up]  
	DCT <-- contains [are melting]

2. In the following example, the bear came up to the man during the pretending event, so we use a `contained` relation.

> He threw himself on the ground and pretended to be dead. The bear came up and sniffed all around him. (http://www.lrec-conf.org/proceedings/lrec2012/pdf/371_Paper.pdf)

**Event Identification:**  
He [threw] himself on the ground and [pretended] to be dead. The bear [came up] and [sniffed] all around him. 

**Relation Identification:**  

	DCT <-- before [threw]  
	[threw] <-- after [pretended]  
	[pretended] <-- contained [came up]  
	[came up] <-- after [sniff]


3. In the next example, the boy was stung during the berry gathering event, so again we use a `contained` relation. The pain was felt after the stining event, and the running was `contained` in the time at which the boy felt pain. Notice also that because the state of smarting with pain is in a dependent clause, the stinging is ordered with respect to the running and not the smarting.

> A boy was gathering berries from a hedge when his hand was stung by a nettle. Smarting with the pain, he ran to tell his mother. (https://aclanthology.org/P12-1010.pdf)

**Event Identification:**  
A boy [was gathering] berries from a hedge when his hand [was stung] by a nettle. [Smarting] with the pain, he [ran] to tell his mother.

**Relation Identification:**  

	DCT <-- before [was gathering]  
	[was gathering] <-- contained [was stung]  
	[was stung] <-- after [ran]  
	[smarting] <-- contained [ran]


### 4.13 Overlap
`overlap` means two events may share an interval of time. It is also comaptible with the events sharing all their times (i.e., happening at identical times).

1. In this example, the loss in value and the falling are are happening at the same time, so the `overlap` relation would be appropriate.

> The insurer’s earnings from commercial property/casualty lines fell 59% in the latest quarter, while it lost $7.2 million in its personal property/casualty business. (https://aclanthology.org/2020.coling-main.294.pdf)

**Event Identification:**  
The insurer’s earnings from commercial property/casualty lines [fell] 59% in the latest quarter, while it [lost] $7.2 million in its personal property/casualty business.

**Relation Identification:**  

	DCT <-- before [fell]  
	[fell] <-- overlap [lost]

	    
2. In the example below, the saying event is overlapping with the calling for ratification. In this case, annotators can use `overlap` to capture the temporal relation. 

> Yeltsin and Kuchma called for the ratification of the treaty, saying it would create a “strong legal foundation”. (https://aclanthology.org/2020.emnlp-main.689.pdf)

**Event Identification:**  
Yeltsin and Kuchma [called for] the ratification of the treaty, [saying] it would create a “strong legal foundation”.

**Relation Identification:**  

	DCT <-- before [called for]  
	[called] <-- overlap [saying]  


3. **Caution:** It is important that annotators are consistent. So do not use the `overlap` relation to annotate present tense states or progressives (which should be annotated with `contains`). Consider again the example from above.

> People are anxious, the world is heating up, the ice caps are melting.

**Event Identification:**  
People [are anxious], the world [is heating up], and the icecaps [are melting].

**(CORRECT VERSION✔️) Relation Identification:**  

	DCT <-- contains [are anxious]  
	DCT <-- contains [is heating up]  
	DCT <-- contains [are melting]

It is true that these events overlap each other. But that is already entailed by this annotation. If every event contains the DCT, then they must overlap. The following annotation would be less informative.

> People are anxious, the world is heating up, and the icecaps are melting.

**(WRONG VERSION✖️) Relation Identification:**  

	DCT <-- contains [are anxious]  
	[are anxious]  <-- overlap [is heating up]  
	[is heating up] <-- overlap [are melting]
			
This does not tell us whether the melting and the anxiousness overlap each other, or whether melting and heating up overlap the document creation time. Since `contains` is a more informative relation, annotators should annotate as in the first example.


## Examples of Annotations

### Example 1 (a paragraph of a children's story)

> Two travelers were on road together, when a bear suddenly appeared on the scene. Before he observed them, one made for a tree at the side of the road, and climbed up into the branches and hid there. (http://www.lrec-conf.org/proceedings/lrec2012/pdf/371_Paper.pdf)

**Event Identification:**  
Two travelers [were on] road together, when a bear suddenly [appeared] on the scene. Before he [observed] them, one [made for] a tree at the side of the road, and [climbed up] into the branches and [hid] there. 

**Explannations:**  
  - **Event annotation**
    - [appear] is correct, because "on" is a locative preposition.
    - [made for] is correct. "Make for" in dictionary means "head for", and two words should not be separated.
  - **First sentence**
    - Main clause: Two travelers [were on] road together
    - Dependent clause: when a bear suddenly [appeared] on the scene 
  - **Second sentence**
    - Main clause: one [made for] a tree at the side of the road, and [climbed up] into the branches and [hid] there 
    - Dependent clause: Before he [observed] them

**Relation Identification:**  

	DCT <-- before [were on]  
	[were on] <-- contained [appeared]  
	[were on] <-- after [made]  
	[observed] <-- before [made]  
	[made] <-- after [climbed up]  
	[climbed up] <-- after [hid]

