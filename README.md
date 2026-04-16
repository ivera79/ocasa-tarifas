# OCASA | Consulta de Tarifas Activas

## 🔗 Link de acceso
https://ivera79.github.io/ocasa-tarifas/ocasa_tarifas.html

## 👤 Usuarios y contraseñas

| Usuario    | Contraseña       |
|------------|------------------|
| ocasa      | tarifas2026      |
| admin      | ocasa2026        |
| logistica  | logistica2026    |

## 📋 Notas
- Actualizado: Abril 2026
- Datos: Tarifas_Activas.xlsx
## query SQL SERVER para actualizar el archivo
SELECT 
    A.Sucursal,
    A.Proveedor_Nombre,
    A.Tipo_Tarifa,
    A.Ruta,
    A.Parametro_Ruta,
    A.Cat_General,
    A.Patente_Vehiculo,
    A.Metodo_General_Pago,
    A.Condicion_Tecnica,
    A.Tipo_Servicio,
    A.Material,
    A.Tipo_Carga,
    A.Valor_Escala,
    A.Cod_Regio,
    A.Detalles_Tarifa,
    B.Periodo,
    B.Valor
FROM dw.Fact_Tarifa_Transporte A
CROSS APPLY (
    SELECT TOP 1
        Periodo,
        Valor
    FROM DW.Fact_Tarifa_Transporte_Historico B
    WHERE A.Tarifa_Id = B.Tarifa_Id
    ORDER BY B.Periodo DESC
) B
WHERE A.Tarifa_Activa = 'Si'
ORDER BY A.Tipo_Tarifa;



