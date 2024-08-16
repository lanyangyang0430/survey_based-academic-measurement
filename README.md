# survey_based-academic-measurement
## Data Collecting
Specifically, we matched titles using “overview” and “survey,” and
matched abstracts using “Large Language Model,” “LLM,” and related phrases. The detailed rules are shown below:
(1) title:overview, survey,review
(2) abstract:large language models, llm, foundation models,
gpt, sora, bert, bloom, generative pre-training transformer,
transformer, gpt-3.5, gpt-4.0, language models, gpt-3.0, gpt-
2.5, llms
## Data Processing
The data processing mainly involves the following steps:
(1) From the metadata obtained through data collection, we
acquire the arXiv IDs of the articles. Using the arXiv API,
we retrieve the full-text PDFs corresponding to the articles.
(2) We utilize the machine learning library GROBID[? ] for
PDF parsing, resulting in JSON format data containing information such as article title, header, year, abstract, body
text, reference entries, etc.
(3) Since the parsed citation data only contains title, year, and
authors information, we retrieve the paper_id and citationCount through the title of the citation. We utilize the
Semantic Scholar API, using the article title as the search
term. Due to parsing errors in both the parsed citation titles and the stored title data in academic databases (such
as undivided conference names and title fields, incomplete
article titles, etc.), to ensure that the retrieved articles are
indeed the ones needed, we perform the following steps:
• Set the number of returned results to 5.
• Convert both the title in the citation data and the titles
returned from the search to lowercase, then calculate
the Rouge value between them, and save the corresponding title with the maximum Rouge value from
the search data list.
• Exclude all data with Rouge values below 0.8.
After processing, the average citation retention rate per
article is 95.4%, ensuring relatively accurate and sufficient
citation data.
