# Survey_based-academic-measurement
## Data Search Strategy
Specifically, we matched titles using "overview" and "survey" and
matched abstracts using "Large Language Model","LLM","generative pre-training transformergenerative pre-training transformer" and related phrases.
## Data Processing
The data processing mainly involves the following steps:  
(1) From the metadata obtained through data collection, we
acquire the arXiv IDs of the articles. Using the arXiv API,
we retrieve the full-text PDFs corresponding to the articles.  
(2) We utilize the machine learning library GROBID for
PDF parsing, resulting in JSON format data containing information such as article title, header, year, abstract, body
text, reference entries, etc.  
(3) Since the parsed citation data only contains title, year, and
authors information, we retrieve the paper_id and citationCount through the title of the citation. We utilize the
Semantic Scholar API, using the article title as the search
term. Due to parsing errors in both the parsed citation titles and the stored title data in academic databases (such
as undivided conference names and title fields, incomplete
article titles, etc.), to ensure that the retrieved articles are
indeed the ones needed, we perform the following steps:  
• Convert both the title in the citation data and the titles  
returned from the search to lowercase, then calculate
the Rouge value between them, and save the corresponding title with the maximum Rouge value from
the search data list.  
• Exclude all data with Rouge values below 0.8.
After processing, the average citation retention rate per
article is 95.4%, ensuring relatively accurate and sufficient
citation data.
## Normal Q-Q Plot of Our Proposed Survey-based Metrics
![image](https://github.com/lanyangyang0430/survey_based-academic-measurement/blob/main/Normal%20Q-Q%20Plot%20of%20Survey-based%20Metrics/Normal%20QQ%20Plots.png)
## Components of Metrics-combined Prompt
![image](https://github.com/lanyangyang0430/survey_based-academic-measurement/blob/main/Components%20of%20metrics-based%20prompt.png)
The components of prompt.{Data} includes three quantitative metrics: CMT, CDL, MSD, and the Cited Source: specific
information on which surveys have cited the focal paper, input in a dictionary structure. {Metrics Explanation} clarifies the
meaning of the metrics, and Field Explanation explains the specific fields of the Cited Source.
