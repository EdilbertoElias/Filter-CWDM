# Filter CWDM - Filtro Óptico de Multiplexação por Divisão de Comprimento de Onda

## 📋 Descrição

Este projeto implementa um **filtro óptico CWDM (Coarse Wavelength Division Multiplexing)** com 200 GHz de espaçamento entre canais. O trabalho envolve simulações de circuitos fotônicos ideais e baseados em PDK (Process Design Kit), análise Monte Carlo para avaliação de robustez, e geração de layouts para fabricação em GDS.

O objetivo principal é validar o design de um multiplexador/demultiplexador óptico utilizando acopladores direcionais em guias de onda de silício integrado.

## 📁 Estrutura do Projeto

```
Filter CDWM/
├── Ideal/
│   └── CWDM_Ideal.ipynb          # Simulação do design ideal (sem variações)
├── PDK/
│   ├── CWDM_PDK.ipynb             # Simulação com PDK realístico
│   └── CWDM.gds                   # Layout do design em formato GDS
├── GDS/
│   ├── CWDM_200GHz_final.gds      # Design final otimizado
│   ├── CWDM_200GHz_final.txt      # Informações do design final
│   ├── CWDM_200GHz_TEST_CREATOR.yaml  # Configuração para testes
│   ├── CWDM_200GHz_DRC.lyrdb      # Regras de verificação de design
│   └── Test_Creator.ipynb         # Script para criar configuração de testes
├── Analise_Monte_Carlo/
│   ├── Analise_Monte_Carlo - DC.ipynb     # Análise Monte Carlo dos acopladores direcionais
│   ├── Analise_Monte_Carlo - GUIAS.ipynb  # Análise Monte Carlo dos guias de onda
│   └── Histograma_*.txt            # Resultados das simulações Monte Carlo
└── README.md
```

## 🔬 Descrição dos Módulos

### 1. **Ideal** - Design Ideal
- **Arquivo**: `CWDM_Ideal.ipynb`
- **Descrição**: Simula o filtro CWDM sob condições ideais
- **Operações principais**:
  - Cálculo de comprimentos de guia de onda baseado em FSR (Free Spectral Range)
  - Configuração de acopladores direcionais com coeficientes de acoplamento ideais (0.5, 0.29, 0.08)
  - Análise de resposta em frequência utilizando ONA (Optical Network Analyzer)
  - Visualização de espectros de transmissão

### 2. **PDK** - Design Realístico com PDK
- **Arquivo**: `CWDM_PDK.ipynb`
- **Descrição**: Simula o filtro usando componentes realísticos do PDK da plataforma de fabricação
- **Operações principais**:
  - Integração com componentes `ebeam_dc_te1550` (acoplador direcional real)
  - Otimização do comprimento de acoplamento (coupling_length)
  - Simulação com parâmetros realísticos do processo de fabricação
  - Comparação de desempenho com o design ideal

### 3. **GDS** - Layout e Testes
- **Arquivos**:
  - `CWDM_200GHz_final.gds`: Layout final em formato GDS-II para fabricação
  - `CWDM_200GHz_TEST_CREATOR.yaml`: Configuração dos pontos de teste ópticos
  - `Test_Creator.ipynb`: Script para gerar automaticamente configurações de teste
  - `CWDM_200GHz_DRC.lyrdb`: Regras para verificação de design (Design Rule Check)

### 4. **Analise_Monte_Carlo** - Análise de Tolerância
- **Arquivos**:
  - `Analise_Monte_Carlo - DC.ipynb`: Análise de variações em acopladores direcionais
  - `Analise_Monte_Carlo - GUIAS.ipynb`: Análise de variações em guias de onda
  - `Histograma_*.txt`: Resultados das simulações (variações de 0.08, 0.29, 0.5, 1.0, 2.0 GHz e 50, 100, 200 amostras)

## 🎯 Parâmetros Principais

| Parâmetro | Valor |
|-----------|-------|
| **Comprimento de onda central** | 1550 nm |
| **Range de comprimento de onda** | 1500 - 1600 nm |
| **Espaçamento entre canais** | 200 GHz |
| **Índice efetivo** | 2.35317 |
| **Índice de grupo** | 4.3458796 |
| **Espaçamentos testados** | 50, 100, 200 GHz |
| **Polarização** | TE (Transversal Elétrica) |

## 📊 Coeficientes de Acoplamento

O design utiliza três acopladores direcionais em cascata com diferentes coeficientes de acoplamento:

- **Acoplador de entrada**: 0.5 (50% de potência)
- **Acoplador 1**: 0.29 (Coeficiente de acoplamento intermediário)
- **Acoplador 2**: 0.08 (Acoplamento fraco)

## 🚀 Como Usar

### Pré-requisitos

1. **Lumerical INTERCONNECT** (v2.21 ou superior)
   - API Python habilitada
   - Paths: `C:\Program Files\Lumerical\v221\api\python\lumapi.py` (Ideal)
   - Paths: `C:\Program Files\Lumerical\v242\api\python\lumapi.py` (PDK)

2. **Python 3.7+** com bibliotecas:
   ```bash
   pip install numpy scipy matplotlib
   ```

### Execução

1. **Executar simulação ideal**:
   ```
   Abrir Ideal/CWDM_Ideal.ipynb e executar todas as células
   ```

2. **Executar simulação com PDK**:
   ```
   Abrir PDK/CWDM_PDK.ipynb e executar todas as células
   ```

3. **Análise Monte Carlo**:
   ```
   Abrir Analise_Monte_Carlo/Analise_Monte_Carlo - DC.ipynb (ou GUIAS.ipynb)
   Executar as células para gerar distribuições de variação
   ```

4. **Criar configuração de testes**:
   ```
   Abrir GDS/Test_Creator.ipynb e executar para gerar YAML de testes
   ```

## 📈 Resultados Esperados

- **Simulações ideais**: Resposta plana com espalhamento de potência entre canais
- **Simulações PDK**: Pequenas diferenças devido a variações de processo
- **Monte Carlo**: Distribuições de transmissão mostrando robustez do design
- **GDS**: Layout otimizado pronto para fabricação

## 📝 Saídas Principais

- Gráficos de transmissão vs comprimento de onda
- Histogramas de variação de desempenho
- Arquivo GDS para litografia
- Configurações de pontos de teste ópticos

## 🔧 Tecnologias Utilizadas

- **Lumerical INTERCONNECT**: Simulação fotônica
- **Python**: Processamento e análise de dados
- **NumPy/SciPy**: Cálculos numéricos
- **Matplotlib**: Visualização de dados
- **GDS-II**: Formato de layout
- **YAML**: Configuração de testes

## 👤 Autor

Edilberto Elias Xavier Junior - Uinersidade Federal de Campina Grande - VIRTUS-CC

## 📅 Data do Projeto

Junho de 2025

## 📄 Licença

Propriedade do autor - Uso acadêmico/pessoal

---

**Nota**: Este projeto requer acesso à plataforma Lumerical INTERCONNECT para execução das simulações. Os dados de histograma pré-computados podem ser analisados sem a plataforma.
