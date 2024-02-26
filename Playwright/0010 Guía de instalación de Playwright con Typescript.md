# 🚀 Instalando el SuperCombo: Playwright + TypeScript + ESLint + Prettier 💻

¡Saludos, maestro del teclado y defensor del código elegante! 😎 Si estás aquí, es porque estás listo para elevar tu juego de automatización al siguiente nivel. Vamos a configurar un combo que hará que tu código brille más que las luces de Broadway.
## Paso 1: ¡Prepárate para el Espectáculo! 🌟

Asegúrate de tener **Node.js** y **NPM** instalados. Si no lo has hecho, ve a [nodejs.org](https://nodejs.org/) y tráelos a la fiesta.

## Paso 2: Playwright, el Actor Principal 🎭

Antes de comenzar el espectáculo echale un pequeño repaso a la [documentación oficial](https://playwright.dev/docs/intro)

Abre tu terminal y ejecuta el siguiente hechizo para invocar a Playwright junto con TypeScript:

`npm init playwright@latest`

Solo sigue las intrucciones y se te descarga un proyecto con la siguiente estructura: 

```
playwright.config.ts
package.json
package-lock.json
tests/
  example.spec.ts
tests-examples/
  demo-todo-app.spec.ts
```

## Paso 3: A darle vida al `package.json` **🛠️**

Solo copie esta estructura en **package.json** y listo: 
```json 
    "scripts": {
            "pw:install": "npx playwright install --with-deps",
            "test:plan": "npx playwright test --reporter=list --project=chromium --list",
            "test:ui": "npx playwright test --ui",
            "test:trace": "npx playwright show-trace",
            "test:debug": "npx playwright test --project=chromium --debug",
            "test": "npx playwright test --project=chromium",
            "test:firefox": "npx playwright test --project=firefox",
            "test:edge": "npx playwright test --project=edge",
            "test:iphone": "npx playwright test --project=iphone",
            "test:ci": "npx playwright test",
            "check-types": "tsc --noEmit --project tsconfig.json"
}
```

## **Paso 4: ESLint y Prettier, los Guardianes del Estilo 💂**

En la lucha por el formato consistente y la legibilidad, incorporen a sus filas ESLint y Prettier:

`npm install eslint prettier --save-dev`

Luchen contra la anarquía del código con la configuración de ESLint:

`npx eslint --init`