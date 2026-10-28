# Ghost Stories Are Never Just About the Dead

Master's thesis · Meng-Yu Chiu · KAIST Graduate School of Culture Technology · 2026

**Gendered Portrayals of Ghosts: An Analysis of 21,242 Texts Across Three Languages**

This was my master's thesis at KAIST's Graduate School of Culture Technology.<br />I wanted to explore similarities and differences in how people across cultures describe ghosts. I brought together **21,242** online ghost stories from PTT, TheQoo, and Reddit, representing different cultural contexts, and used **natural language processing (NLP)** to study **how ghosts of different genders are portrayed**. I built a workflow combining lexical rules, LLMs, and human validation, including domain-specific lexicons of ghost-story terms that other researchers can use, extend, or adapt.

[Notion portfolio: 中文 / English](https://app.notion.com/p/1bdfea401f5a81829bd0dd489be61d51)

## 1. Research Questions and Motivation

While reading ghost stories from Taiwan, the West, and Korea, I noticed that **female ghosts in white clothing** appeared repeatedly across languages and cultural settings. This made me wonder: **Why do people use similar images and words to describe the unknown? Do these descriptions reflect the gender roles and social norms that are repeatedly emphasized and projected within the storytellers' cultural contexts?**<br />In this study, I approach **ghost stories as social representations**: narratives that emerge as **people draw on familiar ideas about gender, kinship, and social roles to make sense of death and the unknown**. Descriptions of a ghost's appearance, setting, and haunting behavior turn abstract ideas into a presence that can be seen, heard, or felt. Studying these recurring details offers a way to understand how gender and social norms enter everyday storytelling.<br />My literature review showed that quantitative studies of folktales and fiction had identified cultural gender inequalities in descriptions of appearance, agency, and character relationships. Qualitative research on ghosts offered rich ethnographies and interpretations of legends, film, and television. One question had received less attention, yet was central to my research: do gendered descriptions of ghosts also recur across large collections of contemporary online stories, and do they form similar or different narrative patterns across cultural contexts?<br />I therefore focused on three questions:<br />1. **Are female and male ghosts placed in different story settings, creating gendered spaces?<br />2. Are male and female ghosts described differently in terms of color, state, and behavior?<br />3. Do narrative patterns differ or recur across cultures and platforms?**

## 2. My Role and Responsibilities

I met weekly with my supervisor, Prof. Juyong Park, to discuss progress and questions arising from the research. He emphasized developing the ability to conduct research independently and offered advice based on my weekly work and the problems I encountered. **I independently defined the topic, designed the study, collected and cleaned the corpus, developed and ran the multilingual classification workflow, manually annotated the data, and conducted the statistical analyses. I then wrote and revised the thesis based on the findings.**

## 3. Data

I wanted to examine **how people today describe and make sense of ghosts**, so I focused on online forums where users share ghost stories anonymously or under pseudonyms. These accounts are rooted in everyday storytelling and undergo less editorial filtering than published collections, offering a closer view of how people imagine supernatural beings today. To keep the scope more comparable, I selected stories labeled or presented as firsthand experiences. My premise was that, if gendered narrative patterns recurred even in accounts presented as personal experiences, this would strongly suggest that descriptions of ghosts draw on cultural gender norms that storytellers project into their narratives.

I collected **22,393 public posts** and retained **21,242 usable texts** after removing posts without body text.

| Platform / language | Selection and collection method | Post date range | Collected posts | Usable texts |
| --- | --- | --- | --- | --- |
| PTT / Traditional Chinese | Marvel posts with “experience” (經驗) in the title; BeautifulSoup4 | 2003-03-09<br />to 2025-09-08 | 15,759 | 14,610 |
| TheQoo / Korean | The horror board's “real experience” (실제경험담) category; Selenium | 2020-08-18<br />to 2025-04-01 | 967 | 965 |
| Reddit / English | Text-based accounts of users' paranormal experiences in r/Paranormal and r/Ghoststories; PRAW API | 2024-11-11<br />to 2025-09-08 | 5,667 | 5,667 |

The collected fields include titles, body text, and source URLs, with the analysis focused on body text. Posts containing only images or videos, without text to analyze, were excluded from the research corpus.

The unit of classification is the **entity mention**: one occurrence of a human character or supernatural presence in a story. I retained the sentence containing each mention and two sentences on either side to classify its gender and state—for example, whether it refers to a living person, someone deceased, or a supernatural presence appearing or interacting with the living. Repeated references to the same character within one story produce multiple records.

When comparing the settings, colors, and haunting methods associated with female and male ghosts, I used **whether the theme appeared within an article** as the criterion. Each article is counted at most once per gender and theme, reducing duplicate counts from repeated references to the same character in a long story. A story featuring both female and male ghosts can still be counted once in each gender group.

I also created a **human validation set of 498 entity mentions** to assess the Cascade classifier's performance. It contains 166 mentions from each platform, sampled across the rules' initial Female, Male, and Unknown labels.

## 4. Tools and Outputs

| Tool | Purpose and output |
| --- | --- |
| Python, BeautifulSoup4, Selenium, PRAW | Collect and organize texts, segment sentences, extract entity mentions, and produce analytical data and figures |
| jieba, Kiwi, spaCy | Tokenize each language and filter parts of speech to prepare words for collocate analysis |
| Claude API | Classify cases the rules cannot resolve, recording labels, evidence, and confidence indicators |
| gensim | Build separate LDA and Word2Vec models for each platform; export topic words and semantic neighbors |
| R | Conduct formal classifier evaluation, statistical tests, effect-size and confidence-interval calculations, and prepare thesis result tables |

## 5. Analysis Process

![Research workflow from corpus collection through rules, LLM classification, human validation, and narrative analysis](figures/research_workflow_en.png)

Classification covers two tasks: gender (Female, Male, Unknown) and state (Alive, Deceased, Supernatural, Unknown). The rule-based classifiers first handle cases with explicit lexical cues. Cases requiring more context go to Claude Haiku, with Sonnet as a fallback when uncertainty remains. Cases without enough evidence retain the Unknown label.

After classification and validation, I used log-likelihood ratio (LLR) analysis to identify words disproportionately associated with female- or male-ghost contexts, then organized them into space, color, and haunting-method themes. LDA provided a cross-check on the suitability of these themes. Word2Vec and close reading helped me interpret the meanings of particular words within ghost stories.

## 6. Key Findings

### ① Ghost gender distribution differed across platforms, with a small effect size

Among supernatural entity mentions, **male ghosts accounted for 51.7% on PTT, compared with 39.4% for female ghosts**. On Reddit, female ghosts accounted for 46.5%, slightly above 43.7% for male ghosts. On TheQoo, female ghosts accounted for 33.4% and male ghosts for 16.1%, but **50.5% of mentions could not be reliably assigned a gender**.

After excluding Unknown, the association between platform and ghost gender was significant under both counting approaches, but Cramér’s V was about **0.10**, indicating a small effect. The corpora show different narrative tendencies, but these results are insufficient to treat those tendencies as fixed traits of entire cultures.

![Gender distribution of supernatural entities across three platforms, counting mentions and deduplicating by article and gender](figures/ghost_counts_raw_pipeline.png)

The top row counts mentions. The bottom row counts each article at most once per gender category.

### ② Gendered settings

I used LLR collocate analysis to identify words disproportionately associated with female- or male-ghost contexts. **On PTT, male-ghost collocates included “squad leader,” “military service,” and “company commander”**. **On TheQoo, female-ghost collocates included bedrooms, beds, and sleep-related terms**.

![Words associated with female- and male-ghost contexts across three platforms](figures/collocate_LLR_divergence_3platforms_v5.png)

The bars show relative association with female- or male-ghost contexts, rather than raw word counts. Collocate significance in this figure uses BH-FDR correction for multiple comparisons. The thematic comparisons of settings, colors, and haunting methods use the separate article-level tests reported in the thesis.

I then compared the share of articles associated with each ghost gender in which a setting theme appeared.

| Platform / setting | Female-ghost articles | Male-ghost articles | Comparison |
| --- | --- | --- | --- |
| TheQoo: indoor / domestic | 19.78% | 5.83% | p = .0025; higher among female-ghost articles |
| Reddit: indoor / domestic | 60.22% | 54.27% | p = .0002; higher among female-ghost articles |
| PTT: military setting | 2.29% | 4.61% | p < .001; higher among male-ghost articles |

I interpreted these results through literature on public/private divisions and the distinction between spaces within and outside the household. Homes and bedrooms connect with family roles, while military settings connect with hierarchy, discipline, and male authority. Word2Vec neighbors of military terms and close reading revealed recurring contexts involving military law, death, and historical violence. These findings allowed me to examine how settings carry gender and power relations and reveal gendered ways of imagining ghosts.

### ③ Similar ghost images can carry different gendered and cultural meanings

**White was significantly associated with female ghosts on PTT and Reddit**, but not on TheQoo. Combining Word2Vec findings with close reading, I compared the different contexts behind these similar portrayals. Korean white-clothed female ghosts connect with traditional white mourning clothes and the difficulty of belonging to a family lineage after dying unmarried. Western White Lady narratives often center on romantic betrayal and revenge against the betrayer after death, carrying a sense of reclaiming agency. Even when both figures wear white, their meanings need to be understood through their own stories and cultural contexts.

**Red was also significantly associated with female ghosts on PTT (p = .0307)**. In the thesis, I discussed how red connects with resentment and revenge in particular contexts, contrasting with its everyday associations with celebration and good fortune and reflecting a distinctive aspect of Taiwanese folk culture.

**Haunting methods also showed gender differences, though not every behavior was significantly associated with gender**. Sound appeared in 30.08% of female-ghost articles and 27.05% of male-ghost articles on PTT, and in 32.06% and 27.57%, respectively, on Reddit. Both comparisons were significant; TheQoo's was not. Touch was significantly associated with female ghosts on TheQoo, but this involved only 16 female-ghost articles and 2 male-ghost articles.<br />Drawing on crying, screaming, and other terms identified through LLR and Word2Vec, together with story examples, I interpreted depictions of **female ghosts drawing attention to themselves through sound** as a narrative way for women to reclaim expression and agency after death.

**These findings suggest that people make sense of the unknown through familiar social roles and norms, describing gendered ghosts in concrete terms through their appearance, settings, and haunting behavior.** These portrayals continue to shape how ghosts are imagined.

## 7. Challenges and Lessons

- **Defining how to classify an entity's gender and state was a major challenge**. For example, “my late grandmother” and “my late grandmother appeared in my older brother's dream” require different state labels for the entity “grandmother”: the former is labeled Deceased, while the latter is labeled Supernatural. Similarly, the Taiwanese expression 好兄弟, literally “good brothers,” can refer to ghosts collectively without specifying that they are male. To help the classifiers distinguish gender and state more accurately, I developed domain-specific lexicons for the classification categories. These include recurring character terms and culturally specific names for ghosts observed in the stories. I also added Unknown to avoid forcing a label when evidence was insufficient and introducing errors into the final results.
- **Validating classification accuracy was another challenge**. In particular, how could I establish that the Cascade classifier, combining rules and LLMs, performed better and produced more accurate labels than rules alone? I used stratified sampling and manually annotated 498 entity mentions to compare the two workflows. I also used an LLM-as-judge approach, asking Claude Sonnet to label another 498 examples as a supplementary reference, while keeping human annotation as the primary basis for evaluation. The results showed that the Cascade classifier performed better than the rule-based classifier. The study helped me see why results need to be accompanied by evidence that the method is valid and a clear explanation of why it was chosen over the alternatives, so the value of the research can be understood.
- One of the most important lessons from the thesis was also easy to overlook: **data and numbers always need to be interpreted in context**. LLR can identify associated words, but a word list alone cannot explain their meanings within a story. I returned those words to the ghost stories they came from and used the literature to supply the context missing from the lists. Combining quantitative analysis with qualitative reading helped me understand gendered portrayals of ghosts and develop interpretations grounded in their cultural meanings.

## Repository Guide

The repository contains research notebooks and selected thesis figures. The raw posts, completed human annotations, intermediate CSVs, trained models, and thesis PDF are not included.

| File | Role in the research |
| --- | --- |
| [02_gender_ghost_analysis.ipynb](notebooks/02_gender_ghost_analysis.ipynb) | Load texts, extract mentions, apply rules and LLM fallbacks, export annotations and collocates; also contains exploratory analyses |
| [01_haunted_space_gender_distribution.ipynb](notebooks/01_haunted_space_gender_distribution.ipynb) | Space, color, and haunting-method comparisons, article-level presence checks, and text retrieval for close reading |
| [03_topic_modeling.ipynb](notebooks/03_topic_modeling.ipynb) | Separate LDA models for each platform and cross-platform topic-to-theme mapping |
| [04_word2vec_LLR_thematic.ipynb](notebooks/04_word2vec_LLR_thematic.ipynb) | Separate Word2Vec models, thematic keyword neighborhoods, vocabulary coverage, and semantic comparisons |
| [05_statistical_analysis.Rmd](notebooks/05_statistical_analysis.Rmd) | Formal classification evaluation, paired comparisons, confidence intervals, and thesis statistical tables |

## Methods and Reported Results

The results below are reported in the 2026 thesis, *Ghost Stories Are Never Just About the Dead: A Cross-Cultural NLP Analysis of Gendered Narrative Patterns*, by Meng-Yu Chiu, supervised by Prof. Juyong Park at KAIST. Corpus selection, date ranges, and counts come from Section 3.1; counting units and human validation from Section 3.2 and Tables 3.3–3.4; classifier metrics from Tables 4.1–4.5; gender distributions from Figure 4.1 and Table 4.6; collocates from Figure 4.2 and Table 4.7; thematic comparisons from Tables 4.10–4.12; semantic context from Section 4.8. Cultural interpretations draw on Sections 5.1–5.5, with the broader conclusions and limitations in Sections 6.1–6.3. These interpretations combine textual evidence and prior literature; they are not direct tests of cultural causes or reader effects.

### Classification and validation

- Classification operates on mentions with local context, not on complete stories or uniquely identified individuals. Gender has three labels: Female, Male, Unknown. State has four: Alive, Deceased, Supernatural, Unknown.
- Rules handle explicit cues. Unresolved cases go to Claude Haiku, followed by Sonnet when the answer is Unknown or confidence is low. The implementation retains method, confidence, and evidence fields. Notebook prompts use local context with character limits in the API helpers.
- The human reference contains 498 mentions: 166 per platform. Sampling was stratified using rule-based gender labels. It is a validation sample, not a population-weighted estimate of corpus-wide accuracy.
- Formal evaluation includes Unknown as a class. Earlier exploratory evaluation cells in notebook 02 use narrower label subsets; the full-label evaluation is implemented in the R Markdown file.

| Task | Method | Macro-F1 | Bootstrap 95% CI | Cohen's κ |
| --- | --- | --- | --- | --- |
| Gender | Rules only | 0.8846 | 0.8534–0.9107 | 0.8331 |
| Gender | Cascade | 0.9397 | 0.9138–0.9615 | 0.9266 |
| State | Rules only | 0.4503 | 0.3947–0.5064 | 0.3787 |
| State | Cascade | 0.6546 | 0.5519–0.7288 | 0.5371 |

The exact McNemar comparison uses paired predictions on the human reference: gender b = 36, c = 6; state b = 58, c = 0; both p < .001. Here, b counts errors corrected by the cascade and c counts new errors introduced by it. A zero c does not mean the classifier made no errors overall.

A separate 498-mention Sonnet reference provides a supplementary comparison: gender Macro-F1 0.8505, κ 0.8773; state Macro-F1 0.4796, κ 0.3347. It complements human annotation and does not replace it. The cascade and supplementary annotator both use models from the Claude family.

### Narrative analysis

- LLR compares content words around female and male supernatural mentions, with language-specific tokenization, stopword filtering, and BH-FDR correction for collocate tests. Pronouns and kinship references are filtered to reduce direct gender-reference effects; domain-specific ghost terms remain visible in the published figure.
- Thematic comparisons use article-level presence of space, color, and haunting-method keywords. The thematic p-values cited above are the individual tests reported in thesis Tables 4.10–4.12; the LLR figure's BH-FDR qualification does not describe those separate tests.
- LDA models were fitted separately for PTT (10 topics), TheQoo (8), and Reddit (7). They provide a cross-check using the same corpora, not a held-out validation set. Color did not consistently emerge as a dominant topic, so its interpretation also uses close reading and prior literature.
- Word2Vec was trained separately for each platform using skip-gram, 200 dimensions, window 5, minimum count 3, and 10 epochs. The models provide semantic neighborhoods within each corpus; they do not create a shared aligned embedding space across languages.
- The retained gender-distribution figure shows both mention counts and counts deduplicated by article and gender. Its article percentages use the sum of category counts as the denominator. An article can contribute to several categories.

## Working With the Notebooks

These are research notebooks with local and Google Colab/Drive paths. To run them, configure their input and output paths and provide the text and intermediate files expected by each notebook.

1. Install the core Python packages:

   ```bash
   python -m pip install -r requirements.txt
   jupyter lab notebooks/
   ```

   Additional packages, language resources, fonts, and R dependencies are declared in the individual setup/import cells. `requirements.txt` covers the core Python stack, not every dependency used in every exploratory cell. The R file lists its required packages at the top.

2. Start with notebook 02 to review raw-text paths, mention extraction, classification settings, and annotation export. Provide `ANTHROPIC_API_KEY` through the environment to use Claude, then review the configured backend and model names. The shown configuration reads the environment variable; it does not automatically load a `.env` file.

3. Complete the exported human annotation task and provide the completed annotation and method-mapping files for formal evaluation. These labels are not supplied in this repository.

4. Use notebook 01 for thematic comparisons, 03 for LDA, and 04 for Word2Vec. Review their input dependencies before execution, then use the R Markdown file for formal evaluation and result tables.

With the LLM backend disabled or unavailable, the configured workflow can fall back to rules. That produces a different classification condition from the reported cascade results.

## License

Code is released under the MIT License; see [LICENSE](LICENSE). Forum texts remain subject to their authors' rights and the platforms' terms, and are not redistributed here.
