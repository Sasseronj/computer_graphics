# Lista 1

* OBS:
  * Variável D = seu dia de nascimento 
  * Variável M = seu mês de nascimento

# Anotações

* Pipepline Fixo: renderização dependente de algoritmos, sem liberdade para customização ou substituição de algoritmos.
* Pipelineline Programável: inclusão de shaders, ou seja, etapas, programáveis de vértices e fragmentos.
* Primitivas Geométricas: Elementos gráficos simples que formam objetos complexos quando combinados. (Exemplos: Linhas, Triângulos, Cores, ...)
* Transformações Geométricas: São operações aplicadas aos vértices dos objetos, ou seja, na descrição geométrica dos objetos:
  * Primárias: Translação, Escala e Rotação
  * Secundárias: Reflexão, Cilhamento
* Ordem das transformações: Sua ordem importa, e sua matriz de transformação final é dada pela primeiro transformação mais a direita e a última a esquerda.

# Exercícios

1. **Qual a diferença entre Processamento de Imagens, Visão Computacional e 
Síntese de Imagens?**
    A diferença entre estes tópicos é relativo ao seus objetivos:
    
    * Processamento de Imagens: Possui o objetivo de melhorar as características visuais (reduzindo ruídos, aumentando brilho e eliminando distorções). Além de extrair elementos de interesse de imagens.
    * Visão Computacional: Possui o objetivo de atribuir sentido na visão da máquina, como por exemplo detecção de objetos, reconhecimento de padrões, ...
    * Computação Gráfica: Possui o objetivo na síntese de imagens (modelagem e renderização), ou seja, o mundo 3D dentro de um ambiente computacional.

2. **O que é e por qual motivo utilizar coordenada homogênea para especificar 
transformações geométricas em CG?**    
    Coordenadas homogêneas facilitam a aplicação de transformações geométricas (rotação, escala, translação) através de multiplicações de matrizes, unificando essas operações em uma única fórmula. Elas permitem a composição eficiente de várias transformações e são essenciais para projeções 3D. Isso simplifica a computação gráfica e melhora o desempenho.

3. **Apresente  a  matriz  que  representa  uma  transformação  geométrica 
consistindo de uma translação seguida de uma rotação.**
    Iremos considerar T como a matriz de translação e R como a de rotação. Então a matriz da transformação final ficaria $M = R \cdot T$

    $$
      \begin{bmatrix}
        \cos(\theta) & -\sin(\theta) & \cos(\theta) \cdot x - \sin(\theta) \cdot y \\
        \sin(\theta) & \cos(\theta)  & \sin(\theta) \cdot x + \cos(\theta) \cdot y \\
        0            & 0             & 1
      \end{bmatrix}
    $$

