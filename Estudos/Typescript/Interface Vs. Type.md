---
tags:
- Typescript
---

# Pergunta
Qual a diferença entre ``interfaces`` e ``types`` no [[Typescript]]?

Exemplo:
```typescript
interface X {
	a: string
	b: string
}

type X = {
	a: string
	b: string
}
```
[Referencia: StackOverflow](https://stackoverflow.com/questions/37233735/interfaces-vs-types-in-typescript)

# Resposta
``types`` e ``interfaces`` são bem similares em diversos casos, e é possivel usar ambos de forma livre. Praticamente todas as funcionalidades disponiveis em ``interfaces`` estão disponiveis em ``types``, a principal distinção é que tipos não podem ser "re-abertos" para adicionar novas propriedades, diferente de ``interfaces`` que sempre podem ser extendidas

![[Example 01 - Interface Vs. Type.png]]

***Obs.** Na maioria das vezes é possivel decidir entre ``types`` e ``interfaces`` baseado na preferencia de cada desenvolvedor, e caso seja necessario o uso especifico de um ou outro, o [[Typescript]] avisará. Caso queira uma [[(Definição) Heuristica]], use ``interfaces`` até que seja necessario usar funcionalidades de ``types``*
[Referencia: Typescript Lang](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces:~:text=typed%20type%20system.-,Differences%20Between%20Type%20Aliases%20and%20Interfaces,-Type%20aliases%20and)