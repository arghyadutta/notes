#### Notes from Oracle guide of java programming. needed for running realKD and Creedo.
#### Mainz, April 2018

<details>
  
<summary> Not sure if Oracle will sue me for writing this personal notes which has copied text from their tutorial. So here    goes the declaration. #RESPECT_ORACLE </summary>
  
```
 /*
 * Copyright (c) 1995, 2008, Oracle and/or its affiliates. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 *   - Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 *
 *   - Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 *
 *   - Neither the name of Oracle or the names of its
 *     contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
 * IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
 * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
 * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 * SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */
```

</details>

* Java hello world
```
/**
 * The HelloWorldApp class implements an application that
 * simply prints "Hello World!" to standard output.
 */
class HelloWorldApp {
    public static void main(String[] args) {
        System.out.println("Hello World!"); // Display the string.
    }
}
```

Save and compile: Save as `hello.java`. Remember that file names in java are case-sensitive. Then compile using `javac hello.java` and this will create the `hello.class` file which is a bytecode file. Then run it using `java hello`.

`/* text */`: The compiler ignores everything from `/*` to `*/`.  
`/** documentation */`: This indicates a documentation comment (doc comment, for short). The compiler ignores this kind of comment. The javadoc tool uses doc comments when preparing automatically generated documentation.   
`// text` : The compiler ignores everything from `//` to the end of the line.

In the Java programming language, every application must contain a main method whose signature is: `public static void main(String[] args)`.The main method accepts a single argument: an array of elements of type String. This array is the mechanism through which the runtime system passes information to your application. For example: `java MyApp arg1 arg2`
