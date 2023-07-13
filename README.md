Olá, Sou Anderson e este é o README.md do projeto/desafio proposto.


Descrição:
      
    - Baixe o projeto enviado via e-mail ou pelo github em: https://github.com/v1ncer3/projeto_eclipseWorks.git;

    - Vá ao arquivo -> api/config/connection.js e insira as informações de conexão do seu banco de dados:
            host_sql = "localhost",
            port_sql = "porta",
            user_sql = "user",
            password_sql = "senha",
            db_name = "eclipseWorks"; -- pode deixar do jeito que está, o script de banco realizou o trabalho de criar o db com este nome.
    
    - Execute o script do banco de dados - este criará o database, as tabelas (`usuario`, `carteira` e `ofertas`) e realizará o insert nas tabelas `usuario` e `carteira`. Caso desejar, fique a vontade para realizar novos inserts na base para testar. Realize inserts/updates nas tabelas `usuario`. Na tabela `carteira` limite-se ao insert, mas caso for realizar um update por qualquer motivo, não altere o valor do campo SLDMDOFT, isso irá trazer instabilidade a aplicação. Consulte o glossário para mais informações sobre o script.

    - Como não temos nenhum front-end desenvolvido para comunicar com a API, inicie o postman (ou ferramenta para consumir APIs, por exemplo insomnia) e crie 3 abas:
        
        Get - http://localhost:8080/offers/ - não é necessário parâmetro nenhum caso não deseje paginação, sendo assim, o sistema irá retornar um array com as ofertas (ativas) e suas respectivas informações daquele dia. Para utilizar a paginação deverá constar na query da url (query.pags_qtd).


        Post - http://localhost:8080/offers/ - utilizando o body->json para inserir os parâmetros a rota espera o modelo abaixo para realizar o processo proposto, caso contrário irá retornar uma mensagem indicando o erro. Caso não ocorra nenhum erro de parametrização/processo, o sistema irá retornar uma mensagem indicando que a oferta foi criada.

        Exemplo_Post: {	
            "CDUSR": value, 
            "CDCTR": value, 
            "CDCNT": value,
            "NMOFT": value,
            "NMOFTMTV": value,
            "VRUTR": value, 
            "QTDOFT": value
        }


        Delete - http://localhost:8080/offers/ - utilizando o body->json para inserir os parâmetros a rota espera o modelo abaixo para realizar o processo proposto, caso contrário irá retornar uma mensagem indicando o erro. Caso não ocorra nenhum erro de parametrização/processo, o sistema irá retornar uma mensagem indicando que a oferta foi deletada (método soft delete).

        Exemplo_Delete: {
            "CDOFT": value, 
            "CDCTR": value, 
            "CDCNT": value
        }

A partir de agora, fique a vontade para testar e quebrar (avise-me se acontecer) a API desenvolvida.

Glossário - Aqui estão alguns indetificadores que irão auxiliar nos testes:

    CREATE TABLE `USUARIO` (
    `CDUSR`           - código do usuário,
    `NMUSR`           - nome do usuário,
    `CDCTR`           - código da carteira,
    PRIMARY KEY (`CDUSR`, `CDCTR`)
    )

    Cada usuário (1), pode ter várias carteiras (N);
    TABLE `CARTEIRA` (
    `CDCTR`           - código da carteira,
    `CDCNT`           - código da conta,
    `NMCTR`           - nome da carteira,
    `TPMD`            - tipo da moeda (ex: BTC, R$, $),
    `SLDMD`           - saldo (+) da carteira,
    `DTCTR`           - data de lançamento da carteira,
    `SLDMDOFT`        - saldo (-) de ofertas relacionadas a essa carteira,
    PRIMARY KEY (`CDCTR`, `CDCNT`)
    )

    Cada usuário (1), pode ter várias carteiras (N), cada carteira pode ter várias ofertas (N).
    TABLE `OFERTA` (
    `CDOFT`           - código da oferta,
    `CDCTR`           - código da carteira,
    `CDCNT`           - código da conta,
    `NMOFT`           - nome da oferta,
    `NMOFTMTV`        - descrição/motivo da oferta, -- pode ser nulo
    `VRUTR`           - valor unitário,
    `QTDOFT`          - quantidade,
    `DTOFT`           - data de lançamento da oferta,
    `HROFT`           - hora de lançamento da oferta,
    `IsDeleted`       - identificador do soft delete,
    PRIMARY KEY (`CDOFT`, `CDCTR`, `CDCNT`)
    )

            Package.json gerado pelo npm:
                {
                    "name": "projeto_nodejs",
                    "version": "1.0.0",
                    "description": "",
                    "main": "index.js",
                    "dependencies": {
                        "corepack": "^0.19.0",
                        "express": "^4.18.2",
                        "mysql2": "^3.5.1",
                        "nodemon": "^3.0.1",
                        "npm": "^9.7.2"
                    },
                    "scripts": {
                        "dev": "nodemon eclipseWorks/config/server.js",
                        "test": "echo \"Error: no test specified\" && exit 1"
                    },
                    "keywords": [],
                    "author": "",
                    "license": "ISC"
                }

    Requisitos para teste:  
            Apps:
                - VsCode:                             -> https://code.visualstudio.com/
                - Mysql Workbench e server>           -> https://www.mysql.com/products/workbench/
                - Postman:                            -> https://www.postman.com/
                - Node (versão utilizada -> v20.4.0): -> https://nodejs.org/en/
            Libs:
                "corepack": "^0.19.0",
                "express": "^4.18.2",
                "mysql2": "^3.5.1",
                "nodemon": "^3.0.1",
                "npm": "^9.7.2",
                "scripts": 
                    "dev": "nodemon eclipseWorks/config/server.js"

