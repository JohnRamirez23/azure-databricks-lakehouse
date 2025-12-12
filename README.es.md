📄 Leer esta documentación en inglés: [English version](README.md)

# Proyecto Lakehouse con Azure Synapse

## Descripción general

Este proyecto implementa una plataforma analítica de datos end-to-end en Azure utilizando una arquitectura Lakehouse.
La solución ingesta datos transaccionales desde Azure SQL Database hacia Azure Data Lake Storage Gen2, aplicando cargas incrementales, transformaciones de datos y buenas prácticas de gobierno de datos.

El pipeline es orquestado mediante Azure Synapse Analytics y sigue la Arquitectura Medallion (capas Bronze, Silver y Gold) para garantizar escalabilidad, calidad de datos y preparación para analítica.

## Arquitectura

La solución está diseñada siguiendo el patrón de arquitectura Lakehouse, separando las capas de ingesta, procesamiento y analítica para asegurar escalabilidad y mantenibilidad.

### Componentes principales

- **Fuente**: Azure SQL Database (sistema OLTP)
- **Orquestación**: Azure Synapse Analytics Pipelines
- **Almacenamiento**: Azure Data Lake Storage Gen2
- **Procesamiento**: Synapse Data Flows / Apache Spark
- **Capa analítica**: Synapse Serverless SQL Pool
- **Gestión de secretos**: Azure Key Vault

## Flujo de datos

1. Los datos se extraen de forma incremental desde Azure SQL Database utilizando una estrategia basada en watermark.
2. Los datos extraídos se almacenan en la capa **Bronze** en formato CSV para trazabilidad y reprocesamiento.
3. Los datos se transforman, tipifican y normalizan en la capa **Silver** utilizando formato columnar Parquet.
4. Los datasets listos para negocio se publican en la capa **Gold**, optimizados para analítica y reporting.
5. Se aplican validaciones de calidad de datos entre capas para asegurar consistencia y confiabilidad.

## Arquitectura Medallion

- **Capa Bronze**: Almacena los datos en bruto tal como llegan desde las fuentes, sin transformaciones.
- **Capa Silver**: Contiene datos limpios, tipificados y estandarizados listos para procesamiento analítico.
- **Capa Gold**: Proporciona datasets curados y listos para consumo por herramientas de BI y analítica.

## Tecnologías utilizadas

- Azure Synapse Analytics
- Azure Data Lake Storage Gen2
- Azure SQL Database
- Azure Key Vault
- Apache Spark
- GitHub

## Seguridad

- Toda la información sensible, como cadenas de conexión y credenciales, se gestiona mediante **Azure Key Vault**.
- Se utilizan **Managed Identities** para autenticar servicios sin credenciales embebidas.
- Los accesos siguen el principio de **menor privilegio**.

## Optimización de costos

- Se utilizan SQL Pools serverless para evitar costos fijos de cómputo.
- Los recursos se configuran con SKUs mínimos adecuados para entornos de desarrollo.
- Se aprovechan formatos columnar para reducir costos de almacenamiento y mejorar el rendimiento de consultas.

## Cómo ejecutar (alto nivel)

1. Aprovisionar los recursos necesarios en Azure (Synapse Analytics, ADLS Gen2, Azure SQL Database).
2. Configurar los Linked Services e integrar Azure Key Vault.
3. Desplegar y configurar los pipelines en Synapse.
4. Ejecutar el pipeline de ingesta y validar los datos en las capas Bronze, Silver y Gold.

## Estado del proyecto

Este proyecto se encuentra en desarrollo activo y será mejorado continuamente con funcionalidades adicionales como validaciones avanzadas de calidad de datos, monitoreo y automatización.
