# ParcialDos

## Función Validación de correo
Para hacer la petición desde postman se debe agregar en la ruta de URL "validar-correo/'correo'" 
(Ej. http://localhost:8080/validar-correo/ejemplo890@.com.co)

```
create or replace function validar_correo (
    correo in varchar2 )
    return varchar2 
is 
    regex_longitud VARCHAR2(100) := '^.{10,30}$';
    regex_primera_parte VARCHAR2(100) := '^[a-zA-Z0-9]+';
    regex_segunda_parte VARCHAR2(10) := '@';
    regex_tercera_parte VARCHAR2(10) := '\.com';
    regex_ultima_parte VARCHAR2(10) := '\.co$';
    primera_parte_correo VARCHAR2(100) := REGEXP_SUBSTR(correo,'[^@]+',1,1);

begin 
    IF NOT REGEXP_LIKE (primera_parte_correo, regex_longitud) OR
       NOT REGEXP_LIKE (correo, regex_primera_parte) OR 
       NOT REGEXP_LIKE (correo, regex_segunda_parte) OR 
       NOT REGEXP_LIKE (correo, regex_tercera_parte) OR 
       NOT REGEXP_LIKE (correo, regex_ultima_parte) THEN

        RETURN '" '|| correo || ' " No es una dirreccion de correo valida'; 
    ELSE
        RETURN '" '|| correo || ' " Si es una dirreccion de correo valida';
    END IF;
end;
```

## Función Validación multiplos de 3

Para hacer la petición desde postman se debe agregar en la ruta de URL "multiploTres/'numero'" 
(Ej. http://localhost:8080/multiploTres/100)

```
create or replace FUNCTION multiplo_tres (numero IN number)
return varchar2
is 
begin
    IF MOD(numero, 3) = 0 THEN
        RETURN numero || ' SI es multiplo de 3';
    ELSE
        RETURN numero || ' NO es multiplo de 3';
    END IF;
end;
```