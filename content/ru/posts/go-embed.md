---
date: 2022-10-11
linktitle: Расширяем возможности go:embed
menu:
  main:
    parent: /
prev: /
title: Расширяем возможности go:embed
weight: 10
tags:
  - "go"
  - "golang"
  - "embed"
  - "development"
categories:
  - "internals"
  - "golang"

summary: |
  В этой статье мы рассмотрим текущие возможности директивы для компилятора [go:embed](https://pkg.go.dev/embed), чего в ней не хватает и как добавить свои изменения. 
---

## **Введение**

Представим ситуацию когда мы хотим встроить файлы в наше приложение на go, например, шаблоны для кодогенерации или статику для http сервера, вот тогда и приходит на помощь директива [go:embed](https://pkg.go.dev/embed).

Описать что это такое, зачем и почему этим пользуются

## **Текущая проблема**

Описать приемущества и недостатки текущей реализации

## **Простое решение**
Показать как можно решить проблему не меняя самого языка

## **Решение с ковырянием исходного кода**

{{< highlight go "linenos=table,hl_lines=9 15-17,linenostart=199" >}}
// GetTitleFunc returns a func that can be used to transform a string to
// title case.
//
// The supported styles are
//
// - "Go" (strings.Title)
// - "AP" (see https://www.apstylebook.com/)
// - "Chicago" (see https://www.chicagomanualofstyle.org/home.html)
//
// If an unknown or empty style is provided, AP style is what you get.
func GetTitleFunc(style string) func(s string) string {
  switch strings.ToLower(style) {
  case "go":
    return strings.Title
  case "chicago":
    return transform.NewTitleConverter(transform.ChicagoStyle)
  default:
    return transform.NewTitleConverter(transform.APStyle)
  }
}
{{< / highlight >}}


{{< highlight html >}}
<section id="main">
  <div>
    <h1 id="title">{{ .Title }}</h1>
    {{ range .Data.Pages }}
      {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
{{< /highlight >}}