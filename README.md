# GuiaXBPS-SRC
Como criar novos pacotes fonte para o XBPS,o sistema de empacotamento nativo do Void Linux.


Este pequeno guia tem objetivo de ajudar as pessoas a criar pacotes a partir de código fonte de programas não disponíveis nos repositórios da distribuição Void Linux.

A maioria do texto foi traduzido pelo Google tradutor , tendo como origem a documentação oficial disponível em inglês em:
https://github.com/void-linux/void-packages/blob/master/Manual.md

A contribuição dos mais experientes no assunto será fundamental para o assessoramento dos mais novos no mundo do Void linux e para o crescimento da distribuição no Brasil.

Este artigo contém um manual completo de como criar novos pacotes fonte para o XBPS, o sistema de empacotamento nativo do Void Linux.

Introdução

O repositório void-packages contém todos os pacotes fonte que são as receitas para baixar, compilar e construir pacotes binários para o Void. 

Esses arquivos de pacotes de origem são chamados de modelos.

Os arquivos de modelo são scripts de shell bash do GNU que devem definir algumas variáveis e funções necessárias/opcionais que são processadas pelo xbps-src (o construtor de pacotes) para gerar os pacotes binários resultantes.

Por convenção, todos os modelos começam com um comentário explicando brevemente o que são. Além disso, pkgname e version não podem conter caracteres que exijam que sejam citados, portanto, não são citados.

Um exemplo simples de modelo é o seguinte: pacote de nome "foo"

# Template file for 'foo'

pkgname=foo

version=1.0

revision=1

build_style=gnu-configure

short_desc="A short description max 72 chars"

maintainer="name <email>"
 
license="GPL-3.0-or-later"

homepage="http://www.foo.org"

distfiles="http://www.foo.org/foo-${version}.tar.gz"

checksum="fea0a94d4b605894f3e2d5572e3f96e4413bcad3a085aae7367c2cf07908b2ff"



O arquivo de modelo contém definições para baixar, criar e instalar os arquivos do pacote em um destino falso e, depois disso, um pacote binário pode ser gerado com as definições especificadas nele.


Não se preocupe se algo não estiver claro como deveria ser. As variáveis e funções reservadas serão explicadas mais adiante. Este arquivo de modelo deve ser criado em um diretório correspondente a $ pkgname, Exemplo:
$ void-packages/srcpkgs/foo/template.

Se tudo correr bem, depois é só rodar  o comando para compilar o pacote binário para futura instalação:

$ ./xbps-src pkg foo

continue.....

Requerimentos de Qualidade:

Siga esta lista para determinar se um software ou outra tecnologia pode ser permitida no repositório do Void Linux. Exceções à lista são possíveis e podem ser aceitas, mas são extremamente improváveis. Se você acredita ter uma exceção, inicie um PR e defenda por que esse software específico, embora não atenda aos requisitos abaixo, é um bom candidato para o sistema de pacotes Void.

Sistema: o software deve ser instalado em todo o sistema, não por usuário.

Compilado: o software precisa ser compilado antes de ser usado, mesmo que não seja necessário para todo o sistema.

Necessário: Outro pacote no repositório ou na inclusão pendente requer o pacote.

FASES DE COMPILAÇÃO DO PACOTE:




##########################################################################################################

Vídeos que ajudaram na construção do guia:
Void Linux - Atualizando pacotes gerados com o xbps-src = https://www.youtube.com/watch?v=98rtE1YE8Gc
Canal do Leandro Ramos

Atualizando o Google-Chrome através do xbps-src e o repositório void-packages.

Entrar na pasta do void-packages
Rodar:
 $ git pull oringin master 
  -> pra verificar atualizações disponíveis

Compare as versões do que está instalado e do que foi disponibilizado no git pull
$ cat srcpkgs/google-chorme/template

 -> verifique na segunda linha do template a versão nova
 -> se forem diferentes e queira atualizar :
 
Gerar novo binário para o pacote:
 $ ./xbps-src pkg google-chorme

Depois de gerado o pacote binário para o Void é só prosseguir com o update da instalação:

$sudo xbps-install -u --repository=home/$USER/void-packages/hostdir/binpkgs/nonfree google-chrome

