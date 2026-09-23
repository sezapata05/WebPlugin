# Cursor WebPlugin

## English

This workspace has two Cursor project rules. They apply only while the `WebPlugin` folder is the open workspace. They watch the active Google Chrome tab, read the page, and answer in the Agent chat. They never type, click, or submit anything in the browser.

### Before you start

1. Open this folder (`WebPlugin`) as the Cursor workspace. Files in `.cursor/rules/` load only for this project.
2. Open **Customize → Rules**. Under the project rules, both of these must show the type **Always Apply**:
   - `python_exercises`
   - `programming_multiple_choice`
3. Use the **Agent** chat. These rules do not run in Cursor Tab or in inline edit (Cmd+K).
4. In Google Chrome, open the page you want the agent to read and leave that tab in front. If you switch tabs or move to another section, the agent follows the tab that is active.
5. Send each command as its own message, exactly as written below. While the agent is watching and still has nothing to answer, it writes nothing in the chat.

### Rule 1 — Python exercises

File: `.cursor/rules/python_exercises.mdc`

The agent looks for a Python problem that is not marked as solved, accepted, or correct. It writes a solution, runs it on your machine, tests edge cases, and replies with code only.

#### Steps

1. Open the exercise page in Chrome. Leave that tab active.
2. In the Agent chat, send:

   ```text
   i'm ready
   ```

3. The agent reads the active tab in a loop.
   - If the page is still loading, shows another screen, has no problem statement, or the exercise is already solved, it waits and reads again. It does not message you.
   - If you change tabs or sections, it follows the active tab.
4. When a pending Python exercise is on the screen, the agent reads the full statement, the constraints, and the input and output examples. It writes a correct and simple solution, runs it locally, and fixes any errors it finds.
5. The chat reply is a single Python block. There is no title, no explanation, and no text before or after. You copy that code yourself. The agent does not paste it into the page, and it does not click Submit, Run, or Check.
6. To cancel before an answer arrives, send:

   ```text
   stop
   ```

   The agent stops immediately and does not send any code.

#### If a detail is missing

If a required detail is not on the page, the reply is one sentence that says what is missing. That is the only case in which the reply is not code.

### Rule 2 — Programming and logic questions

File: `.cursor/rules/programming_multiple_choice.mdc`

The agent answers programming and logic questions from the active tab. It ignores every other topic. The answers stay in the chat. It does not select options or submit the form in Chrome.

After you start it, it stays active. It answers the questions it sees, then keeps reading. It also answers new questions that appear later, until you send the stop phrase.

#### Answers only

1. Open the question page in Chrome. Leave that tab active.
2. In the Agent chat, send:

   ```text
   response
   ```

3. The agent reads the active tab in a loop. Until it sees a programming or logic question, it writes nothing.
4. It answers every matching question:
   - If the question has options, it chooses one.
   - If the question has no options, it gives a short and precise answer.
   - There is no title and no explanation.

   Example:

   ```text
   1. B
   2. use a set
   ```

5. It keeps watching. When you move to the next question, it answers that one in the chat as well.
6. To stop it, send this exact phrase:

   ```text
   strop, no more
   ```

   The agent stops immediately and does not send another answer.

#### Answer and a short reason

1. Use the same setup: the question page is open, and that Chrome tab is active.
2. Send:

   ```text
   response - explain
   ```

3. The agent answers the same kinds of questions and adds one brief justification for each answer.

   Example:

   ```text
   1. B — the loop index starts at 0.
   2. use a set — lookup stays constant time.
   ```

4. It keeps watching and answering until you send:

   ```text
   strop, no more
   ```

`response` and `response - explain` are different commands. Send one of them. The stop phrase is the same for both.

### What neither rule does

- They do not fill in fields, choose options, paste code, or click Submit, Enviar, Run, or Check.
- They do not ask you to paste the page into the chat when they can read it.
- They do not write in the chat while they are waiting for a pending exercise or for a programming or logic question.
- They do not run in any workspace other than this one.

### Commands

| You send | Rule | What happens |
| --- | --- | --- |
| `i'm ready` | `python_exercises` | It watches Chrome until a pending Python exercise appears, then it replies with code only. |
| `stop` | `python_exercises` | It stops watching and does not send code. |
| `response` | `programming_multiple_choice` | It watches Chrome and answers programming or logic questions with no explanation, until you stop it. |
| `response - explain` | `programming_multiple_choice` | It does the same as `response`, and adds a brief justification for each answer. |
| `strop, no more` | `programming_multiple_choice` | It stops watching and does not send another answer. |

## Español

Este workspace tiene dos reglas de proyecto de Cursor. Se aplican solo mientras la carpeta `WebPlugin` es el workspace abierto. Vigilan la pestaña activa de Google Chrome, leen la página y responden en el chat del Agent. Nunca escriben, hacen clic ni envían nada en el navegador.

### Antes de empezar

1. Abre esta carpeta (`WebPlugin`) como workspace de Cursor. Los archivos de `.cursor/rules/` se cargan solo para este proyecto.
2. Abre **Customize → Rules**. En las reglas del proyecto, estas dos deben mostrar el tipo **Always Apply**:
   - `python_exercises`
   - `programming_multiple_choice`
