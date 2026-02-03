SISTEMA DE MONITORAMENTO PREDITIVO DE GLICOSE COM INTELIGÊNCIA ARTIFICIAL EM APOIO A PACIENTES CRÔNICOS DE DIABETES MELITUS TIPO 2 


1. Contextualização do Projeto em Saúde

	O diabetes mellitus tipo 2 (DM2) é uma condição crônica global, afetando quase 600 milhões de adultos em 2024 (IDF, 2024). No Brasil, a diabetes atinge aproximadamente 20 milhões de pessoas (prevalência de 10,5% da população adulta), sendo uma das principais causas de morte associadas a complicações cardiovasculares e renais (Vigitel/IBGE, 2025).

	Um dos maiores desafios no seu manejo é o controle dos níveis de glicose no sangue e a consequente prevenção de complicações agudas, como episódios de hipoglicemia ou hiperglicemia severa, frequentemente denominados "crises diabéticas". A predição precoce desses eventos pode evitar o surgimento e evolução de outras complicações, melhorar a qualidade de vida e reduzir custos com internações. Esse esforço de pesquisa é crucial para pacientes crônicos, familiares, profissionais e sistema de saúde.

	A ciência, através de trabalho em pesquisa e desenvolvimento tem buscado soluções para o combate a essa complexa doença. O significativo desenvolvimento da tecnologia da informação e da chamada Ciência de Dados tem trazido algumas propostas de colaboração a esse esforço. Uma das áreas de pesquisa é a predição com técnicas de Inteligência Artificial, utilizando o suporte de estruturas de computação. 

	Em particular, a predição de crises na DM2 é um assunto complexo e envolve diferentes áreas do conhecimento. Necessita de um ecossistema de meios especializados de sensoreamento-processamento-atuação clínica. No que se refere aos sensores, os exames laboratoriais e mesmo os métodos de coleta de glicose capilar não atendem a necessidades de monitoramento constante dos pacientes. Os recentes sistemas de Monitoramento Contínuo de Glicose (MCG) ainda são caros e com restrita disponibilização de dados, além de oferecerem aplicativos com análise parcial dos datasets produzidos.
	
	Em relação ao processamento das informações, é essencial a existência de uma base de dados estruturada de pacientes, algoritmos de processamento de séries temporais multivariadas e o emprego de modelos de predição validados. Dados como níveis de glicose, ingestão alimentar, medicações, atividade física e parâmetros fisiológicos devem estar disponíveis durante o processo.

  Nesse contexto, modelos de inteligência artificial (IA), especialmente técnicas de aprendizagem automática para problemas de previsão, empregando séries temporais multivariadas, aprendizagem supervisionada, e modelos de previsão profundos de última geração, como redes neurais recorrentes Long Short-Term Memory (LSTM), mostram-se adequadas nas tarefas de predição por sua habilidade em capturar dependências de longo prazo em sequências (Hochreiter & Schmidhuber, 1997). Estudos demonstram que LSTMs podem prever hipoglicemia 30 min antes com 90% de sensibilidade/especificidade em populações específicas (Zheng et al., 2024).

  Contudo, a aplicação clínica de modelos puramente baseados em dados enfrenta barreiras relacionadas à segurança, interpretabilidade e conformidade com práticas médicas estabelecidas. Diante disso, uma abordagem híbrida, que combina regras baseadas em diretrizes médicas, LSTM e mecanismos de atenção, pode oferecer uma solução equilibrada, capaz de unir robustez clínica e capacidade adaptativa da IA. 	

