## 3. Ontología y Razonamiento Semántico (RDFLib y OWL-RL)
### Clases

1. Persona
	2. Estudiante
	3. Jubilado
	4. Empleado
	5. Independiente
2. Ingreso
	7. IngresoFijo
	8. IngresoVariable
3. Crédito
	10. LibreInversion
	11. CreditoHipotecario
	12. CreditoVehicular
4. Historial
	14. PuntajeCrediticio
	15. CapacidadEndeudamiento

### Propiedades
| 1   | Propiedad                   | Dominio            | Rango                                     | Comentario                                                           |
| --- | --------------------------- | ------------------ | ----------------------------------------- | -------------------------------------------------------------------- |
| 2   | `foaf:name`                 | Persona            | `xsd:string`                              | Usa FOAF para el nombre de la persona.                               |
| 3   | `ex:anioNacimiento`         | Persona            | `xsd:gYear`                               | Año de nacimiento.                                                   |
| 4   | `ex:tieneIngreso`           | Persona            | Ingreso                                   | Relaciona a una persona con su ingreso (objeto).                     |
| 5   | `ex:tipoIngreso`            | Ingreso            | `xsd:string`                              | Fijo, variable (puede redundar pero útil para lógica difusa).        |
| 6   | `ex:montoIngreso`           | Ingreso            | `xsd:decimal`                             | Cuánto gana la persona.                                              |
|     | ~~`ex:solicitaCredito`~~    | ~~Persona~~        | ~~Credito~~                               | ~~Indica qué crédito ha solicitado.~~                                |
| 7   | `ex:TieneCredito`           | Persona            | Credito                                   | Indica los créditos que actualmente tiene activos.                   |
| 8   | `ex:monto`                  | Credito            | `xsd:decimal`                             | Monto del crédito.                                                   |
| 9   | ` ↳ ex:montoSolicitado`     | *Credito*          | *`xsd:decimal`*                           | Subpropiedad de `ex:monto`: monto solicitado.                        |
| 10  | ` ↳ ex:montoAprobado`       | *Credito*          | *`xsd:decimal`*                           | Subpropiedad de `ex:monto`: monto aprobado.                          |
| 11  | `ex:plazo`                  | Credito            | `xsd:integer`                             | Plazo en meses o años.                                               |
|     | ~~`ex:tipoCredito`~~        | ~~Credito~~        | ~~Credito~~                               | ~~Apunta a una subclase (LibreInversion, Hipotecario, etc.).~~       |
|     | ~~`dc:date`~~               | ~~Credito~~        | ~~`xsd:date`~~                            | ~~Usa Dublin Core para registrar la fecha de la solicitud.~~         |
| 12  | `ex:tieneHistorial`         | Persona            | Historial                                 | Conecta persona con su historial.                                    |
| 13  | `ex:puntajeCrediticio`      | Historial          | `xsd:decimal`                             | Escala de 0 a 1000, por ejemplo.                                     |
| 14  | `ex:capacidadEndeudamiento` | Historial          | `xsd:decimal`                             | Representa el monto máximo calculado.                                |
| 15  | `ex:estadoCredito`          | Credito            | `xsd:string`                              | Aprobado, Rechazado, Activo, PendienteDeAprobación.                  |
|     | ~~`ex:tieneGarantia`~~      | ~~Credito~~        | ~~Garantia~~                              | ~~Si aplica, apunta a la garantía ofrecida.~~                        |
|     | ~~`ex:valorGarantia`~~      | ~~Garantia~~       | ~~`xsd:decimal`~~                         | ~~Valor estimado del bien ofrecido como garantía.~~                  |
| 18  | `ex:estabilidadLaboral`     | Persona (Empleado) | `xsd:string`                              | Alta, media, baja (útil para lógica difusa).                         |
|     | ~~`foaf:knows`~~            | ~~Persona~~        | ~~Persona~~                               | ~~Usa FOAF para modelar relaciones personales (amigos, conocidos).~~ |
|     | ~~`ex:analizadoPor`~~       | ~~Credito~~        | ~~AnalistaCredito (subclase de Persona)~~ | ~~Indica quién analizó la solicitud.~~                               |
| 19  | `dc:identifier`             | Credito            | `xsd:string`                              | Identificador único del crédito (usa Dublin Core).                   |
## Preguntas
## Prompts

