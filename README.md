Download Link: https://assignmentchef.com/product/solved-cot5930-homework1-fp-concepts
<br>
<h1>Problem 1. FP Concepts</h1>

<ol>

 <li>Referential transparency.

  <ul>

   <li>Explain informally and <strong>with your own words </strong>what referential transparency means. It is silly to say this, but do not copy/paste the definition from the book/note/other sources.</li>

   <li>Give an example of a non-trivial expression that is referential transparent. Explain why it is so using the formal textbook definition. (Just to be sure, do not use the examples from the textbook/notes.</li>

  </ul></li>

</ol>

Not going to repeat this again…)

<ul>

 <li>Give an example of a non-trivial expression that is <strong>not </strong>referential transparent. Explain why it is so using the formal textbook definition.</li>

</ul>

<ol>

 <li>Function purity.

  <ul>

   <li>Explain informally and <strong>with your own words </strong>what a pure function is.</li>

   <li>Give an non-trivial example of a pure function written in Scala. Explain why it is so using the formal textbook definition.</li>

   <li>Give an example of a non-trivial <strong>impure </strong>function written in Scala. Explain why it is so using the formal textbook definition.</li>

  </ul></li>

 <li>Explain why writing pure functions helps us get these advantages:

  <ul>

   <li>composable code and modularity</li>

   <li>simplified testing</li>

  </ul></li>

</ol>

(mention the implications of separation of concerns, made possible by function purity)

<h1>Problem 2. The substitution model</h1>

a)

a.1 Explain with your own words how the substitution model is used for equational reasoning. a.2 Consider this short program:

<table width="665">

 <tbody>

  <tr>

   <td width="665">object p1 {// format a multiline string with product UPC and namedef addProduct(upc: Int, prodName: String, prevProds: String) : String = {     val line = “UPC:%04d Product:%20s”.format(upc, prodName)     prevProds + “
” + line}def main(args: Array[String]): Unit = {     val prod0 = “Apple 2”     val prod1 = “IBM PC”val productLines0 = addProduct(325, prod0, “”)val productLines1 = addProduct(103, prod1, productLines0)// non FP code to display the result:     println(“Products: 
” + productLines1 + “
”)   }</td>

  </tr>

 </tbody>

</table>

}

Use the substitution model to derive the value for variable productLines1. a.3 Explain why function  addProduct is a pure function.

<ol>

 <li>Consider this code:</li>

</ol>

<table width="665">

 <tbody>

  <tr>

   <td width="665">import java.time.LocalDate    // a date class in the local timezone// University Registrar class. class Registrar(val univName: String) {private var allStudents = List[Student]()   // a MUTABLE instance variable// add student to the list of students registered   // Return the number of students already registereddef register(s: Student) : Int = {     allStudents = allStudents :+ s// operator :+ appends something at the end of a list and returns the new list     allStudents.size}def hasRegistered(s: Student) : Boolean = {@annotation.tailrecdef go(lst: List[Student]) : Boolean = {if (lst == Nil) false       else {if (lst.head.name == s.name) true         else go(lst.tail)}     }go(this.allStudents)}}// A student class. class Student(val name:String) {// putting ‘val’ in front of parameter makes name an immutable instance variable   val startedAt : LocalDate = LocalDate.now()}object p2 {   def main(args: Array[String]): Unit = {     val univ = new Registrar(“FAU”)     val alice = new Student(“Alice”)     val bob = new Student(“Bob”)val count1 = univ.register(alice)</td>

  </tr>

  <tr>

   <td width="665">    val count2 = univ.register(bob)     val didBobRegister = univ.hasRegistered(bob)println(“%d students registered”.format(count2))println(“Did Bob register? %b.

”.format(didBobRegister))   }}</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Is expression register(bob) referential transparent ? Explain your answer.</li>

 <li>Is expression hasRegistered(bob) referential transparent ? Explain your answer.</li>

 <li>for 3 points extra credit extra credit    extra credit    extra credit    extra credit    extra credit    Sketch a solution for the student registration part that is pure, i.e. preserves referential transparency. It</li>

</ul>

does not have to be a complete, working program. Use the methodology explained in the textbook/lecture. No need to write Scala code in a separate file.

<h1>Problem 3. Recursion and HOFs</h1>

Write the code for this problem in a file called p3.scala, within an object called <em>p3</em>. a) Consider this function written in a non-functional, imperative style:

