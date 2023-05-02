---
layout: post
title: "Self instruct models fine tuning - for dummies"
categories: routine
author: "s3nh"
meta: "Things I've learned"
---

<a href="https://www.buymeacoffee.com/s3nh"><img src="https://www.buymeacoffee.com/assets/img/guidelines/download-assets-sm-1.svg" alt=""></a>


Just after the LLM hype train arrived, I was struggling how to properly create and train self instruct models. LLM jumped straight into the mainstream and I really had that feeling 
that there is little focus on how this models works and how to properly define a dataset for correct fine-tuning process. 

Also, people automatically forget about smaller architectures, and using models which has number of params smaller than 1b is just a faux pas. 
I decided to write a very simple wrapper for fine tune self instruct model on any architecture, using my last amount of energy and spare time. 


Edit: Need to be refactored, but let me think of it later. 


### Data 

Data was always the most informative part of ml/dl/modelling, but now it is really clear for the masses, that properly define dataset can 
trick you into thinking of AGI, and it cannot be solved by using some fuzzy wuzzy complex architectures. 

So, at the very first information about Alpaca/LLama/chatgpt models I was scratching my head about input, instructions and output. 
These three allow me to spends sleepless nights, because there was not exact information (or maybe I am just unaware and my adhd is strong enought) 
about how these data is put straight into model. 

So I thought that there exist some additional backbone throught network, some magic flow, some internat nn which passes input, communicate with instruction and 
give hand to the output, which is miracolously treat as an response. But, just no. 

This information is just simply put into one big string with additional tokens, and rest is the same. 
Training process did not change, there are vast amount of parameters, models are big enought to learn the parse project, and use context from input 
to gather information to the output. 


### Fine tuning

These 150liner allows you to fine tune almost any model, using trining args and additional configuration params, 
to get some pretty accurate self instruct model. 

It is messy at the moment, but who cares. 


