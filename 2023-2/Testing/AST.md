Abstract Syntax Tree, propio a cada lenguaje por ejemplo python: [AST python][https://docs.python.org/3/library/ast.html]

```python
from ast import *
import ast

tree = parse("2+3")

print(ast.dump(tree,indent=3))
```

Permite ver el ast de esa operación

Muestra el body, el cual contiene una expresión.

![[Drawing 2023-08-22 16.19.29.excalidraw]]
Util para hacer analisis estatico de un codigo.

Podemos sobrescribir el Visitor para hacer un analisis en ciertos tipos de nodos:

```python
from _ast import Call, ClassDef, Expr, FunctionDef
from ast import *
import ast
from typing import Any

class FunctionPrinterVisitor(NodeVisitor):

	def __init__(self) -> None:
		self.vio_super = False
		super().__init__()
	
	def visit_Call(self, node: Call) -> Any:
		NodeVisitor.generic_visit(self, node)
		if isinstance(node.func, Name):
			if node.func.id == "super":
			self.vio_super = True

	def visit_ClassDef(self, node: ClassDef) -> Any:
		if not node.bases:
			return
		else:
			for x in node.body:
			print(x.lineno)
			NodeVisitor.generic_visit(self, node)
			if not self.vio_super:
				print("super init is not called")

visitor = FunctionPrinterVisitor()
visitor.visit(parse(sourceCode1))
```