2. Identificação do Problema e Árvore de Definição

	a. Problema central 
		Pacientes crônicos de diabetes melitus tipo 2 (DM2), profissionais de saúde, familiares e outros interessados têm dificuldade no monitoramento contínuo e proativo da glicose no sangue, resultando em descontrole metabólico e aumento de complicações relacionadas à doença.
			
	b. Causas
		Dificuldade de entendimento e uso de informações disponíveis por parte dos interessados. 
		Os meios (dispositivos de medição contínua de glicose-glicômetros) são inadequados. Nem todos oferecem feedback imediato aos interessados. Têm custo elevado. Não oferecem meios para uma análise mais robusta em tempo real dos dados recebidos de sensores, nem a detecção de padrões anormais e tampouco, predição de crises metabólicas. 
		Há lacunas no desenvolvimento de modelos e algoritmos para predição de descontrole metabólico. 
		Há falta de banco de dados regionalizados adequados de pacientes para o treinamento de modelos de predição. 

	c. Consequências
		 Óbitos prematuros, internações recorrentes, baixa adesão a tratamentos, baixa qualidade de vida do paciente e demais interessados e aumento de custos para o sistema de saúde (público e privado).
   4. Definição da Proposta de Solução com Lean Canvas 
	a. Área do produto
		1) Problema
			Pacientes com DM2, profissionais de saúde e familiares enfrentam dificuldades no monitoramento proativo da glicose, baixa adesão ao autocuidado e sobrecarga dos serviços de saúde, resultando em descontrole metabólico e complicações.

		2) Solução
			Minimum Viable Product (MVP) educativo interativo “Waze da Glicose” (Python em notebook como Google Colab/Jupyter, com execução em tempo real acelerado):
				Modelo fisiológico simplificado e leve baseado em adaptação do Dalla Man et al. (2007) para DM2: absorção realista de carboidratos (6 g/min máx.), decaimento exponencial de insulina rápida (75 min meia-vida), insulina basal contínua, produção hepática modulada por insulina, utilização periférica, ruído estocástico gaussiano e eventos programados (refeições, lanches, exercício). Avanço temporal discreto em passos de 5 minutos fisiológicos por ciclo.
				Pacientes virtuais interativos (classe VirtualPatient): configuração inicial (nome, tipo — ex.: "moderate" como padrão), intervenções manuais em tempo real (ingestão de carbs, bolus de insulina, exercício) e simulação acelerada.
				Previsão glicêmica: rede LSTM com mecanismo de atenção integrada para horizontes de 30–60 minutos (pondera eventos relevantes via atenção, capturando padrões não-lineares em séries temporais simuladas); fallback para extrapolação linear simples (inclinação dos últimos 8–12 pontos) para transparência e baixa latência.
				Motor de alertas clínicos baseado nas ADA Standards of Care in Diabetes—2026: detecção em tempo real de hipoglicemia Level 1 (<70 mg/dL), hiperglicemia (>180 mg/dL), risco iminente e variações rápidas; histórico de alertas registrado.
				Interface de simulação em tempo real (função run_complete_simulation): dashboard ao vivo (glicemia atual, tendências, eventos, alertas via prints estruturados), avanço cíclico com pausas visuais (~2s), intervenções interativas e resumo final com métricas (TIR, média, DP, min/max, contagem de eventos/alertas).
				Visualização final: plot da curva glicêmica completa (matplotlib) com faixa ideal sombreada (70–180 mg/dL verde), limites horizontais, marcação de eventos e legenda.
				Prova de conceito didática para ensino, treinamento e experimentação segura de estratégias de manejo glicêmico; base para futuras evoluções (ex.: interface web SaaS, integração com dados reais de MGC, otimização por reforço).
