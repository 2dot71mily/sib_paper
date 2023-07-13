# Reproducing Underspecification in Language Modeling Tasks: A Causality-Informed Study of Gendered Pronoun Resolution

Follow steps below to reproduce all data and plots.

## Interact with open source demos instead!

If you would rather checkout currently running and more flexible demos, you can also reproduce the methods in this paper by checking out the open-source demos below, otherwise, skip to the `Setup`:
- Spurious Correlations Open Source Hugging Face Space: https://huggingface.co/spaces/emilylearning/spurious_correlation_evaluation.
- Underspecification Metric Measurement Open Source Hugging Face Space: https://huggingface.co/spaces/emilylearning/llm_uncertainty.
- More General Setting Toy SCM: https://colab.research.google.com/drive/1B04P1DGlqDF8L0nf3m__VpUovE7C2iZb.



# Setup
```
git clone https://github.com/2dot71mily/sib_paper.git
cd sib_paper
python3 -m venv venv_sib
source venv_sib/bin/activate
python3 -m pip install --upgrade pip
# If without a GPU comment out `nvidia.*` and `triton` from requirements.tct
# BERT-like and OpenAI models can be tested without GPU
pip install -r requirements.txt
```


# Reproducing plots with existing data
## Method 1
In `config.py`, set `METHOD_IDX`:
```
######################## Select method type #################################
METHODS = ['correlation_measurement', "specification_metric"] 
METHOD_IDX = 0  # Select '0' for Method 1, '1' for for Method 2
```
Then run in terminal:
`python spurious_plotting.py`


## Method 2
In `config.py`, set `METHOD_IDX` & if `WINO_G_ID` (Winogender `Simplified` or not):
```
######################## Select method type #################################
METHODS = ['correlation_measurement', "specification_metric"] 
METHOD_IDX = 1  # Select '0' for Method 1, '1' for for Method 2

...
# Set to `True` if testing with `Simplified` Winogender-gender-identified eval set
WINO_G_ID = False  
```

Then run in terminal:
`python uncertainty_plotting.py`
Note: this process is a bit slow, due to the large number of files ingested.


# Reproducing the data used in the plots
First test the setup as shown below.


## Testing your setup

Note: The LLM weights will be downloaded / cached from Hugging Face. Throughout, it *is* expected that `Some weights of the model checkpoint at bert-base-uncased were not used when initializing BertForMaskedLM: ['cls.seq_relationship.bias', 'cls.seq_relationship.weight']`


### Method 1
In `config.py`, set `TESTING`,  `METHOD_IDX`, `INFERENCE_TYPE_IDX` & `MODEL_IDX`:
```
TESTING = True  # Set to True if testing on subsets of the challenge sets
######################## Select method type #################################
METHODS = ['correlation_measurement', "specification_metric"]  
METHOD_IDX = 0  # Select '0' for Method 1, '1' for for Method 2
...
########################## Select inference type ############################
INFERENCE_TYPES = ["bert_like", "open_ai", "cond_gen"]
INFERENCE_TYPE_IDX = 2
# Select '0' for BERT-like, '1' for `open-ai`, 2 for `UL2-family`
...
###################### Select model type #######################
...
CONDITIONAL_GEN_MODELS = ["UL2-20B-denoiser", "UL2-20B-gen", "Flan-UL2-20B"]
MODEL_IDX = 0
##################### If model is GPT ##################
# Required OpenAI API key only for `open_ai` type inference
OPENAI_API_KEY =  '<OpenAI API key>'
```
Then run in terminal:
`python inference.py`


###  Method 2
In `config.py`, set `TESTING`, `METHOD_IDX`, if `WINO_G_ID` (Winogender `Simplified` or not), `INFERENCE_TYPE_IDX` & `MODEL_IDX`:
```
TESTING = True  # Set to True if testing on subsets of the challenge sets
######################## Select method type #################################
METHODS = ['correlation_measurement', "specification_metric"]  
METHOD_IDX = 1  # Select '0' for Method 1, '1' for for Method 2
...
########################## Select inference type ############################
INFERENCE_TYPES = ["bert_like", "open_ai", "cond_gen"]
INFERENCE_TYPE_IDX = 2
# Select '0' for BERT-like, '1' for `open-ai`, 2 for `UL2-family`
...
###################### Select model type #######################
...
CONDITIONAL_GEN_MODELS = ["UL2-20B-denoiser", "UL2-20B-gen", "Flan-UL2-20B"]
MODEL_IDX = 0
##################### If model is GPT ##################
# Required OpenAI API key only for `open_ai` type inference
OPENAI_API_KEY =  '<OpenAI API key>'
```
Then run in terminal:
`python inference.py`


## Reproducing all the data
### Method 1 
In `config.py`, same as Method 1 above but set:
```
TESTING = False 
```

Then run in terminal:
`python inference.py`


### Method 2
In `config.py`, same as Method 2 above but set:
```
TESTING = False 
```

Then run in terminal:
`python inference.py`

