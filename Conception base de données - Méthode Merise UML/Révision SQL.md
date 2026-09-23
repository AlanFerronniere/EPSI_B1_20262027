# Prérequis

Petite révision de SQL faite sur la BDD d'exemple Northwind.
Téléchargeable ici : https://github.com/busynovadad/northwind-MySQL

1. Téléchargez northwind.sql
2. Téléchargez northwind-data.sql
3. Exécutez les sur votre server MySQL dans cet ordre.

# Requetes faite pendant cette révision


```mysql
#Select simple  
select * from customers  
where country_region='USA';  
  
#join  
select o.id as NumCommande, o.order_date, c.company  
from orders o right join customers c on o.customer_id=c.id  
where o.id is null;  
  
  
  
#autre join  
select o.id,s.company from orders o join shippers s on s.id=o.shipper_id  
  
select s.company from orders o join shippers s on s.id=o.shipper_id  
where o.id is null;  
  
#Andrew Cencini  
select * from orders o join employees e on o.employee_id=e.id  
where e.first_name='Andrew' and e.last_name='Cencini';  
  
#en partant de ça, on liste les clients d'Andrew Cencini  
select distinct c.company, o.id from orders o  
join employees e on o.employee_id=e.id  
join customers c on o.customer_id=c.id  
where e.first_name='Andrew' and e.last_name='Cencini';  
  
#on fait la liste des produits commandés dans ces commandes  
select distinct p.product_name from products p  
join order_details od on p.id=od.product_id  
join orders o on od.order_id=o.id  
join employees e on o.employee_id=e.id  
where e.first_name='Andrew' and e.last_name='Cencini';  
  
#liste des produits jamais commandés  
select p.product_name from products p  
left join order_details od on p.id=od.product_id  
where od.id is null;  
  
#agrrégation  
select count(*) from products p  
left join order_details od on p.id=od.product_id  
where od.id is null;  
  
#group by  
select city, id from customers order by city;  
  
select city, count(*) from customers  
group by city;  
  
#prix moyen des produits par catégorie  
select p.category, avg(p.list_price) as AvgPrice  
from products p  
group by p.category;  
  
#Nombre de commandes par client  
#Attention aux clients sans commande  
#Et attention à count() qui compte les lignes  
select c.company, count(o.id) as NbCommandes  
from customers c left join orders o on c.id=o.customer_id  
group by c.company;  
  
select count(*) from orders  
  
#prix total de chaque commande  
select od.order_id, sum(od.unit_price * od.quantity *(1 - od.discount)) as TotalPrice  
from order_details od  
group by od.order_id;  
  
#prix total par company du client  
select c.company, ifnull(sum(od.unit_price * od.quantity *(1 - od.discount)),0) as TotalPrice  
from customers c  
left join orders o on c.id=o.customer_id  
left join order_details od on o.id=od.order_id  
group by c.company;  
  
#quel est l'employé qui a généré le plus de chiffre d'affaires ?  
select e.first_name, e.last_name, ifnull(sum(od.unit_price * od.quantity *(1 - od.discount)),0) as TotalSales  
from employees e  
join orders o on e.id=o.employee_id  
join order_details od on o.id=od.order_id  
group by e.id  
order by TotalSales desc  
limit 1;  
  
#Quelle est la catégorie de produit la plus vendue  
#(en quantité) à des clients de Chicago ?  
select p.category, sum(od.quantity) as TotalQuantity  
from products p  
join order_details od on p.id=od.product_id  
join orders o on od.order_id=o.id  
join customers c on o.customer_id=c.id  
where c.city='Chicago'  
group by p.category  
order by TotalQuantity desc  
limit 1;  
  
#having : un where après le group by  
select city, count(*) from customers  
group by city  
having count(*)>2  
order by city;  
  
#  
select c.company, ifnull(sum(od.unit_price * od.quantity *(1 - od.discount)),0) as TotalPrice  
from customers c  
left join orders o on c.id=o.customer_id  
left join order_details od on o.id=od.order_id  
group by c.company  
having TotalPrice>2000;  
  
#union  
select company from customers  
union  
select company from shippers  
union  
select company from suppliers;  
  
#le nom prénom email de tous les gens qui sont dans la BDD  
#dans customers, employees, suppliers, shippers  
select first_name, last_name, email_address from employees  
union  
select first_name, last_name, email_address from customers  
union  
select first_name, last_name, email_address from suppliers  
union  
select first_name, last_name, email_address from shippers  
  
#sous requete : par exe
mple  
select * from customers where id not in (select customer_id from orders)
```