
# PS/2 Keyboard

## Responsables

| | |
| :--- | :--- |
| **Ivan Felipe Maluche Suarez** | |
| **Kevin Javier Gonzalez Luna** | |
| **Santiago Guillen** | |
| **Felipe Hortua** | |

## Protocolo

El puerto PS2 está compuesto por dos cables. Hay un cable para datos, cuya transferencia es en serie. El otro cable se emplea para la información del reloj. Este último permite especificar si los datos son válidos y si se pueden recuperar. La información es transmitida como un "paquete" de 11 bits, el cual posee 1 bit de inicio, 8 bits de datos, un bit de paridad impar y finalmente un bit de parada

![PS/2](Imagenes/DTPS2.png)

## Flujo de funcionamiento

```mermaid
---
config:
    flowchart:
        curve: basis
---
graph TD
    A([Conexión]) --> B(Espera de un cambio de estado)
    
    B --> C{Data diferente<br/>de cero}
    C -- No --> B
    C -- Sí --> D(Recibimiento de datos)
    
    D -- entrar en ciclo --> E(Transporte de la señal y<br/>traducción por medio del driver)
    
    E -- Registro 8 bits --> F{¿El valor pertenece a la<br/>lista relevante?}
    
    F -- no --> G(Paso al siguiente loop<br/>de lectura de señales)
    F -- Sí --> H(Conversión de datos al formato<br/>legible por la lógica del sistema)
    
    H --> I(Dato retenido, disponible)
    I --> G
    
    G --> B
```

<details>
<summary>Ver diagrama elaborado en draw.io</summary>

![Diagrama de flujo del teclado PS/2](Imagenes/Diagrama_1.png)

</details>

## Créditos

La documentación y el diseño base de esta plantilla se encuentran en el
repositorio [digital_UN](https://github.com/cicamargoba/digital_UN/tree/main/2026_1),
propiedad de [@cicamargo](https://github.com/cicamargoba).
