# Trabalho Prático 1 - Algoritmos 2
Túlio Dias Altíssimo - 2017014375


## Definição do Problema
O trabalho consiste em criar um algoritmo para resolver o Problema da Galeria de Arte. Dado um polígono que representa a planta de uma galeria de arte, o problema consiste em saber qual o menor número de guardas e em que posições eles devem ser colocados para que toda a galeria seja vigiada simultaneamente. Para tal, era preciso primeiro implementar o algoritmo de triangulação Ear Clipping e, dado o polígono triangulado, fazer a 3-coloração de cada vértice e assim, saber qual a posição dos guardas, analisando a cor de vértice que menos se repete. O algoritmo foi implementado em Python, por Jupyter Notebook criado com o Google Colab.


## Resolução
A resolução do problema foi feita em três etapas. A primeira consiste na implementação do Ear Clipping, a segunda na coloração dos vértices e a terceira em encontrar a posição dos guardas.
Para o Ear Clipping, foi feita uma função que recebe os pontos de cada um dos vértices do polígono e, a partir do ponto inicial, ele analisa o ponto anterior e o posterior para saber se o vértice atual é uma ponta de orelha, verificando a magnitude de uma reta C, formada pelo produto vetorial entre as retas Pi-1-Pi e Pi-1-P1+1. Além disso, é necessário analisar se algum dos outros pontos do polígono está contido dentro do triângulo formado por esses três pontos, pois se existir esse ponto, o vértice atual não é uma ponta de orelha. Caso o vértice seja uma ponta de orelha, salvamos os três pontos em uma lista que guarda todos os triângulos formados pela função e removemos a ponta de orelha do polígono. Se não for uma ponta de orelha, caminhamos para o próximo ponto. O loop termina ao restarem apenas três pontas no polígono original. Após isso criamos um dicionário que representa um grafo de triângulos. Cada nó é um dos triângulos formados pelas operações anteriores, e a aresta entre eles é se eles compartilham um dos lados. Dessa forma cada chave é um índice de triângulo da lista, e os valores são os índices dos triângulos adjacentes. Ao final da função retornamos a lista de triângulos, o grafo, e o plot da execução de cada passagem do Ear Clipping.
Para a coloração, foi feita uma função que recebe a lista de triângulos e o grafo e coloca em um dicionário em que cada chave é um ponto e o valor é a cor dele. Os vértices do primeiro triângulo são coloridos arbitrariamente e, em seguida, analisamos seus vizinhos, dado o grafo recebido. Descobrimos qual dos pontos ainda não está colorido e colocamos a cor restante nele, colocando o índice desse triângulo em uma fila. Ao analisar todos os vizinhos do triângulo atual, andamos com a fila, sendo esse índice retirado o novo triângulo principal. Ao final da execução, todos os vértices estão coloridos e retornamos o dicionário de cores.
Com isso encontramos a cor menos repetida, e a quantidade de vezes que ela aparece. É então plotado o polígono triangulado final, os vértices coloridos e, em cima dos vértices escolhidos, a palavra “guarda”.
