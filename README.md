#Todo com React, TypeScript, NodeJS e MongoDB

# extrutura do projeto 
  ├── dist
  ├── node_modules
  ├── src
    ├── app.ts
    ├── controllers
    |  └── todos
    |     └── index.ts
    ├── models
    |  └── todo.ts
    ├── routes
    |  └── index.ts
    └── types
        └── todo.ts
  ├── nodemon.json
  ├── package.json
  ├── tsconfig.json

  Como você pode ver, essa estrutura de arquivo é relativamente simples. 
  O [dist] diretório servirá como uma pasta de saída assim que o código for compilado para JavaScript simples. 
  Também temos um [app.ts] arquivo que é o ponto de entrada do servidor. 
  Os controladores, tipos e rotas também estão em seus respectivos nomes de pastas.
  Agora, precisamos configurar o [tsconfig.json] arquivo para ajudar o compilador a seguir nossas preferências

no arquivo [tsconfig.json] temos quatro propriedades principais a sublinhar:

[outDir]: diz ao compilador para colocar o código compilado na [dist/js] pasta.
[rootDir]: informa o TypeScript para compilar todos os .tsarquivos localizados na [src] pasta.
[include]: Diz ao compilador para incluir os arquivos que estão no [src] diretório e no subdiretório.
[exclude]: Exclui os arquivos ou pastas passados ​​no array durante o tempo de compilação.

Agora podemos instalar as dependências para habilitar o TypeScript no projeto.  
  yarn add typescript -g
  
dependência para usar Express e MongoDB
  yarn add express cors mongoose

tipos como dependências de desenvolvimento para ajudar o compilador TypeScript a entender os pacotes
  yarn add -D @types/node @types/express @types/mongoose @types/cors

dependências para poder compilar o código TypeScript e iniciar o servidor simultaneamente
  yarn add -D concurrently nodemon

Com isso implementado, agora podemos atualizar o [package.json] arquivo com os scripts necessários para iniciar o servidor.

Dentro do [package.json] o [concurrently] ajudará a compilar o código TypeScript, continue observando as alterações e também iniciará o servidor simultaneamente

Agora podemos iniciar o servidor - no entanto, ainda não criamos nada significativo a esse respeito.

# types / todo.ts
  Aqui, temos uma interface Todo que estende o [Document] tipo fornecido por [mongoose] que usaremos posteriormente para interagir com o MongoDB. 
  Dito isso, agora podemos definir a aparência de um modelo Todo.

# models / todo.ts
  Como você pode ver aqui, começamos importando a interface [ITodo] e alguns utilitários de mongoose. 
  Este último ajuda a definir o esquema Todo e também passa [ITodo] como um tipo para o modelantes de exportá-lo.
  Com isso, agora podemos usar o modelo Todo em outros arquivos para interagir com o banco de dados.

# controllers / todos / index.ts
  Aqui, primeiro precisamos importar alguns tipos de [express] porque desejo digitar os valores explicitamente. 
  Se você também quiser, pode deixar que o TypeScript deduza isso para você.
  Em seguida, usamos a função getTodos()para buscar dados. Ele recebe um reqe resparâmetros e retorna uma promessa.
  E com a ajuda do Todomodelo criado anteriormente, podemos agora obter dados do MongoDB e retornar uma resposta com o array de todos

# METHODs ------
  # ADD Todo
  Como você pode ver, a função [addTodo()] recebe o objeto body que contém os dados inseridos pelo usuário.
  Em seguida, eu uso typecasting para evitar erros de digitação e restringir a [body] variável para corresponder [ITodo]
  Em seguida, criar um novo [Todo] baseado no modelo.
  Com isso no lugar, agora podemos salvar o Todo no banco de dados
  E retornar uma resposta que contém o todo criado e o array todos atualizado.

  # UPDATE Todo
  Para atualizar um todo, precisamos extrair o id e o corpo da [req] objeto e depois passá-los para [findByIdAndUpdate()].
  Este utilitário encontrará o Todo no banco de dados e o atualizará. E assim que a operação for concluída, podemos agora retornar os dados atualizados para o usuário.

  # DELETE Todo
  A função [deleteTodo()] permite excluir um Todo do banco de dados. 
  Aqui, retiramos o id de req e o passamos como um argumento para [findByIdAndRemove()] ,
  para acessar o Todo correspondente e excluí-lo do banco de dados.
  A seguir, exportamos as funções para poder utilizá-las em outros arquivos. 
  Dito isso, agora podemos criar algumas rotas para a API e usar esses métodos para lidar com as solicitações.

# routes / index.ts
 >Crie rotas de API

  Como você pode notar aqui, temos quatro rotas para obter, adicionar, atualizar e excluir todos do banco de dados. 
  E como já criamos as funções, a única coisa que temos que fazer é importar os métodos e passá-los como parâmetros para tratar as requisições.

  Até agora, cobrimos muito, mas ainda assim, nenhum servidor para iniciar. 

  >Crie um servidor
  Antes de criar o servidor, precisamos primeiro adicionar algumas variáveis ​​de ambiente que conterão as credenciais do MongoDB no [nodemon.json] arquivo.
  Você pode obter as credenciais criando um novo cluster no <a href="https://www.mongodb.com/cloud/atlas">MongoDB Atlas</a>

 # app.ts
  Aqui, começamos por importar a [express] biblioteca que nos permite acessar o [use()] método que auxilia no manejo das rotas de Todos.
  Em seguida, usamos o [mongoose] pacote para conectar ao MongoDB anexando ao URL as credenciais mantidas no nodemon.jsonarquivo.
  Dito isso, agora, se nos conectarmos com sucesso ao MongoDB, o servidor iniciará, se apropriado, um erro será gerado.
  Agora terminamos de construir a API com Node, Express, TypeScript e MongoDB. 
  
  Temos agora, começar a construir o aplicativo do lado do cliente com React e TypeScript. 