# Sistema de Reservas de Salones de Eventos - Eventos Premier S.A.S.

Sistema integral de gestión de base de datos relacional para el alquiler de salones destinados a reuniones, fiestas y conferencias en **Eventos Premier S.A.S.**

## 👥 Autores y Créditos
* **Joel Santiago Carreño Vargas** (Desarrollo de Triggers, Auditoría y Módulo de Consultas/Vistas)
* **Juan David Figueroa** (Diseño de Esquema, Estructura de Tablas y Funciones Personalizadas)

---

## 🛠️ Descripción del Proyecto
Este proyecto digitaliza el manejo de reservas de salones de la empresa, garantizando la disponibilidad de espacios, la correcta administración de clientes (Individuales y Corporativos), el cálculo automático de tarifas con IVA (19%), el control de pagos y la auditoría estricta de cambios de precios.

---

## 📂 Estructura de Scripts Organizados
El sistema está dividido en cuatro módulos lógicos para asegurar un despliegue limpio y estructurado:
1. **`01_schema.sql`**: Creación de la base de datos `db_reservas_eventos` y las tablas relacionales (`salones`, `clientes`, `reservas`, `pagos`, `auditoria_precios`) con sus respectivas llaves foráneas.
2. **`02_functions.sql`**: Implementación de funciones personalizadas:
   - `calcular_total_reserva(precio_hora, horas)`: Retorna el valor total aplicando el 19% de IVA.
   - `verificar_disponibilidad(salon_id, fecha_inicio, fecha_fin)`: Retorna `1` si el salón está libre o `0` si está ocupado/en mantenimiento.
3. **`03_triggers.sql`**: Triggers de control de integridad y auditoría:
   - `validar_reserva_trigger`: Evita cruces de horarios y bloquea reservas en salones bajo mantenimiento.
   - `actualizar_estado_salon` & `liberar_salon`: Cambian dinámicamente el estado del salón entre *Disponible* y *Ocupado*.
   - `auditoria_precios_trigger`: Registra automáticamente los cambios de tarifas en la tabla `auditoria_precios`.
4. **`04_data_and_queries.sql`**: Población de datos iniciales de prueba, creación de la vista `vista_resumen_reservas` y ejecución de consultas analíticas avanzadas (`BETWEEN`, `CAPACIDAD > 50`, `GROUP BY` y `COUNT`).

---

## 🚀 Instrucciones de Ejecución (MySQL Workbench)
Para poner en marcha el sistema, abra su gestor MySQL Workbench, cree una pestaña de consultas y ejecute los archivos en estricto orden secuencial:
1. Ejecute `01_schema.sql`
2. Ejecute `02_functions.sql`
3. Ejecute `03_triggers.sql`
4. Ejecute `04_data_and_queries.sql`
