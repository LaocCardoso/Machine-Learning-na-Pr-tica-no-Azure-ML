# Machine-Learning-na-Pr-tica-no-Azure-ML
Aqui foi aonde realizei meu primeiro projeto para o curso da DIO

# Explorando o Machine Learning Automatizado no Azure Machine Learning

## Objetivo
Neste exercício, eu usei o aprendizado de máquina automatizado no Azure Machine Learning para treinar, avaliar e implantar um modelo de previsão de aluguel de bicicletas.


---

## 1. Criando um Workspace no Azure Machine Learning
1. Acesse o portal do Azure: [portal.azure.com](https://portal.azure.com).
2. Criei um recurso do **Azure Machine Learning** com as seguintes configurações:
   - **Região**: Leste dos EUA
   - **Conta de armazenamento, Cofre de chaves, Application Insights**: Criados automaticamente
3. Após a criação, acessei o **Azure Machine Learning Studio**: [ml.azure.com](https://ml.azure.com).

---

## 2. Treinando um Modelo com Aprendizado de Máquina Automatizado
1. No **Azure Machine Learning Studio**, acessei **ML automatizado** e criei um novo trabalho.
2. Configurei os parâmetros básicos:
   - **Nome do experimento**: `mslearn-bike-rental`
   - **Descrição**: Previsão de aluguel de bicicletas
3. **Tipo de tarefa**: Regressão.
4. **Conjunto de dados**:
   - Nome: `bike-rentals`
   - Fonte: Arquivos locais ([Baixar dataset](https://aka.ms/bike-rentals))
   - Tipo: **Armazenamento de Blobs do Azure**
5. **Configurações da tarefa**:
   - **Coluna alvo**: `aluguéis`
   - **Modelos permitidos**: RandomForest e LightGBM
   - **Máximo de tentativas**: 3 | **Tempo limite**: 15 minutos
6. **Validação e Teste**:
   - Tipo: Divisão de validação de treinamento (10% dos dados)

Iniciei o treinamento e aguardei sua conclusão.

---

## 3. Revisando o Modelo Treinado
1. Após a conclusão, revisei o **melhor modelo** na aba **Visão Geral**.
2. Acessei a aba **Métricas** para visualizar gráficos de desempenho:
   - **Resíduos** (diferença entre valores previstos e reais)
   - **Predicted vs. True** (valores previstos comparados aos reais)

---

## 4. Implantando e Testando o Modelo
1. **Implantação**:
   - **Máquina virtual**: `Standard_DS3_v2`
   - **Instâncias**: 3
   - **Ponto de extremidade**: `predict-rentals`
2. Aguardei a implantação ser **bem-sucedida**.

### Testando o Modelo Implantado
1. No **Azure Machine Learning Studio**, acessei **Pontos de Extremidade** > `predict-rentals`.
2. Na aba **Teste**, inseri os seguintes dados JSON de entrada:
   ```json
   {
     "input_data": {
       "columns": [
         "day", "mnth", "year", "season", "holiday",
         "weekday", "workingday", "weathersit", "temp",
         "atemp", "hum", "windspeed"
       ],
       "index": [0],
       "data": [[1,1,2022,2,0,1,1,2,0.3,0.3,0.3,0.3]]
     }
   }
