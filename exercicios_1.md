# Lista de Exercícios: Programação Funcional em Erlang

## 1. Explorando o Shell do Erlang

**Instrução:** Execute comandos no shell Erlang para realizar operações básicas, como cálculo aritmético (`2+3*4`) e exibir texto com `io:format/2`. Observe como o shell responde a cada expressão e como cada comando deve terminar com `.`.

**Ambiente:** REPL (Shell interativo do Erlang)

## 2. Variáveis e Imutabilidade

**Instrução:** No REPL, crie uma variável e atribua um valor a ela (por exemplo, `X = 5.`). Em seguida, tente atribuir um novo valor à mesma variável (`X = 6.`) e observe o resultado. Experimente também usar o sublinhado `_` como variável anônima em uma correspondência (por exemplo, `_ = 10`).

**Ambiente:** REPL

**Reflexão:** Por que o Erlang não permite reatribuir uma variável depois de vinculada? Compare com variáveis em linguagens imperativas (onde valores podem mudar livremente) e considere as implicações da imutabilidade para a segurança e a concorrência do programa.

## 3. Pattern Matching Básico

**Instrução:** Utilize pattern matching no shell para extrair valores de estruturas. Por exemplo, faça corresponder uma tupla `{ok, Valor}` a uma variável `Valor` executando `{ok, Valor} = {ok, 42}.` e decompose uma lista em cabeça e cauda executando `[H|T] = [1,2,3].`. Observe o que acontece se o padrão não combina (ex.: tente corresponder `[X,Y] = [1,2,3]` e veja o erro).

**Ambiente:** REPL

**Reflexão:** Em outras linguagens, como você extrairia partes de uma estrutura (por exemplo, os elementos de uma tupla ou lista)? Compare o pattern matching de Erlang com usar condicionais if/else ou estruturas switch/case para decompor estruturas em linguagens imperativas.

## 4. Listas e Tuplas – Operações Básicas

**Instrução:** No REPL, crie uma lista de alguns elementos (por exemplo, `[10, 20, 30]`) e experimente operações básicas: obtenha a cabeça e a cauda com as funções nativas `hd/1` e `tl/1`; concatene duas listas usando o operador `++` (por exemplo, `[1,2] ++ [3,4]`). Em seguida, crie uma tupla, acesse elementos específicos com `element/2` e obtenha o tamanho da tupla com `tuple_size/1`. Observe os resultados e a diferença entre listas (coleções ligadas) e tuplas (estruturas de tamanho fixo).

**Ambiente:** REPL

## 5. Função Módulo Simples – Quadrado de um Número

**Instrução:** Escreva um módulo Erlang (`math_utils.erl`) definindo uma função `quadrado(N)` que retorne o quadrado de um número dado. Compile o módulo no shell (`c(math_utils).`) e teste chamando `math_utils:quadrado(5).` para verificar o resultado (25).

**Ambiente:** Módulo Erlang (`.erl` compilado)

## 6. Múltiplas Cláusulas e Guardas – Sinal do Número

**Instrução:** Implemente uma função `sinal(N)` em um módulo que devolve `positivo` se `N > 0`, `negativo` se `N < 0` ou `zero` se `N == 0`. Use múltiplas cláusulas de função com guardas para cada condição (por exemplo, `sinal(N) when N > 0 -> positivo`). Compile e teste a função com valores positivos, negativos e zero.

**Ambiente:** Módulo Erlang

## 7. Recursão Básica – Fatorial

**Instrução:** No módulo `math_utils`, escreva a função recursiva `fatorial(N)` que calcula o fatorial de `N` (assuma `N >= 0`, com `0! = 1`). Use uma cláusula base para `N = 0` que retorna 1, e outra cláusula recursiva para `N > 0` que calcula `N * fatorial(N-1)`. Compile e teste a função chamando, por exemplo, `math_utils:fatorial(5).` (o resultado deve ser 120).

**Ambiente:** Módulo Erlang

## 8. Recursão em Listas – Soma dos Elementos

**Instrução:** Crie uma função `soma_lista(List)` em um módulo que calcule a soma de todos os números em uma lista. Use pattern matching para definir o caso base (lista vazia `[]` retorna 0) e o caso recursivo (separando cabeça `H` e cauda `T` da lista, de forma que `soma_lista([H|T])` retorne `H + soma_lista(T)`). Por exemplo, `soma_lista([2,5,7])` deve retornar 14.

