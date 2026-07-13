# 🍉 Pixel Art via K-means e SVD

Projeto da disciplina de **Computação Científica e Análise de Dados**, que transforma imagens em *pixel art* combinando **redução de resolução (downsampling)** com **redução de paleta de cores via K-means**, e compara o resultado com uma abordagem alternativa de compressão via **SVD (Decomposição em Valores Singulares)**.

![preview](assets/preview/comparacao.png)

## 📖 Motivação e Modelagem

Transformar uma imagem em pixel art envolve dois problemas distintos:

1. **Downsampling** — dividir a imagem em blocos e substituir cada bloco pela cor média, criando o efeito de "pixel grande".
2. **Quantização de cor** — reduzir a imagem a apenas `k` cores.

O segundo problema é um problema de **clusterização**: cada pixel é um ponto em ℝ³ (canais R, G, B), e o **K-means** encontra os `k` centros que minimizam a soma dos quadrados das distâncias de cada pixel ao seu centro mais próximo — um problema clássico de **Reconhecimento de Padrões**, como descrito na Seção 2.7.6.2 do CoCADa.

Como comparação, também implementamos uma **compressão por SVD**, aplicada canal a canal (R, G, B), aproximando a imagem por uma matriz de posto baixo. Isso permite discutir duas filosofias diferentes de redução de dados na mesma imagem:

| | K-means | SVD |
|---|---|---|
| O que reduz | Variedade de **cor** | Variedade **espacial/estrutural** |
| Resultado visual | Blocos sólidos (posterização) | Suavização/borrão |
| Resolução espacial | Reduzida (via downsampling) | Mantida |
| Critério de escolha do parâmetro | Método do cotovelo (inércia) | Queda dos valores singulares |

## 🚀 Pipeline

1. Carregamento da imagem
2. Downsampling em blocos (média por bloco)
3. Quantização de cores via K-means
4. Escolha de `k` pelo método do cotovelo
5. Comparação visual variando `k`
6. Bônus: compressão via SVD e comparação com o K-means

## 🛠️ Tecnologias

- Python 3
- NumPy
- Pillow (PIL)
- scikit-learn (KMeans)
- Matplotlib
- Jupyter Notebook / Google Colab

## 📂 Estrutura do repositório

```
pixelart/
├── pixelart.ipynb          # notebook principal com todo o pipeline
├── imagens/                # imagens de entrada
├── outputs/                # resultados gerados
├── assets/preview/         # imagens usadas neste README
├── docs/requirements.txt   # dependências
└── README.md
```

## ▶️ Como rodar

**Opção 1 — Google Colab (recomendado):**
1. Abra [colab.research.google.com](https://colab.research.google.com)
2. Faça upload do `pixelart.ipynb`
3. Faça upload da sua imagem de teste na barra lateral (ícone de pasta)
4. Rode as células em ordem (`Shift + Enter`)

**Opção 2 — Local (VSCode/Jupyter):**
```bash
git clone <url-do-seu-repositorio>
cd pixelart
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r docs/requirements.txt
jupyter notebook pixelart.ipynb
```

## 🔎 Resultados e observações

- O método do cotovelo indicou `k` entre 3 e 4 como ponto de menor ganho marginal, mas `k=6` foi escolhido como melhor equilíbrio entre simplicidade e fidelidade visual (preserva as sementes da melancia).
- A compressão por SVD em postos baixos (1, 3, 5) apresenta franjas cromáticas nas bordas, resultado de aplicar a decomposição independentemente em cada canal RGB — um artefato interessante para discussão técnica.
- K-means e SVD reduzem redundâncias em "eixos" diferentes da imagem: cor vs. estrutura espacial.

## 📚 Referências

- CoCADa — material da disciplina (Seções sobre K-means e SVD)
- [Repositório de exemplo: Eigenfaces (Milton Salgado)](https://github.com/milton-salgado/eigenfaces)

## ✍️ Autor

_seu nome aqui_
