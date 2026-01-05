# Azure Open AI na VNet - DEV Community

**Forem Feed**  
Siga novos Subforems para melhorar seu feed.

**DEV Community**  
Um espaço para discutir e acompanhar o desenvolvimento de software e gerenciar sua carreira em tecnologia.

**Futuro**  
Notícias e discussões sobre ciência e tecnologia, como IA, VR, criptomoedas, computação quântica e muito mais.

**Open Forem**  
Um espaço de discussão geral para a comunidade Forem. Se não tem um lar em outro lugar, pertence aqui.

**Gamers Forem**  
Uma comunidade inclusiva para entusiastas de jogos.

**Music Forem**  
De composição e apresentações a equipamentos, novidades musicais e tudo no meio.

**Vibe Coding Forem**  
Discutindo desenvolvimento de software em IA e mostrando o que estamos construindo.

**Filmes e TV Popcorn**  
Entusiasmo por filmes e TV, críticas e tudo o que está entre eles.

**DUMB DEV Community**  
Memes e crapposting sobre desenvolvimento de software.

**Design Community**  
Design web, design gráfico e tudo relacionado.

**Security Forem**  
Seu centro para tudo relacionado à segurança. De hacking ético e CTFs a GRC e desenvolvimento de carreira, para iniciantes e profissionais.

**Golf Forem**  
Uma comunidade de golfistas e entusiastas do golfe.

**Crypto Forem**  
Uma comunidade colaborativa para tudo sobre criptomoedas—de Bitcoin ao desenvolvimento de protocolos, DeFi, NFTs e análise de mercado.

**Parenting**  
Um lugar para os pais compartilharem as alegrias, desafios e sabedoria que vêm da criação de filhos. Estamos aqui por eles e uns pelos outros.

**Forem Core**  
Discutindo o projeto de código aberto Forem — recursos, bugs, desempenho, e auto-hospedagem.

**Maker Forem**  
Uma comunidade para makers, hobbistas e profissionais discutirem Arduino, Raspberry Pi, impressão 3D e muito mais.

**HMPL.js Forem**  
Para desenvolvedores que usam HMPL.js para construir aplicações web rápidas e leves. Um espaço para compartilhar projetos, fazer perguntas e discutir templating server-driven.

---  

## Azure Open AI na VNet
**Kenichiro Nakamura**  
Postado em 12 de outubro de 2023  

Os modelos GPT estão hospedados em vários provedores de serviços no momento, e o Microsoft Azure é um deles. Apesar de os modelos em si serem os mesmos, existem muitas diferenças, incluindo: 
- custo
- funcionalidades 
- tipo de modelos e versões 
- geolocalização 
- segurança 
- suporte 
- etc.

Um dos aspectos mais importantes ao usá-lo em um ambiente corporativo é, claro, a segurança. Ao usar os recursos de segurança de rede do Azure com o Azure Open AI, os clientes podem consumir o serviço Open AI de dentro da VNet, portanto, nenhuma informação flui para o público.