**Ambiente:** Módulo Erlang

**Reflexão:** Como essa implementação recursiva se compara a como você somaria os elementos de uma lista usando um loop (`for` ou `while`) em uma linguagem imperativa? Explique as diferenças de abordagem – em Erlang usamos recursão e imutabilidade em vez de variáveis mutáveis para acumular resultados.

## 9. Recursão de Cauda – Fatorial Otimizado

**Instrução:** Reimplemente a função `fatorial/1` de maneira tail-recursive (recursão de cauda). Para isso, defina uma função auxiliar `fatorial_acc(N, Acc)` em que `Acc` acumula o resultado parcial. A implementação deve chamar `fatorial_acc(N-1, N*Acc)` recursivamente, e `fatorial_acc(0, Acc)` deve retornar `Acc`. Ajuste `fatorial(N)` para chamar `fatorial_acc(N, 1)` inicialmente. Compile e teste a nova versão para garantir que `math_utils:fatorial(5).` ainda retorna 120.

**Ambiente:** Módulo Erlang

**Reflexão:** Por que a versão tail-recursive é mais eficiente para N grandes? Pesquise o conceito de Tail Call Optimization na VM Erlang e explique como a recursão de cauda evita o crescimento da pilha de chamadas, reutilizando a stack frame da função – similar ao que um loop faria internamente.

## 10. Funções Anônimas e Funções de Ordem Superior

**Instrução:** No REPL, defina uma função anônima que duplica um número, por exemplo: `Dobra = fun(X) -> 2 * X end.`. Aplique essa função a um valor (`Dobra(5)` deve resultar em 10). Em seguida, use `lists:map/2` para aplicar essa função anônima a cada elemento de uma lista: `lists:map(Dobra, [1,2,3,4]).` deve produzir `[2,4,6,8]`. Experimente também definir e usar uma função anônima diretamente na chamada de `map/2` (sem atribuí-la a uma variável).

**Ambiente:** REPL

**Reflexão:** Linguagens como JavaScript, Python ou Java (versões recentes) suportam funções anônimas (lambdas). Como é passar funções como argumentos em Erlang comparado a passar funções/ponteiros de função em outras linguagens? Pense em como isso facilita escrever código mais genérico e evita duplicação, em contraste com soluções orientadas a objetos (como usar interfaces ou classes abstratas para obter comportamentos parametrizáveis).

## 11. List Comprehensions – Filtrando e Transformando Listas

**Instrução:** Utilize list comprehensions no shell para criar novas listas a partir de listas existentes de forma concisa. Por exemplo, dada a lista `[1,2,3,4,5]`, produza uma lista com os quadrados apenas dos números pares:

```erlang
[X*X || X <- [1,2,3,4,5], X rem 2 == 0].
```

Isso deve retornar `[4,16]`. Em seguida, experimente criar outras compreensões, como duplicar todos os elementos de uma lista ou filtrar apenas os elementos que satisfazem uma certa propriedade.

**Ambiente:** REPL

## 12. Implementando map/2 Manualmente

**Instrução:** Implemente sua própria versão de uma função de ordem superior `map(Fun, Lista)` em um módulo (por exemplo, `meu_lista.erl`). A função deve retornar uma nova lista resultante da aplicação de `Fun` a cada elemento de `Lista`. Utilize recursão: o caso base opera em lista vazia, e o caso recursivo aplica `Fun` à cabeça e consome o resto da lista recursivamente. Por exemplo, `meu_lista:map(fun(X) -> X * X end, [2,3,4]).` deve retornar `[4,9,16]`.

**Ambiente:** Módulo Erlang

## 13. Expressão case – Descrevendo uma Lista

**Instrução:** Escreva uma função `descreve_lista(L)` em um módulo que retorna uma descrição do conteúdo da lista `L`. Use uma expressão `case` dentro da função para distinguir os cenários: se `L` é uma lista vazia, retorne, por exemplo, o átomo `vazia`; se tem exatamente um elemento, retorne `um_elemento`; caso contrário, retorne `varios_elementos`. Por exemplo, `descreve_lista([])` → `vazia`, `descreve_lista([5])` → `um_elemento`, `descreve_lista([1,2,3])` → `varios_elementos`.

