# German Industrial Automation RAG Assistant

A German-language learning assistant that answers beginner questions about industrial control systems using passages from a small set of technical textbook pages.

## What it does

This project uses retrieval-augmented generation (RAG): it searches the textbook passages for information relevant to a question, then asks a language model to answer using those passages.

The assistant can:

- Search German text by meaning using a pretrained multilingual embedding model.
- Generate an answer in German using Gemini.
- Include source references in answers.
- Say when its source passages do not contain enough information.

## How it works

1. Loads five pages from *Regelungstechnik – Das interaktive Lehrbuch*.
2. Extracts and splits the page text into passages.
3. Creates embeddings with `sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`.
4. Finds relevant passages for the user's question.
5. Sends those passages to `gemini-3.5-flash-lite` to generate a grounded answer.

The embedding model is pretrained; this project does not train or fine-tune a model.

## Technology

- Python
- Google Colab
- Requests and BeautifulSoup
- Sentence Transformers
- Google Gemini API


The notebook reads the API key from Colab Secrets. 

## Initial manual evaluation

I tried four hand-picked questions:

| Question type | Expected behavior | Result |
|---|---|---|
| Explain a two-point controller | Give a source-supported explanation | Pass |
| Compare two-point and three-point controllers | Explain the difference with citations | Pass |
| Name the four controller-quality criteria | List the four criteria with a citation | Pass |
| Ask about CNC maintenance intervals | Say the sources do not provide enough information | Pass |

This is a small functional check, not a large benchmark or proof of general accuracy.

## Sources and attribution

The technical source material is from *Regelungstechnik – Das interaktive Lehrbuch* by Heiko Peuscher. Its technical content is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

Pages used:

- [Regelungsproblem](https://www.regelungstechnik.de/lehrbuch/regelungstechnik/einfuehrung/regelungsproblem)
- [Zweipunktregler](https://www.regelungstechnik.de/lehrbuch/regelungstechnik/klassischeregler/zweipunktregler)
- [Dreipunktregler](https://www.regelungstechnik.de/lehrbuch/regelungstechnik/klassischeregler/dreipunktregler)
- [PID-Regelung](https://www.regelungstechnik.de/lehrbuch/regelungstechnik/klassischeregler/pidregelung)
- [Gütekriterien](https://www.regelungstechnik.de/lehrbuch/regelungstechnik/einfuehrung/guetekriterien)

Changes made: I extracted the article text, reformatted it into passages for retrieval, and used an AI model to generate answers from retrieved 
