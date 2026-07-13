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

Python:

        from pyspark.sql.functions import *
        from pyspark.sql.types import *
        from delta.tables import DeltaTable, IdentityGenerator


![image](https://github.com/user-attachments/assets/51388639-8bce-4c85-addc-0bdd9df87db7)

Código:

        DeltaTable.create(spark) \
           .tableName("deltalakeall.default.firstdeltaapi") \
           .addColumn("id_col", dataType=LongType(), generatedAlwaysAs=IdentityGenerator()) \
           .addColumn("salary", dataType=IntegerType()) \
           .addColumn("name", dataType=StringType()) \
           .execute()


![image](https://github.com/user-attachments/assets/72eed384-f584-449a-a2df-ad2117027f2c)

___________________________________________________________________________________________________________________________________________________________________________________________________________________________
### 📚 Visión General

Este código crea una tabla Delta Lake llamada deltalakeall.default.firstdeltaapi con 3 columnas, donde una de ellas (id_col) es una columna de identidad auto-incremental (como un IDENTITY en SQL Server o AUTO_INCREMENT en MySQL).
__________________________________________________________________________________________________________
🔍 Desglose Línea por Línea

Línea 1: Inicio de la construcción

Código:
               
         DeltaTable.create(spark) \

**Explicación:**

| Componente | Significado |
|------------|-------------|
| DeltaTable | Clase principal de Delta Lake para interactuar con tablas (crear, leer, actualizar, etc.) |
| .create() | Método estático que inicia el proceso de creación de una nueva tabla Delta |
| spark | La sesión de Spark activa (necesaria para ejecutar operaciones en el cluster) |
| \ | Carácter de continuación en Python (permite escribir el código en varias líneas) |


📌 Equivalente a: "Quiero crear una nueva tabla Delta usando la sesión de Spark que ya tengo activa."

_____________________________________________________________________________________________________________
Línea 2: Nombre de la tabla

python:

        .tableName("deltalakeall.default.firstdeltaapi") \


**Explicación:**

| Componente | Significado |
|------------|-------------|
| .tableName() | Método que define el nombre de la tabla en el catálogo (Hive Metastore / Unity Catalog) |
| "deltalakeall.default.firstdeltaapi" | Nombre completo de la tabla (3 niveles) |


**Estructura del nombre:**

![image](https://github.com/user-attachments/assets/41cab9d0-91ee-43c5-9573-3ef65c200522)

___________________________________________________________________________________________________________________
📌 Equivalente a: "La tabla se llamará firstdeltaapi dentro del esquema default del catálogo deltalakeall."

En Databricks Unity Catalog, el formato es:

<catalog_name>.<schema_name>.<table_name>
__________________________________________________________________________________________________________________
Línea 3: Columna ID (Auto-incremental)

python:

        .addColumn("id_col", dataType=LongType(), generatedAlwaysAs=IdentityGenerator()) \


**Explicación:**

| Componente | Significado |
|------------|-------------|
| .addColumn() | Método que agrega una nueva columna a la tabla |
| "id_col" | Nombre de la columna |
| dataType=LongType() | Tipo de dato: LongType (entero de 64 bits) |
| generatedAlwaysAs=IdentityGenerator() | Configuración clave: Define que esta columna es una columna de identidad |


¿Qué hace IdentityGenerator()?

python:

        IdentityGenerator()

        
•	📌 Equivalente a SQL: GENERATED ALWAYS AS IDENTITY

•	📌 Comportamiento:

 o	✅ Los valores se generan automáticamente al insertar datos

 o	✅ No puedes insertar manualmente valores en esta columna (es generada siempre)

 o	✅ Comienza en 1 y se incrementa de 1 en 1 (por defecto)

 o	✅ Garantiza unicidad y secuencia (ideal para claves primarias)


Alternativas a IdentityGenerator():

Si quisieras permitir insertar valores manuales

python:

         generatedAlwaysAs=IdentityGenerator(start=1, step=1, allowExplicitInsert=True)
         

📌 Equivalente a: "Crea una columna llamada id_col que sea un número entero largo (LongType) y que se genere automáticamente como una secuencia de identidad, como un auto-incremental en bases de datos tradicionales."
________________________________________________________________________________________________________________________________________
Línea 4: Columna Salary

python:

        .addColumn("salary", dataType=IntegerType()) \

        
**Explicación:**

| Componente | Significado |
|------------|-------------|
| .addColumn() | Agrega otra columna |
| "salary" | Nombre de la columna |
| dataType=IntegerType() | Tipo de dato: IntegerType (entero de 32 bits) |

📌 Equivalente a: "Crea una columna llamada salary que almacene números enteros (IntegerType) para representar el salario."

Nota: Esta columna no es auto-generada; tendrás que proporcionar valores al insertar.
_______________________________________________________________________________________________________________________________________
Línea 5: Columna Name

python:

        .addColumn("name", dataType=StringType()) \

**Explicación:**

| Componente | Significado |
|------------|-------------|
| .addColumn() | Agrega otra columna |
| "name" | Nombre de la columna |
| dataType=StringType() | Tipo de dato: StringType (cadena de texto) |


📌 Equivalente a: "Crea una columna llamada name que almacene texto (StringType) para el nombre de la persona."
______________________________________________________________________________________________________________________________________
Línea 6: Ejecutar la creación

python:

        .execute()
        
**Explicación:**

| Componente | Significado |
|------------|-------------|
| .execute() | Método que finalmente ejecuta la creación de la tabla en el catálogo de Spark |


📌 Equivalente a: "¡Ejecuta todos los pasos anteriores y crea la tabla en el metastore de Hive/Unity Catalog!"

____________________________________________________________________________________________________________________________________
**📊 Resultado: La Tabla Creada**

Esquema de la Tabla:

| Columna | Tipo | Descripción |
|---------|------|-------------|
| id_col | BIGINT (LongType) | Auto-generado (IDENTITY), clave primaria |
| salary | INT (IntegerType) | Salario del empleado |
| name | STRING (StringType) | Nombre del empleado |


Propiedades de la Tabla:

sql:

     -- Equivalente en SQL
     CREATE TABLE deltalakeall.default.firstdeltaapi (
         id_col BIGINT GENERATED ALWAYS AS IDENTITY,
         salary INT,
         name STRING
     )
     USING DELTA;
____________________________________________________________________________________________________________________________________

💡 Insertar Datos en Esta Tabla

✅ Correcto (No especificas id_col)

python:

        --# INSERT: No incluyes id_col porque se genera automáticamente
        spark.sql("""
            INSERT INTO deltalakeall.default.firstdeltaapi (salary, name)
            VALUES 
                (50000, 'Juan Pérez'),
                (60000, 'María García'),
                (55000, 'Carlos López')
       """)



 **Resultado:**

* id_col = 1, salary = 50000, name = 'Juan Pérez'

*  id_col = 2, salary = 60000, name = 'María García'

* id_col = 3, salary = 55000, name = 'Carlos López'

❌ Incorrecto (Intentas insertar id_col manualmente)

python:

        --# ERROR: No puedes insertar en id_col porque es GENERATED ALWAYS
        spark.sql("""
            INSERT INTO deltalakeall.default.firstdeltaapi (id_col, salary, name)
            VALUES (100, 50000, 'Juan Pérez')
        """)
        
 ❌ Error: Column 'id_col' is an identity column and cannot be specified

____________________________________________________________________________________________________________________________________________________________________________________________________________________________
### Compute Columns

![image](https://github.com/user-attachments/assets/06250e26-5fcb-436b-9b1f-5917a1fbfa3a)

Código:

        DeltaTable.createOrReplace(spark) \
          .tableName("deltalakeall.default.firstdeltaapi") \
          .addColumn("salaryAfterTax", dataType=DecimalType(12, 1), generatedAlwaysAs="salary * 0.7") \
          .addColumn("salary", dataType=IntegerType()) \
          .addColumn("name", dataType=StringType()) \
          .execute()


![image](https://github.com/user-attachments/assets/a6b0bcee-68fe-4323-8f4e-838e594cb952)

sql:

     INSERT INTO deltalakeall.default.firstdeltaapi(salary,name)
     VALUES
     (100,'aa'),
     (200,'bb')


![image](https://github.com/user-attachments/assets/0d9feea3-6687-4f36-a362-a5b41203afc5)

Código:
                
        select * from deltalakeall.default.firstdeltaapi


![image](https://github.com/user-attachments/assets/aee7a075-030a-4975-b877-93f8e81ed6d9)

Ahora vamos a crear un volumen, para ello vamos a catalogo, luego seleccionamos deltalakeall y dentro de ella default, luego hacemos click en crear de la ventana desplegable seleccionamos volumen y le signamos un nombre (deltavol).

![image](https://github.com/user-attachments/assets/7e175598-fbef-48ee-ab81-e73c1a7bdd6f)

Luego vamos a workspace y creamos un nuevo notebook.

No olvidar enceder el servidor.

![image](https://github.com/user-attachments/assets/13ed0bfd-69a3-4124-acfb-0a77db808329)

___________________________________________________________________________________________________________________________________________________________________________________________________________________________
### Delta Log

Pasamos el siguiente código en la celda.

Python:

        data = [(1, 100, 'aa'),(2, 200, 'bb'),(3, 300, 'cc'),(4, 400, 'dd')]
        df = spark.createDataFrame(data, ['id', 'salary', 'name'])
        display(df)


![image](https://github.com/user-attachments/assets/1a6ff7ee-501b-4336-a09c-fc9a86de7d72)

Ahora creamos un directorio en deltavol

![image](https://github.com/user-attachments/assets/85b61548-9213-46fb-a725-f58d3ba960d9)

/Volumes/deltalakeall/default/deltavol/demosink/

![image](https://github.com/user-attachments/assets/cf3a0b96-7759-45ab-912c-269266929357)

Ahora volvemos al notebook

Python:

        df.write.format("delta")\
            .mode("append")\
            .save("/Volumes/deltalakeall/default/deltavol/demosink/")


![image](https://github.com/user-attachments/assets/7501e02d-51f0-4ae7-9310-646a7e02e60f)

Luego comprobamos que se guardado.

![image](https://github.com/user-attachments/assets/f337a145-ef6a-48bc-8f29-f0164c6b965a)

Ahora leeremos los datos.

Python:

        df = spark.read.format('json')\
            .load('/Volumes/deltalakeall/default/deltavol/demosink/_delta_log/00000000000000000001.json')
        display(df)



![image](https://github.com/user-attachments/assets/d2f61a51-9ae4-4e52-8471-c362a876225e)

Ahora creamos un nuevo cuaderno (3_deltalake).

Schema Enforcement

Código:

        data = [(1, 100, 'aa', 1),(2, 200, 'bb', 1),(3, 300, 'cc', 1),(4, 400, 'dd', 1)]
        df = spark.createDataFrame(data, ['id', 'salary', 'name', 'sus_col'])
        display(df)


![image](https://github.com/user-attachments/assets/ef05db29-3f36-44a1-afec-cca40c4527a5)

El sistema delta no permitirá guardar datso de este esquema.

Schema Evolution

Código:

        df.write.format("delta")\
                .mode("append")\
                .option("mergeSchema", True)\  #merge fusiona el esquema
                .save("/Volumes/deltalakeall/default/deltavol/demosink/")

Reading data with Data Lake

sql:

     SELECT * FROM delta.`/Volumes/deltalakeall/default/deltavol/demosink/`


![image](https://github.com/user-attachments/assets/a2d31e52-1eb8-4053-a6f2-7685a63bd6c9)

Schema Overwrite

Código:

        data = [(1, 100, 'aa', 1),(2, 200, 'bb', 1),(3, 300, 'cc', 1),(4, 400, 'dd', 1)]
        df = spark.createDataFrame(data, ['cust_id', 'income', 'name', 'tip'])
        display(df)


![image](https://github.com/user-attachments/assets/e6518ed5-b607-4f89-a270-f65a1a4b11ed)

Código:

        df.write.format("delta")\
                .mode("overwrite")\
                .option("overwriteSchema", True)\
                .save("/Volumes/deltalakeall/default/deltavol/demosink/")


![image](https://github.com/user-attachments/assets/56400996-1398-4128-a2e2-bc652b5207cd)

Código:

        SELECT * FROM delta.`/Volumes/deltalakeall/default/deltavol/demosink/`

Después de este código podremos ver que ya se sobrescribió esta nueva tabla sobre la anterior.

* Nueva tabla

![image](https://github.com/user-attachments/assets/f4bd9e34-7e97-4603-af91-274502495ee4)

* Anterior tabla.

![image](https://github.com/user-attachments/assets/4d8d3c71-bdfb-49fa-82dd-9330407843f3)

•	Ahora creamos un nuevo cuaderno (4_deltalake)

Nos vamos a catalogo y creamos un nuevo directorio en deltavol, llamado dmlsink 


![image](https://github.com/user-attachments/assets/a8d9eee7-4f18-42f2-ba10-07261da2613c)

![image](https://github.com/user-attachments/assets/191efdb5-512b-48b6-a124-82f05b9177ca)

____________________________________________________________________________________________________________________________________________________________________________________________________________________________
### DML
____________________________________________________________________________________________________________________________________________________________________________________________________________________________

Python:

        data = [(1, 100, 'aa', 1),(2, 200, 'bb', 1),(3, 300, 'cc', 1),(4, 400, 'dd', 1)]
        df = spark.createDataFrame(data, ['cust_id', 'income', 'name', 'tip'])

        df.write.format("delta")\
                .mode("append")\
                .save("/Volumes/deltalakeall/default/deltavol/dmlsink/")


![image](https://github.com/user-attachments/assets/d03c4141-a07b-420d-92a7-29d4d1d7745f)

•	Ahora vamos que sucede si modificamos la numeración del set de datos.

Python:

        data = [(5, 100, 'aa', 1),(6, 200, 'bb', 1),(7, 300, 'cc', 1),(8, 400, 'dd', 1)]
        df = spark.createDataFrame(data, ['cust_id', 'income', 'name', 'tip'])

        df.write.format("delta")\
                .mode("append")\
                .save("/Volumes/deltalakeall/default/deltavol/dmlsink/")

•	Luego mostramos la tabla.

sql:

     SELECT * FROM delta.`/Volumes/deltalakeall/default/deltavol/dmlsink/`


![image](https://github.com/user-attachments/assets/3f5e8eab-9b8b-49c9-aae6-4bfdff741de7)

Verificamos la creación en el volumes/deltavol/dmlsink

![image](https://github.com/user-attachments/assets/c0d9ec85-94cb-4fd3-ba1d-527c5c13b2e5)

_________________________________________________________________________________________________________________________________________
### UPDATE

sql:

     UPDATE delta.`/Volumes/deltalakeall/default/deltavol/dmlsink/` 
     SET income = 100 WHERE cust_id = 5


![image](https://github.com/user-attachments/assets/8b75e8c1-6d51-4330-8fad-59092bc0c326)

%sql:

      SELECT * FROM delta.`/Volumes/deltalakeall/default/deltavol/dmlsink/`


![image](https://github.com/user-attachments/assets/6082083f-02fe-4cce-b8cc-24fe5dc8c8b5)

____________________________________________________________________________________________________________________________________________
### UPSERT

Pyhton:

        data = [(1, 100, 'xyz', 1),(9, 200, 'bb', 1),(10, 300, 'cc', 1)]
        df = spark.createDataFrame(data, ['cust_id', 'income', 'name', 'tip'])
        display(df)


![image](https://github.com/user-attachments/assets/caa92dd7-3865-46b7-bc43-c875eb6e0cde)

Python:

from delta.tables import DeltaTable 


Pyhton:

        dlt_obj = DeltaTable.forPath(spark, "/Volumes/deltalakeall/default/deltavol/dmlsink/")

        dlt_obj.alias("trg").merge(df.alias("src"), "trg.cust_id = src.cust_id")\
            .whenMatchedUpdateAll()\
            .whenNotMatchedInsertAll()\
            .execute()


![image](https://github.com/user-attachments/assets/d4a67c75-b5e8-4382-b6f0-1b02a2286ebd)

**🎯 EXPLICACION DEL CODIGO.**

"Actualiza o inserta registros en la tabla Delta dependiendo de si ya existen o no"
__________________________________________________________________________________________________________________________________________________________________________________________________________
**🔍 Desglose Rápido**

| Línea | Significado |
|-------|-------------|
| DeltaTable.forPath(spark, "/Volumes/...") | Carga la tabla Delta existente desde una ruta específica |
| .alias("trg") |	La tabla se llamará "trg" (target/destino) en la operación |
| .merge(df.alias("src"), "trg.cust_id = src.cust_id") | Combina el DataFrame con la tabla usando cust_id como clave de comparación |
| .whenMatchedUpdateAll() | Si el registro YA EXISTE (coincide la clave), ACTUALIZA todos los campos |
| .whenNotMatchedInsertAll() | Si el registro NO EXISTE (no coincide la clave), INSERTA un nuevo registro |
| .execute() | Ejecuta la operación |

sql:
                
         SELECT * FROM delta.`/Volumes/deltalakeall/default/deltavol/dmlsink/`


![image](https://github.com/user-attachments/assets/c715ef3f-57bf-4c86-a25e-c7be973b03ec)

Ahora creamos un nuevo directorio.

![image](https://github.com/user-attachments/assets/691da364-2093-4498-bc38-cf4b3a5d6338)

Y creamos un nuevo cuaderno llamado 5_deltalake.

Python:
       
        data = [(1, 100, 'xyz', 1),(9, 200, 'bb', 1),(10, 300, 'cc', 1)]
        df = spark.createDataFrame(data, ['cust_id', 'income', 'name', 'tip'])
        display(df)


![image](https://github.com/user-attachments/assets/20263db2-484d-44c9-b4d6-906ff44c2adb)

Python:

        df.write.format("delta")\
            .mode("append")\
            .save("/Volumes/deltalakeall/default/deltavol/schemalevel")


![image](https://github.com/user-attachments/assets/e5504c1a-9684-4744-bf5d-2c1450bd50ab)

Verificamos que haya sido creado.

![image](https://github.com/user-attachments/assets/727d71b8-09e0-4540-ba06-c68697a8c7bc)

%sql:

      -- Enable column mapping first
      ALTER TABLE delta.`/Volumes/deltalakeall/default/deltavol/schemalevel/`
      SET TBLPROPERTIES ('delta.columnMapping.mode' = 'name');

      -- Now rename the column
      ALTER TABLE delta.`/Volumes/deltalakeall/default/deltavol/schemalevel/`
      RENAME COLUMN name TO customer_name

![image](https://github.com/user-attachments/assets/8b5e48fc-1686-436b-83e0-6c3ff5bb5412)

sql:

     SELECT * FROM delta.`/Volumes/deltalakeall/default/deltavol/schemalevel/`


![image](https://github.com/user-attachments/assets/2d02970a-5f2f-4b4a-918b-093580503a87)

Python:

        df = spark.read.format("json")\
                    .load("/Volumes/deltalakeall/default/deltavol/schemalevel/_delta_log/00000000000000000002.json")
        display(df)


![image](https://github.com/user-attachments/assets/883b0139-036b-44d7-b0d2-fcfeae9e29a0)

__________________________________________________________________________________________________________________________________________________________________________________________________________________________
### TABLE UTILITY COMMANDS

sql:

     DESCRIBE deltalakeall.default.first_table


![image](https://github.com/user-attachments/assets/d03a3d90-6cb1-48ae-8b23-7a1a6a622897)

Ahora otra forma de describir la tabla.

sql:

     DESCRIBE EXTENDED deltalakeall.default.first_table


![image](https://github.com/user-attachments/assets/c5c09350-504a-4da1-a745-8ae51ab9f7e3)

Ahora pasaremos a ver historiales.

SQL:

     DESCRIBE HISTORY delta.`/Volumes/deltalakeall/default/deltavol/dmlsink/`


![image](https://github.com/user-attachments/assets/4e04486f-a91e-4a68-a2c9-8fd1de8fd781)

sql:

     RESTORE delta.`/Volumes/deltalakeall/default/deltavol/dmlsink/`
     TO VERSION AS OF 5


![image](https://github.com/user-attachments/assets/76d0701c-c21e-4061-9477-858302ebb255)

sql:

     SELECT * FROM delta.`/Volumes/deltalakeall/default/deltavol/dmlsink/`
     VERSION AS OF 5


![image](https://github.com/user-attachments/assets/31d3de98-8494-46a8-989e-ae7527e57937)

____________________________________________________________________________________________________________________________________________________________________________________________________________________________
### Viajar en el tiempo.

%sql:

      SELECT * FROM delta.`/Volumes/deltalakeall/default/deltavol/dmlsink/`
      TIMESTAMP AS OF '2026-07-02T00:32:37.000+00:00'


![image](https://github.com/user-attachments/assets/69d8aa99-6e5a-4fc9-a461-b10bca0f05a9)

%sql:

      SHOW TBLPROPERTIES deltalakeall.default.first_table


![image](https://github.com/user-attachments/assets/f97b07ed-d84c-49c1-9c8b-da8de9d78d67)

%sql:

      SHOW TBLPROPERTIES delta. `/Volumes/deltalakeall/default/deltavol/dmlsink`


![image](https://github.com/user-attachments/assets/8d17543e-a1af-489d-9b91-5eb8b6b53d95)

__________________________________________________________________________________________________________________________________________________________________________________________________________________________
### Vaciar datos

sql:

     VACUUM delta. `/Volumes/deltalakeall/default/deltavol/dmlsink/` RETAIN 0 HOURS
_________________________________________________________________________________________________________________________________________________________________________________________________________________________
### Clonación profunda.

![image](https://github.com/user-attachments/assets/4e5b81f2-52c7-42ee-8e0e-4dc7cb08b1ea)

__________________________________________________________________________________________________________________________________________________________________________________________________________________________
### Clonación Superficial

%sql:

      CREATE TABLE deltalakeall.default.clonetblshallow
      SHALLOW CLONE deltalakeall.default.first_table


![image](https://github.com/user-attachments/assets/dee78171-0d81-4c92-a17e-d3ed8745b004)

___________________________________________________________________________________________________________________________________________________________________________________________________________________________
### UNIFROM

sql:

     CREATE TABLE IF NOT EXISTS deltalakeall.default.clonetbl
     USING DELTA TBLPROPERTIES(
         'delta.enableIcebergCompatV2' = 'true',
         'delta.universalFormat.enabledFormats' = 'iceberg'
     );


![image](https://github.com/user-attachments/assets/7c44dae4-13dd-4a21-80c8-631ab1accf2a)

____________________________________________________________________________________________________________________________________________________________________________________________________________________________
### OPTIMIZATION

Creamos un nuevo directorio en volumes

![image](https://github.com/user-attachments/assets/c95cf775-2241-418d-a408-ead6fce30353)

Creamos un dataframe.

Python:

        df = spark.read.table("deltalakeall.default.clonetbl")


![image](https://github.com/user-attachments/assets/af11e740-f273-4ba2-b17e-2fec1302d501)

Python:

        Display(df)


![image](https://github.com/user-attachments/assets/7a7ec20e-e6d4-440a-80de-a53b7a4014a1)

Python:

        df.write.format("delta").mode("append").save("/Volumes/deltalakeall/default/deltavol/optimization")


![image](https://github.com/user-attachments/assets/69cf9ad8-ad13-4048-a536-169b39ec1beb)

Luego de dar play 3 veces, veremos los archivos en volúmenes.

![image](https://github.com/user-attachments/assets/845feff4-9a84-4d9d-b4d9-668fa0bc6afd)

Ahora lo optimizaremos.

sql:

     OPTIMIZE delta.`/Volumes/deltalakeall/default/deltavol/optimization/`


![image](https://github.com/user-attachments/assets/6f97111d-f86c-44dc-b46e-6a9420aadadd)

sql:

     DESCRIBE HISTORY delta.`/Volumes/deltalakeall/default/deltavol/optimization`


![image](https://github.com/user-attachments/assets/2e107189-a200-4e69-ac07-17ee67933c43)

Luego veremos el cuarto archivo optimizado.

![image](https://github.com/user-attachments/assets/413ba883-b90b-4c9e-870a-5541779e1b40)

____________________________________________________________________________________________________________________________________________________________________________________________________________________________
### ZORDER

sql:

     SELECT * FROM delta.`/Volumes/deltalakeall/default/deltavol/optimization`


![image](https://github.com/user-attachments/assets/30060427-f1b9-4706-9337-0ebea9e3479e)

sql:

     SELECT * FROM delta.`/Volumes/deltalakeall/default/deltavol/optimization`
     WHERE cust_id = 1


![image](https://github.com/user-attachments/assets/8a49d98d-485f-4151-beed-663accbbd90e)

sql:

     OPTIMIZE delta.`/Volumes/deltalakeall/default/deltavol/optimization/` ZORDER BY (cust_id)


![image](https://github.com/user-attachments/assets/e48052c2-dabd-4593-881a-36574463b3b0)

____________________________________________________________________________________________________________________________________________________________________________________________________________________________
### LIQUID CLUSTERING

sql:

     ALTER TABLE deltalakeall.default.clonetbl
     CLUSTER BY (cust_id)

![image](https://github.com/user-attachments/assets/47b6ecf5-d6b7-4e75-a90d-ef60dbcc5a1a)


sql:

     ALTER TABLE deltalakeall.default.clonetbl
     CLUSTER BY AUTO 

![image](https://github.com/user-attachments/assets/a63bf865-c2b1-46f8-b8c2-7f27f8b243f8)