**Ambiente:** Módulo Erlang

## 14. Expressão if com Guardas – Par ou Ímpar

**Instrução:** Implemente a função `par_ou_impar(N)` em um módulo, que retorna o átomo `par` se `N` for par, ou `impar` caso contrário. Utilize uma expressão `if` para isso, com guardas apropriadas:

```erlang
if
    N rem 2 == 0 -> par;
    true -> impar
end.
```

Lembre-se de incluir uma condição `true` final para abarcar "qualquer outro caso" (quando `N` não for par). Teste a função com valores diferentes, incluindo positivos, negativos e zero.

**Ambiente:** Módulo Erlang

## 15. Records – Definindo Estruturas Nomeadas

**Instrução:** Defina um record `pessoa` com campos `nome` e `idade` no cabeçalho de um módulo (por exemplo, usando `-record(pessoa, {nome, idade}).`). Nesse módulo, escreva uma função `nova_pessoa(Nome, Idade)` que retorna um record `#pessoa{nome=Nome, idade=Idade}`, e uma função `eh_maior_de_idade(P)` que recebe um record `Pessoa` e retorna `true` se `Pessoa#pessoa.idade >= 18` ou `false` caso contrário. Compile o módulo e teste no shell: crie uma pessoa com `P = modulo:nova_pessoa("Joao", 20).` e avalie `modulo:eh_maior_de_idade(P).` para verificar o resultado.

**Ambiente:** Módulo Erlang

**Reflexão:** Compare o uso de records em Erlang com o uso de estruturas/objetos em outras linguagens (por exemplo, structs em C ou objetos simples em Python/Java). Como os records são uma construção em tempo de compilação, qual é a principal diferença em relação a estruturas dinâmicas como mapas/dicionários?

## 16. Criando Processos Erlang

**Instrução:** No shell Erlang, crie um novo processo usando `spawn`. Por exemplo:

```erlang
spawn(fun() -> io:format("Olá de um processo ~p~n", [self()]) end).
```

Isso deverá lançar um processo concorrente que imprime uma mensagem identificando seu próprio Pid. Observe que `spawn` retorna imediatamente o identificador do processo filho. Experimente armazenar o Pid retornado em uma variável e imprimi-lo.

**Ambiente:** REPL (Shell Erlang)

## 17. Enviando e Recebendo Mensagens

**Instrução:** No REPL, crie um processo que aguarde uma mensagem, usando `receive`. Por exemplo:

```erlang
Pid = spawn(fun() ->
    receive
        Msg -> io:format("Recebido: ~p~n", [Msg])
    end
end).
```

Em seguida, envie uma mensagem para esse processo usando o operador `!` (send): `Pid ! {ola, "mundo"}.` Observe no shell que o processo filho imprime a tupla recebida. Tente enviar outros valores ou estruturas (o processo terminará após receber a primeira mensagem nesse exemplo).

**Ambiente:** REPL

**Reflexão:** Note que o envio de mensagem com `Pid ! Mensagem` é assíncrono – o remetente não bloqueia. Como esse modelo de comunicação por mensagens se compara com a comunicação entre threads em linguagens OO tradicionais (que frequentemente compartilham memória e precisam de locks para sincronização)?

## 18. Loop de Mensagens – Servidor de Eco

**Instrução:** Implemente um processo que permaneça ativo para múltiplas mensagens usando loop recursivo. Crie um módulo `eco.erl` com uma função `start()` que inicia um novo processo (com `spawn`) executando a função `loop()`. Na função `loop()`, utilize um `receive` para aguardar mensagens:

- Se receber a mensagem `parar`, o processo deve encerrar retornando algo como `ok`.
- Caso contrário (qualquer outra mensagem `Msg`), o processo deve imprimir `Msg` (eco, usando `io:format` ou similar) e então chamar recursivamente `loop()` para continuar aguardando novas mensagens.

Compile o módulo e teste no shell:

```erlang
Pid = eco:start().
Pid ! "teste".  % o processo deve imprimir "teste"
Pid ! 42.       % o processo deve imprimir 42
Pid ! parar.    % o processo deve encerrar
```

