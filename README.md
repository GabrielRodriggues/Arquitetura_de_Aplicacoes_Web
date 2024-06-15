---

# API JWT Rest API

## Visão Geral
A API Rest é protegida por JWT (JSON Web Tokens), com a autenticação do usuário e a emissão de tokens JWT permitindo o acesso aos pontos de extremidade seguros.

## APIs Disponíveis

### POST /login
Endpoint de autenticação para obter um token JWT.

**Request:**
```json
{
    "username": "string",
    "password": "string"
}
```

**Response:**
- **200 OK:** Retorna um token JWT.
    ```json
    {
        "token": "string"
    }
    ```
- **401 Unauthorized:** Credenciais inválidas.

### GET /username/{token}
Rota que obtém o nome de usuário a partir de um token JWT.

**Request:**
- **Path:** `{token}` - Token JWT.

**Response:**
- **200 OK:** Retorna o nome de usuário.
    ```json
    {
        "username": "string"
    }
    ```
- **401 Unauthorized:** Token inválido ou expirado.

### GET /user
Rota que obtém informações sobre o usuário autenticado.

**Request:**
- **Header:** `Authorization: Bearer {token}`

**Response:**
- **200 OK:** Retorna informações do usuário.
    ```json
    {
        "user": "string"
    }
    ```
- **401 Unauthorized:** Token inválido ou expirado.

### GET /admin
Rota protegida acessível apenas por usuários com a função ADMIN.

**Request:**
- **Header:** `Authorization: Bearer {token}`

**Response:**
- **200 OK:** Retorna informações do administrador.
    ```json
    {
        "admin": "string"
    }
    ```
- **403 Forbidden:** Usuário não autorizado.

### GET /moderado
Rota protegida acessível apenas por usuários com a função MODERADO.

**Request:**
- **Header:** `Authorization: Bearer {token}`

**Response:**
- **200 OK:** Retorna informações do moderador.
    ```json
    {
        "moderador": "string"
    }
    ```
- **403 Forbidden:** Usuário não autorizado.

### GET /comum
Rota acessível por usuários comuns.

**Request:**
- **Header:** `Authorization: Bearer {token}`

**Response:**
- **200 OK:** Retorna informações do usuário comum.
    ```json
    {
        "usuario_comum": "string"
    }
    ```
- **403 Forbidden:** Usuário não autorizado.

## Guia de Introdução
Para começar a usar a API JWT Rest API, siga estes passos:

1. Obtenha uma chave de API ativa para autenticar suas solicitações.
2. Certifique-se de que a chave de API esteja incluída em cada solicitação para os endpoints da API.
3. Todas as solicitações devem ser feitas por HTTPS.
4. As respostas da API estão no formato JSON.

## Autenticação
A API autentica as chamadas usando um token JWT.

Para autenticar uma solicitação:
1. Obtenha um token JWT no endpoint `POST /login`.
2. Passe o token JWT no cabeçalho da solicitação para chamadas subsequentes:
    ```
    Authorization: Bearer {token}
    ```

### Resposta de Erro de Autenticação
Se uma chave de API estiver ausente ou inválida/malformada, a resposta retornará um código de status HTTP `401 Não Autorizado`.

## Limites de Taxa e Uso
Os limites de taxa e uso da API JWT Rest API são os seguintes:

- **Limite de Taxa:** 300 solicitações por minuto por chave de API.
- **Código de Status:** Você receberá uma resposta HTTP `429 Too Many Requests` se exceder o limite de taxa.

### Cabeçalhos de Resposta:
- `X-RateLimit-Limit`: O número máximo de solicitações permitidas por minuto.
- `X-RateLimit-Remaining`: O número de solicitações restantes na janela de limite de taxa atual.
- `X-RateLimit-Reset`: O timestamp de quando a janela de limite de taxa atual será redefinida, em segundos do éon UTC.

### Resposta HTTP 503
Uma resposta HTTP `503` indica que o tráfego da API aumentou inesperadamente. O servidor deve retornar ao normal em um máximo de cinco minutos. Se o problema persistir ou se você continuar recebendo qualquer erro HTTP `5XX`, sinta-se à vontade para contatar a equipe de suporte.

## Testes com Insomnia
A API JWT Rest API foi testada usando o Insomnia. Você pode baixar a coleção de testes e importá-la diretamente no Insomnia para testar os endpoints e o comportamento da API.

### Fluxograma
![Fluxograma](https://github.com/GabrielRodriggues/Arquitetura_de_Aplicacoes_Web/assets/112523344/6b9cc640-661b-4c9f-881f-f7e0628e1df3)

### Prints do Insomnia
1. **Login Endpoint** - "http://localhost:8080/login"
![LOGIN](https://github.com/GabrielRodriggues/Arquitetura_de_Aplicacoes_Web/assets/112523344/b761dea6-0881-4610-9ba3-dcb2b9f4dba6)

2. **Username Endpoint** - "http://localhost:8080/username/{token}"
![USERNAME](https://github.com/GabrielRodriggues/Arquitetura_de_Aplicacoes_Web/assets/112523344/be2513fe-4bb6-48f3-b1d4-0cceb0b91929)

4. **User Endpoint** - "http://localhost:8080/user"
![USER](https://github.com/GabrielRodriggues/Arquitetura_de_Aplicacoes_Web/assets/112523344/f4d5eb8f-e3a0-4212-8e6c-6beab22bb054)

5. **Admin Endpoint**  - "http://localhost:8080/admin"
![ADMINISTRADOR](https://github.com/GabrielRodriggues/Arquitetura_de_Aplicacoes_Web/assets/112523344/35b93fe7-1454-4a50-8121-4fc833cbdf90)

6. **Moderado Endpoint** - "http://localhost:8080/moderado"
![MODERADOR](https://github.com/GabrielRodriggues/Arquitetura_de_Aplicacoes_Web/assets/112523344/e09e3078-3b80-46f8-90b5-92e49c89f2d1)

7. **Comum Endpoint** - "http://localhost:8080/comum"
![USUARIOCOMUM](https://github.com/GabrielRodriggues/Arquitetura_de_Aplicacoes_Web/assets/112523344/04291ec4-4ffe-41d2-94aa-2ddf1888ce07)

## Conclusão
Este é um projeto de demonstração que explica a implementação de segurança em uma aplicação web, utilizando JWT como um mecanismo para suportar autenticação e autorização. Ele descreve a implementação de diferentes níveis de acesso com base nos papéis dos usuários e como, da melhor maneira, implementar tokens JWT para autenticação e autorização de usuários funcionais. Para executar o projeto, é necessário ter um ambiente de desenvolvimento com todas as dependências corretamente instaladas e usar ferramentas de inspeção como o Insomnia para experimentar os endpoints e observar o comportamento da API.