3. Usa el chat del **Agent**. Estas reglas no se ejecutan en Cursor Tab ni en el editado en línea (Cmd+K).
4. En Google Chrome, abre la página que quieres que el agente lea y deja esa pestaña al frente. Si cambias de pestaña o pasas a otra sección, el agente sigue la pestaña que esté activa.
5. Envía cada comando en su propio mensaje, exactamente como está escrito abajo. Mientras el agente vigila y todavía no tiene nada que responder, no escribe nada en el chat.

### Regla 1 — Ejercicios de Python

Archivo: `.cursor/rules/python_exercises.mdc`

El agente busca un problema de Python que no esté marcado como resuelto, aceptado o correcto. Escribe una solución, la ejecuta en tu máquina, prueba los casos límite y responde solo con el código.

#### Pasos

1. Abre la página del ejercicio en Chrome. Deja esa pestaña activa.
2. En el chat del Agent, envía:

   ```text
   i'm ready
   ```

3. El agente lee la pestaña activa en bucle.
   - Si la página sigue cargando, muestra otra pantalla, no tiene enunciado o el ejercicio ya está resuelto, espera y vuelve a leer. No te escribe.
   - Si cambias de pestaña o de sección, sigue la pestaña activa.
4. Cuando hay un ejercicio de Python pendiente en la pantalla, el agente lee el enunciado completo, las restricciones y los ejemplos de entrada y salida. Escribe una solución correcta y simple, la ejecuta en local y corrige los errores que encuentre.
5. La respuesta del chat es un único bloque de Python. No hay título, ni explicación, ni texto antes o después. Copias ese código tú. El agente no lo pega en la página y no pulsa Submit, Run ni Check.
6. Para cancelar antes de que llegue una respuesta, envía:

   ```text
   stop
   ```

   El agente se detiene de inmediato y no envía ningún código.

#### Si falta un dato

Si un dato necesario no está en la página, la respuesta es una frase que dice qué falta. Es el único caso en el que la respuesta no es código.

### Regla 2 — Preguntas de programación y lógica

Archivo: `.cursor/rules/programming_multiple_choice.mdc`

El agente responde las preguntas de programación y lógica de la pestaña activa. Ignora cualquier otro tema. Las respuestas se quedan en el chat. No selecciona opciones ni envía el formulario en Chrome.

Después de que lo inicias, se mantiene activo. Responde las preguntas que ve y luego sigue leyendo. También responde las preguntas nuevas que aparezcan después, hasta que envíes la frase para detenerlo.

#### Solo las respuestas

1. Abre la página de las preguntas en Chrome. Deja esa pestaña activa.
2. En el chat del Agent, envía:

   ```text
   response
   ```

3. El agente lee la pestaña activa en bucle. Hasta que ve una pregunta de programación o lógica, no escribe nada.
4. Responde cada pregunta que corresponda:
   - Si la pregunta tiene opciones, elige una.
   - Si la pregunta no tiene opciones, da una respuesta corta y precisa.
   - No hay título ni explicación.

   Ejemplo:

   ```text
   1. B
   2. use a set
   ```

5. Sigue vigilando. Cuando pasas a la siguiente pregunta, también la responde en el chat.
6. Para detenerlo, envía esta frase exacta:

   ```text
   strop, no more
   ```

   El agente se detiene de inmediato y no envía otra respuesta.

#### Respuesta y una razón breve

1. Usa la misma preparación: la página de las preguntas está abierta y esa pestaña de Chrome está activa.
2. Envía:

   ```text
   response - explain
   ```

3. El agente responde los mismos tipos de preguntas y añade una justificación breve para cada respuesta.

   Ejemplo:

   ```text
   1. B — el índice del bucle empieza en 0.
   2. use a set — la búsqueda se mantiene en tiempo constante.
   ```

4. Sigue vigilando y respondiendo hasta que envíes:

   ```text
   strop, no more
   ```

`response` y `response - explain` son comandos distintos. Envía uno de los dos. La frase para detener es la misma para ambos.

### Qué no hace ninguna de las dos reglas

- No rellenan campos, no eligen opciones, no pegan código y no pulsan Submit, Enviar, Run ni Check.
- No te piden que pegues la página en el chat cuando pueden leerla.
- No escriben en el chat mientras esperan un ejercicio pendiente o una pregunta de programación o lógica.
- No se ejecutan en ningún workspace que no sea este.

### Comandos

| Envías | Regla | Qué pasa |
| --- | --- | --- |
| `i'm ready` | `python_exercises` | Vigila Chrome hasta que aparece un ejercicio de Python pendiente y luego responde solo con el código. |
| `stop` | `python_exercises` | Deja de vigilar y no envía código. |
| `response` | `programming_multiple_choice` | Vigila Chrome y responde las preguntas de programación o lógica sin explicación, hasta que lo detienes. |
| `response - explain` | `programming_multiple_choice` | Hace lo mismo que `response` y añade una justificación breve para cada respuesta. |
| `strop, no more` | `programming_multiple_choice` | Deja de vigilar y no envía otra respuesta. |
