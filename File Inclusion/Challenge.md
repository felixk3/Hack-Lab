Excelente trabalho! Agora aplique as técnicas que você aprendeu para capturar as flags! Familiarizar-se com os conceitos básicos de HTTP na Web pode ajudá-lo a concluir esses desafios.

Certifique-se de que a VM conectada esteja em execução e acesse: http : //IP_DA_MÁQUINA/challenges/index.php

Etapas para testar a LFI
Encontre um ponto de entrada que possa ser via GET , POST , COOKIE ou valores de cabeçalho HTTP !
Insira um valor válido para ver como o servidor web se comporta.
Insira dados inválidos, incluindo caracteres especiais e nomes de arquivos comuns.
Nem sempre confie que o que você digita em formulários seja o que você pretendia! Use a barra de endereços do navegador ou uma ferramenta como o Burp Suite.
Procure por erros ao inserir dados inválidos para descobrir o caminho atual da aplicação web; se não houver erros, então a tentativa e erro pode ser a melhor opção.
Entenda a validação de entrada e se existem filtros!
Tente inserir uma entrada válida para ler arquivos confidenciais.