4. **Apresente a matriz que representa uma transformação consistindo de uma 
translação tx=M e ty=D seguida de uma escala uniforme s=2. Qual o impacto 
dessa transformação para objetos definidos em relação à origem e para 
objetos fora da origem?** 

    Iremos ter o seguinte matriz de transformação final $M = S \cdot T$.
    $$
      \begin{bmatrix}
        2 & 0 & 0 \\
        0 & 2 & 0 \\
        0 & 0 & 1 
      \end{bmatrix}

      \cdot 

      \begin{bmatrix}
        1 & 0 & 4 \\
        0 & 1 & 27 \\
        0 & 0 & 1 
      \end{bmatrix}

      =

      \begin{bmatrix}
        2 & 0 & 8 \\
        0 & 2 & 54 \\
        0 & 0 & 1 
      \end{bmatrix}
    $$

     1. Objetos na origem (0, 0):
        * **Escala**: A escala aumenta ou diminui o tamanho do objeto, multiplicando suas coordenadas. Mesmo que o objeto esteja na origem, a escala afeta sua geometria. Se o objeto tem algum comprimento ou volume, será aumentado em um fator de 22 em todas as direções. Para um ponto exato na origem, a escala não teria impacto porque a multiplicação por qualquer fator de ainda resulta em 00.
        * **Translação**: A translação move objetos em uma determinada direção (horizontal e/ou vertical). No entanto, se o objeto estiver na origem (coordenada (0,0)(0,0)), a translação não terá impacto. Isso ocorre porque, ao adicionar 44 unidades no eixo xx e 2727 no eixo yy a um ponto na origem, ele continua na posição (0,0)(0,0) em termos de movimento de sua geometria (o ponto de origem em si permanece no mesmo local).


      2. Objetos fora da origem:
          * **Escala**: Quando um objeto está fora da origem, a escala vai modificar todas as coordenadas do objeto proporcionalmente. Se a escala é 22, isso significa que todas as coordenadas (x,y)(x,y) do objeto serão multiplicadas por 22, dobrando o tamanho do objeto em ambas as direções. Por exemplo, um ponto no espaço com coordenadas (x,y)=(3,5)(x,y)=(3,5) será redimensionado para (6,10)(6,10), ou seja, ficará duas vezes mais distante da origem.
          * **Translação**: Após a escala, a translação será aplicada. Isso desloca o objeto em relação ao seu novo tamanho. Nesse caso, após redimensionar o objeto, ele será movido 44 unidades para a direita no eixo xx e 2727 unidades para cima no eixo yy. Por exemplo, se um objeto estava originalmente em (3,5)(3,5), ele será escalado para (6,10)(6,10) e, em seguida, transladado para (6+4,10+27)=(10,37)(6+4,10+27)=(10,37).
          * 
5. **Verifique se $R(M+D)$ irá obter a mesma matriz de transformação do que $R(M) \cdot R(D)$.**

    $$
    R(31) = 
      \begin{bmatrix}
        cos(31) & -sen(31) & 0 \\
        sen(31) & cos(31) & 0 \\
        0 & 0 & 1 
      \end{bmatrix}
      =
      \begin{bmatrix}
        0.8571673 & -0.51503807 & 0 \\
        0.51503807 & 0.8571673 & 0 \\
        0 & 0 & 1 
      \end{bmatrix}
    $$

    $$
      R(27) * R (4) = 
      \begin{bmatrix}
        cos(27) & -sen(27) & 0 \\
        sen(27) & cos(27) & 0 \\
        0 & 0 & 1 
      \end{bmatrix}
      \cdot
      \begin{bmatrix}
        cos(4) & -sen(4) & 0 \\
        sen(4) & cos(4) & 0 \\
        0 & 0 & 1 
      \end{bmatrix}
          =
      \begin{bmatrix}
        0.8571673 & -0.51503807 & 0 \\
        0.51503807 & 0.8571673 & 0 \\
        0 & 0 & 1 
      \end{bmatrix}
    $$

    Ou seja, são a mesma coisa.

6. **Forneça a matriz de transformação que realiza a transformação abaixo (a 
seta indica o objeto inicial e o final após a transformação). Em seguida, 
apresente as coordenadas do objeto para uma escala uniforme s=M.** 

    ![alt text](./img/image.png)

    A matriz de transformação $M$, seria:
    $$
    M = 
      \begin{bmatrix}
        1 & 0 & 60 \\
        0 & 1 & 80 \\
        0 & 0 & 1 
      \end{bmatrix}
    $$

    As coordenadas após a escala seriam:
      * $(80, 80, 0)$ 
      * $(240, 80, 0)$
      * $(240, 240, 0)$
      * $(80, 240, 0)$