3) Métricas 
			a)) Métricas Clínicas-simuladas (alinhadas à ADA Standards of Care in Diabetes—2026):
				Tempo na Faixa (TIR 70–180 mg/dL): >70% em perfis ideais/moderados (meta para maioria dos adultos não grávidos);  
				Tempo Abaixo da Faixa (TBR <70 mg/dL): <4% (ou <1% em perfis idosos/complexos); TBR <54 mg/dL: <1%;  
				Redução de eventos graves (hipo/hiper detectados) >50% após intervenções educativas simuladas;  
				Glicose média, desvio-padrão, min/max exibidos no resumo final.

			b)) Métricas Técnicas: 
				RMSE da previsão (Attention-LSTM ou linear) ≤20–30 mg/dL em horizontes curtos (baseado em dados simulados; meta aspiracional para validação qualitativa);  
				% de pontos em zonas A/B da Clarke Error Grid Analysis (CEGA) ≥90% (se implementada em validação futura; atualmente qualitativa via comparação com padrões fisiológicos);  
				Latência por ciclo de atualização <2–3 segundos (incluindo cálculo e exibição);  
				Uptime/execução estável no Colab/Jupyter >98% em sessões típicas.

			c)) Métricas Operacionais/educativas:  
				Conclusão 100% dos cenários educativos simulados (ex.: simulação de 5–10 minutos reais cobrindo múltiplos ciclos);  
				Tempo de simulação equivalente a 24h fisiológicas <10–15 segundos reais (aceleração efetiva);  
				Contagem de alertas/eventos gerados e exibidos no resumo final para
   5. Objetivos
	a. Geral
		Avaliar, de forma preliminar e exploratória, a viabilidade conceitual, técnica e didática de um sistema interativo estilo “Waze da Glicose” para simulação e visualização em tempo real da dinâmica glicêmica em pacientes com Diabetes Mellitus Tipo 2 (DM2), funcionando como um MVP educativo que permita experimentação segura de intervenções terapêuticas (ingestão de carboidratos, bolus de insulina, exercício) em ambiente virtual, com geração de alertas clínicos e métricas de controle glicêmico.


	b. Específicos:
		1) Mapear o estado da arte atual (2025–2026) em processamento de dados de sensores contínuos de glicose (MGC), modelos de previsão glicêmica e sistemas de suporte à decisão para pacientes com DM2, identificando limitações, tendências (incluindo arquiteturas híbridas LSTM-Transformer, Attention-LSTM e modelos baseados em atenção para séries temporais biomédicas) e requisitos regulatórios (ANVISA RDC 657/2022, LGPD).
		2) Desenvolver um módulo de simulação fisiológica glicêmica simplificado e computacionalmente leve, baseado em adaptação do modelo de Dalla Man et al. (2007) para DM2, incorporando absorção realista de carboidratos (taxa máxima ~6 g/min), decaimento exponencial de insulina rápida (meia-vida ~75 min), insulina basal contínua, produção hepática modulada por insulina, ruído estocástico gaussiano e eventos programados (refeições, lanches, exercício), com avanço temporal discreto em passos de 5 minutos como alternativa viável à coleta inicial de dados reais ou à implementação completa de modelos complexos.
		3) Implementar a criação de pacientes virtuais interativos com perfis representativos de variações realistas de controle glicêmico (ex.: moderado com aderência variável), permitindo configuração inicial (nome, tipo de paciente), intervenções manuais em tempo real e simulação acelerada (ex.: 5 minutos reais simulando 5 minutos fisiológicos por ciclo, com atualizações visuais a cada ~2 segundos).
   4) Explorar e implementar uma arquitetura de previsão glicêmica baseada em rede neural recorrente LSTM com mecanismo de atenção, integrada ao paciente virtual para processar históricos de glicemia e prever tendências em horizontes de 30–60 minutos, ponderando dinamicamente eventos relevantes via atenção; manter fallback (alternativa) para extrapolação linear simples (baseada na inclinação dos últimos 8–12 pontos) como opção de baixa latência e alta interpretabilidade, alinhando-se ao estado da arte em previsão glicêmica com LSTM-Atenção e híbridos Transformer para captura de dependências de longo prazo em dados ruidosos/simulados.

		5) Desenvolver um módulo de motor de alertas clínicos baseado nas diretrizes mais recentes da American Diabetes Association (ADA Standards of Care in Diabetes—2025), com detecção em tempo real de hipoglicemia (Level 1: <70 mg/dL), hiperglicemia (>180 mg/dL), risco iminente e variações rápidas, registrando histórico de alertas; priorizar regras determinísticas para garantir segurança didática no MVP, com cálculo de métricas como Tempo na Faixa (TIR >70% em 70–180 mg/dL para a maioria dos adultos), tempo abaixo da faixa (TBR <70 mg/dL <4%, <54 mg/dL <1%) e estatísticas descritivas (média, desvio-padrão, min/max).

		6) Criar um sistema de simulação interativa em tempo real com dashboard visual ao vivo (glicemia atual, tendências, eventos, alertas) e plot final da curva glicêmica (com faixa ideal 70–180 mg/dL sombreada, marcação de eventos e legenda), orquestrando os componentes (paciente virtual, simulação temporal, previsões, alertas); permitir execução por duração definida (ex.: 5–10 minutos reais), avanço manual do tempo, intervenções interativas e observação de métricas educativas (TIR simulado, variabilidade, contagem de alertas/eventos), com foco na experiência didática, demonstração de causa-efeito e experimentação segura de estratégias de manejo glicêmico.
   7) 6. KPIs e OKRs
	a. KPIs (Key Performance Indicators)
		Os KPIs operacionais e de desempenho foram selecionados para monitoramento contínuo durante o desenvolvimento e testes do MVP, priorizando métricas técnicas, simuladas/clínicas e de usabilidade, com foco em validação qualitativa/quantitativa limitada e alinhamento com padrões da área (ADA Standards of Care in Diabetes—2026, CEGA).

		1) Técnicos/Operacionais
			Latência de simulação: < 2–3 s por passo de 5 min fisiológicos (meta: 99% dos ciclos de atualização no dashboard live);  
			Disponibilidade/estabilidade do MVP no Colab/Jupyter: > 98% (sem crashes em sessões de teste > 30 min, incluindo simulações contínuas de 5–10 min reais); 
			RMSE da previsão glicêmica (LSTM - Atenção): ≤ 20–30 mg/dL (média em horizontes de 30–60 min, em simulações com ruído estocástico e eventos);  
			Percentual em zonas A/B da Clarke Error Grid Analysis (CEGA): ≥ 90% para previsões de 30–60 min (meta aspiracional para validação qualitativa/futura comparação com padrões fisiológicos esperados).
		2) Clínicos-Simulados (baseados em ADA Standards of Care in Diabetes—2026)  			Time in Range (TIR 70–180 mg/dL) médio em simulações: ≥ 70% em perfis moderados/ideais; ≥ 50% em perfis complexos (ex.: idoso frágil, se implementado);  
			Time Below Range (TBR <70 mg/dL): < 4% em cenários ideais; < 1% para TBR <54 mg/dL (prioridade em evitar hipoglicemias graves/clinicamente significativas);
