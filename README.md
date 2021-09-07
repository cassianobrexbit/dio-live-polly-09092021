# dio-live-polly-09092021
Repositório de código para o live coding da DIO sobre o Amazon Polly

## Configurando a arquitetura do projeto

### Recursos

- Amazon S3
- AWS Lambda
- Amazon Polly
- Amazon API Gateway

### Criando o bucket no S3

- S3 Dashboard -> Create bucket -> Selecionar região -> Manter as configurações padrão -> Create bucket

### Criando a função lambda

- Lambda Dashboard -> Create function -> Author from scratch -> Enter Function name -> Permissions -> Create a new role with basic Lambda permissions -> Manter as configurações padrão -> Create function
- Inserir o código ```src/pollySynth.js``` na aba Code -> Deploy

### Configurando as permissões de acesso para o S3 e o Amazon Polly no IAM

- Lambda Dashboard -> Selecionar a função criada -> Configuration -> Permissions -> Execution role -> Selecionar a role criada e abrir no IAM Console
- Add inline policy -> Choose a service -> 
  - S3
    - Write: PutObject
    - List: ListBucket
  - Polly
    - All Polly actions (polly:*)

### Criando a API Rest

- API Gateway Dashboard -> Create API -> Rest API -> Inserir API Name -> Manter o restante das configurações padrão -> Create API
- Actions -> Create Resource ```polly``` -> Selecionar o resource -> Crete Method -> POST -> Integration type Lambda Function -> Use Lambda Proxy integration -> Selecionar a função lambda criada -> Save
- Actions -> Deploy API

### Testando a aplicação

- API Gateway Dashboard -> Selecionar a API Rest criada -> Stages -> Selecionar o método criado -> Copiar a URL
- Abrir o Postman -> Colar a URL copiada -> Selecionar POST como método
- Copiar o body do arquivo ```src/input.json``` -> Selecionar Body no Postman -> Raw -> JSON -> Colar o conteúdo copiado -> Send

### Buscando o arquivo de áudio gerado no S3

- S3 Dashboard -> Selecionar o bucket criado -> Selecionar o arquivo gerado -> Download -> Executar o arquivo baixado

