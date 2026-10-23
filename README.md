# Veterinary Income Dashboard

Power BI dashboard that analyzes the income of a veterinary clinic during 2024: how much money comes in, from which services, animals, veterinarians and months.

<img width="700" alt="Captura de pantalla 2026-10-23 173720" src="https://github.com/user-attachments/assets/cbc7d128-5809-426d-b114-1f737afee8c8" />


## Key figures

| Metric | Value |
|---|---|
| Total income | $15,893,493 |
| Records analyzed | 150 services |
| Period | Jan 6, 2024 – Dec 3, 2024 |
| Top service | Emergencia (~$4.2M) |
| Top animal | Gato ($3,901,555) |
| Top veterinarian | Dr. Conley ($3,595,813) |
| Sterilized vs. not | 50.64% Sí / 49.36% No |

> December looks very low because the data ends on Dec 3, not because of a real drop in income.

## What the dashboard shows

- **Total Incomes** card with the full amount (no "M" abbreviation).
- **Incomes by Month**: line chart, January to December.
- **Sterilized**: donut chart with the income split between sterilized and non-sterilized animals.
- **Incomes by Dr.**, **Incomes by Animal** and **Incomes by Service**: ranked bar charts.
- **Filters**: Treatment, Service, Sterilized (Sí / No) and Month.

## Data

The dataset has 150 rows and 12 columns:

| Column | Description |
|---|---|
| Fecha del servicio | Date of the service |
| Nombre cliente | Client name |
| Animal | Species (Perro, Gato, Ave, Conejo, Hámster) |
| Raza mascota | Pet breed |
| Nombre paciente | Pet name |
| Esterilizado? | Whether the pet is sterilized (Sí / No) |
| Servicio recibido | Service (Esterilización, Emergencia, Vacunación, Control de peso, Consulta general) |
| Monto pagado | Amount paid |
| Medico Veterinario que atendió | Veterinarian who attended |
| Diagnóstico | Diagnosis |
| Tratamiento | Treatment |
| Region | Region |

The data is fictional and was used for practice purposes.

### Data cleaning

`Datos_no_corregidos.csv` is the original raw file. `Datosveterinaria.xlsx` is the corrected version used in the report. Main fixes:

- Removed the title and empty rows at the top of the CSV.
- Converted dates from text (`M/D/YYYY`) to a real date type.
- Fixed the encoding of accented characters (á, é, í, ó).
- Added the `Region` column.

## DAX

**Full amount for the card** (avoids Power BI abbreviating to "16M"):

```DAX
Monto completo = FORMAT(SUM(Data[Monto pagado]), "$#,##0")
```

**Month table** (created with *New table*), used to show months as ENE, FEB, MAR... in order. Sort `MesAbreviado` by `MESNUM`:

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

## Repository structure

```
Veterinary-Income-Dashboard/
├── README.md
├── data/
│   ├── Datos_no_corregidos.csv
│   └── Datosveterinaria.xlsx
├── dashboard/
│   └── Veterinary_Income_Dashboard.pbix
└── images/
    └── dashboard.png
```

## How to use

1. Download `dashboard/Veterinary_Income_Dashboard.pbix`.
2. Open it with [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
3. If Power BI asks for the data source, point it to `data/Datosveterinaria.xlsx`.

## Tools

- Power BI Desktop
- DAX
- Excel
