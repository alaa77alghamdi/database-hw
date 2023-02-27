# database-hw
![store](https://user-images.githubusercontent.com/98323604/221439906-a36bf96c-426f-4b05-a351-29c73a98c2f8.png)






create database store;

create table countries
(
    code           int(10) primary key,
    name           varchar(20) unique,
    continent_name varchar(20) not null

);

create table users
(
    id            int(10) primary key,
    full_name     varchar(20),
    email         varchar(20) unique,
    gender        char(1) check ( gender = 'M' or gender = 'F' ),
    date_of_birth varchar(15),
    created_at    datetime,
    country_code  int(10),
    foreign key (country_code) references countries (code)


);
create table orders
(
    id         int(10) primary key,
    user_id    int (10),
    status     varchar(6) check ( status = 'start' or status = 'finish' ),
    created_at datetime,

    foreign key (user_id) references users (id)
);

create table order_products
(
    order_id   int(10) ,
    product_id int(10) ,
    quantity   int default 0,
    foreign key (order_id) references orders(id),
     foreign key (product_id) references products(id)
);

create table products
(
    id         int(10) primary key ,
    name       varchar(10) not null,
    price      int default 0,
    status     varchar(10) check ( status = 'valid' or status = 'expired' ),
    created_at datetime

);




#DML
insert into countries values (300, 'Jeddah', 'Asia');
insert into users values (1, 'alaa alghamdi', 'alaa@gmail.com', 'f', '19-1-1999', '2022/7/2', 300);
insert into orders values (22, 1, 'start', '2022/9/2');
insert into products values (505, 'book', 332, 'valid', '2023/5/6');
insert into order_products values (22,505,100);

select * from countries;
select * from users;
select * from products;

UPDATE countries
SET
    name='Taif'
WHERE code=300;
DELETE FROM
           products
WHERE id=505;

