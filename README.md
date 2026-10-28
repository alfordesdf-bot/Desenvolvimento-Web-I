# Desenvolvimento-Web-I

# UNIVERSIDADE DA MAIA
## Licenciatura em Informática / Tecnologias da Informação
### Disciplina: Desenvolvimento Web I (1º Semestre)

---

# RELATÓRIO DE ESTUDO DE API WEB – MOMENTO 1 (M1)

**Título da API Estudada:** TMDB (The Movie Database) API  
**Identificação do Grupo:** inf26dw1g34   
**Elementos do Grupo:**  
- Alfordes Manuel da Costa João - A049853  

---

## 1. RESUMO DOS REQUISITOS DE ENTREGA E MODO DE SUBMISSÃO

Conforme estipulado no enunciado e na plataforma Moodle da disciplina, a entrega do Momento 1 de Avaliação Contínua é composta por dois elementos obrigatórios e a respetiva apresentação presencial em aula:

### O que é necessário entregar?
1. **Ficheiro de Apresentação / Documentação em Formato Digital (PDF/Word/PPTX):** Documento detalhado cobrindo o estudo crítico, a arquitetura e os pontos funcionais da API selecionada (peso de 75% na nota do M1).
2. **Ficheiro `Postman Collection` (`.json`):** Ficheiro exportado do Postman contendo a coleção estruturada de todos os pedidos (*requests*) funcionais demonstrados e testados pelo grupo (peso de 25% na nota do M1).

### Como e onde deve ser entregue?
- **Plataforma de Submissão:** Área de submissão do Moodle da unidade curricular de Desenvolvimento Web I.
- **Validação Prévia:** O tema e a API devem ser submetidos previamente no Moodle na atividade "Selecção do tema do M1" para aprovação do docente antes da entrega final.
- **Requisito Obrigatório:** A classificação final deste momento de avaliação fica pendente até ao cumprimento cumulativo da entrega dos ficheiros no Moodle e da **apresentação presencial obrigatória** na aula subsequente à entrega.

---

## 2. INTRODUÇÃO E SELEÇÃO DAS APIS PROPOSTAS

No âmbito do estudo, análise crítica e desenho de aplicações e serviços Web, o grupo selecionou a arquitetura REST para o desenvolvimento deste trabalho prático.

### Proposta de APIs ao Docente:
1. **Opção Principal Selecionada:** **TMDB API (The Movie Database)**
   - *Hiperligação da Documentação:* [https://developer.themoviedb.org/docs](https://developer.themoviedb.org/docs)
   - *Justificação:* A API da TMDB é uma referência global no fornecimento de dados sobre a indústria cinematográfica e televisiva. Cumpre rigorosamente a arquitetura REST, faz uso de múltiplos verbos HTTP (`GET`, `POST`, `DELETE`), implementa autenticação via Bearer Token/API Key e disponibiliza dados ricos estruturados em JSON, ideais para o desenvolvimento contínuo das etapas posteriores da disciplina.
2. **Opção Alternativa Secundária:** **CoinGecko API**
   - *Hiperligação da Documentação:* [https://www.coingecko.com/en/api/documentation](https://www.coingecko.com/en/api/documentation)
   - *Justificação:* Serviço focado em dados financeiros de criptomoedas, igualmente RESTful e útil para dashboards em tempo real.

---

## 3. DESCRIÇÃO DOS OBJETIVOS DA API WEB (TMDB)

A **TMDB API** tem como principal objetivo fornecer a desenvolvedores de todo o mundo acesso programático a uma vasta base de dados comunitária contendo metadados sobre filmes, programas de televisão, séries, atores, diretores, equipas técnicas, imagens, capas (*posters*) e avaliações.

### Principais Objetivos Funcionais:
- **Catálogo e Consulta:** Permitir a pesquisa detalhada de produções cinematográficas e televisivas.
- **Personalização de Utilizador:** Possibilitar a gestão de listas de filmes favoritos, listas de reprodução (*watchlists*) e classificações através de contas de utilizador.
- **Integração Multimédia:** Fornecer hiperligações e metadados para conteúdos multimédia (trailers do YouTube, imagens de fundo em alta resolução, cartazes oficiais).
- **Suporte Multilíngue:** Fornecer dados traduzidos em dezenas de idiomas (incluindo Português `pt-PT` e `pt-BR`).

---

## 4. MODO DE FUNCIONAMENTO DA API WEB

### 4.1. Arquitetura e Formato das Mensagens
- **Estilo Arquitetural:** REST (Representational State Transfer).
- **URL Base da API:** `https://api.themoviedb.org/3`
- **Formato das Respostas:** Estritamente **JSON** (JavaScript Object Notation), garantindo interoperabilidade imediata com clientes Web e móveis.
- **Códigos de Estado HTTP Utilizados:**
  - `200 OK`: Pedido processado com sucesso.
  - `201 Created`: Recurso criado/adicionado com sucesso (ex: classificação atribuída).
  - `401 Unauthorized`: Chave de API ou Token inválido/ausente.
  - `404 Not Found`: Recurso não encontrado na base de dados.

### 4.2. Método de Autenticação
A TMDB exige autenticação para a grande maioria das suas rotas, suportando dois métodos principais:
1. **API Key (v3 authentication):** Passada como *Query Parameter* na URL (ex: `?api_key=SUA_CHAVE`).
2. **Bearer Token (v4 authentication - Recomendado):** Enviado no cabeçalho HTTP (*HTTP Request Header*) com o formato:
   
```http
   eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI0MmU5ZGUwNTliN2IzMDFlZGVjMGM2ZjgwMTA0NzAzZiIsIm5iZiI6MTc5MzE4MTY3OC4xNjMsInN1YiI6IjZhZTFjN2VlZDY4M2NmNTZiMDJjM2NjYSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.5tBNeE70HneWl5WwCUGr7hwMS0PShwUORXLUHuNXV88
