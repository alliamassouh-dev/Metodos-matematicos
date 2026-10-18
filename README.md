# Analisador e Filtro de Sinais: Fourier & Laplace

Sistematização da disciplina de Análise de Sinais: aproximamos uma onda quadrada por Série de Fourier, analisamos um sinal com FFT, o filtramos (notch 60 Hz + passa-baixas) e modelamos o filtro como sistema linear com Laplace (polos e zeros).

**Integrante:** Állia Massouh *
**Abrir no Colab:** 

## O sinal

Sintético, `fs = 8000 Hz`, 2 s, semente fixa (`default_rng(42)`): senoides de 440 Hz (amp. 1,0) e 880 Hz (amp. 0,5) + zumbido de 60 Hz (amp. 0,8) + ruído branco gaussiano (σ = 0,15). O código que o gera está na seção 0 do notebook, e os arquivos ficam em `data/`.

## Como executar

**Google Colab (recomendado):** faça upload do `.ipynb` em colab.research.google.com → *Ambiente de execução → Executar tudo*. Nada a instalar.

**Local:**
```bash
pip install -r requirements.txt
jupyter notebook sistematizacao_fourier_laplace.ipynb
```

## Resultados principais

| Etapa | Resultado |
|---|---|
| 1 · Série de Fourier | `b_n = 4/(πn)` (n ímpar); `c_n = −2j/(πn)`; sobressinal de Gibbs estaciona em ≈ 8,95 % do salto |
| 2 · Espectro | picos em 60 Hz (0,8), 440 Hz (1,0) e 880 Hz (0,5); piso de ruído plano; aliasing demonstrado (70 Hz → 30 Hz com fs = 100 Hz) |
| 3 · Filtragem | SNR: 2,6 dB → 18,6 dB (FFT/IFFT) e 17,6 dB (IIR) |
| 4 · Laplace | `H(s) = (s²+ω₀²)/(s²+(ω₀/Q)s+ω₀²) · H_Butter4(s)`; zeros em ±j2π·60; polos com Re(s) < 0 ⇒ **estável**; largura do notch = f₀/Q confirmada numericamente |

| Critério |
|---|---|
| Série de Fourier (22 %) | Etapa 1: coeficientes simbólicos, forma complexa verificada, tabela e gráfico de Gibbs |
| Espectro (22 %) | Etapa 2: `rfft` normalizada, Δf e Nyquist explícitos, picos detectados, demo de aliasing |
| Filtragem e reconstrução (16 %) | Etapa 3: filtro derivado do espectro, `irfft`, comparação antes/depois no tempo e na frequência, SNR, áudios |
| Laplace e polos/zeros (22 %) | Etapa 4: H(s) via Laplace, mapa de polos/zeros, estabilidade, seção 4.5 conectando com a Etapa 2 |
| Relatório e reprodutibilidade (10 %) | Interpretação após cada figura, semente fixa, `requirements.txt` |
| Comunicação (8 %) | `roteiro_video.md` |

## Publicar no GitHub (passo a passo)

```bash
git init
git add .
git commit -m "Sistematização: Fourier e Laplace"
git branch -M main
git remote add origin https://github.com/<usuario>/<repo>.git
git push -u origin main
```
