# Resumo: Redes Complexas - Conceitos Básicos

## 1. Do Grafo Clássico às Redes Complexas
Historicamente, a teoria dos grafos clássica $G(V,E)$ tem sido usada para codificar relacionamentos entre pares de objetos (vértices e arestas), com foco no uso de algoritmos para encontrar menores caminhos ou estabelecer rotas. 

A teoria de **Redes Complexas** expande essa abstração para lidar com sistemas reais que apresentam características que a teoria dos grafos clássica não abrange totalmente:
* **Escala Elevada:** Lidam com quantidades massivas de dados, podendo atingir milhares ou bilhões de vértices.
* **Topologia Não Trivial:** Apresentam padrões de conectividade complexos.
* **Dinâmica:** São grafos que não são necessariamente estáticos, evoluindo ao longo do tempo.

---

## 2. Conceitos Fundamentais e Estatísticos

Devido à sua escala, a investigação em redes complexas foca-se fortemente em **propriedades estatísticas** (como a resiliência da rede à remoção de nós) em vez de focar apenas em caminhos individuais.

### 2.1. Grau do Vértice
* O grau é o número de arestas conectadas a um vértice. Em redes dirigidas, divide-se em grau de entrada (*in-degree*) e de saída (*out-degree*).
* A soma dos graus de todos os vértices de um grafo não dirigido é igual a $2|E|$ (duas vezes o número de arestas).

### 2.2. Distribuição de Grau $P(d)$
* Define a probabilidade de um vértice selecionado aleatoriamente ter o grau $d$.
* Em redes complexas reais (como o Facebook ou a Web), esta distribuição segue frequentemente uma **Lei de Potência (Power-Law)**. Isso significa que a grande maioria dos vértices tem muito poucas conexões, enquanto um número muito reduzido de vértices (os *hubs*) concentra uma quantidade gigantesca de conexões.

---

## 3. Tipos de Redes Complexas

Os fenômenos modelados por redes complexas são muito diversos e agrupam-se em quatro categorias principais:

### 3.1. Redes Sociais
Modelam as relações humanas, onde cada aresta denota uma relação social.
* **Exemplos:** Redes de amizade (escolas, Facebook), redes de atores, redes de coautoria em artigos científicos, redes de e-mail e contactos sexuais.

### 3.2. Redes de Informação (ou Conhecimento)
Nós armazenam informação e as arestas representam a associação entre essas informações.
* **World Wide Web (WWW):** Rede dirigida conectada por hiperlinks.
* **Redes de Citação:** Redes dirigidas e acíclicas (um artigo só pode citar o que já foi publicado). Apresentam o fenômeno em que os "ricos ficam mais ricos" (*the rich get richer*), ou seja, artigos muito citados tendem a atrair ainda mais citações.
* **Redes de Recomendação:** Frequentemente grafos bipartidos relacionando utilizadores a preferências (compras, gostos).
* **Outros:** Redes P2P (Peer-to-Peer) e redes de palavras.

### 3.3. Redes Tecnológicas
Construídas pelo homem, geralmente para transportar algo (dados, energia, pessoas). Têm a particularidade de serem, na sua maioria, **redes físicas e geolocalizadas**.
* **Exemplos:** Estrutura física da Internet (roteadores e cabos), rede de energia elétrica, malha rodoviária e de transporte público, linhas aéreas e rede telefônica.

### 3.4. Redes Biológicas
Codificam os relacionamentos em sistemas biológicos complexos a várias escalas.
* **Redes Metabólicas:** Convertem entradas em produtos úteis no organismo (frequentemente representadas como redes bipartidas entre reações e metabolitos).
* **Exemplos:** Redes neurais (interações por sinais elétricos no cérebro humano), redes de interação entre proteínas, regulação genética e cadeias alimentares (interação entre espécies).