**UNIVERSIDADE LUSÓFONA**

# Lab 11: Blog 📓
Exercício que expande o [blog do lab10](https://github.com/ULHT-PW/pw-lab10/tree/main#1-blog).

**Objetivo**
* Exercitar os conceitos de modelação aprendidos, com uma base de dados que explora todos os tipos de relação.
* Engloba um conjundo de conhecimentos que deverá dominar, e que saem na frequencia final
* Concluir na aula prática!

# Características 😎
* O blog deverá ter uma conta associada. Uma conta apenas pode ter um blog. A conta é caracterizada por um link do repo github e do pythonanywhere onde está o projeto. Esta informação deve constar no rodapé
* O blog está dividido em áreas. Cada área é constituida por uma compilação de artigos.
* O blog tem um conjunto de áreas pré-definidas, mas que podem ser expandidas se desejável.
* Existe um conjunto de autores registados na base de dados que escrevem artigos para o jornal. Cada jornalista tem um nome e áreas de interesse (que se mapeiam com as áreas do blog).
* Um artigo pode ser escrito por um ou mais autores, tendo associado os campos data, área, título, texto, imagem, link, um conjunto de comentários e *likes*.
* um comentário tem um título e texto.
* um artigo pode ter, 0, 1  ou mais likes, tendo associado um contador que é apresentado no artigo, com um ícone, sendo um botão que qualquer pessoa pode clicar para que fique registado que gostou.

# Criação e configuração da aplicação django
só execute estes passos se não tem nenhum projeto: 
1. crie o seu projeto. Com a consola numa pasta à sua escolha para alojar o projeto, execute o comando `django-admin startproject config .` 
2. crie a aplicação jornal, com o comando `python manage.py startapp jornal`
4. em `config\settings.py`, adicione à lista INSTALLED_APPS a aplicação `jornal`. 
5. em `config\settings.py`, indique ainda onde guardará as imagens que carregar, associada a cada artigo. Para tal, adicione as linhas `MEDIA_URL = '/media/'`  e  `MEDIA_ROOT = os.path.join(BASE_DIR, 'media')`

# Models 🛢
1. Faça num papel a modelação com um Diagrama Entidade Relação e valide com o seu docente antes de continuar. Deverá explorar as relações OneToOne, ForeignKey e ManyToMany.
2. Em `blog\models.py`, [defina as classes](https://moodle.ensinolusofona.pt/pluginfile.php/549222/mod_label/intro/pw-04-django-02.pdf?#page=4) necessárias para implementar a base de dados que permita modelar o blog. Não se esqueça de especificar ocmo se apresentam as classes na forma de uma string, usando a função `__str__(self)__`.  
3. Registe todas as classes em admin.py. Por exemplo, para a classe `Artigo`  deverá inserir a instrução `admin.site-register(Artigo)`.
4. crie um ficheiro de migrações com `python manage-py makemigrations`, e migre as classes definidas para a base de dados com `python manage-py migrate`
5. crie um utilizador superuser com `python manage.py createsuperuser`. 
6. Aceda à aplicação admin, `127.0.0.1:8000/admin` que lhe permita aceder à aplicação admin. Insira alguns elementos na base de dados, para verificar se está tudo correto:
   * crie um blog
   * crie um dono
   * crie duas áreas
   * crie dois autores
   * crie dois artigos, um escrito por um autor, outro por dois autores
   * inseria em cada dois comentarios e likes
8. aceda à shell de python com o comando `python manage-py shell` para manipular a base de dados usando o ORM em Python. Antes de mais, importe as classes com `from blog.models import *`. 
9. Exercite a utilização de instruções do ORM Django para fazer operações CRUD na base de dados. Crie um ficheiro Jupyter na pasta journal e implemente as seguintes operações (no exame ser-lheá pedidp ara escrever instruções destes género):
   * primeiro, importe a base de dados, com a instrução `from journal.models import *`
   * Crie dois autores. garanta que ficam guardados na base de dados. Pode usar o método create, que cria e guarda. ou o construtor da classe, que retorna um objeto que deve depois ser guardado.
   * consulte os autores armazenados na base de dados, e confira que existem
   * consulte uma das áreas
   * crie um artigo escrito por ambos: primeiro crie um artigo com titulo e área. Depois deve adicionar cada um dos autores com o método Artigo.autores.add()
   * Liste os artigos do blog
   * liste os artigos escritos por um determinado autor. 
   * ordene os artigos por likes, e identifique o artigo com maior numero de likes 
   * adicione um comentário ao artigo com mais likes
   * liste todos os artigos escritos por um autor num determinado intervalo de dias

# Views e Templates 🏖
1. uma vez testada a base de dados, crie o ficheiro urls.py na aplicação, e crie rotas (em urls.py) para funções (em views.py) que respondem a pedidos HTTP request com ficheiros HTML.
2. a aplicação deve permitir registar novos autores. Para tal, crie em forms.py a classe para gerar o formulário.
3.  a aplicação deve apresentar um formulário que permita criar, editar ou apagar artigos 
4.  Renderize cada notícia na forma de um "postal" que apresente toda a informação de cada artigo. Renderize adequadamente o blog, suas áreas e artigos, utilizando as técnicas de CSS grid e flexbox que aprendeu. 
5.  cada artigo deve ter um botão que permita inserir um novo comentário. 
6.  cada artigo deve ter uma estrela que permita inserir um "like". 


# Models e Views restantes 🛢
* Crie em casa classes para as restantes entidades que foram identificadas no Lab 10 e respetivas views que permitam listar os elementos disponviceis na base de dados.
* Procure estabelecer relações entre tabelas.

# Finalização ☁
1. sincronize o seu projeto com o seu repositorio GitHub. pode usar os seguitnes comandos:
```Bash
git add .
git commit -m "blog expandido com mais classes"
git push
```
2. no PythonAnyWhere, atualize a sua aplicação com o comando `git pull`.
3. sincronize a base fazendo migração (`python manage.py makemigrations`) e sincronização da base de dados (`python manage.py migrate`).
4. lance novamente a aplicação.
