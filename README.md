# Multivacs Blog ✍️
---

A minimal, responsive, and feature-rich Jekyll theme for technical writing.


## What It Does
---

- Blog técnico con posts escritos en Markdown
- Traduce el Markdown a HTML
- Soporte de funciones Latex
- Tema oscuro


## Technology Stack
---

**Theme**: Chirpy Jekyll Theme
**Static generator**: Jekyll
**Testing**: 
**Deployment**: GitHub Actions


## Quick Setup
---

### Prerequisitos
- ruby

### Instalar
```bash
gem install bundler
bundle install
```

## How to run

`bundle exec jekyll serve`

[Getting Started](https://chirpy.cotes.page/posts/getting-started/)

## Estructura del proyecto
---
```
blog.multivacs.com/
├── _data/                          # idiomas, autores, contacto
├── _drafts/                        # borradores de posts
├── _includes/                      # borradores de posts
├── _layouts/                       # borradores de posts
├── _plugins/                       # borradores de posts
├── _posts/                         # borradores de posts
├── _sass/                          # preprocesador CSS añadiendo variables, anidamiento 
├── _site/                          # sitio estático generado
├── _tabs/                          # pestañas de navegación de las páginas
├── .github/                        # github actions para desplegar la página
├── .husky/                         # lint commit messages, code, and run tests
├── assets/                         # elementos estáticos (img, favicons, js, css)
│   ├── css/                        
│   ├── img/                        
│   ├── js/                         
│   └── lib/                        
│
├── docs/
├── tools/
├── _config                         # archivo principal de configuración
├── Gemfile                         # archivo de paquetes gem de Ruby para bundle
├── package.json
└── README.md
```

## License
---

This project is published under [MIT License][license].

[gem]: https://rubygems.org/gems/jekyll-theme-chirpy
[ci]: https://github.com/cotes2020/jekyll-theme-chirpy/actions/workflows/ci.yml?query=event%3Apush+branch%3Amaster
[codacy]: https://app.codacy.com/gh/cotes2020/jekyll-theme-chirpy/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade
[license]: https://github.com/cotes2020/jekyll-theme-chirpy/blob/master/LICENSE
[jekyllrb]: https://jekyllrb.com/
[clipartmax]: https://www.clipartmax.com/middle/m2i8b1m2K9Z5m2K9_ant-clipart-childrens-ant-cute/
[demo]: https://cotes2020.github.io/chirpy-demo/
[wiki]: https://github.com/cotes2020/jekyll-theme-chirpy/wiki
[contribute-guide]: https://github.com/cotes2020/jekyll-theme-chirpy/blob/master/docs/CONTRIBUTING.md
[contributors]: https://github.com/cotes2020/jekyll-theme-chirpy/graphs/contributors
[lib]: https://github.com/cotes2020/chirpy-static-assets
[vscode]: https://code.visualstudio.com/
[jetbrains]: https://www.jetbrains.com/?from=jekyll-theme-chirpy
