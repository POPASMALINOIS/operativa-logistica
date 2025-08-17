# Operativa Logística (Offline, Windows)

Aplicación de escritorio **WPF (.NET 8)**, **offline**, **plug-and-play**, para gestionar la operativa de **carga terrestre y aérea**:
- Importa datos desde **CSV** o **Excel (.xlsx)**.
- Filtro, búsqueda y ordenación en tabla.
- **Un clic** por fila para **LLEGADA REAL** y **SALIDA REAL**.
- Botón **Guardar jornada**: genera un **PDF** en el Escritorio y mantiene **histórico de 30 días** (limpieza automática).
- Sin instalación administrativa; almacena datos en `%LOCALAPPDATA%\OperativaLogistica\data.db` (SQLite).

> **Requisitos de compilación (solo en la máquina de desarrollo):**
> - Windows 10/11
> - .NET 8 SDK
> - (Automático) NuGet: `Microsoft.Data.Sqlite`, `ClosedXML`, `QuestPDF`

### Compilar
```powershell
cd src/OperativaLogistica
dotnet restore
dotnet build -c Release
```

### Publicar en modo "todo en uno" (self-contained, sin instalar nada)
```powershell
dotnet publish -c Release -r win-x64 -p:PublishSingleFile=true -p:PublishTrimmed=true -p:IncludeNativeLibrariesForSelfExtract=true -o ../../Publish/win-x64
```
Copia la carpeta `Publish/win-x64` al PC objetivo y ejecuta `OperativaLogistica.exe`.

### Uso
1. **Archivo → Importar** (CSV o Excel).
2. Para marcar tiempos reales: pulsa en **⏱ Llegada** o **⏱ Salida** dentro de la fila.
3. **Guardar jornada**: crea PDF en `Escritorio\Operativa_Historico` y depura ficheros >30 días.

### Estructura
```
src/OperativaLogistica
├── App.xaml / App.xaml.cs
├── MainWindow.xaml / MainWindow.xaml.cs
├── Models/Operacion.cs
├── Services/DatabaseService.cs
├── Services/ImportService.cs
├── Services/PdfService.cs
├── ViewModels/MainViewModel.cs
├── Commands/RelayCommand.cs
└── OperativaLogistica.csproj
```

### Importación de columnas
Las columnas esperadas (cabeceras) son:
`TRANSPORTISTA, MATRICULA, MUELLE, ESTADO, DESTINO, LLEGADA, SALIDA TOPE, OBSERVACIONES, INCIDENCIAS`
`LLEGADA REAL` y `SALIDA REAL` las gestiona la App.

### Licencia
MIT
