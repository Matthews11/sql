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

# triggers 

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

# funciones 
-- funcion suma 
DELIMITER //
create function suma(num1 int, num2 int) returns int
begin
declare total int;
set total = num1+num2; 
return total;
end //

select suma(2,2);

drop function suma;


# plpgsql

# funciones y trigger
CREATE OR REPLACE FUNCTION public.edited_fecha_column()
  RETURNS trigger AS
$BODY$
BEGIN
    NEW. fecha_mod = now();
    RETURN NEW;	
END;
$BODY$
  LANGUAGE plpgsql;
  
  CREATE TRIGGER fecha_mod
  BEFORE UPDATE
  ON public.icv_cons
  FOR EACH ROW
  EXECUTE PROCEDURE public.edited_fecha_column();
  
  # procedimiento almacenado
  
  create procedure "public".insertar(ss varchar(40))
language plpgsql as $$
begin
insert into a (field) values (ss);
end $$

call "public".insertar('campo_3');
