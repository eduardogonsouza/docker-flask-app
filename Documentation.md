### 1 Criação do Projeto e da Aplicação Flask

O que foi feito: Criação de um diretório para o projeto e um arquivo Python contendo uma aplicação Flask básica, e um arquivo "requirements.txt".

Conteúdo do arquivo requirements.txt:

```python
    Flask==2.3.2
    Werkzeug==2.3.6
```

Conteúdo do arquivo app.py:

```python

from flask import Flask

app = Flask(__name__)


@app.route("/")
def home():
    return "Oii, Essa é minha aplicação docker!!"


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)


```

Explicação: Criamos uma aplicação simples que responde com "Oii, Essa é minha aplicação docker!!" quando acessada.

### 2 Criação do Dockerfile

Criação do arquivo chamado Dockerfile no diretório do projeto

Adição de instruções no Dockerfile para construir a imagem Docker.

Explicação: Cada linha no Dockerfile representa uma etapa na construção da imagem.

Conteúdo do Dockerfile:

```docker
FROM python:3.9-slim

WORKDIR /app

COPY . .

RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8080

CMD ["python", "app.py"]
```

Explicação das instruções:

\- **_FROM:_** Especifica a imagem base (Python 3.9 slim neste caso).

\- **_WORKDIR:_** Define o diretório de trabalho dentro do contêiner.

\- **_COPY:_** Copia arquivos do host para o contêiner.

\- **_RUN:_** Executa comandos durante a construção da imagem.

\- **_EXPOSE:_** Informa qual porta o contêiner vai escutar.

\- **_CMD:_** Define o comando padrão a ser executado quando o contêiner for iniciado.

### 3 Construção da Imagem Docker

Construção da imagem Docker a partir do Dockerfile.

Este passo cria uma imagem Docker baseada nas instruções do Dockerfile.

Comando utilizado:

    docker build -t flask-docker-app -f DockerFile

**_docker build:_** Comando para construir uma imagem Docker.

**_\-t flask-docker-app_**: Atribui um nome (tag) à imagem.

**_\-f DockerFile_** : Indica que o Dockerfile está no diretório atual.

### 4 Execução do Contêiner

O que foi feito: Execução de um contêiner a partir da imagem construída.

Explicação: Este passo cria e inicia um contêiner baseado na imagem que  
construímos.

Comando utilizado:

    docker run -p 8080:8080 flask-docker-app

**_docker run_**: Comando para executar um contêiner.

**_\-p 8080:8080_**: Mapeia a porta 8080 do contêiner para a porta 8080 do host.

**_flask-docker-app_**: Nome da imagem a ser executada.

## **_Screenshot :_**

**_![][image1]_**

[image1]: data:image/png;base64,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
