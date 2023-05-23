**UNIVERSIDADE LUSÓFONA**

# Lab 11: Blog
Exercício que expande o [blog do lab10](https://github.com/ULHT-PW/pw-lab10/tree/main#1-blog).

**Objetivo**
* Exercitar os conceitos de modelação aprendidos, com uma base de dados que explora todos os tipos de relação.
* Engloba um conjundo de conhecimentos que deverá dominar, e que saem na frequencia final

### Blog
* O blog deverá ter um dono, que é um autor. Um autor apenas pode ter um blog.
* O blog está dividido em áreas. Cada área é constituida por uma compilação de artigos.
* O blog tem um conjunto de áreas pré-definidas, mas que podem ser expandidas se desejável.
* Existe um conjunto de autores registados na base de dados que escrevem artigos para o jornal. Cada jornalista tem um nome e áreas de interesse (que se mapeiam com as áreas do blog).
* Um artigo pode ser escrito por um ou mais autores, tendo associado os campos data, área, título, texto, imagem, link, um conjunto de comentários e *likes*.
* um comentário tem um título e texto.
* um artigo pode ter, 0, 1  ou mais likes, tendo associado um contador que é apresentado no artigo, com um ícone, sendo um botão que qualquer pessoa pode clicar para que fique registado que gostou.

### Criação e configuração da aplicação django
só execute estes passos se não tem nenhum projeto: 
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
6. Aceda à aplicação admin, `127.0.0.1:8000/admin` que lhe permita aceder à aplicação admin. Insira alguns elementos na base de dados, para verificar se está tudo correto:
   * crie um blog
   * crie um dono
   * crie duas áreas
   * crie dois autores
   * crie dois artigos, um escrito por um autor, outro por dois autores
   * inseria em cada dois comentarios e likes
8. aceda à shell de python com o comando `python manage-py shell` para manipular a base de dados usando o ORM em Python. Antes de mais, importe as classes com `from jornal.models import *`. 
9. Exercite a utilização de instruções do ORM Django para fazer operarções CRUD na bse de dados. Crie um ficheiro Jupyter na pasta journal e implemente as seguintes operações (no exame ser-lheá pedidp ara escrever instruções destes género):
   * primeiro, importe a base de dados, com a instrução `from journal.models import *`
   * Crie dois autores. garanta que ficam guardados na base de dados. Pode usar o método create, que cria e guarda. ou o construtor da classe, que retorna um objeto que deve depois ser guardado.
   * consulte os autores armazenados na base de dados, e confira que existem
   * consulte uma das áreas
   * crie um artigo escrito por ambos, inserindo o titulo e área. depois deve adicionar cada um dos autores com o método Artigo.autores.add()
   * Liste os artigos do jornal
   * liste os artigos escritos por um determinado autor. 
   * ordene os artigos por likes, e identifique o artigo com maior numero de likes 
   * adicione um comentário ao artigo com mais likes
   * liste todos os artigos escritos por um autor num determinado intervalo de dias

### Views e Templates
12. uma vez testada a base de dados, crie o ficheiro urls.py na aplicação, e crie rotas para funções que respondem a pedidos HTTP request.
13. a aplicação deve permitir registar novos jornalistas. Para tal, crie em forms.py a classe para gerar o formulário.
14.  a aplicação deve apresentar um formulário que permita criar, editar ou apagar artigos 
15.  Renderize cada notícia na forma de um "postal" que apresente toda a informação de cada artigo. Renderize adequadamente o jornal, suas áreas e artigos, utilizando as técnicas de CSS grid e flexbox que aprendeu. 
16.  A aplicação deve permitir escolher um dia e visualizar o jornal desse dia, compilação de artigos desse dia, juntamente com eventuais comentários existentes. 
17.  cada artigo deve ter um botão que permita inserir um novo comentário. 
