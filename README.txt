GraphQl

Toda request feita é POST
Toda request bate no mesmo endpointer (/graphql)

Onde ela consegue fazer a distinção do que ela deve fazer
já que tem o mesmo endpointer

usamos:

Query -> Obter informações ( GET )

Mutations -> Manipular dados ( POST/PATCH/PUT/DELETE ) 

Scalar Types -> String, Int, Boolean, Float e ID

os TYPES são as entidades da nossa aplicação

também conseguimos fazer relacionamentos com os Types

EX:
    type User {
        _id: ID
        name: String
        email: String
        active: Boolean
    }

    type Post {
        _id: ID
        title: String
        content: String
        author: User -> aqui está a chave estrangeira
    }

exemplo de pegar um usuario por ID:

    type Query {
        users: [User]
        getUserByEmail(email: String): User
    }


    Obs: A Linha abaixo é referente ao Revolver

    getUserByEmail: (_, args) => ( users.find( user => user.email == args.email ) )
    -> 2 param que está contido o paramentro passado no type Query




Criando uma Mutations para inserção

1 -> criamos um type

type Mutation {
    createUser(name: String, email: String): User
}

2 -> Dentro do Resolvers criamos o objeto de Mutation

Mutation: {

    createUser: (_, args) => {

        const newUser = {
            _id: String(Math.random()),
            name: args.name,
            email: args.email,
            active: true,
        }

        // colocamos a logica para inserção do dado

    }

}


3 -> executamos essa Mutation no front
mutation {
    createUser(email: "NewTeste@email.com", name: "Novo Usuario 1")
}