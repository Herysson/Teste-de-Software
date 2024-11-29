# Teste de Integração com o Postman! 🎉

### **Objetivo**
Nesta aula, vamos explorar juntos como usar o Postman para realizar testes de interface com APIs. Vamos trabalhar com os **verbos do protocolo HTTP** e criar exemplos práticos utilizando os servidores fornecidos nos seus repositórios.

---

## **O que é o Postman?**

O Postman é uma ferramenta poderosa para:
- Testar APIs de forma manual ou automatizada.
- Simular chamadas HTTP (GET, POST, PUT, DELETE etc.).
- Validar se os servidores backend estão funcionando corretamente.

Ele é amplamente utilizado por desenvolvedores para garantir que os serviços de backend estão funcionando como esperado.

---

## **Passo 1: Configurando o Ambiente**

1. **Clonando os Repositórios:**
   - **Backend:** Clone o repositório [MenuStream Backend](https://github.com/Herysson/Programacao-Para-Web-Java-Spring/tree/main/Aula%2008%20-%20MenuStream/MenuStream) e configure o ambiente Java/Spring Boot.
   - **Frontend:** Clone o repositório [MenuStream Frontend](https://github.com/Herysson/MenuStream-Front) e configure o React.

2. **Rodando o Backend e Frontend Localmente:**
   - Inicie o servidor Spring Boot (Backend).
   - Inicie o servidor React (Frontend).

3. **Instalando o Postman:**
   - Baixe e instale o Postman [aqui](https://www.postman.com/downloads/).

---

## **Passo 2: Explorando os Verbos HTTP com Exemplos**

Os principais verbos do protocolo HTTP são:
- **GET**: Usado para recuperar dados.
- **POST**: Usado para criar novos recursos.
- **PUT**: Usado para atualizar recursos existentes.
- **DELETE**: Usado para excluir recursos.

---

## **Exemplo Prático com o JSON Fornecido**

Vamos usar o JSON de exemplo no endpoint `/products`.

### **GET - Recuperar Todos os Itens do Menu**

1. Abra o Postman e crie uma nova requisição.
2. Configure:
   - Método: `GET`.
   - URL: `http://localhost:8080/products`.
3. Clique em **Send**.
4. Resultado esperado: Todos os itens do menu são exibidos.

---

### **POST - Criar um Novo Item no Menu**

1. Crie uma nova requisição.
2. Configure:
   - Método: `POST`.
   - URL: `http://localhost:8080/products`.
   - **Body**: Selecione a opção `raw` e escolha o tipo `JSON`.
   - Adicione este JSON no corpo:
     ```json
     {
       "name": "Choco Milkshake",
       "description": "Delicious chocolate milkshake.",
       "price": 4.99,
       "category": "Beverage",
       "availability": true,
       "image": "https://example.com/choco-milkshake.jpg"
     }
     ```
3. Clique em **Send**.
4. Resultado esperado: O novo item será salvo e retornará o JSON criado.

#### Cadastrar de mais itens:
```json
[
  {
    "id": 1,
    "name": "Classic Burger",
    "description": "Burger with beef patty, lettuce, tomato, and our special sauce.",
    "price": 6.99,
    "category": "Burger",
    "availability": true,
    "image": "https://www.eatingwell.com/thmb/UY5N-tQKYgA91XJBwiolc_1nbJ0=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/3757723-7c4020ccc47240138323b9bc5b730e8d.jpg"
  },
  {
    "id": 2,
    "name": "Cheese Lover's Burger",
    "description": "Burger with double cheese, pickles, and mustard.",
    "price": 9.99,
    "category": "Burger",
    "availability": true,
    "image": "https://media-cdn.tripadvisor.com/media/photo-s/0f/97/f4/db/classic-burger.jpg"
  },
  {
    "id": 3,
    "name": "Chicken Burger",
    "description": "Grilled chicken breast with avocado and ranch dressing.",
    "price": 10.50,
    "category": "Burger",
    "availability": true,
    "image": "https://www.indianhealthyrecipes.com/wp-content/uploads/2016/02/chicken-burger-recipe-500x500.jpg"
  },
  {
    "id": 4,
    "name": "Veggie Burger",
    "description": "Made with a homemade patty of quinoa, beans, and sun-dried tomatoes.",
    "price": 9.50,
    "category": "Burger",
    "availability": true,
    "image": "https://i.em.com.br/4CZaX9Zg5UhDtcvjRohtP3-wABA=/790x/smart/imgsapp.em.com.br/app/noticia_127983242361/2015/09/24/691615/20150924132717865592e.jpg"
  },
  {
    "id": 5,
    "name": "Spicy Burger",
    "description": "Burger with jalapenos, pepper jack cheese, and spicy mayo.",
    "price": 10.00,
    "category": "Burger",
    "availability": true,
    "image": "https://embed.widencdn.net/img/mccormick/dy2orpqxvj/800x800px/52%20SPICY%20CRUNCHY%20BURGER.jpeg?keep=c&crop=yes&u=a3rg0s&use=aeriv"
  },
  {
    "id": 6,
    "name": "BBQ Bacon Burger",
    "description": "Burger topped with crispy bacon, onion rings and BBQ sauce.",
    "price": 11.99,
    "category": "Burger",
    "availability": true,
    "image": "https://lovelesscafe.com/wp-content/uploads/2023/08/bbq-bacon-burger-recipe.jpeg"
  },
  {
    "id": 7,
    "name": "Fish Burger",
    "description": "Crispy fish fillet with tartar sauce and lettuce.",
    "price": 9.99,
    "category": "Burger",
    "availability": true,
    "image": "https://www.deliciousmagazine.co.uk/wp-content/uploads/2021/12/960x1200-Fish-Burgers-25.png"
  },
  {
    "id": 8,
    "name": "Coke",
    "description": "Classic Coca-Cola, chilled.",
    "price": 1.99,
    "category": "Beverage",
    "availability": true,
    "image": "https://down-br.img.susercontent.com/file/b7efbad4e84391f4bfb7fdfb1f333f85"
  },
  {
    "id": 9,
    "name": "Lemonade",
    "description": "Freshly squeezed lemonade made with real lemons.",
    "price": 2.50,
    "category": "Beverage",
    "availability": true,
    "image": "https://www.torani.com/sites/default/files/recipes/illustration/GettyImages-181856842-min.jpg"
  },
  {
    "id": 10,
    "name": "Craft Beer",
    "description": "Local craft beer with a rich and smooth taste.",
    "price": 3.99,
    "category": "Beverage",
    "availability": true,
    "image": "https://madmonday.au/cdn/shop/articles/Beer_Price.jpg?v=1677277265&width=1100"
  },
  {
    "id": 11,
    "name": "Mystery Burger",
    "description": "Dare to try it? Each week, our chef creates a new burger that keeps its ingredients a secret until you bite into it!",
    "price": 12.99,
    "category": "Burger",
    "availability": true,
    "image": "https://pbs.twimg.com/media/DJiMAEoVAAAWYNS.jpg"
  },
  {
    "id": 12,
    "name": "Heineken",
    "description": "Heineken Beer 600ml",
    "price": 3.00,
    "category": "Beer",
    "availability": true,
    "image": "https://mercado.carrefour.com.br/_next/image?url=https%3A%2F%2Fcarrefourbrfood.vtexassets.com%2Farquivos%2Fids%2F23256938%2Fcerveja-heineken-garrafa-600-ml-3.jpg%3Fv%3D637655998038470000&w=3840&q=75"
  },
  {
    "id": 13,
    "name": "Fanta",
    "description": "Orange Fanta 355ml",
    "price": 2.00,
    "category": "soda",
    "availability": true,
    "image": "https://acougueamigos.com/cdn/shop/products/acougue-amigos_33_3.jpg?v=1619228903"
  },
  {
    "id": 14,
    "name": "Fries",
    "description": "Friend Fries",
    "price": 5.50,
    "category": "Food",
    "availability": true,
    "image": "https://www.tendaatacado.com.br/dicas/wp-content/uploads/2022/06/como-fazer-batata-frita-topo.jpg"
  },
  {
    "id": 15,
    "name": "Juradir",
    "description": "Handsome Jurandir",
    "price": 150.00,
    "category": "Human",
    "availability": true,
    "image": "https://s2-gshow.glbimg.com/vTLjuA6q7B5qDjveIFEAeTWmM9Q=/336x191/top/smart/https://s2.glbimg.com/mfTa3pYxf2rSN14MAdqpwNjQZJU=/i.s3.glbimg.com/v1/AUTH_e84042ef78cb4708aeebdf1c68c6cbd6/internal_photos/bs/2022/T/x/d7OB0nT4ehp74VHMBBxg/jurandir-vieira-1.jpg"
  }
]


```

---

### **PUT - Atualizar o Preço de um Item**

1. Crie uma nova requisição.
2. Configure:
   - Método: `PUT`.
   - URL: `http://localhost:8080/products/1`.
   - **Body**: Selecione `raw` e escolha o tipo `JSON`.
   - Adicione este JSON no corpo:
     ```json
     {
       "id": 1,
       "name": "Choco Milkshake",
       "description": "Delicious chocolate milkshake.",
       "price": 5.99,
       "category": "Beverage",
       "availability": true,
       "image": "https://example.com/choco-milkshake.jpg"
     }
     ```
3. Clique em **Send**.
4. Resultado esperado: O preço do item será atualizado.

---

### **DELETE - Excluir um Item**

1. Crie uma nova requisição.
2. Configure:
   - Método: `DELETE`.
   - URL: `http://localhost:8080/menu/1`.
3. Clique em **Send**.
4. Resultado esperado: O item será excluído.

---

### **Desafios Para Você**

1. **Desafio 1: Criar Múltiplos Itens**
   - Utilize o método `POST` para adicionar mais itens ao menu.

2. **Desafio 2: Filtrar Itens Por Categoria**
   - Utilize um endpoint (ex.: `GET /menu?category=Burger`) para listar apenas itens de uma categoria específica.

3. **Desafio 3: Validação de Erros**
   - Tente criar um item sem fornecer todas as informações obrigatórias. Observe como o backend responde e registre o erro.

---

### **Referências**
Para aprofundar seus conhecimentos sobre **testes de integração utilizando o Postman**, aqui estão algumas referências úteis:

1. **Documentação Oficial do Postman: Testes de Integração**
   - A documentação oficial do Postman oferece um guia detalhado sobre como configurar e executar testes de integração, incluindo a criação de coleções, uso de scripts e execução de testes em diferentes ambientes.
   - [Acessar Documentação](https://learning.postman.com/docs/tests-and-scripts/test-apis/integration-testing/)

