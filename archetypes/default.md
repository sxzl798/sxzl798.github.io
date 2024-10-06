+++
title = '{{ replace .File.ContentBaseName "-" " " | title }}'

categories: ["{{ trim (replace .File.Dir "posts/" "") "/" }}"]

date = {{ .Date }}
draft = true



+++
