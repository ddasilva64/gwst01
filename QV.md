#  QlikView notes
## Introduction
This document isn't a tutorial but is a easy cheatsheet. It contains exemples that you can transform in Excel spreadsheets, input scrpts and images.  
<br>
All of the imagens are obtained by _QlikView Personal Edition_.  
<br>
_Qlik offers a free version of QlikView for personal use. It is meant for individuals, students, or small start-ups. QlikView Personal Edition is the full QlikView Desktop product and uses the same installation package._  
<br>
This Markdown doc it's open to anyone who wants to collaborate, but ever keeping it like an easy cheatsheet.  
<br>
**<u>Note: QlikView it's a trademark in the US and in other countries by Qlik Technologies Inc.</u>**

<p align="center">
  <br><br>
  <img src="https://gwst.eu/wp-content/uploads/2021/01/jo.png">
  <br>
  Daniel da Silva Jarque (author)
</p>  
<br>

## Index
0. [What's the meaning of KISS?](#id0)
1. [Multilanguage Levels](#id1)
2. [Multilanguage Level 1 QlikView sample](#id2)

### What's the meaning of KISS?<a name="id0"></a>
    KISS = Kepp It Simple Sptupid
That's owr philosophy, that's all folks!.<br><br>
### Multilanguage Levels<a name="id1"></a>
    Level 0: Level 0: There aren't no translations in our application.

    Level 1: If you work only in your country market, possibly you won't have more than one brand of product. In this case, you don't need content translation, just tags, messages, and so on.

    Level 2: If you work in several country markets, possibly you will be able to have more than one brand of product. In this case, you need the translation of contents, tags, messages, and so on.    

    Levevel 3: Imagine you live in a bilingual country (like Finland, for exemple). Then you may be able to translate tags, messages, and so on, but not contents. 

If you translate contents, but don't traslate labels, messages and you've only one country market, may be you've a little concept problem.<br><br>
### Multilanguage Level 1 QlikView sample<a name="id2"></a>
In this case we will do a KISS sample of Multilanguage Level 1, in QlikViev.<br><br>
First of all, download for free _**QlikView Personal Edition**_.<br><br>
Second one, make a spreadsheet with extension _**.xlsx**_. You can do that with _**LibreOffice Calc**_ and others.<br><br>

    Book   name       : MultiLanguage.xlsx
    First  spreadsheet: Languages
    Second spreadsheet: Translations
    Third  spreadsheet: Content

**Remember**: Spreadsheet and QlikView application must be at the same folder.<br><br>
**Languages spreadshet Structure:**<br>
| Language | 
| :-----: |
| Catalan |
| Spanish |
| English |

<br>

**Cells rang**: From A1 to A4.<br><br>
**Translations spreadshet Structure:**<br>

| Index | Catalan  | Spanish  | English  |
| :---: | -------: | -------: | -------: |
| 1     | Idioma   | Idioma   | Language |
| 2     | Companyia| Compañía | Company  |
| 3     | Producte | Producto | Product  |
| 4     | Quantitat| Cantidad | Quantity |
| 5     | Preu     | Precio   | Price    |
| 6     | Comanda  | Pedido   | Order    |
| 7     | Sector   | Sector   | Sector   |
| 8     | Data     | Fecha    | Date     |
| 9     | Import   | Importe  | Amount   |
| 10    | Comandes | Pedidos  | Orders   |
| 11    | Nombre de comandes | Número de pedidos  | Number of orders   |
| 12    | Seleccions actuals | Selecciones actuales | Current selecctions |
| 13    | Principal | Principal | Main   |

<br>

**Cells rang**: From A1 to D14.<br><br>
**Content spreadshet Structure:**<br>

| Order | Date      | Company   | Sector  | Product  | Quantity | Price |
| :---: | :-------: | --------: | ------: | -------: | -------: | -------: |
|1|21/02/2021|Catalonia Health robotics|Health robotics|A-001001|123|79,99|
|2|21/02/2021|Catalonia Delivery robotics|Delivery robotics|A-002001|456|49,99|
|3|21/02/2021|Catalonia SAAS|SAAS|A-003001|234|69,99|
|4|21/02/2021|Catalonia Health robotics|Health robotics|A-002001|567|79,99|
|5|21/02/2021|Catalonia Delivery robotics|Delivery robotics|A-002001|123|49,99|

<br>

**Cells rang**: From A1 to G6. Date format is "DD/MM/YYYY".<br><br>


**Create assets**: Image directory <br><br>

| Project forder | subfolder | file |
| :---: | :-------: | :-------- |
|\Multilanguage|||
||\img||||||
|||\catalonia.jpg|
|||\spain.jpg|
|||\uk.jpg|

<br>
**Images**: Download free pictures (54x36 pix or similar) of country flags."<br><br>

![catalonia flag](./MultiLanguage\img/catalonia.jpg)<br>
![spain flag](./MultiLanguage\img/spain.jpg)<br>
![uk flag](./MultiLanguage\img/uk.jpg)<br>

**Script**: Go to File/Script Editor menu, then write: <br><br>
~~~
SET ThousandSep='.';
SET DecimalSep=',';
SET MoneyThousandSep='.';
SET MoneyDecimalSep=',';
SET MoneyFormat='#.###.##0,00 €;(#.###.##0,00 €)';
SET TimeFormat='h:mm:ss';
SET DateFormat='D/M/YYYY';
SET TimestampFormat='D/M/YYYY h:mm:ss[.fff] TT';
SET MonthNames='Jan;Feb;Mar;Apr;May;Jun;Jul;Aug;Sep;Oct;Nov;Des';
SET DayNames='Mon;Tue;Wed;Thu;Fri;Sat;Sun';

Languages:
LOAD Language
FROM
[MultiLanguage.xlsx]
(ooxml, embedded labels, table is [Languages]);

Translations:
LOAD Index, 
     Catalan, 
     English, 
     Spanish
FROM
[MultiLanguage.xlsx]
(ooxml, embedded labels, table is [Translations]);

Orders:
LOAD [Order], 
     Date(Date),  
     Company, 
     Sector, 
     Product, 
     Quantity, 
     Price
FROM
[MultiLanguage.xlsx]
(ooxml, embedded labels, table is [Content]);
~~~

**Variables**: Go to Settings/Varaibale Overview menu, then add:<br><br>
| Variable name | value |
| :--- | :------- | 
|varLanguage|=Language|
|varProduct|=chr(91)&'Product'&chr(95)&'$(vDataLanguage)'&chr(93)|
|varCompany|=chr(91)&'Company'&chr(95)&'$(vDataLanguage)'&chr(93)|
|varSector|=chr(91)&'Sector'&chr(95)&'$(vDataLanguage)'&chr(93)|

<br>

~~~
chr(91)="[" (opening bracket)
chr(93)="_" (underscore)
chr(95)="]" (closing bracket)
~~~

<br>

**Sheet objects**: Go to Main sheet, then add (rigth mouse button):<br><br>

***Text objects***: Locate 3 ones in the same position, for exemple top left of the screen.<br><br>
****Add text object, then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Background picture|catalonia.jpg|
|Actions|Field|Language|
|Actions|String text search|='Catalan'|

<br><br>

****Add text object, then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Background picture|spain.jpg|
|Actions|Field|Language|
|Actions|String text search|='Spanish'|

<br><br>

****Add text object, then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Background picture|uk.jpg|
|Actions|Field|Language|
|Actions|String text search|='English'|

<br><br>

****Add list box object, then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Caption|=Only({<Index={1}>} [$(=varLanguage)])|
|Caption|Show caption check box|marked|

<br>

Tray to change languge in list box, then change flag picture.   
<br>


****Change sheet object (ritgh mouse button), then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Caption|=Only({<Index={13}>} [$(=varLanguage)])|
|Fields|Language|select|
|Fields|Order|select|

<br><br>

This is the current sheet object. So when you change language, also change caption current tab sheet.   
<br>

****Add list box object, then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Caption|=Only({<Index={6}>}[$(=varLanguage)])|
|Caption|Show caption check box|marked|

<br>

This is the order list box, comming soon we see efect. So when you change language, also change caption list box.   
<br>

****Add list box object, then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Caption|=Only({<Index={2}>} [$(=varLanguage)])|
|Caption|Show caption check box|marked|

<br><br>

This is the company list box, comming soon we see efect. So when you change language, also change caption list box.   
<br>

****Add list box object, then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Caption|=Only({<Index={7}>} [$(=varLanguage)])|
|Caption|Show caption check box|marked|

<br><br>

This is the sector list box, comming soon we see efect. So when you change language, also change caption list box, well, anyway it's the same in all three languages.   
<br>

****Add list box object, then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Caption|=Only({<Index={3}>} [$(=varLanguage)])|
|Caption|Show caption check box|marked|

<br><br>

This is the product list box, comming soon we see efect. So when you change language, also change caption list box.   
<br>

****Add current selecton box object, then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Caption|=Only({<Index={12}>} [$(=varLanguage)])|
|Caption|Show caption check box|marked|

<br><br>

This is the current selecton box, comming soon we see efect. So when you change language, also change caption current selection box. If you change anywhere, you will see changes in this box.   
<br>


****Add graph object, then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Window Caption|=Only({<Index={11}>} [$(=varLanguage)])|
|General|Simple Table check box|marked|
|Dimensions|Date(Date)|selected|
|Dimensions|Label Caption|=Only({<Index={8}>} [$(=varLanguage)])|
|Dimensions|Order|selected|
|Dimensions|Label Caption|=Only({<Index={6}>} [$(=varLanguage)])|
|Dimensions|Sector|selected|
|Dimensions|Label Caption|=Only({<Index={7}>} [$(=varLanguage)])|
|Dimensions|Company|selected|
|Dimensions|Label Caption|=Only({<Index={2}>} [$(=varLanguage)])|
|Dimensions|Product|selected|
|Dimensions|Label Caption|=Only({<Index={3}>} [$(=varLanguage)])|
|Expressions|Add|Quantity (definition)|
|Expressions|Label Caption|=Only({<Index={4}>} [$(=varLanguage)])|
|Expressions|Total mode, without totals |off|
|Expressions|Total mode, total expression |off|
|Expressions|Total mode, expression combo |addition|
|Expressions|Add|Price (definition)|
|Expressions|Label Caption|=Only({<Index={5}>} [$(=varLanguage)])|
|Expressions|Total mode, without totals |on|
|Expressions|Total mode, total expression |off|
|Expressions|Total mode, expression combo |off|
|Expressions|Add|Sum(Price)*Sum(Quantity) (definition)|
|Expressions|Label Caption|=Only({<Index={9}>} [$(=varLanguage)])|
|Expressions|Total mode, without totals |off|
|Expressions|Total mode, total expression |off|
|Expressions|Total mode, expression combo |addition|
|Sort|Sort sequence|6, 8, 4, 5, 9, 7, 2, 3|
|Presentation|8=Date|All align to the center|
|Presentation|6=Order|All align to the center|
|Presentation|7=Sector|All align to the left|
|Presentation|2=SCompany|All align to left|
|Presentation|3=Product|All align to the center|
|Presentation|4=Quantity|All align to the rigth|
|Presentation|5=Price|All align to the rigth|
|Presentation|9=Amount|All align to the rigth|
|Style|Style|Table 1|
|Number|4=Quantity|numeric format|
|Number|5=Price|currency format|
|Number|9=Amount|currency format|
<br><br>

This is our first graph box, but the behaviour of it is like a table. The reason is because marked Simple Table check box. 

Be attenton to put dimensions in the same order like the table, please. 

When you fill dimensions do click on the button with a sigma botton (Quick change tip text), then system fill the rows with first data.

In expresions tab we add calculations in our table (quantity, price and amount).

In alignation consider only label, text data and numeric data options.

<br>

****Add graph object, then add properties:****<br><br>
| Tab |Property | Value |
| :--- | :--- | :------- | 
|General|Object ID|default|
|General|Window Caption|=Only({<Index={11}>} [$(=varLanguage)])|
|General|Graph Bar check box|marked|
|Dimensions|Company|selected|
|Dimensions|Label Caption|=Only({<Index={2}>} [$(=varLanguage)])|
|Expressions|Add|Count(Order) (definition)|
|Expressions|Label Caption|=Only({<Index={10}>} [$(=varLanguage)])|
|Expressions|Values over data |on|
<br><br>

In this case we show a graph barr, indicating number of orders by company.

And that's all folks!

<br>

![Catalan](./MultiLanguage\assets/QV001.png)<br>
Results in Catalan language.   
<br>
![Spanish](./MultiLanguage\assets/QV002.png)<br>
Results in Spanish language.   
<br>
![English](./MultiLanguage\assets/QV003.png)<br>
Results in English language.   
<br>
Now try to do it yourself. It's easy, it's KISS ;-).