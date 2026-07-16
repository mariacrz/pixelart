# Pixel Art com K-means e Redução de resolução

Projeto Final da disciplina de **Computação Científica e Análise de Dados**, 
Transforma imagens em *pixel art* combinando **redução de resolução** com **redução de paleta de cores por K-means**.


## Motivação e Modelagem

Transformar uma imagem em pixel art envolve dois problemas diferentes:

1. **Redução da resolução** — dividir a imagem em blocos e substituir cada bloco pela cor média, criando o efeito de "pixel grande".
2. **Quantização de cor** — reduzir a imagem a apenas `k` cores.

O segundo problema é um problema de **clusterização**: cada pixel é um ponto em ℝ³ (R, G, B), e o **K-means** encontra os `k` centros que minimizam a soma dos quadrados das distâncias de cada pixel ao seu centro mais próximo. Isso é um problema clássico de **Reconhecimento de Padrões**, como foi visto no conteúdo da disciplina ao longo do curso.

##  Pipeline

1. Carregamento da imagem
2. Redução da imagem em blocos (média por bloco)
3. Quantização de cores com K-means
4. Escolha de `k` pelo método do cotovelo
5. Comparação visual variando `k`

##  Tecnologias

- Python 3
- NumPy
- Pillow (PIL)
- scikit-learn (KMeans)
- Matplotlib
- Jupyter Notebook / Google Colab

## Estrutura do repositório

```
pixelart/
├── pixelart.ipynb          # notebook principal com todo o pipeline
├── imagens/                # imagens de entrada
├── outputs/                # resultados gerados
├── docs/requirements.txt   # dependências
└── README.md
```

## Como rodar

**Google Colab:**
1. Abrir [colab.research.google.com](https://colab.research.google.com)
2. Fazer upload do `pixelart.ipynb`
3. Rode as células em ordem (`Shift + Enter`)
4. Fazer upload da sua imagem na segunda célula (clicar em 'escolher arquivos')


## Resultados e observações

## Conclusões

- A redução da resolução controla a resolução espacial da pixel art, pois blocos maiores deixam a imagem mais estilizada,
  mas apagam detalhes finos
- O K-means encontra a quantidade de cores como um problema de clusterização em ℝ³,
  minimizando a soma dos quadrados das distâncias de cada pixel ao centro do seu
  cluster
- O método do cotovelo mostrou que o ganho de reduzir o erro cai
  fortemente entre k=1 e k=4, e praticamente fica constante depois disso
- O k=6 foi escolhido como valor final, porque preserva melhor detalhes
  relevantes da imagem que se perderiam com um k
  menor, mesmo que o ganho de k=4 para k=6 já seja pequeno.
- Isso ilustra uma diferença importante entre otimizar um critério matemático
  (erro quadrático) e otimizar a percepção visual humana. O cotovelo é um guia
  quantitativo, mas a escolha final também depende da avaliação da qualidade do
  resultado.

## Referências

- material da disciplina: https://drive.google.com/file/d/1gs_W6fUx4uDV9xDi01Yx8VTbtRz86Lpq/view?usp=sharing
- exemplos de projetos: 

## Autor

Maria Clara Rodrigues Zago