Redução de eventos hipoglicêmicos graves (<54 mg/dL ou alertas Level 2) e hiperglicêmicos (>180 mg/dL prolongados): ≥ 50% após aplicação de intervenções corretivas simuladas (ex.: bolus, carbs rápidos).
7. Metodologia e Técnicas de IA
	a. Metodologia
		O presente trabalho propõe o desenvolvimento de um protótipo de aplicativo/simulador para predição e monitoramento de glicemia em pacientes com diabetes mellitus tipo 2 (DM2), utilizando dados gerados por simulação fisiológica como teste de conceito. Enquadra-se metodologicamente como pesquisa-piloto ou pré-teste de caráter exploratório (Lakatos & Marconi, 2003), com foco na construção de um MVP (Minimum Viable Product) funcional, interativo e educativo. A metodologia consistiu no desenvolvimento de um simulador computacional interativo implementado em Python, com execução em ambiente de notebook (como Google Colab ou Jupyter), que reproduz a dinâmica glicêmica de um paciente virtual com DM2 de forma simplificada, porém realista e controlada.

		O núcleo do simulador baseia-se em uma adaptação do modelo fisiológico de Dalla Man et al. (2007) para o contexto de diabetes tipo 2, incorporando os principais subsistemas: taxa de aparecimento de glicose da refeição (Ra), produção endógena de glicose hepática modulada por insulina, utilização periférica de glicose dependente e independente de insulina, secreção
de insulina endógena e clearance plasmático. Para viabilizar a execução em tempo real e a interatividade em recursos computacionais limitados, optou-se por: avanço temporal discreto em passos de 5 minutos (simulando aceleração temporal); absorção de carboidratos com taxa máxima fisiologicamente plausível (~6 g/min); decaimento exponencial da insulina rápida (meia-vida aproximada de 75 minutos); insulina basal contínua; ruído estocástico gaussiano para representar variabilidade biológica; eventos programados representativos de um dia típico (refeições principais, lanches, exercício).

		Adicionalmente, foram integrados componentes avançados para predição e suporte à decisão: Modelo preditivo baseado em LSTM com mecanismo de atenção — uma rede neural recorrente de longo curto prazo de memória (LSTM) treinada nos dados históricos gerados pelo simulador, com camada de atenção para ponderar os timestamps mais relevantes na previsão de glicemia futura (horizonte de 30–60 minutos), melhorando a captura de padrões temporais complexos e não-lineares.

		Sistema de alertas clínicos — regras baseadas em diretrizes internacionais (ADA) para detecção em tempo real de hipoglicemia (<70 mg/dL), hiperglicemia (>180 mg/dL), risco iminente de hipo/hiper e variações rápidas, registrando histórico de alertas para análise posterior.
		Interface de simulação em tempo real — implementação de um paciente virtual interativo que permite:configuração inicial (nome, severidade: leve/moderada/grave);
