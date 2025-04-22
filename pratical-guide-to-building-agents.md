# Pratical guide to building agents from OpenAI

> Agentes são sitemas independentes que operam tarefas em seu lugar 
 
> Workflow é a sequencia de passos para atingir o objetivo desejado, seja ele commitar um push no git, ou fazer uma pesquisa profunda

---

## Caracteristicas principais dos agents

1. **Agents conseguem reconhecer o workflow quando completo, corrigir ações se necessário e em caso de falha, pode ser transferido o poder de volta para o usuário**

2. **Pode possuir diversas ferramentas para interagir com sistemas externos, sendo elas guardadas com contexto permitindo tomar ações de forma dinamica dependendo do estado do workflow, operando de forma clara com "barreias protetoras"**


## Quando devemos construir agents?

1. Quando temos decições complexas - Que envolvem nuances, exceções ou decisões sensíveis ao contexto

2. Dificuldade de manter regras - Sistemas que se tornaram pesados demais devido a quantidade de regras presentes para funcionar, tornando atualizações caras ou sujeitas a erros 

3. Grande dependência a dados não estruturados - Cenários que envolvem a interpretação de linguagem natural, extraindo significado de documentos ou interagindo com pessoas atráves de conversas 

> Antes de construir um agent, entenda se seu problema se encaixa nesses critérios, caso não, soluções deterministicas devem ser o suficiente 


## Fundamentos do agent desing 

De forma fundamental, o agente consiste em 3 componetes principais 

1. Modelo - Qual LLM vai dar poder de razão e descição para para o agent 

2. Ferramentas - Funções externas ou APIs que ele pode usar para tomar ação 

3. Intruções - Guia explicito e barreias protetoras defindo o comportamento do agent

## Selecionando seu modelo

Diferentes modelos tem diferentes forças e tradeoffs relacionadno a complexidade da tarefa, latência e custo. Considere usar diferentes modelos para diferents tarefas no workflow, visto que nem toda tarefa necessita do modelo mais inteligente

Uma simples tarefa simples pode ser passada para um modelo menor, que é  mais rápido, enquanto uma tarefa complexa que requer tomada de decições se beneficia de um modelo mais capaz
A melhor abordagem seria criar um protótipo de agent com o modelo mais capaz para se estabelecer uma linha base boa de perfomance, e a partir dai, seguir trocando partes do workflow por modelos menores para ver se eles conseguem cumprir a função com resultados semelhates, assim você não precisa limitar as habilidades dos agents e criar um diagnostico de onde modelos mais inteligentes vão falhar ou ter sucesso 

Em resumo, os principios para escolher os modelos são:

1. Configure avaliações para estabelecer a linha base de performance que espera do agent

2. Foque em obeter a acurácia alvo com os melhores modelos disponíveis 

3. Otimize para reduzir custo e latência trocando por modelos menores quando possível 

## Definindo ferramentas 

Ferramentas extendem as capacidades dos agents atráves de APIs e para sistemas sem APIs, agents podem usar modelos capazes de interagir com o computador diretamente como um ser humano faria 

Cada ferramente deve ter uma definição padronizada, permetindo flexibilidade e multiplas relações entre agents e ferramentas. Uma boa documentação, testes de performance e ferramentas reutilizavéis melhoram descoberta, simplifica a manutenção e previne redundâncias 

**Agents necessitam de 3 tipos básicos de ferramentas:**

| Type | Descrição | Exemplo |
|:---- | :-------: | :------ |
| Data | Permite buscar informações necessárias para executar o workflow | Querys, Leitura de PDFs ou Docs, Pesquisa na web |	
| Ações | Permite interagir com sistemas e tomar ações como adicionar informações, criar documentos ou mandar mensagens | Mandar Emails, fazer commit, Atender pessoas |
| Orquestração | Agents por eles mesmo podem servir de ferramentas para outros agents | Agent de pesquisa, Agent para escrita, etc... |

## Configurando instruções 

> Intruções de alta qualidade são essencias para LLMs, especialmente para agents se você quiser reduzir ambiguidade e melhorar a tomada de decição, reduzindo erros no workflow.

**Melhores práticas para instruções**

| Princípio                         | Descrição                                                                                      |
| :-------------------------------- | :--------------------------------------------------------------------------------------------- |
| Use documentação existente        | Quando criar rotinas, use documentos prontos, documentação de processos ou banco de conhecimento para oferecer contexto aos modelos |
| Solicite aos agentes dividir tarefas | Ao acessar documentos densos, providencie um pequeno e claro passo a passo para reduzir ambiguidade e ajudar o modelo a seguir instruções |
| Defina ações claras               | Tenha certeza de que cada passo na rotina seja específico a uma ação ou resultado esperado, evitando cometer erros de interpretação |
| Capture casos extremos | Interações na vida real causam pontos de descisão, como dados faltantes ou perguntas inesperadas, uma rotina robusta antecipa comportamentos comuns e inclue instruções de como lidar com essas intereções |


> Podemos usar os modelos com raciocínio para escrever instruções automaticamente a partir de uma documentação 

Exemplo de prompt descrito no pdf:

``` 
You are an expert in writing instructions for an LLM agent. Convert the following help center document into a clear set of instructions, written in a numbered list.
The document will be a policy followed by an LLM. Ensure that there is no ambiguity, and that the instructions are written as directions for an agent.
The help center document to convert is the following {{help_center_doc}}  

``` 

## Orquestração 

Com os componentes básicos no lugar, podemos considerar padrões de orquestração para ajudar o agent a executar o workflow de maneira eficiênte 

> Por mais que seja tendador começar a construir uma arquitetura complexa de inicio, é recomendado usar uma abordagem incremental para garantir um maior sucesso 

Em geral, padrões de orquestração seguem duas **categorias**:

Categoria | Descrição 
:-------- | :---------
Single-agent systems | Onde um unico modelo é equipado com ferramentas apropriadas e instruções para executar workflows em loops 
Multi-agents systems | Onde um workflow é executado de maneira distribuída entre múltiplos agents coordenados 

### Single-agent systems 


Single-agent:
![alt text](https://github.com/dinizjp/estudos/blob/main/imgs/single-agent.png)

