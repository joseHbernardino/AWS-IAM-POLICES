# Policy Region Restriction

1. Abaixo está uma política atualizada com os comentários:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "DenyAllExceptAllowedRegions", # Identificador da regra
            "Effect": "Deny", # Ação que vai negar o acesso
            "Action": "*", # Todas as ações são negadas
            "Resource": "*", # Todos os recursos são negados
            "Condition": { # Condição para permitir ou negar o acesso
                "StringNotEquals": {
                    "aws:RequestedRegion": [ # Regiões permitidas
                        "us-west-2", # Oregon
                        "us-west-1", # N. California
                        "us-east-1" # N. Virginia
                    ]
                }
            }
        }
    ]
}
```


## Premissa

A premissa desse código é restringir o acesso às regiões de N. Virginia, N. California e Oregon na AWS. Ele pode ser utilizado como uma política de segurança para impedir que usuários, funções ou serviços criem recursos nessas regiões.

A política nega todas as ações e recursos, exceto aqueles que são permitidos nas regiões especificadas. Ela é baseada em condições, que permitem que as políticas de segurança sejam aplicadas somente quando determinadas condições são atendidas. Nesse caso, a condição é a região solicitada, que precisa ser uma das regiões permitidas para que a ação seja autorizada.

Essa política pode ser útil para empresas que desejam restringir o acesso a regiões específicas da AWS, para garantir que seus recursos e dados estejam armazenados apenas em regiões consideradas mais seguras ou que atendam a requisitos regulatórios. Ela pode ser aplicada a várias contas, usuários ou funções dentro de uma organização da AWS, para garantir que todos estejam seguindo as mesmas regras de segurança.
