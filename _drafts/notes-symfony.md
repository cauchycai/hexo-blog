# Symfony #

## Symfony versus Flat PHP ##

1. Actions methods can receive arguments
2. Setting layout in view files instead of in Control Class
3. View files have a naming format
4. Code in control class is simpler
5. Using getter/setter in DB Manager class
6. Should have an exception thrower method in Control Base Class (eg. createNotFoundException)
7. An independent view object
8. Routing configuration map written in yaml format
9. View object is related to route map
10. Having independent Request/Response Class
11. A controller method returns a Response object to the front controller who then send it
12. HTTP caching by Symfony has internal HTTP cache or more powerful tools such as Varnish
13. Being able to use open source tools developed by the Symfony community
14. Symfony uses [Twig][^1] templating engine by default

## Installing and Configuring Symfony ##

```
$ curl -LsS http://symfony.com/installer > symfony.phar
$ sudo mv symfony.phar /usr/local/bin/symfony
$ chmod a+x /usr/local/bin/symfony
```

## Creating Pages in Symfony ##

1. To use render(), the controller should extend `Symfony\Bundle\FrameworkBundle\Controller\Controller`




[^1]: http://twig.sensiolabs.org
