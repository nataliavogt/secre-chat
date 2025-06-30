# secretaria-virtual/
├── app.py                 # Servidor Flask que recebe mensagens
├── twilio_handler.py      # Lógica da secretária
├── requirements.txt       # Lista de bibliotecas necessárias
├── README.md              # Explicação do projeto
from flask import Flask, request
from twilio.twiml.messaging_response import MessagingResponse
from twilio_handler import responder_mensagem

app = Flask(__name__)

@app.route("/whatsapp", methods=['POST'])
def whatsapp():
    mensagem = request.form.get('Body')
    resposta = responder_mensagem(mensagem)
    twilio_response = MessagingResponse()
    twilio_response.message(resposta)
    return str(twilio_response)

if __name__ == "__main__":
    app.run()
def responder_mensagem(mensagem):
    mensagem = mensagem.lower()

    if "consulta" in mensagem:
        return "Claro! Qual o melhor dia e horário para sua consulta?"
    elif "horário" in mensagem:
        return "Atendemos de segunda a sexta, das 8h às 18h."
    elif "endereço" in mensagem:
        return "Nosso consultório fica na Rua Exemplo, 123 – Centro."
    elif "cancelar" in mensagem:
        return "Tudo bem, sua consulta foi cancelada. Se quiser reagendar, me avise!"
    else:
        return "Olá! Posso te ajudar com agendamentos, horários ou endereço."
Flask
twilio
# 🤖 Secretária Virtual para Consultório Médico – WhatsApp

Este é um projeto em Python que usa Flask + Twilio para responder mensagens via WhatsApp, como uma secretária automatizada.

## Funcionalidades
- Agendamento de consultas
- Informações sobre horário e endereço
- Cancelamento de consultas

## Como rodar
1. Crie um ambiente virtual (opcional):
2. Instale as dependências:
3. Rode o app localmente:
4. Use [ngrok](https://ngrok.com/) ou [Render](https://render.com) para expor publicamente e conectar ao Twilio.

---