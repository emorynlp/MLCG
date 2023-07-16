# Annotation Guideline: Coreference

*Yuxin Ji*


## Quick Guide for Coreference

|      Annotation  | Situation |
|---------------|-----------------------------|
|  do not annotate  | A is not referred to elsewhere in the document | 
|`A --- B --- C`      | Entities/events A, B, and C are identity coreferences |
|`A --(subset)--> B`      | Entity A is a subset of entity B |

## 1. Coreference Types

We annotate two types of coreferential relationships: **identitfy coreference** and **subset-set relations**. They are annotated in two separate layers: 
- _**Coreference**_ layer for _identity coreference_, where coreference mentions are linked in a transitive chain;
- _**Coreference Subset**_ layer for _subset-set relations_, where subset-sets are linked by directed edges.

## 2. Coreference Mention Labels
A coreference mention is a span of text that is involved in some coreferential relationship. For a coreference mention, there are six types of concept labels: 
1. `entity`: the mention is an entity, most noun phrases fall into this category, pronouns refering to an entity should also be labeled as an entity. 
   - Do not annotate singletons, i.e. there is no other coreference for the same entity.
   - Alignment: align the span with whatever is needed for coreference. For example, the entire noun phrase _my dog_ is coreferenced with _it_, while **my** is linked to **I**.
       > [_[**My**] dog_] is naughty. [_It_] keeps messing up the room and [**I**] have to clean the house.
2.  `event`: the mention is an event, most verbs/actions and occasionally nouns (e.g. event nominals) fall into this category, pronouns refering to an event should also be labeled as an event. 
    - Alignment: for verb phrases, align everything from '_be_' to the main predicate (i.e. head verb) with the concept (e.g. _**am surprised**_). 
      > I [_am surprised_] by the news. 
    - Event nominals should be labeled as event, and aligned following the standard for `entity` (i.e., the entire span needed for the coreference; e.g. _**The drastic fluctuation**_). Note that the two _fluctuate_ events have an identity coreference relation.
      > The stock price [_**fluctuated**_] drastically in the past few weeks. [_**The drastic fluctuation**_] was not expected by most people.
3.  `gen-entity`: the mention is a generic entity, e.g. [_Doctors_] help [_doctors_].
4.  `doc-situation`: the mention is refering to the situation described in the document. 
      - In the below example, **_this_** is refering to the combination of events described prior to it, and we could not easily identify an event that could well-represent the summary of such situation. In this case, label _this_ as `doc-situation`.
         > I feel like the school is stressful recently. I failed three exams out of five. I am having a hard time. My dog got sick and I don't have time to take care of him, partly due to the college. [_**This**_] is driving me crazy. 
      - Singletons should be annotated with this label, i.e. the mention could appear on its own and not linked to other mentions. However, if there are multiple mentions, we should still link the mentions in a coreference chain. The same applies for the `post` label.
5.  `post`: the mention is refering to the Reddit post.
      - Note the difference between `doc-situation` and `post`. While the prior is referring to the situation described in the post, the later is referring to the post itself. 
        > I feel like the school is stressful recently. I failed three exams out of five. I am having a hard time. My dog got sick and I don't have time to take care of him, partly due to the college. Thank you for reading [**_this_**].


### Note: Singletons

Do not annotate entities or events with no coreference. Exceptions are _post_ and _doc-situation_, they could appear as singletons, but they should also be linked if their are multiple mentions.

### Note: Generic _You_

Generic _you_ occurs frequently in the Reddit data. To distinguish between the generic and non-generic _you_'s, we can run the following tests. Passing one or both of the tests is a signal that the _you_ might be generic and should be labeled as `gen-entity`.

Example 1 (generic): 
> Brushing [**your**] teeth is healthy.

Example 2 (non-generic): 
> I hope [**you**] can get some good rest.

**Test 1:** Can we substitute _you_ with _one_ without changing the sentence meaning? If so, it is likely generic.
- Example 1 passes this test as we can say "Brushing [_**ones**_] teeth is healthy" without changing the meaning.
- Exmaple 2 does not pass this test. "I hope one can get some good rest" does not mean the same thing.

**Test 2:** Can _you_ include the speaker of the sentence? If so, it is likely generic.
- Example 1 passes this test since the statement of brushing teeth is healthy applies to both the hearer and the speaker.
- Example 2 does not pass this test.

### Note: Spans
The general principle for spans is to include whatever is needed for the coreference. It does not need to be the complete noun phrase. However, there are some rules when deciding the spans for verbs:
   - In most cases, we annotate the span of the head verb including copula and tense, but not modals.
      > Mary [was working] on the homework.
   - Copula (_be_) and everything between the copula and the head verb should be annotated (including adjectives)
      > Mary [is always working] on the homework.
   - However, if there is no copula, only the head verb is annotated (do not include adjectives in this case)
      > Mary always [work] on the homework.
   - Modals like _have_, _must_, _should_ are not included in the span.
      > Mary must [work] on the homework. \
      > Mary have [been working] on the homework.
   - A special case is _light verb_, where the semantic meaning is not stored in the verb but some additional expression (e.g. _take a bath_, the meaning is conveyed through the _bath_ instead of _take_). We should annotate the light verb _plus_ the expression that actually conveys the meaning. 
      > I [took a bath]. \
      > The car [is heading towards] the city.


## 3. Coreference Relations

