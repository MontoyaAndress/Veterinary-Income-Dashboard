# Dashboard de Ingresos Veterinarios

Dashboard en Power BI que analiza los ingresos de una clínica veterinaria durante 2024: cuánto dinero entra, por qué servicios, animales, veterinarios y meses.

[read in English](readme-en.md)
<p align="center">
  <img width="700" alt="Dashboard de Ingresos Veterinarios" src="https://github.com/user-attachments/assets/cbc7d128-5809-426d-b114-1f737afee8c8" />
</p>

## Cifras clave

| Métrica | Valor |
|---|---|
| Ingreso total | $15,893,493 |
| Registros analizados | 150 servicios |
| Periodo | 6 de enero de 2024 – 3 de diciembre de 2024 |
| Servicio con más ingresos | Emergencia (~$4.2M) |
| Animal con más ingresos | Gato ($3,901,555) |
| Veterinario con más ingresos | Dr. Conley ($3,595,813) |
| Esterilizados vs. no esterilizados | 50.64% Sí / 49.36% No |

> Diciembre se ve muy bajo porque los datos terminan el 3 de diciembre, no porque los ingresos hayan caído.

## Qué muestra el dashboard

- **Total Incomes**: tarjeta con el monto completo (sin abreviar a "M").
- **Incomes by Month**: gráfica de líneas de enero a diciembre.
- **Sterilized**: gráfica de dona con la división de ingresos entre animales esterilizados y no esterilizados.
- **Incomes by Dr.**, **Incomes by Animal** e **Incomes by Service**: gráficas de barras ordenadas de mayor a menor.
- **Filtros**: Tratamiento, Servicio, Esterilizado (Sí / No) y Mes.

## Datos

La base tiene 150 filas y 12 columnas:

| Columna | Descripción |
|---|---|
| Fecha del servicio | Fecha en que se dio el servicio |
| Nombre cliente | Nombre del cliente |
| Animal | Especie (Perro, Gato, Ave, Conejo, Hámster) |
| Raza mascota | Raza de la mascota |
| Nombre paciente | Nombre de la mascota |
| Esterilizado? | Si la mascota está esterilizada (Sí / No) |
| Servicio recibido | Servicio (Esterilización, Emergencia, Vacunación, Control de peso, Consulta general) |
| Monto pagado | Monto pagado por el servicio |
| Medico Veterinario que atendió | Veterinario que atendió |
| Diagnóstico | Diagnóstico |
| Tratamiento | Tratamiento aplicado |
| Region | Región |

Los datos son ficticios y se usaron con fines de práctica.

### Limpieza de datos

`Datos_no_corregidos.csv` es el archivo original sin tratar. `Datosveterinaria.xlsx` es la versión corregida que se usa en el reporte. Principales correcciones:

- Se quitaron el título y las filas vacías del inicio del CSV.
- Las fechas pasaron de texto (`M/D/AAAA`) a tipo fecha.
- Se corrigió la codificación de los acentos (á, é, í, ó).
- Se agregó la columna `Region`.

## DAX

**Monto completo para la tarjeta** (evita que Power BI lo abrevie a "16M"):

```DAX
Monto completo = FORMAT(SUM(Data[Monto pagado]), "$#,##0")
```

**Tabla de meses** (se crea con *Nueva tabla*), para mostrar los meses como ENE, FEB, MAR... en orden. Ordena `MesAbreviado` por `MESNUM`:

```DAX
TablaMeses =
DATATABLE(
    "MesAbreviado", STRING,
    "MESNUM", INTEGER,
    {
        {"ENE", 1}, {"FEB", 2}, {"MAR", 3}, {"ABR", 4},
        {"MAY", 5}, {"JUN", 6}, {"JUL", 7}, {"AGO", 8},
        {"SEP", 9}, {"OCT", 10}, {"NOV", 11}, {"DIC", 12}
    }
)
```

## Estructura del repositorio

```
Veterinary-Income-Dashboard/
├── README.md
├── data/
│   ├── Datos_no_corregidos.csv
│   └── Datosveterinaria.xlsx
└── dashboard/
    └── Veterinary_Income_Dashboard.pbix
```

## Cómo usarlo

1. Descarga `dashboard/Veterinary_Income_Dashboard.pbix`.
2. Ábrelo con [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
3. Si Power BI pide la fuente de datos, apúntalo a `data/Datosveterinaria.xlsx`.

## Herramientas

- Power BI Desktop
- DAX
- Excel