intervenções manuais em tempo real (ingestão de carboidratos, bolus de insulina rápida, exercício);
atualização periódica do estado fisiológico (a cada ~2 segundos na visualização);

		Exibição de dashboard ao vivo com glicemia atual, tendências, métricas (TIR 70–180 mg/dL, média, desvio-padrão, min/max) e eventos registrados.

		Modo de simulação completa automatizada — função dedicada (run_complete_simulation) que executa ciclos contínuos por duração definida (ex.: 5–10 minutos reais simulando horas/dias do paciente), com plot final da curva glicêmica completa, marcação de eventos e faixa-alvo sombreada.

		A abordagem seguiu prototipagem iterativa: parametrização inicial por regras clínicas clássicas (razões 1800/500 ajustadas por peso corporal para bolus e basal), validação qualitativa por comparação com padrões fisiológicos esperados (respostas pós-prandiais, efeito dawn, rebound hipoglicêmico etc.) e ênfase na interatividade educativa. O protótipo permite experimentação segura de estratégias de manejo glicêmico (decisões de bolus, correção, jejum prolongado, exercício), visualização imediata das consequências e análise de métricas quantitativas (TIR, tempo abaixo/acima da meta, estatísticas descritivas da série temporal).Essa estrutura possibilita tanto uso didático (treinamento de pacientes/estudantes/profissionais) quanto base para futuras extensões (integração com dados reais de MGC, otimização de controle por reforço, closed-loop híbrido), mantendo o caráter exploratório e de baixo custo computacional do MVP conceitual.


	b. Técnicas de IA
		Neste trabalho, inicialmente foram pesquisados códigos em Python do modelo fisiológico de Dalla Man et al. (2007), adaptado para diabetes mellitus tipo 2 (DM2), com o objetivo de simular de forma mais precisa a dinâmica glicêmica, especialmente as respostas pós-prandiais. Devido às restrições computacionais do ambiente Google Colab (limites de tempo de execução, memória e GPU) e ao foco em entregar um MVP (Minimum Viable Product) funcional, interativo e de rápida demonstração didática, optou-se por uma modelagem aproximada e leve do
    simulador fisiológico, com avanço temporal em passos de 5 minutos e simplificações em absorção de carboidratos, decaimento insulínico e ruído estocástico.

		No componente de inteligência artificial para previsão glicêmica, foi implementada uma rede LSTM com mecanismo de atenção integrada ao paciente virtual. Esse modelo processa séries temporais históricas de glicemia geradas pelo simulador, aplicando uma camada de atenção para ponderar dinamicamente os timestamps mais relevantes (ex.: picos pós-prandiais recentes ou tendências de queda), permitindo previsões de glicemia em horizontes de 30 a 60 minutos com maior capacidade de capturar dependências de longo prazo e padrões não-lineares complexos.
 
		A escolha da arquitetura Attention-LSTM justifica-se por sua robustez em tarefas de séries temporais biomédicas, combinando a memória seletiva da LSTM com o foco contextual da atenção, o que melhora a interpretabilidade parcial e a precisão em cenários com variabilidade biológica (ruído, eventos irregulares). Embora o código permita desabilitar o LSTM (fallback para extrapolação linear simples baseada na inclinação dos últimos 8–12 pontos para maior transparência e latência mínima), a versão principal prioriza o Attention-LSTM como componente preditivo principal, alinhando-se ao estado da arte em 2026. Estudos recentes reforçam que arquiteturas híbridas envolvendo LSTM e mecanismos de atenção (ou fusões com Transformer) representam abordagens de fronteira na previsão glicêmica para suporte à decisão em diabetes. 
    10. Referências Bibliográficas

AMERICAN DIABETES ASSOCIATION. Standards of Care in Diabetes—2025. Diabetes Care, Alexandria, v. 48, supl. 1, p. S1-S352, jan. 2025. Disponível em: https://diabetesjournals.org/care/issue/48/Supplement_1. Acesso em: 28 jan. 2026.

BATTELINO, T. et al. Clinical targets for continuous glucose monitoring data interpretation: recommendations from the international consensus on time in range. Diabetes Care, [S.l.], 2019. 

BRASIL. Agência Nacional de Vigilância Sanitária. Resolução da Diretoria Colegiada - RDC nº 751, de 8 de setembro de 2022. Dispõe sobre requisitos de segurança e desempenho, rotulagem e outros para dispositivos médicos. Diário Oficial da União, Brasília, DF, 9 set. 2022. Disponível em: https://www.in.gov.br/web/dou/-/resolucao-rdc-n-751-de-8-de-setembro-de-2022-426751979. Acesso em: 28 jan. 2026.

______. ______. Resolução da Diretoria Colegiada - RDC nº 848, de 21 de maio de 2024. Estabelece requisitos essenciais de segurança e desempenho para dispositivos médicos e IVD. Diário Oficial da União, Brasília, DF, 22 maio 2024.

______. Conselho Nacional de Saúde. Resolução nº 510, de 7 de abril de 2016. Dispõe sobre as normas aplicáveis a pesquisas em Ciências Humanas e Sociais. Diário Oficial da União, Brasília, DF, 24 maio 2016. Disponível em: https://www.gov.br/conselho-nacional-de-saude/pt-br/atos-normativos/resolucoes/2016/resolucao-no-510.pdf. Acesso em: 28 jan. 2026.