**Ambiente:** Módulo Erlang

## 19. Estado em Processos – Contador Acumulador

**Instrução:** Crie um módulo `contador.erl` que implemente um processo contador com estado interno. Implemente:

- `start(ValorInicial)`: spawn de um processo rodando `loop(ValorInicial)`.
- `loop(ValorAtual)`: no `receive`, trate três tipos de mensagem:
  - `{incrementar, X}`: o processo deve calcular um novo valor = `ValorAtual + X` e então chamar recursivamente `loop(NovoValor)`.
  - `{consultar, Caller}`: enviar o `ValorAtual` de volta para o processo `Caller` (`Caller ! ValorAtual`), depois continuar em `loop(ValorAtual)`.
  - `parar`: retornar normalmente, terminando o processo.

Teste no shell criando um contador:

```erlang
Pid = contador:start(0).
Pid ! {incrementar, 5}.
Pid ! {incrementar, 3}.
Pid ! {consultar, self()}.  % espera-se receber 8 de volta
receive X -> io:format("Valor = ~p~n", [X]) end.
Pid ! parar.
```

Observe como o estado (`ValorAtual`) é mantido no argumento da função recursiva, já que variáveis não podem ser alteradas.

**Ambiente:** Módulo Erlang

## 20. Timeout em Recebimento de Mensagem

**Instrução:** Ajuste o servidor de eco ou o contador para lidar com inatividade usando timeout no `receive`. Por exemplo, modifique o loop do exercício 18 (`eco:loop`) para:

```erlang
receive
    parar -> ok;
    Msg ->
        io:format("Eco: ~p~n", [Msg]),
        loop()
after 5000 ->
    io:format("Nenhuma mensagem recebida em 5s, terminando.~n", [])
end.
```

Isso faz o processo imprimir um aviso e encerrar caso nenhuma mensagem chegue em 5000ms. Teste enviando uma mensagem normal (deve resetar o temporizador quando o loop recomeçar) e depois não enviando nada para ver o timeout ocorrer.

**Ambiente:** Módulo Erlang

## 21. Comunicação Bidirecional – Ping-Pong

**Instrução:** Implemente dois processos concorrentes que trocam mensagens entre si como em um jogo de ping-pong. Crie um módulo `pingpong.erl` com:

- Uma função `iniciar(N)` que cria dois processos, um `ping` e um `pong`, passando a eles o número de trocas `N` a realizar.
- O processo `ping` deve enviar a mensagem `ping` ao processo `pong`, então aguardar uma resposta. Quando receber `pong` de volta, ele decrementa uma contagem e, se ainda não tiver terminado `N` rodadas, envia `ping` novamente. Se as trocas atingiram `N`, ele envia uma mensagem de parada ao `pong` e então termina.
- O processo `pong` deve aguardar mensagens: se receber `ping`, responde enviando `pong` de volta e continua; se receber um sinal de parada (por exemplo, `parar`), ele termina.

Teste chamando `pingpong:iniciar(5)` e observe no console a sequência de mensagens trocadas.

**Ambiente:** Módulo Erlang

## 22. Falha de Processo – Filosofia "Let It Crash"

**Instrução:** No REPL, provoque uma falha em um processo para ver como erros são isolados. Por exemplo:

```erlang
spawn(fun() -> 5 = 6 end).
```

ou

```erlang
spawn(fun() -> error(bad_thing) end).
```

Cada `spawn` inicia um processo que irá falhar imediatamente (por uma match inválida ou por lançar um erro). Observe a mensagem de erro exibida no shell e note que apenas o processo filho terminou anormalmente – o shell (processo chamador) não foi afetado.

**Ambiente:** REPL

**Reflexão:** Explique o conceito de "let it crash" na filosofia Erlang. Por que os desenvolvedores Erlang frequentemente permitem que um processo falhe sem tentar tratar todas as exceções? Compare com a abordagem de linguagens como Java, onde geralmente se usa try/catch para evitar que erros propaguem. Qual é a vantagem de deixar o processo cair e reiniciar limpo (possivelmente sob supervisão), em vez de tentar recuperar de um estado possivelmente corrompido?

## 23. Processos Linkados – Propagação de Falhas

