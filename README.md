# AluraGemini_AgenteIA_GestaoRequisito

# Projeto - Agente de Gestão de Requisitos

## 1. Visão Geral

Este projeto desenvolve um agente inteligente utilizando o modelo Gemini da Google para auxiliar na gestão de requisitos de projetos. O agente é capaz de classificar, categorizar, identificar ambiguidades e inconsistências em documentos de requisitos, otimizando o processo de análise e garantindo a qualidade dos requisitos.

## 2. Funcionalidades

O projeto implementa as seguintes funcionalidades principais:

* **Classificação e Categorização de Requisitos:** O agente analisa o documento de requisitos e os classifica em categorias relevantes (ex: funcional, não funcional, infraestrutura, segurança).
* **Detecção de Ambiguidade e Inconsistência:** O agente identifica ambiguidades, inconsistências, redundâncias e lacunas nos requisitos, fornecendo sugestões para melhoria.

## 3. Tecnologias Utilizadas

* **Google Gemini:** Modelo de linguagem avançado para processamento e análise de texto.
* **Google ADK (Agent Development Kit):** Framework para desenvolvimento de agentes inteligentes.
* **Python:** Linguagem de programação principal.
* **python-docx:** Biblioteca Python para manipulação de arquivos Word (.docx).

## 4. Configuração e Instalação

1.  **Pré-requisitos:**
    * Conta Google Cloud com acesso à API Gemini.
    * Chave de API do Google Gemini configurada como variável de ambiente (`GOOGLE_API_KEY`).
    * Python 3.6 ou superior.
    * pip (Gerenciador de Pacotes do Python).

2.  **Instalação das Dependências:**

    ```bash
    pip install google-genai google-adk python-docx
    ```

## 5. Uso

1.  **Importar as Bibliotecas Necessárias:**

    ```python
    import os
    from google.colab import userdata
    from google import genai
    from google.adk.agents import Agent
    from google.adk.runners import Runner
    from google.adk.sessions import InMemorySessionService
    from google.adk.tools import google_search
    from google.genai import types
    from datetime import date
    import textwrap
    from IPython.display import display, Markdown
    import requests
    import warnings
    from docx import Document
    from google.colab import files

    warnings.filterwarnings("ignore")
    ```

2.  **Configurar a Chave da API Gemini:**

    ```python
    os.environ["GOOGLE_API_KEY"] = userdata.get('GOOGLE_API_KEY')
    client = genai.Client()
    MODEL_ID = "gemini-2.0-flash"
    ```

3.  **Definir as Funções dos Agentes:**

    * `agente_classificar(requisito, data_de_hoje)`: Classifica e categoriza os requisitos.
    * `agente_ambiguidade(requisito, requisitos_classificados)`: Detecta ambiguidades e inconsistências.

4.  **Carregar o Documento de Requisitos:**

    ```python
    uploaded = files.upload()
    for filename in uploaded:
        print(f'Arquivo "{filename}" com tamanho {len(uploaded[filename])} bytes foi carregado.')

    pathArq = r"/content/nome_do_seu_arquivo.docx" # Substitua pelo caminho correto
    try:
        document_word = Document(pathArq)
        with open("requisitos.txt", "a") as arquivo:
            for paragraph in document_word.paragraphs:
                print(paragraph.text)
                arquivo.write(paragraph.text + "\n")
    except FileNotFoundError:
        print(f"Erro: Arquivo não encontrado em {pathArq}.")
    except Exception as e:
        print(f"Ocorreu um erro ao processar o arquivo: {e}")
    ```

5.  **Executar os Agentes:**

    ```python
    # Exemplo de uso
    data_atual = date.today().strftime("%d de %B de %Y")
    with open("requisitos.txt", "r") as arquivo:
      requisitos = arquivo.read()

    requisitos_classificados = agente_classificar(requisitos, data_atual)
    print("Requisitos Classificados:\n", requisitos_classificados)

    ambiguidades_identificadas = agente_ambiguidade(requisitos, requisitos_classificados)
    print("\nAmbigüidades Identificadas:\n", ambiguidades_identificadas)
    ```

## 6. Estrutura do Projeto

├── README.md           # Documentação do projeto

├── Projeto - Agente Gestao Requisito.ipynb  # Notebook Colab com o código do projeto

├── requisitos.txt      # Arquivo de texto com os requisitos extraídos do documento Word

└── Documento_RequisitosVarejo_Medio_Porte_Brasil.docx # Documento de exemplo


## 7. Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou enviar pull requests para melhorar este projeto.

## 8. Licença

Este projeto é licenciado sob a [Licença MIT](LICENSE).

## 9. Autores

* Simone Alves Diana

## 10. Agradecimentos

* Alura pela organização e execução da imersão Inteligência Artificial junto à Google.
* Google Gemini e Google ADK pela poderosa tecnologia de IA.
* Comunidade Python pelo suporte e bibliotecas incríveis.

  
