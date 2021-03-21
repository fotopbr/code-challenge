Olá! Obrigado por participar de nosso processo seletivo. Abaixo iremos descrever um teste para o desenvolvimento fullstack.

## Descrição

Criar um sistema de agendametno de trabalhos onde é possível selecionar o tipo de trabalho e o horário do dia que será agendado. Deve ser exibido para o usuário os horário disponíveis e indisponíveis. Os horários não disponíveis não devem permitir seleção. Deve ser possível fazer um agendamento nos horários disponíveis.

Os horários são definidos por configuração de tipo de trabalho. Cada tipo de trabalho possui um conjunto de configurações diferente e a configuração segue o tipo abaixo:

```typescript
type JobType = {
    title: string;
    initialScheduleHour: string;
    finalScheduleHour: string;
    intervalBetweenJobs: "00:15" | "00:30" | "01:00" | "01:30";
};
```

O tipo de job possui as seguintes configurações:

- título: nome do tipo de trabalho. Deverá ser exibido na caixa de seleção de tipos de trabalho.

- horário inicial de agendamento: o horário do dia que é possível iniciar agendamentos. O valor desse campo deve ser uma string representando um horário do dia. Ex: 08:00, 08:30, 10:00.

- horário final de agendamento: o horário do dia que é possível marcar o último agendamento: O valor desse campo deve ser uma string representando um horário do dia: Ex: 17:00, 18:00.

- intervalo entre agendamentos: qual o espaço de tempo deve existir entre um horário de agendamento e outro. Ex: caso o intervalo seja `00:15` o usuário poderá escolher agendamentos no intervalo de 15 minutos como 10:00, 10:15, 10:30, 10:45...

**Todos os trabalhos são geridos por uma configuração de quantidade de agendamentos simultâneos. Essa configuração é apenas um `integer` que informa quantos trabalhos são permitidos para um determinado horário.**

Esta configuração permite desativar alguns horários de agendamento quando muitos trabalhos são marcados. Como é possível configurar tipos de trabalho com intervalo entre agendamentos diferentes, quando houver mais de um tipo de trabalho os horários de agendamentos não disponível devem considerar o maior intervalo entre agendamentos cadastrado. Dessa forma:

- Tipo de trabalho 1: horário de início às `08:00` e intervalo entre agendamentos de `00:15`.
- Tipo de trabalho 2: horário de início às `08:00` e intervalo entre agendamentos de `01:30`.
- Trabalhos simultâneos: 1.

Quando um job for cadastrado usando o `tipo de trabalho 2` no horário das `08:00` e um segundo trabalho for agendado usando o `tipo de trabalho 1`, os horários de agendamento devem ser exibidos da seguinte forma:

- 08:00 -> indisponível
- 08:15 -> indisponível
- 08:30 -> indisponível
- 08:45 -> indisponível
- 09:00 -> indisponível
- 09:15 -> indisponível
- 09:30 -> disponível
- ...

## Execução e tecnologia
Deverá ser entregue uma interface contendo as informações necessárias para fazer um agendamento: a seleção do tipo de trabalho e do horário para marcar o agendamento. Os agendamentos não disponíveis não devem permitir seleção.

As configurações devem ser buscadas de uma API e o agendamento deve ser submetido para a API.

Não é necessário nenhuma forma de banco de dados, os agendamentos podem ser armazenados em memória, assim como a configuração de tipo de trabalho e de trabalhos simultâneos. As configurações pode ser definidas de forma fixa no código, mas deve estar obrigatóriamente na API e devem ser acessados pelo cliente via requisições HTTP.

### Aplicação cliente
A aplicação cliente deve ser desenvolvida com as seguintes tecnologias:

- React com Typescript através do framework NextJS;
- Pode usar qualquer biblioteca de renderização que achar melhor: bootstrap, styled-components ou outra;
- Pode usar qualquer biblioteca para conexão com a API;
- Nenhuma biblioteca que influa diretamente na regra de negócio deve ser utilizada;
- Nenhuma biblioteca obsoleta deve ser usada (request, moment, ...).

### API
A API deve ser desenvolvida com as seguintes tecnologias:

- NodeJS (não utilize Typescript na API);
- ExpressJS.

## Avaliação
Os seguintes pontos da aplicação serão avaliados:

- Totalidade da entrega e funcionamento da aplicação;
- Código limpo e claro (caso queira destacar algum ponto ou informar alguma dificuldade pode utilizar comentários no código);
- Padrões e boas práticas utilizadas (use e abuse do SOLID).

Não avaliaremos mas gostamos de ver:
- Testes automatizados (principalmente testes unitários cobrindo as regras de negócio).

## Entrega
Disponibilize o código para acessarmos em um repositório em alguma plataforma que utiliza git como controle de versão (github, gitlab, ...). Caso queira manter o repositório privado basta conceder acesso para o email `pedro@fotop.com.br`.

Nos notifique por email que o codigo está pronto para ser avaliado e nos envie o link do repositório.

**Importante: No README.md do repositório deve possuir as informações necesárias para executar a aplicação. Você pode optar por usar um monorepo ou repositórios separados.** 
