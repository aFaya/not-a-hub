---
title: Difference between Subtyping and Inheritance
url: SubtypeAndInheritance
tags:
  - Typing
date: 2018.11.01
author: fuafa
type: todo
desc: 好像没什么好说的, 因为维基百科已经解析得很到位了, 暂且占个位置, 假装我已经学会了.
---

Subtyping and inheritance are independent (orthogonal) relationships. They may coincide, but none is a special case of the other. In other words, between two types S and T, all combinations of subtyping and inheritance are possible:

1. S is neither a subtype nor a derived type of T
2. S is a subtype but is not a derived type of T
3. S is not a subtype but is a derived type of T
4. S is both a subtype and a derived type of T

The first case is illustrated by independent types, such as Boolean and Float.

The second case can be illustrated by Int32 and Int64; in most object oriented programming languages, Int64 is not derived by inheritance from Int32, however Int64 <: Int32. Since an Int32 value can always be replaced by an Int64 value, the Liskov substitution principle is satisfied; therefore Int64 can be considered a subtype of Int32.

The third case is a consequence of function subtyping input contravariance. Assume a super class of type T having a method m returning an object of the same type (i.e. the type of m is T → T, also note that the first argument of m is this/self) and a derived class type S from T. By inheritance, the type of m in S is S → S. In order for S to be a subtype of T the type of m in S must be a subtype of the type of m in T, in other words: S → S ≤: T → T. By bottom-up application of the function subtyping rule, this means: S ≤: T and T ≤: S, which is only possible if S and T are the same. Since inheritance is an irreflexive relation, S can't be a subtype of T.

Subtyping and inheritance are compatible when all inherited fields and methods of the derived type have types which are subtypes of the corresponding fields and methods from the inherited type

> Classes and types are different things! Java and C# purposely confuse them as a matter of convenience, but you should keep the concepts separate. A class defines an object’s behavior. Subclassing inherits behavior, modifying behavior via extension and override. A type describes what fields an object has and what messages it can respond to. Subtyping is a question of substitutability and what we want to flag as a type error. So try to avoid saying things like, “overriding the method in the supertype” or, “using subtyping to pass an argument of the superclass.” That said, this confusion is understandable in languages where every class declaration introduces a class and a type with the same name.