# Calculadora de precios para automatizaciones con IA

Herramienta de una sola página para cotizar servicios de automatización sin equivocarse en el margen.

## El problema que resuelve

Quien vende automatizaciones suele cotizar mal por tres razones concretas.

Confunde markup con margen. Aplicar un multiplicador de 1,30 no deja 30% de margen, deja 23,08%. El markup se calcula sobre el costo y el margen sobre el precio, son denominadores distintos y el resultado se ve razonable, así que el error sobrevive años.

Cotiza la implementación y olvida la mantención. Sin una mensualidad definida, todo el trabajo posterior es gratis.

No define umbrales de uso. Cuando el cliente crece, el costo de las APIs se lo come el proveedor.

## Qué hace

Recibe el costo mensual de herramientas y APIs, las horas estimadas de implementación, el valor hora propio, el sueldo del rol que el sistema reemplaza y el volumen esperado de operaciones.

Devuelve el precio de implementación sugerido, la mensualidad, el umbral de operaciones incluidas con su precio de excedente, el margen real resultante y el ingreso proyectado a doce meses.

Y avisa dos cosas. Si el multiplicador que estás usando produce un margen distinto al que crees, mostrando cuál sería el correcto. Y si dejaste la mensualidad en cero.

## Referencias de mercado incluidas

Los rangos que muestra la herramienta como contexto vienen de precios efectivamente cobrados y publicados por practicantes del rubro.

```
Implementación      mediana 1.000 USD, rango típico 500 a 2.400
Mantención          75 a 150 al mes
                    150 a 480 si el sistema reemplaza un rol completo
Umbral de ejemplo   5.000 operaciones incluidas, 1 USD por cada 100 adicionales
```

## Cómo se construyó

El código lo generó **GPT-6 Astra**, invocado a través de Codex CLI **desde dentro de Claude Code**, sin salir del terminal.

El flujo fue así. Claude Code redactó la especificación funcional a partir del problema de negocio, incluyendo las reglas de cálculo y los rangos de referencia. Esa especificación se le pasó a Astra con `codex exec --model gpt-6-astra`. Astra devolvió el archivo completo. Claude Code lo verificó abriéndolo en un navegador real con Playwright y comprobando que el cálculo del markup diera 23,08% para un multiplicador de 1,30, que es el error que la herramienta existe para evitar.

Después de la verificación quedaron dos correcciones. El multiplicador correcto salía con seis decimales y ahora sale con dos. Y el texto usaba el signo menos unicode, que se reemplazó por un guion normal.

Lo interesante del ejercicio no es que un modelo escriba HTML. Es que un agente puede especificar, delegar a otro modelo, verificar el resultado en un navegador y corregir lo que encuentre, sin que una persona toque el código en el medio.

## Uso

Es un solo archivo sin dependencias. Se abre `index.html` en cualquier navegador o se despliega como sitio estático.

## Licencia

MIT
