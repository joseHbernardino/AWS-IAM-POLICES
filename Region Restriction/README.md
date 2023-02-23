# Policy Region Restriction

1. Abaixo está uma política atualizada com os comentários:

```:bash
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "DenyAllExceptAllowedRegions", // Identificador da regra
            "Effect": "Deny", // Ação que vai negar o acesso
            "Action": "*", // Todas as ações são negadas
            "Resource": "*", // Todos os recursos são negados
            "Condition": { // Condição para permitir ou negar o acesso
                "StringNotEquals": {
                    "aws:RequestedRegion": [ // Regiões permitidas
                        "us-west-2", // Oregon
                        "us-west-1", // N. California
                        "us-east-1" // N. Virginia
                    ]
                }
            }
        }
    ]
}
```

A política tem uma versão específica, definida no campo **"Version"**. O campo **"Statement"** define a regra em si, contendo um identificador para a regra **("Sid")**, o efeito que a regra terá **("Deny")**, a lista de ações que serão negadas **("Action")** e a lista de recursos que serão negados **("Resource")**. Além disso, há uma condição definida na seção **"Condition"** que permite que a política seja aplicada apenas para as regiões especificadas.