### Implantação de Exemplo
O repositório de amostras do Azure fornece arquivos bicep de exemplo para implantar o Azure Open AI em um ambiente VNet.  
GitHub: [openai-enterprise-iac](https://github.com/Azure-Samples/openai-enterprise-iac)

As principais características usadas pelo bicep são: 
- VNet 
- Integração VNet para Aplicativo Web 
- Endpoint Privado para Azure Open AI 
- Endpoint Privado para Pesquisa Cognitiva 
- Zona DNS Privada 

Usando esses recursos, todo o tráfego de saída do Aplicativo Web é roteado apenas dentro da VNet e todos os nomes são resolvidos em endereços IP privados. O Open AI e a Pesquisa Cognitiva desativam o endereço IP público, portanto, já não há mais um endpoint de interface pública disponível.

### Implantar
O arquivo bicep implanta os seguintes recursos do Azure.  
Vamos implantar e confirmar como funciona. Eu crio um grupo de recursos na região East US para meu próprio teste.

```bash
git clone https://github.com/Azure-Samples/openai-enterprise-iac
cd openai-enterprise-iac
az group create -n openaitest -l eastus
az deployment group create -g openaitest -f .\infra\main.bicep
```

Assim que executar o comando acima, vejo que a implantação foi iniciada.  
Espere até que a implantação seja concluída.

### Teste
Vamos ver se a implantação foi bem-sucedida. **Azure Open AI**
Vamos tentar o acesso público primeiro.  
Eu poderia criar uma implantação sem nenhum problema. Mas quando tento pelo playground do Chat em meu portal do Azure, vejo o seguinte erro.

E quanto ao acesso via API Web?  
A partir da ferramenta avançada do App Service, eu faço login em uma sessão Bash, e primeiro pingo a URL do serviço.  
Vejo o endereço IP privado atribuído ao Endpoint Privado sendo retornado.  
Em seguida, uso o comando curl para enviar uma solicitação ao endpoint.

---  
**Top comments**  
(0)  
Assine  
**Personal**  
Usuário Confiável  
Criar template  
Templates permitem que você responda rapidamente perguntas frequentes ou armazene trechos para reutilização.  
Enviar  
Visualizar  
Descartar  
**Código de Conduta**  
•  
Reportar abuso  
Você tem certeza de que deseja ocultar este comentário? Ele ficará oculto em sua postagem, mas ainda será visível por meio do permalink do comentário.  
Ocultar comentários filhos também  
Confirmar  
Para mais ações, você pode considerar bloquear essa pessoa e/ou reportar abuso.

---  
**Kenichiro Nakamura**  
Siga  
Entrou em 3 de fevereiro de 2018  
Mais de **Kenichiro Nakamura**  
- Azure ML Prompt flow: Use content safety before sending a request to LLM  
- Não perca tempo escrevendo README, use readme-ai em vez disso  
- C#: Azure Open AI e Chamada de Função  

---  
💎 **Patrocinadores Diamante do DEV**  
Obrigado aos nossos patrocinadores Diamante por apoiar a comunidade DEV.  
Google AI é o parceiro oficial de Modelos e Plataformas de IA do DEV.  
Neon é o parceiro oficial de banco de dados do DEV.  
Algolia é o parceiro oficial de busca do DEV.  

---  
**DEV Community**  
— Um espaço para discutir e acompanhar o desenvolvimento de software e gerenciar sua carreira em tecnologia.  
Início  
DEV++  
Lista de leitura  
Podcasts  
Vídeos  
Trilhas de Educação DEV  
Desafios DEV  
Ajuda DEV  
Anuncie no DEV  
Exibição DEV  
Sobre  
Contato  
Banco de Dados Postgres Gratuito  
Comparações de software  
Loja Forem  
**Código de Conduta**  
**Política de Privacidade**  
**Termos de Uso**  
Construído em  
Forem  
— o software de código aberto que alimenta o DEV e outras comunidades inclusivas.  
Feito com amor e Ruby on Rails.  
DEV Community © 2016 - 2026.  
Somos um lugar onde programadores compartilham, mantêm-se atualizados e crescem em suas carreiras.  
Conecte-se  
Crie uma conta.
# Azure Open AI na VNet - DEV Community

**Forem Feed**  
Siga novos Subforems para melhorar seu feed.

**DEV Community**  
Um espaço para discutir e acompanhar o desenvolvimento de software e gerenciar sua carreira em tecnologia.

**Futuro**  
Notícias e discussões sobre ciência e tecnologia, como IA, VR, criptomoedas, computação quântica e muito mais.

**Open Forem**  
Um espaço de discussão geral para a comunidade Forem. Se não tem um lar em outro lugar, pertence aqui.

**Gamers Forem**  
Uma comunidade inclusiva para entusiastas de jogos.

**Music Forem**  
De composição e apresentações a equipamentos, novidades musicais e tudo no meio.

**Vibe Coding Forem**  
Discutindo desenvolvimento de software em IA e mostrando o que estamos construindo.

**Filmes e TV Popcorn**  
Entusiasmo por filmes e TV, críticas e tudo o que está entre eles.

**DUMB DEV Community**  
Memes e crapposting sobre desenvolvimento de software.

**Design Community**  
Design web, design gráfico e tudo relacionado.

**Security Forem**  
Seu centro para tudo relacionado à segurança. De hacking ético e CTFs a GRC e desenvolvimento de carreira, para iniciantes e profissionais.

**Golf Forem**  
Uma comunidade de golfistas e entusiastas do golfe.

**Crypto Forem**  
Uma comunidade colaborativa para tudo sobre criptomoedas—de Bitcoin ao desenvolvimento de protocolos, DeFi, NFTs e análise de mercado.

**Parenting**  
Um lugar para os pais compartilharem as alegrias, desafios e sabedoria que vêm da criação de filhos. Estamos aqui por eles e uns pelos outros.

**Forem Core**  
Discutindo o projeto de código aberto Forem — recursos, bugs, desempenho, e auto-hospedagem.

**Maker Forem**  
Uma comunidade para makers, hobbistas e profissionais discutirem Arduino, Raspberry Pi, impressão 3D e muito mais.

**HMPL.js Forem**  
Para desenvolvedores que usam HMPL.js para construir aplicações web rápidas e leves. Um espaço para compartilhar projetos, fazer perguntas e discutir templating server-driven.

---  

## Azure Open AI na VNet
**Kenichiro Nakamura**  
Postado em 12 de outubro de 2023  

Os modelos GPT estão hospedados em vários provedores de serviços no momento, e o Microsoft Azure é um deles. Apesar de os modelos em si serem os mesmos, existem muitas diferenças, incluindo: 
- custo
- funcionalidades 
- tipo de modelos e versões 
- geolocalização 
- segurança 
- suporte 
- etc.

Um dos aspectos mais importantes ao usá-lo em um ambiente corporativo é, claro, a segurança. Ao usar os recursos de segurança de rede do Azure com o Azure Open AI, os clientes podem consumir o serviço Open AI de dentro da VNet, portanto, nenhuma informação flui para o público.

### Implantação de Exemplo
O repositório de amostras do Azure fornece arquivos bicep de exemplo para implantar o Azure Open AI em um ambiente VNet.  
GitHub: [openai-enterprise-iac](https://github.com/Azure-Samples/openai-enterprise-iac)

As principais características usadas pelo bicep são: 
- VNet 
- Integração VNet para Aplicativo Web 
- Endpoint Privado para Azure Open AI 
- Endpoint Privado para Pesquisa Cognitiva 
- Zona DNS Privada 

Usando esses recursos, todo o tráfego de saída do Aplicativo Web é roteado apenas dentro da VNet e todos os nomes são resolvidos em endereços IP privados. O Open AI e a Pesquisa Cognitiva desativam o endereço IP público, portanto, já não há mais um endpoint de interface pública disponível.

### Implantar
O arquivo bicep implanta os seguintes recursos do Azure.  
Vamos implantar e confirmar como funciona. Eu crio um grupo de recursos na região East US para meu próprio teste.

```bash
git clone https://github.com/Azure-Samples/openai-enterprise-iac
cd openai-enterprise-iac
az group create -n openaitest -l eastus
az deployment group create -g openaitest -f .\infra\main.bicep
```

Assim que executar o comando acima, vejo que a implantação foi iniciada.  
Espere até que a implantação seja concluída.

### Teste
Vamos ver se a implantação foi bem-sucedida. **Azure Open AI**
Vamos tentar o acesso público primeiro.  
Eu poderia criar uma implantação sem nenhum problema. Mas quando tento pelo playground do Chat em meu portal do Azure, vejo o seguinte erro.

E quanto ao acesso via API Web?  
A partir da ferramenta avançada do App Service, eu faço login em uma sessão Bash, e primeiro pingo a URL do serviço.  
Vejo o endereço IP privado atribuído ao Endpoint Privado sendo retornado.  
Em seguida, uso o comando curl para enviar uma solicitação ao endpoint.

---  
**Top comments**  
(0)  
Assine  
**Personal**  
Usuário Confiável  
Criar template  
Templates permitem que você responda rapidamente perguntas frequentes ou armazene trechos para reutilização.  
Enviar  
Visualizar  
Descartar  
**Código de Conduta**  
•  
Reportar abuso  
Você tem certeza de que deseja ocultar este comentário? Ele ficará oculto em sua postagem, mas ainda será visível por meio do permalink do comentário.  
Ocultar comentários filhos também  
Confirmar  
Para mais ações, você pode considerar bloquear essa pessoa e/ou reportar abuso.

---  
**Kenichiro Nakamura**  
Siga  
Entrou em 3 de fevereiro de 2018  
Mais de **Kenichiro Nakamura**  
- Azure ML Prompt flow: Use content safety before sending a request to LLM  
- Não perca tempo escrevendo README, use readme-ai em vez disso  
- C#: Azure Open AI e Chamada de Função  

---  
💎 **Patrocinadores Diamante do DEV**  
Obrigado aos nossos patrocinadores Diamante por apoiar a comunidade DEV.  
Google AI é o parceiro oficial de Modelos e Plataformas de IA do DEV.  
Neon é o parceiro oficial de banco de dados do DEV.  
Algolia é o parceiro oficial de busca do DEV.  

---  
**DEV Community**  
— Um espaço para discutir e acompanhar o desenvolvimento de software e gerenciar sua carreira em tecnologia.  
Início  
DEV++  
Lista de leitura  
Podcasts  
Vídeos  
Trilhas de Educação DEV  
Desafios DEV  
Ajuda DEV  
Anuncie no DEV  
Exibição DEV  
Sobre  
Contato  
Banco de Dados Postgres Gratuito  
Comparações de software  
Loja Forem  
**Código de Conduta**  
**Política de Privacidade**  
**Termos de Uso**  
Construído em  
Forem  
— o software de código aberto que alimenta o DEV e outras comunidades inclusivas.  
Feito com amor e Ruby on Rails.  
DEV Community © 2016 - 2026.  
Somos um lugar onde programadores compartilham, mantêm-se atualizados e crescem em suas carreiras.  
Conecte-se  
Crie uma conta.