<table width="665">

 <tbody>

  <tr>

   <td width="665">  // imperative, impure version:  don’t do like thisdef trueForAll_imperative(bools: List[Boolean]) : Boolean = {     var lst = bools     while (lst != Nil) {       if (! lst.head) {return false             // CAUTION: non-functional, bad programming style to use return}       else {lst = lst.tail}     }     true}</td>

  </tr>

 </tbody>

</table>

Write a <strong>tail recursive pure function </strong>called <em>trueForAll </em>that returns the same values as <em>trueForAll_imperative</em>. Use the correct annotation.

<ol>

 <li>Write a tail-recursive polymorphic function with this signature: def countWithProperty[T](xs: List[T], p: T =&gt; Boolean) : Int that returns the number of elements <em>x</em> from list <em>xs </em>for which <em>p(x)</em> is true.</li>

</ol>

For example:

val luckyNumbers = List(4, 8, 15, 16, 23, 42)

val evenCount = countWithProperty(luckyNumbers, (x: Int) =&gt; x % 2 == 0)

The value of variable <em>evenCount </em>is 4.

<ol>

 <li>Write a tail-recursive polymorphic function with this signature: def scalarProduct(x: Array[Double], y: Array[Double]) : Double that returns the scalar product of arrays x and y.</li>

</ol>

For example:

<table width="665">

 <tbody>

  <tr>

   <td width="665">    val xvec = Array(-1.0, -2, 3)     val yvec = Array(2.0, -3, 1)val prod  = scalarProduct(xvec, yvec)     // prod == 7</td>

  </tr>

 </tbody>

</table>

<ol>

 <li>Write a tail-recursive polymorphic function with this signature: def countCommonElements[T](xs: Array[T], ys: Array[T], p: (T, T) =&gt; Boolean): Int</li>

</ol>

that returns the number of elements <em>x </em>in <em>xs </em>and <em>y </em>in <em>ys</em>, such that p(x, y) is true. This can be used, for example, to count the number of elements in <em>xs </em>that are also in <em>ys</em>:

<table width="665">

 <tbody>

  <tr>

   <td width="665">    val as = Array(7, 3, 8, 4, 9, 3, 5)     val bs = Array(8, -4, 5, 1, 0, 2, 4)val commonNumbers = countCommonElements(as, bs, (x: Int, y: Int) =&gt; x == y)       // commonNumbers ==  3, for 8, 5, 4 are both in as and bs</td>

  </tr>

 </tbody>

</table>

<ol>

 <li>Write a <em>main </em>function in object p3 that illustrates how to use the above functions with anonymous functions. Do not use the example code given in parts a)-d).</li>

</ol>

<strong>Problem 4. Partial application, composition, currying.</strong>

Write the code for this problem in a file called p4.scala, within an object called <em>p4</em>. Add in p4 an empty method <em>main</em>.

<ol>

 <li>Partial function application.

  <ul>

   <li>Write a function <strong><em>partial2</em></strong> that takes as parameters a value <em>a:A</em> and a function <em>f:(A,B,C)=&gt;D,</em> of 3 arguments, and returns as result a function of two arguments that partially applies <em>f</em> to This is an extension of the textbook function <strong><em>partial1 </em></strong>from 2 arguments to 3 arguments.</li>

   <li>Consider this function of three arguments:</li>

  </ul></li>

</ol>




def formatStudentInfo(isGraduate: Boolean, year: Int, name: String) = {     val grad = if (isGraduate) “graduate” else “undergraduate”     “%s student %s enrolled in year %d”.format(grad, name, year)   }

Write code in function <em>main </em>that shows how to obtain a function of 2 parameters using <strong><em>partial2</em></strong> that partially applies <em>formatStudentInfo</em> with parameter <em>isGraduate</em> set to <em>true</em>. Assign the new function to a val called <em>formatGraduateStd</em>. Then write in <em>main </em>code that uses <em>formatGraduateStd </em>with some sample student information and display the resulting string.

(Hint: if this sounds complicated, the problem wants to use <em>partial2</em> in the same way the lecture notes show how to use <em>partial1</em> with a function of 2 arguments called <em>firstNChars</em>.) b) Composition.

<ul>

 <li>Consider these functions that format HTML elements:</li>

</ul>

