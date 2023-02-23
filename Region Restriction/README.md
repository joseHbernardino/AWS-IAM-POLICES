# Policy Region Restriction

1. Código comentado:

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