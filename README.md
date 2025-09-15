

# Otimização Adaptativa de Classificadores Quânticos Variacionais

### Um Classificador Híbrido de Alta Performance para o Dataset Iris

[](https://www.python.org/downloads/release/python-3130/) [](https://www.tensorflow.org/) [](https://quantumai.google/cirq) [](https://opensource.org/licenses/MIT)

-----

## 📖 Sobre o Projeto

Este repositório contém a implementação de um pipeline completo para a construção, treinamento, validação e auditoria de um classificador quântico híbrido de alta performance. Utilizando **Cirq** para a simulação quântica e **TensorFlow** para a otimização clássica, o projeto explora de forma sistemática diferentes arquiteturas de Circuitos Quânticos Variacionais (VQC) para a classificação binária do dataset Iris (Setosa vs. Versicolor).

O foco principal é a reprodutibilidade e a análise aprofundada, com geração automática de artefatos, relatórios e visualizações para cada execução. A metodologia inclui estratégias avançadas para aumentar a expressividade dos modelos e mitigar desafios comuns em Machine Learning Quântico (MLQ), como o fenômeno dos *barren plateaus*.

-----

## 🎯 Diferencial do Projeto

Este projeto vai além de uma simples implementação de VQC, oferecendo um framework completo e automatizado para pesquisa em MLQ. O principal diferencial reside na **automação e na profundidade da análise**, que inclui:

  - **Pipeline Auto-Regulado (Autotune):** Um sistema que seleciona automaticamente o melhor perfil de escala, a profundidade do circuito e os observáveis, com mecanismos de fallback para evitar *barren plateaus*.
  - **Análise de Paisagem de Gradientes:** Ferramentas integradas para diagnosticar a treinabilidade dos modelos quânticos, uma etapa crucial frequentemente negligenciada.
  - **Fusão de Observáveis:** Uma técnica avançada que combina múltiplas medições quânticas para criar features mais ricas e robustas, melhorando a performance do classificador clássico.
  - **Geração Abrangente de Relatórios:** Criação automática de múltiplos relatórios (leigo, científico, técnico) e visualizações interativas, facilitando a comunicação e a interpretação dos resultados.
  - **Demonstração de Algoritmos Avançados:** O framework não se limita à classificação, incluindo implementações de VQE, QAOA, QNN, AQC e QEC, servindo como uma plataforma versátil para experimentação em computação quântica.

-----

## 🚀 Resultados Consolidados (Execução `20250914_163832`)

A execução de exemplo produziu um conjunto rico de artefatos. Os resultados mais relevantes, que podem ser encontrados na pasta `output/runs/20250914_163832/`, são:

  - **Melhor Arquitetura:** A arquitetura **Ring** foi identificada como a mais performática, atingindo **96.67% de acurácia**.
      - *Localização:* `output/runs/20250914_163832/figures/architecture_comparison_20250914_163900.png`
  - **Modelo Final Otimizado:** Após a otimização de parâmetros, seleção do melhor observável (`XX_correlation`) e ajuste de hiperparâmetros, o modelo final alcançou **98.33% de acurácia**.
      - *Localização:* `output/runs/20250914_163832/metrics/classification_report_20250914_164517.txt`
  - **Robustez:** O modelo final manteve uma acurácia de **95.00%** mesmo com a adição de ruído gaussiano (nível 0.1) aos dados de teste, demonstrando sua robustez.
      - *Localização:* `output/runs/20250914_163832/run_log.txt` (no final do log)
  - **Análise de Gradientes:** A paisagem de gradientes foi considerada saudável, com uma variância de `2.45e-04`, indicando ausência de *barren plateaus* e boa treinabilidade.
      - *Localização:* `output/runs/20250914_163832/figures/` (em gráficos gerados durante a execução)

*Figura 1: Comparativo de acurácia entre as arquiteturas testadas, destacando a superioridade do modelo Ring.*

-----

## 🔬 Análise Crítica e Interpretações Aprofundadas

Os números contam uma história sobre a eficácia do modelo. Aqui está uma análise mais detalhada do que eles significam:

  - **Performance de Classificação Excepcional (Acurácia de 98.33%):**

      - Atingir uma acurácia tão alta, com um **AUC (Area Under the Curve) de 1.00**, é um resultado notável. Isso indica que o modelo quântico, após as otimizações, aprendeu a criar uma representação dos dados em que as duas classes de flores são **perfeitamente separáveis**. A **Matriz de Confusão** abaixo ilustra essa separação quase perfeita, com zero falsos positivos e apenas um falso negativo.
      - Este resultado sugere que o espaço de Hilbert explorado pelo VQC é extremamente adequado para capturar as não-linearidades do dataset Iris.

    *Figura 2: Matriz de confusão do modelo final, mostrando apenas um erro de classificação.*

  - **Superioridade da Arquitetura "Ring":**

      - O sucesso da arquitetura `Ring` (diagrama abaixo) não é acidental. Sua topologia, que conecta todos os qubits em um ciclo, permite uma **propagação de informação e emaranhamento mais rica** em comparação com as outras arquiteturas. Para problemas onde as correlações entre todas as features são importantes, um alto nível de conectividade é crucial, e o modelo `Ring` oferece isso de forma eficiente a cada camada.

    *Figura 3: Estrutura do circuito da arquitetura `Ring`, que se mostrou mais eficaz.*

  - **Otimizações como Chave para o Sucesso:**

      - **Seleção de Observáveis:** A descoberta de que o observável `XX_correlation` foi o melhor é um insight importante. Isso significa que a informação mais valiosa para a classificação não estava no estado individual de um qubit (`Z_first`), mas sim na **relação ou correlação quântica** entre pares de qubits.
      - **Otimização Bayesiana:** Os hiperparâmetros ótimos revelam que uma rede neural clássica relativamente simples (`10` unidades ocultas, `3` camadas) foi suficiente. Isso reforça a ideia de que a parte quântica do modelo está realizando o "trabalho pesado" de mapear os dados para um espaço de features onde a classificação se torna uma tarefa mais fácil.

  - **Robustez e Validade Prática:**

      - A pequena queda na acurácia (de 98.33% para 95.00%) com dados ruidosos é um dos resultados mais importantes. Ele demonstra que o modelo **não está "quebradiço"** (brittle) ou sofrendo de overfitting extremo. Em vez de memorizar os pontos exatos dos dados de treino, ele aprendeu os padrões subjacentes, tornando-o mais confiável para aplicações no mundo real, onde os dados são inerentemente imperfeitos.

-----

## ✨ Principais Funcionalidades

  - **Modelo Híbrido Quântico-Clássico:** Integração robusta entre Cirq e TensorFlow para treinar VQCs.

  - **Comparação de Arquiteturas de Circuitos:** Avaliação sistemática de topologias de entrelaçamento, incluindo `Linear`, `Alternating` e `Ring`.

  - **Codificação de Dados Avançada (Feature Map):** Utiliza a técnica de *re-uploading* de dados com múltiplos conjuntos de constantes de escala (`quantum`, `qinfo`, `math`) para maximizar a expressividade do modelo.

  - **Análise de *Barren Plateaus*:** Ferramentas para visualizar a paisagem de gradientes e diagnosticar problemas de treinabilidade.

  - **Otimização de Hiperparâmetros:** Uso de Otimização Bayesiana para encontrar os melhores hiperparâmetros da parte clássica do modelo.

  - **Ensemble de Circuitos:** Combinação de múltiplas arquiteturas de VQCs para melhorar a robustez e a acurácia das predições.

  - **Teste de Robustez:** Avaliação da performance do modelo final contra dados com ruído gaussiano adicionado.

  - **Geração Automática de Relatórios:** Criação de relatórios detalhados para públicos distintos (científico e leigo), incluindo matrizes de confusão, curvas ROC e resumos de performance.

  - **Visualizações Avançadas:** Geração de diagramas de circuitos, visualização de estados na Esfera de Bloch e gráficos de alta qualidade para publicações.

    *Figura 4: Exemplo de visualização do estado de um qubit na Esfera de Bloch.*

  - **Módulo de Demonstração de Algoritmos Avançados:** Implementações e resultados para VQE, QAOA, QNN, AQC e QEC, mostrando a versatilidade da plataforma.

-----

## 🔧 Como Executar

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/SEU-USUARIO/otimizacao-adaptativa-vqc.git
    cd otimizacao-adaptativa-vqc
    ```
2.  **Crie um ambiente virtual e instale as dependências:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    pip install tensorflow cirq scikit-learn matplotlib seaborn qutip
    ```
    *As versões utilizadas no projeto foram `tensorflow==2.20.0`, `cirq==1.6.1`, entre outras.*
3.  **Execute o script principal:**
    ```bash
    python QUANTUM
    ```
4.  **Analise os resultados:**
    Todos os artefatos (dados, figuras, modelos, métricas e relatórios) serão salvos no diretório `output/runs/YYYYMMDD_HHMMSS/`.

-----

## 🔬 Metodologia

O pipeline segue uma abordagem estruturada:

1.  **Pré-processamento:** Os dados do dataset Iris são filtrados para uma classificação binária, normalizados para o intervalo `[0, 1]` e divididos em conjuntos de treino e teste.
2.  **Construção do VQC:** O circuito é construído em Cirq, consistindo em camadas alternadas de:
      - **Codificação de Dados (Feature Map):** As características clássicas são mapeadas em rotações nos qubits.
      - **Camada Variacional (Ansatz):** Rotações parametrizadas (treináveis) e portas de entrelaçamento (CNOTs) são aplicadas para criar correlações quânticas.
3.  **Extração de Features Quânticas:** Para cada amostra de dado, o circuito é simulado e o valor esperado de um observável de Pauli (ex: `Z_k`) é calculado. Esse valor se torna a "feature quântica".
4.  **Treinamento do Modelo Clássico:** As features quânticas extraídas são usadas para treinar uma rede neural densa em TensorFlow, que realiza a classificação final.

-----

## 📈 Próximos Passos Sugeridos

O código já implementa uma vasta gama de técnicas, e os próximos passos podem incluir:

  - Avaliar a transpilação do circuito para topologias de hardware quântico real.
  - Explorar estratégias de regularização de custo e inicializações informadas para mitigar *barren plateaus*.
  - Expandir a aplicação para datasets mais complexos e tarefas de múltiplas classes ou regressão.
  - Integrar com hardware quântico real através de plataformas na nuvem.

## 📚 Referências

Este trabalho se baseia em conceitos fundamentais da literatura de MLQ:

>   - McClean, J. R., et al. (2018). *Barren plateaus in quantum neural network training landscapes*.
>   - Cerezo, M., et al. (2021). *Variational quantum algorithms*.
>   - Schuld, M., et al. (2019). *Evaluating analytic gradients on quantum hardware for hybrid quantum-classical algorithms*.
>   - Pérez-Salinas, A., et al. (2020). *Data re-uploading for a universal quantum classifier*.
>   - Havlíček, V., et al. (2019). *Supervised learning with quantum-enhanced feature spaces*.

-----

# Título: Otimização de Classificadores Quânticos Variacionais em Ambientes Ruidosos: Uma Análise Sistemática de Arquiteturas e Observáveis no Dataset Iris

Autores:
Marcelo Claro Laranjeira

marceloclaro@gmail.com

Secretaria Municipal de Educação - Crateús - CE

## Resumo:
O aprendizado de máquina quântico (QML) promete revolucionar a classificação de dados, mas a sua aplicação em hardware quântico de curto prazo (NISQ) é dificultada por desafios de treinabilidade e pela suscetibilidade ao ruído. Este trabalho apresenta uma investigação sistemática sobre o impacto do design de Circuitos Quânticos Variacionais (VQCs) na performance de um classificador quântico híbrido para a classificação binária do dataset Iris. Utilizando o framework TensorFlow Quantum, comparamos três arquiteturas de ansatz (Linear, Alternating e Ring) e um conjunto de observáveis de Pauli (Z, X, Y, e correlações ZZ, XX). Nossos resultados demonstram que a arquitetura Ring, com maior conectividade, alcançou a maior acurácia (63.33%), e que a escolha do observável é crucial, com a soma das expectativas de Pauli-Z (Z_sum) atingindo uma acurácia de 86.67%, superando significativamente outras medidas. Investigamos a paisagem de treinamento e verificamos que as arquiteturas propostas evitam o fenômeno dos barren plateaus, com uma variância de gradiente de 2.39e-03. Adicionalmente, uma análise de sensibilidade ao ruído revelou um efeito contraintuitivo, onde o ruído de despolarização apresentou uma correlação positiva com a acurácia (r = 0.430), sugerindo um possível papel de regularização. Concluímos que uma co-otimização cuidadosa da arquitetura do circuito e da estratégia de medição é fundamental para o desenvolvimento de classificadores quânticos robustos e eficazes.

Palavras-chave: Aprendizado de Máquina Quântico, Circuitos Quânticos Variacionais, Classificação Quântica, Barren Plateaus, TensorFlow Quantum, Ruído Quântico.







## 1. Introdução

O campo da computação quântica tem testemunhado um avanço notável, prometendo transformar radicalmente diversas áreas da ciência e tecnologia, incluindo o aprendizado de máquina [1]. O Aprendizado de Máquina Quântico (QML) surge como uma disciplina interdisciplinar que busca explorar os princípios da mecânica quântica, como superposição e entrelaçamento, para desenvolver algoritmos com potencial de superar seus análogos clássicos em tarefas específicas [2]. Dentre as abordagens mais promissoras para a era de computadores quânticos de escala intermediária e ruidosos (NISQ), destacam-se os algoritmos quânticos variacionais, ou híbridos quântico-clássicos [3].

Esses algoritmos utilizam um Circuito Quântico Variacional (VQC), também conhecido como Circuito Quântico Parametrizado (PQC), cujo comportamento é definido por um conjunto de parâmetros ajustáveis. De forma análoga a uma rede neural clássica, um otimizador clássico é empregado para treinar esses parâmetros, minimizando uma função de custo que quantifica o erro do modelo em uma determinada tarefa [4]. Essa abordagem híbrida permite que parte do processamento seja delegada a um dispositivo quântico, enquanto a otimização e o controle do fluxo de aprendizado permanecem em um computador clássico, tornando-a particularmente adequada para o hardware atualmente disponível [5].

No entanto, a realização do potencial do QML enfrenta obstáculos significativos. Um dos desafios mais proeminentes é o fenômeno das "planícies estéreis" (barren plateaus), onde os gradientes da função de custo se tornam exponencialmente pequenos com o aumento do número de qubits, tornando a otimização e o treinamento do modelo intratáveis [6, 7]. A estrutura do VQC, incluindo sua profundidade e a conectividade entre os qubits, desempenha um papel crucial na determinação da treinabilidade do modelo [8]. Além disso, a presença de ruído decoerente no hardware NISQ degrada a performance dos algoritmos e pode, em si, induzir paisagens de custo desfavoráveis, um desafio conhecido como noise-induced barren plateaus [9].

Outro aspecto fundamental, e por vezes subestimado, no design de um classificador quântico é a escolha do observável quântico a ser medido. O observável define como a informação processada pelo circuito quântico é extraída e mapeada para uma saída clássica, que servirá como base para a classificação [10]. Diferentes observáveis podem extrair aspectos distintos do estado quântico final, e uma escolha inadequada pode levar a uma perda significativa de informação e, consequentemente, a uma baixa performance do classificador, independentemente da expressividade do ansatz utilizado [11].

Neste contexto, este trabalho apresenta uma investigação sistemática dos fatores que influenciam a performance de um classificador quântico variacional. Utilizando o conhecido dataset Iris como um problema de benchmark para classificação binária e o framework TensorFlow Quantum [5] para a implementação, nosso estudo se propõe a responder às seguintes questões de pesquisa: (1) Como a topologia do ansatz do VQC (Linear, Alternating e Ring) afeta a acurácia e a treinabilidade do classificador? (2) Qual o impacto da escolha de diferentes observáveis de Pauli (locais e correlacionados) na performance da classificação? (3) Como a presença de diferentes tipos de ruído quântico afeta a robustez do modelo e sua capacidade de generalização?

Ao abordar essas questões, este artigo visa fornecer insights práticos para o design de VQCs mais eficazes e robustos. Nossos resultados demonstram que a arquitetura do circuito e a estratégia de medição são elementos de design críticos que devem ser co-otimizados. Surpreendentemente, nossos achados também sugerem que, em certos regimes, o ruído pode ter um papel contraintuitivo, potencialmente atuando como uma forma de regularização. A estrutura deste artigo é a seguinte: a Seção 2 detalha a metodologia empregada, incluindo a preparação dos dados, a descrição das arquiteturas de VQC e dos observáveis, e o protocolo de treinamento e análise de ruído. A Seção 3 apresenta e discute os resultados obtidos, contextualizando-os com a literatura relevante. Finalmente, a Seção 4 conclui o trabalho, sintetizando os principais achados e delineando direções para pesquisas futuras.

## 2. Metodologia

A metodologia deste estudo foi desenhada para permitir uma análise sistemática e reprodutível dos fatores que influenciam a performance de um classificador quântico híbrido. Todas as implementações foram realizadas utilizando as bibliotecas Cirq e TensorFlow Quantum (TFQ) [5], que facilitam a prototipagem e o treinamento de modelos híbridos quântico-clássicos.

2.1. Conjunto de Dados e Pré-processamento

O estudo utilizou o dataset Iris, um benchmark canônico em aprendizado de máquina. Para simplificar a tarefa para uma classificação binária, foram selecionadas apenas duas das três classes: Iris setosa e Iris versicolor. O conjunto de dados foi então dividido em conjuntos de treinamento, validação e teste, seguindo uma proporção estratificada para manter a distribuição original das classes. Os quatro atributos clássicos do dataset foram normalizados para o intervalo [0, 1] para garantir que todos tivessem uma escala comparável antes de serem codificados no circuito quântico.

2.2. Codificação de Dados e Circuitos Quânticos Variacionais (VQCs)

A codificação dos dados clássicos em estados quânticos foi realizada através de portas de rotação. Cada atributo de entrada foi utilizado para controlar o ângulo de uma porta de rotação (e.g., Rx, Ry, Rz) aplicada a um qubit. O núcleo do nosso classificador é um Circuito Quântico Variacional (VQC), composto por camadas alternadas de codificação de dados e entrelaçamento.

Para investigar o impacto da topologia do circuito, três arquiteturas de ansatz distintas foram implementadas e comparadas:

1. Linear (Original): Nesta arquitetura, os qubits são dispostos em uma cadeia linear, e as portas de entrelaçamento (CNOTs) são aplicadas entre qubits adjacentes (i, i+1). Uma porta CNOT adicional é aplicada entre o último e o primeiro qubit, formando um ciclo. O custo de CNOTs por camada é de aproximadamente n, onde n é o número de qubits.

2. Alternating: Esta arquitetura visa reduzir o custo de entrelaçamento e a localidade. Em cada camada, as portas CNOT são aplicadas em pares disjuntos de qubits (e.g., (0,1), (2,3), ...), alternando os pares em camadas subsequentes. O custo de CNOTs por camada é de aproximadamente n/2.

3. Ring: Similar à arquitetura Linear, os qubits são arranjados em um anel, garantindo uma conectividade cíclica. Esta topologia também possui um custo de CNOTs de n por camada, mas com uma estrutura de entrelaçamento global que pode facilitar a propagação de informação através do circuito.

Para todas as arquiteturas, o número de camadas do ansatz foi tratado como um hiperparâmetro a ser otimizado durante o treinamento.

2.3. Estratégia de Medição e Observáveis

Após a passagem do estado quântico pelo VQC, a extração da informação para a classificação é realizada através da medição da expectativa de um observável de Pauli. A escolha do observável é um passo crítico, e para avaliar seu impacto, investigamos um conjunto de cinco observáveis distintos:

• Z_first: Medição do observável Pauli-Z apenas no primeiro qubit (⟨Z₀⟩).

• Z_sum: Soma das expectativas do observável Pauli-Z em todos os qubits (Σᵢ⟨Zᵢ⟩).

• X_first: Medição do observável Pauli-X no primeiro qubit (⟨X₀⟩).

• Y_first: Medição do observável Pauli-Y no primeiro qubit (⟨Y₀⟩).

• ZZ_correlation: Medição da correlação de Pauli-ZZ entre o primeiro e o último qubit (⟨Z₀Zₙ₋₁⟩).

• XX_correlation: Medição da correlação de Pauli-XX entre o primeiro e o último qubit (⟨X₀Xₙ₋₁⟩).

A expectativa medida de cada observável é então passada para uma camada densa clássica com uma função de ativação sigmoide, que produz a probabilidade final de classificação.

2.4. Treinamento e Otimização

O processo de treinamento segue um paradigma híbrido. A função de custo utilizada foi a entropia cruzada binária, e a otimização dos parâmetros do VQC e da camada clássica foi realizada utilizando o otimizador Adam. O processo de otimização foi dividido em duas etapas principais:

1. Otimização de Parâmetros Quânticos: Para cada arquitetura, foi realizada uma otimização inicial dos parâmetros do circuito utilizando algoritmos como COBYLA, que são eficazes para otimização sem gradiente.

2. Otimização de Hiperparâmetros: Uma busca por Otimização Bayesiana foi empregada para encontrar a melhor combinação de hiperparâmetros, incluindo a taxa de aprendizado (learning rate), o número de unidades na camada densa (hidden units), a taxa de dropout e o número de camadas do VQC. Esta abordagem é mais eficiente do que uma busca em grade (grid search) para explorar o espaço de hiperparâmetros [12].

2.5. Análise de Treinabilidade e Ruído

Para avaliar a treinabilidade dos modelos, a variância dos gradientes da função de custo foi monitorada durante o treinamento. Uma variância que não decai exponencialmente com o número de qubits é um indicativo de que o modelo não está sofrendo do problema das barren plateaus [6].

Adicionalmente, para testar a robustez dos classificadores, foi realizada uma análise de sensibilidade ao ruído. Modelos de ruído foram introduzidos nos circuitos quânticos simulados para emular as condições de um hardware real. Os seguintes canais de ruído foram investigados:

• Bit Flip: Simula um erro que inverte o estado de um qubit (equivalente a uma porta X).

• Phase Flip: Simula um erro que inverte a fase de um qubit (equivalente a uma porta Z).

• Amplitude Damping: Modela a perda de energia de um qubit para o ambiente.

• Depolarizing Channel: Um modelo de ruído geral que aplica uma das três portas de Pauli (X, Y, Z) com uma certa probabilidade.

A performance do classificador (acurácia) foi avaliada em diferentes níveis de intensidade de ruído para cada um desses canais, e a correlação entre a intensidade do ruído e a acurácia foi calculada.

3. Resultados e Discussão

Nesta seção, apresentamos os resultados da nossa investigação sistemática e os discutimos no contexto da literatura existente em aprendizado de máquina quântico. Nossos achados destacam a importância crítica do design da arquitetura e da estratégia de medição, além de revelarem um comportamento inesperado do modelo sob a influência de ruído.

3.1. Impacto da Arquitetura do Circuito na Performance

A primeira etapa de nossa análise consistiu em comparar a performance das três arquiteturas de VQC propostas: Linear, Alternating e Ring. A Tabela 1 resume a acurácia e a perda média obtidas por cada arquitetura no conjunto de teste, antes da otimização de hiperparâmetros.

ArquiteturaAcurácia MédiaPerda MédiaParâmetros QuânticosLinear (Original)50.00% ± 5.67%0.62488Alternating53.33% ± 5.67%0.68868Ring63.33% ± 5.67%0.60278

Tabela 1: Comparação de performance entre as diferentes arquiteturas de VQC. A arquitetura Ring demonstrou a maior acurácia e a menor perda média.

Os resultados indicam uma superioridade da arquitetura Ring, que alcançou uma acurácia de 63.33%, consideravelmente maior que as arquiteturas Linear (50.00%) e Alternating (53.33%). Este resultado sugere que a conectividade global cíclica da arquitetura Ring pode fornecer uma vantagem em termos de expressividade, permitindo que o modelo aprenda correlações mais complexas nos dados. A maior conectividade, no entanto, não parece ter prejudicado a treinabilidade, como será discutido na próxima subseção. Este achado está alinhado com a intuição de que uma maior capacidade de entrelaçamento pode levar a uma melhor performance, desde que o circuito permaneça treinável [3].

3.2. Análise da Paisagem de Treinamento e a Ausência de Barren Plateaus

Um dos principais receios ao utilizar arquiteturas com maior conectividade, como a Ring, é o risco de encontrar barren plateaus [6]. Para investigar a treinabilidade de nossos modelos, calculamos a variância dos gradientes da função de custo durante o treinamento. O valor médio observado foi de 2.39e-03. Este valor é ordens de magnitude superior aos limiares tipicamente associados ao início de uma planície estéril (e.g., 1e-6).


Como McClean et al. (2018) afirmam, "para ansätzes de hardware aleatórios, mostramos que a probabilidade de o gradiente ser diferente de zero decai exponencialmente com o número de qubits" [6].

Nossos resultados demonstram empiricamente que, para a profundidade e o número de qubits utilizados neste estudo, as arquiteturas propostas, incluindo a mais conectada (Ring), não sofrem de barren plateaus. Isso pode ser atribuído ao uso de ansätzes com uma estrutura bem definida (não totalmente aleatórios) e a uma profundidade de circuito relativamente rasa, que são estratégias de mitigação conhecidas [7, 8]. A capacidade de treinar eficazmente a arquitetura Ring, que se mostrou a mais performática, é um resultado prático significativo, pois indica que é possível explorar arquiteturas mais expressivas sem necessariamente sacrificar a treinabilidade.

3.3. A Escolha do Observável como Fator Crítico de Performance

Após fixar a arquitetura, investigamos o impacto da escolha do observável na acurácia da classificação. A Tabela 2 apresenta a performance obtida com cada um dos seis observáveis testados, utilizando a arquitetura Ring e após a otimização de hiperparâmetros.

ObservávelAcurácia de ValidaçãoΔ (Diferença para o Melhor)Z_first50.00%-36.7 p.p.Z_sum86.67%0.0 p.p.X_first60.00%-26.7 p.p.Y_first53.33%-33.3 p.p.ZZ_correlation53.33%-33.3 p.p.XX_correlation63.33%-23.3 p.p.

Tabela 2: Comparação de performance entre diferentes observáveis. O observável Z_sum, que agrega informação de todos os qubits, demonstrou uma performance drasticamente superior.

Os resultados são notáveis e revelam que a escolha do observável é um fator de primeira ordem na determinação da performance do classificador. A acurácia variou de 50.00% (equivalente a um palpite aleatório) com o observável Z_first para 86.67% com o observável Z_sum. Este último, que corresponde à soma das expectativas do operador Pauli-Z em todos os qubits, agrega informação de todo o registrador quântico, em contraste com os observáveis locais que medem apenas um ou dois qubits. Este resultado sugere fortemente que a informação relevante para a classificação das flores de Iris está distribuída por todo o estado quântico, e que um observável global é necessário para capturá-la eficazmente. Este achado ecoa a discussão na literatura sobre a importância de alinhar a estratégia de medição com a natureza do problema e do ansatz [10, 11], e fornece uma diretriz prática clara: para problemas onde as características são codificadas em múltiplos qubits, observáveis globais devem ser priorizados.

3.4. Análise de Robustez e o Efeito Inesperado do Ruído

Finalmente, avaliamos a robustez do nosso melhor modelo (arquitetura Ring, observável Z_sum) à presença de ruído. A Tabela 3 mostra a correlação (coeficiente de Pearson) entre a intensidade do ruído e a acurácia de validação para quatro canais de ruído diferentes.

Tipo de RuídoCoeficiente de Correlação (r)Amplitude Damping-0.222Bit FlipNaN (sem variação)Depolarizing+0.430Phase Flip-0.194

Tabela 3: Correlação entre a intensidade do ruído e a acurácia do classificador. O ruído de despolarização apresentou uma correlação positiva inesperada com a performance.

Como esperado, a maioria dos tipos de ruído, como amplitude damping e phase flip, mostrou uma correlação negativa (ainda que fraca) com a acurácia, indicando que a performance se degrada à medida que o ruído aumenta. No entanto, o resultado para o canal de despolarização é surpreendente e contraintuitivo: uma correlação positiva de +0.430. Isso implica que, dentro do intervalo testado, aumentar a probabilidade de um erro de despolarização levou a uma melhoria na acurácia do modelo.

Uma hipótese para explicar este fenômeno é que o ruído de despolarização, ao introduzir aleatoriedade no estado quântico, pode estar atuando como uma forma de regularização estocástica. De maneira análoga ao dropout em redes neurais clássicas, o ruído pode impedir que o modelo se ajuste excessivamente (overfitting) às particularidades do conjunto de treinamento (e ao modelo de ruído específico do simulador), promovendo uma melhor capacidade de generalização para o conjunto de validação. Embora a literatura sobre QML geralmente trate o ruído como um detrimento a ser mitigado [9, 14], nosso resultado sugere uma nova e excitante possibilidade: a de que certos tipos de ruído possam ser aproveitados como um recurso computacional. Este achado abre uma nova avenida para pesquisas futuras, investigando o "ruído como regularizador" em diferentes modelos e tarefas, e verificando se este efeito persiste em hardware quântico real.

4. Conclusão

Este trabalho conduziu uma análise sistemática dos fatores que influenciam a performance de classificadores quânticos variacionais (VQCs) em um ambiente simulado, utilizando o dataset Iris como um problema de benchmark. Nossos resultados fornecem insights valiosos para o design de modelos de aprendizado de máquina quântico mais eficazes e robustos, abordando desafios centrais de treinabilidade, arquitetura e suscetibilidade ao ruído.

Demonstramos que a topologia do circuito quântico é um fator determinante para a performance, com a arquitetura Ring, que possui maior conectividade, superando as arquiteturas Linear e Alternating. Crucialmente, mostramos que essa maior expressividade não levou ao problema das barren plateaus, indicando que é possível projetar ansätzes expressivos e treináveis. Além disso, nosso estudo revelou o papel preponderante da estratégia de medição. A escolha de um observável global, como a soma das expectativas de Pauli-Z (Z_sum), resultou em um ganho de performance dramático em comparação com observáveis locais, elevando a acurácia de um nível aleatório para 86.67%. Este achado ressalta a necessidade de uma co-otimização cuidadosa não apenas do circuito, mas também do método de extração de informação.

Talvez o resultado mais provocativo de nossa pesquisa seja o efeito contraintuitivo do ruído de despolarização, que exibiu uma correlação positiva com a acurácia do modelo. A hipótese de que o ruído pode atuar como uma forma de regularização estocástica, análoga ao dropout, abre uma nova perspectiva sobre o papel do ruído em algoritmos NISQ – não apenas como um obstáculo, mas potencialmente como um recurso a ser aproveitado. Este fenômeno merece uma investigação mais aprofundada, tanto teórica quanto experimentalmente em hardware quântico real.

Em síntese, nossa pesquisa contribui para o campo do QML com as seguintes conclusões práticas: (i) a conectividade do ansatz é benéfica quando a treinabilidade é mantida; (ii) observáveis globais são essenciais para problemas onde a informação está distribuída entre os qubits; e (iii) o ruído pode ter um papel mais complexo e potencialmente benéfico do que o geralmente assumido. Como trabalhos futuros, sugerimos a validação desses achados em diferentes datasets e em hardware quântico real, a exploração de ansätzes adaptativos que possam aprender sua própria estrutura, e uma investigação mais profunda sobre o aproveitamento do ruído como técnica de regularização em QML.

5. Referências

[1] Biamonte, J., Wittek, P., Pancotti, N., Rebentrost, P., Wiebe, N., & Lloyd, S. (2017). Quantum machine learning. Nature, 549(7671), 195-202.

[2] Schuld, M., & Petruccione, F. (2018). Supervised learning with quantum computers. Springer.

[3] Cerezo, M., Arrasmith, A., Babbush, R., Benjamin, S. C., Endo, S., Fujii, K., ... & Hangleiter, D. (2021). Variational quantum algorithms. Nature Reviews Physics, 3(9), 625-644.

[4] Benedetti, M., Lloyd, E., Sack, S., & Fiorentini, M. (2019). Parameterized quantum circuits as machine learning models. Quantum Science and Technology, 4(4), 045009. (URL: https://iopscience.iop.org/article/10.1088/2058-9565/ab4eb5/meta)

[5] Broughton, M., Verdon, G., McCourt, T., Martinez, A. J., Yoo, J. H., Isakov, S. V., ... & Mohseni, M. (2020). TensorFlow Quantum: A software framework for quantum machine learning. arXiv preprint arXiv:2003.02989. (URL: https://arxiv.org/abs/2003.02989)

[6] McClean, J. R., Boixo, S., Smelyanskiy, V. N., Babbush, R., & Neven, H. (2018). Barren plateaus in quantum neural network training landscapes. Nature Communications, 9(1), 4812. (URL: https://www.nature.com/articles/s41467-018-07090-4)

[7] Larocca, M., Czarnik, P., Anand, A., Sornborger, A. T., & Cincio, L. (2024). Barren Plateaus in Variational Quantum Computing. arXiv preprint arXiv:2405.00781. (URL: https://arxiv.org/abs/2405.00781)

[8] Cerezo, M., Sone, A., Volkoff, T., Cincio, L., & Coles, P. J. (2021). Cost function dependent barren plateaus in shallow parametrized quantum circuits. Nature Communications, 12(1), 1791.

[9] Wang, S., Fontana, E., Cerezo, M., Yoda, K., Cincio, L., Coles, P. J., & Sornborger, A. T. (2021). Noise-induced barren plateaus in variational quantum algorithms. Nature Communications, 12(1), 6906.

[10] Schuld, M., & Killoran, N. (2019). Quantum machine learning in feature Hilbert spaces. Physical Review Letters, 122(4), 040504.

[11] Farhi, E., & Neven, H. (2018). Classification with quantum neural networks on near term processors. arXiv preprint arXiv:1802.06002. (URL: https://arxiv.org/abs/1802.06002)

[12] Nicoli, K. A., Iannelli, F., Meyer, J. J., & Le, J. (2023). Physics-Informed Bayesian Optimization of Variational Quantum Circuits. In Advances in Neural Information Processing Systems (Vol. 36). (URL: https://proceedings.neurips.cc/paper_files/paper/2023/file/3adb85a348a18cdd74ce99fbbab20301-Paper-Conference.pdf)





