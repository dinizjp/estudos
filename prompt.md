#Engenharia de prompt - Asimov 

Tomar cuidado com os vieses, pois eles podem reproduzir vieses que estão nos dados da internet

Prompt exige um processo interativo:

Ideia -> Implemento -> Resultado experimental -> Análise de erros -> Recomeçar o ciclo                     

1º Princípio - Clareza e Especificidade 

- Clareza: O modelo não tem contexto da situação que estou passando, o modelo precisa saber quem eu sou e o que eu sei para que a resposta seja mais precisa

- Especificidade: Quando mais especifico eu sou, mais eu reduzo o campo de possibilidades do modelo para que ele entenda exatamente qual problema eu quero resolver 

Problemas de clareza e especificidade: 
- Sobrecarga - colocar informações demais que não são importantes para o contexto 
- Ambiguidade - não ficar falando de várias possibilidades, seja especifico e direto
- Complexidade - Não utilizar termos muito técnicos e nichados 

4 Elementos necessários de um prompt

- Contexto 
- Instrução ( O que o modelo deve fazer )
- Dados de entrada 
- Indicador de saída ( A partir daqui, quero que me dê a resposta )


Adicionais de contexto:

- Uso de Personas (Exemplo: Pessoas conhecidas, um estilo de fala, estilo de escrita, quem é você)

Exemplo: Crie uma história de magia usando o Estilo do Autor de senhor dos anéis

- Uso do público (Exemplo: Explique LLM para crianças)

- Uso de Exemplos (Passe exemplos de como ele deve se comportar)

Delimitadores - Use para separar exemplos, contextos específicos, ideias 

"""
- ####
- ’’’’
- ||||
- " ```` "
"""

Saída Estruturada - Use para criar consistência na saída da resposta 

Técnicas comuns
- One-Shot (Usar somente um exemplo para ele replicar)
- Few-Shot (Usar mais de um exemplo para entender / Limitações - Isso não ajuda o modelo a racionar, somente segue o exemplo que foi inserido) 


2º Princípio - Dar ao modelo tempo para pensar

COT (Chain of Thoughts) - Cadeia de pensamentos 
- Dê o exemplo do raciocínio para o modelo seguir antes de executar uma tarefa 


Usos:

Use modelos para resumo e extração de dados
-> Modelos são ótimos para entender e resumir uma grande quantidade de informações em formato texto, como reviews de um site ou respostas densas de formulários 


Inferência e Análise de sentimento
-> Da mesma forma que entendem e resumem muitas informações, podem inferir sobre o sentimento que está presente em um texto 

Tradução
-> Modelos são excelentes para traduzir e transformar grandes conjuntos de texto

Modificação 
-> Transformar formatos, exemplo: transformar arquivos json em dicionários 
























