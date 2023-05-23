**UNIVERSIDADE LUSÓFONA**

# Lab 11: Blog 📓

**Objetivo**
* Exercitar os conceitos de modelação aprendidos, com uma base de dados que explora todos os tipos de relação.
* Engloba um conjundo de conhecimentos que deverá dominar, e que saem na frequencia final
* Tente concluir na aula prática!
* Este exercício expande o [blog desenvolvido no lab10](https://github.com/ULHT-PW/pw-lab10/tree/main#1-blog). Mas se ainda não fez, comece a partir de aqui diretamente, e integre depois.

# Modelação
* veja com atenção estes [slides sobre modelação](https://moodle.ensinolusofona.pt/pluginfile.php/549222/mod_label/intro/pw-04-django-03-models.pdf)

# Modelação da aplicação blog
* O blog deverá ter uma conta associada. Uma conta apenas pode ter um blog. A conta é caracterizada por um link do repo github e do pythonanywhere onde está o projeto. Esta informação deve constar no rodapé
* O blog está dividido em áreas. Cada área é constituida por uma compilação de artigos.
* O blog tem um conjunto de áreas pré-definidas, mas que podem ser expandidas se desejável.
* Existe um conjunto de autores registados na base de dados que escrevem artigos para o jornal. Cada autor tem um nome e um conjunto de áreas de interesse (que se mapeiam com as áreas do blog).
* Um artigo pode ser escrito por um ou mais autores, tendo associado os campos data, área, título, texto, imagem, link, um conjunto de comentários e *likes*.
* um comentário tem um título e texto.
* um artigo pode ter, 0, 1  ou mais likes, tendo associado um contador que é apresentado no artigo, com um ícone, sendo um botão que qualquer pessoa pode clicar para que fique registado que gostou.

# Projeto Django
1. Se já fez o lab 10 Portfolio Parte II e tem a aplicação django a correr no pythonAnyWhere, abra-a e passe para a criação de Models.
2. Senão, siga o [video-tutorial para criação de app no PythonAnyWhere e sua edição num PC local](https://educast.fccn.pt/vod/clips/29lxpwwtds/html5.html?locale=pt).
3. alternativamente, pode criar diretamente um projeto local no seu PC da seguinte forma:
    1. Abra uma pasta vazia com o VS Code e execute na consola o comando `django-admin startproject config .` 
    2. crie a aplicação jornal, com o comando `python manage.py startapp jornal`
    4. em `config\settings.py`, adicione à lista INSTALLED_APPS a aplicação `jornal`. 
    5. em `config\settings.py`, indique ainda onde guardará as imagens que carregar, associada a cada artigo. Para tal, adicione as linhas `MEDIA_URL = '/media/'`  e  `MEDIA_ROOT = os.path.join(BASE_DIR, 'media')`

# Criação de Models (ficheiro `models.py`) e da base de dados 🛢
1. Faça num papel a modelação com um Diagrama Entidade Relação e valide com o seu docente antes de continuar. Deverá explorar as relações OneToOne, ForeignKey e ManyToMany.
2. Em `blog\models.py`, defina as classes necessárias para implementar a base de dados que permita modelar o blog. Não se esqueça de especificar ocmo se apresentam as classes na forma de uma string, usando a função `__str__(self)__`.  
3. Registe todas as classes em admin.py. Por exemplo, para a classe `Artigo`  deverá inserir a instrução `admin.site.register(Artigo)`.
4. crie um ficheiro de migrações com `python manage.py makemigrations`, e migre as classes definidas para a base de dados com `python manage.py migrate`
5. crie um utilizador superuser com `python manage.py createsuperuser`. 
6. Aceda à aplicação admin usando o seu browser e URL `127.0.0.1:8000/admin`. Este permitir-lhe-á aceder à aplicação admin. Autentique-se com as credenciais criadas. Insira alguns elementos na base de dados através do interface, para depois exercitar sobre estes dados:
   * crie um blog
   * crie um dono do blog
   * crie três áreas do blog (por exemplo, tecnologia, música, desporto)
   * crie dois autores
   * crie três artigos em cada área, uns escritos por um autor, outros por dois autores
   * crie dois comentários para cada artigo
   * incremente os likes de cada artigo de forma diferenciada

# Manipulação da base de dados (operações CRUD) com ORM django
1. aceda à shell de python com o comando `python manage.py shell` para manipular a base de dados usando o ORM em Python. 
2. Importe as classes definidas em models.py com a instrução `from blog.models import *`. 
2. Exercite na shell instruções do ORM Django para fazer operações CRUD na base de dados (no exame ser-lhe-á pedido para escrever instruções destes género, com base no [glossário]([url](https://moodle.ensinolusofona.pt/pluginfile.php/549224/mod_resource/content/4/PW_glossario_2023.pdf)) que terá disponivel no exame):
   * Crie mais dois autores. garanta que ficam guardados na base de dados. 
       * Pode usar o método create, `Autor.objects.create(nome='Luis')` que cria e guarda diretamente na base de dados.
       * Pode usar o construtor da classe, devendo depois gravar na base de dados: `a = Autor(nome='Luis')` e depois `a.save()`
   * na aplicação admin, consulte a tabela de autores, verificando se os autores criados ficaram devidamente armazenados na base de dados. Atribua uma área a cada autor.
   * liste todos os autores da base de dados com o comando `Autores.objects.all()`
   * liste as áreas existentes,  com o comando `areas = Area.objects.all()`
   * aceda ao primeiro elemento da lista com `area = areas[0]`. obtenha a sua chave primária e nome com `area.pk` e  `area.nome`
   * usando a chave primaria dessa área e o método filter, consulte os artigos que existem dessa área
   * crie um artigo escrito por ambos: primeiro crie um artigo com titulo e área. Depois deve adicionar cada um dos autores com o método Artigo.autores.add()
   * crie uma lista com todos os artigos do blog
   * itere com um ciclo pela lista e imprima cada um dos artigos 
   * liste os artigos escritos por um determinado autor. 
   * liste os artigos escritos por um determinado autor numa determinada área. 
   * ordene os artigos por likes, e identifique o artigo com maior numero de likes. 
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
1. sincronize o seu projeto com o seu repositorio GitHub. pode usar os seguintes comandos:
```Bash
git add .
git commit -m "blog expandido com mais classes"
git push
```
2. no PythonAnyWhere, atualize a sua aplicação com o comando `git pull`.
3. sincronize a base fazendo migração (`python manage.py makemigrations`) e sincronização da base de dados (`python manage.py migrate`).
4. lance novamente a aplicação.
