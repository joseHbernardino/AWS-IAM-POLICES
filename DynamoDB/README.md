# Policy DynamoDB

1. Abaixo está uma política atualizada com os comentários:

```:bash
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Deny", // Ação que vai negar o acesso
            "Action": [
                "dynamodb:CreateTable", // Não permite a criação de tabelas
                "dynamodb:DeleteTable", // Não permite a exclusão de tabelas
                "dynamodb:DescribeTable", // Não permite a descrição de tabelas
                "dynamodb:ListTables", // Não permite a listagem de tabelas
                "dynamodb:UpdateTable", // Não permite a atualização de tabelas
                "dynamodb:TagResource", // Não permite a aplicação de tags
                "dynamodb:UntagResource", // Não permite a remoção de tags
                "dynamodb:ListTagsOfResource" // Não permite a listagem de tags
            ],
            "Resource": "*" // Não permite o acesso a nenhum recurso
        }
    ]
}

```


## Premissa

A premissa desse código é negar o acesso a ações relacionadas ao Amazon DynamoDB, como criar tabelas, excluir tabelas, atualizar tabelas, listar tabelas, aplicar ou remover tags, e obter informações sobre as tags aplicadas.

A política nega todas as ações relacionadas ao DynamoDB, impedindo que os usuários, funções ou serviços realizem qualquer operação nesse serviço. Além disso, a política também nega o acesso a todos os recursos do DynamoDB.

Essa política pode ser utilizada para garantir que apenas usuários ou funções autorizados possam acessar o DynamoDB e realizar as operações permitidas. Por exemplo, uma empresa pode aplicar essa política a uma função específica, permitindo que ela acesse somente algumas tabelas do DynamoDB e realizando apenas as operações permitidas.

É importante ressaltar que essa política deve ser testada com cuidado antes de ser aplicada em ambientes de produção, para evitar que ela bloqueie o acesso necessário aos usuários e serviços.