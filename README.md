# Planejamento Agrícola Otimizado — Programação Linear (PuLP + Python)

**Autores:**  
Felipe Petini (RA: 102990)<br>João Victor Lopes Fernandes (RA: 111408)  
Leonardo Henrique Barbosa Colla (RA: 111604)  
Lucas Fortolan Sampaio (RA: 113676)  

## Resumo
Este repositório contém um modelo de **Programação Linear** implementado em Python (biblioteca **PuLP**) para determinar a alocação ótima de hectares entre três culturas (arroz, feijão e milho). O modelo incorpora níveis atuais de nutrientes do solo (N, P, K), necessidades nutricionais específicas por cultura, preços dos fertilizantes e receita por hectare — com o objetivo de **maximizar o lucro líquido total** da propriedade.

Junto ao código está um artigo técnico em LaTeX que formaliza o modelo, detalha hipóteses e sugere extensões e análises de sensibilidade.

## Avaliação crítica (resumo executivo)
**O que funciona bem**
- Modelagem clara: conversão da deficiência de nutrientes em custo por hectare e transformação desses custos em coeficientes da função objetivo é uma abordagem simples e direta.
- Uso de PuLP: solução rápida e reproduzível para problemas lineares com poucas variáveis.
- Documento LaTeX bem estruturado: cobre formulação, hipóteses e extensões possíveis.

**Limitações e pontos de atenção**
- Conversão de restrições agronômicas em custo implica perda de informações: o modelo deixa de controlar limites físicos (ex.: máximo total de N aplicável por safra) e dinâmica do solo (acúmulo / esgotamento entre safras).
- Ligações input → resultado altamente sensíveis: preços de insumos e preço/produção por saca são drivers determinantes. Sem validação dos dados, recomendações podem ser equivocadas.
- Variáveis com `lowBound=0.5` forçam presença de todas as culturas — útil em alguns cenários, mas pode mascarar uma solução economicamente ótima sem essa obrigatoriedade.
- Não há verificação de consistência de unidades e plausibilidade dos valores de entrada (ex.: preço por saca atípico).
- Modelo estático (single-period): não modela rotação, rotação de nutrientes nem efeitos multi-período.

**Recomendações rápidas**
- Validar e normalizar entradas (unidades e plausibilidade).  
- Incluir restrições agronômicas e orçamento para fertilizantes como opções configuráveis.  
- Implementar análise de sensibilidade/paramétrica automática.  
- Documentar e versionar datasets e cenários usados em exemplos.

## Interpretação dos Resultados (Como Ler a Saída)

- **Áreas alocadas:** hectares recomendados para cada cultura após a otimização, com base nos parâmetros fornecidos.
- **Lucro por hectare:** é a receita por hectare menos o custo de correção de nutrientes (fertilizantes).
- **Receita total / Custo total / Lucro total:** valores agregados para a fazenda inteira, calculados multiplicando os valores por hectare pela área alocada para cada cultura.
- **Aviso prático:** Se uma cultura apresentar lucro por hectare negativo, isso pode ocorrer devido à exigência de área mínima imposta pelo modelo. Considere permitir que o modelo remova essa restrição de área mínima.

## Limitações e Cuidados de Uso

1. **Validação dos dados de entrada:** Certifique-se de que as unidades fornecidas (kg/ha para nutrientes, R$/kg para insumos, R$/saca para preços) sejam plausíveis. Dados inconsistentes podem gerar resultados incorretos.
2. **Avaliação agronômica:** O modelo serve como uma ferramenta de apoio à decisão, **não substituindo** uma análise técnica de solo ou recomendações agronômicas específicas. Utilize os resultados como um ponto de partida para decisões, não como prescrição final.
3. **Horizonte temporal:** Este modelo é estático, ou seja, trabalha com um único período de tempo. Se o produtor planeja rotacionar culturas ou usar o modelo para planejamento de múltiplos períodos, a abordagem deve ser expandida.
4. **Sustentabilidade e restrições ambientais:** A otimização econômica pode resultar em práticas que não são sustentáveis a longo prazo (ex.: aplicação excessiva de Nitrogênio). Considere adicionar restrições ambientais, como limites de uso de fertilizantes por hectare, quando necessário.
5. **Sensibilidade a parâmetros:** O modelo é sensível a alterações nos preços dos insumos, produtividade e preços de venda. Sempre execute análises de sensibilidade antes de implementar decisões em larga escala.
6. **Configurações do modelo:** Parâmetros como área mínima por cultura, orçamento máximo de insumos e outras restrições podem influenciar significativamente os resultados. Documente e justifique as escolhas de configuração.

## Licença

Este projeto está licenciado sob a **MIT License**.
