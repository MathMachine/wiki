## Разработка транслятора

### Лексический анализ

Программа на языке программирования представляет собой последовательность лексем.

В языке программирования C есть 6 типов лексем:

1. идентификаторы;
2. ключевые слова;
3. константы;
4. строки;
5. операции;
6. другие разделители.

Описание этих типов лексем см. в [1].

Задача лексического анализа заключается в том, чтобы в исходной последовательности символов выделить лексемы.

Рассмотрим алгоритм выделения одной лексемы.

Построим диаграмму.

![Рис. 1](/images/translator/fig1.png)

«S» — это начальное состояние, «идентификатор» и «число» — это заключительные состояния.

Пусть текущее состояние — это состояние «S». Если входной символ — буква, то происходит переход в состояние «послед-ть букв и цифр». Если входной символ — цифра, то происходит переход в состояние «послед-ть цифр».

Данная диаграмма позволяет осуществить выделение идентификаторов и целых чисел.

При переходе в заключительное состояние процесс выделения лексемы завершается.

Рассмотренный механизм представляет собой конечный детерминированный автомат.

Теперь займёмся реализацией лексического анализа.

Реализовать данный механизм можно либо при помощи серии ветвлений, либо используя напрямую конечный детерминированный автомат.

Прежде всего, нам понадобятся подходящие типы и структуры данных.

Перечислимый тип ```TokenType``` — тип лексемы.

```cpp
enum TokenType {
  TOKEN_TYPE_END_OF_FILE,
  TOKEN_TYPE_ERROR,
  TOKEN_TYPE_IDENTIFIER_OR_KEYWORD,
  TOKEN_TYPE_INT_CONST,
  TOKEN_TYPE_REAL_CONST,
  TOKEN_TYPE_CHAR_CONST,
  TOKEN_TYPE_STRING_CONST,
  TOKEN_TYPE_OPERATION,
  TOKEN_TYPE_DELIMITER
}
```

Для представления лексемы используем класс ```Token```.

```cpp
class Token {
protected:
  std::string text;
  int line, pos;
public:
  virtual ~Token() {}
  virtual TokenType GetTokenType() const = 0;
  const std::string& Text() const { return text; }
  int Line() const { return line; }
  int Pos() const { return pos; }
};

class Token_end_of_file : public Token {
public:
  TokenType GetTokenType() const {
  return TOKEN_TYPE_END_OF_FILE; }
};

class Token_int_const : public Token {
  int value;
public:
  TokenType GetTokenType() const {
  return TOKEN_TYPE_INT_CONST; }
  int Value() const { return value; }
};
```

В случае реализации конечного детерминированного автомата напрямую необходимо хранить таблицу переходов автомата.


### Синтаксический анализ

Пусть имеется некоторый алфавит — множество символов. Языком называется некоторое множество строк, составленных из символов алфавита.

Для задания языка можно использовать формальную грамматику. Формальная грамматика — это набор правил подстановки. Правило подстановки имеет вид $$u ::= x$$, где $$u$$ — символ, $$x$$ — строка.

В заданной формальной грамматике символы, которые встречаются в левых частях правил подстановки, называются нетерминальными. Остальные символы называются терминальными.

Говорят, что строка $$w$$ непосредственно выводима из строки $$v$$ (пишут: $$v \Rightarrow w$$), если для некоторых строк $$x$$ и $$y$$ можно написать: $$v = xUy$$, $$w = xuy$$, где существует правило подстановки $$U ::= u$$.

Говорят, что $$w$$ выводима из $$v$$ ($$v\Rightarrow\!+\, w$$), если существует последовательность непосредственных выводов $$v = u_0 \Rightarrow u_1 \Rightarrow u_2 \Rightarrow \ldots \Rightarrow u_n = w,\; n > 0$$. Эта последовательность называется выводом.

И наконец, пишут $$v \Rightarrow\! * \, w$$, если $$v \Rightarrow\!+\, w$$ или $$v = w$$.

Заметим, что пока в строке есть хотя бы один нетерминальный символ, из неё можно вывести новую строку. Однако если нетерминальный символ отсутствует, то вывод надо закончить.

Пусть дана строка, состоящая из одних терминальных символов. Задача синтаксического анализа состоит в восстановлении вывода, приводящего к данной строке. Вывод можно наглядно представить синтаксическим деревом.

Формальная грамматика языка программирования C описана в [1].
Рассмотрим алгоритм синтаксического анализа на примере следующей формальной грамматики.

<выражение> ::= <слагаемое> | <слагаемое> + <выражение>

<слагаемое> ::= <множитель> | <множитель> * <слагаемое>

<множитель> ::= число | ( <выражение> )

Для строки `5*(3+7)+2*3` синтаксическое дерево будет следующим.

![Рис. 2](/images/translator/fig2.png)

Как осуществить синтаксический анализ? Из первого правила подстановки видно, что задача разбора выражения сводится к задаче разбора слагаемого. Если после слагаемого идёт +, то следует применить правило подстановки <выражение> ::= <слагаемое> + <выражение>. В противном случае следует применить правило подстановки <выражение> ::= <слагаемое>. Аналогично осуществляется разбор слагаемого.

Для реализации описанного алгоритма удобно использовать рекурсивные функции `ParseExpression()`, `ParseTerm()` и `ParseFactor()`.

Для решения задачи синтаксического анализа программы на языке C, прежде всего, необходимо разработать подходящие типы и структуры данных. Нужно определиться, что должно быть на выходе процедуры синтаксического анализа.

