# geracao-graficos-nascimentos

## Importações de Bibliotecas:
* os: Fornece uma maneira de interagir com o sistema operacional, utilizado para manipular diretórios e caminhos de arquivos.
* pandas: Biblioteca para manipulação e análise de dados.
* matplotlib.pyplot: Usado para criar visualizações, neste caso, gráficos.
python```
import os
import pandas as pd
import matplotlib.pyplot as plt
```
## Função criar_diretorios_e_graficos:
* Esta função recebe a lista de arquivos e o mês escolhido pelo usuário.
* Itera sobre cada arquivo.
* Extrai o mês do nome do arquivo.
* Verifica se o mês corresponde ao mês escolhido pelo usuário.
* Lê o arquivo CSV usando a biblioteca Pandas.
* Cria um diretório usando o mês.
* Gera um gráfico de barras empilhadas da distribuição de idades das mães e salva no diretório.

python```
def criar_diretorios_e_graficos(arquivos, mes_escolhido):
    for arquivo in arquivos:
        # Obter o mês a partir do nome do arquivo
        mes = arquivo.split("_")[3][:3]

        # Verificar se o mês corresponde à escolha do usuário
        if mes.upper() == mes_escolhido.upper():
            # Ler o arquivo CSV
            df = pd.read_csv(arquivo)

            # Criar diretório
            diretorio = f"2019-{mes}"
            os.makedirs(diretorio, exist_ok=True)

            # Criar gráfico de barras empilhadas
            plt.figure(figsize=(10, 6))
            plt.hist([df[df['IDADEMAE'] <= 18]['IDADEMAE'], 
                      df[(df['IDADEMAE'] > 18) & (df['IDADEMAE'] <= 35)]['IDADEMAE'],
                      df[df['IDADEMAE'] > 35]['IDADEMAE']], bins=20, stacked=True, color=['blue', 'green', 'orange'])
            
            plt.title(f"Distribuição de Idades das Mães para {mes}")
            plt.xlabel("Idade da Mãe")
            plt.ylabel("Número de Nascimentos")
            plt.legend(['<= 18 anos', '19-35 anos', '> 35 anos'])
            plt.savefig(os.path.join(diretorio, f"grafico_{mes}.png"))
            plt.close()
```

## Bloco Principal (if __name__ == "__main__":):
* Lista os arquivos fornecidos.
* Solicita ao usuário escolher o mês desejado.
* Chama a função criar_diretorios_e_graficos com a lista de arquivos e o mês escolhido.


python```

if __name__ == "__main__":
    # Lista de arquivos fornecidos
    arquivos = [
        "SINASC_RO_2019_ABR.csv",
        "SINASC_RO_2019_AGO.csv",
        "SINASC_RO_2019_DEZ.csv",
        "SINASC_RO_2019_FEV.csv",
        "SINASC_RO_2019_JAN.csv",
        "SINASC_RO_2019_JUL.csv",
        "SINASC_RO_2019_JUN.csv",
        "SINASC_RO_2019_MAI.csv",
        "SINASC_RO_2019_MAR.csv",
        "SINASC_RO_2019_NOV.csv",
        "SINASC_RO_2019_OUT.csv",
        "SINASC_RO_2019_SET.csv",
    ]

    # Solicitar ao usuário escolher o mês desejado
    mes_escolhido = input("Digite o mês desejado (ex: JAN, FEV, MAR): ")

    # Chamar a função para criar diretórios e gráficos para o mês escolhido
    criar_diretorios_e_graficos(arquivos, mes_escolhido)

    print(f"Diretórios e gráficos para {mes_escolhido.upper()} gerados com sucesso!")
```

  
  
