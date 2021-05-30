# testMaven
test build project pake maven

DB

Create database
CREATE DATABASE hotel
Create table customer
CREATE TABLE public.customer (
    id int4 NOT NULL,
    id_card_number varchar(16) NULL,
    "name" varchar(255) NULL,
    place_of_birth varchar(255) NULL,
    date_of_birth date NULL,
    gender varchar(1) NULL,
    address varchar(255) NULL,
    CONSTRAINT customer_pk PRIMARY KEY (id)
);
Create table room category dan room type
CREATE TABLE public.room_category (
    id int4 NOT NULL,
    "name" varchar(15) NULL,
    description varchar(255) NULL,
    active bool NULL,
    created_by varchar(15) NULL,
    created_at timestamp NULL,
    CONSTRAINT room_category_pk PRIMARY KEY (id)
);
CREATE TABLE public.room_type (
    id int4 NOT NULL,
    room_category_id int4 NOT NULL,
    "name" varchar(15) NULL,
    description varchar(255) NULL,
    active bool NULL,
    created_by varchar NULL,
    created_at timestamp NULL,
    CONSTRAINT room_type_pk PRIMARY KEY (id)
);
ALTER TABLE public.room_type ADD CONSTRAINT room_type_fk FOREIGN KEY (room_category_id) REFERENCES room_category(id);
Create room stock dan room price
CREATE TABLE public.stock_room (
    id int4 NOT NULL,
    room_type_id int4 NOT NULL,
    stock_total int4 NULL,
    stock_available int4 NULL,
    stock_ordered int4 NULL,
    created_by varchar(15) NULL,
    created_at timestamp NULL,
    updated_by varchar(15) NULL,
    updated_at timestamp NULL,
    CONSTRAINT stock_room_pk PRIMARY KEY (id)
);
ALTER TABLE public.stock_room ADD CONSTRAINT stock_room_fk FOREIGN KEY (room_type_id) REFERENCES room_type(id);
CREATE TABLE public.price_room (
    id int4 NOT NULL,
    room_type_id int4 NOT NULL,
    price float8 NULL,
    discount float8 NULL,
    updated_by varchar(15) NULL,
    updated_at timestamp NULL,
    CONSTRAINT price_room_pk PRIMARY KEY (id)
);
ALTER TABLE public.price_room ADD CONSTRAINT price_room_fk FOREIGN KEY (room_type_id) REFERENCES room_type(id);
Create transaction history dan transaction history detail
CREATE TABLE public.transaction_history (
    id int4 NOT NULL,
    "number" varchar NULL,
    customer_id int4 NULL,
    created_by varchar(15) NULL,
    created_at timestamp NULL,
    CONSTRAINT transaction_history_pk PRIMARY KEY (id)
);

ALTER TABLE public.transaction_history ADD CONSTRAINT transaction_history_fk FOREIGN KEY (customer_id) REFERENCES customer(id);
CREATE TABLE public.transaction_history_detail (
    id int4 NOT NULL,
    transaction_history_id int4 NULL,
    room_type_id int4 NULL,
    room_ordered int4 NULL,
    quantity int4 NULL,
    price int4 NULL,
    created_by varchar NULL,
    created_at timestamp NULL,
    updated_by varchar NULL,
    updated_at timestamp NULL,
    CONSTRAINT transaction_history_detail_pk PRIMARY KEY (id)
);
ALTER TABLE public.transaction_history_detail ADD CONSTRAINT transaction_history_detail_fk FOREIGN KEY (transaction_history_id) REFERENCES transaction_history(id);
ALTER TABLE public.transaction_history_detail ADD CONSTRAINT transaction_history_detail_fk_1 FOREIGN KEY (room_type_id) REFERENCES room_type(id);

