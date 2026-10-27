# PPS-E1 · Lectura entrada→sink

Cópiala como `PPS-E1-lectura.md` y rellénala.

| Fichero | Punto de entrada | Sink(s) | Validación (¿cuál? ¿basta?) | Dónde falla según su modelo de ejecución |
|---|---|---|---|---|
| `validar.py` (interpretado) |sys.argv[1]|con.execute(consulta)os.system(...)eval(regla) |entre 1 y 32 caracteres; no basta |eval(regla)|
| `Validar.java` (bytecode / JVM) |args[0]|st.executeQuery(consulta)|que no sea nulo y que tenga entre 1 y 32 caracteres. No basta.|el programa puede llegar a ejecutar una consulta SQL construida con el dato del usuario |
| `validar.c` (nativo) |argv[1]|strcpy(buffer, nombre) |ninguna|buffer overflow|

## ¿Cómo lo corregirías? (una línea por fichero)

- `validar.py`: evitar os.system() con datos del usuario y eliminar eval()
- `Validar.java`: usar PreparedStatement con parámetros en lugar de concatenar nombre en la consulta.
- `validar.c`: comprobar la longitud de nombre y usar una copia con límite de tamaño, evitando escribir fuera de buffer
