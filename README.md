Insomnia: simulador de front-end

NEST.JS

    -Framework utilizada pela fluxo;
    -Framework é a interface entre servidor e aplicação;
    -Typescript;

INTRO WEB

    -Interação de máquinas virtuais, que têm a interface dos dados;
    -Frontend realiza requisições para o servidor onde o backend está hospedado;

    -Usa protocolos HTTP (hypertext transfer protocol) para trânsito de dados;

    JSON

        -Javascript Object Notation (semelhante ao dict do python);

    HTTP

        -Métodos (CRUD: Verbs)
            Create: Post
            Read:   Get
            Update: Patch/Put
            Delete: Delete
        
        ESTRUTURA PADRÃO DE ROTAS:

            /users                 -> rota para todos usuários
            /users/{id}            -> rota para um usuário específico
            /posts                 -> todos posts
            /users/{id}/posts      -> todos posts de um usuário
            /users/{id}/posts/{id} -> um post de um usuário em específico


----------------------------------------------------------------

PARTE PRÁTICA

    INICIALIZANDO A MÁQUINA VIRTUAL

        No path da pasta que será usada, inserir npm i -g @nestjs/cli

            -g (generate)

    INICIALIZANDO UM NOVO PROJETO

        nest new project-<nome projeto>

        ENTER para usar o gerenciador do node

        entrar na pasta inicializada
        
    PARA RODAR A APLICAÇÃO 

        npm run start:dev

        ROTA NO INSOMNIA:
            
            http://localhost:3000

----------------------------------------------------------------

BANCO DE DADOS (SQL):

    BAIXANDO ALGUMAS LIBS:

        npm install @nestjs/typeorm typeorm

        npm install sqlite3 --save
            
            --save salva dentro do package.json

CONFIGURAR O app.module.ts:

    IMPORTS

        dentro de @Module
        imports:[TypeOrmModule.forRoot({
            type:'sqlite',
            database:'db',
            entities:[],
            synchronize:true, -> sincroniza configs
            autoLoadEntities:true -> ajuda a evitar erros de configurações nos modules
        }),
        userModule]
    
    CRIANDO TABELAS E ENTIDADES

        nest generate resource user (cria entidade para usuário)

            tipo: REST API
            generate crud? YES -> poder usar os verbos do http

CONFIGURAR O user.module

    dentro de @Module
    imports: [TypeOrmModule.forFeature([User])],


CRIANDO user.entity.ts:

    import { Column, Entity, PrimaryGeneratedColumn } from "typeorm"

    @Entity({name:'user'})
    export class User {
        @PrimarGeneratedColumn()    
        id:number,

        @Column()
        username:string,
        
        @Column()
        password:string,
        
        @Column()
        createdAt:Date
    
    }

    O que é uma primary generated column?
        gera automaticamente um id sempre que um user for inicializado
    
    O banco é criado a partir do app.module.ts

DTO (Data Transfer Object): Padronização de json
    Para os dois métodos que usam json

    Criando um user (object, no geral):

        create-user-dto.ts

            export class CreateUserDto {

                username:string;

                password:string;

            }
    
    Atualizar um user (object, no geral)

CONFIGURANDO user.controller.ts:

    Cria as rotas


    injetar o 
    export class UserService {
        constructor(@InjectRepository(User) private userRepository:Repository<User>){}
    }

    código 201: criado e pedido bem sucedido

-----------------------------------------

CRIANDO POSTS (NO SENTIDO DE TWITTER KKKKK):

    post.entity.ts