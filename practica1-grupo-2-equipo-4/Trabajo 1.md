## 2. Lógica Difusa (Sci-kit Fuzzy)

### Variables Difusas

1. **Ingreso Mensual**

	- **Universo del Discurso:** $U = [0, 10]$ (en millones de pesos)
	- **Funciones de Pertenencia:**
	  - $\mu_{bajo}(x) = trapezoidal(x; 0, 0, 1.4, 2.8)$
	  - $\mu_{medio}(x) = triangular(x; 1.4, 3, 5.5)$
	  - $\mu_{alto}(x) = gaussiana(x; \mu=10, \sigma=2.8)$
	- **Modificadores:**
	  - $\mu_{más\_o\_menos\_alto}(x) = \sqrt{\mu_{alto}(x)}$
	  - $\mu_{extremadamente\_alto}(x) = [\mu_{alto}(x)]^3$

	![ingresos_mensuales.png](images/ingresos_mensuales.png)

---

2. **Estabilidad Laboral**

	- **Universo del Discurso:** $U = [0, 10]$ (escala numérica de estabilidad)
	- **Funciones de Pertenencia:**
	  - $\mu_{inestable}(x) = trapezoidal(x; 0, 0, 2, 4)$
	  - $\mu_{moderada}(x) = triangular(x; 3, 5.5, 7)$
	  - $\mu_{estable}(x) = gaussiana(x; \mu=10, \sigma=2.5)$
	- **Modificadores:**
	  - $\mu_{muy\_estable}(x) = [\mu_{estable}(x)]^2$
	  - $\mu_{más\_o\_menos\_estable}(x) = \sqrt{\mu_{estable}(x)}$

	![estabilidad_laboral.png](images/estabilidad_laboral.png)

---

3. **Puntaje Crediticio**

	- **Universo del Discurso:** $U = [0, 1000]$ (escala típica de puntajes crediticios)
	- **Funciones de Pertenencia:**
	  - $\mu_{malo}(x) = triangular(x; 0, 0, 500)$
	  - $\mu_{regular}(x) = gaussiana(x; \mu=500, \sigma=150)$
	  - $\mu_{bueno}(x) = trapezoidal(x; 600, 720, 1000, 1000)$
	- **Modificadores:**
	  - $\mu_{muy\_bueno}(x) = [\mu_{bueno}(x)]^2$
	  - $\mu_{más\_o\_menos\_malo}(x) = \sqrt{\mu_{malo}(x)}$

	![puntaje_crediticio.png](images/puntaje_crediticio.png)

---

4. **Riesgo de Impago**

	- **Universo del Discurso:** $U = [0, 100]$ (escala de riesgo porcentual)
	- **Funciones de Pertenencia:**
	  - $\mu_{bajo}(x) = triangular(x; 0, 0, 35)$
	  - $\mu_{medio}(x) = trapezoidal(x; 20, 40, 60, 80)$
	  - $\mu_{alto}(x) = gaussiana(x; \mu=100, \sigma=25)$
	- **Modificadores:**
	  - $\mu_{muy\_bajo}(x) = [\mu_{bajo}(x)]^2$
	  - $\mu_{más\_o\_menos\_alto}(x) = \sqrt{\mu_{alto}(x)}$

	![riesgo_impago.png](images/riesgo_impago.png)

### Reglas Difusas.

A continuación, se presentan las reglas definidas para evaluar el riesgo de impago basado en el ingreso mensual, la estabilidad laboral y el puntaje crediticio.

### Reglas Difusas para Evaluar el Riesgo de Impago

A continuación se presentan las reglas del sistema de inferencia difuso. Estas fueron diseñadas para ser más flexibles y realistas, permitiendo decisiones menos estrictas pero coherentes con el comportamiento esperado de riesgo crediticio:

1. **Regla 1:**  
   Si el ingreso mensual es **bajo** y el puntaje crediticio es **malo**,  
   entonces el **riesgo de impago** es **alto**.

2. **Regla 2:**  
   Si el ingreso mensual es **medio** o la estabilidad laboral es **moderada**,  
   y el puntaje crediticio es **regular**,  
   entonces el **riesgo de impago** es **medio**.

3. **Regla 3:**  
   Si el ingreso mensual es **alto** o el puntaje crediticio es **bueno**,  
   entonces el **riesgo de impago** es **bajo**.

4. **Regla 4:**  
   Si el ingreso mensual **no es alto** y la estabilidad laboral es **inestable**,  
   entonces el **riesgo de impago** es **más o menos alto**.

5. **Regla 5:**  
   Si el ingreso mensual es **bajo** o el puntaje crediticio **no es bueno**,  
   entonces el **riesgo de impago** es **alto**.

6. **Regla 6:**  
   Si el ingreso mensual es **medio** y el puntaje crediticio es **regular**,  
   entonces el **riesgo de impago** es **medio**.

7. **Regla 7:**  
   Si la estabilidad laboral es **muy estable** y el puntaje crediticio **no es malo**,  
   entonces el **riesgo de impago** es **bajo**.

8. **Regla 8:**  
   Si la estabilidad laboral es **inestable** y el puntaje crediticio es **malo**,  
   entonces el **riesgo de impago** es **alto**.

9. **Regla 9:**  
   Si el ingreso mensual es **medio** y el puntaje crediticio es **bueno**,  
   entonces el **riesgo de impago** es **bajo**.

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
![graph_before.png](images/graph_before.png)
#### Después:
![graph_after.png](images/graph_after.png)

