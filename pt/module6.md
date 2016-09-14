# Módulo 6 -- Criar uma base de dados SQL {#module6}

## Objetivos:
- Desenhar um esquema de base de dados simples para guardar informação de vias metabólicas
- Usar chaves estrangeiras

## Input:
- Nenhum

## Output:
- Ficheiro de base de dados: `pathways.db`

## Passos:

1. Vamos começar por criar uma nova base de dados vazia no ficheiro `pathways.db` com três tabelas.
Primeiro, crie um _script_ `module6.py` com o seguinte código:
```python
    # `sqlite3` is a package that can be used to create a file containing
    # a relational database. We use this package to create the database,
    # insert data in it and query the data.
    
    import sqlite3
    
    # To access a database, we need to connect to it. If the file does not
    # exist, one will be created
    connection = sqlite3.connect('pathways.db')
```

2. Agora que temos uma base de dados vazia, vamos adicionar as tabelas necessárias para guardar os dados de vias metabólicas.
```python
    # This table will contain data about the pathways
    connection.execute('''
        CREATE TABLE path (
            id VARCHAR(255) PRIMARY KEY,
            name VARCHAR(255) NOT NULL,
            class VARCHAR(255) NOT NULL
        )
    ''')
    
    # This table will contain data about the enzymes
    connection.execute('''
        CREATE TABLE enzyme (
            id VARCHAR(255) PRIMARY KEY,
            sequence TEXT NOT NULL
        )
    ''')
    
    # This table will associate each pathway with its enzymes
    connection.execute('''
        CREATE TABLE path_enzyme (
            path_id VARCHAR(255),
            enzyme_id VARCHAR(255),
            PRIMARY KEY (path_id, enzyme_id),
            FOREIGN KEY (path_id) REFERENCES path (id),
            FOREIGN KEY (enzyme_id) REFERENCES enzyme (id)
        )
    ''')
```

3. Uma vez criadas as tabelas, podemos inserir os dados.
Como exemplo, vamos inserir apenas uma via e duas enzimas dessa via.
Se necessário, consulte os ficheiros criados nos módulos anteriores para encontrar o nome da via `hsa00730` e as enzimas que fazem parte dela.
```python
    connection.execute('''
        INSERT INTO path (id, name, class)
        VALUES ('hsa00730', '???', '???')
    ''')
    
    connection.execute('''
        INSERT INTO enzyme (id, sequence)
        VALUES ('Q53FP3','???')
    ''')
    
    connection.execute('''
        INSERT INTO enzyme (id, sequence)
        VALUES ('???','???')
    ''')
    
    connection.execute('''
        INSERT INTO path_enzyme (path_id, enzyme_id)
        VALUES ('hsa00730','???')
    ''')
    
    connection.execute('''
        INSERT INTO path_enzyme (path_id, enzyme_id)
        VALUES ('???','???')
    ''')
    
    # Ensure that the data is saved
    connection.commit()
```

4. Por fim, vamos assegurar-nos que as tabelas contêm os dados que lá colocámos.
Para tal, como exemplo, vamos selecionar as enzimas de cada via.
```python
    rows = connection.execute('SELECT id, sequence FROM enzymes')
    for row in rows:
        enzyme_id = row[0]
        enzyme_sequence = row[1]
        
        print enzyme_id + ' starts with ' + enzyme_sequence[:5]
```

5. Verifique que o output corresponde ao seguinte:
```text
    Q53FP3 starts with MLLRA
    Q9Y697 starts with MLLRA
```

6. Certifique-se de que mantém uma cópia do ficheiro `pathways.db` para si, assim como do _script_ `module6.py`, de forma a que os possa usar nos próximos módulos.
Por exemplo, envie-os para si por email ou faça o upload para a Dropbox.

## Após a aula:

1. Verifique a razão pela qual a chave primária da tabela path_enzyme tem dois atributos.

2. Modifique o esquema da base de dados para que possa guardar também o nome de cada enzima e a sua posição na via metabólica (um número inteiro).

3. Altere o código do passo 4 para que verifique também o conteúdo das tabelas `paths` e `path_enzyme`.
