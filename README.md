# Delta-Lake-4.2
________________________________________________________________________________________________________________________________________________________________________________________________________________
1.	Creamos un catálogo; seleccionamos la pestaña de catalogo y hacemos click en +
   ![image](https://github.com/user-attachments/assets/fe612112-9186-4647-8bad-1b2da371ec60)

   ![image](https://github.com/user-attachments/assets/951e133f-08d8-4e9e-9a24-6fba24e11cc8)

  Luego en la ventana emergente solo haz click en siguiente (next) y en la siguiente ventana emergente guardar (save).

![image](https://github.com/user-attachments/assets/d158ffe0-d4c5-448c-a454-ef9edc75db5b)

![image](https://github.com/user-attachments/assets/bb337c12-b14e-4cdc-ba46-f7b5526e71d7)
   
Ahora vamos a espacio de trabajo y creamos una carpeta llamada DeltaLake4.0.

![image](https://github.com/user-attachments/assets/08433ff1-2fc7-40c4-90e8-11de0ee0cd82)

![image](https://github.com/user-attachments/assets/7116b31e-bcc1-40b3-b3ea-4af260262982)

Ahora creamos un cuaderno con nombre 1_deltalake.
    
![image](https://github.com/user-attachments/assets/b7d92305-052d-4aae-ba14-1b4af22120fc)

Luego hacemos click en el circulo verde que está en la parte superior izquierda y seleccionamos serverless.

![image](https://github.com/user-attachments/assets/b49a4ddf-d5f7-4517-94a8-8e29b74933ec)

Ahora creamos una tabla.

**Create Delta Table**

Using SQL API

sql:

     CREATE TABLE deltalakeall.default.first_table
     (
         id INT,
         salary INT
     )

Esto creará una tabla automáticamente.


![image](https://github.com/user-attachments/assets/e14926f7-384a-44ad-ba96-f6e877830dbe)

Ahora para trabajar con Delta Lake primero importamos DeltaTable.

Python:

        from delta.tables import DeltaTable


![image](https://github.com/user-attachments/assets/79dca89b-2018-4058-b0ab-0cdfab90f1fd)

Vamos a la documentación de Delta API 

![image](https://github.com/user-attachments/assets/52fb14fb-1ac4-4ebf-8856-09ce4fdb06af)

Vamos a conector apache spark

![image](https://github.com/user-attachments/assets/5f363850-47a8-4a7d-ba0e-ae0ee337663a)

Luego bajamos hasta la sección DeltaTableBuilder.

![image](https://github.com/user-attachments/assets/21e0540a-50ef-4ca1-b33d-c47b2f0972fd)

Luego pegamos lo seleccionado en una celda de Databricks.

![image](https://github.com/user-attachments/assets/19e41680-4a1c-4783-b0c3-178a0a33685b)

Luego para mantener la misma estructura del ejemplo anterior, quitamos las filas que están demás.

![image](https://github.com/user-attachments/assets/49bd28d0-95aa-40c3-978a-d5c01b4b33ec)

![image](https://github.com/user-attachments/assets/95f2eff1-d951-4d86-972d-878f3f419343)

Luego cambiamos el nombre de la tabla.

![image](https://github.com/user-attachments/assets/eb103281-53dc-4130-a23a-f63821ab565b)

El código final es el siguiente:

Código:

        DeltaTable.createIfNotExists(spark) \
          .tableName("deltalakeall.default.firstdeltaapi") \
          .addColumn("id", "INT") \
          .addColumn("salary", "INT") \
          .execute()

Y finalmente lo ejecutamos.


![image](https://github.com/user-attachments/assets/57c1673f-b6b5-49e3-a50a-4b7558020dd7)

Ahora podemos ver que ya tenemos las dos tablas, la que se acaba de ejecutar (firstdeltaapi) y la anterior (first_table)

![image](https://github.com/user-attachments/assets/6cef1abf-2b0c-4f54-ab59-b934e0751857)

Ahora para verificar que se haya creado bien; vamos a catalogo y buscamos el archivo deltalakeall, luego hacemos click en la tabla firstdeltaapi y luego a detalles.

![image](https://github.com/user-attachments/assets/de485596-d3ad-46a9-985b-7d639997ca50)

Ahora eliminamos la tabla para desarrollar el siguiente tema bajo el mismo concepto.

sql:

      DROP TABLE deltalakeall.default.firstdeltaapi


![image](https://github.com/user-attachments/assets/19280c43-b15a-48ed-a941-1e592478b04c)

## GENERATED COLUMNS

Identity Columns

![image](https://github.com/user-attachments/assets/dd91a66a-beb9-4ab4-aeff-b75da9315664)

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()
