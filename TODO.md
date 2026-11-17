# TO DO

`sh <engine>/do new <domain> --owner <org> --mails <client mails>` creates the private repo from this demo, the Cloudflare CI token, the GitLab backup, GA4, Search Console and the Drive files (plan first; `--apply` runs it). Below are only the steps it cannot do.


## STEPS


### Local

- Existing clone: `git submodule update --init --recursive`
- Run it: `sh do dev` (fast) or `sh do local` (production build + local Worker for forms/commerce)
- Save and publish: `sh do up ["message"]`; bring others' changes: `sh do down` (on a conflict both leave a ready prompt for an agent)
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
      - `base/icon.svg` (or `base/icon.png`) ⏩ the build generates the favicons (`base/favicon.ico` only to override)
  - FONTS
    - Google Fonts: just the family and weights in `data/styles.yml ⏩ fonts` (the build downloads them)
    - Other fonts: `.otf/.ttf` files in `assets/fonts` ⏩ `sh do fonts` ⏩ use the printed family and weights in `data/styles.yml ⏩ fonts`
  - CONTENT
    - `content/*`
      - SCRAP
        - Copy [this Spreadsheet Layout](https://docs.google.com/spreadsheets/d/1bJQaAFoBAwHhWz_WFRIHlkHoDmZZyT8H8NtdCnSTdaU)
        - First scrap with Screaming Frog and paste `url` and `title`
        - Second scrap with `IMPORTXML` formula in `content-start` tab
        - If need HTML content
          - Three scrap with `Web Scraper` chrome extension and paste in `content-scrap` tab
          - Copy `content-start` tab into `content-next` and get `body_code` (by `content-scrap`) with `VLOOKUP` formula
          - Copy `body_code` column to `body`, replace double quotes, [convert to Markdown](https://smalldev.tools/html-to-markdown-converter-online) and clean it
          - Check the Markdown content:
            - headers: `^#`
            - images: `!\[.+?\)`
            - links: `(^|[^!])\[.+?\)`
            - internal links: `https?://(www\.)?example\.com`
          - Paste in sheet
        - Export to CSV, convert each row to a Markdown file and move them to `content/`
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

- Cloudflare Workers (default): `sh do new --only cloudflare,gsc --production --apply` (zone, Worker custom domains, Search Console verification); then point the registrar to the printed nameservers and repeat
- If Netlify mirror (`params.netlify`; the CI creates the site)
  - [`Domain Management`](https://app.netlify.com/sites/var_name/settings/domain) ⏩ `Add custom domain` ⏩ copy the records from `Check DNS configuration` to the DNS ⏩ `Verify DNS configuration`


#### Forms

- If SanSoulSend Form
  - Add domain and emails in [GSS](https://docs.google.com/spreadsheets/d/1yQEoxReqnvQbQ5LkGnhUvu2_Aa-PhGfFztoRG1qY6iM/edit?gid=0#gid=0)
- If Worker Form (`action: worker`)
  - `params.worker_vars` + Worker secrets (`FORMS_ADMIN_TOKEN`, Gmail…): see `core/README-ROOT.md`
- [formsubmit.co](https://formsubmit.co/)
- If Google Form: [Tutorial](https://seacomoseo.com/instrucciones/#google-forms)


#### Google Analytics

- Google Signals: open the link printed by `sh do new` ⏩ `Recogida de datos de Google signals ⏩ Empezar`
- Once Search Console is verified: `Admin ⏩ Vinculaciones de productos ⏩ Search Console ⏩ Vincular`


#### [Google My Business](https://business.google.com/)

- `Add company ⏩ ...` ⏩ wait 13 days to receive postal and insert code to verify


#### [Disqus](https://disqus.com/)

- `data/config.yml ⏩ disqus`


#### Collaborators

- [Google My Business](https://business.google.com/)
  - `Site ⏩ Users ⏩ Add users` ⏩ Add emails of collaborators with role `Owner`


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