**Instrução:** Experimente linkar dois processos para observar falhas propagadas. No shell, chame `process_flag(trap_exit, true)` para habilitar captura de saídas no processo atual (shell) e então:

```erlang
Pid = spawn_link(fun() -> exit(falhou) end).
```

Aqui o processo filho termina imediatamente com um sinal de saída. Como o processo pai (shell) está linkado ao filho, ele receberá um sinal de saída. No shell interativo, você deverá ver uma mensagem indicando que o shell recebeu um exit (o shell é uma exceção, ele se reinicializa para você continuar trabalhando).

**Ambiente:** REPL

**Reflexão:** Links criam uma relação de destino comum: se um processo cai, ele derruba os linkados (a não ser que estes capturem o sinal). Para que cenários você acha que ligar processos é útil em Erlang?

## 24. Supervisão Básica com trap_exit

**Instrução:** Implemente manualmente um supervisor simples usando `trap_exit`. Por exemplo, crie um módulo `meu_sup.erl` onde a função `iniciar()` faça o seguinte:

1. Ative `process_flag(trap_exit, true)` no processo supervisor.
2. Use `spawn_link` para iniciar um processo "trabalhador" (pode ser qualquer função que eventualmente falhe, por exemplo, uma que dê `exit(erro)`).
3. Em um loop `receive`, capture mensagens `{'EXIT', Pid, Razao}`. Quando receber o aviso de que o trabalhador caiu (`Razao ≠ normal`), logue essa ocorrência (por exemplo, `io:format("Processo ~p caiu: ~p~n", [Pid, Razao])`) e lance um novo processo trabalhador substituto (novamente com `spawn_link`), continuando o loop de supervisão. Você pode decidir encerrar o supervisor após certo número de restarts, ou executá-lo indefinidamente.

Execute `meu_sup:iniciar()` no shell e teste deixar o trabalhador falhar para observar o supervisor relançando-o automaticamente.

**Ambiente:** Módulo Erlang (supervisor simples)

**Reflexão:** Esse mecanismo manual imita o comportamento de um supervisor OTP. Qual a vantagem de ter um componente separado reiniciando processos caídos? Pense em como isso contribui para a tolerância a falhas no sistema – um processo monitora outros e garante que eles retomem uma função conhecida após falhas inesperadas.

## 25. Monitoramento de Processos

**Instrução:** Ao invés de usar links, utilize monitores para vigiar um processo sem derrubar o monitor caso o alvo caia. No shell Erlang, experimente:

```erlang
Pid = spawn(fun() -> timer:sleep(5000) end).  % processo que dorme 5s
Ref = erlang:monitor(process, Pid).           % iniciar monitoramento
exit(Pid, kill).                              % força o término do processo
flush().                                      % ou use receive para capturar a mensagem 'DOWN'
```

Você deverá receber uma mensagem do formato `{'DOWN', Ref, process, Pid, Razao}` no shell, indicando que o processo monitorado morreu (`Razao` será `killed` neste caso). Note que, diferentemente de links, o monitor apenas envia uma notificação e não encerra o processo monitor.

**Ambiente:** REPL

**Reflexão:** Quando você usaria `erlang:monitor/2` em vez de link? Compare as duas abordagens: o monitoramento permite observar a queda de um processo de forma unilateral (somente quem monitora recebe aviso) sem arriscar cair junto, enquanto o link geralmente é usado em processos que devem compartilhar destino (cair juntos) a menos que façam `trap_exit`.

## 26. (Dissertativo) Isolamento de Processos vs. Threads

**Instrução:** Explique por que os processos Erlang não compartilham memória e como esse isolamento impacta o modelo de concorrência. Compare o modelo de atores do Erlang (processos leves, isolados, comunicando-se por mensagens) com o modelo de threads em linguagens orientadas a objetos tradicionais (threads do SO compartilhando memória, sincronização via mutex/locks). Quais são os benefícios do isolamento de processos do Erlang em termos de evitar condições de corrida e deadlocks? Há algum custo ou desvantagem desse modelo em comparação com threads nativas compartilhando memória?

**Ambiente:** N/A (Pergunta conceitual)

## 27. Estruturando um Projeto com Rebar3

**Instrução:** Pratique a organização de código Erlang em um projeto OTP usando Rebar3. No terminal do sistema (não no shell Erlang), crie um novo projeto com `rebar3`:

