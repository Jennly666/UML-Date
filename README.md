В данной работе была описана деятельность магазина Shop, который: имеет свое название name, адрес adress, ассортимент assortment, обладает возможностью закупать продукты add(product: Product) и включает в себя кассиров Cashier. Кассиры Cashier и покупатели Supplier наследуют имя name и возраст age от класса Human. По этой причине в дальнейшем описании эти атрибуты повторять не будем. Кассиры могут продавать продукты sellProduct(product: Product) (вычитают продукты из ассортимента) и создавать чек Check методом createCheck(cart: cart): Check. Продавцы в свою же очередь имеют атрибут корзины cart : List<Product>, состоящего из множества продуктов Product, который пополняется методом addProduct(product: Product) или вычитается методом delProduct(product: Product), и обладают возможностью получить чек Check. Чек принимает на вход корзину cart и возвращает стоимость корзины, благодаря методу calcTotal(cart: cart): Float. Сам же класс Product включает в себя атрибуты: price, weight, count, названия которые говорят за себя. 

![Uploading aaa.drawio (1).png…]()

