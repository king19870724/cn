---
layout: default
title: Creating a controller
permalink: /creating-a-spring-controller/
sitemap:
    priority: 0.7
    lastmod: 2019-02-01T00:00:00-00:00
---

# <i class="fa fa-bolt"></i> Creating a Spring controller

## Introduction
## 介绍

_Note: this sub-generator is much simpler than the [entity sub-generator]({{ site.url }}/creating-an-entity/) that creates full CRUD entities_

_提示：这个子生成器创建全功能CRUD实体要比[entity sub-generator]({{ site.url }}/creating-an-entity/) 简单。_

This sub-generator generates a Spring MVC REST Controller. It is also able to create simple REST methods.
它同时也能生成 SpringMVC REST 的Controller和简单的REST方法。

In order to generate a "Foo" Spring MVC REST controller, just type:
生成一个名为Foo的Controller只需要输入

`jhipster spring-controller Foo`


The sub-generator will ask you which method you want to generate: just answer the method name and the HTTP verb you want to use, and a simple method will be generated.

这时这个生成器会询问你待生成的方法名和请求类型（get，post..）后生成所添加的方法。 

## Can we document this Spring MVC REST Controller with Swagger?
## 是否可以使用Swagger管理SpringMVC REST Controller文档

Yes! In fact it's already done! In `dev` mode, just use the `Administration > API` menu to access Swagger UI and start using the generated controller.
是的！实际上已经在这样做了！在 "dev" 模式下，在`Administration > API` 菜单打开swagger 界面，就可以了。

## Can we add security to Spring MVC REST Controllers?
## 是否在SpringMVC REST Controller中可以添加安全范围控制？

Yes! Just add Spring Security's `@Secured` annotation on your class or on your methods, and use the provided `AuthoritiesConstants` class to restrict access to specific user authorities.

是的！在对应类或者方法 添加sping security的标签`@Secured`，并用`AuthoritiesConstants`类限制特定的用户具有访问权限。

## Can we proxy it from our Microservice Gateway dev server?
## 是否可以使用微服务网关代理生成的Controller？

Yes! By adding the servicename to the context of the proxy in webpack/webpack.dev.js
是的！在webpack/webpack.dev.js中添加服务名称，即可。

```javascript
module.exports = (options) => webpackMerge(commonConfig({ env: ENV }), {
    devtool: 'eval-source-map',
    devServer: {
        contentBase: './target/www',
        proxy: [{
            context: [
                '/<servicename>',
                /* jhipster-needle-add-entity-to-webpack - JHipster will add entity api paths here */
                ....
```
