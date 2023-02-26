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
    gender        char(1),
    date_of_birth varchar(15),
    created_at    datetime,
    country_code  int,
    foreign key (country_code) references countries (code),
    Gender        varchar(1) check ( Gender = 'M' or Gender = 'F' )

);
create table orders
(
    id         int(10) primary key,
    user_id    int,
    status     varchar(6),
    created_at datetime,
    Status     varchar(6) check ( Status = 'start' or Status = 'finish' ),
    foreign key (user_id) references users (id)
);

create table order_products
(
    order_id   int(10) primary key,
    product_id int(10) primary key,
    quantity   int default 0,
    foreign key (order_id) references orders (id),
    foreign key (product_id) references products (id)
);

create table products
(
    id         int(10),
    name       varchar(10) not null,
    price      int default 0,
    status     varchar(10),
    created_at datetime,
    Status     varchar(10) check ( Status = 'valid' or Status = 'expired' )
);

ALTER TABLE orders
    ADD COLUMN created_at TIMESTAMP;
ALTER TABLE orders
    ALTER COLUMN created_at SET DEFAULT now();
ALTER TABLE users
    ADD COLUMN created_at TIMESTAMP;
ALTER TABLE users
    ALTER COLUMN created_at SET DEFAULT now();

#DML
insert into countries
values (300, 'Jeddah', 'Asia');
insert into users
values (1, 'alaa abdullah alghamdi', 'alaa@gmail.com', 'f', '19-1-1999', '3-2-2023', 66);
insert into orders
values (22, 1234, 'start', '2-9-2022');
insert into products
values (505, 'book', 332, 'valid', '5-5-2023');
insert into order_products
values (565, 787, 45);
select * from countries;


UPDATE countries
SET
    name='Taif'
WHERE code=300;
DELETE FROM
           products
WHERE id=505;