```bash
rebar3 new app meu_app
```

Isso gerará a pasta `meu_app/` com estrutura padrão (`src/`, `test/`, etc.). Abra o arquivo `meu_app/src/meu_app_app.erl` e observe o módulo de aplicação OTP gerado. Em seguida, dentro do diretório do projeto, compile-o com `rebar3 compile`. Rode `rebar3 shell` para entrar no shell Erlang com a aplicação carregada (note que a aplicação define um supervisor vazio por padrão). Como exercício, crie um novo módulo no diretório `src` (por exemplo, `calc.erl` com uma função simples `soma/2`) e adicione esse módulo ao arquivo `.app.src` se necessário. Recompile o projeto e teste sua nova função no shell do projeto (`calc:soma(2,3).`).

**Ambiente:** Terminal do SO (uso da ferramenta Rebar3) e Editor de código (arquivos `.erl`)

**Reflexão:** Compare a organização de um projeto Erlang/OTP (com diretórios predefinidos e arquivo `.app` de configuração) com a forma como projetos são estruturados em outras linguagens que você conhece. Como ferramentas de build/gerência de dependências como Rebar3 facilitam o desenvolvimento em Erlang?

## 28. (Dissertativo) Paradigma Funcional vs. Orientado a Objetos

**Instrução:** Discuta as principais diferenças entre programação funcional (como em Erlang) e programação orientada a objetos (como em Java/C++). Foque em conceitos fundamentais:

- **Imutabilidade vs. Mutabilidade:** Como o tratamento de variáveis difere? Quais os benefícios de trabalhar com dados imutáveis em termos de bug e concorrência?
- **Estruturas de controle:** Comparar o uso de recursão, pattern matching e funções de alta ordem em Erlang com loops, condicionais e polimorfismo em linguagens OO.
- **Encapsulamento de estado:** Em Erlang, o estado é encapsulado dentro de processos isolados; em OO, dentro de objetos que interagem via métodos. Quais as implicações de cada modelo?
- **Concorrência:** Contraste o modelo de atores (processos + mensagens) com o modelo de threads compartilhadas.

Forneça exemplos de situações em que o estilo funcional oferece vantagens, e cenários onde pensar em objetos/classe pode ser mais natural, refletindo sobre sua experiência prévia em linguagens imperativas.

**Ambiente:** N/A (Pergunta conceitual)

## 29. (Dissertativo) Conceitos de OTP – Gen_Server e Supervisor

**Instrução:** Explique brevemente o que são behaviours OTP no Erlang. Em particular, descreva o propósito de um `gen_server` e de um `supervisor` no design de aplicações Erlang robustas. Como o `gen_server` abstrai o loop de recebimento de mensagens, facilitando a implementação de servidores genéricos (com chamadas síncronas via `call` e assíncronas via `cast`)? E como os processos do tipo `supervisor` definem estratégias de reinício automático de subprocessos em caso de falha? Relacione esses conceitos com o que você fez "manualmente" nos exercícios anteriores (como implementar loop de mensagem e reinício de processos).

**Ambiente:** N/A (Pergunta conceitual)

## 30. Refatorando do Imperativo para o Funcional

**Instrução:** Considere uma função imperativa (pseudocódigo) que encontra o maior número em uma lista de inteiros:

```
max = arr[0]
for i in 1 até len(arr)-1:
    if arr[i] > max:
        max = arr[i]
return max
```

Reescreva essa lógica em Erlang de forma funcional. No módulo `lista_utils.erl`, implemente a função `max_lista(List)` que retorna o maior valor de `List`. Use pattern matching e recursão (por exemplo, compare a cabeça com o máximo do restante da lista, ou utilize um parâmetro acumulador que carregue o maior valor encontrado até então). Por exemplo, `lista_utils:max_lista([7,2,9,4]).` deve retornar 9. Assuma que a lista contém pelo menos um elemento.

**Ambiente:** Módulo Erlang

**Reflexão:** Como foi o processo de converter um algoritmo de loop imperativo para um estilo funcional recursivo em Erlang? Quais mudanças de pensamento (como evitar variáveis mutáveis e usar recursion) foram necessárias? Após implementar, você vê vantagens na clareza ou desvantagens em relação à versão imperativa original?
