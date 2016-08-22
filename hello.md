% Data processing for metabolic pathways
  using files, web services and databases
% João D. Ferreira; Francisco M. Couto
% August 2016

# Introduction

The aim of these exercises is to provide students the ability and competence to process data in an automatic fashion.
The main topic surrounding these exercises will be metabolic pathway data processing, with a closer focus on the proteins that catalyse the chemical reaction those pathways, also known as _enzymes_.
Despite working with metabolic pathways during the classes, the data processing methods that the students will learn in this class can be applied to many other types of data.

## Data

The following figure represents the first steps in the glycolysis, a metabolic pathway that decomposes glucose in smaller chemical compounds.
This figure includes a representation of five steps in this pathway, each one catalysed by a different enzyme.

![A Metabolic pathway](images/pathway.png "An example of a metabolic pathway")

For this class, we will provide [an Excel file](files/metabolic_pathways.xls) with information on 297 metabolic pathways.
Each line in this file contains:

- an identifier of the metabolic pathway;
- the name of the pathway;
- the class it belongs to;
- a list of the enzymes that participate in the pathway.

Therefore, the Excel file has 297 lines, plus another one for the column headers.

The following image shows a screenshot of the Excel file and its data

![A screenshot of the Excel file](images/excel.png "A screenshot showing part of the data in the Excel file")

This information comes from an online database called [Kyoto Encyclopedia of Genes and Genome](http://www.genome.jp/kegg/kegg2.html). The enzymes are referred by their UniProt code.
[UniProt](http://www.uniprot.org/) is a database of proteins that contain, among a vast amount of information, the aminoacid sequences of the proteins.

## Processing

Despite the data being provided to the students as an Excel file, the data processing operations will mostly be executed with a programming language.
In this class, we will use [Python](http://www.python.org)
Processing our data with Python instead of Excel offers several benefits:

- We can define a set of operations to be executed automatically, which in Excel would take a large amount of time, since it is mostly driven by user interaction rather than direct commands
- Programming languages can handle complex data types, while Excel is mostly oriented towards numeric computations

No deep knowledge of programming will be required for the class exercises, as we will provide most of the code.
In fact, the students will not directly learn the details of Python as a programming language, but will instead be given "recipes" that contain most of the necessary logic, with small snippets of missing code that the students need to fill.
However, we expect that the students familiarize themselves with Python syntax before the first module of this class by following some online courses.
For example, [Codecademy](https://www.codecademy.com/en/tracks/python) contains six modules that will help the students in this task:

- [Python Syntax](https://www.codecademy.com/courses/introduction-to-python-6WeG3/0/1?curriculum_id=4f89dab3d788890003000096)
- [Strings & Console Output](https://www.codecademy.com/courses/python-beginner-sRXwR/0/1?curriculum_id=4f89dab3d788890003000096)
- [Conditionals & Control Flow](https://www.codecademy.com/courses/python-beginner-BxUFN/0/1?curriculum_id=4f89dab3d788890003000096)
- [Python Lists and Dictionaries](https://www.codecademy.com/courses/python-beginner-en-pwmb1/0/1?curriculum_id=4f89dab3d788890003000096)
- [File Input/Output](https://www.codecademy.com/courses/python-intermediate-en-OGNHh/0/1?curriculum_id=4f89dab3d788890003000096)


# Module 1 -- Metabolic pathways data

## Part I: Notepad++ and Python

### Objectives

- Open Notepad++, write some Python code and save the file
- Execute the file with Python

### Steps

1. In the Windows start menu, open `Notepad++`.

![Open Notepad++](images/open-notepad.png "Open Notepad++")

2. Write a small "Hello World!" program and save the file in the Desktop (or in whichever folder you want) with the name `test.py`.

![The small \"Hello World\" file](images/hello-world.png "The small \"Hello World\" file")

3. In the start menu, open the command line (`cmd`).

![Starting the command line](images/open-cmd.png "Starting the command line")

4. In the terminal (the command line window), we need to navigate to the Desktop folder and then instruct Python to run our `test.py`.
   We do this by running the following commands:
```bash
cd Desktop
python test.py
```
![The \"Hello World\" output](images/hello-world-run.png "The \"Hello World\" output")

5. Observe the output produced by python.


## Part II: Beginning data processing

### Objectives
- Understand the CSV format
- Convert between CSV and the Excel format
- Read CSV files with Python

### Input:
- File: [metabolic_pathways.xls](files/metabolic_pathways.xls)

### Output:
- File: metabolic_pathways.csv
- Console:
```awk
Glycolysis / Gluconeogenesis
Citrate cycle (TCA cycle)
Pentose phosphate pathway
Pentose and glucuronate interconversions
...
```

### Steps:
1. Abrir o ficheiro Excel. Tome atenção ao conteúdo do ficheiro e tente familiarizar-se com os dados. Este passo é importante para o processamento, pois permite ganhar uma certa intuição acerca da informação com que estamos a lidar.

2. Escrever os dados num ficheiro no formato CSV.

3. Abrir o ficheiro CSV num editor de texto (Notepad++) e estudar o seu formato (e.g. determinar qual o separador dos campos, se os campos são delimitados, e como, etc.)

4. Ler o ficheiro CSV com o Python e, para cada via, imprimir o seu nome. Pode usar o seguinte código, completando nos dois locais assinalados com reticências e num fundo verde (...):
```python
    import csv
    f = open('metabolic_pathways.csv')    # Abrir o ficheiro
    paths = csv.reader(f, delimiter=...) # Criar um leitor de CSV
    for path in paths:
        print ... # Para cada via, imprime o seu nome
```

### Quiz:
1. Como procederia para imprimir não o nome das vias mas sim a sua classe?
2. Explique porque alguns campos são delimitados por aspas ( " ) e outros não.