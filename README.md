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

python:

# Si quisieras permitir insertar valores manuales

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
Componente	Significado
.addColumn()	Agrega otra columna
"name"	Nombre de la columna
dataType=StringType()	Tipo de dato: StringType (cadena de texto)
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

        # INSERT: No incluyes id_col porque se genera automáticamente
        spark.sql("""
            INSERT INTO deltalakeall.default.firstdeltaapi (salary, name)
            VALUES 
                (50000, 'Juan Pérez'),
                (60000, 'María García'),
                (55000, 'Carlos López')
       """)



# Resultado:

# id_col = 1, salary = 50000, name = 'Juan Pérez'

# id_col = 2, salary = 60000, name = 'María García'

# id_col = 3, salary = 55000, name = 'Carlos López'

❌ Incorrecto (Intentas insertar id_col manualmente)

python:

        # ERROR: No puedes insertar en id_col porque es GENERATED ALWAYS
        spark.sql("""
            INSERT INTO deltalakeall.default.firstdeltaapi (id_col, salary, name)
            VALUES (100, 50000, 'Juan Pérez')
        """)
        
# ❌ Error: Column 'id_col' is an identity column and cannot be specified


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
