import requests

URL_BASE = "https://api.minhaloja.com"


# Cenário Positivo: Criação de Recurso
def test_cadastrar_produto_com_sucesso():
    payload = {"nome": "Bolo de Cenoura", "preco": 25.00}
    resposta = requests.post(f"{URL_BASE}/produtos", json=payload)

    # Asserção de Status Code 201 Created
    assert resposta.status_code == 201

    # Validação do corpo da resposta JSON
    dados = resposta.json()
    assert "id" in dados
    assert dados["nome"] == "Bolo de Cenoura"


# Cenário Negativo: Recurso Não Encontrado
def test_buscar_produto_inexistente_retorna_404():
    resposta = requests.get(f"{URL_BASE}/produtos/999999")

    # Asserção de Status Code 404 Not Found
    assert resposta.status_code == 404