### 3.0. General principle

Relations (either identity or subset) should occur between mentions with the same label types (e.g. entity to entity, gen-entity to gen-entity, event to event). DO NOT connect mentions with different labels._

### 3.1. Identity Coreference  

Identity coreferences are annotated on the _coreference_ layer where all the coreference mentions of the same concept are linked in a transitive chain. There is no need to specify the relationship in this layer.
The relation A -- B -- C represents A, B, and C are mentions of the same concept.
> A --- B --- C

   - Base case:
       > [_**The little boy**_] heard a noise outside and [_**he**_] went out to check. Surprisingly, [_**the boy**_] did not see anything. So [_**he**_] closed the door and went back to sleep.
   - Embedded case: the entire noun phrase _my dog_ is coreferenced with _it_, while **my** is linked to **I**.
       > [_[**My**] dog_] is naughty. [_It_] keeps messing up the room and [**I**] have to clean the house.
   - **Date and time** should also be linked. 
       > I will meet with you at [_**three o'clock**_]. By [_**that time**_] you should finish all the work. 
   - **Negated existentials** should also be linked. 
       > _**Nobody**_ took a picture of _**themselves**_.
       - Note that to ensure consistency, we should align the entire span of the NP **including the negation** with the mention. 
           > [_**Some boys**_] took out [_**their**_] camera, but [_**no boy**_] took a picture of [_**himself**_].
   - **Generic and underspecified** coreference
       - We annotate generic/underspecified entities as long as there is a clear coreference relation. In the example below, it is clear that the two _people_ are refering to the same group of entities. Thus, we should label both mentions as generic entity and link them with an identity relation.
           > [_**People**_] nowadays seem to be mad. [_**People**_] are always overwhelmed.
   - **Quotations** should be dealt carefully since the speaker changes. 
       >  [_**He**_] said to me: " Mary and  [_**I**_] are going to get married next month."
   - **Important Note**: having of the same shape/spelling does not guarantee a coreference relationship. Spans should be conceptually referring to the same thing in order to be an identity coreference. In the following example, there are three occurrances of _the toy_, but only the first one is coreferenced with _my doll_.
       > I like [_my doll_]. [_The toy_] has beautiful eyes and clothes. My mom bought [_it_] at _the toy_ shop. I once heard someone said that the best childhood fantasy comes from _the toy_ you cherish. 
  - **Modifiers** should be annotated only when they are proper nouns. 
       - For example, the modifier _Facebook_ is extracted for the coreference relationship because it is a proper noun.
            > The [**Facebook**] employee complained about his work though he like the working environment at [**Facebook**]. (coref) 
       - We **DO NOT** annotate if the form of the proper noun changed when acting as a modifier, as in _Mexican_ with respect to _Mexico_.
            > I like [**Mexican**] food. I want to visit [**Mexico**] one day. (no coref)

Other things we **DO NOT** annotate:

   - **DO NOT** annotate appositives. An example of appositives is as follows.
       > [John (NP)], [a scientist (apposition)], works at the CDC. (appositive, no coref)
       - Sometimes and often in news reports, the apposition occurs in front of the noun phrase, we do not annotate these forms either.
            > [West Ham Defender (apposition)]  [Zoe Joey (NP)] entered the room. (appositive, no coref)
   - **DO NOT** annotate attributive uses since they are represented in argument-predicate structures.
       > _**New York**_ is _**a big city**_. (attributive, no coref)

       > _**That**_ is the _**movie**_ I told you yesterday. (attributive, no coref)
   - Similarly, **DO NOT** annotate expletive uses.
       > _**It**_ is okay to _**be sad**_. (expletive, no coref) 


### 3.2. Subset Relation

The subset relation is used to mark a set of entities/events that belong to another set of entities/events. 
The relation A subset B represents A is a subset of B:
> A --(subset)--> B

If the entity or event has multiple identity coreferences, we annotate the subset relation only once. Connect the subset relation with the first mention.

If there are chains of subset relations, e.g. A is subset of B, both A and B are subsets of C, we only annotate the relations for A subset B subset C but not A subset C, as follows:
> A --(subset)--> B --(subset)--> C.

 - Example 1: subset relationship between entities     
     - In this example, entity _**The boy**_ and  _**he**_ are both subsets of _**the  students**_. 
        > _**The boy**_ studied hard every night but  _**he**_ still got the lowest grade among _**the  students**_.
        
        Relation(s): [The boy] --> [the students]
     - Subset is also used for groupings
        > **_Mary_** and **_John_** are married. _**They**_ will move into a new house next month.
       
       Relation(s): [Mary] --> [They]; [John] --> [They]
 - Example 2: subset relationship between events
     - In this example, event _**lied**_ and _**did**_ are both subsets of _**the  lies**. 
        > The girl  _**lied**_ to the teacher and the boy  _**did**_ the same. The teacher is irritated by _**the  lies**_. 
        
        Relation(s): [lied] --> [the lies]; [did] --> [the lies]
 - Example 3: subset relationship involving nested/embedded spans
     - In the following example, _most of my group_ is a subset of _my group_ and should be linked by the subset relation. _most of my group_ is also involved in the identity coreference relation with _they_.
        > [_Most of [**my group**]_] do not like the design. [_They_] think it does not express the meaning well. 
        
        Relation(s): [Most of my group] --> [My group]