______. Lei nº 13.709, de 14 de agosto de 2018. Lei Geral de Proteção de Dados Pessoais (LGPD). Diário Oficial da União, Brasília, DF, 15 ago. 2018.


BROWNLEE, Jason. Deep learning for time series forecasting. v. 1.6, 2019. Copyright 2019 Jason Brownlee. 

BUENO, Tom. Tempo no alvo: o que ele revela sobre o diabetes que a hemoglobina glicada nãomostra. Disponível em https://umdiabetico.com.br. Acesso em 25 Jan 26. 

DALLA MAN et al., GIM, Simulation Software of the Glucose-Insulin System, 2007.


__________________, A Model of Glucose Regulation in the Type 2 Diabetic Condition, 2008.

HOCHREITER, S.; SCHMIDHUBER, J. Long short-term memory. Neural computation, Cambridge, v. 9, n. 8, p. 1735-1780, 1997.

HOVORKA, R., et al, Nonlinear model predictive control of glucose concentration in subjects with type 1 diabetes, 2004. Physiological Measurement, 25(4), 905–920.

INTERNATIONAL DIABETES FEDERATION. IDF Diabetes Atlas 2024. Bruxelas, 2024. Disponível em:  https://diabetesatlas.org . Acesso em: 28 jan. 2026.

LAKATOS, Eva Maria; MARCONI, Marina de Andrade. Fundamentos de metodologia científica. 5. ed. São Paulo: Atlas, 2003.

SOARES, Anderson; et al. Análise preditiva de complicações em pacientes diabéticos. Saúde Business, [s. l.], 17 set. 2017. Disponível em: https://www.saudebusiness.com/artigos/anlise-preditiva-de-complicaes-em-pacientes-diabticos/. Acesso em: 26 jan. 2026.

SOCIEDADE BRASILEIRA DE DIABETES. Brasil já tem cerca de 20 milhões de pessoas com diabetes. Portal SBD, 2025. Disponível em:  https://diabetes.org.br/brasil-ja-tem-cerca-de-20-milhoes-de-pessoas-com-diabetes/ . Acesso em: 28 jan. 2026.

VETTORETTI, G. et al. Hypoglycemia prediction using machine learning models for patients with type 2 diabetes. Journal of Diabetes Science and Technology, [S.l.], v. 9, n. 4, p. 914-920, jul. 2015. Disponível em: https://pmc.ncbi.nlm.nih.gov/articles/PMC4495530/
. Acesso em: 28 jan. 2026. 

ZHENG, S. et al. Generalization of a deep learning model for continuous glucose monitoring to predict hypoglycemia in Chinese and US populations with type 1 and type 2 diabetes. JMIR Medical Informatics, Toronto, v. 12, e56909, 2024. Disponível em:  https://medinform.jmir.org/2024/1/e56909/ . Acesso em: 28 jan. 2026.
Anexo “A” - Manual do Usuário – Waze da Glicose
-----------------------------------------------------------------------------------------------------------------------

Simulador Educativo Interativo de Manejo Glicêmico em Diabetes Mellitus Tipo 2
Versão MVP – Prova de Conceito (2026)

1. Introdução e Objetivo
	Bem-vindo ao Waze da Glicose – um simulador educativo interativo desenvolvido como prova de conceito (MVP) para fins didáticos e de pesquisa exploratória.
	Este protótipo permite simular, em tempo real acelerado, a dinâmica glicêmica de um paciente virtual com Diabetes Mellitus Tipo 2 (DM2), experimentando de forma segura intervenções como ingestão de carboidratos, bolus de insulina rápida e exercício físico.  
	Importante: Este é um ambiente virtual de aprendizado. Não substitui monitoramento real, consulta médica ou dispositivos clínicos (ex.: MGC, bomba de insulina). Use apenas para educação, treinamento e análise de cenários hipotéticos.
	O simulador integra:
		Modelo fisiológico aproximado (adaptação leve do Dalla Man et al., 2007, para DM2)
		Previsão glicêmica com LSTM + mecanismo de atenção (opcional; fallback para tendência linear)
		Alertas clínicos baseados em diretrizes ADA 2026
		Dashboard ao vivo e resumo final com métricas (TIR, média, desvio-padrão, min/max, alertas)

2. Requisitos e Execução
	Ambiente: Python em notebook (Google Colab recomendado)
	Bibliotecas necessárias: numpy, matplotlib, time (já inclusas no código)
	Execução: Rode o script completo. No final, responda 's' para iniciar a simulação automática de 5 minutos (ou execute manualmente via comandos).

3. Como Iniciar e ConfigurarAo executar o código, você verá:

