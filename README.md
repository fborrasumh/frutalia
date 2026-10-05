# FrutalIA

Simulador de decisiones para elegir **portainjerto y variedad en 18 cultivos frutales** según las condiciones de la finca, con casos prácticos autocorregidos. Aplicación web de un solo fichero (`index.html`).

**Usar la app:** https://fborrasumh.github.io/frutalia/

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23161695.svg)](https://doi.org/10.5281/zenodo.23161695)

**Idiomas:** español (por defecto), inglés y portugués; selector en la barra superior (o `?lang=en` / `?lang=pt` en la URL).

## Origen de la idea

La Dra. Francisca Hernández García (Universidad Miguel Hernández de Elche, asignatura *Fruticultura*, Grado en Ingeniería Agroalimentaria y Agroambiental) observó que el alumnado memoriza fichas técnicas de portainjertos sin saber aplicarlas en el campo. Su cuaderno *Selección de portainjertos de manzano* las convirtió en una herramienta interactiva: tabla de patrones (M.9, M.25, MM.106, MM.111, MI-793), gráfico de vigor frente al franco, filtro por resistencias y un caso práctico (Gala, pulgón lanígero, sin presupuesto para tutorado). FrutalIA generaliza ese enfoque a 18 cultivos.

## Qué hace

- **Simulador de la finca (paso 1).** Cultivo, caliza activa, salinidad, horas de frío, drenaje, agua, objetivo, nematodos, replantación, plagas confirmadas y presupuesto para estructura. Cada cambio recalcula al instante el ranking de patrones (recomendado / con reservas / descartado) con los motivos de cada veredicto y un gráfico de vigor relativo.
- **Variedad y plantación (paso 2).** Marco, densidad (frente al rango del patrón), número de árboles, polinizadores o machos, horas de frío frente a las de la variedad, estructura de apoyo, formación sugerida, entrada en producción y época de maduración. Informe en Word y CSV.
- **Retos (paso 3).** Casos de finca generados con semilla (reproducibles por número de caso), con pista, corrección razonada y **sin nota**. El caso 0 es el del cuaderno.
- **Fichas técnicas.** Todos los patrones y variedades, con modo estudio que oculta los valores hasta que se pulsan.
- **Tutor IA (opcional).** Explica el resultado ya calculado y comenta la justificación del alumno.

### Cultivos
Manzano, peral, membrillero, níspero del Japón, melocotonero, albaricoquero, ciruelo, cerezo, almendro, olivo, vid, cítricos, caqui, nogal, pistachero, granado, higuera y algarrobo (75 patrones o sistemas de plantación). La guía docente 2026-27 lista 11; los otros 7 son una propuesta que la profesora puede cambiar editando `src/datos.js`.

## Cómo decide (el código, no la IA)

Cada condición de la finca exige un nivel 0-3 y cada patrón aporta una capacidad 0-3. Hueco ≤ 0: cumple · hueco 1: **con reservas** · hueco ≥ 2: **descartado**. Las plagas o enfermedades confirmadas exigen resistencia (3). Sin presupuesto para estructura se descartan los patrones de entutorado obligatorio. El vigor frente al objetivo solo resta puntos, nunca descarta. Con los datos del cuaderno reproduce su caso práctico (MM.106 y MM.111) y su filtro doble (solo MI-793 es «Resistente» a pulgón y fuego bacteriano; MM.111, «Tolerante», queda con reservas).

## Cómo se usa la IA

Con la propia clave de OpenAI, Google Gemini o Anthropic Claude (se guarda solo en el navegador). **El código calcula; la IA solo redacta** la explicación a partir del caso ya calculado y no cambia ningún veredicto. El código marca las cifras de la respuesta que no estaban en el caso calculado.

## Privacidad

Los datos de la finca y el progreso se guardan en el navegador (IndexedDB). Solo sale algo hacia el proveedor de IA si se pulsa un botón de tutor, y antes del primer envío se muestra exactamente qué sale. La justificación escrita se envía con correos, teléfonos y documentos de identidad enmascarados.

## Límites

- **Los datos son orientativos.** Solo el manzano usa valores del cuaderno (vigor, entutorado, fuego bacteriano, pulgón, densidad); el resto de campos del manzano y **todos los demás cultivos son borradores pendientes de revisión por la profesora** (marcados «Borrador» en las fichas). No sustituyen la bibliografía ni el asesoramiento técnico.
- Los niveles 0-3 y los umbrales (caliza, salinidad, frío) son simplificaciones docentes; la compatibilidad de injerto con cada variedad no se modela (solo se avisa).
- En olivo, granado, higuera y algarrobo casi no hay portainjertos diferenciados: los «patrones» son sistemas de plantación.
- No incluye cálculo de necesidades hídricas, análisis foliar ni cálculo de horas frío a partir de series de temperatura (otras prácticas de la asignatura).
- Probado con IA simulada; no con claves reales.

## Autoría

- Francisca Hernández García (Universidad Miguel Hernández de Elche) · ORCID [0000-0003-3739-8748](https://orcid.org/0000-0003-3739-8748) — idea original y cuaderno de partida.
- Fernando Borrás Rocher (Universidad Miguel Hernández de Elche) · ORCID [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573) — desarrollo.

## Desarrollo y pruebas

```bash
python3 build.py && node --check all.js
node tests/test_nucleo.js                                    # lógica pura (caso del cuaderno, 180 retos)
NODE_MODULES=/ruta/node_modules python3 tests/smoke_test.py  # navegador: idiomas, IA simulada, móvil (docx@8.5.0 jszip)
```

## Cómo citar

Hernández García, F., y Borrás Rocher, F. (2026). *FrutalIA* (v1.0.0) [Software]. DOI: [10.5281/zenodo.23161695](https://doi.org/10.5281/zenodo.23161695)

## Licencia

MIT. Véase [LICENSE](LICENSE).
