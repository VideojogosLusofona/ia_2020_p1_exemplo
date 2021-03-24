## Exemplo de repositório para o Projeto 1 de IA 2020/21

_Nota: os comandos seguintes foram testados no Git Bash. No Windows PowerShell
poderão existir pequenas diferenças._

* Criar pasta para o repositório, fazer `cd` para dentro da mesma e inicializar
  repositório Git.
* Adicionar ficheiro [`.gitignore`](.gitignore) apropriado para projetos C#.
  Este ficheiro deve também ignorar a pasta `color-shape-links-ai-competition/`.
* Clonar o projeto ColorShapeLinks para dentro da pasta (será ignorado pelo Git
  caso o ficheiro [`.gitignore`](.gitignore) esteja bem configurado)
  ```
  git clone --recurse-submodules https://github.com/VideojogosLusofona/color-shape-links-ai-competition.git
  ```
* Criar projeto C# ([.NET Standard 2.0]) para a vossa IA (substituam `Ultron`
  pelo nome da vossa IA):
  ```
  dotnet new classlib -n Ultron -f netstandard2.0
  ```
* Adicionem uma referência à biblioteca [Common] que contém o contém todas as
  classes necessárias para desenvolverem o vosso projeto:
  ```
  dotnet add Ultron reference color-shape-links-ai-competition/ConsoleApp/ColorShapeLinks/Common
  ```
* Criar ou copiar uma IA básica para a pasta [`Ultron`](Ultron) (como por
  exemplo [esta](Ultron/UltronThinker.cs)), e verificar se funciona:
  ```
  dotnet build Ultron -c Release
  dotnet run -c Release -p color-shape-links-ai-competition/ConsoleApp/ColorShapeLinks/TextBased/App -- match -a $(pwd)/Ultron/bin/Release/netstandard2.0/Ultron.dll -W ColorShapeLinks.Common.AI.Examples.RandomAIThinker -R Ultron.UltronThinker
  ```
* Também é possível testar no Unity, bastando para isso copiar a pasta
  [`Ultron`](Ultron) para dentro da pasta
  `color-shape-links-ai-competition/UnityApp/Assets/Scripts`.

### Sugestões

* Tentar perceber exatamente o que os comandos apresentados fazem.
* Criar um ou mais _scripts_ para o Git Bash para não terem de escrever
  comandos tão compridos.
* Criar um projeto adicional de consola para testar a IA isoladamente (e já
  agora criar uma solução para poder abrir os projetos ao mesmo tempo no VS
  Code):
  ```
  dotnet new console -n TestUltron
  dotnet add TestUltron reference Ultron
  dotnet new sln
  dotnet sln add Ultron
  dotnet sln add Ultron
  ```

[.NET Standard 2.0]:https://docs.microsoft.com/pt-pt/dotnet/standard/net-standard
[Common]:https://videojogoslusofona.github.io/color-shape-links-ai-competition/docs/html/namespace_color_shape_links_1_1_common.html