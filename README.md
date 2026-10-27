# Ghost Stories Are Never Just About the Dead

Master's thesis · Meng-Yu Chiu · KAIST Graduate School of Culture Technology · 2026

**Gender in Ghost Stories: An Analysis of 21,242 Texts Across Three Languages**

For my master's thesis at KAIST's Graduate School of Culture Technology, I analyzed ghost stories from PTT, TheQoo, and Reddit to study how ghosts of different genders are described. I built an analysis workflow combining lexical rules, LLMs, and human validation. On 498 manually annotated entity mentions, gender classification reached a Macro-F1 of **0.94**.

[Notion portfolio: 中文 / English](https://app.notion.com/p/1bdfea401f5a81829bd0dd489be61d51)

## 1. Research Questions and Motivation

While reading ghost stories on PTT, TheQoo, and Reddit, I noticed that female ghosts in white clothing appeared repeatedly across languages and cultural settings. I wondered why people use similar images to describe unfamiliar beings, and how these stories bring in gender roles and social norms from everyday life.

I approached ghost stories as social representations: people draw on familiar ideas about gender, kinship, and social roles to make sense of death and the unknown. Through a ghost's appearance, setting, and haunting behavior, abstract ideas become something that can be seen, heard, or felt. Studying these recurring details offers a way to understand how gender expectations and social order enter everyday storytelling.

My literature review showed that quantitative studies of folktales and fiction had identified gender biases in appearance, agency, and character relationships. Research on ghosts offered rich interpretations through ethnography, legends, and film. Less systematically examined was whether these gendered descriptions recur across large collections of contemporary online stories, and how their patterns compare across cultural contexts.

Cross-cultural comparison also requires attention to differences. The Western public/private distinction and the East Asian inner/outer distinction both connect gender with space, but have different historical and cultural backgrounds. I chose online forums where users share their own stories to examine contemporary narratives, comparing Traditional Chinese, Korean, and English texts to explore which patterns recur and which need to be understood within their particular contexts.

I therefore focused on **whether female and male ghosts appear in different settings and are described through different appearances and actions, and whether these differences recur across platforms in different languages**. I organized the analysis around ghost gender distribution, space, color, and haunting methods, combining text analysis with close reading and the literature to interpret recurring narrative patterns.

## 2. My Role and Responsibilities

Under the supervision of Prof. Juyong Park, I was responsible for the research design, corpus collection and cleaning, multilingual classification workflow, manual annotation, statistical analysis, figures, and thesis writing. I used Claude and Claude Code to assist with implementation; I was responsible for the research questions, classification definitions, human annotations, and interpretation.

The project required working with both texts and numbers. I translated concepts from cultural research into variables that could be labeled and compared, then returned to the stories and literature to assess which interpretations the statistical results could support.

## 3. Data

I wanted to examine how people today describe and make sense of ghosts, so I chose online forums where users share stories anonymously or under pseudonyms. These provide everyday narratives with less editorial filtering than published collections. To keep the scope more comparable, I focused on stories presented as firsthand experiences, using each platform's categories or community rules to select them. “Firsthand experience” describes how the posts are framed; the research examines how the stories are told.

I collected **22,393 public posts** and retained **21,242 usable texts** after removing posts without body text.

| Platform / language | Selection and collection method | Post date range | Collected posts | Usable texts |
| --- | --- | --- | --- | --- |
| PTT / Traditional Chinese | Marvel posts with “experience” (經驗) in the title; BeautifulSoup4 | 2003-03-09<br />to 2025-09-08 | 15,759 | 14,610 |
| TheQoo / Korean | The horror board's “real experience” (실제경험담) category; Selenium | 2020-08-18<br />to 2025-04-01 | 967 | 965 |
| Reddit / English | Text-based accounts of users' paranormal experiences in r/Paranormal and r/Ghoststories; PRAW API | 2024-11-11<br />to 2025-09-08 | 5,667 | 5,667 |

The collected fields include titles, body text, and source URLs, with the analysis focused on body text. Other users' replies were removed from PTT posts. Posts containing only images or videos, without text to analyze, were excluded from the text corpus.

Classification uses **entity mentions**: individual occurrences of a human character or supernatural presence in a story. I retained the sentence containing each mention and up to two sentences on either side to classify its gender and whether it refers to a living person, someone deceased who is only being mentioned, or a supernatural presence appearing or interacting in the story. Repeated references to the same character can produce several records within one story.

For settings, colors, and haunting methods, I instead examined **whether a theme appeared within an article**, counting each article at most once per gender and theme. This reduces the influence of repeated references to a character in a long story. A story featuring both female and male ghosts can still contribute to both groups.

I also created a **human validation set of 498 entity mentions**, with 166 from each platform, sampled across the rules' initial Female, Male, and Unknown labels. These records were used to assess classification quality; they were not an additional 498 stories.

The platforms differ in their collection periods, corpus sizes, and user populations. Reddit's English-language posts are also not a direct sample of the US population. The results therefore describe narrative patterns in these corpora, and cross-platform differences need to be interpreted within those limits.

## 4. Tools and Outputs

| Tool | Role and output |
| --- | --- |
| Python, BeautifulSoup4, Selenium, PRAW | Collect and organize texts, segment sentences, extract entity mentions, and produce analytical data and figures |
| jieba, Kiwi, spaCy | Tokenize each language and filter parts of speech to prepare words for collocate analysis |
| Claude API | Classify cases the rules cannot resolve, recording labels, evidence, and confidence indicators |
| gensim | Build separate LDA and Word2Vec models for each platform; export topic words and semantic neighbors |
| R | Conduct formal classifier evaluation, statistical tests, effect-size and confidence-interval calculations, and prepare thesis result tables |

## 5. Analysis Process

![Research workflow from corpus collection through rules, LLM classification, human validation, and narrative analysis](figures/research_workflow_en.png)

Classification covers two tasks: gender (Female, Male, Unknown) and state (Alive, Deceased, Supernatural, Unknown). Rules handle cases with explicit lexical cues. Cases requiring context go to Claude Haiku, with Sonnet as a fallback when uncertainty remains. Cases without enough evidence retain the Unknown label.

After classification and validation, I used log-likelihood ratio (LLR) analysis to identify words that occur disproportionately in female- or male-ghost contexts, then organized them into space, color, and haunting-method themes. LDA provided a cross-check on the themes; Word2Vec and close reading helped interpret what the words meant within the stories.

## 6. Key Findings

### ① Ghost gender distribution differed across platforms, with a small effect size

Among supernatural entity mentions, male ghosts accounted for 51.7% on PTT, compared with 39.4% for female ghosts. On Reddit, female ghosts accounted for 46.5%, slightly above 43.7% for male ghosts. On TheQoo, female ghosts accounted for 33.4% and male ghosts for 16.1%, but **50.5% of mentions had an unknown gender**. That uncertainty needs to be considered alongside the female-to-male proportions.

After excluding Unknown, the association between platform and ghost gender was significant under both mention and article counting, but Cramér’s V was about **0.10**, indicating a small effect. The corpora show different narrative tendencies, but these results are insufficient to treat those tendencies as fixed traits of entire cultures.

![Gender distribution of supernatural entities across three platforms, counting mentions and deduplicating by article and gender](figures/ghost_counts_raw_pipeline.png)

The top row counts mentions. The bottom row counts each article at most once per gender category. An article can contribute to several categories, so the bottom-row percentages do not represent mutually exclusive groups of articles.

In Chapter 5, I drew on stories and the literature to discuss Taiwan's migration history, ancestral worship, and military ghost stories as possible contexts for understanding PTT's higher male-ghost share. These are interpretations of the results; the study did not directly test how much each factor contributed to the gender distribution.

### ② Settings suggest gender roles, with different levels of support across platforms

I used LLR collocate analysis to identify words disproportionately associated with female- or male-ghost contexts. On PTT, male-ghost collocates included “squad leader,” “military service,” and “company commander.” On TheQoo, female-ghost collocates included bedrooms, beds, and sleep-related terms. I then compared the share of articles associated with each ghost gender in which a setting theme appeared.

| Platform / setting | Female-ghost articles | Male-ghost articles | Comparison |
| --- | --- | --- | --- |
| PTT: indoor / domestic | 23.56% | 21.65% | p = .0557; did not meet the .05 significance threshold |
| TheQoo: indoor / domestic | 19.78% | 5.83% | p = .0025; higher among female-ghost articles |
| Reddit: indoor / domestic | 60.22% | 54.27% | p = .0002; higher among female-ghost articles |
| PTT: military setting | 2.29% | 4.61% | p < .001; higher among male-ghost articles |

Each percentage uses the corresponding female- or male-ghost article group within that platform as its denominator, following thesis Table 4.10. TheQoo's indoor / domestic result comes from 36 female-ghost articles and 6 male-ghost articles, so the small counts call for caution.

![Words associated with female- and male-ghost contexts across three platforms](figures/collocate_LLR_divergence_3platforms_v5.png)

The bars show relative association with female- or male-ghost contexts, rather than raw word counts. Collocate significance in this figure uses BH-FDR correction for multiple comparisons. The thematic comparisons of settings, colors, and haunting methods use the separate article-level tests reported in the thesis. They do not use the figure's BH-FDR correction and are best treated as exploratory leads for close reading and further validation.

In Chapter 5, I interpreted these results through literature on public/private and inner/outer divisions: homes and bedrooms connect with family roles, while military settings connect with hierarchy, discipline, and male authority. Word2Vec neighbors of military terms and close reading added context involving military law, death, and historical violence. Together, these sources let me discuss how settings carry gender and power relations while retaining differences across platforms. The results do not support a general claim that female ghosts belong at home and male ghosts outside in every culture.

### ③ Similar ghost images can carry different cultural meanings

**White was significantly associated with female ghosts on PTT and Reddit**, but not on TheQoo. Combining Word2Vec with close reading, I used Chapter 5 to examine the different contexts behind these similar images. Korean white-clothed female ghosts connect with mourning clothes, unmarried status, and family belonging; Western White Lady narratives often center on romantic betrayal and loss. Even when the clothing looks similar, its meaning needs to be interpreted through the particular stories and literature.

Red was also significantly associated with female ghosts on PTT (p = .0307). Chapter 5 uses stories about female ghosts in red to discuss how the color can convey resentment and revenge in a particular narrative context, contrasting with its everyday associations with celebration and good fortune. Black, by comparison, showed no significant gender difference on any platform. Some male ghosts are described as dark figures, but this does not establish black as an exclusively male-ghost trait.

**Haunting methods also differed, but gender associations did not extend to every behavior**. Sound appeared in 30.08% of female-ghost articles and 27.05% of male-ghost articles on PTT, and in 32.06% and 27.57%, respectively, on Reddit. Both comparisons were significant; TheQoo's was not. Touch was significantly associated with female ghosts on TheQoo, but this involved only 16 female-ghost articles and 2 male-ghost articles. Visual appearance and movement showed no significant gender differences on any platform, so differences visible in a chart should not all be treated as stable gender patterns.

In Chapter 5, I combined words such as crying and screaming with story examples to interpret some female ghosts' audible presence as a narrative way for suppressed figures to reclaim expression and agency. In another PTT story examined through close reading, a deceased mother helps a gambler win money in exchange for his promise to care for her child, then punishes him after he breaks that promise. She has supernatural power, yet acts as a mother demanding that someone fulfill a caregiving responsibility.

This also connects with the conclusions in Chapters 5 and 6: **people make sense of the unfamiliar through familiar social roles, then give those roles concrete form through appearance, settings, and haunting behavior**. Identities such as mother, unmarried woman, or soldier continue to organize how ghosts are imagined. This is an interpretation combining textual patterns and the literature. The study did not analyze reader responses, so it cannot establish whether reading these stories changes or reinforces readers' views of gender.

### ④ Adding an LLM improved classification, with a gap between gender and state

The narrative analysis first requires identifying who is being mentioned and whether that entity is a supernatural presence. I compared rules alone with the rules-plus-LLM workflow on the same 498 human-annotated mentions.

| Classification task | Rules-only Macro-F1 | Rules + LLM Macro-F1 | Rules + LLM Cohen’s κ |
| --- | --- | --- | --- |
| Gender: Female, Male, Unknown | 0.88 | **0.94** | 0.93 |
| State: Alive, Deceased, Supernatural, Unknown | 0.45 | **0.65** | 0.54 |

For gender, the cascade corrected 36 errors made by the rules, while introducing errors in 6 cases the rules had classified correctly. A paired exact McNemar test found a significant difference between the workflows (p < .001). This gave me direct evidence of what adding the LLM contributed.

Macro-F1 averages the F1 scores across classes, including Unknown. These results measure classification performance on sampled mentions. The gender score of **0.94** does not mean that 94% of complete stories were classified correctly, or that the entire analysis is 94% accurate. State classification's Macro-F1 of 0.65 remains an important limitation for the subsequent narrative interpretations.

## 7. Challenges and Lessons

### Define the target before choosing a classification method

A passing reference to a deceased grandmother needs a different state label from a grandmother returning to speak with her family. Similarly, the Taiwanese expression “good brothers” can refer to ghosts without specifying gender. I incorporated these distinctions into category definitions, lexical rules, and prompts, and retained Unknown when evidence was insufficient. State classification's Macro-F1 of 0.65 also made the limits that classification quality places on later interpretation clear.

### Establish a checkable standard for automated labels

Another set of automated labels can show whether systems agree, but cannot directly establish correctness. I therefore drew a stratified sample, annotated the mentions myself, and compared both workflows on the same examples, including Unknown. Sonnet labeled another 498 mentions as a supplementary comparison; human annotation remained the primary reference. For collocate analysis, I also added stopwords such as pronouns and kinship terms to reduce the risk of merely repeating gender references.

### Check the denominator when comparing corpora of different sizes

PTT contained 14,610 usable texts and TheQoo only 965, so raw frequency comparisons could reflect corpus size. I examined both mention and article counts, compared theme presence as a share of articles associated with each gender, and reported effect sizes. This helped distinguish statistical significance from a large difference, while keeping TheQoo's smaller sample and high Unknown share in view.

### Return words and model outputs to their narrative context

LLR identifies associated words, but a word list alone cannot explain their meaning in a story. I used Word2Vec neighbors, close reading, and the literature to develop that interpretation. LDA supported some space and haunting-method themes, while color did not consistently form a dominant topic. Interpretation of color therefore relied more on textual examples and prior research. I kept track of what each method could support and adjusted the strength of the argument accordingly.

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
