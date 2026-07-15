# Prueba privada: World + DFlow + x402 en Claude

Guía para la soft launch y monkey testing de la experiencia completa: conexión, login, creación de wallets, permisos, firmas, fondos, transferencias, swaps, mercados de predicción y servicios x402.

---

## Mensaje 1 de 5 — Preparación y reglas

Gracias por ayudar con esta soft launch. Van a recibir dos conectores para usar en Claude: **World** y **DFlow**. La prueba cubre la experiencia completa: conexión, login, creación de wallets, permisos, firmas, fondos, transferencias, swaps, mercados de predicción y servicios x402.

### Cómo probar

Compórtense como usuarios reales. Usen sus propias palabras, prueben en español, inglés o mezclado, y anoten cualquier momento de confusión.

En el primer intento de cada flujo, traten de resolverlo sin copiar exactamente el camino de otra persona. Si se bloquean, publíquenlo en el grupo. Después pueden ayudarse entre ustedes. El bloqueo inicial también es feedback valioso.

### Preparación obligatoria

1. Conecten World y DFlow en la superficie de Claude que les comparta.
2. Completen el inicio de sesión con SSO.
3. Creen **dos wallets de Solana** en Paybox.
4. Descubran y habiliten los grants, permisos o firmas que les pida el sistema.
5. Pídanle al agente que muestre sus wallets, direcciones y saldos iniciales.
6. Anoten cuántos pasos, clics, ventanas y aprobaciones hicieron. Reporten cualquier instrucción que resulte confusa.

### Reglas

- Esto usa dinero real. Usen montos mínimos: entre **$0.01 y $1** por operación.
- Fondeen únicamente con **USDC**. No agreguen SOL manualmente. Queremos comprobar que el gas sea patrocinado.
- Si no consiguen USDC, publiquen su dirección pública de Solana y les puedo enviar hasta $1.
- Nunca compartan seed phrase, private key, passkey, códigos de seguridad ni datos de tarjeta.
- Antes de aprobar una operación, revisen wallet, token, red, destinatario, monto, precio y comisión.
- Si el agente dice “success”, confirmen con saldo, posición y enlace de transacción. El mensaje del agente por sí mismo no confirma que ocurrió.
- Si una operación queda en `pending`, no la repitan. Pidan: `check the status of the existing request until it reaches a final state`.
- Guarden siempre `request_id`, enlace o hash de transacción, hora aproximada y evidencia.
- Hagan una operación a la vez.
- Si el monto cambia o aparece un gasto que no autorizaron, cancelen y repórtenlo.

---

## Mensaje 2 de 5 — Wallet, fondos y transferencias

### A. Wallet vacía

Antes de fondear, prueben estas acciones desde una wallet con 0 USDC y 0 SOL:

1. Pedir al agente que muestre wallets, saldos y capacidades disponibles.
2. Firmar un mensaje de prueba, por ejemplo: `sign the message "paybox soft launch test"`.
3. Intentar enviar **$0.01 USDC**.
4. Intentar hacer una predicción de **$0.10**.
5. Intentar usar un servicio x402 barato.

Aquí evaluamos si el agente:

- Detecta fondos insuficientes antes de gastar.
- Explica el problema claramente.
- Evita crear operaciones o posiciones fantasma.
- Propone una forma razonable de continuar.
- Mantiene los saldos intactos después del intento fallido.

### B. Fondeo en USDC

Fondeen solo una de las dos wallets. Dejen la otra completamente vacía.

Pueden:

- Pedirle al agente un enlace de MoonPay para comprar USDC.
- Enviar USDC desde una wallet externa.
- Pedir fondos en este grupo compartiendo únicamente su dirección pública.

Verifiquen:

- Que el enlace use la wallet, red, token y monto correctos.
- Que el saldo no cambie antes de completar el pago.
- Que el agente confirme la llegada consultando el saldo real.
- Que la wallet siga pudiendo operar sin SOL.

Ejemplo de intención, sin obligación de copiarlo literalmente:

> I need to fund this wallet with USDC. Give me the correct checkout link and show the destination address before I continue.

### C. Transferencias de USDC sobre Solana

Desde la wallet fondeada hagan dos envíos separados de **$0.01 USDC**:

1. A una dirección que ya tenga fondos.
2. A una dirección nueva o vacía, sin USDC y sin SOL. Puede ser su segunda wallet de Paybox.

Después de cada envío:

- Verifiquen el saldo del remitente y del destinatario.
- Confirmen que no tuvieron que agregar SOL.
- Guarden el `request_id` y el enlace de Solana.
- Revisen que el agente no confunda la wallet de origen cuando existen dos wallets.

Prueben además una instrucción ambigua, como:

> send one cent to my other wallet

El agente debería identificar qué información falta o pedir aclaración antes de mover fondos. Si escoge una wallet o un destinatario sin confirmar, cancelen y repórtenlo.

---

## Mensaje 3 de 5 — DFlow, World y x402

### D. DFlow: swaps y BONK

