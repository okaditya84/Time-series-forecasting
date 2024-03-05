
# Time Series Forecasting for AQi using LLMs

This github repository contains an implementation of time series forecasting using open source LLMs. In this case, I have worked with [![Gemma:7b](https://huggingface.co/google/gemma-7b)](https://huggingface.co/google/gemma-7b) and ollama running locally.

My approach is described as follows:
- Collected data of Ashok Nagar, Delhi, India from [CPCB website](https://cpcb.nic.in/automatic-monitoring-data/), with precision of every half hour.
- General anaylysis of the data and interpolation of null values.
- Choosing a day to prompt the LLM about. (19th December 2023).
- Analysis of different parameters for that day including finding max, min, average and AQI subindex values using the AQI formula as per Indian Standards.
- Analysis of 20th December 2023 for the same parameters and calculating sub indices.
- Running ollama Gemma:7b model and applying zero prompting with data for 19th december to predict for 20th december. 
- Applying different prompting techniques and also giving some context about the data.
- Validating the results with the actual analysis of 20th December so found earlier.
- Repeating these steps for 19th and 20th december 2023 as test and validating data respectively.

#### Directories overview:
- extracted important : AQI Dataset for ashok nagar.
- 19decto20Dec: extracted data for 19th and 20th december, analysis of AQI on 19th and 20th december.
- 31decto31Jan: extracted data for 31st december and 1st January, analysis of AQI.
- Two images for the output of Gemma:7b
- requirements.txt for installation and testing.



## Reference materials

[AQI Formulation](https://www.pranaair.com/blog/what-is-air-quality-index-aqi-and-its-calculation/) for understanding what is AQI, what are it's parameters and sub indices.

[National AQI](https://pib.gov.in/newsite/printrelease.aspx?relid=110654) for Reference of BPHI, BPLO, IHi and ILo ranges.

[TimeLLM](https://github.com/KimMeen/Time-LLM) This is an open-source LLM specially designed for time series forecasting (multivariate too).

[Ollama Custom modelling](https://github.com/ollama/ollama#customize-a-model) for making a custom ModelFile for ollama

[How to do time series forecasting](https://colab.research.google.com/drive/10Z5fsjKPNqyaI9qMo-mgHb6i9l--Roye?usp=sharing#scrollTo=XG9C9ZmrhLmd) this is a colab notebook for referring on how to do time series forecasting. 


## Run Locally

Clone the project

For LINUX/WSL based system
```bash
 curl -fsSL https://ollama.com/install.sh | sh
```

For Windows based system
[Download here](https://ollama.com/download/windows)

Install dependencies

```bash
  pip install -r requirements.txt
```

Start the server
Open Command Prompt in administration mode
```bash
    ollama serve
```

```bash
    ollama run gemma:7b
```

NOTE: You can replace the gemma:7b with any other model available in the [Ollama Library](https://ollama.com/library)


## Proposed steps and insights
- We can use [TimeLLM](https://github.com/KimMeen/Time-LLM), [TimeGPT-1](https://docs.nixtla.io/reference/timegpt_timegpt_post) for the time series forecasting. (Given a computationally advanced decvice capable of running LLMs smoothly or Pro subscription of Google Colab/Kaggle for cloud GPUs).
- Trying simple zero-shot, zero-shot with a little context and few shot prompting for better results.
- Deeper analysis of PM 2.5, PM 10, NO2, CO, SO2 and O3 (as these 6 indices have larger contribution in determining AQI) with each day, each month, each season and every year can give more insights on the trends of sub indices.
- RAG or PEFT fine-tuning the LLMs weights is one of the best option to consider for the forecast.
- PAP (Prompt as prefix) technique can also be utilized for the same.

INFORMATION: All General made LLMs are capable of time series forecasting but LLMs like those mentioned above are fine-tuned on the kernel level to give the best output for the task.



## Additional Information

Due to the limitation of hardware on the local machine, the prompting took a long time to answer. 
This implementation is a high-level code of performing time series forecasting.

