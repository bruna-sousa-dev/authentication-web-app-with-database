![Python](https://img.shields.io/badge/Python-3.11-blue)
![Flask](https://img.shields.io/badge/Flask-API-black)
![SQLite](https://img.shields.io/badge/SQLite-Database-blue)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-ORM-red)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![Gunicorn](https://img.shields.io/badge/Gunicorn-WSGI-green)
![Render](https://img.shields.io/badge/Deploy-Render-purple)
![GitHub Pages](https://img.shields.io/badge/Frontend-GitHub%20Pages-black)
![License](https://img.shields.io/badge/License-MIT-blue)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)

# Aplicação WEB Fullstack para Autenticação de Usuários 

**Solução Full Stack desacoplada para autenticação de usuários com persistência em banco de dados SQLite.**

🔗 [Clique aqui para testar a aplicação](https://bruna-sousa-dev.github.io/authentication-web-app-with-database)

🔗 [Clique aqui para acessar a imagem Docker do backend](https://hub.docker.com/r/brunasousadev/authenticationwebappwithdatabase)

## 🌐 Overview

Esta aplicação é uma solução **Full Stack** desacoplada para autenticação e gerenciamento de usuários, composta por:
* Uma API RESTful desenvolvida em Flask, com autenticação segura via sessões e integração com banco de dados SQLite.
* Um frontend estático construído com HTML, CSS e JavaScript, que interage com a API via requisições HTTP, simulando um fluxo real de autenticação.
* Containerização via Docker, com deploy automatizado na Render, garantindo escalabilidade e reprodutibilidade do ambiente de produção.

Essa estrutura separada entre cliente e servidor segue as práticas modernas de desenvolvimento web, permitindo maior flexibilidade, manutenibilidade e segurança. O backend pode ser consumido por qualquer cliente (web, mobile, etc.), enquanto o frontend pode ser substituído ou estendido sem impacto na lógica de autenticação.

---

## 🛠️ Arquitetura

- **Backend**
  - API RESTful construída com Flask
  - Containerização com Docker
  - Utilização do Gunicorn como servidor WSGI
  - Implantação na Render
  - Autenticação de usuários
  - Gerenciamento de banco de dados SQLite

- **Frontend**
  - Site estático (HTML, CSS, JavaScript)
  - Hospedado em GitHub Pages
  - Interação com o backend por meio de solicitações HTTP seguras

---

## ✨ Características
- Autenticação de usuário e tratamento de sessão
- Frontend e backend desacoplados
- Compartilhamento de recursos de origem cruzada (CORS) habilitado para comunicação segura

---

## 🔐 Autenticação e Gerenciamento de Sessão

O sistema de autenticação é implementado usando [Flask-Login](https://flask-login.readthedocs.io/en/latest/) para gerenciamento de sessão do usuário e [Werkzeug Security](https://werkzeug.palletsprojects.com/en/2.3.x/utils/#module-werkzeug.security) para hashing e verificação de senha segura.

**Principais recursos:**
- Tratamento de sessão do usuário via `LoginManager`
- `UserMixin` fornece implementações padrões para métodos de usuário comuns
- As senhas são armazenadas com segurança usando `generate_password_hash`
- O login do usuário é validado usando `check_password_hash`
- As rotas são protegidas com `@login_required`

> ✅ Esses recursos garantem sessões criptografadas e seguras, compatíveis com solicitações de origem cruzada (CORS), ideais para frontends desacoplados modernos.

---

## 📬 API Endpoints

| Método | Endpoint         | Descrição                               | Lógica de Login     | Lógica de administração      |
|--------|------------------|-----------------------------------------|---------------------|------------------------------|
| GET    | `/check_session` | Verificar sessão ativa                  | Login requerido     | Qualquer usuário             |
| GET    | `/debug_session` | Depurar sessão ativa                    | Login requerido     | Qualquer usuário             |
| POST   | `/del_user`      | Deletar usuário                         | Login requerido     | Apenas usuário administrador |
| PUT    | `/edit_user`     | Editar usuário                          | Login requerido     | Apenas usuário administrador |
| GET    | `/get_test_user` | Retornar o usuário de teste registrado" | Login não requerido | Qualquer usuário             |
| GET    | `/hello_world`   | Retornar "Hello World"                  | Login não requerido | Qualquer usuário             |
| POST   | `/login`         | Logar usuário                           | Login não requerido | Qualquer usuário             | 
| GET    | `/logout`        | Deslogar usuáio                         | Login requerido     | Qualquer usuário             | 
| POST   | `/register`      | Registrar novo usuário                  | Login requerido     | Apenas usuário administrador |
| GET    | `/users`         | Listar usuários registrados             | Login requerido     | Qualquer usuário             |

---

## 📎 Tecnologias

### ⬅️ Backend
- Python 3
- Flask
- Flask-Login
- Flask-CORS
- Flask-Session
- Flask-SQLAlchemy
- SQLite
- Gunicorn
- Docker
- Werkzeug Security (Password Hashing)
- Render

### ➡️ Frontend
- HTML5 + CSS3 + JavaScript
- Github Pages
- .htaccess – configuração de cache para garantir que os arquivos atualizados sejam carregados
- robots.txt – bloqueio de indexação por mecanismos de busca protegendo áreas específicas
- sitemap.xml – definição da estrutura de URL para indexação eficiente por mecanismos de busca

---

# 🚀 Deploy com Docker – Containerização da API

Este repositório demonstra o uso de **Docker** para conteinerizar uma API Flask backend, destacando boas práticas de construção e distribuição de imagens Docker.

A aplicação foi **implantada na Render**, e a imagem Docker foi publicada no **Docker Hub** para facilitar a reprodutibilidade.

> **Nota sobre persistência de dados na Render**  
> Esta versão utiliza **SQLite** para simplificar o deploy e remover a dependência de um serviço PostgreSQL externo. Em containers Docker, o banco SQLite é armazenado em arquivo. Por isso, em ambientes como a Render, recomenda-se configurar um **Persistent Disk** caso seja necessário manter os dados após redeploys, reinicializações ou recriações do serviço.

---

## 🐳 Sobre o Uso do Docker

A conteinerização da API foi realizada utilizando apenas o **Docker CLI**, sem uso de `docker-compose`. A decisão de não utilizar o Docker Compose foi técnica e estratégica:

> **Motivo da não utilização do Docker Compose**  
> O serviço de hospedagem utilizado (Render) requer uma única imagem Docker para o deploy. O uso do Docker Compose é recomendado quando há múltiplos containers interdependentes (por exemplo, uma API, um banco de dados e um cache). Como este projeto consiste apenas em uma API isolada, o Docker Compose seria redundante e não compatível com o ambiente de deploy.

---

## 📦 Estrutura do Docker

### `Explicação detalhada do Dockerfile`

O `Dockerfile` abaixo foi projetado para criar uma imagem leve e otimizada de uma aplicação Python. Ele é estruturado em camadas com foco em performance, segurança e compatibilidade com ambientes de produção.

```Dockerfile
FROM python:3.11-slim
```
* **Base da imagem**: Utiliza a imagem oficial do Python 3.11 em sua versão slim, que é significativamente menor em tamanho comparada à versão completa. Isso reduz o tempo de build, o consumo de banda e o espaço ocupado na hospedagem.

```Dockerfile
ENV DEBIAN_FRONTEND=noninteractive
```
* **Evita prompts interativos** durante a instalação de pacotes. Essa variável de ambiente impede que comandos apt solicitem interação do usuário durante o processo de instalação (útil especialmente em ambientes automatizados como Docker).

```Dockerfile
WORKDIR /app
```
* Define o diretório de trabalho dentro do container como /app. Todos os comandos subsequentes (COPY, RUN, CMD etc.) serão executados a partir deste diretório.

```Dockerfile
COPY requirements.txt .
```
* Copia apenas o arquivo requirements.txt para o diretório de trabalho. Isso permite instalar dependências em uma camada separada, melhorando o cache do Docker.

```Dockerfile
RUN pip install --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt && \
    pip install --no-cache-dir gunicorn
```
* Atualiza o pip para a versão mais recente.
* Instala as dependências do projeto listadas no requirements.txt.
* Instala o Gunicorn, um servidor WSGI de produção, que é uma boa prática para aplicações Python (como Flask ou FastAPI) em ambiente real.
* A flag --no-cache-dir evita que o cache do pip seja salvo na imagem final, reduzindo seu tamanho.

```Dockerfile
COPY . .
```
* Copia todo o conteúdo do diretório atual (onde está o Dockerfile) para dentro do container no diretório /app.

```Dockerfile
COPY start.sh /start.sh
RUN chmod +x /start.sh
```
* Copia o script de inicialização start.sh para a raiz do container e concede permissão de execução. Este script inicializa o servidor Gunicorn.

```Dockerfile
EXPOSE 5000 80 443
```
* Documenta que o container expõe as portas 5000, 80 e 443. Isso é uma declaração informativa para orquestradores e serviços de rede — por si só não abre as portas no host.

```Dockerfile
CMD ["/start.sh"]
```
* Define o comando padrão que será executado quando o container for iniciado. Aqui, o `start.sh` é usado como ponto de entrada, centralizando a lógica de inicialização da aplicação.

#### Esta estrutura modular garante:
* Builds mais rápidos graças ao cache eficiente.
* Uma imagem final leve (base slim + sem cache pip).
* Facilidade de manutenção e clareza na inicialização.
* Compatibilidade com provedores como Render, Heroku e outros que exigem um único processo principal rodando no container.

### `Explicação detalhada do .dockerignore`

O arquivo .dockerignore funciona de forma semelhante ao .gitignore, mas é utilizado pelo Docker durante o processo de build. Ele informa ao Docker quais arquivos e diretórios devem ser ignorados ao copiar conteúdo para a imagem, o que melhora a performance e reduz o tamanho da imagem final.

```.dockerignore
**/__pycache__
```
* Ignora todos os diretórios __pycache__, independentemente de onde estejam na estrutura do projeto (graças ao **/).
* Esses diretórios são gerados automaticamente pelo Python para armazenar bytecode compilado, e não são necessários dentro da imagem Docker, já que o código será recompilado dentro do container.
* Excluí-los evita poluição no sistema de arquivos da imagem e reduz o tamanho final.

```.dockerignore
venv
```
* Ignora o diretório venv, que é utilizado para armazenar o ambiente virtual local de desenvolvimento.
* Esse ambiente não deve ser incluído na imagem Docker, pois a imagem já define seu próprio ambiente baseado em uma imagem oficial do Python (python:3.11-slim), incluir o venv local poderia causar conflitos de dependências e aumentar desnecessariamente o tamanho da imagem e, a instalação de dependências é tratada de forma isolada com pip install -r requirements.txt.

```.dockerignore
.pre-commit-config.yaml
```
* Esse arquivo é usado para configurar o Pre-commit, uma ferramenta que executa "ganchos" antes de você fazer um commit, como verificação de formatação, lint, remoção de espaços em branco, etc.
* Esse tipo de configuração é relevante apenas para desenvolvimento local. Ele não precisa estar na imagem Docker final, já que não influencia na execução do aplicativo em produção. Ignorá-lo evita enviar arquivos desnecessários ao docker build.

```.dockerignore
postman_collection.json
```
* Esse é um arquivo de exportação do Postman, contendo uma coleção de requisições HTTP para testar APIs.
* Esse arquivo é útil para testes locais ou documentação da API, mas não é necessário no ambiente de execução do container. Incluir esse arquivo na imagem só aumentaria o tamanho sem motivo.

#### Benefícios de um .dockerignore bem configurado:
* Performance: evita a cópia de arquivos desnecessários, acelerando o build.
* Segurança: impede que arquivos sensíveis ou irrelevantes sejam enviados para a imagem.
* Imagens menores: contribui para imagens mais leves e eficientes, otimizando o deploy.

---

## 🔑 Comandos Docker Utilizados

Abaixo estão os comandos utilizados para gerar a imagem Docker e subir para o Docker Hub:

1. Build da imagem
```docker
docker build -t usuario_dockerhub/nome-da-api:latest .
```

2. Login no Docker Hub
```docker
docker login
```

3. Push da imagem para o Docker Hub
```docker
docker push usuario_dockerhub/nome-da-api:latest
```

---

# ✅ Rodando a API localmente

Você pode executar esta aplicação localmente de três maneiras: utilizando a imagem Docker pública disponibilizada no Docker Hub, usando Docker para gerar a imagem você mesmo ou executando diretamente com Python.

---

## 📥 Utilizando a imagem presente no Docker Hub (recomendado)

A imagem está disponível publicamente no Docker Hub.

Link da Imagem: [Acesse a imagem Docker aqui](https://hub.docker.com/r/brunasousadev/fullstackauthenticationwebappwithdatabase)

Como baixar e executar:

```docker
docker pull brunasousadev/fullstackauthenticationwebappwithdatabase
docker run -d -p 5000:5000 -e DATABASE_URL=sqlite:////app/app.db --name authenticationwebappwithdatabase brunasousadev/fullstackauthenticationwebappwithdatabase
```

---

## 🧩 Gerando a imagem Docker (recomendado)

Certifique-se de ter o Docker instalado em sua máquina: [Instalar Docker](https://docs.docker.com/get-started/get-docker/)

Passos:
```bash
# Clone o repositório
git clone https://github.com/bruna-sousa-dev/fullstack-authentication-web-app-with-database.git
cd fullstack-authentication-web-app-with-database
cd backend

# Construa a imagem Docker
docker build -t flask-auth-api .

# Execute o container
docker run -d -p 5000:5000 \
  -e DATABASE_URL=sqlite:////app/app.db \
  flask-auth-api
```
A aplicação estará disponível em http://localhost:5000

Para persistir o arquivo SQLite fora do ciclo de vida do container, você pode montar um volume local:

```bash
docker run -d -p 5000:5000 \
  -e DATABASE_URL=sqlite:////app/data/app.db \
  -v ${PWD}/data:/app/data \
  flask-auth-api
```

---

## 🧫 Executando sem Docker (modo desenvolvimento)

Pré-requisitos:
* Python 3.11+
* SQLite, utilizado diretamente pela aplicação por meio do Flask-SQLAlchemy. Não é necessário instalar ou configurar um servidor de banco de dados externo.

#### Passos:
```bash
# Clone o repositório
git clone https://github.com/bruna-sousa-dev/fullstack-authentication-web-app-with-database.git
cd fullstack-authentication-web-app-with-database
cd backend

# (Opcional) Crie e ative um ambiente virtual
python -m venv .venv
source .venv/bin/activate  # Linux/macOS
.venv\Scripts\activate     # Windows

# Instale as dependências
python.exe -m pip install --upgrade pip
pip install -r requirements.txt
```

#### Configure as variáveis de ambiente:
No diretório `backend`, copie o arquivo `.env.example` e cole uma cópia com o nome `.env`. Esse arquivo será utilizado para definir as variáveis de ambiente necessárias para a execução local da API.

Exemplo:
```bash
cp .env.example .env
```

No Windows PowerShell:
```powershell
Copy-Item .env.example .env
```

Depois, confira se o arquivo `.env` contém as configurações necessárias:
```env
FLASK_APP=app.py
FLASK_ENV=development
SECRET_KEY=sua-chave-secreta
DATABASE_URL=sqlite:///app.db
DEFAULT_PASSWORD=defaut-password
```
Essa configuração cria/utiliza o arquivo `app.db` como banco de dados local da aplicação.

#### Inicialize o banco (se necessário):
```bash
flask shell
>>> from app import db
>>> db.create_all()
>>> exit()
```

#### Inicie o servidor Flask:
```bash
flask run
```
A aplicação estará disponível em http://localhost:5000

#### Observações importantes:
* Como o projeto utiliza SQLite, não é necessário manter um serviço externo de banco de dados em execução.
* Em ambiente Docker/Render, o banco pode ser configurado por meio da variável `DATABASE_URL=sqlite:////app/app.db`, utilizando caminho absoluto dentro do container.
* Caso a aplicação seja redeployada na Render sem disco persistente configurado, o arquivo SQLite pode ser recriado e os dados podem ser perdidos. Para persistência real em produção, configure um Persistent Disk na Render ou utilize um banco externo gerenciado.
* A aplicação foi projetada para permitir integração segura com frontends externos, habilitando CORS e gerenciamento de sessão via cookies.

## 🧪 Testando a API com o Postman

A API foi testada manualmente utilizando o Postman, uma ferramenta popular para desenvolvimento e testes de APIs REST. Esta abordagem permite validar os endpoints, as respostas, os códigos de status HTTP e o comportamento da API em diferentes cenários.

### Objetivos dos testes

* Verificar se os endpoints da API estão funcionando corretamente;
* Confirmar a resposta esperada (status, corpo da resposta, headers);
* Testar casos de sucesso e de erro (por exemplo, autenticação inválida, dados incompletos);
* Garantir que o deploy no ambiente de produção (Render) operará como esperado.

### Como os testes foram executados

1. Coleção Postman criada com os endpoints da API.
2. Cada requisição foi configurada com:
    * Método HTTP adequado (GET, POST, PUT, DELETE, etc.);
    * URL completa da API (por exemplo: http://localhost:5000/login);
    * Headers necessários (como Content-Type: application/json);
    * Corpo da requisição (para endpoints POST/PUT), utilizando JSON conforme a estrutura esperada;
    * Verificação manual da resposta, status code e conteúdo do body.

###  Importando os testes

Uma coleção do Postman foi exportada e está disponível aqui: [postman_collection.json](/backend/postman_collection.json).

Para utilizar:
1. Abra o Postman;
2. Vá em "Import";
3. Selecione o arquivo postman_collection.json;

Os endpoints estarão disponíveis e organizados para execução imediata.

#### Exemplo de teste

Requisição POST /login
* Body: 
```json
{
    "username": "test_user@mail.com", 
    "password": "123456789"
}
```
* Resposta esperada (Status code: 200 OK):
```json
{
    "message": "Login realizado com sucesso!",
    "success": true,
    "username": "test_user@mail.com"
}
```

---

# 📄 Licença
Este projeto está licenciado sob a Licença MIT.
Você pode usá-lo, modificá-lo, distribuí-lo e até mesmo integrá-lo em seus próprios projetos — seja para estudo, aprendizado ou criação de novos sistemas.

**Sinta-se à vontade para explorar, adaptar e evoluir este código da forma que mais contribuir para o seu aprendizado e crescimento como desenvolvedor(a)!**

📃 Leia o texto completo da licença [aqui](/LICENSE).

---

# 🤝 Contribuindo

Contribuições são **muito bem-vindas!**

Este repositório é um espaço aberto para aprendizado, compartilhamento de ideias e desenvolvimento colaborativo.

Você pode contribuir de várias formas:

* 💡 Sugerindo melhorias ou novas funcionalidades
* 🐞 Reportando bugs
* 🧪 Corrigindo problemas ou falhas
* 🧰 Refatorando o código ou melhorando a estrutura
* 📚 Melhorando a documentação ou escrevendo tutoriais

*As diretrizes para contrinuição estão presentes [aqui](/CONTRIBUTING.md)*

#### Toda ajuda é valiosa! Mesmo sugestões pequenas fazem a diferença ❤️

---

## 📌 Considerações Finais

Esta aplicação demonstra a implementação de uma arquitetura Full Stack modular, segura e escalável, ideal como base para projetos reais de autenticação de usuários. A separação entre frontend e backend promove a reutilização de componentes e facilita o deploy em ambientes distintos.

Além disso:

* O uso de Flask-Login e Werkzeug Security garante sessões e senhas criptografadas.
* A documentação dos endpoints e a explicação dos arquivos Docker facilitam a contribuição e o aprendizado.
* A decisão de não usar docker-compose torna o deploy em serviços como a Render mais simples e direto.
* O uso de arquivos como .htaccess, robots.txt e sitemap.xml no frontend demonstra preocupação com SEO e boas práticas de cache.

#### Sugestão de melhoria futura:
Implementar testes automatizados para os endpoints da API com ferramentas como pytest ou Postman + newman.

---

## 👩‍💻 Autor

Developed by Bruna Sousa.

Electronic Engineer | IoT Developer | Web Developer | AI Developer