1. Pídanle al agente que descubra qué tokens y operaciones están disponibles.
2. Soliciten una cotización para cambiar entre **$0.10 y $1 de USDC a BONK**.
3. Antes de aprobar, revisen cuánto entregan, cuánto reciben, el precio estimado y cualquier costo.
4. Ejecuten el swap y verifiquen que bajó USDC y apareció BONK.
5. Envíen una pequeña cantidad de BONK a la segunda wallet vacía.
6. Verifiquen ambos saldos y que la wallet receptora no necesitó SOL.
7. Cambien parte o todo el BONK de vuelta a USDC.
8. Vuelvan a verificar los saldos y los enlaces de transacción.

Al final, después de terminar las pruebas gasless, pueden probar un swap pequeño de USDC a SOL y un envío de SOL si el conector lo ofrece. Marquen ese caso por separado.

### E. World: mercados de predicción

1. Pidan al agente que encuentre mercados activos y explique brevemente opciones, precios y vencimiento.
2. Intenten una predicción de **$0.10 desde la wallet vacía**.
3. Repitan desde la wallet fondeada.
4. Pueden usar un mercado de BTC a 5 o 15 minutos, un partido o cualquier mercado activo que aparezca.
5. Antes de ejecutar, pidan costo total, outcome elegido, posible retorno y comisiones.
6. Después de ejecutar, pidan las posiciones abiertas y el saldo restante.
7. Si se permite, cierren o vendan la posición.
8. Si el mercado se resuelve durante la prueba, intenten reclamar o redimir el resultado y confirmen el saldo.
9. Prueben también un monto superior al saldo disponible. Debe rechazarse claramente y sin gasto parcial.

Ejemplo natural:

> quiero apostar 10 centavos. muéstrame qué hay disponible, explícame las opciones y no ejecutes nada hasta que confirme.

### F. x402: descubrimiento y pagos

1. Pidan al agente que descubra al menos **tres servicios x402 compatibles con Solana**, indicando precio y utilidad.
2. Usen dos servicios baratos, manteniendo el gasto combinado por debajo de **$0.25**.
3. En uno, pidan algo abierto, como descubrir un servicio útil.
4. En el otro, pidan algo específico, como datos, noticias o información disponible en ese momento.
5. Verifiquen precio anunciado, cobro real, resultado entregado y saldo final.
6. Revisen si el agente identifica la red antes de intentar pagar.
7. Si aparece un servicio que requiere Base o una wallet EVM, no fondeen otra red. Reporten si el agente explicó claramente la incompatibilidad y ofreció una alternativa de Solana.

Son reportes importantes:

- Un pago sin resultado.
- Un resultado sin pago verificable.
- Un cobro superior a lo anunciado.
- Una afirmación de éxito sin cambio real.
- Una selección automática de un servicio incompatible.

---

## Mensaje 4 de 5 — Exploración libre y coordinación en Telegram

Además del recorrido obligatorio, cada persona debe probar al menos **cinco** variaciones. Escojan combinaciones distintas y anuncien en el grupo cuáles van a cubrir:

- Español, inglés y mensajes mezclados.
- Errores de escritura, nombres incompletos y lenguaje informal.
- Omitir monto, token, wallet de origen o destinatario.
- Pedir más dinero del disponible.
- Usar dos wallets y dar una orden ambigua.
- Pedir una cotización y luego cambiar el monto.
- Negar o cancelar una firma y revisar el estado final.
- Dejar una solicitud pendiente y consultar su estado sin repetirla.
- Abrir un chat nuevo después de finalizar una operación y pedir historial, saldo o posiciones.
- Pedir dos acciones encadenadas, por ejemplo comprar BONK y después enviar una parte.
- Repetir accidentalmente una instrucción ya completada y comprobar que no haya doble gasto.
- Intentar un token, red, dirección o servicio no compatible y evaluar la claridad del error.
- Desconectar y volver a conectar cuando no haya operaciones pendientes.
- Buscar lugares donde puedan reducirse clics, aprobaciones, ventanas o texto.
- Preguntar al agente si una operación ocurrió y comprobar si verifica antes de responder.
- Probar desde otro navegador o dispositivo, cuando sea posible.

Cuando terminen un flujo, pueden proponerle a otro tester una variante nueva. No envíen muchas órdenes simultáneas ni generen volumen artificial.

### Evidencia mínima

Cada tester debe entregar video de estos seis flujos:

1. Conexión y creación de wallet.
2. Fondeo.
3. Transferencia a una wallet vacía.
4. Swap y envío de BONK.
5. Predicción con fondos.
6. Pago x402.

Cada bug adicional debe tener su propio screenshot o clip cuando sea posible.

### Trabajo en el grupo