```python'


import argparse
import pandas as pd 
import pathlib
import pickle as pkl
import transformers
import torch 
import json

from pathlib import Path
from torch.utils.data import Dataset, random_split
from transformers import AutoTokenizer 
from transformers import AutoModelForCausalLM
from transformers import TrainingArguments
from transformers import Trainer

from transformers import HfArgumentParser
from transformers import TrainingArguments
from typing import List, Tuple, Union
torch.manual_seed(42)

def get_args():
    parser = argparse.ArgumentParser()
    parser.add_argument('-m', '--model', nargs="?", default="")
    parser.add_argument('-d', '--destination', nargs="?", default="")
    parser.add_argument('-t', '--tokenizer', nargs="?", default="")
    args = parser.parse_args()
    return args

class CFG:
    model_name: str = 'EleutherAI/gpt-neo-125m'
    tokenizer_name: str = 'EleutherAI/gpt-neo-125m'
    max_length: int  = 512
    device: str = 'cuda'
    cuda: bool = True
    train_ratio: float = 0.9
    args_path: str = 'args.json'
    data_path: str = 'data.csv'

config =  CFG();

def load_model(name):
    model = AutoModelForCausalLM.from_pretrained(name)
    if config.cuda:
        return model.cuda()
    return model

def load_tokenizer(name):
    tokenizer = AutoTokenizer.from_pretrained(name)
    if tokenizer.pad_token is None:
        tokenizer.pad_token = tokenizer.eos_token
    return tokenizer

def generate_prompt(instruction: str, input: str, response: str):
    if input:
        return f"""Poniżej znajduje się instrukcja
        opisująca zadanie,
        połączona z danymi wejściowymi
        , które zapewniają dalszy konktekst.
        Napisz odpowiedź, która odpowiednio odpowie na pytanie.

### Instruction:
{instruction}

### Input:
{input}
|
### Response:
{response}
"""

class InstructDataset(Dataset):
    
    def __init__(self, data, tokenizer, max_length):
        
        self.input_ids: List = []
        self.attn_masks: List = []
        self.labels: List = []
        
        for txt in data:
            instruction = generate_prompt(instruction = txt['instruction'], 
                                          input = txt['input'], 
                                          response = txt['output'])
            encodings_dict = tokenizer(instruction, padding="max_length", max_length = max_length, truncation=True)
            self.input_ids.append(torch.tensor(encodings_dict['input_ids']))
            self.attn_masks.append(torch.tensor(encodings_dict['attention_mask']))
            
    def __len__(self):
        return len(self.input_ids)

    def __getitem__(self, idx) -> Tuple[List, List]:
        return self.input_ids[idx], self.attn_masks[idx]
    
Pathable = Union[str, pathlib.Path]

def get_extension(input_path: Pathable):
    if isinstance(input_path, pathlib.Path):
        input_path = str(input_path)
    return input_path.split('.')[-1]

class BasicException(Exception):
    ...

def read_data(input_path: Pathable):
    proper_types: List = ['csv', 'json', '']
    extension = get_extension(input_path) 
    if extension not in proper_types:
        raise BasicException("Please provide a proper file extension")

def dataset_prep(configtokenizer) -> Tuple[torch.utils.data.Dataset, torch.utils.data.Dataset]:
    input_data = read_data(config.data_path)
    dataset = InstructDataset(data = input_data, tokenizer = tokenizer, max_length = config.max_length)
    train_size = int(config.train_ratio * len(input_data))
    val_size = len(dataset) - train_size
    train_dataset, val_dataset = random_split(dataset, [train_size, val_size])
    return train_dataset, val_dataset

def save_training_args(args: TrainingArguments) -> None:
    args_json = args.to_json_string()
    with open(config.args_path, 'w') as outfile:
        outfile.write(args_json)

def load_training_args() -> TrainingArguments:
    parser = HfArgumentParser(TrainingArguments)
    training_args, = parser.parse_json_file(json_file = config.args_path)
    return training_args

def parse_model_name(model_name: str) -> str:
    return model_name.split('/')[-1]

def create_outpath(model_name) -> None:
    name: str = parse_model_name(model_name=model_name)
    outpath = f"./result/{name}"
    return outpath

def create_training_args():
    ...
    # How to properly create training algorithms

# def  collate_data(data):
#     lambda data: {'input_ids': torch.stack([f[0] for f in data]),
#     'attention_mask': torch.stack([f[1] for f in data]),
#     'labels': torch.stack([f[0] for f in data])}).train()

def train():
    ...

def main():
    args = get_args()
    args_list: List = [args.model, args.destination, args.tokenizer] 
    # If empty, go straight to  config
    if "" in args_list:
        model_name = config.model_name
        tokenizer_name = config.tokenizer_name

    else:
        model_name = args.model
        tokenizer_name = args.tokenizer
    
    parsed_name = parse_model_name(model_name)
    output_path = create_outpath(parsed_name)
    model = load_model(model_name)
    tokenizer = load_tokenizer(tokenizer_name)
    
    
    #train_dataset, val_dataset = dataset_prep(config = config)

    data = pd.read_csv("alpaca_dolly.csv")
    dict_data = pd.DataFrame.to_dict(data, orient='records' )
    dataset = InstructDataset(data = dict_data, tokenizer = tokenizer, max_length=512)
    train_size = int(0.9 * len(dataset))
    train_dataset, val_dataset = random_split(dataset, [train_size, len(dataset) - train_size])
        
    training_args = TrainingArguments(output_dir=output_path, num_train_epochs=2, logging_steps=5000,
                                  per_device_train_batch_size=8, per_device_eval_batch_size=2,
                                  warmup_steps=10, weight_decay=0.01,
                                  learning_rate = 1e-3, logging_dir='./logs', 
                                 save_total_limit=2)
    
    trainer = Trainer(model = model, 
            args = training_args, 
            train_dataset = train_dataset, 
            eval_dataset = val_dataset, 
            data_collator= lambda data: {'input_ids': torch.stack([f[0] for f in data]),
                                                              'attention_mask': torch.stack([f[1] for f in data]),
                                                              'labels': torch.stack([f[0] for f in data])}).train()
    trainer.train()

if __name__ == "__main__":
    main()


```





