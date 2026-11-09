# TO DO

Below I describe the typical steps to follow once the repository has been copied. These are the manual steps, although I usually use scripts that do almost everything via APIs.


## STEPS


### Local

- If new project (not fork):
  - Copy [var_domain project files](https://github.com/var_owner/var_domain)
  - `git submodule add https://github.com/seacomoseo/sansoul.git core`
- Else if fork:
  - Download submódule theme files: `git submodule update --init --recursive`
- `hugo.yml` ⏩ `baseURL` ("var_domain") + `params.owner`, `repo`, `worker` (+ `netlify` only for a Netlify mirror) ⏩ `sh do root-docs`
- Run it: `sh do dev` (fast) or `sh do local` (production build + local Worker for forms/commerce)
- GitHub secrets: `CLOUDFLARE_API_TOKEN` (account token), `GL_PAT` (GitLab backup), `NETLIFY_AUTH_TOKEN` (only with a Netlify mirror)
- Design
  - You can edit any file with the same structure of theme sansoul
  - GENERAL
    - `hugo.yml`
    - `data/*.{yml,md}`
  - IMG + LOGO + FAVICON
    - `uploads/` folder ⏩ [Compress image tool](https://compressor.io/)
      - `base/poster.png`
      - `logo.svg`
      - `logo.png`
      - `icon.png`
      - `favicon.ico` ⏩ [Favicon converter tool](https://favicon.io/favicon-converter/)
  - FONTS
    - Fonts that not be in Google Fonts:
      - .otf/.ttf files in `assets/fonts` + rename
      - You need the `sansoul_tools` project in `../_tools` folder
      - Run `do fonts` comand
      - `Family` + `Style` + `Weight` must match in `styles.yml ⏩ fonts` + `_fonts.scss` (and disable `fonts.google` if appropriate)
  - CONTENT
    - `content/*`
      - `page/divisores.md` ⏩ remove
      - SCRAP
        - Copy [this Spreadsheet Layout](https://docs.google.com/spreadsheets/d/1bJQaAFoBAwHhWz_WFRIHlkHoDmZZyT8H8NtdCnSTdaU)
        - First scrap with Screaming Frog and paste `url` and `title`
        - Second scrap with `IMPORTXML` formula in `content-start` tab
        - If need HTML content
          - Three scrap with `Web Scraper` chrome extension and paste in `content-scrap` tab
          - Copy `content-start` tab into `content-next` and get `body_code` (by `content-scrap`) with `VLOOKUP` formula
          - Copy `body_code` column to `body`, replace double quotes, [convert to Markdown](https://smalldev.tools/html-to-markdown-converter-online) and clean it
          - Paste in `file.md` in `./Downloads` and run `_tools/md-replaces.command`
          - Check `file_new.md` content:
            - headers: `^#`
            - images: `!\[.+?\)`
            - links: `(^|[^!])\[.+?\)`
            - internal links: `https?://(www\.)?example\.com`
          - Paste in sheet
        - Export to CSV like `./Downloads/file.csv` and run `_tools/csv-to-md.command`
        - Move files from `markdown_files` to `blog` project
  - HTML: `data/config.yml ⏩ langs[*].html.{head,body}`
  - CSS: `assets/_custom.scss` ⏩ `{*,_variables-custom.scss,_custom.scss}`
  - JS: `assets/custom.js`
  - ROBOTS: `assets/robots.txt`
  - LLMS: `assets/llms.txt`
  - MEDIA: `media/*`
  - REDIRECTS: `data/redirects.yml`
  - Try in Safari and Firefox
  - Check in [W3 Validator](https://validator.w3.org/)
  - Check in [PageSpeed Insights](https://pagespeed.web.dev/)


### After client validate web


#### Domain

- Cloudflare Workers (default)
  - The domain zone must be in Cloudflare
  - Cloudflare ⏩ `Workers & Pages ⏩ var_name ⏩ Settings ⏩ Domains & Routes ⏩ Add ⏩ Custom domain` ⏩ `var_domain` and `www.var_domain`
- If Netlify mirror (`params.netlify`; the CI creates the site)
  - [`Domain Management / settings`](https://app.netlify.com/sites/var_name/settings/domain)
  - `Add custom domain`
  - `Check DNS configuration` Copy
  - Add `DNS Records` copied from Netlify to Domain gestor:
    - From: `var_domain`
      DNS Record: `ALIAS`, `ANAME` or `flattened CNAME`
      To: `apex-loadbalancer.netlify.com`
    - From: `var_domain`
      DNS Record: `A`
      To: `75.2.60.5`
    - From: `www`
      DNS Record: `CNAME`
      To: `var_name.netlify.app.`
    - Maybe you need to eliminate the previous records with similar names
  - `Verify DNS configuration`
  - If it does not work after a while, try `Set as main domain` in the `www` version and also in te `nowww` version


#### Forms

- If SanSoulSend Form
  - Add domain and emails in [GSS](https://docs.google.com/spreadsheets/d/1yQEoxReqnvQbQ5LkGnhUvu2_Aa-PhGfFztoRG1qY6iM/edit?gid=0#gid=0)
- If Worker Form (`action: worker`)
  - `params.worker_vars` + Worker secrets (`FORMS_ADMIN_TOKEN`, Gmail…): see `core/README-ROOT.md`
- [formsubmit.co](https://formsubmit.co/)
- If Google Form: [Tutorial](https://seacomoseo.com/instrucciones/#google-forms)


#### [Google Analytics](https://analytics.google.com/)

- `Admin ⏩ Libre acount ⏩ New property ⏩ ...` copy ID
- `data/config.yml ⏩ ga4` ⏩ paste ID
- `Ajustes de datos`
  - `Recogida de datos`
    - `Recogida de datos de Google signals ⏩ Empezar`
    - `Consentimiento de recogida de datos de usuario` ⏩ Check
  - `Conservación de datos ⏩ Conservación de datos de eventos ⏩ 14 meses ⏩ Guardar`
- `Eventos clave ⏩ Nuevo eventos clave ⏩ Nombre de evento nuevo` ⏩ add `contact`
- `Definiciones personalizadas ⏩ Crear dimensión personalizada ⏩ Nombre de la dimensión + Parámetro de evento` ⏩ add `ID + id` + `Label + label` + `Type + type`


#### [Google Search Console](https://search.google.com/search-console)

- Add property
- Verify versions ⏩ `data/config.yml`
  - `ga4`
  - `g_site_verify`
  - `g_file_verify`
  - DNS:
    From: `@`
    DNS Record: `TXT`
    To: `google-site-verification=[g_site_verify]`
- Link with Analytics
- Add sitemap.xml


#### [Google My Business](https://business.google.com/)

- `Add company ⏩ ...` ⏩ wait 13 days to receive postal and insert code to verify


#### [Disqus](https://disqus.com/)

- `data/config.yml ⏩ disqus`


#### Collaborators

- [Google Analytics](https://analytics.google.com/) ⏩ `Admin ⏩ Libre acount ⏩ Site ⏩ Property access management ⏩ Add users` ⏩ Add emails of collaborators with role `Reader` or `Admin`.
- [Google Search Console](https://search.google.com/search-console) ⏩ `Site ⏩ Settings ⏩ Users and permissions ⏩ Add user` Add emails of collaborators with `Full` permission
- [Google My Business](https://business.google.com/)
  - `Site ⏩ Users ⏩ Add users` ⏩ Add emails of collaborators with role `Owner`


##### Services Layout

1. [Servicios var_domain](https://drive.google.com/file/d/1trq28fMfEVwoZOk4ue0tJzAJDZtj64BK) ⏩ `File ⏩ Make a copy` ⏩ Select client directory.
1. Change the info.
1. `Share` ⏩ Add emails of collaborators with `Editor` permission.


##### Delivery

Send to all collaborators next:

###### WhatsApp

```md
*ENTREGA WEB var_domain*

Te dejo aquí este mensaje como referencia (también te lo paso por email con el asunto `ENTREGA WEB var_domain`).

En el siguiente enlace tienes instrucciones sobre cosas referentes a tu sitio web (cómo modificar cosas, información extra, ect.):

https://seacomoseo.com/entrega/

No es necesario que lo veas, solo lo es si quieres hacer cosas por tu cuenta o si no estoy disponible.

¡Un saludo!
```

###### Mail

```
Asunto: ENTREGA WEB var_domain
Cuerpo:
Te dejo aquí este email como referencia.

En el siguiente enlace tienes instrucciones sobre cosas referentes a tu sitio web (cómo modificar cosas, información extra, ect.):

https://seacomoseo.com/entrega/

No es necesario que lo veas, solo lo es si quieres hacer cosas por tu cuenta o si no estoy disponible.

¡Un saludo!
```

## GADS

### GA4

- Vincular
  - `Herramientas`
  - `Gestor de datos`
  - `Google Analytics (GA4) & Firebase ⏩ Detalles`
  - Buscar proyecto y ⏩ `Vincular`
- Importar conversiones
  - `Objetivos`
  - `Conversiones`
  - `Resumen`
  - `Nueva acción de conversión`
  - `Importar`
  - `Propiedades de Google Analytics 4`
  - `Web`
  - `Continuar`
  - Seleccionar `contact_click` y `contact_form_submit`
  - `Importar y continuar`
- Cambiar a `Maximizar conversiones`
  - `Campañas`
  - `⚙️`
  - `Puja`
  - `Cambiar estrategia de puja`
  - `¿En qué quieres centrarte? ⏩ Conversiones`
