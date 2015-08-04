# Meetup_BPM_ECM
Notas sobre as reuniões do Meetupu BPM &amp; ECM de Curitiba

#Meetup 01/08/2015 - Temas abordados:

## 1. Modelagem de Processos de Negócio (BPM – Business Process Management) 

BPM se apresenta como um conjunto de técnicas e práticas que ajudam a mapear os ativos e os serviços de TI nas necessidades de negócio das organizações.

Chamamos de “Arquitetura de Negócio” (não confundir com Arquitetura de TI – atenção há um erro na figura do PDF distribuído no Meetup) a 4 grupos de informações:
* Mapeamento dos Processos de Negócio (BPM)
* Mapeamento dos Papéis dos envolvidos
* Mapeamento das Regras de Negócio
* Mapeamento dos Ativos Documentais

Vimos que houve um movimento na primeira década deste século que resultou em um conjunto de padrões: para notação e automação de processos (BPMN), para regras de negócio (DMN), e para especificação de repositórios de Ativos Documentais (CMIS).

**Importante: a BPMN em sua versão 2.0 padroniza a notação e também a automação de processos.**

##1.1 BPMS
Vimos que os sistemas de automação de processos de negócio (BPMS – Business Process Management Systems) podem ser estruturados em componentes (vejam figura do material distribuído), sendo o Motor-BPM, o módulo de Experiência-do-Usuário e o Modelador, 3 destes principais componentes.

![componentes de um BPMS](./images/bpms.png?raw=true "Componentes de um BPMS")

## 2. Exercício de Modelagem
Instalamos e rodamos o BPMS Activiti (www.activiti.org) um projeto free-software com um poderoso motor de BPM.

Observação: a justificativa da escolha do Activiti como primeira solução de BPMS a ser apresentada para o grupo está baseada na simplicidade do Modelador e da interface do usuário, e pelo fato do motor deste produto ter uma das mais amplas implementações da BPMN disponíveis no mercado.

Foi utilizado o documento _BPMN 2.0 by Example_ que pode ser baixado do site da OMG.

Implementamos _quase todo_ o primeiro processo apresentado no documento. O fluxo deste processo possui as seguintes particularidades:

###2.1 Junções e Disjunções
O fluxo modelado utiliza 3 tipos diferentes de disjunções e junções:
* paralelismo
* ou-exclusivo
* ou-inclusivo

Uma forma divertida de analisar o comportamento destas junções é criar instâncias do fluxo e verificar como o Motor-BPM se comporta conforme a execução das tarefas.

Por exemplo, para o fluxo _Hardware Retailer_, a próxima figura mostra quais tarefas estão sendo executadas depois do fluxo passar pela disjunção _Paralela_ e pela disjunção de _OU-exclusivo-.

![componentes de um BPMS](./images/running.png?raw=true "Componentes de um BPMS")

Na configuração da junção ou-exclusivo chamada “Mode of Delivery” utilizou-se uma variável de processo chamada `carrier' que é atribuída a um de 2 valores:
- Normal(false) ou 
- Carrier(true) 

(pelo usuário que executa a tarefa precedente _Decide if normal post or special shipment_) 

Um dos fluxos de saída da junção está marcado como `default` enquanto o outro apresenta uma lógica onde o valor da variável é testado:

`${carrier == false}


# 3. Tarefas
Neste fluxo todas as tarefas são do tipo _tarefas de usuários_ (user tasks), cujo funcionamento implica em interfacear com o usuário para a execução da mesma.

Vale ressaltar que a BPMN 2.0 não especifica “como” este interfaceamento com o usuário ocorre, isto fica a cargo de cada implementação da _Experiência do Usuário_ de cada BPMS.

No caso do _Activiti_ estamos usando variáveis definidas na propriedade _form_properties_, porém _Activiti_ provê outras formas mais robustas para resolvermos esta questão.

Para variar um pouco, na implementação disponibilizada eu troquei uma das tarefas para o tipo _script_task_, e registrei um _script_groovy_ que faz apenas um log de mensagem:

`out.printn("UM SCRIPT GROOVY");

O BPMS Activiti também suporta javascript.

##3.1 Orquestração

Outro tema importante é que o fluxo do exemplo não especifica como as informações são trocadas entre as tarefas e os diversos usuários que as executam. A análise de como as informações são estruturadas durante a execução de um fluxo é chamada de “orquestração”.

# 4. Fluxo em BPMN2.0
O fluxo está disponível para download.





