# mysql 
# creacion de tablas  

CREATE TABLE productos (
    id INT NOT NULL AUTO_INCREMENT,
    nombre VARCHAR(20) NOT NULL,
    estado VARCHAR(20) NOT NULL DEFAULT 'disponible',
    precio FLOAT NOT NULL DEFAULT 0.0,
    PRIMARY KEY(id),
    Foreign KEY(campo) REFERENCES tabla (campo);
);

drop table productos;
alter table productos add column apellido varchar(25);
alter table productos add constraint fk_productos foreign key (campo) references tabla(campo);

#inner join 
select * from productos as p inner join vendedor as v on p.id=v.id;
select * from productos as p inner join vendedor as v on p.id=v.id where id;

# procedimientos almacenados 
DELIMITER $$
create procedure insertar(in nombre varchar(255), in estado varchar(255), in precio int)
BEGIN 
insert into productos (nombre,estado,precio) values (nombre,estado,precio);
END$$

CALL insertar("tv","disponible",300);

drop procedure insertar;

#triggers

DELIMITER $$
create trigger mitabla_bu before|after insert|update|delete on miTabla for each row
BEGIN
SET @nombreViejo = OLD.nombre;
set @nombreNuevo = NEW.nombre;
END$$

DELIMITER $$
create trigger logg before insert on miTabla for each row
BEGIN 
insert into lo (usuario) value (CURRENT_USER());
END$$