Начнём с представления выражения. Выражение будем представлять в виде дерева, подобного синтаксическому дереву. Для строки `5*(3+7)+2*3` это дерево имеет следующий вид.

![Рис. 3](/images/translator/fig3.png)

Перечислимый тип ```ExprNodeClass``` — тип узла дерева.

```cpp
enum ExprNodeClass {
  EXPR_NODE_CLASS_EXP,
  EXPR_NODE_CLASS_ASSIGNMENT_EXP,
  EXPR_NODE_CLASS_CONDITIONAL_EXP,
  EXPR_NODE_CLASS_BINARY_EXP,
  EXPR_NODE_CLASS_UNARY_EXP,
  EXPR_NODE_CLASS_POSTFIX_EXP,
  EXPR_NODE_CLASS_PRIMARY_EXP
}
```

Узел дерева будет храниться в переменной типа ```ExprNode```.

```cpp
struct ExprNode {
  virtual ~ExprNode() {}
  virtual ExprNodeClass GetExprNodeClass() const = 0;
};

enum BinaryExpClass {
  BINARY_EXP_CLASS_LOGICAL_OR,
  BINARY_EXP_CLASS_LOGICAL_AND,
  BINARY_EXP_CLASS_INCLUSIVE_OR,
  BINARY_EXP_CLASS_EXCLUSIVE_OR,
  BINARY_EXP_CLASS_AND,
  BINARY_EXP_CLASS_EQUALITY,
  BINARY_EXP_CLASS_RELATIONAL,
  BINARY_EXP_CLASS_SHIFT,
  BINARY_EXP_CLASS_ADDITIVE,
  BINARY_EXP_CLASS_MULT,
}

struct BinaryExp : public ExprNode {
  BinaryExpClass binary_exp_class;
  ExprNode* arg1;
  BinaryOperation op;
  ExprNode* arg2;
  BinaryExp(BinaryExpClass, ExprNode*, BinaryOperation,
    ExprNode*);
  ExprNodeClass GetExprNodeClass() const {
    return EXPR_NODE_CLASS_BINARY_EXP; }
};
```

Теперь перейдём к представлению описаний.

Для хранения описаний будем использовать таблицу символов, в которой записываются пары (тип, имя).

Описание включает в себя спецификатор типа и описатель.

Спецификаторы типа: char, int, float, спецификатор структуры, спецификатор перечисления.

Описатель включает в себя идентификатор, определяющий имя переменной. Кроме того, в описателе могут присутствовать описатель указателя, описатель массива и описатель функции.

Рассмотрим тип ```VarType``` — тип переменной.

```
struct VarType {
  TypeSpec* type_spec;
  Declarator declarator;
  VarType();
};

enum TypeSpecClass {
  TYPE_SPEC_CLASS_BASE,
  TYPE_SPEC_CLASS_STRUCT,
  TYPE_SPEC_CLASS_ENUM
}

enum BaseType {
  BASE_TYPE_VOID,
  BASE_TYPE_CHAR,
  BASE_TYPE_INT,
  BASE_TYPE_FLOAT
}

struct TypeSpec {
  virtual ~TypeSpec() {}
  virtual TypeSpecClass GetTypeSpecClass() const = 0;
};

struct BaseTypeSpec : public TypeSpec {
  BaseType base_type;
  BaseTypeSpec(BaseType);
  TypeSpecClass GetTypeSpecClass() const {
    return TYPE_SPEC_CLASS_BASE; }
};

struct StructSpec : public TypeSpec {
  DeclTypeStruct* decl_type_struct;
  /* указатель на описание типа структуры, которое
  хранится в таблице символов */
  StructSpec(DeclTypeStruct*);
  TypeSpecClass GetTypeSpecClass() const {
    return TYPE_SPEC_CLASS_STRUCT; }
};

typedef std::vector<DeclaratorElem*> Declarator;

enum DeclaratorElemClass {
  DECLARATOR_ELEM_CLASS_POINTER,
  DECLARATOR_ELEM_CLASS_ARRAY,
  DECLARATOR_ELEM_CLASS_FUNC
}

struct DeclaratorElem {
  virtual ~DeclaratorElem() {}
  virtual DeclaratorElemClass
  GetDeclaratorElemClass() const = 0;
};

struct DeclaratorElemPointer : public DeclaratorElem {
  bool is_const;
  DeclaratorElemPointer(bool);
  DeclaratorElemClass GetDeclaratorElemClass() const {
    return DECLARATOR_ELEM_CLASS_POINTER; }
};

struct DeclaratorElemArray : public DeclaratorElem {
  //если const_exp отсутствует, то const_exp_value == 0,
  //иначе const_exp_value > 0
  int const_exp_value;
  DeclaratorElemArray(int);
  DeclaratorElemClass GetDeclaratorElemClass() const {
    return DECLARATOR_ELEM_CLASS_ARRAY; }
};
```

Наконец, рассмотрим представление операторов. Тип ```Stat``` — оператор. Тип ```ExpStat``` — оператор-выражение. Тип ```CompoundStat``` — составной оператор.

```
struct Stat {
  virtual ~Stat() {}
};

struct ExpStat : public Stat {
  ExprNode* exp;
};

struct CompoundStat : public Stat {
  SymTableBlock sym_table;
  std::vector<Stat*> stat_list;
};
```

### Список литературы

1. Керниган Б. В., Ричи Д. М. Язык C. [http://lib.ru/CTOTOR/kernigan.txt](http://lib.ru/CTOTOR/kernigan.txt)
