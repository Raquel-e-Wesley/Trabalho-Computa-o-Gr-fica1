# Trabalho de Computacao Grafica

Autores: Raquel Nunes e Wesley Araújo
 
## Introdução
Este trabalho consiste na implementação de algoritmos para rasterização de pontos e linhas, o qual é requisito como parte da nota referente à disciplina de Introdução à Computação Gráfica, ministrada pelo professor Christian Azambuja Pagot no Centro de Informática da Universidade Federal da Paraíba. Para isso, foi utilizado um framework desenvolvido pelo professor a fim de simular o acesso direto à memória de vídeo.

## Metodologia
A implementação das funções requeridas foi feita utilizando-se da linguagem de programação C, do Codeblocks e do GLUT (OpenGL Utility Toolkit).

## Fundamentação Teórica
É necessário entender que a disposição dos pixels no monitor difere da memória. Enquanto que no primeiro considera-se um espaço bidimensional (largura e altura), no segundo eles estão dispostos de forma linear no Color Buffer. Dessa Forma, tais diferenças devem ser levadas em consideração no acionamento dos pixels.
Além disso, o padrão RGBA foi utilizado nesse trabalho. Portanto, cada pixel é formado por 4 componentes de cor sendo: R para vermelho (RED), G para verde (GREEN), B para azul (BLUE) e A para o alfa (ALPHA). As imagens a seguir ilustram o que foi explicado
![alt text](https://github.com/Raquel-e-Wesley/Trabalho-Computa-o-Gr-fica1/blob/master/1.png)

![texto alt](https://github.com/Raquel-e-Wesley/Trabalho-Computa-o-Gr-fica1/blob/master/2.png)

## Rasterização de Pontos
Para implementar a função de desenhar Pontos na tela putPixel(), foi utilizado o framework disponibilizado pelo professor, o qual contém um ponteiro chamado FBPtr que aponta para o início da região do framebuffer e manipulando o mesmo foi possível implementar a função PutPixel() . Essa função rasteriza um ponto na memória de vídeo recebendo como parâmetro o objeto da classe Vertex, que possui a posição (x,y) dele na tela e sua cor (RGBA). A figura abaixo mostra três pontos desenhados na tela usando essa função. 

![texto alt]{https://github.com/Raquel-e-Wesley/Trabalho-Computa-o-Gr-fica1/blob/master/3.png}

## Rasterização de Linhas
Rasterização de linhas é a geração de pontos em um determinado intervalo, gerando, assim, retas. Dentre os métodos de rasterização, o proposto para este trabalho foi o de Bresenham. Esse algoritmo é caracterizado por sua eficiência e desempenho já que não faz arredondamentos nem multiplicações sucessivas.
Ele funciona escolhendo entre dois pixels a cada iteração, baseado na variável de decisão previamente calculada, e posteriormente incrementando tal variável de acordo com o valor escolhido do pixel. Esse processo repete-se até o desenho completo da reta. Esta variável de decisão pode ser definida por:
D = 2y — dx;
onde
Dx = Xfinal — X
Dy = Yfinal — Y
Se o valor de D <= 0 então o pixel escolhido está acima da reta, logo sua variável de decisão será incrementada com erro de aproximação E = 2dy. Caso contrário, o pixel está abaixo dela e, portanto, o erro será de SE = 2*dy — dx. Tal procedimento repete-se até o desenho completo da reta.
Inicialmente, o algoritmo baseia-se no fato de que o segmento de reta encontra-se no primeiro octante, ou seja, com inclinação entre 0º e 45º, em que o coeficiente linear esteja entre 0 ≤ m ≤ 1. Entretanto, é possível generalizar o algoritmo para os demais octantes observando e modificando os valores assumidos por essas variáveis nos demais octantes.
O algoritmo pode ser estendido para atender valores de m entre 0 e -1 checando se y precisa ser incrementado ou decrementado. Isso foi feito no função plotLineLow(). A figura abaixo mostra uma linha obtida com essa função.

![textp alt}{https://github.com/Raquel-e-Wesley/Trabalho-Computa-o-Gr-fica1/blob/master/4.png}
 
Uma maneira de implementar o algoritmo de Bresenham para valores grandes de m (maiores que 1) positivos e negativos é simplesmente fazer uma troca de eixos, e eixo x passa a ser o eixo y e vice-versa. A função plotLineHigh() faz esse papel.
Por fim, a função drawLine() combina as duas funções apresentadas anteriormente, detectando qual das duas funções é mais apropriada dependendo da entrada e se as coordenadas precisam ser invertidos antes de desenhar. A figura abaixo mostra linhas desenhadas em todos os octantes usando essa função.

![texto alt]{https://github.com/Raquel-e-Wesley/Trabalho-Computa-o-Gr-fica1/blob/master/5.png}
## Triângulos
Para desenhar triângulos foi desenvolvida a função drawTriangle(). Esta função desenha as arestas de um triângulo na tela recebendo como parâmetros os três vértices. Logo, é necessário realizar a chamada da função DrawLine() três vezes passando dois vértices em cada chamada. A figura abaixo mostra dois triângulos desenhados na tela usando essa função. 

 
## Considerações Finais
Sem dúvidas o trabalho acrescentou bastante no nosso conhecimento em OpenGL com relação a rasterização. O algoritmo de Bresenham foi a parte mais trabalhosa sobretudo sua generalização para os oito octantes bem como a interpolação.
Como melhoria seria interessante o preenchimento por completo dos triângulos inicialmente sem interpolação e posteriormente com.
 
## Referências

https://github.com/ThiagoLuizNunes/CG-Assignments/tree/master/cg_framework
https://en.wikipedia.org/wiki/Bresenham%27s_line_algorithm

