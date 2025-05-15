
README - Sistema de Pagamentos via PIX com Flask
=================================================

Descrição
---------
Este projeto é uma aplicação web construída com Flask que simula a geração e confirmação de pagamentos via PIX. 
A aplicação permite criar pagamentos, exibir QR Codes para pagamento, e confirmar automaticamente via eventos em tempo real usando Socket.IO.

Funcionalidades
---------------
- Criar pagamentos PIX
- Exibir QR Code do pagamento
- Confirmar pagamentos recebidos
- Atualização em tempo real via WebSocket (Socket.IO)

Requisitos
----------
- Python 3.8 ou superior
- Pip (gerenciador de pacotes)
- SQLite (já incluído no Python padrão)

Instalação
----------
1. Clone o repositório:
   git clone <URL-do-repositório>
   cd <nome-da-pasta>

2. Crie e ative um ambiente virtual:
   python -m venv venv
   source venv/bin/activate  (Linux/Mac)
   venv\\Scripts\\activate     (Windows)

3. Instale as dependências:
   pip install -r requirements.txt

4. Inicialize o banco de dados (se necessário):
   flask shell
   >>> from repository.database import db
   >>> from app import app
   >>> with app.app_context():
   ...     db.create_all()
   ...     exit()

Como Executar
-------------
Execute a aplicação com o comando:

python app.py

A aplicação estará disponível em: http://127.0.0.1:5000

Endpoints da API
----------------

1. Criar Pagamento PIX
   - POST /payments/pix
   - JSON Body: { "value": 100.0 }
   - Resposta: QR Code e dados do pagamento.

2. Visualizar QR Code
   - GET /payments/pix/qr_code/<nome_arquivo>

3. Confirmar Pagamento
   - POST /payments/pix/confirmation
   - JSON Body: { "bank_payment_id": "<id>", "value": 100.0 }

4. Visualizar Página do Pagamento
   - GET /payments/pix/<id_do_pagamento>

Estrutura de Diretórios
------------------------
project/
│
├── app.py
├── requirements.txt
├── repository/
│   └── database.py
├── db_models/
│   └── payment.py
├── payments/
│   └── pix.py
├── static/
│   └── img/
├── templates/
│   ├── payment.html
│   ├── confirmed_payment.html
│   └── 404.html

Observações
-----------
- A comunicação em tempo real ocorre com Socket.IO. O frontend pode escutar os eventos com o nome: payment-confirmed-<ID>.
- A criação do QR Code está simulada através da classe Pix e não utiliza uma API bancária real.

Licença
-------
Este projeto é open-source e pode ser modificado livremente.
"""
