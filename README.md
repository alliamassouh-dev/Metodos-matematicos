# Analisador e Filtro de Sinais: Fourier & Laplace

Sistematização da disciplina de Análise de Sinais: aproximamos uma onda quadrada por Série de Fourier, analisamos um sinal com FFT, o filtramos (notch 60 Hz + passa-baixas) e modelamos o filtro como sistema linear com Laplace (polos e zeros).

**Integrante:** Állia Massouh 

**R.A:** 22450300 

**Abrir no Colab:** https://colab.research.google.com/drive/1B--4VwX_5f6NL-wLWstyi502upRMFZ_Q?usp=sharing

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

### Resultados por Etapa

#### 1. Série de Fourier
* **Coeficientes:** `b_n = 4/(πn)` (n ímpar) e `c_n = −2j/(πn)`
* **Fenômeno de Gibbs:** Sobressinal estaciona em **`≈ 8,95%`** do salto.

#### 2. Análise Espectral
* **Picos Detectados:** `60 Hz` (0,8), `440 Hz` (1,0) e `880 Hz` (0,5)
* **Comportamento:** Piso de ruído plano.
* **Aliasing:** Demonstrado de `70 Hz` para `30 Hz` com amostragem $f_s = 100\text{ Hz}$.

#### 3. Filtragem e Reconstrução
* **Ganho de SNR:**
  * **FFT / IFFT:** `2,6 dB` ➔ **`18,6 dB`**
  * **Filtro IIR:** `2,6 dB` ➔ **`17,6 dB`**

#### 4. Análise por Laplace
* **Função de Transferência:** $H(s) = \frac{s^2+\omega_0^2}{s^2+(\omega_0/Q)s+\omega_0^2} \cdot H_{\text{Butter4}}(s)$
* **Zeros:** $\pm j2\pi \cdot 60$
* **Estabilidade:** $\text{Re}(s) < 0$ $\rightarrow$ **Sistema Estável**
* **Notch:** Largura de banda $f_0/Q$ confirmada numericamente.

---

### Critérios de Avaliação

**Série de Fourier** `(22%)`
  - Coeficientes simbólicos e forma complexa verificada
  - Tabela e gráficos de Gibbs

**Espectro** `(22%)`
  - `rfft` normalizada com $\Delta f$ e Nyquist explícitos
  - Picos detectados e demonstração de aliasing

**Filtragem e Reconstrução** `(16%)`
  - Filtro derivado do espectro e reconstrução com `irfft`
  - Comparação antes/depois (tempo e frequência), SNR e áudios

**Laplace e Polos/Zeros** `(22%)`
  - $H(s)$ via Laplace, mapa de polos/zeros e checagem de estabilidade
  - Conexão da seção 4.5 com a Etapa 2

**Relatório e Reprodutibilidade** `(10%)`
  - Interpretações textuais após figuras
  - Semente aleatória fixa e `requirements.txt`

**Comunicação** `(8%)`
  - Arquivo `roteiro_video.md`
