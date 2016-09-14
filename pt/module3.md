# Módulo 3 -- UniProt como serviço web {#module3}

## Objetivos:
- Reconhecer a importância das fontes de dados externas
- Usar um serviço web através de código Python
- Processar a informação proveniente de um serviço web

## Input:
- Ficheiro: [selected2.csv](files/selected2.csv)
    - criado no módulo anterior

## Output:
- Ficheiro: `sequences.csv`
    - contendo as sequências de aminoácidos de cada enzima

## Passos:

1. Abra o URL <http://www.uniprot.org/uniprot/P12345.fasta> no _browser_ e estude o formato FASTA.
Altere o identificador do link de `P12345` para outro à sua escolha e estude o seu conteúdo e quais as diferenças entre os dois.

2. Num _script_ Python chamado `module3.py`, crie uma função chamada `get_sequence` que recebe o identificador de uma proteína e devolve a sua sequência de aminoácidos.
Esta função:

    a. abre o URL mencionado acima,
    
    b. lê o conteúdo acessível por esse URL,
    
    c. extrai a sequência de aminoácidos, e
    
    d. junta todas as linhas numa só, de forma a devolver apenas uma _string_.
    ```python
        import urllib # This module contains functions to read URLs

        def get_sequence(identifier):
            # Establish the URL to open
            url = 'http://www.uniprot.org/uniprot/' + ??? + '.fasta'
            
            # Open the URL
            f = urllib.urlopen(url)
            
            # Read all the lines into a list
            lines = f.readlines()
            
            # Ignore the first line, which contains metadata
            del lines[0]
            
            # Join all the remaining lines into a single string
            sequence = str.join("", lines)
            
            # Remove the line ends (the "enter" used to start the next line)
            # This line end is represented as \n
            sequence = str.replace(sequence, '\n', '')
            
            # Return the sequence
            return ???
    ```

3. Vamos experimentar executar a função com um pequeno número de proteínas.
Para tal, adicione as seguintes linhas ao _script_ Python, substituindo `???` pelos identificadores que quiser:
```python
    sequence1 = get_sequence('P12345')
    sequence2 = get_sequence('???')
    sequence3 = get_sequence('???')
    
    print "SEQUENCE 1:\n" + sequence1 + "\n"
    print "SEQUENCE 2:\n" + sequence2 + "\n"
    print "SEQUENCE 3:\n" + sequence3 + "\n"
```

4. Agora que já vimos como utilizar a função, vamos ler as enzimas do ficheiro `selected2.csv` e determinar as suas sequências de aminoácidos.
    
    a. Remova ou comente as linhas do passo 3.
    
    b. Substitua-as por:
    ```python
        import csv
        
        # Open the output file from the previous module
        f = open('selected2.csv')
        paths = csv.reader(f, delimiter=???)
        
        # Start with an empty list of enzymes
        enzymes = []
        
        # Then:
        # - read the information of each pathway,
        # - extract the list of enzymes of each pathway, and
        # - append each enzyme to the list of enzymes
        for path in paths:
            enzymes_field = path[???] # The field of the enzymes
            
            # Split the enzymes into a list, as in module 2
            enzymes_in_this_path = str.split(enzymes_field, ???)
            
            # Append each one into the master enzyme list
            for e in enzymes_in_this_path:
                enzymes.append(e)
    ```

5. Agora que temos uma lista de enzimas, podemos usá-la juntamente com a função que criamos anteriormente para obter as suas sequências de aminoácidos.
Vamos gravar esta informação num novo ficheiro `sequences.csv`.
Para tal, continue a adicionar códugo ao _script_ `module3.py`:
```python
    f = open('sequences.csv', 'w')
    w = csv.writer(f, delimiter=???)
    
    for e in enzymes:
        seq = get_sequence(e)
        w.writerow([e, seq])
    
    f.close()
```

6. Execute o código e estude o conteúdo do novo ficheiro (`sequences.csv`).
Corresponde ao que esperava ver?

7. Certifique-se de que mantém uma cópia do ficheiro `sequences.csv` para si, assim como do _script_ `module3.py`, de forma a que os possa usar nos próximos módulos.
Por exemplo, envie-os para si por email ou faça o upload para a Dropbox.

## Após a aula:

1. Verifique que no ficheiro `sequences.csv` algumas enzimas aparecem repetidas. Tente explicar porquê.