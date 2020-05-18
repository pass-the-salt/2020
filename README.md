# Requirements

Jekyll v4.0.1

Prefer to use `gem` and beware that older Debian packages might interfer, e.g. (be root!):

```
# apt-get remove jekyll
# apt-get remove ruby-liquid
# gem uninstall jekyll
# gem2.5 uninstall jekyll
# apt-get install ruby-dev

# gem install jekyll
// or to force:
# gem install jekyll -v '4.0.1'

# gem install jekyll-paginate
```

# Compilation

`--future` to preview the future news.

```
jekyll serve --future
```

For last generation before commit and push to production, use: 

```
JEKYLL_ENV=production jekyll serve
```

That way, you will generate good expand of `site.url` expression to your current production URL (`url` parameter in `_config.yml`). 

# Server setup to update the site automatically

```
a2enmod cgi
systemctl restart apache2
chown -R www-data:www-data /var/www/2018
chown -R www-data:www-data /var/www/2018-passthesalt
apt-get install rsync

# Add to /etc/apache2/sites-available/2018-passthesalt-ssl.conf
    ScriptAlias /cgi-bin/ "/var/www/2018/cgi-bin/"
    <Directory "/var/www/2018/cgi-bin/">
        Options +ExecCGI
        AddHandler cgi-script .cgi
    </Directory>

```

Then add the CGI URL to a Github webhook:
Go to the settings of your repository, click on "webhooks & Services" and "Add webhook".
