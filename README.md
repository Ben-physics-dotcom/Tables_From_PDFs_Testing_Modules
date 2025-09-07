# Tables_From_PDFs_Testing_Modules

Goal of the repository is to make a little bit research which python package is usefull to transform pdf tables into data frames with minimal work. 

## Info

The notebooks are in the Notebooks folder. I used the Imports notebook to load packages and data that are the same for all other notebooks. In the other notebooks I run the Imports notebook with `%run Imports.ipynb`.

I will test three different python packages to get tables out of pdf files:

- camelot-py
- tabula-py
- pymupdf
  
In the next section I will explain my results.

## Results

### Tabula

Installation: I installed tabula with `pip install tabula-py`. 

A difficulty in this package is that java must be install on the computer. I do not work with java, so I have not install java. So the tabular do not work proberly. See the error massage in the (notebook)[https://github.com/Ben-physics-dotcom/Tables_From_PDFs_Testing_Modules/Notebooks/tabula.ipynb].

### PyMuPDF

Installation: I install pymupdf with `pip install pymupdf`.

Compare to tabula pymupdf do not need java to work. To get access to the pdf `doc = pymupdf.open(path_to_file)` can be used. What is very practical is to 
get the meta data from the pdf with `doc.metadata()`. 

With `test = doc.load_page(int).find_tabular()` tables can be found on a 
specific page (int). In `find_tabular()` I use `strategy='line'` to let the line work proberly. `test[0].extract()` can be used to extract the tables from the previous line. 

As an output I get lists with sublists, where each sublist is a line in a table. 
The data is very uncleaned. I think it will consume much time to clean the data and put them into a data frame.

## Camelot

Installation: I install camelot with `camelot-py[all]`.

For the test I want the pages 1 to 101 to be searched. So I created
a variable named `pages=0-100`. 

To get the tables from the defined pages I used the line `tables = camelot.read_pdf('path_to_file', pages=pages, process_background=True)`. With printing `tables` `n=int` tells how many tables are found. 

With `tables[0].parsing_report` I can look at the accuracy of the parcing and which page the table was found. The order gives the order in which order the tables are found on each page. 

The problem in the pymupdf is that I got lists. With `tables[0].df` I get the 
first table as a data frame. 

For later work, I think camelot is the best choice to get tables from 
pdf files.
