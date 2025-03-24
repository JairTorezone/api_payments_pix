# API Payments Pix

Esta aplicação em Python utiliza **websockets** para simular pagamentos via PIX. O objetivo é permitir a integração e testes de simulações de pagamento, facilitando o desenvolvimento de sistemas que precisam trabalhar com transações PIX.

## Estrutura do Projeto
```bash
api_payments_pix/
├── db_models/           # Módulos ou classes relacionados aos modelos de dados
├── instance/            # Arquivos de configuração ou dados específicos de ambiente
├── payments/            # Lógica relacionada aos pagamentos e integrações de PIX
├── repository/          # Acesso a banco de dados ou repositórios de dados
├── static/              # Arquivos estáticos (imagens, CSS, JS, etc.)
├── templates/           # Templates HTML (se aplicável)
├── tests/               # Scripts de teste da aplicação
├── .gitignore           # Arquivo de configurações do Git
├── app.py               # Arquivo principal da aplicação
├── requirements.txt     # Lista de dependências do projeto
└── README.md            # Documentação principal do projeto


```

## Visão Geral

A **API Payments Pix** oferece:
- Simulação de transações de pagamento via PIX.
- Comunicação em tempo real utilizando websockets.
- Um ambiente para testar fluxos de pagamento sem a necessidade de integração com sistemas bancários reais.

## Funcionalidades

- **Simulação de Pagamentos:** Crie e monitore transações PIX simuladas.
- **Comunicação via Websocket:** Envio e recebimento de mensagens em tempo real.
- **Interface Simples:** Facilita a integração com outros sistemas durante o desenvolvimento e testes.


## Testando a API

Você pode testar a API utilizando clientes websocket, como:

* WebSocket King Client

* Postman (versão com suporte a websocket)

* Script em Python: Veja o exemplo abaixo
```python
import sys
sys.path.append("../")

import pytest
import os
from payments.pix import Pix

def test_pix_create_payment():
  pix_instance = Pix()

  payment_info = pix_instance.create_payment(base_dir="../")

  assert "bank_payment_id" in payment_info
  assert "qr_code_path" in payment_info

  qr_code_path = payment_info["qr_code_path"]
  assert os.path.isfile(f"../static/img/{qr_code_path}.png")
```


## Requisitos

- **Python 12.5+**
- **Bibliotecas necessárias:**  
  - `websockets`  
  - `asyncio`  
  - Outras dependências listadas no arquivo `requirements.txt`

## Instalação

1. **Clone o repositório:**

   ```bash
    git clone https://github.com/JairTorezone/api_payments_pix.git
    cd api_payments_pix
    ```

2. **Crie um ambiente virtual (opcional, mas recomendado)**

 ```bash
  python -m venv venv
  source venv/bin/activate   # Linux/MacOS
  venv\Scripts\activate      # Windows
```

3. Instale as dependências e executar:
 ```bash
  pip install -r requirements.txt
  python app.py
```