## Running the sample code

1. Start a local Cassandra server on default port 9042. The included `docker-compose.yml` starts everything required for running locally.

    ```
    docker-compose up -d
    ```

2. Start a first node:

    ```
    mvn compile exec:exec -DAPP_CONFIG=local1.conf
    ```

3. Try it with [grpcurl](https://github.com/fullstorydev/grpcurl):

    ```
    # add item to cart
    grpcurl -d '{"cartId":"cart2", "itemId":"socks", "quantity":3}' -plaintext 127.0.0.1:8101 shoppingcart.ShoppingCartService.AddItem
   
    # get cart
    grpcurl -d '{"cartId":"cart2"}' -plaintext 127.0.0.1:8101 shoppingcart.ShoppingCartService.GetCart
   
    # update quantity of item
    grpcurl -d '{"cartId":"cart2", "itemId":"socks", "quantity":5}' -plaintext 127.0.0.1:8101 shoppingcart.ShoppingCartService.UpdateItem
   
    # check out cart
    grpcurl -d '{"cartId":"cart2"}' -plaintext 127.0.0.1:8101 shoppingcart.ShoppingCartService.Checkout
    ```
