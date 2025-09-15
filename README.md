# Otimização Adaptativa de Classificadores Quânticos Variacionais

### Um Classificador Híbrido de Alta Performance para o Dataset Iris

[](https://www.python.org/downloads/release/python-3130/)
[](https://www.tensorflow.org/)
[](https://quantumai.google/cirq)
[](https://opensource.org/licenses/MIT)

## 📖 Sobre o Projeto

[cite\_start]Este repositório contém a implementação de um pipeline completo para a construção, treinamento, validação e auditoria de um classificador quântico híbrido de alta performance[cite: 5]. [cite\_start]Utilizando **Cirq** para a simulação quântica e **TensorFlow** para a otimização clássica [cite: 82][cite\_start], o projeto explora de forma sistemática diferentes arquiteturas de Circuitos Quânticos Variacionais (VQC) para a classificação binária do dataset Iris (Setosa vs. Versicolor)[cite: 5].

[cite\_start]O foco principal é a reprodutibilidade e a análise aprofundada, com geração automática de artefatos [cite: 6, 45][cite\_start], relatórios e visualizações para cada execução[cite: 131]. [cite\_start]A metodologia inclui estratégias avançadas para aumentar a expressividade dos modelos e mitigar desafios comuns em Machine Learning Quântico (MLQ), como o fenômeno dos *barren plateaus*[cite: 6, 11].

-----

## ✨ Principais Funcionalidades

  - [cite\_start]**Modelo Híbrido Quântico-Clássico:** Integração robusta entre Cirq e TensorFlow para treinar VQCs[cite: 82, 128].
  - [cite\_start]**Comparação de Arquiteturas de Circuitos:** Avaliação sistemática de topologias de entrelaçamento, incluindo `Linear`, `Alternating` e `Ring`[cite: 19, 22, 24, 430].
  - [cite\_start]**Codificação de Dados Avançada (Feature Map):** Utiliza a técnica de *re-uploading* de dados com múltiplos conjuntos de constantes de escala (`quantum`, `qinfo`, `math`) para maximizar a expressividade do modelo[cite: 284, 293, 303].
  - [cite\_start]**Análise de *Barren Plateaus*:** Ferramentas para visualizar a paisagem de gradientes e diagnosticar problemas de treinabilidade[cite: 11, 452, 103].
  - [cite\_start]**Otimização de Hiperparâmetros:** Uso de Otimização Bayesiana para encontrar os melhores hiperparâmetros da parte clássica do modelo[cite: 31, 466].
  - [cite\_start]**Ensemble de Circuitos:** Combinação de múltiplas arquiteturas de VQCs para melhorar a robustez e a acurácia das predições[cite: 459, 869, 103].
  - [cite\_start]**Teste de Robustez:** Avaliação da performance do modelo final contra dados com ruído gaussiano adicionado[cite: 863, 103].
  - [cite\_start]**Geração Automática de Relatórios:** Criação de relatórios detalhados para públicos distintos (científico e leigo), incluindo matrizes de confusão, curvas ROC e resumos de performance[cite: 102, 181, 195, 482].
  - [cite\_start]**Visualizações Avançadas:** Geração de diagramas de circuitos, visualização de estados na Esfera de Bloch e gráficos de alta qualidade para publicações[cite: 34, 35, 389].
  - [cite\_start]**Módulo de Demonstração de Algoritmos Avançados:** Implementações e resultados para VQE, QAOA, QNN, AQC e QEC, mostrando a versatilidade da plataforma[cite: 668, 871, 104].

-----

## 🚀 Resultados de Exemplo (Execução `20250914_163832`)

Os artefatos fornecidos correspondem a uma execução completa do pipeline. Abaixo estão os principais resultados consolidados.

#### **Configuração do Ambiente**

  - [cite\_start]**Python:** 3.13.3 [cite: 976]
  - [cite\_start]**TensorFlow:** 2.20.0 [cite: 977]
  - [cite\_start]**Cirq:** 1.6.1 [cite: 977]
  - [cite\_start]**Dataset:** Iris (Setosa vs. Versicolor), 70 amostras de treino e 30 de teste[cite: 977].
  - **Configuração do VQC:** 4 qubits, 2 camadas, e conjunto de escalas `qinfo`.

#### **Resumo dos Algoritmos Avançados Demonstrados**

| Algoritmo | Métrica Principal | Valor Obtido |
| :--- | :--- | :--- |
| **VQE** | `ground_state_energy` | [cite\_start]-0.997575 [cite: 1] |
| **QAOA** | `max_expectation` | [cite\_start]2.511605 [cite: 1] |
| **QNN** | `final_loss` | [cite\_start]0.039483 [cite: 1] |
| **AQC** | `final_overlap` | [cite\_start]1.000000 [cite: 1] |
| **QEC** | `final_fidelity` | [cite\_start]0.975000 [cite: 1] |

#### **Melhores Hiperparâmetros Encontrados (Otimização Bayesiana)**

  - **Learning Rate:** `0.0405`
  - **Hidden Units:** `10`
  - **Dropout Rate:** `0.489`
  - **Num Layers (Clássico):** `3`
  - **Melhor Score (val\_loss):** `0.445`

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

    [cite\_start]*As versões utilizadas no projeto foram `tensorflow==2.20.0`, `cirq==1.6.1`, entre outras[cite: 976, 977].*

3.  **Execute o script principal:**

    ```bash
    python QUANTUM
    ```

4.  **Analise os resultados:**
    [cite\_start]Todos os artefatos (dados, figuras, modelos, métricas e relatórios) serão salvos no diretório `output/runs/YYYYMMDD_HHMMSS/`[cite: 45, 136].

-----

## 🔬 Metodologia

O pipeline segue uma abordagem estruturada:

1.  [cite\_start]**Pré-processamento:** Os dados do dataset Iris são filtrados para uma classificação binária, normalizados para o intervalo `[0, 1]` e divididos em conjuntos de treino e teste[cite: 14, 16, 768].
2.  **Construção do VQC:** O circuito é construído em Cirq, consistindo em camadas alternadas de:
      - [cite\_start]**Codificação de Dados (Feature Map):** As características clássicas são mapeadas em rotações nos qubits[cite: 289, 290].
      - [cite\_start]**Camada Variacional (Ansatz):** Rotações parametrizadas (treináveis) e portas de entrelaçamento (CNOTs) são aplicadas para criar correlações quânticas[cite: 334].
3.  **Extração de Features Quânticas:** Para cada amostra de dado, o circuito é simulado e o valor esperado de um observável de Pauli (ex: `Z_k`) é calculado. [cite\_start]Esse valor se torna a "feature quântica"[cite: 9, 28, 778, 781].
4.  [cite\_start]**Treinamento do Modelo Clássico:** As features quânticas extraídas são usadas para treinar uma rede neural densa em TensorFlow, que realiza a classificação final[cite: 29, 807].

-----

## 📈 Próximos Passos Sugeridos

O código já implementa uma vasta gama de técnicas, e os próximos passos podem incluir:

  - [cite\_start]Avaliar a transpilação do circuito para topologias de hardware quântico real[cite: 106].
  - [cite\_start]Explorar estratégias de regularização de custo e inicializações informadas para mitigar *barren plateaus*[cite: 106].
  - [cite\_start]Expandir a aplicação para datasets mais complexos e tarefas de múltiplas classes ou regressão[cite: 106].
  - [cite\_start]Integrar com hardware quântico real através de plataformas na nuvem[cite: 874].

## 📚 Referências

Este trabalho se baseia em conceitos fundamentais da literatura de MLQ:

>   - McClean, J. R., et al. (2018). [cite\_start]*Barren plateaus in quantum neural network training landscapes*[cite: 71, 153].
>   - Cerezo, M., et al. (2021). [cite\_start]*Variational quantum algorithms*[cite: 72, 154].
>   - Schuld, M., et al. (2019). [cite\_start]*Evaluating analytic gradients on quantum hardware for hybrid quantum-classical algorithms*[cite: 73, 155].
>   - Pérez-Salinas, A., et al. (2020). [cite\_start]*Data re-uploading for a universal quantum classifier*[cite: 321].
>   - Havlíček, V., et al. (2019). [cite\_start]*Supervised learning with quantum-enhanced feature spaces*[cite: 322].
