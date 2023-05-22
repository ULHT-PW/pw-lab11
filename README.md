**UNIVERSIDADE LUSÓFONA**

# Lab 11: Blog Estruturado

### Objetivo: 
* exercicio de laboratório a realizar durante a aula
* Exercitar os conceitos de modelação aprendidos, criando uma pequena aplicação com uma base de dados que explora todos os tipos de relação.
* Engloba um conjundo de conhecimentos que deverá dominar, e que saem na frequencia final

### Jornal
Crie uma aplicação em django de raíz que implemente um blog com as seguintes características:
* O jornal deverá ter um nome e uma especialidade (informática, cultura, desporto, música, culinária, lazer, ... o que quiser).
* O jornal deverá estar sediado numa determinada morada. Numa morada apenas pode existir um jornal, e um jornal pode apenas ter uma morada.
* O jornal é diário. Está dividido em áreas. Cada área é constituida por uma compilação de artigos desse dia.
* O jornal tem um conjunto de áreas pré-definidas (por exemplo, se for de culinária, poderá ser entradas, pratos principais, sobremesas). A sequência das áreas que se apresentam no jornal é sempre semelhante
* Existe um conjunto de jornalistas que escrevem artigos para o jornal. Cada jornalista tem um nome e área de especialização em que escreve.
* Um artigo pode ser escrito por um ou mais jornalistas, tendo associado também uma data, área, título, texto e pode ter uma fotografia assim como um link.
* um artigo pode ter um ou mais comentários, que devem ter um título, nome do autor e texto.

### Criação e configuração da aplicação django
1. crie o seu projeto. Com a consola numa pasta à sua escolha para alojar o projeto, execute o comando `django-admin startproject config .` 
2. crie a aplicação jornal, com o comando `python manage.py startapp jornal`
4. em `config\settings.py`, adicione à lista INSTALLED_APPS a aplicação `jornal`. 
5. em `config\settings.py`, indique ainda onde guardará as imagens que carregar, associada a cada artigo. Para tal, adicione as linhas `MEDIA_URL = '/media/'`  e  `MEDIA_ROOT = os.path.join(BASE_DIR, 'media')`

### Models
1. Faça num papel a modelação com um Diagrama Entidade Relação e valide com o seu docente antes de continuar. Deverá explorar as relações OneToOne, ForeignKey e ManyToMany.
2. Implemente em `jornal\models.py` as classes necessárias para implementar a base de dados que permita modelar o jornal. Não se esqueça de especificar ocmo se apresentam as classes na forma de uma string, usando a função `__str__(self)__`.  
3. Registe todas as classes em admin.py. Por exemplo, para a classe `Artigo`  deverá inserir a instrução `admin.site-register(Artigo)`.
4. crie um ficheiro de migrações com `python manage-py makemigrations`, e migre as classes definidas para a base de dados com `python manage-py makemigrations`
5. crie um utilizador superuser com `python manage.py createsuperuser`. 
6. Aceda à aplicação admin, `127.0.0.1:8000/admin` que lhe permita aceder à aplicação admin. Insira alguns elementos na base de dados, para verificar se está tudo correto
7. aceda à shell de python com o comando `python manage-py shell` para manipular a base de dados usando o ORM em Python. Antes de mais, importe as classes com `from jornal.models import *`. Exercite a utilização de ORM implementando as seguintes operações que deverá guardar posteriormente num ficheiro "manipulations.py":
   * Crie dois jornalistas. garanta que ficam guardados na base de dados
   * crie um artigo escrito por ambos
   * Liste os artigos do jornal
   * liste os artigos de um determinado dia
   * liste os artigos de um determinado dia e de uma área específica
   * liste os artigos escritos por um determinado jornalista. Como Para tal, deve explicitar que o artigo existe num determinado. Crie um jornalista e dois artigos com pelo menos dois autores.
   * liste todos os artigos escritos por um jornalista num determinado intervalo de dias

### Views e Templates
12. uma vez testada a base de dados, crie o ficheiro urls.py na aplicação, e crie rotas para funções que respondem a pedidos HTTP request.
13. a aplicação deve permitir registar novos jornalistas. Para tal, crie em forms.py a classe para gerar o formulário.
14.  a aplicação deve apresentar um formulário que permita criar, editar ou apagar artigos 
15.  Renderize cada notícia na forma de um "postal" que apresente toda a informação de cada artigo. Renderize adequadamente o jornal, suas áreas e artigos, utilizando as técnicas de CSS grid e flexbox que aprendeu. 
16.  A aplicação deve permitir escolher um dia e visualizar o jornal desse dia, compilação de artigos desse dia, juntamente com eventuais comentários existentes. 
17.  cada artigo deve ter um botão que permita inserir um novo comentário. 