- Asignen IDs `T01` a `T06`.
- Publiquen resultados a medida que ocurren, incluidos los éxitos.
- Usen una etiqueta consistente: `[T03][WORLD-FUNDED][FAIL]`.
- Códigos sugeridos: `SETUP`, `EMPTY`, `FUND`, `USDC-FUNDED`, `USDC-EMPTY`, `BONK-SWAP`, `BONK-SEND`, `BONK-SELL`, `WORLD-EMPTY`, `WORLD-FUNDED`, `WORLD-CLOSE`, `WORLD-REDEEM`, `X402-DISCOVER`, `X402-PAY`, `SIGN`, `GRANT`, `UX`.
- Si alguien publica un problema, respondan sobre ese mismo mensaje cuando logren reproducirlo.
- Expliquen qué cambiaron al reproducir: navegador, idioma, monto, wallet, prompt o conector.
- Conserven el reporte del error inicial después de encontrar la solución. Publiquen la solución como respuesta.
- Cada screenshot o video debe tener su propio pie: escenario, acción, resultado y qué debemos mirar.
- Graben desde antes de enviar el prompt hasta después de verificar saldo, posición o transacción.
- Oculten información personal. Las direcciones públicas y enlaces de transacción se pueden compartir; los secretos y datos de pago no.

### Qué cuenta como hallazgo

- Dice que terminó, pero saldo, posición o transacción no coinciden.
- Cobra o firma sin explicar monto y costo.
- Usa la wallet, red, token, mercado u outcome equivocados.
- Duplica una operación.
- Queda pendiente sin una forma clara de consultar o recuperar.
- Muestra un error técnico imposible de entender.
- La interfaz obliga a pasos innecesarios o no deja claro qué aprobar.
- El agente inventa el resultado o responde sin verificar.

---

## Mensaje 5 de 5 — Cómo reportar y cerrar la prueba

### Estados

- `PASS`: quedó confirmado con saldo, posición o transacción.
- `FAIL`: el resultado fue incorrecto.
- `BLOCKED`: no fue posible continuar.
- `UX`: funcionó, pero fue confuso, lento o tuvo pasos innecesarios.

### Severidad

- `blocker`: impide completar el recorrido.
- `high`: dinero, permisos, wallet, duplicación o estado incorrecto.
- `medium`: falla recuperable o mensaje poco claro.
- `low`: texto, diseño, clics o fricción menor.

### Reporte de resultado exitoso

```text
[T##][ESCENARIO][PASS]
Fecha y hora:
Dispositivo / sistema / navegador:
Claude.ai o Claude Code:
Idioma usado:
Prompt exacto:
Wallet de origen: últimos 6 caracteres
Monto y token:
Saldo antes / después:
request_id:
Enlace de transacción:
Tiempo aproximado:
Notas:
Video o screenshot:
```

### Reporte de error, bloqueo o UX

```text
[T##][ESCENARIO][FAIL | BLOCKED | UX]
Severidad: blocker | high | medium | low
Qué intentaba hacer:
Pasos exactos:
Prompt exacto:
Qué esperaba:
Qué ocurrió:
Mensaje de error exacto:
Estado mostrado:
Saldo / posición antes y después:
request_id:
Enlace de transacción, si existe:
Fecha, hora y zona:
Dispositivo / sistema / navegador:
Claude.ai o Claude Code:
Conector usado:
Wallet: últimos 6 caracteres
¿Se cobró dinero?: sí / no / no sé
¿Es reproducible?: sí / no / no intenté
Video o screenshots:
Idea de mejora:
```

### Resumen final de cada tester

```text
TESTER:
Experiencia con cripto: ninguna | básica | intermedia | avanzada
Tiempo total:
Fondos reales usados:
Saldos iniciales y finales por wallet:
Conexión de World: PASS | FAIL | BLOCKED
Conexión de DFlow: PASS | FAIL | BLOCKED
SSO: PASS | FAIL | BLOCKED
Creación de dos wallets: PASS | FAIL | BLOCKED
Grants y firma: PASS | FAIL | BLOCKED
Fondeo USDC: PASS | FAIL | BLOCKED
Operación sin SOL: PASS | FAIL | BLOCKED
USDC a wallet con fondos: PASS | FAIL | BLOCKED
USDC a wallet vacía: PASS | FAIL | BLOCKED
Swap USDC → BONK: PASS | FAIL | BLOCKED
Envío de BONK: PASS | FAIL | BLOCKED
Swap BONK → USDC: PASS | FAIL | BLOCKED
Predicción sin fondos: PASS | FAIL | BLOCKED
Predicción con fondos: PASS | FAIL | BLOCKED
Ver/cerrar/redimir posición: PASS | FAIL | BLOCKED
Descubrimiento x402: PASS | FAIL | BLOCKED
Dos pagos x402: PASS | FAIL | BLOCKED
Variaciones libres completadas:
Número de bugs encontrados:
Número de transacciones exitosas:
Número de solicitudes pendientes o atascadas:
Número de operaciones cobradas sin resultado:
¿Hubo alguna diferencia de saldo sin explicar?: sí | no
¿El agente afirmó éxito incorrectamente?: sí | no
Claridad general, 1–5:
Confianza para usarlo con $10, 1–5:
Facilidad para recuperarse de un error, 1–5:
Momento más confuso:
Paso con más fricción:
Mejor parte:
Tres cambios prioritarios:
Links a todos los videos y evidencias:
```

### Rifa

Quienes intenten y documenten todo el recorrido entran en la rifa de **233 millones de UVD**.

Un bug bien documentado cuenta como prueba completada. La calidad de la evidencia forma parte del resultado.
