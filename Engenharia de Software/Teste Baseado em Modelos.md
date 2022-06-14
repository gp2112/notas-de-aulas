# TDM - Teste Baseado em Modelos

- Já foi o método em que houve grande especulação por ser o ideal.

- **Modelo mais usado:** Máquina de Estados

```dot
digraph G {
	bgcolor="transparent"
	center=true
	1 -> 2 [taillabel="x/0"]
	3 -> 2 [taillabel="y/1"]
	3 -> 4 [taillabel="x/0"]
	4 -> 1 [taillabel="y/1"]
	1 -> 3 [taillabel="y/1"]
	2 -> 1 [taillabel="y/0"]
	2 -> 2 [taillabel="x/1"]

}

```


