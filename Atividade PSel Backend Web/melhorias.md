 **Parte 2 - PSel - Melhorias propostas**
  
  _Resumo_:
    O presente documento aborda possíveis melhorias sugeridas ao projeto apresentado 

 
  **Tópicos de melhorias**
  
 **1. Reposicionar funções**
  
 Dentro da pasta _"/gravações(...)/"_ e da pasta _"/src"_ algumas funções são declaradas em um arquivo e são usadas somente uma vez em outro arquivo. Neste caso a importação a função ocorre somente uma vez portanto a mesma pode ser definida no único arquivo em que ela é utilizada, facilitando assim a consulta. Segue abaixo os casos de, função, arquivo de origem,  arquivo de destino 

  ~~~javascript
  * createEvent, "/utils/validators", "/routes/plataform.route"
  * updateDay, "/utils/validators", "/routes/plataform.route"
  * createEventObject, "/utils/validators", "/routes/plataform.route"
  * createEventosObject, "/utils/validators", "/routes/plataform.route"
  * logRequestStart, "/logs/requestLoogers", "/app"
  * handleError, "/errors/ErrorHandler", "/routes/plataform.route"
  *
  ~~~
  
  **2. Renomear ou comentar funções**
  
  A função _createEventObject_ capta os dados do Object e pode ser facilmente confundida com _createEventosObject_ que capta os dados do Evento a sugestão de melhoria nesse caso é chamar a primeira função de _createDataObject_ e a segunda função de _createEventObject_  capta os dados de um único evento por vez.
  
  Dentro da pasta _"Mocks"_ no arquivo _"MongoEvents"_ as funções a seguir não possuem corpo e são chamadas em nenhuma parte do código
  ~~~javascript
  * createEvent
  * getAll
  * countEvents
  * deleteEvent
  * updateEvent
  * updateEventPush
  ~~~
  Neste caso a sugestão de melhoria é apagar as funções que não tem utilidade, caso a função tenha utilidade um comentario dentro do corpo da mesma torna mais fácil o entendimento do motivo dela ter sido criada.
  
  
 **3. Organizar pastas**
  
  Algumas pastas possuem cada uma um arquivo, os arquivos destas pastas são pouco modificados pelo desenvolvedor após serem escritos. O conteúdo das seguintes pastas pode ser renomeado e com o nome da pasta que ele pertence e redirecionado para uma pasta unica chamada _"/org/"_
  
  ~~~javascript
  * config
  * dbs/mongo
  * errors
  * prometheus
  * __mocks__
  ~~~
  
  
 **4. Sugestão de funcionalidade: manipulação de rotas**
  
  As rotas definidas no projeto apresentam a opção de selecionar a camera desejada no dia desejado. O cliente pode selecionar o dia que ele quer ter acesso e todos os videos daquele dia são mostrados. Estabelecientos franqueados podem ter mais de um turno de trabalho podendo chegar a funcionar 24 horas por dia. Diferentes turnos podem ter diferentes demandas devido ao movimento variar e acordo com o horario. Ao ocorrer a troca de turno os funcionarios também são trocados, para o proprietario é mais facil ser notificado dos problemas de cada turno e assim acessar os videos de cada turno.
  A proposta de melhoria nesse caso seria criar mais seis rotas e as respectivas funções :

  ~~~javascript
  1. router.get('/:estabelecimento/:camera/:dia/:turno', handleGetCameraDiaTurno())
  2. router.get('/:estabelecimento/:camera/:dia/:turno/query', handleGetCameraDiaTurnoQuery())
  3. router.put('/:estabelecimento/:camera/:dia/:turno', validator.updateDay(), handlePutCameraDiaTurno())
  4. router.put('/:estabelecimento/:camera/:dia/:turno/:id', validator.updateEvent(), handlePutCameraDiaTurnoId())
  5. router.delete('/:estabelecimento/:camera/:dia/:turno', handleDeleteCameraDiaTurno())
  6. router.delete('/:estabelecimento/:camera/:dia/:turno/:id', handleDeleteCameraDiaTurnoId())
  ~~~
  
  