def htmlTag(elem: String, inner: String) = “&lt;%s&gt;%s&lt;/s&gt;n
”.format(elem, inner, elem)   val mkBold = (inner: String) =&gt; htmlTag(“B”, inner)

Define in object <em>p4’s main </em>method <em> </em>an immutable variable called <em>mkItalic</em> initialized with a lambda expression that is similar to <em>mkBold</em> but instead of returning a boldface &lt;B&gt;…&lt;/B&gt; element (like <em>mkBold</em>) it returns an italic face element, &lt;I&gt;….&lt;/I&gt;.

<ul>

 <li>Define in object <em>p4’s main </em>method an immutable variable called <em>mkBoldItalic</em> initialized with a lambda expression that uses the <em>compose </em>method from trait Function2 and the two lambda expressions, <em>mkBold</em> and <em>mkItalic </em>to format an italic bold font style with the composed element &lt;I&gt;&lt;B&gt;….&lt;B&gt;&lt;/I&gt;.</li>

 <li>Define in object <em>p4’s main </em>method an immutable variable called <em>mkItalicBold</em> initialized with a lambda expression that uses the <em>andThen </em>method from trait Function2 and the two lambda expressions, <em>mkBold</em> and <em>mkItalic </em>to format a bold italic font style with the composed element &lt;B&gt;&lt;I&gt;….&lt;/I&gt;&lt;/B&gt;. c) Currying.</li>

 <li>Write a function <strong><em>curry2</em></strong> that takes as parameters a function <em>f:(A,B,C)=&gt;D,</em> of 3 arguments, and returns as result a function of type <em>A</em> that returns a function of <em>B</em> and <em>C</em> returning <em>D, </em>e. <em>curry2</em> returns type A =&gt; ((B,C) =&gt; D).</li>

</ul>

This is an extension of the textbook function <strong><em>curry  </em></strong>from argument functions with 2 parameters, i.e.

from (<em>A</em>, <em>B</em>) =&gt; <em>C</em> to 3 parameters, <em>(A,B,C)=&gt;D</em>.

In other words, if <em>f</em>’s type is (<em>A,B,C</em>) =&gt; <em>D</em>, then <em>curry2</em>(<em>f</em>) returns a function of type <em>A</em> =&gt; ((<em>B, C</em>) =&gt; <em>D</em>). The function returned from <em>curry2</em>(<em>f</em>) takes an <em>a</em>:<em>A</em> argument and returns a function that partially applies <em>f</em> to <em>a.</em>

Hint: use <em>curry</em>()’s source code given in the lecture notes as a template.

<ul>

 <li>Use the <em>curry2 </em>and <em>formatStudentInfo</em> functions to write in p4’s <em>main </em>method a lambda expression stored in variable <em>mkStdInfo</em> that can be used to partially apply <em>formatStudentInfo</em> with a Boolean parameter, as shown next:</li>

</ul>

val mkStdInfo = curry2(formatStudentInfo) : Boolean =&gt; (Int, String) =&gt; String     val formatGradStdInfo = mkStdInfo(true)   // good for graduate student info

println(formatGradStdInfo(2020, “Harry Potter”))

// displays: graduate student Harry Potter enrolled in year 2020

<ul>

 <li>Use lambda expression <em>mkStdInfo</em> to write in p4’s <em>main </em>method a lambda expression stored in variable <em>formatUndergradStdInfo </em>that can be used to format data for undergraduate students in the same way <em>formatGradStdInfo </em>is used for graduate students. <strong>Problem 5. Traits, objects, and classes.</strong></li>

</ul>

Write the code for this problem in a file called p5.scala, within an object called <em>p5</em>. Add in <em>p5</em> an empty method <em>main</em>.

<ol>

 <li>Write a trait called <em>Shape</em> with two methods returning <em>Double</em>: <em>area</em> and <em>perimeter</em>.</li>

 <li>Write a class called <em>Circle</em> with the appropriate instance variables that extends <em>Shape</em>.</li>

 <li>Write a class called <em>Rectangle</em> with the appropriate instance variables that extends <em>Shape</em>.</li>

 <li>Write code in <em>main</em> variables that uses these classes.</li>

 <li>Initialize in <em>main</em> a variable (val) with an expression that returns an anonymous class implementing <em>Shape</em> that returns a perimeter of value 16.0 and an area 15.0.</li>

</ol>