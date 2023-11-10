
# Seguimiento de alta calidad de cualquier cosa en videos

## Metadata

- Autores: Jiawen Zhu, Zhenyu Chen, et al.
- Año: 2023
- DOI: [10.48550/arXiv.2307.13974](https://doi.org/10.48550/arXiv.2307.13974)

## Introducción

El artículo propone [[HQTrack]], un marco para el seguimiento de alta calidad de múltiples objetos en videos. #track

## Métodos

[[HQTrack]] consiste de dos componentes principales:

### Video Multi-Object Segmenter (VMOS)

Propaga máscaras de objetos del primer fotograma al fotograma actual usando modelado de apariencia, identificación y memoria a corto/largo plazo. Es una variante mejorada del modelo [[DeAOT]].

### Mask Refiner (MR) 

Un modelo [[HQ-SAM]] pre-entrenado que refina las máscaras predichas por [[VMOS]]. [[HQ-SAM]] puede manejar mejor estructuras de objetos complejas.

- [[VMOS]] usa propagación multi-escala y extractor de características Intern-T para mejor percepción de objetos pequeños.
- [[MR]] toma máscaras y indicaciones de cuadro de [[VMOS]] como entrada para refinar máscaras.
- Las máscaras finales se seleccionan entre [[VMOS]] y [[MR]] en base a su puntuación IoU para evitar refinamientos deficientes.

## Resultados

- Sin ningún truco de tiempo de prueba, [[HQTrack]] logra el 2do lugar en el desafío [[VOTS2023]] para rastreo y segmentación de múltiples objetos en videos.
- Demuestra un rendimiento sólido en seguimiento a largo plazo, seguimiento multi-objeto, captura precisa de objetos a pesar de desafíos como oclusión, cambios de escala/apariencia, etc.

## Conclusión

En resumen, el [[HQTrack]] propuesto logra estado del arte en seguimiento y segmentación de alta calidad de múltiples objetos en videos usando [[VMOS]] para propagación y [[MR]] para refinamiento de máscara.