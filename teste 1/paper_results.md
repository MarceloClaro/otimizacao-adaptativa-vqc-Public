# Resultados Consolidados (Pronto para Publicação)

## 1. quantum vs math (n=5 seeds)
- quantum: Val 96.00% ± 5.83%, Test 91.00% ± 6.63%
- math:    Val 99.00% ± 2.00%, Test 96.00% ± 5.83%
- p-valor (t pareado em Test): N/A (não avaliado)

## 2. Implicações Metodológicas
- Gap médio (quantum): 5.00 p.p.; (math): 3.00 p.p.
- Decisões por validação, avaliação única em teste (sem vazamento).

## 3. Correlações Quânticas e Híbridas
- r(profundidade, Val acc): -0.257
- r(init_scale, Val acc): -0.256
- r(p ruído, Val acc) por tipo:
  - amplitude_damp: r = -0.222
  - bit_flip: r = nan
  - depolarize: r = 0.430
  - phase_flip: r = -0.194

## 4. Observações
- Valores acima são média±desvio sobre seeds; resultados podem variar por splits.
- Para avaliar significância, executar teste t pareado em Test acc (quantum vs math).
## 5. Perfis de Escala — Interpretação das Distribuições
As Figuras scale_profiles_boxplot.png e scale_profiles_violin.png apresentam as distribuições numéricas das constantes usadas em cada perfil de escala (quantum, quantum_strict, qinfo e math). Em termos gerais:
- O perfil quantum exibe amplitudes elevadas (por conter 2π e √2·π) e valores adimensionais físicos (g_e, α·π), o que tende a ampliar a faixa angular efetiva. Isso aumenta a expressividade do feature map e pode favorecer projeções úteis em X/Y/Z, mas requer atenção à saturação quando combinado com circuitos mais profundos.
- O perfil quantum_strict concentra-se em constantes estritamente adimensionais e controladas (2π, π, g_e, 2π·α, ln2·π, (1/√2)·π). A dispersão é mais moderada — refletida por um desvio padrão menor — e isso melhora a estabilidade numérica, reduzindo riscos de saturação e facilitando a treinabilidade.
- O perfil qinfo inclui constantes típicas de informação quântica (incluindo balanços 1/√2 e 1/√3). A distribuição tende a privilegiar rotações coerentes com portas balanceadas e relações bits↔nats, o que pode produzir codificações mais “equilibradas” em problemas sensíveis à orientação de bases.
- O perfil math funciona como baseline com números clássicos (π, π/2, 2π, e, √2·π, φ·π). Sua distribuição é intuitiva e de fácil interpretação, fornecendo um ponto de partida robusto e autoexplicativo, com risco menor de outliers físicos.
Do ponto de vista estatístico (min, max, média e desvio por perfil), observamos que perfis com maior amplitude (maior max e média), como quantum, tendem a permitir codificações mais “agressivas”, úteis para aumentar separabilidade em ROC/AUC, porém com maior sensibilidade a overfitting e a barren plateaus em profundidades altas. Perfis com menor desvio (como quantum_strict) favorecem estabilidade e podem reduzir o gap Val→Test.
Na prática, a escolha do perfil deve considerar o trade-off entre expressividade e estabilidade: para cenários onde AUC precisa ser maximizada sem deteriorar a generalização, recomenda-se iniciar com quantum_strict ou qinfo e migrar para quantum quando a análise de gradiente indicar paisagem saudável. O perfil math é um baseline útil quando se deseja transparência e previsibilidade nas escalas.
