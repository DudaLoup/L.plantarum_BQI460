# 🧬 Controle de Qualidade e Pré-processamento: Lactiplantibacillus plantarum

Este repositório documenta o pipeline de controle de qualidade (QC) e trimmagem de dados de sequenciamento de nova geração (NGS), etapa fundamental para a montagem *de novo* do genoma de *Lactiplantibacillus plantarum*.

## 📊 Visão Geral dos Dados
* **Organismo:** *Lactiplantibacillus plantarum*
* **Plataforma de Sequenciamento:** Illumina MiSeq
* **Estratégia:** Paired-End (PE)
* **Comprimento Inicial das Leituras:** 301 pb
* **Conteúdo GC:** ~44,5% (Confirmado via FastQC, condizente com a referência do NCBI).

## 🛠️ Ferramentas Utilizadas
* **FastQC:** Avaliação primária das métricas de qualidade das bibliotecas brutas e processadas.
* **Trimmomatic:** Remoção de sequências adaptadoras e filtragem rigorosa baseada em escores Phred.
* **MultiQC:** Consolidação dos relatórios de QC em um dashboard HTML interativo.

## ⚙️ Pipeline e Parâmetros de Filtragem
A avaliação inicial detectou decaimento de qualidade característico nas extremidades 5' e 3' (especialmente na fita reversa), presença de bases ambíguas (N) e contaminação por adaptadores. Para mitigar esses artefatos, o **Trimmomatic** foi executado com os seguintes parâmetros:

* `ILLUMINACLIP`: Remoção completa de sequências de adaptadores sintéticos da Illumina.
* `HEADCROP:15`: Excisão das 15 bases iniciais de todas as *reads* para eliminar flutuações de sinal e instabilidades do início do ciclo.
* `TAILCROP:10`:  Excisão das 10 bases finais de todas as *reads* para eliminar flutuações de sinal e instabilidades do início do ciclo.
* `SLIDINGWINDOW:4:25`: Avaliação dinâmica das extremidades 3', cortando a sequência caso a qualidade média em uma janela de 4 bases caísse abaixo do escore Phred 25.
* `MINLEN:100`: Retenção estrita de fragmentos com comprimento superior a 100 pb, prevenindo a hiperfragmentação dos grafos nas etapas subsequentes de montagem.

## 📈 Resumo dos Resultados
A aplicação do filtro resultou em um conjunto de dados de alta fidelidade estrutural:
* **Total de pares originais:** 353.248
* **Sobrevivência integral (Paired):** 62,22% (219.794 pares)
* **Impacto na Cobertura:** O rigor da qualidade reduziu a cobertura teórica de ~66x para ~20x, estabelecendo um balanço ideal entre volume de dados e precisão nucleotídica para a montagem *de novo*.

---

### 🔍 Relatório Interativo
O relatório comparativo completo gerado pelo **MultiQC** (demonstrando as métricas pré e pós-trimmagem) está hospedado via GitHub Pages e pode ser acessado abaixo:

👉 **[Visualizar Relatório MultiQC]([(https://github.com/DudaLoup/L.plantarum_BQI460))**