O sistema inclui:
1. 📦 Modelo Dalla Man modificado para DM2
2. 🧠 LSTM com mecanismo de atenção
3. ⚠️ Sistema de alertas clínicos
4. 👤 Paciente virtual em tempo real
5. 📊 Dashboard interativo

Deseja executar a simulação? Digite 's' para sim (recomendado) ou 'n' para não:

Digite 's' → inicia simulação automática de 5 minutos reais (cada ciclo simula 5 minutos fisiológicos, com ~2s de pausa para visualização).

Digite 'n' → modo manual: crie paciente e simule passo a passo.

4. Criando e Controlando o Paciente Virtual
	No modo manual ou para customização:python

		patient = VirtualPatient(name="Maria Silva", patient_type="moderate")

		name: Nome do paciente (ex.: "João Oliveira")
		patient_type: "moderate" (padrão; outros perfis podem ser adicionados futuramente)

		Intervenções em tempo real (após cada simulate_minutes(5)):Ingestão de carboidratos: patient.add_carbs(grams=45) → simula refeição
		Bolus de insulina rápida: patient.add_bolus(units=5) → correção ou cobertura
		Exercício: patient.add_exercise(intensity='moderate', duration_min=30) → reduz glicemia

5. Simulação em Tempo Real
	Função principal: run_complete_simulation(duration_minutes=5)
		Duração: Tempo real de execução (ex.: 5 min → ~5 ciclos de 5 min fisiológicos cada)
	Atualizações: A cada ciclo, avança 5 minutos no paciente virtual
	Dashboard live: Mostra glicemia atual, tendências, eventos e alertas
	Pausa: ~2 segundos entre ciclos (para visualização; última iteração sem pausa)

	Exemplo de saída no dashboard:Glicemia atual
		Tendência (seta ou valor)
		Alertas ativos (ex.: " Hipoglicemia detectada: 65 mg/dL")
		Métricas parciais

6. Alertas Clínicos (Baseados em ADA Standards of Care 2026)
	O sistema gera alertas em tempo real conforme diretrizes ADA 2026:Hipoglicemia Level 1: <70 mg/dL → Ação imediata recomendada (ex.: ingerir carboidratos rápidos)
		Hiperglicemia: >180 mg/dL → Considerar correção
		Risco iminente de hipo/hiper ou variações rápidas
		Histórico de alertas exibido no resumo final

	Metas de referência (ADA 2026, para a maioria dos adultos não grávidos):Tempo na Faixa (TIR): >70% em 70–180 mg/dL (~17h/dia)
	Tempo Abaixo da Faixa (TBR): <4% <70 mg/dL; <1% <54 mg/dL
	Tempo Acima da Faixa (TAR): Minimizar >180 mg/dL

7. Resumo Final e Visualização
	Ao final da simulação:Estatísticas: Glicose média, desvio-padrão, mínima/máxima
		TIR calculado (70–180 mg/dL)
		Contagem: Pontos totais, eventos, alertas gerados
		Gráfico final (matplotlib):Curva de glicemia ao longo do tempo
		Faixa ideal sombreada (verde 70–180 mg/dL)
		Linhas horizontais: Limite inferior (vermelho 70), superior (laranja 180)
		Pontos vermelhos: Eventos (refeições, bolus, exercício)
		Legenda e grid para clareza

8. Dicas Educativas e Limitações
	Exploração segura: Teste decisões como "comer sem bolus" ou "exercício após refeição" e veja impactos.
	Interpretação: Use para entender causa-efeito (ex.: por que hiperglicemia pós-prandial? Por que hipoglicemia tardia?).
	Limitações do MVP:Simulação aproximada (não modelo exato Dalla Man)
	Dados simulados (não reais de MGC)
	Sem integração multimodal (ex.: sono, estresse)
	Execução em Colab pode variar por máquina



