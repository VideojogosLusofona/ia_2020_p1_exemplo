# Exemplo de repositório para o Projeto 1 de IA 2020/21

## Introdução

Este documento, bem como o código incluído no repositório, servem como exemplo
de como criar um agente de IA (_thinker_) para a competição [ColorShapeLinks]
que seja **testável isoladamente**, ou seja, que não precise de ser testado
dentro da _framework_ de competição. É perfeitamente possível desenvolver um
_thinker_ dentro da _framework_ de competição, tanto em consola como em Unity,
ignorando os passos sugeridos aqui. No entanto torna-se muito mais difícil de
testar o _thinker_ dessa forma.

## Passos

### Criar um projeto para o vosso _thinker_

* Criem uma pasta onde colocar (1) a _framework_ [ColorShapeLinks], e, (2) o
  repositório do vosso _thinker_:
  ```
  mkdir projeto_ia
  cd projeto_ia
  git clone --recurse-submodules https://github.com/VideojogosLusofona/color-shape-links-ai-competition.git
  mkdir my_thinker
  cd my_thinker
  git init
  ```
* Neste momento a estrutura de pastas é a seguinte, estando nós dentro da pasta
  `my_thinker`:
  ```
  └──projeto_ia/
    ├──color-shape-links-ai-competition/
    └──my_thinker/
  ```
* Criem ou adicionem um ficheiro [`.gitignore`](.gitignore) apropriado
  para projetos C# à pasta `my_thinker`.
* Criem um projeto C# ([.NET Standard 2.0]) para a vossa IA -- substituam
  `Ultron` pelo nome da vossa IA nos restantes comandos até ao fim deste
  documento:
  ```
  dotnet new classlib -n Ultron -f netstandard2.0
  ```
* Adicionem uma referência à biblioteca [Common] que contém o contém todas as
  classes necessárias para desenvolverem o vosso projeto:
  ```
  dotnet add Ultron reference ../color-shape-links-ai-competition/ConsoleApp/ColorShapeLinks/Common
  ```
* Criem ou copiem uma IA básica para a pasta [`Ultron`](Ultron) (como por
  exemplo [esta](Ultron/UltronThinker.cs)), e verificar se funciona na aplicação
  de consola do [ColorShapeLinks]:
  ```
  dotnet build Ultron
  dotnet run -p ../color-shape-links-ai-competition/ConsoleApp/ColorShapeLinks/TextBased/App -- match -a $(pwd)/Ultron/bin/Debug/netstandard2.0/Ultron.dll -W ColorShapeLinks.Common.AI.Examples.RandomAIThinker -R Ultron.UltronThinker
  ```
  * <span style="font-size:80%">_Nota:_ Se estiverem a usar PowerShell e não Git Bash, devem substituir
  `$(pwd)` por `$pwd` no comando anterior.</span>
* Também é possível testar o vosso _thinker_ na aplicação Unity do
  [ColorShapeLinks], bastando para isso copiar os ficheiros C# na pasta
  [`Ultron`](Ultron) para a pasta
  `color-shape-links-ai-competition/UnityApp/Assets/Scripts`. Isso pode ser
  feito no Explorador de Ficheiros do Windows ou com o seguinte comando:
  ```
  cp Ultron/*.cs ../color-shape-links-ai-competition/UnityApp/Assets/Scripts/
  ```
  * <span style="font-size:80%">_Nota:_ É necessário fazer a cópia de novo cada
    vez que atualizarem o vosso _Thinker_ e o quiserem testar no Unity.</span>

### Criar um projeto para testar o vosso _thinker_ isoladamente

* Assumindo que estamos na pasta `my_thinker`, criar um novo projeto
  de consola para testar o nosso _thinker_:
  ```
  dotnet new console -n TestUltron
  ```
* Adicionar ao novo projeto [`TestUltron`](TestUltron) uma referência ao nosso
  _thinker_, que está no projeto [`Ultron`](Ultron):
  ```
  dotnet add TestUltron reference Ultron
  ```
* Criar uma solução para que ambos os projetos possam ser abertos ao mesmo tempo
  no Visual Studio:
  ```
  dotnet new sln
  dotnet sln add TestUltron
  dotnet sln add Ultron
  ```
* Agora podemos importar os _namespaces_ do [ColorShapeLinks] e do
  [`Ultron`](Ultron) dentro do projeto [`TestUltron`](TestUltron) e podemos
  testar o nosso _thinker_ isoladamente, ou seja, fora da _framework_ de
  competição ([exemplo](TestUltron/Program.cs)). A estrutura de pastas é agora
  a seguinte:
  ```
  └──projeto_ia/
     ├──color-shape-links-ai-competition/
     └──my_thinker/
        ├──.gitignore
        ├──my_thinker.sln
        ├──TestUltron/
        └──Ultron/
  ```

### Outras sugestões

* Usem o método [`OnThinkingInfo()`] dentro do vosso _thinker_ para imprimir na
  consola e não `Console.WriteLine()` ou `Debug.Log()`. O método
  [`OnThinkingInfo()`] imprime corretamente nas consolas PowerShell ou GiBash e
  na consola do Unity.
* Usem o GitHub para terem um repositório remoto do vosso repositório local
  `my_thinker` e forneçam-me acesso ao mesmo.

## Licenças

Todo o código neste repositório é disponibilizado através da licença [MPLv2].
Os textos e restantes ficheiros são disponibilizados através da licença
[CC BY-NC-SA 4.0].

## Metadados

* Autor: [Nuno Fachada]
* Curso:  [Licenciatura em Videojogos][lamv]
* Instituição: [Universidade Lusófona de Humanidades e Tecnologias][ULHT]

[MPLv2]:https://opensource.org/licenses/MPL-2.0
[CC BY-NC-SA 4.0]:https://creativecommons.org/licenses/by-nc-sa/4.0/
[lamv]:https://www.ulusofona.pt/licenciatura/videojogos
[Nuno Fachada]:https://github.com/fakenmc
[ULHT ]:https://www.ulusofona.pt/
[ColorShapeLinks]:https://github.com/VideojogosLusofona/color-shape-links-ai-competition
[.NET Standard 2.0]:https://docs.microsoft.com/pt-pt/dotnet/standard/net-standard
[Common]:https://videojogoslusofona.github.io/color-shape-links-ai-competition/docs/html/namespace_color_shape_links_1_1_common.html
[`OnThinkingInfo()`]:https://videojogoslusofona.github.io/color-shape-links-ai-competition/docs/html/class_color_shape_links_1_1_common_1_1_a_i_1_1_abstract_thinker.html#a3610cd145e44a055a68076043d7b6cdc