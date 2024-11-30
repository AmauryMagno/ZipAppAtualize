
# Metodologia

## Relação de Ambientes de Trabalho

<table> <tbody> <tr align=center> <td width="250px"><b>Plataforma</b></td> <td width="350px"><b>Ambiente</b></td> <td width="250px"><b>Link</b></td> </tr> <tr> <td>Visual Studio</td> <td>Desktop</td> <td><a href="https://visualstudio.microsoft.com/pt-br/downloads/" target="_blank">Acessar Visual Studio</a></td> </tr> </tr> </tbody> </table>

## Controle de Versão

A ferramenta de controle de versão adotada no projeto foi o
[Git](https://git-scm.com/), sendo que o [Github](https://github.com)
foi utilizado para hospedagem do repositório.

O projeto segue a seguinte convenção para o nome de branches:

- `main`: versão estável já testada do software
- `develop`: versão já testada do software, porém instável
- `dev-task`: Cada Dev terá sua branch de acordo com sua tarefa atual,dificultando problemas com conflito na hora do merge

Quanto à gerência de issues, o projeto adota a seguinte convenção para
etiquetas:

- `Documentação`: melhorias ou acréscimos à documentação
- `bug`: uma funcionalidade encontra-se com problemas
- `Melhoria`: uma funcionalidade precisa ser melhorada
- `Desenvolvimento`: uma nova funcionalidade precisa ser introduzida

Essa configuração de divisão de branchs e de issues foi a melhor forma encontrada para minimizar a possibilidade de erros,tanto no momento do merge com as branch "develop" e "main",quanto no momento de gerenciar as tarefas,agilizando e facilitando o desenvolvimento do aplicativo.

Cada dev terá sua branch de sua respectiva tarefa,ele criará esse branch originada da main,para que sua branch local possa ser a mais atualizada de maneira estável,assim podendo dar inicio a sua tarefa. Ao final da sua tarefa o código será implementado na branch develop para que possa ser testado e após os testes será feito o merge com o main,esse ciclo será repetido até o final do projeto.
