# Perfis de Escala — Constantes e Objetivos

## quantum
Constantes: 6.283185, 3.141593, 5.083204, 2.002319, 0.022925, 4.442883

Resumo: min=0.022925, max=6.283185, média=3.496018, desvio=2.065718

Perfil 'quantum': usa razões adimensionais inspiradas em MQ/QED (2π, π, φ·π, g_e, α·π, √2·π).
Objetivo: alta expressividade mantendo ângulos fisicamente coerentes. Pode explorar melhor projeções em X/Y/Z.

## quantum_strict
Constantes: 6.283185, 3.141593, 2.002319, 0.045851, 2.177586, 2.221441

Resumo: min=0.045851, max=6.283185, média=2.645329, desvio=1.873032

Perfil 'quantum_strict': apenas constantes estritamente adimensionais recorrentes (2π, π, g_e, 2π·α, ln2·π, (1/√2)·π).
Objetivo: controle fino de escala angular e estabilidade numérica, reduzindo saturação.

## qinfo
Constantes: 6.283185, 2.221441, 1.813799, 0.693147, 1.442695, 0.022925

Resumo: min=0.022925, max=6.283185, média=2.079532, desvio=2.013236

Perfil 'qinfo': constantes úteis em informação quântica (2π, (1/√2)·π, (1/√3)·π, ln2, log2(e), α·π).
Objetivo: favorecer estados e rotações típicos de portas Hadamard/balanced e relações bits↔nats.

## math
Constantes: 3.141593, 1.570796, 6.283185, 2.718282, 4.442883, 5.083204

Resumo: min=1.570796, max=6.283185, média=3.873324, desvio=1.568801

Perfil 'math': conjunto matemático clássico (π, π/2, 2π, e, √2·π, φ·π).
Objetivo: baseline matemático versátil, de fácil interpretação e autoexplicativo.

