---
title: "2022 05 30  Test Post"
date: 2022-05-28T16:46:55-06:00
draft: false
categories: ["planet express"]
tags: [human]
images: [AmyWong.png]
---
Lorem ipsum dolor sit amet consectetur adipisicing elit. Quidem excepturi aspernatur nobis, officiis necessitatibus iure doloremque aperiam impedit placeat officia provident sed sequi fuga asperiores consequatur possimus omnis debitis nemo?

{{< img-index "0" "Test Post Picture" >}}

```go-html-template
{{/*  production options  */}}
{{- $opts := dict "minify" true "target" "es2015" -}}
{{- /*  development options  */ -}}
{{- if eq hugo.Environment "development" -}}
{{- $opts = dict "sourceMap" "inline" "target" "es2015" -}}
{{- end -}}
{{- $built := resources.Get . | js.Build $opts | fingerprint }}
<script type="text/javascript" src="{{ $built.RelPermalink }}" integrity="{{ $built.Data.Integrity }}"></script>
```
