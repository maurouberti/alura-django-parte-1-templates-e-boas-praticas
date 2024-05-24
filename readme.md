![Static Badge](https://img.shields.io/badge/Alura-%230b182c)
![Static Badge](https://img.shields.io/badge/Django-4.2.13-%23092E20?logoColor=ffffff)

# Iniciar

```
cp .env.example .env
virtualenv venv
source venv/bin/activate          # Ativar o ambiente virtual (Linux/macOS)
pip install -r requirements.txt   # Instalar todas as dependências
python manage.py collectstatic    # Executar o comando collectstatic
python manage.py runserver        # Subir servidor
deactivate                        # Sair do ambiente virtual
```

# Passo a passo do curso

## 1 - Iniciando aplicação e subindo servidor

Criar um ambiente virtual dentro do diretório do projeto

```
virtualenv venv
```

Entrar no ambiente virtual

```
source venv/bin/activate
```

Sair do ambiente virtual

```
deactivate
```

Instalar o django

```
pip install django
```

Criar arquivo com as dependências e pacotes do Python

```
pip freeze > requirements.txt
```

Criar projeto django

```
django-admin startproject setup .
```

Rodar o servidor

```
python manage.py runserver
```

## 2 - Configurações, git e github

Alterar idioma e horario do brasil no arquivo de configurações do projeto **setup/settings.py**

```
LANGUAGE_CODE = 'pt-br'
TIME_ZONE = 'America/Sao_Paulo'
```

Instalar o pacote `python-dotenv`

```
pip install python-dotenv
pip freeze > requirements.txt
```

Alterar o arquivo de configurações **setup/settings.py**

```
from dotenv import load_dotenv
load_dotenv()
...
SECRET_KEY = str(os.getenv('SECRET_KEY'))
```

Criar arquivo **.env**

Criar arquivo **.gitignore** e adicionar repositório github.

## 3 - Projeto, app e views

Criar um **app**

```
python manage.py startapp galeria
```

Adicionar o **app** no arquivo de configurações **setup/settings.py**

```
INSTALLED_APPS = [
    ...
    'galeria',
]
```

Alterar arquivo de rota **setup/urls.py**  
Alterar arquivo de view **galeria/views.py**  
Criar um novo arquivo de rota **galeria/urls.py**  

Criar pasta **templates** com os arquivos **.html**  
Adicionar o caminho da pasta **templates** no arquivo de configurações **setup/settings.py**

```
TEMPLATES = [
    {
        ...
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        ...
    },
]
```

## 4 - Arquivos estáticos

Criar pasta **setup/static**  
Adicionar no arquivo de configurações **setup/settings.py**

```
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'setup/static')
]
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```

Executar o comando para criar a pasta **static**

```
python manage.py collectstatic
```

Adicionar no arquivo **template/galeria/index.html**

```
{% load static %}
```

### Criar nova pagina

Criar arquivo **templates/galeria/imagem.html**  
Criar view (controller) no arquivo **galeria/views.py**  
Criar rota no arquivo **galeria/urls.py**  

## 5 - Boas práticas e partials

No arquivo de rota **galeria/urls.py** adicionado um `name`

```
path('imagem/', imagem, name='imagem')
```

No arquivo **templates/galeria/index.html** alterado os `hred`

```
href="{% url 'imagem' %}"
```

### Método DRY (Don't Repeat Yourself - Não se repita)

Criar arquivo **galeria/base.html**  
Inserir no arquivo **galeria/base.html** os trechos de código que se repetem em index.html e imagem.html.

Criar arquivo **galeria/paartials/_footer_.html**  
Inserimos dentro de **galeria/paartials/_footer_.html** o código de imagem.html e index.html correspondente ao rodapé.
