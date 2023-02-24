# Policy DynamoDB


## PolicyDynamoDB

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

## Permission for 3 users

```:bash
{
    "Version": "2012-10-17",

    "Statement": [
        {
            "Sid": "AllowDynamoDBTableActions", // Identificador único da política.
            "Effect": "Allow", // A ação que a política realiza. Neste caso, permite.
            "Action": [
                "dynamodb:CreateTable", // Ação permitida pela política: criar tabelas.
                "dynamodb:ListTables" // Ação permitida pela política: listar tabelas.
            ],
            "Resource": "arn:aws:dynamodb:*:*:table/*", // O recurso ao qual a política se aplica. Neste caso, todas as tabelas do DynamoDB.
            "Condition": {
                "StringEquals": {
                    "aws:username": [ // Nome de usuário do AWS que a política permite realizar ações.
                        "username1",
                        "username2",
                        "username3"
                    ]
                }
            }
        }
    ]
}


```
## Premissa

A política permite apenas as ações de criação e listagem de tabelas no DynamoDB, definindo a ação como "permitir" (Allow), e especifica as contas de usuário que têm permissão para realizar essas ações por meio da cláusula "Condition".

Isso garante que apenas os usuários especificados possam realizar essas ações em todas as tabelas do DynamoDB na conta AWS, adicionando uma camada de segurança e controle para o gerenciamento de recursos.

## 
## Permission For 3 users - 2 
##

```:bash
{
    "Version": "2012-10-17",

    "Statement": [
        {
            "Sid": "AllowDynamoDBTableActions", // Identificador único da primeira declaração.
            "Effect": "Allow", // A ação que a política realiza. Neste caso, permite.
            "Action": [
                "dynamodb:CreateTable", // Ação permitida pela política: criar tabelas.
                "dynamodb:ListTables" // Ação permitida pela política: listar tabelas.
            ],
            "Resource": "arn:aws:dynamodb:*:*:table/*", // O recurso ao qual a política se aplica. Neste caso, todas as tabelas do DynamoDB.
            "Condition": {
                "StringEquals": {
                    "aws:username": [ // Nome de usuário do AWS que a política permite realizar ações.
                        "username1",
                        "username2",
                        "username3"
                    ]
                }
            }
        },
        {
            "Sid": "AllowDynamoDBTableDeletion", // Identificador único da segunda declaração.
            "Effect": "Allow", // A ação que a política realiza. Neste caso, permite.
            "Action": [
                "dynamodb:DeleteTable" // Ação permitida pela política: excluir tabelas.
            ],
            "Resource": "arn:aws:dynamodb:*:*:table/*", // O recurso ao qual a política se aplica. Neste caso, todas as tabelas do DynamoDB.
            "Condition": {
                "StringEquals": {
                    "aws:username": "username2" // Nome de usuário do AWS que a política permite realizar ações.
                }
            }
        }
    ]
}

```

## Premissa

A política permite apenas as ações de criação e listagem de tabelas no DynamoDB para todos os usuários especificados na cláusula "Condition" da primeira declaração (statement). Foi adicionada uma segunda declaração (statement) para permitir apenas o usuário 2 realizar a ação de exclusão de tabelas no DynamoDB.

Com essa atualização, a política garante que apenas o usuário 2 possa realizar a ação de exclusão de tabelas no DynamoDB na conta AWS, adicionando uma camada de segurança e controle para o gerenciamento de recursos.
