# Desafio Kubedev 
Objetivo deste desafio e transformar esta aplicação em uma imagem Docker seguindo os padrões de documentação.
## Etapa para criar uma imagem
  * Identificar em qual linguagem foi desenvolvida e sua versão caso seja necessário;
  * Identificar dependências além do arquivos de dependências da aplicação;
  * Definir se é uma aplicação stateless ou stateful;
  * Identificar requisitos não funcionais ou serviço de apoio;
    * ex: Vai utilizar um padrão sidecar com logs.
    * ex: vai necessita de banco de dados.
  * Identificar se será necessário variáveis de ambiente;
    * Definir se será variáveis em momento de construção ou momento de execução.
  * Definir porta padrão de trabalho;
    * Definir se é portão será para serviço interno ou externo.
### As etapas anteriores são baseadas nas recomendações 12factor link abaixo.
  [12factor](https://12factor.net/)

## Descrição da Aplicação
  - É uma aplicação desenvolvida em python3 com flask.
    - Não tem definição de versão, irá utilizar a mais atual.
    - **requirements.txt** define as dependências da aplicação.
    * **app.py** Arquivo que inicia a aplicação e define a porta de trabalho. 
  - Porta de padrão de trabalho *5000*.
    - Não tem definição então irá rodar na porta padrão acima.
  - Sem necessidade de variáveis na criação do container.
  - Aplicação tipo stateless.
  - Sem requisitos funcionais e de apoio.
  - Necessário instalar as dependências, utilizar usando o *pip3*.

## Recomendações
  - Trabalhar com layer de dependências separadas da aplicação, e assim ganhar performance no momento de build.
  - Se possível trabalhar com versão da imagem Alpine.
  - Criar arquivo *.dockerignore*  para evitar de copiar arquivos desnecessários.
  - Criar arquivo *Dockerfile* seguindo as recomendações oficiais Dockerinc.
    - [Best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
    - [exemplo de Dockerfile](https://docs.docker.com/language/python/build-images/)
## Exemplo de DockerFile e comentário
  - Abaixo está um exemplo de DockerFile simples
```sh
FROM python:3.10.1-alpine
LABEL maintainer="Rodrigo Freitas"
WORKDIR /app
COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt
COPY . .
EXPOSE 5000
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0" ]
  ```
