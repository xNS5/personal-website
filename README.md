# michaelkennedy.dev

This is the repository for my personal website using [Zola](https://www.getzola.org/) -- a static website generator written in rust. 

I decided to use Zola for a few reasons: first and foremost, I'm not really doing anything super intense which would require a heroku dyno or AWS/Azure.
I could easily have thrown something together with a Node/Django/Flask/Spring Boot/Flutter backend, but realistically speaking I may update the content on these pages
every once in a while; I may update my resume, add a new project description file, but that's about it. Second, I'm a big fan of markdown and Zola's content pages
use markdown. Lastly, cost. I'm an unemployed new grad, so putting all of that time and money into a website that I wouldn't realistically be updating every day or
week seems like a waste.

Zola uses this neat thing called "Shortcode" to fill in content. For example in my `base.html` file, I use shortcode in a javascript function which pushes `<a/>`
tags to the navbar -- reading in data from the configuration file (`config.toml`). It has basic loops (`{% for foo in bar %} {% endfor %}`) and variable
setting (`{% set foo = bar %}`). There are some other built-in functions which can be seen on the Zola documentation website.

