# Floquinho-viajante
Projeto feito para a disciplina de Inteligência Artificial SCC 0530 ministrada pela professora doutora Solange Oliveira Rezende.

Esse trabalho buscava aplicar em algum problema real, as técnicas de busca informada e não informada que vimos na disciplina.

Como a grande maioria dos membros do grupo participava do grupo de extensão da Campanha USP do Agasalho, escolhemos um problema relacionado à Campanha, a busca das caixas de arrecadação.

![Símbolo da Campanha](https://github.com/user-attachments/assets/c3cf4321-0243-4853-aae3-062aa318715d)

O grupo possui mais de 100 caixas de doações espalhadas pela região de São Carlos, e organizar rotas selecionando quais caixas buscar e qual caminho tomar sempre foi um desafio com nossa quantia reduzida de carros.

Diante desse desafio, desenvolvemos duas abordagens em python, uma utilizando busca não informada e outra informada, e comparando os resultados, seguindo os requisitos da disciplina. O código pode ser encontrado no colab presente neste git, mas uma explicação mais detalhada também pode ser encontrada abaixo.


Antes de continuarmos, alguns detalhes adicionais importantes. 

Primeiro, limitamos o número de caixas a serem buscadas para 5, mas poderíamos facilmente escalar para mais caixas, aumentando um pouco o tempo de execução dos algorimtos. Escolhemos 5 por ser a quantidade aproximada de caixas que um carro consegue coletar antes de encher e por ser um número pequeno, ajuda tanto com o tempo de execução do algoritmo, quanto na visualização dos resultados.

Além disso, um outro aspecto importante da nossa busca é que é importante priorizarmos as caixas mais antigas, para evitar insatisfação dos donos de estabelecimentos com caixas antigas e liberar as caixas mais rapidamente para receberem mais doações.

##Modelagem
Primeiro de tudo, para conseguirmos aplicar os métodos de busca, precisaríamos modelar o  nosso problema. Para isso, utilizamos a biblioteca osmnx para conseguir gerar um grafo das ruas da cidade de São Carlos e desenvolvemos funções para descobrir a distância entre caixas a partir das coordenada da caixa aplicada nesse grafo.

![Grafo das ruas acessíveis de São Carlos.](https://github.com/user-attachments/assets/66b4096a-e73b-4c96-b84f-adb8390633e9)

Com as caixas e as distâncias entre elas, conseguimos montar o nosso grafo em que faríamos as buscas. Não ficou exatamente um grafo bonitinho, ainda mais quando colocávamos muitas caixas, mas tínhamos um grafo.

![Grafo com as caixa. Cada caixa é um vértice e as arestas contém como peso as distâncias entre elas. Detalhe importante que o peso de dia e volta pode ser diferente.](https://github.com/user-attachments/assets/423801ee-3e62-4338-8fa8-cdcd9ee8fd56)

## Busca Não Informada

A primeira estratégia que decidimos utilizar foi a busca em profundidade (DFS). Escolhemos ela ao invés da em largura, pois esta percorreria muitos nós a cada iteração (crescimento fatorial), o que a tornaria muito inviável conforme aumentássemos o número de caixas.

Como fizemos um algoritmo bem simplificado, o retorno consiste nas 5 primeiras caixas inseridas no grafo ( ou seja, as mais antigas), um resultado simples mas consideravelemnte satisfatório, pois pelo menos resolveu o problema de priorizar as caixas que estão cheias há mais tempo.

Para vizualização, utilizamos o google maps para representar as rotas, e é perceptível a falta de uma otimização nas caixas escolhidas.![mapa no maps do DFS](https://github.com/user-attachments/assets/68f41610-4206-4343-a7e6-1b34916b571b)

## Busca Informada

Aqui, para a nossa busca heurítica, escolhemos um algoritmo que adicionava na rota sempre a caixa de menor custo, podendo haver inserções no fim, início ou meio da rota. O custo era determinado pela distância em metros somada a 100 * a quantidade de dias que estava cheia, buscando um certo equilíbrio entre gasto de combustível e tempo que a caixa ficaria cheia.

 Repetimos o uso do google maps para gerar a rota, e obtivemos um resultado bem mais satisfatório. ![map no maps da busca heurística](https://github.com/user-attachments/assets/f302ea30-4085-4187-bc4e-b15c2bc705b6)

 #Membros do grupo

Angela Patricia Mestas Muñante
Artur de Vlieger Lima  		
Bruna Pereira Serrano da Mata 	 
Ítalo de Matos Saldanha			
Lucas Pereira Franco de Almeida	
Pedro Henrique Cruz da Silva
