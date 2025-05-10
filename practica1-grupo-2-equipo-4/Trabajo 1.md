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
|       | Propiedad                   | Dominio            | Rango            | Comentario                                                        |
| ----- | --------------------------- | ------------------ | ---------------- | ----------------------------------------------------------------- |
| 1     | `foaf:name`                 | Persona            | `xsd:string`     | Usa FOAF para el nombre de la persona.                            |
| 2     | `ex:anioNacimiento`         | Persona            | `xsd:gYear`      | Año de nacimiento.                                                |
| 3     | `ex:tieneIngreso`           | Persona            | Ingreso          | Relaciona a una persona con su ingreso (objeto).                  |
| ~~4~~ | ~~`ex:tipoIngreso`~~        | ~~Ingreso~~        | ~~`xsd:string`~~ | ~~Fijo, variable (puede redundar pero útil para lógica difusa).~~ |
| 5     | `ex:montoIngreso`           | Ingreso            | `xsd:decimal`    | Cuánto gana la persona.                                           |
| 6     | `ex:TieneCredito`           | Persona            | Credito          | Indica los créditos que actualmente tiene activos.                |
| 7     | `ex:monto`                  | Credito            | `xsd:decimal`    | Monto del crédito.                                                |
| 8     | ` ↳ ex:montoSolicitado`     | *Credito*          | *`xsd:decimal`*  | Subpropiedad de `ex:monto`: monto solicitado.                     |
| 9     | ` ↳ ex:montoAprobado`       | *Credito*          | *`xsd:decimal`*  | Subpropiedad de `ex:monto`: monto aprobado.                       |
| 10    | `ex:plazo`                  | Credito            | `xsd:integer`    | Plazo en meses o años.                                            |
| 11    | `ex:tieneHistorial`         | Persona            | Historial        | Conecta persona con su historial.                                 |
| 12    | `ex:puntajeCrediticio`      | Historial          | `xsd:decimal`    | Escala de 0 a 1000, por ejemplo.                                  |
| 13    | `ex:capacidadEndeudamiento` | Historial          | `xsd:decimal`    | Representa el monto máximo calculado.                             |
| 14    | `ex:estadoCredito`          | Credito            | `xsd:string`     | Aprobado, Rechazado, Activo, PendienteDeAprobación.               |
| 15    | `ex:estabilidadLaboral`     | Persona (Empleado) | `xsd:string`     | Alta, media, baja (útil para lógica difusa).                      |
| 16    | `dc:identifier`             | Credito            | `xsd:string`     | Identificador único del crédito (usa Dublin Core).                |
### Comparativa de Grafos (Antes vs Después del Razonador)
la aplicación del razonamiento semántico ha permitido ampliar automáticamente el grafo RDF, generando nuevas afirmaciones que fortalecen la representación del conocimiento.
La segunda imagen muestra el **grafo después del razonamiento**. En este caso, se han añadido automáticamente nuevas afirmaciones implícitas derivadas de las reglas semánticas. Estas inferencias enriquecen el conocimiento representado en el grafo.
#### Antes:
![[graph_before.png]]
#### Después:
![[graph_after.png]]