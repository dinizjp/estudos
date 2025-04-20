# Pratical guide to building agents from OpenAI

```
 Agentes são sitemas independentes que operam tarefas em seu lugar 
 
```
* Workflow é a sequencia de passos para atingir o objetivo desejado, seja ele commitar um push no git, ou fazer uma pesquisa profunda

## Caracteristicas principais dos agents

1 - Agents conseguem reconhecer o workflow quando completo, corrigir ações se necessário e em caso de falha, pode ser transferido o poder de volta para o usuário

2-  Pode possuir diversas ferramentas para interagir com sistemas externos, sendo elas guardadas com contexto permitindo tomar ações de forma dinamica dependendo do estado do workflow, operando de forma clara com "barreias protetoras"

## Quando devemos construir agents ?

1 - Quando temos decições complexas - que envolvem nuancias, excessões ou decisões sensíveis ao contexto

2 - Dificuldade de manter regras - Sistemas que se tornaram pesados demais devido a quantidade de regras presentes para funcionar, tornando atualizações caras ou sujeitas a erros 

3 - Grande dependência a dados não estruturados - Cenários que envolvem a interpretação de linguagem natural, extraindo significado de documentos ou interagindo com pessoas atráves de conversas 

* Antes de construir um agent, entenda se seu problema se encaixa nesses criterios, caso não, soluções deterministicas devem ser o suficiente 

## Fundamentos do agent desing 

De forma fundamental, o agente consiste em 3 componetes principais 

1 - Modelo - Qual LLM vai dar poder de razão e descição para para o agent 

2 - Ferramentas - Funções externas ou APIs que ele pode usar para tomar ação 

3 - Intruções - Guia explicito e barreias protetoras defindo o comportamento do agent

## Selecionando seu modelo

Diferentes modelos tem diferentes forças e tradeoffs relacionadno a complexidade da tarefa, latência e custo. Considere usar diferentes modelos para diferents tarefas no workflow, visto que nem toda tarefa necessita do modelo mais inteligente

Uma simples tarefa simples pode ser passada para um modelo menor, que é  mais rápido, enquanto uma tarefa complexa que requer tomada de decições se beneficia de um modelo mais capaz

A melhor abordagem seria criar um protótipo de agent com o modelo mais capaz para se estabelecer uma linha base boa de perfomance, e a partir dai, seguir trocando partes do workflow por modelos menores para ver se eles conseguem cumprir a função com resultados semelhates, assim você não precisa limitar as habilidades dos agents e criar um diagnostico de onde modelos mais inteligentes vão falhar ou ter sucesso 

Em resumo, os principios para escolher os modelos são:

01 - Configure avaliações para estabelecer a linha base de performance que espera do agent

02 - Foque em obeter a acurácia alvo com os melhores modelos disponíveis 

03 - Otimize para reduzir custo e latência trocando por modelos menores quando possível 

## Definindo ferramentas 

Ferramentas extendem as capacidades dos agents atráves de APIs e para sistemas sem APIs, agents podem usar modelos capazes de interagir com o computador diretamente como um ser humano faria 

Cada ferramente deve ter uma definição padronizada, permetindo flexibilidade e multiplas relações entre agents e ferramentas. Uma boa documentação, testes de performance e ferramentas reutilizavéis melhoram descoberta, simplifica a manutenção e previne redundâncias 

Agents necessitam de 3 tipos básicos de ferramentas:

| Type | Descrição | Exemplo |
|:---- | :-------: | :------ |
| Data | Permite buscar informações necessárias para executar o workflow | Querys, Leitura de PDFs ou Docs, Pesquisa na web |
| Ações | Permite interagir com sistemas e tomar ações como adicionar informações, criar documentos ou mandar msgs | Mandar Emails, fazer commit, Atender pessoas |
| Orquestração | Agents por eles mesmo podem servir de ferramentas para outros agents | Agent de pesquisa, Agent para escrita, etc... |
 
  



