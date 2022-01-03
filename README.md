# SDK Java

SDK de integração eRede utilizado no Ecommerce para autorizar transações e usada no WS para os Cancelamentos das mesmas.
Projeto forkado para a utilização da SDK rodando com a versão da JDK 1.8, e não 11 como foi feito no projeto inicial. 

# Utilizando

## Autorizando uma transação

```java
// Configuração da loja
Store store = new Store("PV", "TOKEN");

// Transação que será autorizada
Transaction transaction = new Transaction(20.99, "pedido123")
    .creditCard(
        "5448280000000007",
        "123",
        "12",
        "2020",
        "Fulano de Tal"
    );

// Autoriza a transação
transaction = (new eRede(store).create(transaction));

if (transaction.getReturnCode().equals("00")) {
  System.out.printf("Transação autorizada com sucesso: %s", transaction.getTid());
}
```

Por padrão, a transação é capturada automaticamente; caso seja necessário apenas autorizar a transação, o método `Transaction::capture()` deverá ser chamado com o parâmetro `false`:

```java
// Configuração da loja
Store store = new Store("PV", "TOKEN");

// Transação que será autorizada
Transaction transaction = new Transaction(20.99, "pedido123")
    .creditCard(
        "5448280000000007",
        "123",
        "12",
        "2020",
        "Fulano de Tal"
    ).capture(false);

// Autoriza a transação
transaction = (new eRede(store).create(transaction));

if (transaction.getReturnCode().equals("00")) {
  System.out.printf("Transação autorizada com sucesso: %s", transaction.getTid());
}
```

## Autorizando uma transação IATA

```java
// Configuração da loja
Store store = new Store("PV", "TOKEN");

// Transação que será autorizada
Transaction transaction = new Transaction(20.99, "pedido123")
    .creditCard(
        "5448280000000007",
        "123",
        "12",
        "2020",
        "Fulano de Tal"
    ).iata("code123", "250");

// Autoriza a transação
transaction = (new eRede(store).create(transaction));

if (transaction.getReturnCode().equals("00")) {
  System.out.printf("Transação autorizada com sucesso: %s", transaction.getTid());
}
```
