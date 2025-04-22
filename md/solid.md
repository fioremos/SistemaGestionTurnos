# Anexo - Principios SOLID

## ¿Qué son los principios SOLID?

Los principios SOLID son un conjunto de buenas prácticas para el diseño y la arquitectura de software orientado a objetos. Están pensados para crear sistemas que sean fáciles de mantener, escalar, probar y entender, reduciendo el acoplamiento entre clases y aumentando su cohesión.

El acrónimo SOLID representa cinco principios fundamentales:

- **S**: Single Responsibility Principle (Responsabilidad Única)
- **O**: Open/Closed Principle (Abierto/Cerrado)
- **L**: Liskov Substitution Principle (Sustitución de Liskov)
- **I**: Interface Segregation Principle (Segregación de Interfaces)
- **D**: Dependency Inversion Principle (Inversión de Dependencias)

## ¿Por qué aplicarlos en un sistema de turnos médicos?
El sistema de turnos médicos debe ser:
* **Flexible**: permitir agregar nuevas funcionalidades como notificaciones, reportes, estadísticas.
* **Escalable**: para adaptarse a distintos centros de salud, médicos y especialidades.
* **Fácil de mantener**: para modificar partes del sistema sin afectar el resto.
* **Seguro y robusto**: con lógica clara y bien separada, evitando errores por dependencias innecesarias.

Aplicar los principios SOLID nos permite evitar clases que hagan "demasiado", reducir código duplicado, permitir la extensión sin romper el código ya hecho y mantener el foco en una arquitectura limpia y mantenible.

## Breve resumen de cada principio
* [**SRP – Principio de Responsabilidad Única**](srp.md) Una clase debe tener una sola razón para cambiar. Esto implica que cada clase debe enfocarse en una única funcionalidad del sistema.
* [**OCP – Principio Abierto/Cerrado**](ocp.md) El software debe estar abierto para su extensión, pero cerrado para su modificación. Esto se logra mediante el uso de herencia, interfaces y polimorfismo. 
* [**LSP – Principio de Sustitución de Liskov**](lsp.md) Las subclases deben poder sustituir a sus clases base sin alterar la lógica del programa.
* [**ISP – Principio de Segregación de Interfaces**](isp.md) Las clases no deben verse obligadas a depender de métodos que no utilizan. Es preferible tener interfaces más pequeñas y específicas.
* [**DIP – Principio de Inversión de Dependencias**](dip.md) Las clases deben depender de abstracciones y no de implementaciones concretas.

## Beneficios en el proyecto
* **Mantenibilidad**: las clases se pueden modificar sin riesgo de romper otras funcionalidades.
* **Reusabilidad**: componentes reutilizables en otros proyectos o contextos.
* **Testeo fácil**: al depender de interfaces, es más sencillo usar mocks y stubs para pruebas unitarias.
* **Evolución del sistema**: se pueden agregar nuevas funcionalidades sin reescribir las existentes.

## Conclusión
Aplicar los principios SOLID al diseño del sistema de turnos médicos no solo mejora la calidad del código, sino que sienta las bases para un software confiable, adaptable y profesional. Cada decisión de diseño se vuelve más consciente, y el sistema queda preparado para evolucionar junto con las necesidades del centro de salud.