9. Arquitetura do sistemas
	O Waze da Glicose é um protótipo modular implementado em Python, projetado para rodar em ambientes como Google Colab ou Jupyter Notebook. Sua arquitetura segue princípios de orientação a objetos e separação de responsabilidades, facilitando a compreensão, manutenção e futuras expansões.

	a. Visão Geral dos Componentes Principais
		O sistema é composto por camadas interconectadas:Camada de Simulação Fisiológica (Núcleo do Paciente Virtual)  
		Classe principal: 	VirtualPatient  
			Modela a dinâmica glicêmica de um paciente com DM2 usando uma adaptação simplificada e leve do modelo fisiológico de Dalla Man et al. (2007).  
			Inclui subsistemas chave:  Absorção de carboidratos (taxa máxima realista ~6 g/min)  
			Decaimento exponencial de insulina rápida (meia-vida ~75 min)  
			Insulina basal contínua  
			Produção hepática de glicose modulada por insulina  
			Utilização periférica de glicose  
			Ruído estocástico gaussiano para variabilidade biológica  
			Eventos programados (refeições, lanches, exercício)

		Avanço temporal: discreto em passos de 5 minutos fisiológicos por ciclo (simulação acelerada).  
		Armazena histórico completo (history) com timestamps, glicemia, eventos e estado interno.

		Camada de Previsão com Inteligência Artificial
 			Modelo principal: LSTM com mecanismo de atenção (Attention-LSTM)  				Processa séries temporais históricas de glicemia (geradas pelo simulador).  
				A camada de atenção pondera dinamicamente os pontos mais relevantes (ex.: picos recentes pós-prandiais ou tendências de queda), melhorando a captura de padrões não-lineares e dependências de longo prazo.  
				Horizonte de previsão: 30–60 minutos à frente.  
				Treinado em dados simulados; fallback para extrapolação linear simples (inclinação dos últimos 8–12 pontos) para cenários de baixa latência ou quando o modelo LSTM for desabilitado.

				Alinha-se ao estado da arte 2025–2026: arquiteturas híbridas LSTM-Attention ou LSTM-Transformer são amplamente usadas em previsão glicêmica (ex.: multimodal CNN-BiLSTM-Attention para DM2, ou fusões Transformer-LSTM para dependências globais e locais em MGC).

				Camada de Alertas Clínicos (Motor de Regras)  Sistema de regras determinísticas baseado nas ADA Standards of Care in Diabetes—2026 (publicado em dezembro 2025).  
				Alertas em tempo real para:  Hipoglicemia Level 1: <70 mg/dL (ação preventiva recomendada)  
					Hiperglicemia: >180 mg/dL  
					Risco iminente de hipo/hiper ou variações rápidas

				Registra histórico de alertas (alert_history) para análise posterior.  
				Prioriza segurança: regras clínicas determinísticas sobre previsões probabilísticas.

			Camada de Interface e Simulação em Tempo Real  Função principal: run_complete_simulation(duration_minutes=...)  
				Executa ciclos contínuos por duração definida (ex.: 5 minutos reais simulando horas/dias do paciente).  
				Atualiza estado a cada ~2 segundos (pausa visual para observação).  
Exibe dashboard ao vivo (via prints estruturados com emojis): glicemia atual, tendências, eventos, alertas ativos.

			Modo manual: métodos como simulate_minutes(5), display_live_dashboard(), add_carbs(), add_bolus(), add_exercise() para intervenções interativas.

			Camada de Visualização e Resumo  Resumo final: estatísticas (média, desvio-padrão, min/max, TIR 70–180 mg/dL, contagem de pontos/eventos/alertas).  
			Plot final (matplotlib):  Curva de glicemia ao longo do tempo  
			Faixa ideal sombreada (verde: 70–180 mg/dL)  
			Limites horizontais (vermelho 70 mg/dL, laranja 180 mg/dL)  
			Pontos vermelhos para eventos  
			Legenda, grid e rotação de eixos para clareza.

		Fluxo Geral de Execução
			Criação do paciente virtual → 2. Simulação cíclica (avança tempo + aplica intervenções) → 3. Previsão (Attention-LSTM ou linear) → 4. Geração de alertas → 5. Atualização do dashboard → 6. Resumo final + gráfico.

		Essa arquitetura modular permite experimentação educativa segura, com foco em interatividade e métricas alinhadas à ADA 2026 (TIR >70% em 70–180 mg/dL para a maioria dos adultos; TBR <70 mg/dL <4%; <54 mg/dL <1%). 
		Futuras evoluções podem incluir integração com dados reais de MGC, interface web (ex.: Streamlit) ou otimização por aprendizado por reforço.

10. Contato e Referências
	Em caso de dúvidas ou sugestões para o projeto acadêmico: 
         	 - Contate o autor do trabalho (nobrecunha@yahoo.com.br ou whatsapp 85992831228). 	

	Desenvolvido para fins acadêmicos (pós-graduação, 2026).
	Referências principais:  
	ADA Standards of Care in Diabetes—2026 (seção 6: Glycemic Goals)  
	Dalla Man et al. (2007) – modelo fisiológico adaptado  
	Literatura recente em Attention-LSTM para previsão glicêmica, em particular ZHENG, S. et al. (2024). 

	Divirta-se experimentando e aprendendo!