7. **Mostre  que  a  ordem  das  transformações  pode  modificar  a  matriz  de 
transformação resultante (problema da comutatividade). OBS: É suficiente 
fornecer um exemplo.**
    Iremos considerar duas matrizes:
    $$
      S = 
        \begin{bmatrix}
          2 & 0 & 0 \\
          0 & 2 & 0 \\
          0 & 0 & 1 
        \end{bmatrix}
      T = 
        \begin{bmatrix}
          1 & 0 & -1 \\
          0 & 1 & 1 \\
          0 & 0 & 1 
        \end{bmatrix}
    $$
    $$ 
        \begin{bmatrix}
          2 & 0 & 0 \\
          0 & 2 & 0 \\
          0 & 0 & 1 
        \end{bmatrix}

        \cdot

        \begin{bmatrix}
          1 & 0 & -1 \\
          0 & 1 & 1 \\
          0 & 0 & 1 
        \end{bmatrix}

        =
        \begin{bmatrix}
          2 & 0 & -2 \\
          0 & 2 & 2 \\
          0 & 0 & 1 
        \end{bmatrix}

    $$
    $$ 

        \begin{bmatrix}
          1 & 0 & -1 \\
          0 & 1 & 1 \\
          0 & 0 & 1 
        \end{bmatrix}
        \cdot
        \begin{bmatrix}
          2 & 0 & 0 \\
          0 & 2 & 0 \\
          0 & 0 & 1 
        \end{bmatrix}
        =
        \begin{bmatrix}
          2 & 0 & -1 \\
          0 & 2 & 2 \\
          0 & 0 & 1 
        \end{bmatrix}

    $$

    Assim considerando as matrizes $S$ e $T$, temos resutlados diferentes quando fazemos $S \cdot T$ e $T \cdot S$.

8. **As transformações de rotação e escala são comutativas entre si? Leve em 
conta tanto escalas uniformes quanto não uniformes.**
    
    Transformações de rotação e escala uniforme são comutativas; a ordem de aplicação não altera o resultado final. No entanto, transformações de rotação e escala não uniforme não são comutativas; a ordem de aplicação influencia o resultado. A escala uniforme altera apenas a magnitude, enquanto a escala não uniforme modifica as direções dos vetores, afetando a rotação subsequente. Portanto, a ordem de aplicar uma escala não uniforme e uma rotação importa.

9. **As transformações de translação e escala são comutativas entre si? E entre 
translação e rotação?**

    Translação e escala não são comutativas; a ordem de aplicação altera o resultado final. Da mesma forma, translação e rotação também não são comutativas; a ordem influencia o resultado. Isso ocorre porque translação modifica a posição dos pontos, enquanto escala e rotação alteram suas magnitudes e orientações, respectivamente. Portanto, aplicar uma transformação antes da outra resulta em efeitos diferentes.

10. **Forneça a sequência de transformações que leva o triângulo T1 ao triângulo 
T2 e dê a matriz resultante. É suficiente mostrar as matrizes que compõem a 
matriz resultante explicando o que é cada matriz e seus componentes.**
    
    ![alt text](./img/10.png)

    Como visto no execício 8 escala e rotação são comutativas, então não importa a ordem da nossas matrizes: ($c = \cos \theta$ e $s = \cos \theta$)

      $$ 
        \begin{bmatrix}
          c & -s & 0 \\
          s &  c & 0 \\
          0 &  0 & 1 
        \end{bmatrix}
        \cdot
        \begin{bmatrix}
          1 & 0 & x \\
          0 & 1 & y \\
          0 & 0 & 1 
        \end{bmatrix}
        =
        \begin{bmatrix}
          c & -s & cx - sy \\
          s &  c & sx + cy \\
          0 &  0 & 1 
        \end{bmatrix}
      $$

      Agora multiplicando a matriz resultante pelo ponto de origem e destino, teremos as esqueções: $(8, 6) \rightarrow (0, 4)$ e $(5, 2) \rightarrow (4, 1)$
      $$
        \begin{align*}
         0&=8c-6s+cx-sy, \\
         4&=6c+8s+sx+cy, \\
         4&=5c-2c-cx-sy, \\
         1&=2c-5s+sx+cy
        \end{align*}
      $$

      A solução do sistema é:
      $$
        s= 0.091, c=0.4541, x=-6.302, y=2.4676
      $$