# Multi-layered Cross-genre Corpus

The multi-layered cross-genre corpus (MLCG) is a comprehensive and diverse collection of texts that encompasses various genres, such as news articles, children's stories, and Reddit posts. This corpus has been specifically annotated at multiple layers to facilitate in-depth analysis and exploration of the texts' coreference resolution, causal relations, and temporal relations.

The MLCG corpus includes a wide array of text types, allowing researchers and language enthusiasts to study and compare the characteristics of different genres. The genres represented in the corpus have distinct stylistic and structural features that present unique challenges for both human annotators and machine learning models.

For instance, children's stories in the corpus exhibit a linear temporal structure and clearly defined causal relations, enabling a coherent narrative flow. On the other hand, news articles often employ non-linear temporal sequences, incorporating minimal first-person pronouns or conditional language to provide factual information. Reddit posts, in contrast, are characterized by author-centered explanations of ongoing situations, occasionally referencing the meta-textual aspects of the platform.

The annotation schemes used in the MLCG corpus have been carefully adapted from existing work to suit a broad range of text types. By incorporating annotations for coreference resolution, causal relations, and temporal relations, the corpus provides valuable insights into the interplay between different forms of semantic information within and across genres.

Researchers can leverage the MLCG corpus to explore the diverse textual characteristics and uncover the nuances associated with each genre. The availability of this corpus under the open-source Apache 2.0 license encourages collaboration, fosters advancements in natural language processing, and supports the development of more effective machine learning models and language understanding systems.

## Corpus Breakdown

| |Causal|Coref|Temporal|
|---|---|---|---|
|CNN[^1]|50|50|50|
|Fables[^2]|50|50|50|
|Reddit[^3]|100|100|150|
|Reuters[^4]|50|50|50|
|Wind in the Willows[^2]|-|-|50|
|Wizard of Oz[^2]|50|50|50|
|**Total**|300|300|400|

All data is tokenized using the ELIT Tokenizer[^5] and filtered to a length of 100-200 tokens. Reddit posts are additionally filtered using the Profanity-Check Python module[^6].

## Contact

* [Jinho D. Choi](https://www.emorynlp.org/faculty/jinho-choi)

[^1]: https://huggingface.co/datasets/cnn_dailymail
[^2]: https://www.gutenberg.org/
[^3]: https://github.com/emorynlp/reddit-college
[^4]: https://www.kaggle.com/datasets/nltkdata/reuters
[^5]: https://github.com/emorynlp/elit-tokenizer
[^6]: https://github.com/vzhou842/profanity-check
