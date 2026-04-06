# Day 1[MONDAY]

sellers[icon:user]{
  seller_id SERIAL PK,
  seller_name VARCHAR(50),
  email VARCHAR(322) unique not null,
  phone VARCHAR(12) unique,


}

customers[icon:user]{
  customer_id SERIAL PK,
  customer_name VARCHAR(50),
  email VARCHAR(322) unique not null,
  phone VARCHAR(12) unique,
  address TEXT,

  
}

products[icon:product]{
  product_id SERIAL PK,
  seller_id INT FK,
  product_name VARCHAR(20),
  product_type BOOLEAN(),//thrift or handmade
  number_of_product_remaining INT(3),
  size INT,
  color VARCHAR(10),
  about_condition TEXT,
  price INT,
  

}
orders[icon:order]{
  order_id SERIAL PK,
  customer_id INT FK,
  numberof_items INT,
  

}

orderitems[icon:orderitem]{
  orderitem_id SERIAL PK,
  order_id INT FK,
  product_id INT FK, 
  number_of_product INT,
  total_price INT ,

  ordered_at timestamp,
}

payments[icon:payment]{
  payment_id VARCHAR PK,
  order_id INT FK,
  paymented_at timestamp,
  payment_status BOOLEAN,
  payment_method VARCHAR(20),
  payment_amount INT,

}

shippings[icon: ship]{
  shipping_id VARCHAR pk,
  order_id INT FK,
  address TEXT,
  shipping_status boolean,//delivered or not
  delivered_at timestamp,

}

//one seller- many product
sellers.seller_id < products.seller_id

//one customer -many order
customers.customer_id < orders.customer_id

//one order -many orderiten
orders.order_id <orderitems.order_id

//one product-manyorderitem 
products.product_id <orderitems.product_id



//oneorder -1 payment
orders.order_id - payments.order_id


//1order -1 shipping
orders.order_id - shippings.order_id



