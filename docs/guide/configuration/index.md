---
title: Configuration
---

# {{ $frontmatter.title }}

AEM Vite provides a factory configuration which enables multiple different front end setups to be used at the same time. This means that you can work on multiple codebases without ever having to stop and switch between configurations.

## OSGI configuration

Within your projects OSGI configuration folder, create a new file called:

> xyz.cshaw.aem.vite.impl.ViteDevServerConfigImpl-project.cfg.json

Because AEM Vite allows factories, you can create as many projects as you would like and you only need to replace `project` with something unqiue.

::: warning .cfg.json not working?
If using `.cfg.json` doesn't work for you, switch to the XML format `.config.xml`. Read more about about creating [OSGI configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en).
:::

## Properties

### Automatic injection?

Use automatic injection which detects Vite's DevServer and strips away any defined ClientLibs along with injecting Vite's client module.

**Key:** `automatic.injection`<br>
**Type:** `Boolean`<br>
**Default:** `true`

### ClientLib categories

A list of ClientLib categories that will be used to strip certain CSS/JS from the page.

**Key:** `clientlib.categories`<br>
**Type:** `String[]`

### Content paths

A list of content paths where injection should occur.

**Key:** `content.paths`<br>
**Type:** `String[]`

### Manual injection selector

A custom selector to use when automatic injection is disabled. You can enable AEM Vite by adding your custom selector to the content URL. E.g.

> http://localhost:4502/content/project/mypage.vite.html

**Key:** `manual.injection.selector`<br>
**Type:** `String`<br>
**Default:** `vite`

### DevServer protocol

Which protocol should be used to contact Vite's DevServer?

**Key:** `devserver.protocol`<br>
**Type:** `String`<br>
**Accepts:** `http` or `https`<br>
**Default:** `http`

### DevServer hostname

Which hostname should be used to contact Vite's DevServer?

**Key:** `devserver.hostname`<br>
**Type:** `String`<br>
**Default:** `localhost`

### DevServer Docker

Enable this option if your AEM instance is running within Docker. This will ensure that the DevServer check works correctly via `http://host.docker.internal`.

**Key:** `devserver.docker`<br>
**Type:** `Boolean`<br>
**Default:** `false`

### DevServer port

Which port should be used to contact Vite's DevServer?

**Key:** `devserver.port`<br>
**Type:** `Integer`<br>
**Default:** `3000`

### DevServer entrypoints

A list of entry points to inject onto the page.

**Key:** `devserver.entrypoints`<br>
**Type:** `String[]`

### Using React?

Enable this option is enabled when using React to ensure things work correctly.

**Key:** `using.react`<br>
**Type:** `Boolean`<br>
**Default:** `false`

## Example configuration

```json
{
  "automatic.injection": true,
  "clientlib.categories": ["<project>.base"],
  "content.paths": ["/content/<project>"],
  "manual.injection.selector": "vite",
  "devserver.protocol": "http",
  "devserver.hostname": "127.0.0.1",
  "devserver.docker": false,
  "devserver.port": 3000,
  "devserver.entrypoints": ["src/js/main.ts"],
  "using.react": false
}
```