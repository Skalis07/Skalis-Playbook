# PROMPT — Comentar código (Didáctico, profundo y realista)

Quiero que analices y comentes este código con un enfoque **DIDÁCTICO, PROFUNDO y REALISTA**, como si fueras un mentor senior explicándole a alguien que quiere entender de verdad.

---

## REQUISITOS IMPORTANTES (NO NEGOCIABLES)

1. **NO cambies la lógica ni el comportamiento del código.**
2. **NO refactorices, NO optimices, NO “mejores” nada** a menos que te lo pida explícitamente.
3. **NO elimines ni reescribas comentarios existentes.**
4. Si agregas comentarios, que sean **EXPLICATIVOS**, no obvios.
5. Explica el **“POR QUÉ”** de cada bloque, no solo el “QUÉ”.
6. Usa lenguaje claro, humano y progresivo (**mentor > manual**).
7. Asume que quiero **ENTENDER** el código, no solo que funcione.
8. Explica conceptos generales cuando aparezcan usando **ejemplos simples y analogías** cuando ayuden.
9. Indica qué **problemas reales** resuelve cada patrón usado.
10. Si algo es defensivo, preventivo o por compatibilidad, explícalo explícitamente.
11. Respeta mi estilo de indentación, saltos de línea y espacios; **NO los modifiques**.
12. Si algo parece “innecesario”, explica por qué **SÍ tiene sentido** en este contexto.
13. No resumas en exceso: prefiero claridad y detalle antes que brevedad.
14. Si hay decisiones avanzadas (performance, UX, embeds, cross-browser, mobile), explícalas paso a paso.
15. Mantén el foco en aprendizaje real, no en “best practices genéricas”.

---

## FORMATO DE SALIDA (OBLIGATORIO)

- Devuélveme el **mismo código**, con **comentarios agregados dentro del archivo**.
- **NO** respondas con explicación suelta fuera del código, salvo la sección opcional “Notas finales”.
- **NO** cambies:
  - indentación
  - espacios
  - saltos de línea
  - orden del código
  - nombres de variables/funciones

### Notas finales (opcional)

Al final, puedes incluir una sección aparte llamada:

`## Notas finales`

Con máximo:

- **10 bullets**
- solo observaciones de:
  - riesgos reales
  - edge cases importantes
  - supuestos del código
  - puntos donde rompería si cambia el contexto

---

## CÓMO COMENTAR (GUÍA DE CALIDAD)

- Prefiere comentarios **sobre bloques** (funciones, secciones, grupos de líneas), no comentario por cada línea.
- Evita comentarios redundantes tipo “incrementa i” o “crea variable”.
- Cuando haya una función, comenta siempre:
  - su **responsabilidad**
  - su **input/output** (aunque sean implícitos)
  - invariantes (“esto siempre debe ser cierto”)
  - side effects (“esto impacta X”)
- Cuando haya:
  - async / timers / observers / render loop
  - DOM / UI state
  - cache / memo
  - errores silenciosos
  - compatibilidad
    explica el motivo y el riesgo.

---

## OBJETIVO FINAL

Quiero poder leer el código y entender:

- qué hace,
- por qué está escrito así,
- qué problema evita,
- qué pasaría si se quitara,
- y cuándo tendría sentido modificarlo.

---

## EJEMPLO DE REFERENCIA (ASÍ DEBE QUEDAR COMENTADO)

```js
/* -----------------------------------------------------------------------
   PLANIFICACIÓN SUAVIZADA DEL RECÁLCULO
   - Este bloque NO ejecuta el cálculo directamente.
   - Se encarga de decidir CUÁNDO recalcular, no CÓMO.
   - Combina debounce + requestAnimationFrame para:
     • evitar ejecuciones excesivas
     • sincronizar cálculos con el render del navegador
     • prevenir jank y layouts forzados
   ----------------------------------------------------------------------- */
function schedule() {
  // Si ya hay un temporizador pendiente, noteamos que
  // llegó un nuevo evento (resize, observer, etc.)
  // y cancelamos el anterior.
  // Esto es el patrón "debounce":
  // esperamos a que el usuario DEJE de interactuar.
  if (debounceTimer) clearTimeout(debounceTimer);

  // Creamos un nuevo temporizador corto.
  // 40ms ≈ 2 frames a 60Hz:
  // suficiente para agrupar eventos rápidos,
  // pero imperceptible para el usuario.
  debounceTimer = setTimeout(() => {
    // Si ya hay un requestAnimationFrame programado,
    // NO agendamos otro.
    // Esto evita múltiples cálculos en el mismo frame.
    if (rafId) return;

    // requestAnimationFrame asegura que el cálculo:
    // - ocurra justo antes del repintado
    // - no fuerce layouts intermedios
    // - sea más eficiente que setTimeout directo
    rafId = requestAnimationFrame(computeAndApply);
  }, 40);
}

/* -----------------------------------------------------------------------
   OBSERVADORES DE CAMBIO DE TAMAÑO
   - Detectan cuándo el contenedor cambia de ancho
   - Disparan schedule(), NO el cálculo directo
   - Esto separa "detección" de "ejecución"
   ----------------------------------------------------------------------- */
if (typeof ResizeObserver !== "undefined") {
  // ResizeObserver es más preciso que window.resize:
  // detecta cambios reales del elemento, no solo de la ventana
  const ro = new ResizeObserver(schedule);

  // Observamos solo el wrapper del título,
  // no toda la página (menor costo y más intención)
  ro.observe(wrap);
}

// Fallback clásico:
// algunos navegadores antiguos no soportan ResizeObserver,
// así que escuchamos resize de la ventana.
window.addEventListener("resize", schedule, { passive: true });

// Primera ejecución manual:
// garantiza que el título se ajuste correctamente
// al cargar la página, incluso sin eventos previos.
requestAnimationFrame(schedule);
```

## AQUÍ ESTÁ EL CÓDIGO A ANALIZAR:

(pegas aquí el código)
