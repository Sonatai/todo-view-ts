# todo-view-ts

Die ist ei ganz kleines Todo-List Projekt um mit Vue vertraut zu werden.
Folgende Technologien / Packages habe ich verwendet:

-   Vite (+ Vue)
-   Typescript
-   Sass
-   ESLint + Plugins
-   Prettier (config)
-   Yarn
-   ElementPlus

Die Seite ist unter diesem Link aufrufbar: https://sonatai.github.io/todo-vue-ts/

## Was das Projekt beinhaltet

-   Das Hinzufügen, Bearbeiten und Löschen von Listen
-   Das Hinzufügen, Bearbeiten und Löschen von Todo-Items
-   Speicherung der Daten im LocalStorage
-   Schnabeltiere, um den Style aufzuwerten - nona

## Was das Projekt nicht beinhaltet

-   Anständiges Styling
-   Anständige UX/UI => Ideen sind da, können drüber quatschen
-   Testing
-   State-Management

## Probleme, die ich hatte

-   Ich konnte keine TodoItem-Componente nutzen. Anscheinend wird die Reference nicht runter gegeben? Ich weiß nicht 100%ig, was das Problem ist, aber ich hatte nicht die Zeit das jetzt zu fixen für die Demo 😵

-   State-Management und Reloading der Page => Ich hab es jetzt erzwungen mit einem reload, aber das sieht echt nicht gut aus. Adhoc habe ich aber keinen "einfachen" Weg gefunden und wollte jetzt nicht in Vuex oder ähnlichem eintauchen für dieses kleine Demo Projekt.

-   Wie man eine Prop typed und weitergibt. Ich bin mir immernoch nicht sicher, ob ich das 100% richtig gemacht habe 😅

-   Inputs. Die el-inputs haben gar nicht funktioniert - 100%ig weil ich etwas nicht richtg gemacht habe - und die inputs haben in einer Sub-Componente nicht funktioniert 🤔

## Was ich gelernt habe

-   Vue Projekt aufsetzen zusammen mit Vite, Sass, Typescript, ESLint und Prettier

-   Typen von Props sowie das verwenden von Props in Funktionen und als Initial-Values.

-   Verwendung von if-else sowie for-schleifen (mapping) im Vue-Context

-   Struktur eines Vue-Projektes im Allgemeinen 🤗
