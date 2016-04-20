---
layout: default
title: AIML Standard Library
---

# AIML Standard Library

The following are standard library AIML categories (Github repo: [aimlstandardlibrary.aiml](http://github.com/pandorabots/aiml-utilities)). These include some math, boolean and string operations, and other basic operations that can be used for more complex AIML programming involving SRAI handling of end-user input. Some of these are base operations used by other operations.

In Syntax column, replace {} with actual values. See Example column for input/output result examples.

<table class="table table-striped table-bordered table-condensed">
<tr>
	<th class="col-md-1">Operation</th><th class="col-md-2">Syntax</th><th class="col-md-3">Description</th><th class="col-md-3">Example</th>
</tr>

<tr>
    <td>False</td><td>XFALSE {input}</td><td>Returns FALSE for any input.</td><td><b>INPUT:</b> XFALSE true<br/><b>OUTPUT:</b> FALSE<br/><br/><b>INPUT:</b> XFALSE hello there<br/><b>OUTPUT:</b> FALSE</td>
</tr>
<tr>
    <td>True</td><td>XTRUE {input}</td><td>Returns TRUE for any input.</td><td><b>INPUT:</b> XTRUE false<br/><b>OUTPUT:</b> TRUE<br/><br/><b>INPUT:</b> XTRUE hello there<br/><b>OUTPUT:</b> TRUE</td>
</tr>
<tr>
    <td>Number</td><td>XNUMBER {input}</td>
    <td>Returns the input if it is a number. Otherwise, it will return your bot's UDC response. Limited to positive numbers only.</td>
    <td><b>INPUT:</b> XNUMBER 3<br/><b>OUTPUT:</b> 3<br/><br/><b>INPUT:</b> XNUMBER hello there<br/><b>OUTPUT:</b> I don't have an answer for that.</td>
</tr>
<tr>
    <td>String</td><td>XSTRING {input}</td>
    <td>Returns the input as a normalized string.</td>
    <td><b>INPUT:</b> XSTRING yum@goodeats.com<br/><b>OUTPUT:</b> yum at goodeats dot com<br/><br/><b>INPUT:</b> XSTRING Hello there.<br/><b>OUTPUT:</b> Hello there</td>
</tr>
<tr>
    <td>True if True</td><td>XISTRUE {input}</td><td>Returns TRUE if the input string is true.</td>    <td><b>INPUT:</b> XISTRUE true<br/><b>OUTPUT:</b> TRUE<br/><br/><b>INPUT:</b> XISTRUE 6<br/><b>OUTPUT:</b> FALSE</td>
</tr>

<tr>
    <td>True if False</td><td>XISFALSE {input}</td><td>Returns TRUE if the input string is false.</td>    <td><b>INPUT:</b> XISFALSE true<br/><b>OUTPUT:</b> FALSE<br/><br/><b>INPUT:</b> XISFALSE false<br/><b>OUTPUT:</b> TRUE</td>
</tr>

<tr>
    <td>True if Number</td><td>XISNUMBER {input}</td><td>Returns TRUE if the input string is a number, and FALSE if it is not. Limited to positive integers only.</td>    <td><b>INPUT:</b> XISNUMBER 236<br/><b>OUTPUT:</b> TRUE<br/><br/><b>INPUT:</b> XISNUMBER telegram<br/><b>OUTPUT:</b> FALSE</td>
</tr>

<tr>
    <td>Check Data Type<br/>(Number, String, Boolean)</td><td>XTYPEOF {input}</td><td>Returns datatypes XNUMBER, XSTRING, or XBOOL depending upon the type. Limited to positive integers only.</td><td><b>INPUT:</b> XTYPEOF true<br/><b>OUTPUT:</b> XBOOL<br/><br/><b>INPUT:</b> XTYPEOF Now is the time <br/><b>OUTPUT:</b> XSTRING<br/><br/><b>INPUT:</b> XTYPEOF 34235 <br/><b>OUTPUT:</b> XNUMBER</td>
</tr>

<tr>
    <td>Addition </td><td>XADD {number} XS {number}</td><td>Returns sum of two numbers. Limited to positive integers only.</td><td><b>INPUT:</b> XADD 45 XS 132<br/><b>OUTPUT:</b> 177<br/><br/><b>INPUT:</b> XADD 1 XS 1 <br/><b>OUTPUT:</b> 2</td>
</tr>

<tr>
    <td>Subtraction</td><td>XSUB {number} XS {number}</td><td>Returns difference of two numbers. Limited to positive integers only. Returns 0 if result would be negative.</td><td><b>INPUT:</b> XADD 67 XS 1 <br/><b>OUTPUT:</b> 66<br/><br/><b>INPUT:</b> XADD 45 XS 132<br/><b>OUTPUT:</b> 0<br/></td>
</tr>

<tr>
    <td>Multiplication</td><td>XMUL {number} XS {number}</td><td>Returns product of two numbers. Limited to positive integers only.</td><td><b>INPUT:</b> XMUL 3 XS 5<br/><b>OUTPUT:</b> 15<br/><br/><b>INPUT:</b> XMUL 0 XS 5 <br/><b>OUTPUT:</b> 0</td>
</tr>

<tr>
    <td>Division</td><td>XDIV {number} XS {number}</td><td>Returns the quotient of two numbers. Limited to positive integer values. The decimal value will be truncated (rounded down). Returns infinite if trying to divide by zero.</td><td><b>INPUT:</b> XDIV 11 XS 3<br/><b>OUTPUT:</b> 3<br/><br/><b>INPUT:</b> XDIV 4 XS 0 <br/><b>OUTPUT:</b> infinite</td>
</tr>
<tr>
    <td>Modulo operation</td><td>XMOD {number} XS {number}</td><td>Returns the remainder after division of one number by another. Limited to positive integer values.</td><td><b>INPUT:</b> XMOD 11 XS 3<br/><b>OUTPUT:</b> 2<br/><br/><b>INPUT:</b> XMOD 10 xs 5 <br/><b>OUTPUT:</b> 0</td>
</tr>
<tr>
    <td>Less than</td><td>XLT {number} XS {number}</td><td>Returns TRUE if first number is less than second number. Otherwise, returns FALSE. Limited to positive integer values.</td><td><b>INPUT:</b> xlt 88 xs 123<br/><b>OUTPUT:</b> TRUE<br/><br/><b>INPUT:</b> XLT 10 XS 3 <br/><b>OUTPUT:</b> FALSE</td>
</tr>
<tr>
    <td>Greater than</td><td>XGT {number} XS {number}</td><td>Returns TRUE if first number is greater than second number. Otherwise, returns FALSE. Limited to positive integer values.</td><td><b>INPUT:</b> xgt 88 xs 88<br/><b>OUTPUT:</b> FALSE<br/><br/><b>INPUT:</b> XGT 10 XS 3 <br/><b>OUTPUT:</b> TRUE</td>
</tr>
<tr>
    <td>Less than or Equal to</td><td>XLE {number} XS {number}</td><td>Returns TRUE if first number is less than or equal to second number. Otherwise, returns FALSE. Limited to positive integer values.</td><td><b>INPUT:</b> XLE 44 XS 44<br/><b>OUTPUT:</b> TRUE<br/><br/><b>INPUT:</b> XLE 5 XS 2 <br/><b>OUTPUT:</b> FALSE</td>
</tr>
<tr>
    <td>Greater than or Equal to</td><td>XGE {number} XS {number}</td><td>Returns TRUE if first number is greater than or equal to second number. Otherwise, returns FALSE. Limited to positive integer values.</td><td><b>INPUT:</b> XGE 3 XS 3<br/><b>OUTPUT:</b> TRUE<br/><br/><b>INPUT:</b> XGE 23 XS 582 <br/><b>OUTPUT:</b> FALSE</td>
</tr>
<tr>
    <td>String Concatenation</td><td>XADD {string} XS {string}</td><td>Returns combination of two strings.</td><td><b>INPUT:</b> XADD Betty XS Boop<br/><b>OUTPUT:</b> BettyBoop</td>
</tr>
<tr>
    <td>String Equals</td><td>XEQ {string} XS {string}</td><td>Returns TRUE if first string is the same as second string. Otherwise, returns FALSE. Capitalization is not considered.</td><td><b>INPUT:</b> XEQ john XS John<br/><b>OUTPUT:</b> TRUE<br/><br/><b>INPUT:</b> XEQ fish XS fishing <br/><b>OUTPUT:</b> FALSE</td>
</tr>
<tr>
    <td>String Not Equal</td><td>XNE {string} XS {string}</td><td>Returns TRUE if first string is not the same as second string. Otherwise, returns FALSE. Capitalization is not considered.</td><td><b>INPUT:</b> XNE john XS John<br/><b>OUTPUT:</b> FALSE<br/><br/><b>INPUT:</b> XNE fish XS fishing <br/><b>OUTPUT:</b> TRUE</td>
</tr>
<tr>
    <td>NOT operation</td><td>XNOT {input}</td><td>Returns TRUE if input is false, and vice versa. If input is not boolean, returns FALSE.</td><td><b>INPUT: </b> XNOT true<br/><b>OUTPUT:</b> FALSE<br/><br/><b>INPUT:</b> XNOT false<br/><b>OUTPUT:</b>TRUE</td>
</tr>
<!--
<tr>
    <td>Logical AND</td><td>XAND [ {input} ] XS [ {input} ]</td><td>Returns TRUE if both inputs are true. Otherwise, returns FALSE.</td><td><b>INPUT:</b> <br/><b>OUTPUT:</b> <br/><br/><b>INPUT:</b> XAND [ true ] XS [ false ] <br/><b>OUTPUT:</b> FALSE</td>
</tr>
<tr>
    <td>Logical OR</td><td>XOR [ {input} ] XS [ {input} ]</td><td>Returns FALSE if both inputs are false. Otherwise returns TRUE. </td><td><b>INPUT:</b> <br/><b>OUTPUT:</b> <br/><br/><b>INPUT:</b>  <br/><b>OUTPUT:</b></td>
</tr>
-->
<tr><td>Count characters</td><td>XLENGTH {string}</td><td>Returns number of characters in the string. Note that space characters are not counted, if there are more than one word in the string.</td><td><b>INPUT:</b> XLENGTH hello<br/><b>OUTPUT:</b> 5<br/><br/><b>INPUT:</b> XLENGTH hello there<br/><b>OUTPUT:</b> 10</td></tr>

<tr><td>Random Number</td><td>	XRANDOM	</td><td>	Returns a random single digit number, 0-9 inclusive.	</td><td>	<b>INPUT:</b> XRANDOM<br/><b>OUTPUT:</b> 9	</td></tr>

<tr><td>Extract substring</td><td>	XSUBSTRING {input} XS {number}	</td><td>Returns a substring from the input starting after the first N characters.	</td><td><b>INPUT:</b> XSUBSTRING rosemary XS 4<br/><b>OUTPUT:</b> mary</td></tr>

<tr><td>	Maximum Number	</td><td>XMAX {number} {number} ... {number}	</td><td>	Returns the maximum value from a list of numbers. Limited to positive integer numbers.</td><td>	<b>INPUT:</b> XMAX 10 3 7 2<br/><b>OUTPUT:</b> 10<br/><br/><b>INPUT:</b> XMAX 10 10 <br/><b>OUTPUT:</b> 10	</td></tr>

<tr><td>	First word	</td><td>	XCAR {sentence}	</td><td>	Returns the first word of a string. Limited to a single sentence.</td><td><b>INPUT:</b> XCAR How are you?<br/><b>OUTPUT:</b> How</td></tr>

<tr><td>	Remaining words after first	</td><td>	XCDR {sentence}	</td><td>	Returns the remainder of the words after stripping out the first word. Limited to a single sentence.	</td><td>	<b>INPUT:</b> XCDR How are you?<br/><b>OUTPUT: </b>are you</td></tr>
<tr><td>Concatenate strings</td><td>	XIMPLODE {input1} {input2} ..	</td><td>	Returns a string with input strings combined. Limited to a single sentence.	</td><td><b>INPUT:</b> XIMPLODE hello there stranger<br/><b>OUTPUT:</b> hellotherestranger</td></tr>
<tr><td>Reverse words</td><td>	XREVERSE {string}</td><td>	Returns a string with words in reverse order.	</td><td>	<b>INPUT:</b> XREVERSE parkbench picnic<br/><b>OUTPUT:</b> picnic parkbench<br/><br/><b>INPUT:</b> XREVERSE one two three<br/><b>OUTPUT:</b>	three two one</td></tr>
<tr><td>	NULL	</td><td>	XBLACKHOLE {input}	</td><td>	Returns nothing back in bot response	</td><td>	<b>INPUT:</b> XBLACKHOLE<br/><b>OUTPUT:</b>	</td></tr>
<tr><td>	Output string N times	</td><td>	XLOOP {string} XS {number}	</td><td>	Returns string value concatenated multiple times. Note: does not work if string includes sentence splitting characters.	</td><td>	<b>INPUT:</b> XLOOP bot XS 4<br/><b>OUTPUT:</b> botbotbotbot<br/><br/><b>INPUT:</b>  XLOOP I like you XS 2<br/><b>OUTPUT:</b> I like youI like you	</td></tr>
<tr><td>	Word Count	</td><td>	XCOUNT {string}	</td><td>	Returns number of words in input string. Words are delimited by space and special characters that have been normalized.	</td><td>	<b>INPUT:</b> XCOUNT now is the time<br/><b>OUTPUT:</b> 4<br/><br/><b>INPUT:</b> XCOUNT My email is cup@me.com <br/><b>OUTPUT:</b> 8	</td></tr>
</table>
